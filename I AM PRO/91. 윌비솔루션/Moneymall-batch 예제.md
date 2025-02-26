---
tags:
  - jcascalog
Created: Invalid date
Updated: Invalid date
---
package com.shinsegae.moneymall.mr.analytics;

import java.text.SimpleDateFormat;

import java.util.ArrayList;

import java.util.HashMap;

import java.util.Iterator;

import java.util.List;

import java.util.Map;

import java.util.Map.Entry;

import jcascalog.Api;

import jcascalog.Subquery;

import org.apache.avro.Schema;

import org.apache.hadoop.conf.Configuration;

import org.apache.hadoop.conf.Configured;

import org.apache.hadoop.fs.FileStatus;

import org.apache.hadoop.fs.FileSystem;

import org.apache.hadoop.fs.Path;

import org.apache.hadoop.util.Tool;

import org.joda.time.DateTime;

import org.joda.time.DateTimeUtils;

import cascading.avro.ParquetScheme;

import cascading.flow.FlowProcess;

import cascading.operation.AggregatorCall;

import cascading.operation.FunctionCall;

import cascading.operation.OperationCall;

import cascading.scheme.hadoop.TextDelimited;

import cascading.tap.MultiSourceTap;

import cascading.tap.Tap;

import cascading.tap.hadoop.Hfs;

import cascading.tuple.Fields;

import cascading.tuple.Tuple;

import cascalog.CascalogAggregator;

import cascalog.CascalogFunction;

import com.shinsegae.moneymall.util.HadoopConfiguration;

public class AnalyticsIfOrderViewEvent extends Configured implements Tool {

private static final String AVRO_INPUT_SCHEMA = "/META-INF/avro/order-view-event.avsc";

private String tmpJars;

public void setTmpJars(String tmpJars) {

this.tmpJars = tmpJars;

}

public int run(String[] args) throws Exception {

Configuration hadoopConf = this.getConf();

String inputPath = args[0];

String outputPath = args[1];

int daysNum = 30;

// m/r compression.

HadoopConfiguration.setMapOutputSnappyCompression(hadoopConf, true);

HadoopConfiguration.setJobOutputLzopCompression(hadoopConf, false);

this.getConf().set("[mapred.job.name](http://mapred.job.name/)", "AnalyticsIfOrderViewEvent");

if (this.tmpJars != null) {

this.getConf().set("tmpjars", this.tmpJars);

}

Map<String, String> confMap = new HashMap<String, String>();

Iterator<Entry<String, String>> iter = hadoopConf.iterator();

while (iter.hasNext()) {

Entry<String, String> entry = iter.next();

confMap.put(entry.getKey(), entry.getValue());

}

// set from / to time range.

Api.setApplicationConf(confMap);

// first, delete the output path.

FileSystem fs = FileSystem.get(hadoopConf);

fs.delete(new Path(outputPath), true);

/*

* 날짜 계산

*/

ArrayList<String> pathList = new ArrayList<>();

int cnt=0;

String startDate = "";

long to = DateTimeUtils.currentTimeMillis();

DateTime dt = new DateTime(to);

SimpleDateFormat formatDate = new SimpleDateFormat("yyyy-MM-dd");

// 데이터 소스 경로

while(cnt < daysNum) {

DateTime dtime = new DateTime(dt);

long fromday_long = dtime.minusDays(++cnt).getMillis();

startDate = formatDate.format(fromday_long);

String inputDir = inputPath + "/" + startDate;

// check if input path exists.

FileStatus[] status = fs.listStatus(new Path(inputDir));

if (status == null) {

System.out.println("input path [" + inputDir + "] does not exist! / ");

continue; //item-view-evnet는 30일이 아직 들어오지 않았음

}

pathList.add(inputDir);

}

// 사용할 데이터의 스키마 : 분석&설계 > 운영계 Tracking Logging 요소 정의 > 1

String[] inputFields = new String[] {"!baseProperties", "!subOrderItemList", "!ordNo"};

String[] outputFields = new String[] {"!mbrId", "!itemId", "!ordQty"};

final Schema inputSchema = new Schema.Parser().parse(getClass()

.getResourceAsStream(AVRO_INPUT_SCHEMA));

ParquetScheme inputScheme = new ParquetScheme(inputSchema);

inputScheme.setSourceFields(new Fields(inputFields));

// file extension 에 맞는 file 중 time range 에 포함된 path 추가. default file

// extension 은 'avro'.

if (pathList.size() == 0) {

System.err.println("No Path found as sources!");

return -1;

}

Tap[] sources = new Tap[pathList.size()];

int i = 0;

for(String path : pathList) {

sources[i++] = new Hfs(inputScheme, path);

System.out.println(path);

}

MultiSourceTap multiSourceTap = new MultiSourceTap(sources);

Tap outputTap = new Hfs(new TextDelimited(false, "\t", "\""), outputPath);

Subquery baseQuery = new Subquery(outputFields)

.predicate(multiSourceTap, inputFields)

.predicate(new Flatten(), inputFields)

.out(outputFields);

Subquery sumQuery = new Subquery("!mbrId", "!itemId", "!itemSumQty")

.predicate(baseQuery, outputFields)

.predicate(new SumAggregator(), "!ordQty")

.out("!itemSumQty");

Api.execute(outputTap, sumQuery);

return 0;

}

public static class Flatten extends CascalogFunction {

@Override

public void operate(FlowProcess flow_process, FunctionCall fnCall) {

Tuple basePropertiesTuple = (Tuple) fnCall.getArguments().getObject(0);

List<Tuple> subOrderItemList = (List<Tuple>) fnCall.getArguments().getObject(1);

for(Tuple subOrderItem : subOrderItemList) {

// unitPrice > 0

//if(Integer.parseInt(subOrderItem.getString(4)) <= 0) continue;

fnCall.getOutputCollector().add(

new Tuple(

basePropertiesTuple.getString(5), // mbrId

subOrderItem.getString(1), // itemid

subOrderItem.getString(3) // ordQty

)

);

}

}

}

public static class SumAggregator extends CascalogAggregator

{

private long itemSumQty;

@Override

public void prepare(FlowProcess flowProcess, OperationCall operationCall) {

}

@Override

public void start(FlowProcess flowProcess, AggregatorCall aggregatorCall) {

itemSumQty = 0;

}

@Override

public void aggregate(FlowProcess fp, AggregatorCall ac) {

int ordQty = ac.getArguments().getString(0)==null ? 0 : Integer.parseInt(ac.getArguments().getString(0));

itemSumQty = itemSumQty + ordQty;

}

@Override

public void complete(FlowProcess flowProcess, AggregatorCall aggregatorCall) {

aggregatorCall.getOutputCollector().add(

new Tuple(

itemSumQty

));

}

}

}