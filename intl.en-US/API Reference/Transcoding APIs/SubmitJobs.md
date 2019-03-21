# SubmitJobs {#reference_ksb_vdt_x2b .reference}

The SubmitJobs API submits transcoding tasks. A transcoding output generates a transcoding task. This API returns the list of transcoding tasks. Tasks are added to an Media Transcoding queue for scheduling and execution. After tasks are executed, call the query transcoding tasks API to poll the task execution results. Asynchronous notification can be used.

**Note:** If you want to use a preset transcoding template, call the SubmitAnalysisJob \(SubmitAnalysisJob\) API to trigger template analysis and call the QueryAnalysisJobList \(QueryAnalysisJobList\) API to obtain a list of preset transcoding templates available for the input file. If the preset template specified in the submitted transcoding task is not in the list of available preset templates, the transcoding task fails.

## Request parameters {#section_iqn_qbt_x2b .section}

|Parameter|Type|Required or not|Description|
|:--------|:---|:--------------|:----------|
|Action|String|Yes|API of the action, system required parameter. Value: SubmitJobs|
|Input|String|Yes|Job input, which is a JSON object. For the Input definition, see `Appendix-Parameter details-19 Details of transcoding task input`. Example: `{``"Bucket":"example-bucket",``"Location":"oss-cn-hangzhou",``"Object":"example.flv"``}`Cloud resource authorization must be completed in the console.|
|OutputBucket|String|Yes|Output bucket. Cloud resource authorization must be completed in the console.|
|OutputLocation|String|No|Data center where the output bucket belongs.The default value is oss-cn-hangzhou.

|
|Outputs|String|Yes|-   Outputs consists of the Output list, which is a JSON array and has up to 30 Output parameters.
-   For Output definition, see the glossary.
-   For details about the Output parameter, see “2. Output” in “Parameters” of “Appendix.”

Example: `[{``"OutputObject":"example-output.flv",``"TemplateId":"S00000000-000010",``"WaterMarks":[{``"InputFile":{``"Bucket":"example-bucket",``"Location":"oss-cn-hangzhou",``"Object":"example-logo.png"``},``"WaterMarkTemplateId":"88c6ca184c0e47098a5b665e2a126797"``}],``"UserData":"testid-001"``}]`|
|PipelineId|String|Yes|MPS queue ID.-   For the MPS queue definition, see the glossary.
-   If asynchronous notification is required, ensure that the MPS queue is bound to an available message subject.

|

## Response parameters {#section_ogh_wbt_x2b .section}

|Parameters|Type|Description|
|:---------|:---|:----------|
|JobResultList|AliyunJobResult\[ \]|List of submitted transcoding task results|

## Examples {#section_gpq_zbt_x2b .section}

Request example

```
http://mts.cn-hangzhou.aliyuncs.com/?PipelineId=88c6ca184c0e47098a5b665e2a126799&Action=SubmitJobs&Input=%7b%22Bucket%22%3a%22example-bucket%22%2c%22Location%22%3a%22oss-cn-hangzhou%22%2c%22Object%22%3a%22example.flv%22%7d&Outputs=%5b%7b%22OutputObject%22%3a%22example-output.flv%22%2c%22TemplateId%22%3a%22S00000000-000010%22%2c%22WaterMarks%22%3a%5b%7b%22InputFile%22%3a%7b%22Bucket%22%3a%22example-bucket%22%2c%22Location%22%3a%22oss-cn-hangzhou%22%2c%22Object%22%3a%22example-logo.png%22%7d%2c%22WaterMarkTemplateId%22%3a%2288c6ca184c0e47098a5b665e2a126797%22%7d%5d%7d%5d&OutputBucket=example-bucket&Public Parameters>
```

Response example

XML

```
<SubmitJobsResponse>
        <RequestId>25818875-5F78-4A13-BEF6-D7393642CA58</RequestId>
        <JobResultList list="true">
            <JobResult>
                <Success>true</Success>
                <Code> </Code>
                <Message> </Message>
                <Job>
                    <JobId>31fa3c9ca8134f9cec2b4b0b0f787830</JobId>
                    <Input>
                        <Bucket>example-bucket</Bucket>
                        <Location>oss-cn-hangzhou</Location>
                        <Object>example.flv</Object>
                    </Input>
                    <Output>
                         <OutputFile>
                            <Bucket>example-bucket</Bucket>
                            <Location>oss-cn-hangzhou</Location>
                            <Object>example-output.flv</Object>
                        </OutputFile>
                        <TemplateId>S00000000-000010</TemplateId>
                        <WaterMarkList list="true">
                            <WaterMark>
                                <InputFile>
                                    <Bucket>example-logo-bucket</Bucket>
                                    <Location>0ss-cn-hangzhou</Location>
                                    <Object>example-logo.png</Object>
                                </InputFile>
                                <WaterMarkTemplateId>88c6ca184c0e47098a5b665e2a126797</WaterMarkTemplateId>
                            </WaterMark>
                        </WaterMarkList>
                        <UserData>testid-001</UserData>
                    </Output>
                    <State>Submitted</State>
                    <Code> </Code>
                    <Message> </Message>
                    <Percent>0</Percent>
                    <PipelineId>88c6ca184c0e47098a5b665e2a126797</PipelineId>
                    <CreationTime>2014-01-10T12:00:00Z</CreationTime>
                </Job>
            </JobResult>
        </JobResultList>
    </SubmitJobsResponse>
```

JSON

