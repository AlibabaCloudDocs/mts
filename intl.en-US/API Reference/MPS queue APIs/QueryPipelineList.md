# QueryPipelineList {#reference_owd_vnt_x2b .reference}

The QueryPipelineList API queries MPS queues and returns the name and status of the specified MPS queues.

## Request parameters {#section_iqn_qbt_x2b .section}

|Parameters|Type|Required or not|Description|
|:---------|:---|:--------------|:----------|
|Action|String|Yes|API of the action, system required parameter. Value: QueryPipelineList|
|PipelineIds|String|Yes|MPS queue list.Query up to 10 at a time, separated by a comma.

|

## List of non-existing MPS queue IDs. If no data exists, this structure is not returned. {#section_ogh_wbt_x2b .section}

|Return parameters|Type|Description|
|:----------------|:---|:----------|
|PipelineList|AliyunPipeline\[ \]|MPS queue list|
|NonExistPids|String\[ \]|List of non-existing MPS queue IDs. If no data exists, this structure is not returned.|

## Examples {#section_gpq_zbt_x2b .section}

Request example

```
http://mts.cn-hangzhou.aliyuncs.com/?PipelineIds=31fa3c9ca8134f9cec2b4b0b0f787830&Action=QueryPipelineList&<Public parameter>
```

Response example

XML

```
<QueryPipelineListResponse>
<RequestId>25818875-5F78-4A13-BEF6-D7393642CA58</RequestId>
<PipelineList list="true">
   <Pipeline>
    <Id>31fa3c9ca8134f9cec2b4b0b0f787830</Id>
    <Name>example-pipeline</Name>
    <State>Active</State>
    <Speed>Standard</Speed>
    <NotifyConfig>
        <Topic>mts-topic-1</Topic>
    </NotifyConfig>
    <Role>AliyunMTSDefaultRole</Role>
   </Pipeline>
</PipelineList>
</QueryPipelineList>
```

JSON

```
{
 "RequestId": "25818875-5F78-4A13-BEF6-D7393642CA58",
    "TotalCount": 1,
    "PageNumber": 1,
    "PageSize": 10,
    "PipelineList": {
        "Pipeline": [{
            "Id": "31fa3c9ca8134f9cec2b4b0b0f787830",
            "Name": "example-pipeline",
            "State": "Active",
            "Speed":"Standard",
            "NotifyConfig":{
                "Topic":"mts-topic-1"
            },
            "Role":"AliyunMTSDefaultRole"
            }]
     }
}
```

