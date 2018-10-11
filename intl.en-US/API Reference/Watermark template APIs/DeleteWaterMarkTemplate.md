# DeleteWaterMarkTemplate {#reference_ny1_dmg_y2b .reference}

The DeleteWaterMarkTemplate API deletes a watermark template. If the watermark template is being used by “Submitted” tasks, the template cannot be deleted.

## Request parameters {#section_iqn_qbt_x2b .section}

|Parameters|Type|Required or not|Description|
|:---------|:---|:--------------|:----------|
|Action|String|Yes|API of the action, system required parameter. Value: DeleteWaterMarkTemplate|
|WaterMarkTemplateId|String|Yes|Watermark template ID.|

## Response parameters {#section_ogh_wbt_x2b .section}

|Parameter|Type|Description|
|:--------|:---|:----------|
|WaterMarkTemplateId|String|Watermark template ID|

## Examples {#section_gpq_zbt_x2b .section}

Request example

```
http://mts.cn-hangzhou.aliyuncs.com/?WaterMarkTemplateId=88c6ca184c0e47098a5b665e2a126799&Action=DeleteWaterMarkTemplate&<Public parameter>
```

Response example

XML

```
<DeleteWaterMarkTemplateResponse>
    <RequestId>017F1B2D-2B5B-4441-ABBA-E0DC08F5AFEC</RequestId>
    <WaterMarkTemplateId>88c6ca184c0e47098a5b665e2a126799</WaterMarkTemplateId>
    </DeleteWaterMarkTemplateResponse>
```

JSON

```
{  
     "RequestId":"3E767BAD-9F4C-4FC8-9FAE-E3F4A639066B",
     "WaterMarkTemplateId": "88c6ca184c0e47098a5b665e2a126799"
    }
```

