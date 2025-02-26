---
Created: Invalid date
Updated: Invalid date
---
package com.shinsegae.moneymall.mr.analytics;

import java.util.ArrayList;

import java.util.List;

import jcascalog.Api;

import jcascalog.Subquery;

import org.junit.Before;

import org.junit.Test;

import cascading.flow.FlowProcess;

import cascading.operation.AggregatorCall;

import cascading.operation.OperationCall;

import cascading.tuple.Tuple;

import cascalog.CascalogAggregator;

import com.twitter.maple.tap.StdoutTap;

public class AnalyticsIfOrderViewEventStubTestSkip {

@Before

public void init() {

}

private List generateOrderViewEvent() {

List orderViewEvent = new ArrayList();

//-------------------------------------

List subList = new ArrayList();

subList.add("1"); // mbr_id

subList.add("2"); // itemId

subList.add("1"); // ordQty

orderViewEvent.add(subList);

//--------------------------------------

//-------------------------------------

subList = new ArrayList();

subList.add("1"); // mbr_id

subList.add("2"); // itemId

subList.add("2"); // ordQty

orderViewEvent.add(subList);

//--------------------------------------

//-------------------------------------

subList = new ArrayList();

subList.add("2"); // mbr_id

subList.add("2"); // itemId

subList.add("10"); // ordQty

orderViewEvent.add(subList);

//--------------------------------------

//-------------------------------------

subList = new ArrayList();

subList.add("2"); // mbr_id

subList.add("2"); // itemId

subList.add("12"); // ordQty

orderViewEvent.add(subList);

//--------------------------------------

//-------------------------------------

subList = new ArrayList();

subList.add("1"); // mbr_id

subList.add("3"); // itemId

subList.add("5"); // ordQty

orderViewEvent.add(subList);

//--------------------------------------

//-------------------------------------

subList = new ArrayList();

subList.add("1"); // mbr_id

subList.add("3"); // itemId

subList.add("6"); // ordQty

orderViewEvent.add(subList);

//--------------------------------------

return orderViewEvent;

}

@Test

public void run() {

String[] inputFields = new String[] {"!mbrId", "!itemId", "!ordQty"};

List orderViewTab = generateOrderViewEvent();

Subquery sumQuery = new Subquery("!mbrId", "!itemId", "!itemSumQty")

.predicate(orderViewTab, inputFields)

.predicate(new SumAggregator(), "!ordQty")

.out("!itemSumQty");

Api.execute(new StdoutTap(), sumQuery);

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