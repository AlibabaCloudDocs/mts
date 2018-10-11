# CategoryTree {#reference_x35_qph_y2b .reference}

The CategoryTree API retrieves a category tree.

## Request parameters {#section_iqn_qbt_x2b .section}

|Parameters|Type|Required or not|Description|
|:---------|:---|:--------------|:----------|
|Action|String|Yes|API of the action, system required parameter. Value: CategoryTree|

## Response parameters {#section_ogh_wbt_x2b .section}

|Parameter|Type|Description|
|:--------|:---|:----------|
|CategoryTree|String|Category tree|

## Examples {#section_gpq_zbt_x2b .section}

Request example

```
http://mts.cn-hangzhou.aliyuncs.com/?Action=CategoryTree&<publiv parameter>
```

Response example

XML

```
<CategoryTreeResponse>
      <CategoryTree>[{"CateId":3659747,"CateName":"Adult education","ParentId":-1,"Level":0,"SubcateList":[{"CateId":8102754,"CateName":"aaa","ParentId":3659747,"Level":1}]},{"CateId":4154805,"CateName":"this is a new cate","ParentId":-1,"Level":0},{"CateId":7503631,"CateName":"Not suitable for children","ParentId":-1,"Level":0}]</CategoryTree>
      <RequestId>A68615EA-0CF5-420E-AB19-ACFABF794745</RequestId>
    </CategoryTreeResponse>
```

JSON

```
{
    "CategoryTree": "[{\"CateId\":3659747,\"CateName\":\"Adult education\",\"ParentId\":-1,\"Level\":0,\"SubcateList\":[{\"CateId\":8102754,\"CateName\":\"aaa\",\"ParentId\":3659747,\"Level\":1}]},{\"CateId\":4154805,\"CateName\":\"this is a new cate\",\"ParentId\":-1,\"Level\":0},{\"CateId\":7503631,\"CateName\":\"Not suitable for children\",\"ParentId\":-1,\"Level\":0}]", 
    "RequestId": "B74DFDF2-3214-43FD-9051-4E1A1544CF92"
  }
```

