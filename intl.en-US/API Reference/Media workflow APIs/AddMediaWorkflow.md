# AddMediaWorkflow {#reference_k1h_tng_y2b .reference}

The AddMediaWorkflow API adds a media workflow and defines the topology of the media workflow, and Activity and dependencies.

**Note:** For more information, see [Activity](reseller.en-US/API Reference/Appendix/Workflow activity introduction.md#).

## Request parameters {#section_iqn_qbt_x2b .section}

|Parameters|Type|Required or not|Description|
|:---------|:---|:--------------|:----------|
|Action|String|Yes|API of the action, system required parameter. Value: AddMediaWorkflow|
|Name|String|Yes|Media workflow name,-   and cannot be a null string.
-   The name must be unique,
-   which consists of up to 64 bytes.
-   It must be UTF-8 encoded.

|
|Topology|String|Yes|Topology of the media workflow.JSON object. The topology includes the activity list and activity dependencies, as shown in the following topology example.

|
|TriggerMode|String|No|Trigger mode.Range: OssAutoTrigger、NotInAuto

|

Topology example

```
{
  "Activities": {
    "Act-Transcode-M3U8": {
      "Parameters": {
        "Outputs": [
          {
            "OutputObject": "transcode%2F%7BObjectPrefix%7D%7BFileName%7D",
            "TemplateId": "957d1719ee85ed6527b90cf62726cbef"
          }
        ],
        "OutputBucket": "panda-vod-hls",
        "OutputLocation": "oss-cn-hangzhou"
      },
      "Type": "Transcode"
    },
    "Act-Start": {
      "Name": "Act-Start",
      "Parameters": {
        "PipelineId": "130266f58161436a80bf07cb12c8009a",
        "InputFile": {
          "Bucket": "panda-vod",
          "Location": "oss-cn-hangzhou"
        }
      },
      "Type": "Start"
    },
    "Act-Report": {
      "Name": "Act-Report",
      "Parameters": {
      },
      "Type": "Report"
    }
  },
  "Dependencies": {
    "Act-Transcode-M3U8": [
      "Act-Report"
    ],
    "Act-Start": [
      "Act-Transcode-M3U8"
    ],
    "Act-Report": [
    ]
  }
}
```

## Response parameters {#section_ogh_wbt_x2b .section}

|Parameter|Type|Description|
|:--------|:---|:----------|
|MediaWorkflow|[MediaWorkflow](https://help.aliyun.com/document_detail/29251.html?spm=a2c4g.11186623.6.676.oyhBPl#MediaWorkflow)|Media workflow.|

## Examples {#section_gpq_zbt_x2b .section}

Request example

```
https://mts.cn-hangzhou.aliyuncs.com/?Name=mediaworkflow-test&Action=AddMediaWorkflow&Topology=%7B%22Activities%22%3A%7B%22Act-Start%22%3A%7B%22Parameters%22%3A%7B%22PipelineId%22%3A%22130266f58161436a80bf07cb12c8009a%22%2C%22InputFile%22%3A%22%7B%5C%22Bucket%5C%22%3A+%5C%22panda-vod%5C%22%2C%5C%22Location%5C%22%3A+%5C%22oss-cn-hangzhou%5C%22%7D%22%7D%2C%22Type%22%3A%22Start%22%7D%2C%22Act-Report%22%3A%7B%22Parameters%22%3A%7B%7D%2C%22Type%22%3A%22Report%22%7D%2C%22Act-Transcode-M3U8%22%3A%7B%22Parameters%22%3A%7B%22Outputs%22%3A%22%5B%7B%5C%22OutputObject%5C%22%3A%5C%22transcode%252F%257BObjectPrefix%257D%257BFileName%257D%5C%22%2C%5C%22TemplateId%5C%22%3A+%5C%22957d1719ee85ed6527b90cf62726cbef%5C%22%7D%5D%22%2C%22OutputBucket%22%3A%22panda-vod-hls%22%2C%22OutputLocation%22%3A%22oss-cn-hangzhou%22%7D%2C%22Type%22%3A%22Transcode%22%7D%7D%2C%22Dependencies%22%3A%7B%22Act-Start%22%3A%5B%22Act-Transcode-M3U8%22%5D%2C%22Act-Report%22%3A%5B%5D%2C%22Act-Transcode-M3U8%22%3A%5B%22Act-Report%22%5D%7D%7D&<Public parameter>
```

Response example

XML

```
<AddMediaWorkflowResponse> 
      <RequestId>F1D21261-ADB9-406A-BF6F-491382139D59</RequestId>  
      <MediaWorkflow> 
        <CreationTime>2016-04-01T05:29:37Z</CreationTime>  
        <Name>mediaworkflow-test</Name>  
        <State>Inactive</State>  
        <Topology>{"Activities":{"Act-Start":{"Parameters":{"PipelineId":"130266f58161436a80bf07cb12c8009a","InputFile":"{\"Bucket\": \"panda-vod\",\"Location\": \"oss-cn-hangzhou\"}"},"Type":"Start"},"Act-Report":{"Parameters":{},"Type":"Report"},"Act-Transcode-M3U8":{"Parameters":{"Outputs":"[{\"OutputObject\":\"transcode%2F%7BObjectPrefix%7D%7BFileName%7D\",\"TemplateId\": \"957d1719ee85ed6527b90cf62726cbef\"}]","OutputBucket":"panda-vod-hls","OutputLocation":"oss-cn-hangzhou"},"Type":"Transcode"}},"Dependencies":{"Act-Start":["Act-Transcode-M3U8"],"Act-Report":[],"Act-Transcode-M3U8":["Act-Report"]}}</Topology>  
        <MediaWorkflowId>e00732b977da427d9177a4dee646b1aa</MediaWorkflowId> 
      </MediaWorkflow> 
    </AddMediaWorkflowResponse>
```

JSON

```
{
        "RequestId": "F1D21261-ADB9-406A-BF6F-491382139D59",
        "MediaWorkflow": {
            "CreationTime": "2016-04-01T05:29:37Z",
            "Name": "mediaworkflow-test",
            "State": "Inactive",
            "Topology": "{\"Activities\":{\"Act-Start\":{\"Parameters\":{\"PipelineId\":\"130266f58161436a80bf07cb12c8009a\",\"InputFile\":\"{\\\"Bucket\\\": \\\"panda-vod\\\",\\\"Location\\\": \\\"oss-cn-hangzhou\\\"}\"},\"Type\":\"Start\"},\"Act-Report\":{\"Parameters\":{},\"Type\":\"Report\"},\"Act-Transcode-M3U8\":{\"Parameters\":{\"Outputs\":\"[{\\\"OutputObject\\\":\\\"transcode%2F%7BObjectPrefix%7D%7BFileName%7D\\\",\\\"TemplateId\\\": \\\"957d1719ee85ed6527b90cf62726cbef\\\"}]\",\"OutputBucket\":\"panda-vod-hls\",\"OutputLocation\":\"oss-cn-hangzhou\"},\"Type\":\"Transcode\"}},\"Dependencies\":{\"Act-Start\":[\"Act-Transcode-M3U8\"],\"Act-Report\":[],\"Act-Transcode-M3U8\":[\"Act-Report\"]}}",
            "MediaWorkflowId": "93ab850b4f6f44eab54b6e91d24d81d4"
        }
    }
```

