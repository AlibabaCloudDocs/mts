# SearchTemplate {#reference_u1p_lmt_x2b .reference}

The SearchTemplate API searches for custom templates in the specified state.

## Request parameters {#section_iqn_qbt_x2b .section}

|Parameters|Type|Required or not|Description|
|:---------|:---|:--------------|:----------|
|Action|String|Yes|API of the action, system required parameter. Value: SearchTemplate|
|PageNumber|Long|No|Current page number,-   which starts from 1.
-   Default value: 1.

|
|PageSize|Long|No|When querying by page, this parameter indicates the size of each page.-   Maximum value is 100.
-   Default value: 10.

|
|State|String|No|Transcoding template status.-   All indicates all states,
-   Normal indicates normal templates,
-   and Deleted indicates deleted templates.

Default value: All.

|

## Response parameters {#section_ogh_wbt_x2b .section}

|Parameter|Type|Description|
|:--------|:---|:----------|
|TemplateList|AliyunTemplate\[ \]|Template list|

## Examples {#section_gpq_zbt_x2b .section}

Request example

```
http://mts.cn-hangzhou.aliyuncs.com/?Action=SearchTemplate&<Public parameter>
```

Response example

XML

```
<SearchTemplateResponse>
    <RequestId>017F1B2D-2B5B-4441-ABBA-E0DC08F5AFEC</RequestId>
    <TotalCount>1</TotalCount>
    <PageNumber>1</PageNumber>
    <PageSize>10</PageSize>
    <TemplateList list="true">
        <Template>
            <Id>88c6ca184c0e47098a5b665e2a126799</Id>
            <Name>MTS-example</Name>
            <Container>
                <Format>mp4</Format>
            </Container>
            <Video>
                <Codec>H. 264</Codec>
                <Profile>high</Profile>
                <Bitrate>500</Bitrate>
                <Crf>Auto</Crf>
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
                <Bitrate>Auto</Bitrate>
                <Channels>Auto</Channels>
            </Audio>
            <TransConfig>
                 <TransMode>fixCRF</TransMode>
            </TransConfig>
            <State>Normal</State>
        </Template >
    </TemplateList>
    </SearchTemplateResponse>
```

JSON

```
{
     "RequestId":"3E767BAD-9F4C-4FC8-9FAE-E3F4A639066B",
     "PageNumber":1,
     "PageSize":10,
     "TotalCount":1,
     "TemplateList": {
            "Template": [{
                "Id": "88c6ca184c0e47098a5b665e2a126799",
                "Name": "MTS-example",
                "Container": {
                    "Format": "mp4"
                    },
                "Video": {
                    "Codec": "H. 264",
                    "Profile": "high",
                    "Bitrate": "500",
                    "Crf": "Auto",
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
                    " Samplerate": "44100",
                    "Bitrate": "Auto",
                    "Channels": "Auto"
                    },
                "TransConfig":{
                    "TransMode":"fixCRF"
                },
                "State": "Normal"
                }]
            }
    }
```

