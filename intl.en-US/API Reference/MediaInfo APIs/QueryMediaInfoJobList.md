# QueryMediaInfoJobList {#reference_ez1_4bt_x2b .reference}

The QueryMediaInfoJobList API queries information about MediaInfo tasks.

## Request parameters {#section_iqn_qbt_x2b .section}

|Parameter|Type|Required or not|Description|
|:--------|:---|:--------------|:----------|
|Action|String|Yes|API of the action, system required parameter. Value: QueryMediaInfoJobList|
|MediaInfoJobIds|String|Yes|List of MediaInfo task IDs.Separated by commas \(,\). A maximum of 10 MediaInfo task IDs can be entered at a time.Comma separated, with a maximum of 10 queries at a time.

|

## Response parameters {#section_ogh_wbt_x2b .section}

|Parameter|Type|Description|
|:--------|:---|:----------|
|Mediainfojoblist|AliyunMediaInfoJob\[ \]|MediaInfo task list.|
|NonExistMediaInfoJobIds|String\[ \]|List of non-existing MediaInfo task IDs. If no data exists, this structure is not returned.|

## Examples {#section_gpq_zbt_x2b .section}

Request example

```
http://mts.cn-hangzhou.aliyuncs.com/?Action=QueryMediaInfoJobList&MediaInfoJobIds=88c6ca184c0e47098a5b665e2a126797<Public Parameters>
```

Response example

XML

```
<QueryMediaInfoJobListResponse>
        <RequestId>25818875-5F78-4A13-BEF6-D7393642CA58</RequestId>
        <MediaInfoJobList list="true">
            <MediaInfoJob>
                <JobId>88c6ca184c0e47098a5b665e2a126797</JobId>
                <Input>
                    <Bucket>example-bucket</Bucket>
                    <Location>oss-cn-hangzhou</Location>
                    <Object>example.flv</Object>
                </Input>
                <UserData>testid-001</UserData>
                <State>Analyzing</State>
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
                <Code> </Code>
                <Message> </Message>
                <PipelineId>88c6ca184c0e47098a5b665e2a126797</PipelineId>
                <CreationTime>2014-01-10T12:00:00Z</CreationTime>
            </MediaInfoJob>
        </MediaInfoJobList>
    </QueryMediaInfoJobListResponse>
```

JSON

```
{
     "RequestId": "25818875-5F78-4A13-BEF6-D7393642CA58",
     "MediaInfoJobList":{
             "MediaInfoJob": [{
                 "JobId": "88c6ca184c0e47098a5b665e2a126797",
                 "Input": {
                         "Bucket": "example-bucket",
                         "Location": "oss-cn-hangzhou",
                         "Object": "example.flv"
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
                 "UserData":"testid-001",
                 "State": "Analyzing",
                 "Code": "",
                 "Message": "",
                 "PipelineId": "88c6ca184c0e47098a5b665e2a126797",
                 "CreationTime”:”2014-01-10T12:00:00Z"
            }]
       }
    }
```

