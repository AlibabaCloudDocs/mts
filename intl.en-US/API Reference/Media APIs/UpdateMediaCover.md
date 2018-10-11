# UpdateMediaCover {#reference_gdj_pyg_y2b .reference}

The UpdateMediaCover API updates the media cover.

## Request parameters {#section_iqn_qbt_x2b .section}

|Parameters|Type|Required or not|Description|
|:---------|:---|:--------------|:----------|
|Action|String|Yes|API of the action, system required parameter. Value: UpdateMediaCover|
|MediaId|String|Yes|Media ID.|
|CoverURL|String|No|Media cover.-   The URL format follows the RFC 2396 standard and is subject to UTF-8 encoding and URL encoding. A URL consists of up to 3,200 bytes.

|

## Response parameters {#section_ogh_wbt_x2b .section}

|Parameter|Type|Description|
|:--------|:---|:----------|
|Media|[Media](https://help.aliyun.com/document_detail/29251.html#Media)|Media|

## Examples {#section_gpq_zbt_x2b .section}

Request example

```
http://mts.cn-hangzhou.aliyuncs.com?CoverURL=http%3A%2F%2Fzzyoutputbucket.oss-cn-hangzhou.aliyuncs.com%2F47b42486019c4f688bf144c1a6ba059a%252F0.jpg&MediaId=3e1cd21131a94525be55acf65888bf46&<public parameter>
```

Response example

XML

```
<UpdateMediaCoverResponse>
     <RequestId>4BEB6635-FB40-4C26-B116-1CEE997FF99F</RequestId>
   </UpdateMediaCoverResponse>
```

JSON

```
{
    "RequestId":"5428F518-F18E-440D-A000-5667C48599CF"
    }
```

