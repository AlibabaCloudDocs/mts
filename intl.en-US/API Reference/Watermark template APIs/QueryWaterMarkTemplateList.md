# QueryWaterMarkTemplateList {#reference_g5g_tkg_y2b .reference}

The QueryWaterMarkTemplateList API queries details about watermark templates by watermark template ID.

## Request parameters {#section_iqn_qbt_x2b .section}

|Parameters|Type|Required or not|Description|
|:---------|:---|:--------------|:----------|
|Action|String|Yes|API of the action, system required parameter. Value: QueryWaterMarkTemplateList|
|WaterMarkTemplateIds|String|Yes|List of watermark template IDs separated by commas \(,\).Up to 10 template IDs can be entered.

|

## Response parameters {#section_ogh_wbt_x2b .section}

|Parameter|Type|Description|
|:--------|:---|:----------|
|WaterMarkTemplateList|AliyunWaterMarkTemplate\[ \]|List of watermark templates.|
|NonExistWids|String\[ \]|List of non-existing watermark templates. If no data exists, this structure is not returned.|

## Examples {#section_gpq_zbt_x2b .section}

Request example

```
http://mts.cn-hangzhou.aliyuncs.com/?WaterMarkTemplateIds=88c6ca184c0e47098a5b665e2a126797&Action=QueryWaterMarkTemplateList&<Public parameter>
```

Response example

XML

```
<QueryWaterMarkTemplateListResponse>
    <RequestId>25818875-5F78-4A13-BEF6-D7393642CA58</RequestId>
    <TotalCount>1</TotalCount>
    <PageNumber>1</PageNumber>
    <PageSize>10</PageSize>
    <WaterMarkTemplateList list="true">
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
    </WaterMarkTemplateList>
    </QueryWaterMarkTemplateListResponse>
```

JSON

```
{
     "RequestId": "25818875-5F78-4A13-BEF6-D7393642CA58",
        "TotalCount": 1,
        "PageNumber": 1,
        "PageSize": 10,
        "WaterMarkTemplateList": {
            "WaterMarkTemplate": [{
                "Id": "88c6ca184c0e47098a5b665e2a126797",
                "Name": "example-watermark",
                "Width": "10",
                "Height": "30",
                "Dx": "10",
                "Dy": "5",
                "ReferPos": "TopRight",
                "Type": "Image",
                "State": "Normal"
                }]
       }
    }
```

