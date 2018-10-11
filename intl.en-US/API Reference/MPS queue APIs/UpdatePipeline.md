# UpdatePipeline {#reference_i2n_jnt_x2b .reference}

The UpdatePipeline API updates an MPS queue. You can modify the name and notification settings and change the status of an MPS queue.

## Request parameters {#section_iqn_qbt_x2b .section}

|Parameters|Type|Required or not|Description|
|:---------|:---|:--------------|:----------|
|Action|String|Yes|API of the action, system required parameter. Value: UpdatePipeline|
|PipelineId|String|Yes|MPS queue ID.|
|Name|String|Yes|MPS queue name.Up to 128 characters.

|
|State|String|Yes|MPS queue status, which can be Active and Paused.-   Active: tasks in the MPS queue will be scheduled, transcoded, and executed by Media Processing.
-   Paused: The MPS queue is paused, and tasks in the MPS queue will not be scheduled, transcoded, and executed by Media Processing. The status of all tasks in the MPS queue is Submitted. Ongoing transcoding tasks are not paused.

|
|NotifyConfig|String|No|Message Service configuration.Example: `{"Topic":"mts-topic-1"}`

.|
|Role|String|No|Roles|

## Response parameters {#section_ogh_wbt_x2b .section}

|Parameter|Type|Description|
|:--------|:---|:----------|
|Pipeline|String|MPS queue|

## Examples {#section_gpq_zbt_x2b .section}

Request example

```
http://mts.cn-hangzhou.aliyuncs.com/?PipelineId=5efb0fa33836432e9488ed56eb0075c8&Name=example-watermark&State=Paused&Action=UpdatePipeline&NotifyConfig=%7b&quot%3btopic&quot%3b%3a&quot%3bmts-topic-1&quot%3b%2c+&quot%3brole&quot%3b%3a&quot%3brole1&quot%3b%7d<Public parameter>
```

Response example

XML

```
<UpdatePipelineResponse>
        <RequestId>25818875-5F78-4A13-BEF6-D7393642CA58</RequestId>
        <Pipeline>
            <Id>31fa3c9ca8134f9cec2b4b0b0f787830</Id>
            <Name>qupai-pipeline</Name>
            <State>Active</State>
            <Speed>Standard</Speed>
            <NotifyConfig>
                <Topic>mts-topic-1</Topic>
            </NotifyConfig>
            <Role>AliyunMTSDefaultRole</Role>
        </Pipeline>
    </UpdatePipelineResponse>
```

JSON

```
{
        "RequestId":"25818875-5F78-4A13-BEF6-D7393642CA58",
        "Pipeline":{
            "Id":"31fa3c9ca8134f9cec2b4b0b0f787830",
            "Name":"qupai-pipeline",
            "State":"Active",
            "Speed":"Standard",
            "NotifyConfig":{
                "Topic":"mts-topic-1"
            }，
            "Role":"AliyunMTSDefaultRole"
        }
    }
```

