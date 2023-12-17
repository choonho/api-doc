---
title: "CloudServiceStats"
linkTitle: "CloudServiceStats"
weight: 3
bookFlatSection: true
---
# [CloudServiceStats](#CloudServiceStats)
A CloudServiceStats is statistics data created from from cloud service query sets.


>  **Package : spaceone.api.inventory.v1**

<br>
<br>

## CloudServiceStats





**CloudServiceStats Methods:**


| Method | Request | Response |
| :----- | :-------- | :-------- |
| [**list**](./CloudServiceStats#list) | [CloudServiceStatsQuery](CloudServiceStats#cloudservicestatsquery) | [CloudServiceStatsInfo](CloudServiceStats#cloudservicestatsinfo) |
| [**analyze**](./CloudServiceStats#analyze) | [CloudServiceStatsAnalyzeQuery](CloudServiceStats#cloudservicestatsanalyzequery) | [Struct](CloudServiceStats#struct) |
| [**stat**](./CloudServiceStats#stat) | [CloudServiceStatsStatQuery](CloudServiceStats#cloudservicestatsstatquery) | [Struct](CloudServiceStats#struct) |



    
<br>

### list

Gets a list of raw statistics data.
You can use a query to get a filtered list of statistics data.



> **POST** /inventory/v1/cloud-service-stats/list
>





 {{< tabs " list " >}}

 {{< tab "Request Example" >}}



[CloudServiceStatsQuery](./CloudServiceStats#cloudservicestatsquery)

* **query_set_id** (string)   `Required` 


* **query** (Query)  


* **provider** (string)  


* **cloud_service_group** (string)  


* **cloud_service_type** (string)  


* **region_code** (string)  


* **account** (string)  


* **workspace_id** (string)  


* **project_id** (string)  





{{< highlight json >}}
{
   "query": <SearchQuery>,
   "query_set_id": "query-set-abcd1234",
   "provider": "aws",
   "cloud_service_group": "EC2",
   "cloud_service_type": "Instance",
   "region_code": "us-east-1",
   "account": "aws-account-id",
   "project_id": "project-abcd1234"
}
{{< /highlight >}}
{{< /tab >}}


 {{< tab "Response Example" >}}

[CloudServiceStatsInfo](#CLOUDSERVICESTATSINFO)
* **results** (CloudServiceStatInfo)  `Repeated`   `Required` 

* **total_count** (int32)   `Required` 



{{< highlight json >}}
{
   "results": [
       {
           "query_set_id": "query-set-abcd1234",
           "key": "Disk Size",
           "values": {
               "Disk Size": 1040,
               "Memory Size": 1024,
               "CPU": 2
           },
           "unit": {
               "Disk Size": "GB",
               "Memory": "GB",
               "CPU": "Core"
           },
           "provider": "aws",
           "cloud_service_group": "EC2",
           "cloud_service_type": "Instance",
           "region_code": "us-east-1",
           "account": "aws-account-id",
           "additional_info": {
               "instance_type": "t2.micro"
           },
           "project_id": "project-abcd1234",
           "domain_id": "domain-58010aa2e451",
           "created_date": "2022-06-22"
       },
       {...}
   ],
   "total_count": 2
}
{{< /highlight >}}
{{< /tab >}}


{{< /tabs >}}


    
<br>

### analyze





> **POST** /inventory/v1/cloud-service-stats/analyze
>






    
<br>

### stat





> **POST** /inventory/v1/cloud-service-stats/stat
>






    


<br>
<br>

## Message



### CloudServiceStatInfo
* **query_set_id** (string)   `Required` 

    
* **values** (Struct)   `Required` 

    
* **unit** (Struct)   `Required` 

    
* **provider** (string)   `Required` 

    
* **cloud_service_group** (string)   `Required` 

    
* **cloud_service_type** (string)   `Required` 

    
* **region_code** (string)   `Required` 

    
* **account** (string)   `Required` 

    
* **additional_info** (Struct)   `Required` 

    
* **domain_id** (string)   `Required` 

    
* **workspace_id** (string)   `Required` 

    
* **project_id** (string)   `Required` 

    
* **created_date** (string)   `Required` 

    <br>

### CloudServiceStatsAnalyzeQuery
* **query** (TimeSeriesAnalyzeQuery)   `Required` 

    
* **query_set_id** (string)   `Required` 

    <br>

### CloudServiceStatsInfo
* **results** (CloudServiceStatInfo)  `Repeated`    `Required` 

    
* **total_count** (int32)   `Required` 

    <br>

### CloudServiceStatsQuery
* **query_set_id** (string)   `Required` 

    
* **query** (Query)  

    
* **provider** (string)  

    
* **cloud_service_group** (string)  

    
* **cloud_service_type** (string)  

    
* **region_code** (string)  

    
* **account** (string)  

    
* **workspace_id** (string)  

    
* **project_id** (string)  

    <br>

### CloudServiceStatsStatQuery
* **query** (StatisticsQuery)   `Required` 

    
* **query_set_id** (string)  

    <br>
