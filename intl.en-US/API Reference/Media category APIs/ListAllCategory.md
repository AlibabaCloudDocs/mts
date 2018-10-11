# ListAllCategory {#reference_g21_wph_y2b .reference}

The ListAllCategory API retrieves a category list.

## Request parameters {#section_iqn_qbt_x2b .section}

|Parameters|Type|Required or not|Description|
|:---------|:---|:--------------|:----------|
|Action|String|Yes|API of the action, system required parameter. Value: ListAllCategory|

## Response parameters {#section_ogh_wbt_x2b .section}

|Parameter|Type|Description|
|:--------|:---|:----------|
|Category|[Category](https://help.aliyun.com/document_detail/29251.html#Category)\[\]|Category information|

## Examples {#section_gpq_zbt_x2b .section}

Request example

```
http://mts.cn-hangzhou.aliyuncs.com?SAction=ListAllCategory&<public parameter>
```

Response example

XML

```
<ListAllCategoryResponse>
  <RequestId>A7327D37-65F2-45BC-BD97-E5522BE3E5B9</RequestId>
  <CategoryList>
    <Category>
      <ParentId>-1</ParentId>
      <CateId>3659747</CateId>
      <CateName>Adult education</CateName>
      <Level>0</Level>
    </Category>
    <Category>
      <ParentId>-1</ParentId>
      <CateId>4154805</CateId>
      <CateName>this is a new cate</CateName>
      <Level>0</Level>
    </Category>
    <Category>
      <ParentId>-1</ParentId>
      <CateId>7503631</CateId>
      <CateName>Not suitable for children</CateName>
      <Level>0</Level>
    </Category>
    <Category>
      <ParentId>3659747</ParentId>
      <CateId>8102754</CateId>
      <CateName>aaa</CateName>
      <Level>1</Level>
    </Category>
  </CategoryList>
</ListAllCategoryResponse>
```

JSON

```
{
    "RequestId": "533A9B93-7CB4-4712-9065-A8A77E34F333", 
    "CategoryList": {
        "Category": [
            {
                "ParentId": -1, 
                "CateId": 3659747, 
                "CateName": "Adult education", 
                "Level": 0
            }, 
            {
                "ParentId": -1, 
                "CateId": 4154805, 
                "CateName": "this is a new cate", 
                "Level": 0
            }, 
            {
                "ParentId": -1, 
                "CateId": 7503631, 
                "CateName": "Not suitable for children", 
                "Level": 0
            }, 
            {
                "ParentId": 3659747, 
                "CateId": 8102754, 
                "CateName": "aaa", 
                "Level": 1
            }
        ]
    }
}
```

