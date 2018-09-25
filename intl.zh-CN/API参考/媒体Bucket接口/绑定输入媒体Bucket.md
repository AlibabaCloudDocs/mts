# 绑定输入媒体Bucket {#reference_mpp_dqh_y2b .reference}

媒体库绑定输入Bucket。 理。

**说明：** 行为：当媒体库绑定了此Bucket后，用户如果有调用PutObject等操作完成时，都会触发MPS收到相应消息通知，可以理解成在OSS此Bucket上新建了一个类似触发器的功能，每当Bucket里有上传文件，删除文件时都会通知MPS进行处

## 请求参数 {#section_iqn_qbt_x2b .section}

|名称|类型|是否必须|描述|
|:-|:-|:---|:-|
|Action|String|是|操作接口名，系统规定参数，取值：BindInputBucket|
|Bucket|String|是|Bucket名称，不超过64个字节。|

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
<BindInputBucketResponse>
  <RequestId>740DD2EF-5452-4990-970D-5E3D87BFF201</RequestId>
</BindInputBucketResponse>
```

JSON

```
{
  "RequestId":"740DD2EF-5452-4990-970D-5E3D87BFF201"
  }
```