```
{
        "RequestId": "25818875-5F78-4A13-BEF6-D7393642CA58",
        "JobResultList": {
            "JobResult": [{
                "Success": true,
                "Code": "",
                "Message": "",
                "Job": {
                    "JobId": "31fa3c9ca8134f9cec2b4b0b0f787830",
                    "Input": {
                            "Bucket": "example-bucket",
                            "Location": "oss-cn-hangzhou",
                            "Object": "example.flv"
                    },
                    "Output": {
                        "OutputFile": {
                            "Bucket": "example-bucket",
                            "Location": "oss-cn-hangzhou",
                            "Object": "example-output.flv"
                        },
                        "TemplateId": "S00000000-000010",
                        "WaterMarkList": {
                            "WaterMark": [{
                                 "InputFile": {
                                    "Bucket": "example-bucket",
                                    "Location": "oss-cn-hangzhou",
                                    "Object": "example-logo.png"
                                },
                                "WaterMarkTemplateId": "88c6ca184c0e47098a5b665e2a126797"
                            }]
                        },
                        "UserData":"testid-001"
                    },
                    "State": "Submitted",
                    "Code": "",
                    "Message": "",
                    "Percent": 0,
                    "PipelineId": "88c6ca184c0e47098a5b665e2a126797",
                    "CreationTime”:”2014-01-10T12:00:00Z"
                }
            }]
        }
    }
```

## Transcoding error codes {#section_h1h_p2t_x2b .section}

|Error code|Description|Detailed information|
|:---------|:----------|:-------------------|
|InvalidParameter.ResourceContentBad|The transcoding fails because the transcoding source file is damaged.|The resource operated is broken.|
|PermissionDenied.ResourceAccess|Problems with authorization|The operation has no authorization.|
|InternalError|Internal unrecognized error|The operation has failed due to some unknown error, exception or failure.|
|InvalidParameter.NullValue|The parameter value is Null.|The specified parameter “%s” cannot be null.|
|InvalidParameter.EmptyValue|The parameter is blank.|The specified parameter “%s” can not be empty.|
|InvalidParameter.UUIDFormatInvalid|The ID is not in UUID format.|The parameter “%s” is invalid.A uuid must: 1\) be comprised of chracters\[a-f\],numbers\[0-9\]; 2\) be 32 characters long|
|InvalidParameter.OutOfRange|The parameter value is out of the value range.|The specified parameter “%s” is out of range.|
|InvalidParameter.ResourceNotFound|The resource does not exist.|The resource operated “%s” cannot be found.|
|InvalidParameter.ResourceDeleted|The resource is deleted.|The resource operated “%s” has been deleted.|
|InvalidParameter.BucketNameInvalid|The bucket name is invalid.|The bucket name “%s” is invalid. A bucket name must: 1\) be comprised of lower-case characters, numbers, underscore\(\_\) or dash\(-\); 2\) start with lower case or numbers; 3\) be between 3-255 characters long.|
|InvalidParameter.LocationInvalid|The location is invalid.|The location “%s” is invalid. A location name must be one of the five: oss-cn-hangzhou, oss-cn-shanghai, oss-cn-beijing, oss-us-west-1 and oss-cn-shenzhen.|
|InvalidParameter.ObjectKeyInvalid|The object name is invalid.|The object key “%s” is invalid. An object name should be between 1 - 1023 bytes long when encoded as UTF-8 and cannot contain LF or CR or unsupported chars in XML1.0|
|InvalidParameter.JsonArrayFormatInvalid|The parameter is not a JSON array.|The parameter “%s” does not conform to the JSON Array specification.|
|Parameters.NotSupported|The parameter is not supported.|The Parameters “%s” is not supported the same time,choose one of them.|
|InvalidParameter.ResourceNotSupported|The resource type is not supported.|The resource operated “%s” is not supported.|
|NotSupportedJob.SystemTemplateJobNotSupported|The system template does not support high-speed transcoding.|The Template “%s” is a system template,cannot be supported by boost pipeline”.|
|InvalidParameter.Format|The parameter format is incorrect.|The format of parameter “%s” is invalid.|
|InvalidParameter.TemplateNotFound|The template cannot be found.|The Template operated “%s” cannot be found.|
|InvalidParameter.TemplateNotSupported|The template is not supported.|The template operated “%s” is not supported.|
|InvalidParameter.NumberFormatInvalid|The parameter is not a number.|he number format of parameter “%s” is invalid.|
|ParameterNotBoolean|The parameter is not a Boolean value.|ParameterNotBoolean, The Parameter “%s” is not boolean value.|
|InvalidParameter.DigiWatermark|The digital watermarking parameter is invalid.|The specified parameter “%s” must include alternative of “InputFile” or “\(NumberMark, StringMark\).|
|InvalidParameter.WaterMarkFileFormatNotSupported|The watermarking format is not supported.|The resource operated “%s” is not supported, watermark only supports png file.|
|InvalidParameter.InvalidDigitalWaterMarkType|The digital watermarking type is invalid.|The specified parameter “%s” is invalid.|
|InvalidParameter.ListSizeExceed|The length of the parameter list exceeds the threshold.|The specified parameter “%s” size exceed limits.|
|InvalidParameter.InvalidBase64Format|The parameter does not conform to the Base64 format and is invalid.|The specified parameter “%s” should be encoded by base64\_urlsafe.|
|InvalidParameter.ServiceNotSupportRegion|The feature is not supported in this region.|The parameter region “%s” has not support the open video service.|
|DataEncryption.ContainerFormatNotSupported|The data is encrypted, and the container format is not supported.|The container format only support: m3u8.|
|DataEncryption.CiphertextNotExist|The data is encrypted, and the ciphertext does not exist.|The ciphertext does not exist.|

