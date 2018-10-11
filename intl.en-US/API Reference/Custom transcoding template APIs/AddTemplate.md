# AddTemplate {#reference_ksb_hkt_x2b .reference}

The AddTemplate API creates a custom template, which includes the container information, and settings such as video and audio stream settings. If some information is not set in the template, bitstreams that are transcoded using the template do not contain such information.

## Request parameters {#section_iqn_qbt_x2b .section}

|Parameters|Type|Required or not|Description|
|:---------|:---|:--------------|:----------|
|Action|String|Yes|API of the action, system required parameter. Value: AddTemplate|
|Parameter|String|Yes|Template name.Up to 128 bytes.

|
|Container|String|No|Container.-   -   JSON object. For details, see “7. Container” in “Parameters” of “Appendix.”
-   Example: `{"Format":"mp4"}`

|
|Video|String|No|Video stream configuration.-   JSON object. For details, see “8. Video” in “Parameters” of “Appendix.”
-   Example: `{``"Codec":"H. 264",``"Profile":"high",``"Bitrate":"500",``"Crf":"15",``"Width":"256",``"Height":"800",``"Fps":"25",``"Gop":"10"``}`

**Note:** If the Video parameter is not set, video streams are not output after transcoding. If you want to retain the video, the Video parameter must be set.

|
|Audio|String|No|Audio stream configuration.-   JSON object. For details, see “10. Audio” in “Parameters” of “Appendix.”
-   Example: `{``"Codec":"aac",``"Samplerate":"44100",``"Bitrate":"500",``"Channels":"2"``}`

**Note:** If the Audio parameter is not set, audio streams are not output after transcoding. If you want to retain the audio, the Audio parameter must be set.

|
|TransConfig|String|No|General transcoding configuration.-   JSON object. For details, see “16. TransConfig” in “Parameters” of “Appendix.”
-   Example: `{``"TransMode":"onepass"``}`

|
|MuxConfig|String|No|Encapsulation configuration-   JSON object. For details, see “17. MuxConfig” in “Parameters” of “Appendix.”
-   Example: `{``"Segment":{``"Duration":"12"``}``}`

|

## Response parameters {#section_ogh_wbt_x2b .section}

|Parameter|Type|Description|
|:--------|:---|:----------|
|Template|AliyunTemplate|Transcoding template|

## Examples {#section_gpq_zbt_x2b .section}

Request example

```
http://mts.cn-hangzhou.aliyuncs.com/?Container=%7B%22Format%22%3A%22mp4%22%7D&Video=%7B%22Codec%22%3A%20%22H. 264%22%2C%22Profile%22%3A%20%22high%22%2C%20%22BitRate%22%3A%20%22500%EF%BC%8C%22CRF%22%3A%20%2215%22%2C%20%22Width%22%3A%20%22256%22%2C%22Height%22%3A%20%22800%22%2C%20%22FPS%22%3A%20%2225%22%2C%20%22GOP%22%3A%20%2210%22%20%7D&Audio=%7B%22Codec%22%3A%22aac%22%2C%22SampleRate%22%3A%2244100%22%2C%0A%22BitRate%22%3A%22500%22%2C%22Channels%22%3A%222%22%7D%0A&Action=AddTemplate&<Public parameter>
```

Return example

XML

```
<AddTemplateResponse>
    <RequestId>017F1B2D-2B5B-4441-ABBA-E0DC08F5AFEC</RequestId>
        <Template>
            <Id>88c6ca184c0e47098a5b665e2a126799</Id>
            <Name>MTS-example</Name>
            <Container>
                <Format>mp4</Format>
            </Container>
            <Video>
                <Codec>H. 264</Codec>
                <Profile>high</Profile>
                <Bitrate>Auto</Bitrate>
                <Crf>15</Crf>
                <Width>256</Width>
                <Height>800</Height>
                <Fps>25</Fps>
                <Gop>10</Gop>
                <Preset>lower</Preset>
                <ScanMode></ScanMode>
                <Bufsize>6000</Bufsize>
                <Maxrate></Maxrate>
                <BitrateBnd>
                   <Max></Max>
                   <Min></Min>
                </BitrateBnd>
            </Video>
            <Audio>
                <Codec>aac</Codec>
                <Samplerate>44100</Samplerate>
                <Bitrate>500</Bitrate>
                <Channels>2</Channels>
            </Audio>
            <TransConfig>
                 <TransMode>onepass</TransMode>
            </TransConfig>
            <State>Normal</State>
        </Template>
    </AddTemplateResponse>
```

JSON

```
{
     "RequestId":"3E767BAD-9F4C-4FC8-9FAE-E3F4A639066B",
     "Template": {
                "Id": "88c6ca184c0e47098a5b665e2a126799",
                "Name": "MTS-example",
                "Container": {
                    "Format": "mp4"
                    },
                "Video": {
                    "Codec": "H. 264",
                    "Profile": "high",
                    "Bitrate": "Auto",
                    "Crf": "15",
                    "Width": "256",
                    "Height": "800",
                    "Fps": "25",
                    "Gop": "10",
                    "Preset": "lower",
                    "ScanMode": "",
                    "Bufsize": "6000",
                    "Maxrate": "500",
                    "BitrateBnd":{
                        "Max":"",
                        "Min":""
                    }
                    },
                "Audio": {
                    "Codec": "aac",
                    "Samplerate": "44100",
                    "Bitrate": "500",
                    "Channels": "2"
                    },
                "TransConfig":{
                    "TransMode":"onepass"
                },
                "State": "Normal"           
                }
            }
    }
```

