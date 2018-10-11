# ListJob {#reference_ms1_tft_x2b .reference}

The ListJob API lists transcoding tasks by task status, creation time range, and transcoding MPS queue. By default, tasks are sorted in descending order by CreationTime.

## Request parameters {#section_iqn_qbt_x2b .section}

|Parameters|Type|Required or not|Description|
|:---------|:---|:--------------|:----------|
|Action|String|Yes|API of the action, system required parameter. Value: ListJob|
|NextPageToken|String|No|Identifier of the next page, which is a 32-bit UUID.|
|MaximumPageSize|Long|No|Maximum number of media workflow execution instances that can be returned.-   Default value: 10.
-   Value range: \[1, 100\].

|
|State|String|No|Transcoding task status.-   All indicates all states,
-   Submitted indicates submitted tasks,
-   Transcoding indicates tasks being transcoded,
-   TranscodeSuccess indicates tasks that are successfully transcoded,
-   TranscodeFail indicates tasks that fail to be transcoded,
-   and TranscodeCancelled indicates tasks with canceled transcoding.

Default value: All.

|
|PipelineId|String|No|MPS queue ID.|
|StartOfJobCreatedTimeRange|String|No|Start date of the time range of creating transcoding tasks.-   The date format conforms to ISO 8601 and UTC time is used.
-   Format: YYYY-MM-DDThh:mm:ssZ.
-   Example: 2014-01-10T12:00:00Z \(January 10, 2014 at 20:00:00, Beijing time\).

|
|EndOfJobCreatedTimeRange|String|No|End date of the time range of creating transcoding tasks.-   The date format conforms to ISO 8601 and UTC time is used.
-   Format: YYYY-MM-DDThh:mm:ssZ.
-   Example, 2014-01-11T12:00:00Z \(January 11, 2014 at 20:00:00, Beijing time\).

|

## Response parameters {#section_ogh_wbt_x2b .section}

|Parameter|Type|Description|
|:--------|:---|:----------|
|JobList|AliyunJob\[ \]|Set of transcoding tasks|
|NextPageToken|String|Identifier of the next page, which is a 32-bit UUID.|

## Examples {#section_gpq_zbt_x2b .section}

Request example

```
http://mts.cn-hangzhou.aliyuncs.com/?StartOfJobCreatedTimeRange=2014-01-10T12%3A00%3A00Z&State=All&EndOfJobCreatedTimeRange=2014-01-11T12%3A00%3A00Z&PipelineId=88c6ca184c0e47098a5b665e2a126797&Action=ListJob&<Public parameter>
```

Response example

XML

```
<ListJobResponse>
        <RequestId>58CBF1B8-048C-4550-B59C-F6EA57A8CEB6</RequestId>
        <NextPageToken>8c6ca184c0e47098a5b665e2a126797</NextPageToken>
        <JobList list="true">
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
                    <TemplateId>0001-01</TemplateId>
                    <WaterMarkList list="true">
                        <WaterMark>
                            <InputFile>
                                <Bucket>example-logo-bucket</Bucket>
                                <Location>oss-cn-hangzhou</Location>
                                <Object>example-logo.png</Object>
                            </InputFile>
                            <WaterMarkTemplateId>88c6ca184c0e47098a5b665e2a126797</WaterMarkTemplateId>
                        </WaterMark>
                    </WaterMarkList>
                    <Properties>
                              <Streams>
                                  <VideoStreamList>
                                      <VideoStream>
                                          <Index>1</Index>
                                          <CodecName>h264</CodecName>
                                          <CodecLongName>H. 264 / AVC / MPEG-4 AVC / MPEG-4 part 10</CodecLongName>
                                          <Profile>High</Profile>
                                          <CodecTimeBase>1001/48000</CodecTimeBase>
                                          <CodecTagString>[0][0][0][0]</CodecTagString>
                                          <CodecTag>0x0000</CodecTag>
                                          <Width>1920</Width>
                                          <Height>1080</Height>
                                          <HasBFrames>1</HasBFrames>
                                          <Sar>1:1</Sar>
                                          <Dar>16:9</Dar>
                                          <PixFmt>yuv420p</PixFmt>
                                          <Level>41</Level>
                                          <Fps>25</Fps>
                                          <AvgFPS>24000/1001</AvgFPS>
                                          <Timebase>1/1000</Timebase>
                                          <StartTime>0.042000</StartTime>
                                          <Duration>100</Duration>
                                          <Bitrate>30541090</Bitrate>
                                          <NumFrames>100</NumFrames>
                                          <Lang>eng</Lang>
                                          <NetworkCost>
                                              <PreloadTime>8</PreloadTime>
                                              <CostBandwidth>10</CostBandwidth>
                                              <AvgBitrate>300.34</AvgBitrate>
                                          </NetworkCost>
                                      </aliyun_video_stream>
                                  </VideoStreamList>
                                  <AudioStreamList>
                                      <AudioStream>
                                          <Index>1</Index>
                                          <CodecName>dca</CodecName>
                                          <CodecTimeBase>1/48000</CodecTimeBase>
                                          <CodecLongName>DCA (DTS Coherent Acoustics)</CodecLongName>
                                          <CodecTagString>[0][0][0][0]</CodecTagString>
                                          <CodecTag>0x0000</CodecTag>
                                          <SampleFmt>fltp</SampleFmt>
                                          <Samplerate>48000</Samplerate>
                                          <Channels>2</Channels>
                                          <ChannelLayout>5.1(side)</ChannelLayout>
                                          <Timebase>1/1000</Timebase>
                                          <StartTime>0.042000</StartTime>
                                          <Duration>123</Duration>
                                          <Bitrate>1536000</Bitrate>
                                          <NumFrames>123</NumFrames>
                                          <Lang>eng</Lang>
                                      </aliyun_audio_stream>
                                  </AudioStreamList>
                                  <SubtitleStreamList>
                                      <SubtitleStream>
                                          <Index>3</Index>
                                          <Lang>eng</Lang>
                                      </aliyun_subtitle_stream>
                                  </SubtitleStreamList>
                              </Streams>
                              <Format>
                                  <NumStreams>1</NumStreams>
                                  <NumPrograms>2</NumPrograms>
                                  <FormatName>matroska,webm</FormatName>
                                  <FormatLongName>Matroska / WebM</FormatLongName>
                                  <StartTime>0.042000</StartTime>
                                  <Duration>17.600000</Duration>
                                  <Size>70569598</Size>
                                  <Bitrate>32077090</Bitrate>
                              </Format>
                    </Properties>
                    <UserData>testid-001</UserData>
                </Output>
                <State>TranscodeSuccess</State>
                <Code> </Code>
                <Message> </Message>
                <Percent>100</Percent>
                <PipelineId>88c6ca184c0e47098a5b665e2a126797</PipelineId>
                <CreationTime>2014-01-10T12:00:00Z</CreationTime>
            </Job>
        </JobList>
    </ListJobResponse>
```

