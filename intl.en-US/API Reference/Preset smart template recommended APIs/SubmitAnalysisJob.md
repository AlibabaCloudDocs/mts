# SubmitAnalysisJob {#reference_k1c_gct_x2b .reference}

When you submit a file to the preset template analysis job interface, the MPS will intelligently analyze the input file to recommend a preset template suitable for the input file; the template analysis job result may be obtained using the QueryTemplateAnalysisJob interface, or the asynchronous notification mechanism.

**Note:** The result of the preset template analysis is only retained for half a month and will be deleted after this two-week period. If the job is submitted again using the recommended template preset more than half a month later, the transcoding job will fail. The failed error code is: `AnalysisResultNotFound`.

## Request parameters {#section_iqn_qbt_x2b .section}

|Parameter|Type|Required or not|Description|
|:--------|:---|:--------------|:----------|
|Action|String|Yes|Operation interface name, system-defined parameter, value: SubmitAnalysisJob|
|Input|String|Yes|Input, Json Object: `{``"Bucket":"example-bucket",``"Location":"oss-cn-hangzhou",``"Object":"example.flv"``}`. You need to grant this Bucket read permission to the MPS on the Bucket Authorization page in the console’s Resource Control Channel.|
|Priority|String|No|The task’s transcoding priority within its corresponding pipe,-   in the range of \[1-10\].
-   10 is the highest priority.
-   Default value: 6

 |
|UserData|String|No|User-defined data.Maximum length is 1,024 bytes

.|
|PipelineId|String|Yes|The pipe ID.If asynchronous notification is required, ensure that this pipe is bound to the available message subject

.|

## Response parameters {#section_ogh_wbt_x2b .section}

|Parameter|Type|Description|
|:--------|:---|:----------|
|AnalysisJob|AliyunAnalysisJob|System Preset Template Analysis Job|

## Examples {#section_gpq_zbt_x2b .section}

Request example

```
http://mts.cn-hangzhou.aliyuncs.com/?Action=SubmitAnalysisJob&Input=%7B%22Bucket%22%3A%22example-bucket%22%2C%22Location%22%3A%22oss-cn-hangzhou%22%2C%0A%22Object%22%3A%22example.flv%22%7D%7D<Public parameters>
```

Response example

XML

```
<SubmitAnalysisJobResponse>
        <RequestId>25818875-5F78-4A13-BEF6-D7393642CA58</RequestId>
        <AnalysisJob>
            <Id>88c6ca184c0e47098a5b665e2a126797</Id>
            <InputFile>
               <Bucket>example-bucket</Bucket>
               <Location>oss-cn-hangzhou</Location>
               <Object>example.flv</Object>
            </InputFile>
            <AnalysisConfig>
                <QualityControl>
                    <RateQuality>25</RateQuality>
                    <MethodStreaming>network</MethodStreaming>
                </QualityControl>
            </AnalysisConfig>
            <UserData>testid-001</UserData>
            <State>Success</State>
            <TemplateList list="true">
                <Template>
                    <Id>S00000000-000020</Id>
                    <Name>FLV-UD</Name>
                    <Container>
                        <Format>flv</Format>
                    </Container>
                    <Video>
                        <Codec>Auto</Codec>
                        <Profile>Auto</Profile>
                        <Bitrate>Auto</Bitrate>
                        <Crf>Auto</Crf>
                        <Width>Auto</Width>
                        <Height>Auto</Height>
                        <Fps>Auto</Fps>
                        <Gop>Auto</Gop>
                    </Video>
                    <Audio>
                        <Codec>Auto</Codec>
                        <Samplerate>Auto</Samplerate>
                        <Bitrate>Auto</Bitrate>
                        <Channels>Auto</Channels>
                    </Audio>
                    <State>Normal</State>
                </Template >
            </TemplateList>
            <Code> </Code>
            <Message> </Message>
            <Percent>100</Percent>
            <CreationTime>2014-01-10T12:00:00Z</CreationTime>
            <PipelineId>88c6ca184c0e47098a5b665e2a126797</PipelineId>
        </AnalysisJob>
    </SubmitAnalysisJobResponse>
```

JSON

```
{
     "RequestId": "25818875-5F78-4A13-BEF6-D7393642CA58",
     "AnalysisJob": {
         "Id": "88c6ca184c0e47098a5b665e2a126797",
         "InputFile": {
                 "Bucket": "example-bucket",
                 "Location": "oss-cn-hangzhou",
                 "Object": "example.flv"
         },
         "AnalysisConfig": {
                "QualityControl": {
                    "RateQuality": 25,
                    "MethodStreaming": "network"
                }
         },
         "UserData":"testid-001",
         "State": "Success",
         "Code": "",
         "Message": "",
         "Percent": 100,
         "PipelineId": "88c6ca184c0e47098a5b665e2a126797",
         "CreationTime”:”2014-01-10T12:00:00Z",
         "TemplateList": {
            "Template": [{
                "Id": "S00000000-000020",
                "Name": "FLV-UD",
                "Container": {
                    "Format": "flv"
                    },
                "Video": {
                    "Codec": "Auto",
                    "Profile": "Auto",
                    "Bitrate": "Auto",
                    "Crf": "Auto",
                    "Width": "Auto",
                    "Height": "Auto",
                    "Fps": "Auto",
                    "Gop": "Auto"
                    },
                "Audio": {
                    "Codec": "AAC",
                    "Samplerate": "44100",
                    "Bitrate": "Auto",
                    "Channels": "Auto"
                    },
                "State": "Normal"
                }]
         }
      }
    }
```

