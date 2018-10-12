# DeleteMediaTag {#reference_b3f_bmh_y2b .reference}

The DeleteMediaTag API deletes a media tag.

## Request parameters {#section_iqn_qbt_x2b .section}

|Parameters|Type|Required or not|Description|
|:---------|:---|:--------------|:----------|
|Action|String|Yes|API of the action, system required parameter. Value: DeleteMediaTag|
|MediaId|String|Yes|Media ID.|
|Tag|String|Yes|Media tags, which consists of up to 32 UTF-8 encoded bytes.|

## Response parameters {#section_ogh_wbt_x2b .section}

None

## Examples {#section_gpq_zbt_x2b .section}

Request example

```
http://mts.cn-hangzhou.aliyuncs.com?Tag=tag1&MediaId=3e6149d5a8c944c09b1a8d2dc3e4ac65&<public parameter>
```

Response example

XML

```
<DeleteMediaTagResponse>
          <RequestId>1B8D2461-60D2-41B4-B9DA-FC8AC40B559D</RequestId>
  </DeleteMediaTagResponse>
```

JSON

```
{
    "RequestId":"1B8D2461-60D2-41B4-B9DA-FC8AC40B559D"
    }
```

