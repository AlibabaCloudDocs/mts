# ActivateMediaWorkflow {#reference_o5t_y4g_y2b .reference}

The ActivateMediaWorkflow API activates a media workflow. If a media workflow is activated, it cannot be modified.

## Request parameters {#section_iqn_qbt_x2b .section}

|Parameters|Type|Required or not|Description|
|:---------|:---|:--------------|:----------|
|Action|String|Yes|API of the action, system required parameter. Value: ActivateMediaWorkflow|
|MediaWorkflowId|String|Yes|Media workflow ID|

## Response parameters {#section_ogh_wbt_x2b .section}

None

## Examples {#section_gpq_zbt_x2b .section}

Request example

```
https://mts.cn-hangzhou.aliyuncs.com/?MediaWorkflowId=93ab850b4f6f44eab54b6e91d24d81d4&<public parameter>
```

Response example

XML

```
<ActivateMediaWorkflowResponse>
     <RequestId>A1326BD4-30B1-4CB6-B116-3330B877B0D4</RequestId>
</ActivateMediaWorkflowResponse>
```

JSON

```
{
     "RequestId":"A1326BD4-30B1-4CB6-B116-3330B877B0D4"    
 }
```

