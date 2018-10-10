# AddMedia {#reference_zgr_lsg_y2b .reference}

The AddMedia API adds media.

**Note:** 

-   After workflows are configured and a media file is uploaded to OSS, OSS automatically notifies Media Processing and Media Processing identifies the active workflow that matches a specific OSS bucket and object. Then the matched workflow is automatically executed. Therefore, in normal cases, files are automatically processed using the AddMedia without manual intervention, but you can manually call this API to process inventory video files in OSS without uploading.
-   Media information is automatically obtained when the specified active workflow is executed. When no workflow is specified, media information is not obtained.

## Request parameters {#section_iqn_qbt_x2b .section}

|Parameters|Type|Required or not|Description|
|:---------|:---|:--------------|:----------|
|Action|String|Yes|API of the action, system required parameter. Value: AddMedia|
|FileURL|String|Yes|Path to a media file,-   which consists of up to 3,200 bytes.
-   The URL format follows the RFC 2396 standard. \(The URL is subject to UTF-8 encoding and URL encoding.\)

|
|Title|String|No|Media title,-   which consists of up to 128 bytes.
-   UTF-8 encoding.

|
|Description|String|No|Description.-   which consists of up to 1,024 bytes.
-   UTF-8 encoding.

|
|CoverURL|String|No|Cover,-   which consists of up to 3,200 bytes.
-   The URL format follows the RFC 2396 standard \(The URL is subject to UTF-8 encoding and URL encoding\).

|
|CateId|Long|No|Category ID,which cannot be a negative number.

|
|Tags|String|No|List of labels.-   Separated by commas \(,\). Up to 16 tags.
-   Each tag consists of up to 32 bytes.
-   UTF-8 encoding.

|
|MediaWorkflowId|String|No|Media workflow ID.|
|MediaWorkflowUserData|String|No|Custom data of a media workflow,-   which consists of up to 1,024 bytes.
-   UTF-8 encoding.

