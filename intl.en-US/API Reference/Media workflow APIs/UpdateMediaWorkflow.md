# UpdateMediaWorkflow {#reference_qwf_2qg_y2b .reference}

The UpdateMediaWorkflow API updates the topology of a media workflow.

## Request parameters {#section_iqn_qbt_x2b .section}

|Parameters|Type|Required or not|Description|
|:---------|:---|:--------------|:----------|
|Action|String|Yes|API of the action, system required parameter. Value: UpdateMediaWorkflow|
|MediaWorkflowId|String|Yes|Media workflow ID.|
|Topology|String|Yes|Media workflow topology.JSON object. The topology includes the activity list and activity dependencies, as shown in the following topology example.

|

Topology example

```
{
        "Activities": {
            "Act-Transcode-M3U8": {
                "Parameters": {
                    "Outputs": "[{\"OutputObject\":\"transcode%2F%7BObjectPrefix%7D%7BFileName%7D\",\"TemplateId\": \"957d1719ee85ed6527b90cf62726cbef\"}]",
                    "OutputBucket": "panda-vod-hls",
                    "OutputLocation": "oss-cn-hangzhou"
                },
                "Type": "Transcode"
            },
            "Act-Start": {
                "Name": "Act-Start",
                "Parameters": {
                    "PipelineId": "130266f58161436a80bf07cb12c8009a",
                    "InputFile": "{\"Bucket\": \"panda-vod\",\"Location\": \"oss-cn-hangzhou\"}"
                },
                "Type": "Start"
            },
            "Act-Report": {
                "Name": "Act-Report",
                "Parameters": {},
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
            "Act-Report": []
        }
    }
```

## Response parameters {#section_ogh_wbt_x2b .section}

|Parameter|Type|Description|
|:--------|:---|:----------|
|MediaWorkflow|[MediaWorkflow](reseller.en-US/API Reference/Data types.md#)|Media workflow|

## Examples {#section_gpq_zbt_x2b .section}

Request example

```
https://mts.cn-hangzhou.aliyuncs.com/?Action=UpdateMediaWorkflow&Topology=%7B%22Activities%22%3A%7B%22Act-Start%22%3A%7B%22Parameters%22%3A%7B%22PipelineId%22%3A%22130266f58161436a80bf07cb12c8009a%22%2C%22InputFile%22%3A%22%7B%5C%22Bucket%5C%22%3A+%5C%22panda-vod%5C%22%2C%5C%22Location%5C%22%3A+%5C%22oss-cn-hangzhou%5C%22%7D%22%7D%2C%22Type%22%3A%22Start%22%7D%2C%22Act-Report%22%3A%7B%22Parameters%22%3A%7B%7D%2C%22Type%22%3A%22Report%22%7D%2C%22Act-Transcode-M3U8%22%3A%7B%22Parameters%22%3A%7B%22Outputs%22%3A%22%5B%7B%5C%22OutputObject%5C%22%3A%5C%22transcode%252F%257BObjectPrefix%257D%257BFileName%257D%5C%22%2C%5C%22TemplateId%5C%22%3A+%5C%22957d1719ee85ed6527b90cf62726cbef%5C%22%7D%5D%22%2C%22OutputBucket%22%3A%22panda-vod-hls%22%2C%22OutputLocation%22%3A%22oss-cn-hangzhou%22%7D%2C%22Type%22%3A%22Transcode%22%7D%7D%2C%22Dependencies%22%3A%7B%22Act-Start%22%3A%5B%22Act-Transcode-M3U8%22%5D%2C%22Act-Report%22%3A%5B%5D%2C%22Act-Transcode-M3U8%22%3A%5B%22Act-Report%22%5D%7D%7D&<public parameter>
```

Response example

XML

```
<UpdateMediaWorkflowResponse> 
      <RequestId>F95B44E5-ECE1-4356-AD1C-2CF2D2B5043C</RequestId>  
      <MediaWorkflow> 
        <CreationTime>2016-04-01T05:29:38Z</CreationTime>  
        <Name>mediaworkflow-test</Name>  
        <State>Inactive</State>  
        <Topology>{"Activities":{"Act-Start":{"Parameters":{"PipelineId":"130266f58161436a80bf07cb12c8009a","InputFile":"{\"Bucket\": \"panda-vod\",\"Location\": \"oss-cn-hangzhou\"}"},"Type":"Start"},"Act-Report":{"Parameters":{},"Type":"Report"},"Act-Transcode-M3U8":{"Parameters":{"Outputs":"[{\"OutputObject\":\"transcode%2F%7BObjectPrefix%7D%7BFileName%7D\",\"TemplateId\": \"957d1719ee85ed6527b90cf62726cbef\"}]","OutputBucket":"panda-vod-hls","OutputLocation":"oss-cn-hangzhou"},"Type":"Transcode"}},"Dependencies":{"Act-Start":["Act-Transcode-M3U8"],"Act-Report":[],"Act-Transcode-M3U8":["Act-Report"]}}</Topology>  
        <MediaWorkflowId>93ab850b4f6f44eab54b6e91d24d81d4</MediaWorkflowId> 
      </MediaWorkflow> 
    </UpdateMediaWorkflowResponse>
```

JSON

```
{
        "RequestId": "A06BF02F-1BA7-4866-85FE-B17D318DBD47",
        "MediaWorkflow": {
            "CreationTime": "2016-04-01T05:29:38Z",
            "Name": "mediaworkflow-test",
            "State": "Inactive",
            "Topology": "{\"Activities\":{\"Act-Start\":{\"Parameters\":{\"PipelineId\":\"130266f58161436a80bf07cb12c8009a\",\"InputFile\":\"{\\\"Bucket\\\": \\\"panda-vod\\\",\\\"Location\\\": \\\"oss-cn-hangzhou\\\"}\"},\"Type\":\"Start\"},\"Act-Report\":{\"Parameters\":{},\"Type\":\"Report\"},\"Act-Transcode-M3U8\":{\"Parameters\":{\"Outputs\":\"[{\\\"OutputObject\\\":\\\"transcode%2F%7BObjectPrefix%7D%7BFileName%7D\\\",\\\"TemplateId\\\": \\\"957d1719ee85ed6527b90cf62726cbef\\\"}]\",\"OutputBucket\":\"panda-vod-hls\",\"OutputLocation\":\"oss-cn-hangzhou\"},\"Type\":\"Transcode\"}},\"Dependencies\":{\"Act-Start\":[\"Act-Transcode-M3U8\"],\"Act-Report\":[],\"Act-Transcode-M3U8\":[\"Act-Report\"]}}",
            "MediaWorkflowId": "93ab850b4f6f44eab54b6e91d24d81d4"
        }
    }
```

