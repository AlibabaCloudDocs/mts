# 查询媒体Bucket {#reference_a5b_5qh_y2b .reference}

列出媒体库所有媒体Bucket。

## 请求参数 {#section_iqn_qbt_x2b .section}

|名称|类型|是否必须|描述|
|:-|:-|:---|:-|
|Action|String|是|操作接口名，系统规定参数，取值：ListAllMediaBucket|

## 返回参数 {#section_ogh_wbt_x2b .section}

|名称|类型|描述|
|:-|:-|:-|
|MediaBucket|[MediaBucket](https://help.aliyun.com/document_detail/29251.html#MediaBucket)\[\]|媒体Bucket列表|

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

