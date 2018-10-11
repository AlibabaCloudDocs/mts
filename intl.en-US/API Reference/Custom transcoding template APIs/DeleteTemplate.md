# DeleteTemplate {#reference_nqp_1nt_x2b .reference}

The DeleteTemplate API deletes a custom template. If the custom transcoding template to be deleted is used by “Submitted” tasks, the template cannot be deleted.

## Request parameters {#section_iqn_qbt_x2b .section}

|Parameters|Type|Required or not|Description|
|:---------|:---|:--------------|:----------|
|Action|String|Yes|API of the action, system required parameter. Value: DeleteTemplate|
|TemplateId|String|Yes|Template ID.|

## Response parameters {#section_ogh_wbt_x2b .section}

|Parameter|Type|Description|
|:--------|:---|:----------|
|TemplateId|String|Template ID|

## Examples {#section_gpq_zbt_x2b .section}

Request example

```
http://mts.cn-hangzhou.aliyuncs.com/?TemplateId=88c6ca184c0e47098a5b665e2a126799&Action=DeleteTemplate&<Public parameter>
```

Response example

XML

```
<DeleteTemplateResponse>
    <RequestId>017F1B2D-2B5B-4441-ABBA-E0DC08F5AFEC</RequestId>
    <TemplateId>88c6ca184c0e47098a5b665e2a126799</TemplateId>
    </DeleteTemplateResponse>
```

JSON

```
{
     "RequestId":"3E767BAD-9F4C-4FC8-9FAE-E3F4A639066B",
     "TemplateId": "88c6ca184c0e47098a5b665e2a126799"
    }
```

