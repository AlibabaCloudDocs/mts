# QueryMediaWorkflowList {#reference_nq3_mqg_y2b .reference}

The QueryMediaWorkflowList API queries registered media workflows.

## Request parameters {#section_iqn_qbt_x2b .section}

|Parameters|Type|Required or not|Description|
|:---------|:---|:--------------|:----------|
|Action|String|Yes|API of the action, system required parameter. Value: QueryMediaWorkflowList|
|MediaWorkflowIds|String|Yes|List of media workflow IDs,separated by commas \(,\). A maximum of 10 IDs can be entered.

|

## Response parameters {#section_ogh_wbt_x2b .section}

|Parameter|Type|Description|
|:--------|:---|:----------|
|MediaWorkflowList|[MediaWorkflow](https://help.aliyun.com/document_detail/29251.html#MediaWorkflow)\[\]|Media workflow list.|
|NonExistMediaWorkflowIdList|String\[\]|List of non-existing media workflow IDs.|

## Examples {#section_gpq_zbt_x2b .section}

Request example

```
https://mts.cn-hangzhou.aliyuncs.com/?MediaWorkflowIds=93ab850b4f6f44eab54b6e91d24d81d4&<public parameter>
```

Response example

XML

```
<QueryMediaWorkflowListResponse> 
      <MediaWorkflowList> 
        <MediaWorkflow> 
          <CreationTime>2016-04-01T05:29:38Z</CreationTime>  
          <Name>mediaworkflow-test</Name>  
          <State>Active</State>  
          <Topology>{"Activities":{"Act-Start":{"Parameters":{"PipelineId":"130266f58161436a80bf07cb12c8009a","InputFile":"{\"Bucket\": \"panda-vod\",\"Location\": \"oss-cn-hangzhou\"}"},"Type":"Start"},"Act-Report":{"Parameters":{},"Type":"Report"},"Act-Transcode-M3U8":{"Parameters":{"Outputs":"[{\"Object\":\"transcode/{ObjectPrefix}{FileName}\",\"TemplateId\": \"957d1719ee85ed6527b90cf62726cbef\"}]","OutputBucket":"panda-vod-hls","OutputLocation":"oss-cn-hangzhou"},"Type":"Transcode"}},"Dependencies":{"Act-Start":["Act-Transcode-M3U8"],"Act-Report":[],"Act-Transcode-M3U8":["Act-Report"]}}</Topology>  
          <MediaWorkflowId>93ab850b4f6f44eab54b6e91d24d81d4</MediaWorkflowId> 
        </MediaWorkflow> 
      </MediaWorkflowList>  
      <RequestId>FEC5AAFA-A8E5-43A4-9FDB-E62E708AF7E4</RequestId> 
    </QueryMediaWorkflowListResponse>
```

JSON

```
{
        "MediaWorkflowList": {
            "MediaWorkflow": [
                {
                    "CreationTime": "2016-04-01T05:29:38Z",
                    "Name": "mediaworkflow-test",
                    "State": "Active",
                    "Topology": "{\"Activities\":{\"Act-Start\":{\"Parameters\":{\"PipelineId\":\"130266f58161436a80bf07cb12c8009a\",\"InputFile\":\"{\\\"Bucket\\\": \\\"panda-vod\\\",\\\"Location\\\": \\\"oss-cn-hangzhou\\\"}\"},\"Type\":\"Start\"},\"Act-Report\":{\"Parameters\":{},\"Type\":\"Report\"},\"Act-Transcode-M3U8\":{\"Parameters\":{\"Outputs\":\"[{\\\"Object\\\":\\\"transcode/{ObjectPrefix}{FileName}\\\",\\\"TemplateId\\\": \\\"957d1719ee85ed6527b90cf62726cbef\\\"}]\",\"OutputBucket\":\"panda-vod-hls\",\"OutputLocation\":\"oss-cn-hangzhou\"},\"Type\":\"Transcode\"}},\"Dependencies\":{\"Act-Start\":[\"Act-Transcode-M3U8\"],\"Act-Report\":[],\"Act-Transcode-M3U8\":[\"Act-Report\"]}}",
                    "MediaWorkflowId": "93ab850b4f6f44eab54b6e91d24d81d4"
                }
            ]
        },
        "RequestId": "16CD0CDD-457E-420D-9755-8385075A618B"
    }
```