|
|OverrideParams|Json|No|Override parameters.-   Example 1: HLS package subtitle override\{“WebVTTSubtitleOverrides”,\[\{“RefActivityName”:”subtitleNode”,”WebVTTSubtitleURL”:”http://test.oss-cn-hangzhou.aliyuncs.com/subtitle1.vtt"\}\]\}。
-   Example 2: DASH package subtitle override\{“subtitleTransNodeName”:\{“InputConfig”:\{“Format”:”stl”,”InputFile”:\{“URL”:”http://subtitleBucket.oss-cn-hangzhou.aliyuncs.com/package/subtitle/CENG.stl"\}\}\}\}。

|

-   Matching rules for workflow triggering

    Matching rule execution policy: Check the workflow binding position based on the path to the new file. A match is found if the path contains the rule-bound string. For the path `http://bucket.oss-cn-hangzhou.aliyuncs.com/A/B/C/test1.flv`, the matching rules are as follows:

    ```
    1. http://bucket.oss-cn-hangzhou.aliyuncs.com/A/B/C/        Matched
      2. http://bucket.oss-cn-hangzhou.aliyuncs.com/A/B/            Matched
      3. http://bucket.oss-cn-hangzhou.aliyuncs.com/A/              Matched
      4. http://bucket.oss-cn-hangzhou.aliyuncs.com/                Matched
      5. http://bucket.oss-cn-hangzhou.aliyuncs.com/A/B/C/test.flv  Matched
      6. http://bucket.oss-cn-hangzhou.aliyuncs.com/A/B/CC/         Not matched
      7. http://bucket.oss-cn-hangzhou.aliyuncs.com/A/B2/           Not matched
      8. http://bucket.oss-cn-hangzhou.aliyuncs.com/A2/B/C/         Not matched
    ```

    **Note:** Do not configure the input path of a workflow as the prefix of the input path of another workflow; otherwise, two workflow execution instances are triggered for the same incremental file. For example, the input path of a workflow is “test” and that of another workflow is “test1”. After an input file is uploaded to the test1 folder, two workflow execution instances are triggered because the test1 folder also matches the “test” prefix.\*

-   File name extension matching

    Only a multimedia file can trigger a media workflow, which is determined by the media repository using the file name extension. The file does not contain an extension \(the file name does not contain the extension separator “.”\) or the extension meets the following rules:

    **Note:** QoS is not guaranteed for files with the .swf file name extension in terms of screenshot and transcoding.

    |Type|File name extension|
    |:---|:------------------|
    |Video|3gp, asf, avi, dat, dv, flv, f4v, gif, m2t, m3u8, m4v, mj2, mjpeg, mkv, mov, mp4, mpe, mpg, mpeg, mts, ogg, qt, rm, rmvb, swf, ts, vob, wmv, webm|
    |Audio|aac, ac3, acm, amr, ape, caf, flac, m4a, mp3, ra, wav, wma, aiff|

-   Media workflow message

    Media workflows use [Alibaba Cloud Message Service](https://www.aliyun.com/product/mns) to send messages to users that access video cloud services after the Start and Report activities are completed. If you want to receive messages, set the MNS queue name and notification name on the Start node and use the [Message Service SDK](https://help.aliyun.com/document_detail/27508.html) to obtain the messages that are stored in the MNS queue or notification. The message format is as follows:

    |Name|Type|Description|
    |:---|:---|:----------|
    |RunId|String|Workflow execution ID.|
    |Name|String|Activity name.|
    |Type|String|Activity type,which can be Report or Start.

|
    |State|String|Activity status,which can be fail or success.

|
    |Code|String|Error code.An error code is returned if the activity status is Fail.

|
    |Message|String|Error message.An error message is returned if the activity status is Fail.

|
    |MediaWorkflowExecution|[MediaWorkflowExecution](https://help.aliyun.com/document_detail/29251.html#MediaWorkflowExecution)|Information of media workflow execution.|

-   Sample JSON message body:

    ```
    {
            "RunId": "8f8aba5a62ab4127ae2add18da20b0f2",
            "Name": "Act-7",
            "Type": "Report",
            "State": "Success",
            "MediaWorkflowExecution": {
                "Name": "ConcurrentSuccess",
                "RunId": "8f8aba5a62ab4127ae2add18da20b0f2",
                "Input": {
                    "InputFile": {
                        "Bucket": "inputfirst",
                        "Location": "oss-test",
                        "Object": "mediaWorkflow/ConcurrentSuccess/01.wmv"
                    },
                    "UserData":"test"
                },
                "State": "Success",
                "MediaId": "2be491ab4cb6499cd0befe5fcf0cb670",
                "ActivityList": [
                    {
                        "RunId": "8f8aba5a62ab4127ae2add18da20b0f2",
                        "Name": "Act-1",
                        "Type": "Start",
                        "State": "Success",
                        "StartTime": "2016-03-15T02: 53: 41Z",
                        "EndTime": "2016-03-15T02: 53: 41Z"
                    },
                    {
                        "RunId": "8f8aba5a62ab4127ae2add18da20b0f2",
                        "Name": "Act-2",
                        "Type": "Transcode",
                        "JobId": "f34b6d1429dd491faa7a6c1c8f905285",
                        "State": "Success",
                        "StartTime": "2016-03-15T02: 53: 43Z",
                        "EndTime": "2016-03-15T02: 53: 47Z"
                    },
                    {
                        "RunId": "8f8aba5a62ab4127ae2add18da20b0f2",
                        "Name": "Act-3",
                        "Type": "Transcode",
                        "JobId": "888ac3903ecf4898b9d790cf7f1d969e",
                        "State": "Success",
                        "StartTime": "2016-03-15T02: 53: 44Z",
                        "EndTime": "2016-03-15T02: 53: 48Z"
                    },
                    {
                        "RunId": "8f8aba5a62ab4127ae2add18da20b0f2",
                        "Name": "Act-5",
                        "Type": "Snapshot",
                        "JobId": "c14150be33304825a5d67cd5364c35cb",
                        "State": "Success",
                        "StartTime": "2016-03-15T02: 53: 44Z",
                        "EndTime": "2016-03-15T02: 53: 45Z"
                    },
                    {
                        "RunId": "8f8aba5a62ab4127ae2add18da20b0f2",
                        "Name": "Act-6",
                        "Type": "Snapshot",
                        "JobId": "8c30c30ca7324286afda1a9a1b14d03c",
                        "State": "Success",
                        "StartTime": "2016-03-15T02: 53: 48Z",
                        "EndTime": "2016-03-15T02: 53: 49Z"
                    },
                    {
                        "RunId": "8f8aba5a62ab4127ae2add18da20b0f2",
                        "Name": "Act-7",
                        "Type": "Report",
                        "State": "Success",
                        "StartTime": "2016-03-15T02: 53: 49Z",
                        "EndTime": "2016-03-15T02: 53: 49Z"
                    }
                ],
                "CreationTime": "2016-03-15T02: 53: 39Z"
            }
        }
    ```


## Response parameters {#section_ogh_wbt_x2b .section}

|Parameter|Type|Description|
|:--------|:---|:----------|
|Media|[Media](https://help.aliyun.com/document_detail/29251.html#Media)|Media|

## Examples {#section_gpq_zbt_x2b .section}

Request example

```
http://mts.cn-hangzhou.aliyuncs.com?MediaWorkflowUserData=test&MediaWorkflowId=09bc2f74e39c48dd86597849e2b060f6&FileURL=http%3A%2F%2Fzzzinput-test.oss-cn-hangzhou.aliyuncs.com%2Ftail_comm-33.mp4&<public parameter>
```

Response example

XML

```
<AddMediaResponse>
         <Media>
           <CoverURL>http://zzyoutputbucket.oss-cn-hangzhou.aliyuncs.com/aa9bb3115da54befa74e0bd81a7a9e46%2F0.jpg</CoverURL>
           <Format>mov,mp4,m4a,3gp,3g2,mj2</Format>
           <PublishState>Published</PublishState>
           <Height>1280</Height>
           <MediaId>3e6149d5a8c944c09b1a8d2dc3e4ac65</MediaId>
           <Title>tail_comm-33.mp4</Title>
           <CreationTime>2016-09-20T03:02:40Z</CreationTime>
           <RunIdList>
             <RunId>adee42a78b1f407184a792b8777efb3c</RunId>
           </RunIdList>
           <CateId>0</CateId>
           <Duration>2.645333</Duration>
           <Width>1280</Width>
           <Fps>25.0</Fps>
           <Bitrate>1148.77</Bitrate>
           <Size>379860</Size>
         </Media>
         <RequestId>13E58723-4746-46A5-900D-B41D425A2A44</RequestId>
        </AddMediaResponse>
```

JSON

```
{
            "Media": {
                "CoverURL": "http://zzyoutputbucket.oss-cn-hangzhou.aliyuncs.com/adee42a78b1f407184a792b8777efb3c%2F0.jpg", 
                "Format": "mov,mp4,m4a,3gp,3g2,mj2", 
                "PublishState": "Published", 
                "Height": "1280", 
                "MediaId": "3e6149d5a8c944c09b1a8d2dc3e4ac65", 
                "Title": "tail_comm-33.mp4", 
                "CreationTime": "2016-09-20T03:02:40Z", 
                "RunIdList": {
                    "RunId": [
                        "cbad98d35629470fa05ff393d347fd73"
                    ]
                }, 
                "CateId": 0, 
                "Duration": "2.645333", 
                "Width": "1280", 
                "Fps": "25.0", 
                "Bitrate": "1148.77", 
                "Size": "379860"
            }, 
            "RequestId": "A29ED91C-84A2-41FE-8F7F-116531A28544"
        }
```

