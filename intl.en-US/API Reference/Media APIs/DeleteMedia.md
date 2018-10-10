# DeleteMedia {#reference_kmk_hxg_y2b .reference}

The DeleteMedia API deletes media. This API only deletes media logically, but does not delete the input/output physical files stored in OSS buckets.

## Request parameters {#section_iqn_qbt_x2b .section}

|Parameter|Type|Required or not|Description|
|:--------|:---|:--------------|:----------|
|Action|String|Yes|API of the action, system required parameter. Value: DeleteMedia|
|MediaIds|String|Yes|Media ID list,separated by commas \(,\). A maximum of 10 media IDs can be entered at a time.

|

## Response parameters {#section_ogh_wbt_x2b .section}

None

## Examples {#section_gpq_zbt_x2b .section}

Request example

```
http://mts.cn-hangzhou.aliyuncs.com?MediaIds=3e1cd21131a94525be55acf65888bf46&<public parameter>
```

Response example

XML

```
<DeleteMediaResponse>
       <RequestId>CFEF84B7-A57F-480F-B7FD-E0A649C76086</RequestId>
    </DeleteMediaResponse>
```

JSON

```
{
    "RequestId":"CFEF84B7-A57F-480F-B7FD-E0A649C76086"
    }
```

