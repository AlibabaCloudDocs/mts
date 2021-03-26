# 查询删除DNA文件

调用QueryFpFileDeleteJobList查询删除DNA文件。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Mts&api=QueryFpFileDeleteJobList&type=RPC&version=2014-06-18)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|QueryFpFileDeleteJobList|操作接口名，系统规定参数，取值：

 **QueryFpFileDeleteJobList**。 |
|JobIds|String|否|88c6ca184c0e47098a5b665e2a126797|视频DNA删除作业Ids，以英文（,）逗号隔开，如为空则返回最近20个作业列表。 |

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|FpFileDeleteJobList|Array of FpFileDeleteJob| |删除作业列表。参见[数据类型FpFileDeleteJob](~~93555~~)。 |
|FpFileDeleteJob| | | |
|Code|String|0|分析失败时错误码。 |
|CreationTime|String|2020-06-30T00:33:18Z|创建时间。 |
|FileIds|String|41e6536e4f2250e2e9bf26cdea19bd7a|文件ID。 |
|FinishTime|String|2020-06-30T00:34:02Z|完成时间。 |
|FpDBId|String|88c6ca184c0e47098a5b665e2a126797|DNA库ID。 |
|Id|String|25bacf2824614bcf9273dc0744db5f21|作业ID。 |
|Message|String|Success|分析失败时错误信息。 |
|PipelineId|String|fb712a6890464059b1b2ea7c8647be16|管道ID。 |
|Status|String|Success|作业状态，包括：Queuing、Analysing、Success、Fail。 |
|UserData|String|UserData|用户自定义数据。 |
|NonExistIds|List|fb712a6890464059b1b2ea7c8647ai58|不存在的作业ID列表。 |
|RequestId|String|25818875-5F78-4A13-BEF6-D7393642CA58|请求ID。 |

## 示例

请求示例

```
http(s)://[Endpoint]/?Action=QueryFpFileDeleteJobList
&<公共请求参数>
```

正常返回示例

`XML`格式

```
<RequestId>25818875-5F78-4A13-BEF6-D7393642CA58</RequestId>
<FpFileDeleteJobList>
    <FpFileDeleteJob>
        <Status>Success</Status>
        <FinishTime>2020-06-30T00:34:02Z</FinishTime>
        <Message>Success</Message>
        <UserData>UserData</UserData>
        <CreationTime>2020-06-30T00:33:18Z</CreationTime>
        <PipelineId>fb712a6890464059b1b2ea7c8647be16</PipelineId>
        <Id>25bacf2824614bcf9273dc0744db5f21</Id>
        <FileIds>41e6536e4f2250e2e9bf26cdea19bd7a</FileIds>
        <Code>0</Code>
        <FpDBId>88c6ca184c0e47098a5b665e2a126797</FpDBId>
    </FpFileDeleteJob>
</FpFileDeleteJobList>
<NonExistIds>
    <String>fb712a6890464059b1b2ea7c8647ai58</String>
</NonExistIds>
```

`JSON`格式

```
{
    "RequestId": "25818875-5F78-4A13-BEF6-D7393642CA58",
    "FpFileDeleteJobList": {
        "FpFileDeleteJob": {
            "Status": "Success",
            "FinishTime": "2020-06-30T00:34:02Z",
            "Message": "Success",
            "UserData": "UserData",
            "CreationTime": "2020-06-30T00:33:18Z",
            "PipelineId": "fb712a6890464059b1b2ea7c8647be16",
            "Id": "25bacf2824614bcf9273dc0744db5f21",
            "FileIds": "41e6536e4f2250e2e9bf26cdea19bd7a",
            "Code": 0,
            "FpDBId": "88c6ca184c0e47098a5b665e2a126797"
        }
    },
    "NonExistIds": {
        "String": "fb712a6890464059b1b2ea7c8647ai58"
    }
}
```

## 错误码

|HttpCode|错误码|错误信息|描述|
|--------|---|----|--|
|500|InternalError|The operation has failed due to some unknown error, exception or failure.|内部错误，偶发请重试。|

访问[错误中心](https://error-center.aliyun.com/status/product/Mts)查看更多错误码。

