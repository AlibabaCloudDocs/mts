# QueryTemplateList {#reference_nwl_1mt_x2b .reference}

The QueryTemplateList API queries custom templates. This API can be used to query details about transcoding templates using custom template IDs.

## Request parameters {#section_iqn_qbt_x2b .section}

|Parameters|Type|Required or not|Description|
|:---------|:---|:--------------|:----------|
|Action|String|Yes|API of the action, system required parameter. Value: QueryTemplateList|
|TemplateIds|String|Yes|List of template IDs separated by commas \(,\).A maximum of 10 template IDs can be entered.

|

## Response parameters {#section_ogh_wbt_x2b .section}

|Parameter|Type|Description|
|:--------|:---|:----------|
|TemplateList|AliyunTemplate\[ \]|List of transcoding templates.|
|NonExistTids|String\[ \]|List of non-existing transcoding templates. If no data exists, this structure is not returned.|

## Examples {#section_gpq_zbt_x2b .section}

Request example

```
http://mts.cn-hangzhou.aliyuncs.com/?TemplateIds=88c6ca184c0e47098a5b665e2a126799&Action=QueryTemplateList&<Public parameter>
```

Response example

XML

```
<QueryTemplateListResponse>
    <RequestId>017F1B2D-2B5B-4441-ABBA-E0DC08F5AFEC</RequestId>
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
    </QueryTemplateListResponse>
```

JSON

```
{
     "RequestId":"3E767BAD-9F4C-4FC8-9FAE-E3F4A639066B",
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
                    "Codec": "AAC",
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

