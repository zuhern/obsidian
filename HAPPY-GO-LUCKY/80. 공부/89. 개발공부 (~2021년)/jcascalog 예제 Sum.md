---
Created: Invalid date
Updated: Invalid date
---
SUM ////////////////////////////////////////////////////////////////////////////////////////

Subquery baseQuery = new Subquery(outputFields)  
.predicate(multiSourceTap, inputFields)  
.predicate(new Flatten(), inputFields)  
.out(outputFields);// aggregator에 적지 않은 인자들로 Group by 된다  
Subquery sumQuery = new Subquery("!mbrId", "!itemId", "!itemSumQty")  
.predicate(baseQuery, outputFields)  
.predicate(new SumAggregator(), "!ordQty")  
.out("!itemSumQty  

”

);

public static class SumAggregator extends CascalogAggregator  
{private long itemSumQty;@Overridepublic void prepare(  
FlowProcess flowProcess, OperationCall operationCall) {  
}@Overridepublic void start(  
FlowProcess flowProcess, AggregatorCall aggregatorCall) {itemSumQty = 0;  
}@Overridepublic void aggregate(  
FlowProcess fp, AggregatorCall ac) {int ordQty = ac.getArguments().getString(0)==null ? 0 : Integer.parseInt(ac.getArguments().getString(0));itemSumQty = itemSumQty + ordQty;  
}@Overridepublic void complete(  
FlowProcess flowProcess, AggregatorCall aggregatorCall) {  
aggregatorCall.getOutputCollector().add(new Tuple(itemSumQty  
));  
}  
}  

/////////////////////////////////////////////////////////////////////////////////////////////