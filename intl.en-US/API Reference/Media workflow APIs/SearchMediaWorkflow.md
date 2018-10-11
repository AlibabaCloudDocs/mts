# SearchMediaWorkflow {#reference_wdk_tqg_y2b .reference}

The SearchMediaWorkflow API searches for media workflows.

## Request parameters {#section_iqn_qbt_x2b .section}

|Parameters|Type|Required or not|Description|
|:---------|:---|:--------------|:----------|
|Action|String|Yes|API of the action, system required parameter. Value: SearchMediaWorkflow|
|StateList|String|No|Media workflow status list,-   separated by commas \(,\).
-   The states include inactive, active, deleted.

Default value: “Inactive, Active, Deleted”

|
|PageSize|Long|No|Page size.-   Maximum value: 100.
-   Default value: 10.

|
|PageNumber|Long|No|The page number.Default value: 1.

|

## Response parameters {#section_ogh_wbt_x2b .section}

|Parameter|Type|Description|
|:--------|:---|:----------|
|MediaWorkflowList|[MediaWorkflow](https://help.aliyun.com/document_detail/29251.html#MediaWorkflow)\[\]|List of media workflows.|
|TotalCount|Long|Total number.|
|PageSize|Long|The page size.|
|PageNumber|Long|Page number.|

## Examples {#section_gpq_zbt_x2b .section}

Request example

```
https://mts.cn-hangzhou.aliyuncs.com/?PageSize=1&<public parameter>
```

Response example

XML

```
<SearchMediaWorkflowResponse> 
  <PageNumber>1</PageNumber>  
  <MediaWorkflowList> 
    <MediaWorkflow> 
      <CreationTime>2016-04-01T05:38:41Z</CreationTime>  
      <Name>mediaworkflow-test1</Name>  
      <State>Inactive</State>  
      <Topology>{"Activities":{"Act-Start":{"Parameters":{"PipelineId":"130266f58161436a80bf07cb12c8009a","InputFile":"{\"Bucket\": \"panda-vod\",\"Location\": \"oss-cn-hangzhou\"}"},"Type":"Start"},"Act-Report":{"Parameters":{},"Type":"Report"},"Act-Transcode-M3U8":{"Parameters":{"Outputs":"[{\"Object\":\"transcode/{ObjectPrefix}{FileName}\",\"TemplateId\": \"957d1719ee85ed6527b90cf62726cbef\"}]","OutputBucket":"panda-vod-hls","OutputLocation":"oss-cn-hangzhou"},"Type":"Transcode"}},"Dependencies":{"Act-Start":["Act-Transcode-M3U8"],"Act-Report":[],"Act-Transcode-M3U8":["Act-Report"]}}</Topology>  
      <MediaWorkflowId>e00732b977da427d9177a4dee646b1aa</MediaWorkflowId> 
    </MediaWorkflow> 
  </MediaWorkflowList>  
  <TotalCount>339</TotalCount>  
  <PageSize>1</PageSize>  
  <RequestId>691EA73C-3937-4604-8031-580E5931783B</RequestId> 
</SearchMediaWorkflowResponse>
```

JSON

```
{
        "PageNumber": 1,
        "MediaWorkflowList": {
            "MediaWorkflow": [
                {
                    "CreationTime": "2016-04-01T05:38:41Z",
                    "Name": "mediaworkflow-test1",
                    "State": "Inactive",
                    "Topology": "{\"Activities\":{\"Act-Start\":{\"Parameters\":{\"PipelineId\":\"130266f58161436a80bf07cb12c8009a\",\"InputFile\":\"{\\\"Bucket\\\": \\\"panda-vod\\\",\\\"Location\\\": \\\"oss-cn-hangzhou\\\"}\"},\"Type\":\"Start\"},\"Act-Report\":{\"Parameters\":{},\"Type\":\"Report\"},\"Act-Transcode-M3U8\":{\"Parameters\":{\"Outputs\":\"[{\\\"Object\\\":\\\"transcode/{ObjectPrefix}{FileName}\\\",\\\"TemplateId\\\": \\\"957d1719ee85ed6527b90cf62726cbef\\\"}]\",\"OutputBucket\":\"panda-vod-hls\",\"OutputLocation\":\"oss-cn-hangzhou\"},\"Type\":\"Transcode\"}},\"Dependencies\":{\"Act-Start\":[\"Act-Transcode-M3U8\"],\"Act-Report\":[],\"Act-Transcode-M3U8\":[\"Act-Report\"]}}",
                    "MediaWorkflowId": "e00732b977da427d9177a4dee646b1aa"
                }
            ]
        },
        "TotalCount": 339,
        "PageSize": 1,
        "RequestId": "9AB3E295-F459-44C6-A0D4-6370700"
    }
Related articles
```

