# SubmitSnapshotJob {#reference_vcv_lmg_y2b .reference}

The SubmitSnapshotJob API submits screenshot tasks.

**Note:** JPG images are supported currently.

-   Synchronous mode: A screenshot result is synchronously returned over the API, and a screenshot is generated in the corresponding bucket during result returning.
-   Asynchronous mode: A screenshot may not be generated when a screenshot result is returned over the API. The screenshot task queues at the background, and the screenshot is taken asynchronously. If either the Interval or Num parameter is set, the asynchronous mode is used.
-   Message notification: If the PipelineId parameter is set, an asynchronous message is sent when a screenshot task is submitted.

## Request parameters {#section_iqn_qbt_x2b .section}

|Parameters|Type|Required or not|Description|
|:---------|:---|:--------------|:----------|
|Action|String|Yes|API of the action, system required parameter. Value: SubmitSnapshotJob|
|Input|String|Yes|Task input.-   JSON object. For the Input definition, see the glossary.
-   For example:

    ```
{"Bucket":"example-bucket", "Location": "oss-cn-hangzhou",
              "Object":"example.flv" }
    ```

For more information, see example of using [Snapshot interface](../../../../../reseller.en-US/SDK Reference/Transcoding SDKs/Java SDK/Screenshot.md#).

-   The bucket permission must be granted to Media Transcoding in the console.

|
|SnapshotConfig|String|Yes|Screenshot configuration.-   SON object. For details, see “11. SnapshotConfig” in Parameters” of “Appendix.”
-   For example:
    -   Synchronous mode:

        ```
{"OutputFile": {"Bucket": "example-001","Location":
              "oss-cn-hangzhou","Object": "example.jpg"},"Time": "5"}
        ```

    -   Asynchronous mode: \(start at 5 ms, one screenshot is taken per 20s, and 10 screenshots need to be taken\):

        ```
{"OutputFile": {"Bucket": "example-001","Location":
              "oss-cn-hangzhou","Object": "{Count}.jpg"},"Time":
              "5","Num":"10","Interval":"20"}
        ```


|
|PipelineId|String|No|MPS queue ID.-   Ensure that the Media Processing queue is bound to an available message subject. Otherwise, the message cannot be properly sent.

|
|UserData|String|No|Custom data.Up to 1,024 bytes.

|

## Response parameters {#section_ogh_wbt_x2b .section}

|Parameter|Type|Description|
|:--------|:---|:----------|
|SnapshotJob|[AliyunSnapshotJob](reseller.en-US/API Reference/Data types.md#)|Screenshot task|

## Examples {#section_gpq_zbt_x2b .section}

Request example

```
http://mts.cn-hangzhou.aliyuncs.com?Action=SubmitSnapshotJob&Input=%7b%22Bucket%22%3a%22example-bucket%22%2c%22Location%22%3a%22oss-cn-hangzhou%22%2c%22Object%22%3a%22example.flv%22%7d&SnapshotConfig=%7B%22OutputFile%22%3A%7B%22Bucket%22%3A%22example-001%22%2C%22Location%22%3A%22oss-cn-hangzhou%22%2C%22Object%22%3A%22example.jpg%22%7D%2C%22Time%22%3A%225%22%7D&PipelineId=88c6ca184c0e47098a5b665e2a126797<Public parameter>
```

Response example

XML

```
<SubmitSnapshotJobResponse>
        <RequestId>
            25818875-5F78-4A13-BEF6-D7393642CA58
        </RequestId>
        <SnapshotJob>
            <Id>88c6ca184c0e47098a5b665e2a126797</Id>
            <State>Success</State>
            <Code> </Code>
            <Message> </Message>
            <SnapshotConfig>
               <OutputFile>
                  <Bucket>example-001</Bucket>
                  <Location>oss-cn-hangzhou</Location>
                  <Object>example.png</Object>
               </OutputFile>
               <Time>4</Time>
            </SnapshotConfig>
            <PipelineId>88c6ca184c0e47098a5b665e2a126797</PipelineId>
            <UserData>testid-001</UserData>
            <CreationTime>2014-01-10T12:00:00Z</CreationTime>
        </SnapshotJob>
    </SubmitSnapshotJobResponse>
```

JSON

```
{
        "RequestId": "25818875-5F78-4A13-BEF6-D7393642CA58",
        "SnapshotJob": {
            "Id": "88c6ca184c0e47098a5b665e2a126797",
            "State": "Success",
             "Code": "",
            "Message": "",
            “SnapshotConfig”:{
               "OutputFile": {
                   "Bucket": "example-001",
                   "Location": "oss-cn-hangzhou",
                   "Object": "example.png"
               },
               “Time”:”5”
             },
             "PipelineId": "88c6ca184c0e47098a5b665e2a126797",
             "UserData": "testid-001",
             "CreationTime": "2014-01-10T12:00:00Z"
       }
    }
```

## Screenshot error codes {#section_dvc_vmg_y2b .section}

|Error codes|Description|Detailed information|
|:----------|:----------|:-------------------|
|InvalidParameter.ResourceNotFound|The screenshot file cannot be found.|The resource operated cannot be found.|
|SnapshotTimeOut|The screenshot times out. If time-out occurs frequently in synchronous mode, we recommend that the asynchronous mode be used to prevent time-out. Retry is not recommended.|Snapshot times out.|
|InvalidParameter.ResourceContentBad|The screenshot file is damaged, or the screenshot fails to be taken because it does not meet the specifications.|The resource operated is broken.|
|EntityNotExist.Role|The role does not exist.|The role not exists.|
|PermissionDenied.ResourceAccess|The operation has no authorization.|MTS not authorized to operate on the specified resource.|
|InternalError|Internal unrecognized error.|The operation has failed due to some unknown error, exception or failure.|
|TransientNetWorkError|A temporary network error occurs during data download. Generally, you can recover the download by retry.|Snapshot fail,transient network error occurs, please retry again!|

