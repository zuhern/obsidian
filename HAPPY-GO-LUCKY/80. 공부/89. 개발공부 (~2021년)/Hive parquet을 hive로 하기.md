---
Created: Invalid date
Updated: Invalid date
---
## [https://cwiki.apache.org/confluence/display/Hive/Parquet](https://cwiki.apache.org/confluence/display/Hive/Parquet)

## **Hive QL Syntax**

A [CREATE TABLE](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+DDL#LanguageManualDDL-CreateTable) statement can specify the Parquet storage format with syntax that depends on the Hive version.

### Hive 0.10 - 0.12

CREATE TABLE parquet_test ( id int, str string, mp MAP<STRING,STRING>, lst ARRAY<STRING>, strct STRUCT<A:STRING,B:STRING>)  
PARTITIONED BY (part string)  
ROW FORMAT SERDE 'parquet.hive.serde.ParquetHiveSerDe' STORED AS INPUTFORMAT 'parquet.hive.DeprecatedParquetInputFormat' OUTPUTFORMAT 'parquet.hive.DeprecatedParquetOutputFormat';  

### Hive 0.13 and later

CREATE TABLE parquet_test ( id int, str string, mp MAP<STRING,STRING>, lst ARRAY<STRING>, strct STRUCT<A:STRING,B:STRING>)  
PARTITIONED BY (part string)  
STORED AS PARQUET;