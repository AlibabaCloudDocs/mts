# QueryAnalysisJobList {#reference_m4c_xct_x2b .reference}

Query Template Analysis Job interface. After the template analysis job is completed, a list of available preset templates is returned.

## Request parameters {#section_iqn_qbt_x2b .section}

|Parameters|Type|Required or not|Description|
|:---------|:---|:--------------|:----------|
|Action|String|Yes|Operation interface name, system-defined parameter, value: QueryAnalysisJobList|
|AnalysisJobIds|String|Yes|Template Analysis job ID list.-   Up to 10 queries at a time.
-   Use standard commas \(,\) as separator.

|

## Response parameters {#section_ogh_wbt_x2b .section}

|Parameter|Type|Description|
|:--------|:---|:----------|
|AnalysisJobList|AliyunAnalysisJob\[ \]|Template Analysis Job List.|
|NonExistAnalysisJobIds|String\[ \]|List of nonexistent template analysis jobs’ ID, the structure does not return if there is no data.|

## Examples {#section_gpq_zbt_x2b .section}

Request example

```
http://mts.cn-hangzhou.aliyuncs.com/?Action=QueryAnalysisJobList&AnalysisJobIds=31fa3c9ca8134f9cec2b4b0b0f787830&<Public parameters>
```

Response example

XML

```
<QueryAnalysisJobListResponse>
        <RequestId>25818875-5F78-4A13-BEF6-D7393642CA58</RequestId>
        <AnalysisJobList list="true">
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
                <Code> </Code>
                <Message> </Message>
                <Percent>100</Percent>
                <CreationTime>2014-01-10T12:00:00Z</CreationTime>
                <PipelineId>88c6ca184c0e47098a5b665e2a126797</PipelineId>
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
            </AnalysisJob>
        </AnalysisJobList>
    </QueryAnalysisJobListResponse>
```

JSON

```
{
        "RequestId": "25818875-5F78-4A13-BEF6-D7393642CA58",
        "AnalysisJobList": {
            "AnalysisJob": [{
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
                "CreationTime”:”2014-01-10T12:00:00Z"
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
                }]
            }
    }
```

