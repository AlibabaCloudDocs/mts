# AddWaterMarkTemplate {#reference_f5q_w4t_x2b .reference}

The AddWaterMarkTemplate API creates a watermark template.

## Request parameters {#section_iqn_qbt_x2b .section}

|Parameters|Type|Required or not|Description|
|:---------|:---|:--------------|:----------|
|Action|String|Yes|API of the action, system required parameter. Value: AddWaterMarkTemplate|
|Name|String|Yes|Template name.Up to 128 bytes.

|
|Config|String|Yes|Watermark template configuration.-   JSON object. For details, see “5. WaterMarkConfig” in Parameters” of “Appendix.”
-   Example: `{``"Width":"10",``"Height":"30",``"Dx":"10",``"Dy":"5",``"ReferPos":"TopRight",``"Type":"Image",``"Timeline":{"Start":"0", "Duration":"10"}``}`

|

## Response parameters {#section_ogh_wbt_x2b .section}

|Parameter|Type|Description|
|:--------|:---|:----------|
|WaterMarkTemplate|AliyunWaterMarkTemplate|Watermark template|

## Examples {#section_gpq_zbt_x2b .section}

Request example

```
http://mts.cn-hangzhou.aliyuncs.com/?Name=example-watermark&Config=%7B%22Width%22%3A%2210%22%2C%22Height%22%3A%2230%22%2C%22Dx%22%3A%2210%22%2C%0A%22Dy%22%3A%225%22%2C%22ReferencePos%22%3A%22TopRight%22%2C%0A%22Type%22%3A%22Image%22%7D%0A&Action=AddWaterMarkTemplate&<Public parameter>
```

Response example

XML

```
<AddWaterMarkTemplateResponse>
    <RequestId>25818875-5F78-4A13-BEF6-D7393642CA58</RequestId>
    <WaterMarkTemplate>
        <Id>88c6ca184c0e47098a5b665e2a126797</Id>
        <Name>example-watermark</Name>
        <Width>10</Width>
        <Height>30</Height>
        <Dx>10</Dx>
        <Dy>5</Dy>
        <ReferPos>TopRight</ReferPos>
        <Type>Image</Type>
        <State>Normal</State>
    </WaterMarkTemplate>
    </AddWaterMarkTemplateResponse>
```

JSON

```
{
      "RequestId": "25818875-5F78-4A13-BEF6-D7393642CA58",
      "WaterMarkTemplate": {
            "Id": "88c6ca184c0e47098a5b665e2a126797",
            "Name": "example-watermark",
            "Width": "10",
            "Height": "30",
            "Dx": "10",
            "Dy": "5",
            "ReferPos": "TopRight",
            "Type": "Image",
            "State": "Normal"
        }
    }
```

