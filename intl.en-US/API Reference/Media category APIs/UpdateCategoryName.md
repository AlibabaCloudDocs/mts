# UpdateCategoryName {#reference_vfh_kph_y2b .reference}

The UpdateCategoryName API updates a category name.

## Request parameters {#section_iqn_qbt_x2b .section}

|Parameters|Type|Required or not|Description|
|:---------|:---|:--------------|:----------|
|Action|String|Yes|API of the action, system required parameter. Value: UpdateCategoryName|
|CateId|String|Yes|Category ID.|
|CateName|String|Yes|Category name,-   which consists of up to 64 bytes.
-   UTF-8 encoding.

|

## Response parameters {#section_ogh_wbt_x2b .section}

None

## Examples {#section_gpq_zbt_x2b .section}

Request example

```
http://mts.cn-hangzhou.aliyuncs.com?CateId=7503631&&CateName=%E5%B0%91%E5%84%BF%E4%B8%8D%E5%AE%9C&<public parameter>
```

Response example

XML

```
<UpdateCategoryNameResponse>
  <RequestId>69310704-DC96-44C2-8B70-58048020EA7E</RequestId>
</UpdateCategoryNameResponse>
```

JSON

```
{
  "Requestid": 69310704-DC96-44C2-8B70-58048020EA7E"
  }
```

