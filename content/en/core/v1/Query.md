---
title: "Query"
linkTitle: "Query"
weight: 3
bookFlatSection: true
---
# [Query](#Query)



>  **Package : spaceone.api.core.v1**

<br>
<br>

## Query







<br>
<br>

## Message



### AggregateCount
* **name** (string)   `Required` 

    <br>

### AggregateGroup
* **keys** (AggregateGroupKey)  `Repeated`    `Required` 

    
* **fields** (AggregateGroupField)  `Repeated`    `Required` 

    <br>

### AggregateGroupField
* **key** (string)   `Required` 

    
* **k** (string)   `Required` 

    
* **name** (string)   `Required` 

    
* **n** (string)   `Required` 

    
* **operator** (string)   `Required` 

    
* **o** (string)   `Required` 

    
* **fields** (AggregateGroupSubField)  `Repeated`    `Required` 

    
* **conditions** (AggregateSubCondition)  `Repeated`    `Required` 

    <br>

### AggregateGroupKey
* **key** (string)   `Required` 

    
* **k** (string)   `Required` 

    
* **name** (string)   `Required` 

    
* **n** (string)   `Required` 

    
* **date_format** (string)   `Required` 

    <br>

### AggregateGroupSubField
* **key** (string)   `Required` 

    
* **k** (string)   `Required` 

    
* **name** (string)   `Required` 

    
* **n** (string)   `Required` 

    <br>

### AggregateProject
* **fields** (AggregateProjectField)  `Repeated`    `Required` 

    
* **exclude_keys** (bool)   `Required` 

    <br>

### AggregateProjectField
* **key** (string)   `Required` 

    
* **k** (string)   `Required` 

    
* **name** (string)   `Required` 

    
* **n** (string)   `Required` 

    
* **operator** (string)   `Required` 

    
* **o** (string)   `Required` 

    <br>

### AggregateSort
* **key** (string)   `Required` 

    
* **desc** (bool)   `Required` 

    
* **keys** (SortKey)  `Repeated`    `Required` 

    <br>

### AggregateSubCondition
* **key** (string)   `Required` 

    
* **k** (string)   `Required` 

    
* **value** (Value)   `Required` 

    
* **v** (Value)   `Required` 

    
* **operator** (string)   `Required` 

    
* **o** (string)   `Required` 

    <br>

### AggregateUnwind
* **path** (string)   `Required` 

    <br>

### AnalyzeQuery
* **group_by** (string)  `Repeated`    `Required` 

    
* **field_group** (string)  `Repeated`    `Required` 

    
* **filter** (Filter)  `Repeated`    `Required` 

    
* **filter_or** (Filter)  `Repeated`    `Required` 

    
* **page** (Page)   `Required` 

    
* **sort** (SortKey)  `Repeated`    `Required` 

    
* **fields** (Struct)   `Required` 

    
* **select** (Struct)   `Required` 

    
* **keyword** (string)   `Required` 

    <br>

### ExportAnalyzeQuery
* **filter** (Filter)  `Repeated`    `Required` 

    
* **filter_or** (Filter)  `Repeated`    `Required` 

    
* **keyword** (string)   `Required` 

    
* **sort** (SortKey)  `Repeated`    `Required` 

    
* **group_by** (string)  `Repeated`    `Required` 

    
* **fields** (Struct)   `Required` 

    
* **select** (Struct)   `Required` 

    <br>

### ExportOption
* **name** (string)   `Required` 

    
* **query_type** (QueryType)   `Required` 

    
* **search_query** (ExportSearchQuery)   `Required` 

    
* **analyze_query** (ExportAnalyzeQuery)   `Required` 

    <br>

### ExportSearchQuery
* **filter** (Filter)  `Repeated`    `Required` 

    
* **filter_or** (Filter)  `Repeated`    `Required` 

    
* **keyword** (string)   `Required` 

    
* **sort** (SortKey)  `Repeated`    `Required` 

    
* **fields** (ListValue)   `Required` 

    <br>

### Filter
* **key** (string)   `Required` 

    
* **k** (string)   `Required` 

    
* **value** (Value)   `Required` 

    
* **v** (Value)   `Required` 

    
* **operator** (string)   `Required` 

    
* **o** (string)   `Required` 

    <br>

### Page
* **start** (uint32)   `Required` 

    
* **limit** (uint32)   `Required` 

    <br>

### Query
* **filter** (Filter)  `Repeated`    `Required` 

    
* **filter_or** (Filter)  `Repeated`    `Required` 

    
* **sort** (Sort)   `Required` 

    
* **page** (Page)   `Required` 

    
* **minimal** (bool)   `Required` 

    
* **count_only** (bool)   `Required` 

    
* **only** (string)  `Repeated`    `Required` 

    
* **keyword** (string)   `Required` 

    <br>

### Sort
* **key** (string)   `Required` 

    
* **desc** (bool)   `Required` 

    
* **keys** (SortKey)  `Repeated`    `Required` 

    <br>

### SortKey
* **key** (string)   `Required` 

    
* **desc** (bool)   `Required` 

    <br>

### StatisticsAggregate
* **unwind** (AggregateUnwind)   `Required` 

    
* **group** (AggregateGroup)   `Required` 

    
* **count** (AggregateCount)   `Required` 

    
* **sort** (AggregateSort)   `Required` 

    
* **project** (AggregateProject)   `Required` 

    
* **limit** (int32)   `Required` 

    
* **skip** (int32)   `Required` 

    <br>

### StatisticsQuery
* **filter** (Filter)  `Repeated`    `Required` 

    
* **filter_or** (Filter)  `Repeated`    `Required` 

    
* **aggregate** (StatisticsAggregate)  `Repeated`    `Required` 

    
* **page** (Page)   `Required` 

    
* **distinct** (string)   `Required` 

    
* **keyword** (string)   `Required` 

    <br>

### TimeSeriesAnalyzeQuery
* **granularity** (Granularity)   `Required` 

    
* **start** (string)   `Required` 

    
* **end** (string)   `Required` 

    
* **group_by** (string)  `Repeated`    `Required` 

    
* **field_group** (string)  `Repeated`    `Required` 

    
* **filter** (Filter)  `Repeated`    `Required` 

    
* **filter_or** (Filter)  `Repeated`    `Required` 

    
* **page** (Page)   `Required` 

    
* **sort** (SortKey)  `Repeated`    `Required` 

    
* **fields** (Struct)   `Required` 

    
* **select** (Struct)   `Required` 

    
* **keyword** (string)   `Required` 

    <br>
