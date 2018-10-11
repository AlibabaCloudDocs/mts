# UpdateMediaCategory {#reference_hj3_jyg_y2b .reference}

The UpdateMediaCategory API updates media categories.

## Request parameters {#section_iqn_qbt_x2b .section}

|Parameters|Type|Required or not|Description|
|:---------|:---|:--------------|:----------|
|Action|String|Yes|API of the action, system required parameter. Value: UpdateMediaCategory|
|MediaId|String|Yes|Media ID.|
|CateId|Long|No|Category ID, which cannot be a negative number.|

## Response parameters {#section_ogh_wbt_x2b .section}

|Parameter|Type|Description|
|:--------|:---|:----------|
|Media|[Media](https://help.aliyun.com/document_detail/29251.html#Media)|Media|

## Examples {#section_gpq_zbt_x2b .section}

Request example

```
http://mts.cn-hangzhou.aliyuncs.com?MediaId=3e1cd21131a94525be55acf65888bf46&<public parameter>
```

Response example

XML

```
<UpdateMediaCategoryResponse>
      <RequestId>E3931857-E3D3-4D6E-9C7B-D2C09441BD01</RequestId>
    </UpdateMediaCategoryResponse>
```

JSON

```
{
    "RequestId":"894A984A-CEC2-4784-B899-77A7414FD159"
    }
```