JSON

```
{
        "NextPageToken":"8c6ca184c0e47098a5b665e2a126797",
        "JobList": {
            "Job": [{
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
                    "TemplateId": "0001-01",
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
                    "Properties":{
                                "Streams":{
                                    "VideoStreamList":{
                                        "VideoStream":[
                                            {
                                                "Index":"1",
                                                "CodecName":"h264",
                                                "CodecLongName":"H. 264 / AVC / MPEG-4 AVC / MPEG-4 part 10",
                                                "Profile":"High",
                                                "CodecTimeBase":"1001/48000",
                                                "CodecTagString":"[0][0][0][0]",
                                                "CodecTag":"0x0000",
                                                "Width":"1920",
                                                "Height":"1080",
                                                "HasBFrames":"1",
                                                "Sar":"1:1",
                                                "Dar":"16:9",
                                                "PixFmt":"yuv420p",
                                                "Level":"41",
                                                "Fps":"25",
                                                "AvgFPS":"24000/1001",
                                                "Timebase":"1/1000",
                                                "StartTime":"0.042000",
                                                "Duration":"100",
                                                "Bitrate":"30541090",
                                                "NumFrames":"100",
                                                "Lang":"eng",
                                                "NetworkCost":{
                                                    "PreloadTime":"8",
                                                    "CostBandwidth":"10",
                                                    "AvgBitrate":"300.34"
                                                }
                                            }
                                        ]
                                    },
                                    "AudioStreamList":{
                                        "AudioStream":[
                                            {
                                                "Index":"1",
                                                "CodecName":"dca",
                                                "CodecTimeBase":"1/48000",
                                                "CodecLongName":"DCA (DTS Coherent Acoustics)",
                                                "CodecTagString":"[0][0][0][0]",
                                                "CodecTag":"0x0000",
                                                "SampleFmt":"fltp",
                                                "Samplerate":"48000",
                                                "Channels":"2",
                                                "ChannelLayout":"5.1(side)",
                                                "Timebase":"1/1000",
                                                "StartTime":"0.042000",
                                                "Duration":"123",
                                                "Bitrate":"1536000",
                                                "NumFrames":"123",
                                                "Lang":"eng"
                                            }
                                        ]
                                    },
                                    "SubtitleStreamList":{
                                        "SubtitleStream":[
                                            {
                                                "Index":"3",
                                                "Lang":"eng"
                                            }
                                        ]
                                    }
                                },
                                "Format":{
                                    "NumStreams":"1",
                                    "NumPrograms":"2",
                                    "FormatName":"matroska,webm",
                                    "FormatLongName":"Matroska / WebM",
                                    "StartTime":"0.042000",
                                    "Duration":"17.600000",
                                    "Size":"70569598",
                                    "Bitrate":"32077090"
                                }
                          },
                        "UserData":"testid-001" 
                },
                "State": "TranscodeSuccess",
                "Code": "",
                "Message": "",
                "Percent": 100,
                "PipelineId": "88c6ca184c0e47098a5b665e2a126797",
                "CreationTime":"2014-01-10T12:00:00Z"
            }]
        },
     "RequestId":"06CB45EF-903C-4464-A812-AD276948D5BB"
    }
```

