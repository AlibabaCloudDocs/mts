# 绑定输出媒体Bucket {#reference_x12_lqh_y2b .reference}

媒体库绑定输出Bucket。

## 请求参数 {#section_iqn_qbt_x2b .section}

|名称|类型|是否必须|描述|
|:-|:-|:---|:-|
|Action|String|是|操作接口名，系统规定参数，取值：BindOutputBucket|
|Bucket|String|是|媒体库输出Bucket名称，不超过64个字节。|

## 返回参数 {#section_ogh_wbt_x2b .section}

无

## 示例 {#section_gpq_zbt_x2b .section}

请求示例

```
http://mts.cn-hangzhou.aliyuncs.com?Bucket=watermark-zzz&<公共参数>
```

返回示例

XML

```
<Error>
      <RequestId>0A23F656-D3E6-4222-A2E8-449AD48C031D</RequestId>
      <Code>Bucket.AlreadyBind</Code>
      <Message>Bucket "watermark-zzz" already binded to media store,can not bind twice</Message>
    </Error>
```

JSON

```
{
    "RequestId": "1DB03A02-C3E1-429C-A3DA-4BFDC4294534", 
    "Code": "Bucket.AlreadyBind", 
    "Message": "Bucket \"watermark-zzz\" already binded to media store,can not bind twice "
}
```

