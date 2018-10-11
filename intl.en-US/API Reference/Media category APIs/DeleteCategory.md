# DeleteCategory {#reference_sdx_2ph_y2b .reference}

The DeleteCategory API deletes a category.

## Request parameters {#section_iqn_qbt_x2b .section}

|Parameters|Type|Required or not|Description|
|:---------|:---|:--------------|:----------|
|Action|String|Yes|API of the action, system required parameter. Value: DeleteCategory|
|CateId|Long|Yes|Category ID.|

## Response parameters {#section_ogh_wbt_x2b .section}

None

## Examples {#section_gpq_zbt_x2b .section}

Request example

```
http://mts.cn-hangzhou.aliyuncs.com?CateId=7503631&<public parameter>
```

Response example

XML

```
<DeleteCategoryResponse>
  <RequestId>79B1A82B-C299-49E9-AB67-189E0C1CEC49</RequestId>
</DeleteCategoryResponse>
```

JSON

```
{
  "RequestId":"79B1A82B-C299-49E9-AB67-189E0C1CEC49"
  }
```

