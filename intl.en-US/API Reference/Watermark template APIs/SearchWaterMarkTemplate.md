# SearchWaterMarkTemplate {#reference_d4v_2lg_y2b .reference}

The SearchWaterMarkTemplate API searches for watermark templates in the specified state.

## Request parameters {#section_iqn_qbt_x2b .section}

|Parameters|Type|Required or not|Description|
|:---------|:---|:--------------|:----------|
|Action|String|Yes|API of the action, system required parameter. Value: SearchWaterMarkTemplate|
|PageNumber|Long|No|Current page number,-   which starts from 1.
-   Default value: 1.

|
|PageSize|Long|No|When querying by page, this parameter indicates the size of each page.-   Maximum value: 100.
-   Default value: 10.

|
|State|String|No|Watermark template status.-   All indicates all states,
-   Normal indicates normal templates,
-   and Deleted indicates deleted templates.

Default value: All.

|

## Response parameters {#section_ogh_wbt_x2b .section}

|Name|Type|Description|
|:---|:---|:----------|
|WaterMarkTemplateList|AliyunWaterMarkTemplate\[ \]|List of watermark templates|

## Examples {#section_gpq_zbt_x2b .section}

Request example

```
http://mts.cn-hangzhou.aliyuncs.com/?Action=SearchWaterMarkTemplate&<Public parameter
```

Response example

XML

```
<SearchWaterMarkTemplateResponse>
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
    </SearchWaterMarlateResponse>
JSON
```

JSON

```
{
     "RequestId": "25818875-5F78-4A13-BEF6-D7393642CA58",
        "TotalCount": 100,
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

