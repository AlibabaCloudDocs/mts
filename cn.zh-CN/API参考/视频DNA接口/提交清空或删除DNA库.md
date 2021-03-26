# 提交清空或删除DNA库

调用SubmitFpDBDeleteJob提交清空或删除DNA库。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Mts&api=SubmitFpDBDeleteJob&type=RPC&version=2014-06-18)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|SubmitFpDBDeleteJob|操作接口名，系统规定参数，取值：**SubmitFpDBDeleteJob**。 |
|FpDBId|String|是|88c6ca184c0e47098a5b665e2a126797|DNA库ID。 |
|PipelineId|String|否|fb712a6890464059b1b2ea7c8647be16|管道ID，用于绑定消息通知。 |
|UserData|String|否|UserData|用户自定义数据，最大长度128个字节。 |
|DelType|String|否|Purge|操作类型，支持类型：Purge（清空DNA库），Delete（删除DNA库），默认为清空DNA库操作。 |

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|JobId|String|88c6ca184c0e47098a5b665e2a126797|清空删除DNA库作业ID。 |
|RequestId|String|25818875-5F78-4A13-BEF6-D7393642CA58|请求ID。 |

## 示例

请求示例

```
http(s)://[Endpoint]/?Action=SubmitFpDBDeleteJob
&<公共请求参数>
```

正常返回示例

`XML`格式

```
<RequestId>25818875-5F78-4A13-BEF6-D7393642CA58</RequestId>
<JobId>88c6ca184c0e47098a5b665e2a126797</JobId>
```

`JSON`格式

```
{
    "RequestId": "25818875-5F78-4A13-BEF6-D7393642CA58",
    "JobId": "88c6ca184c0e47098a5b665e2a126797"
}
```

## 错误码

|HttpCode|错误码|错误信息|描述|
|--------|---|----|--|
|500|InternalError|The operation has failed due to some unknown error, exception or failure.|内部错误，偶发请重试。|

访问[错误中心](https://error-center.aliyun.com/status/product/Mts)查看更多错误码。

