# UpdateWaterMarkTemplate {#reference_qqz_bjg_y2b .reference}

The UpdateWaterMarkTemplate API updates the name and configurations of a specified watermark template. If the watermark template to be updated is used by “Submitted” tasks, the template cannot be updated.

## Request parameters {#section_iqn_qbt_x2b .section}

|Parameters|Type|Required or not|Description|
|:---------|:---|:--------------|:----------|
|Action|String|Yes|API of the action, system required parameter. Value: UpdateWaterMarkTemplate|
|WaterMarkTemplateId|String|Yes|Watermark template ID.|
|Name|String|Yes|Template name.Up to 128 bytes.

|
|Config|String|Yes|Watermark template configurations.-   JSON object. For details, see “5. WaterMarkConfig” in Parameters” of “Appendix.”
-   Example: `{``"Width":"10px",``"Height":"30px",``"Dx":"10px",``"Dy":"5px",``"Type":"Image",``"Timeline":{"Start":"0", "Duration":"10"}``}`

|

## Response parameters {#section_ogh_wbt_x2b .section}

|Parameter|Type|Description|
|:--------|:---|:----------|
|WaterMarkTemplate|AliyunWaterMarkTemplate|Watermark template|

## Examples {#section_gpq_zbt_x2b .section}

Request example

```
http://mts.cn-hangzhou.aliyuncs.com/?WaterMarkTemplateId=88c6ca184c0e47098a5b665e2a126797&Name=example-watermark&Config=%7B%22Width%22%3A%20%2210px%22%2C%22Height%22%3A%20%2230px%22%2C%22Dx%22%3A%20%2210px%22%2C%22Dy%22%3A%225px%22%2C%22ReferencePos%22%3A%0A%22TopRight%22%2C%22Type%22%3A%22Image%22%7D%0A&Action=UpdateWaterMarkTemplate&<Public parameter>
```

Response example

XML

```
<UpdateWaterMarkTemplateResponse>
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
    </UpdateWaterMarkTemplateResponse>
```

JSON

```
{
     "RequestId":"25818875-5F78-4A13-BEF6-D7393642CA58",
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

