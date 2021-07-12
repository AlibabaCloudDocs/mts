# 提交删除DNA文件

调用SubmitFpFileDeleteJob接口提交删除文件。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Mts&api=SubmitFpFileDeleteJob&type=RPC&version=2014-06-18)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|SubmitFpFileDeleteJob|操作接口名，系统规定参数，取值：**SubmitFpFileDeleteJob**。 |
|PipelineId|String|否|ed450ea0bfbd41e29f80a401fb4d\*\*\*\*|管道ID，用于绑定消息通知。 |
|FpDBId|String|是|41e6536e4f2250e2e9bf26cdea19\*\*\*\*|DNA库ID。 |
|UserData|String|否|UserData|用户自定义数据，最大长度128个字节。 |
|FileIds|String|是|41e6536e4f2250e2e9bf26cdea19\*\*\*\*|需要删除的视频FileId，以英文逗号（,）隔开，最多支持200个。 |

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|RequestId|String|25818875-5F78-4A13-BEF6-D7393642\*\*\*\*|请求ID。 |
|JobId|String|88c6ca184c0e47098a5b665e2a12\*\*\*\*|指纹删除作业ID。 |

## 示例

请求示例

```
http(s)://[Endpoint]/?Action=SubmitFpFileDeleteJob
&PipelineId=ed450ea0bfbd41e29f80a401fb4d****
&FpDBId=41e6536e4f2250e2e9bf26cdea19****
&UserData=UserData
&FileIds=41e6536e4f2250e2e9bf26cdea19****
&公共请求参数
```

正常返回示例

`XML`格式

```
HTTP/1.1 200 OK
Content-Type:application/xml

<SubmitFpFileDeleteJobResponse>
    <RequestId>25818875-5F78-4A13-BEF6-D7393642****</RequestId>
    <JobId>88c6ca184c0e47098a5b665e2a12****</JobId>
</SubmitFpFileDeleteJobResponse>
```

`JSON`格式

```
HTTP/1.1 200 OK
Content-Type:application/json

{
  "RequestId" : "25818875-5F78-4A13-BEF6-D7393642****",
  "JobId" : "88c6ca184c0e47098a5b665e2a12****"
}
```

## 错误码

|HttpCode|错误码|错误信息|描述|
|--------|---|----|--|
|400|InvalidParameter.DBNotExist|The DNA database does not exist.|指纹数据库不存在|
|500|InternalError|The operation has failed due to some unknown error, exception or failure.|内部错误，偶发请重试。|

访问[错误中心](https://error-center.aliyun.com/status/product/Mts)查看更多错误码。

