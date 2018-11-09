# 查询媒体Bucket {#reference_a5b_5qh_y2b .reference}

列出媒体库所有媒体Bucket。

## 请求参数 {#section_iqn_qbt_x2b .section}

|名称|类型|是否必须|描述|
|:-|:-|:---|:-|
|Action|String|是|操作接口名，系统规定参数，取值：ListAllMediaBucket|
|NextPageToken |String|否|下一页标识。第一次请求，服务会返回此token，第二次请求带上即可。|
|MaximumPageSize|Integer|否|本次请求可返回的媒体bucket数目最大值。-   范围：\[1,100\]
-   默认值：50

|

## 返回参数 {#section_ogh_wbt_x2b .section}

|名称|类型|描述|
|:-|:-|:-|
|MediaBucket|[MediaBucket](intl.zh-CN/API参考/数据类型.md#)\[\]|媒体Bucket列表|
|NextPageToken|String|查询下一页标识。|

## 示例 {#section_gpq_zbt_x2b .section}

请求示例

```
http://mts.cn-hangzhou.aliyuncs.com?Action=ListAllMediaBucket&<公共参数>
```

返回示例

XML

```
<ListAllMediaBucketResponse>
      <RequestId>79760D91-D3CF-4165-8068-B7E2836EF62A</RequestId>
      <NextPageToken>BohcFbNNj7F0RcUsHx44Qx</NextPageToken>
      <MediaBucketList>
        <MediaBucket>
          <Type>Input</Type>
          <Bucket>watermark-zzz</Bucket>
        </MediaBucket>
        <MediaBucket>
          <Type>Output</Type>
          <Bucket>zzyoutputbucket</Bucket>
        </MediaBucket>
        <MediaBucket>
          <Type>Input</Type>
          <Bucket>zzzinput-test</Bucket>
        </MediaBucket>
      </MediaBucketList>
    </ListAllMediaBucketResponse>
```

JSON

```
{
    "RequestId": "50B35FE9-18B2-45D6-B8C4-99D05E7570F6", 
    "NextPageToken":"BohcFbNNj7F0RcUsHx44Qx" 
    "MediaBucketList": {
        "MediaBucket": [
            {
                "Type": "Input", 
                "Bucket": "watermark-zzz"
            }, 
            {
                "Type": "Output", 
                "Bucket": "zzyoutputbucket"
            }, 
            {
                "Type": "Input", 
                "Bucket": "zzzinput-test"
            }
        ]
    }
}
```

