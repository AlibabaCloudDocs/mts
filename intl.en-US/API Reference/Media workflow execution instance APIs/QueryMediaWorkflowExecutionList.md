# QueryMediaWorkflowExecutionList {#reference_ukq_bsg_y2b .reference}

The QueryMediaWorkflowExecutionList API queries media workflow execution instances.

## Request parameters {#section_iqn_qbt_x2b .section}

|Parameters|Type|Required or not|Description|
|:---------|:---|:--------------|:----------|
|Action|String|Yes|API of the action, system required parameter. Value: QueryMediaWorkflowExecutionList|
|RunIds|String|Yes|A list of media workflow execution instance IDs,separated by commas \(,\). A maximum of 10 instance IDs can be entered.

|

## Response parameters {#section_ogh_wbt_x2b .section}

|Parameter|Type|Description|
|:--------|:---|:----------|
|MediaWorkflowExecutionList|[MediaWorkflowExecution](https://help.aliyun.com/document_detail/29251.html#MediaWorkflowExcution)\[\]|A list of media workflow execution instances.|
|NonExistRunIds|String\[\]|A list of nonexistent media workflow execution instance IDs.|

## Examples {#section_gpq_zbt_x2b .section}

Request example

```
https://mts.cn-hangzhou.aliyuncs.com?RunIds=9bd5a286b59d4cf19685d5b3c501e528&<public parameter>
```

Response example

XML

```
<QueryMediaWorkflowExecutionListResponse> 
      <RequestId>1629B273-1F03-421B-9C5E-9C398E04805F</RequestId>  
      <MediaWorkflowExecutionList> 
        <MediaWorkflowExecution> 
          <CreationTime>2016-04-01T06:53:43Z</CreationTime>  
          <Name>ConcurrentSuccess</Name>  
          <Input> 
            <InputFile> 
              <Bucket>inputfirst</Bucket>  
              <Location>oss-test</Location>  
              <Object>mediaWorkflow/ConcurrentSuccess/test-1280x1280-0_wp.mp4</Object> 
            </InputFile> 
          </Input>  
          <State>Success</State>  
          <RunId>9bd5a286b59d4cf19685d5b3c501e528</RunId>  
          <ActivityList> 
            <Activity> 
              <Name>Act-1</Name>  
              <State>Success</State>  
              <Type>Start</Type>  
              <EndTime>2016-04-01T06:53:44Z</EndTime>  
              <StartTime>2016-04-01T06:53:44Z</StartTime> 
            </Activity>  
            <Activity> 
              <Name>Act-2</Name>  
              <State>Fail</State> 
              <Code>InvalidParameter.ResourceContentBad</Code>
              <Message>The resource operated InputFile is bad</Message>
              <Type>Transcode</Type>  
              <JobId>2376030d9d0849399cd20e20c876f4f3</JobId>  
              <EndTime>2016-04-01T06:54:00Z</EndTime>  
              <StartTime>2016-04-01T06:53:45Z</StartTime> 
            </Activity>  
            <Activity> 
              <Name>Act-3</Name>  
              <State>Success</State>  
              <Type>Transcode</Type>  
              <JobId>f2ffd10aee504c15b0bd6f39b92ca667</JobId>  
              <EndTime>2016-04-01T06:54:03Z</EndTime>  
              <StartTime>2016-04-01T06:53:47Z</StartTime> 
            </Activity>  
            <Activity> 
              <Name>Act-5</Name>  
              <State>Success</State>  
              <Type>Snapshot</Type>  
              <JobId>5dd9639f217c43eda011a95ee121ffc3</JobId>  
              <EndTime>2016-04-01T06:53:47Z</EndTime>  
              <StartTime>2016-04-01T06:53:47Z</StartTime> 
            </Activity>  
            <Activity> 
              <Name>Act-6</Name>  
              <State>Success</State>  
              <Type>Snapshot</Type>  
              <JobId>617cb572ad204e8daaa7da4bbd6f63af</JobId>  
              <EndTime>2016-04-01T06:54:01Z</EndTime>  
              <StartTime>2016-04-01T06:54:01Z</StartTime> 
            </Activity>  
            <Activity> 
              <Name>Act-7</Name>  
              <State>Success</State>  
              <Type>Report</Type>  
              <EndTime>2016-04-01T06:54:03Z</EndTime>  
              <StartTime>2016-04-01T06:54:03Z</StartTime> 
            </Activity> 
          </ActivityList>  
          <MediaId>21a32670ce4e1b1c93f569b2546f5180</MediaId> 
        </MediaWorkflowExecution> 
      </MediaWorkflowExecutionList> 
    </QueryMediaWorkflowExecutionListResponse>
```

JSON

```
{
    "RequestId": "ED86B7DE-A1C0-4D83-8DDA-886637532178",
    "MediaWorkflowExecutionList": {
        "MediaWorkflowExecution": [
            {
                "CreationTime": "2016-04-01T06:53:43Z",
                "Name": "ConcurrentSuccess",
                "Input": {
                    "InputFile": {
                        "Bucket": "inputfirst",
                        "Location": "oss-test",
                        "Object": "mediaWorkflow/ConcurrentSuccess/test-1280x1280-0_wp.mp4"
                    },
                    "UserData":"test-userData"
                },
                "State": "Success",
                "RunId": "9bd5a286b59d4cf19685d5b3c501e528",
                "ActivityList": {
                    "Activity": [
                        {
                            "Name": "Act-1",
                            "State": "Success",
                            "Type": "Start",
                            "EndTime": "2016-04-01T06:53:44Z",
                            "StartTime": "2016-04-01T06:53:44Z"
                        },
                        {
                            "Name": "Act-2",
                            "State": "Fail",
                            "Code":"InvalidParameter.ResourceContentBad",
                            "Message":"The resource operated InputFile is bad",
                            "Type": "Transcode",
                            "JobId": "2376030d9d0849399cd20e20c876f4f3",
                            "EndTime": "2016-04-01T06:54:00Z",
                            "StartTime": "2016-04-01T06:53:45Z"
                        },
                        {
                            "Name": "Act-3",
                            "State": "Success",
                            "Type": "Transcode",
                            "JobId": "f2ffd10aee504c15b0bd6f39b92ca667",
                            "EndTime": "2016-04-01T06:54:03Z",
                            "StartTime": "2016-04-01T06:53:47Z"
                        },
                        {
                            "Name": "Act-5",
                            "State": "Success",
                            "Type": "Snapshot",
                            "JobId": "5dd9639f217c43eda011a95ee121ffc3",
                            "EndTime": "2016-04-01T06:53:47Z",
                            "StartTime": "2016-04-01T06:53:47Z"
                        },
                        {
                            "Name": "Act-6",
                            "State": "Success",
                            "Type": "Snapshot",
                            "JobId": "617cb572ad204e8daaa7da4bbd6f63af",
                            "EndTime": "2016-04-01T06:54:01Z",
                            "StartTime": "2016-04-01T06:54:01Z"
                        },
                        {
                            "Name": "Act-7",
                            "State": "Success",
                            "Type": "Report",
                            "EndTime": "2016-04-01T06:54:03Z",
                            "StartTime": "2016-04-01T06:54:03Z"
                        }
                    ]
                },
                "MediaId": "21a32670ce4e1b1c93f569b2546f5180"
            }
        ]
    }
}
related articles
```

