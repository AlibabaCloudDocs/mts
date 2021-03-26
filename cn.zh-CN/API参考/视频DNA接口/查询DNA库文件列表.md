# 查询DNA库文件列表

调用ListFpShotFiles查询DNA库文件列表。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Mts&api=ListFpShotFiles&type=RPC&version=2014-06-18)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|ListFpShotFiles|操作接口名，系统规定参数，取值：

 **ListFpShotFiles**。 |
|FpDBId|String|是|2288c6ca184c0e47098a5b665e2a12\*\*\*\*|DNA库ID。 |
|NextPageToken|String|否|ae0fd49c0840e14daf0d66a75b83\*\*\*\*|支持分页查询，请求第一页时，NextPageToken为空；请求后续文件时需传入前一页查询结果中的NextPageToken值。 |
|PageSize|Integer|否|20|单页数据个数，默认为20。 |

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|FpShotFileList|Array of FpShotFile| |视频DNA文件。参见[数据类型FpShotFile](~~93555~~)。 |
|FpShotFile| | | |
|FileId|String|41e6536e4f2250e2e9bf26cdea19bd7a|视频文件ID。 |
|InputFile|Struct| |作业输入。 |
|Bucket|String|oss-test|OSS的Bucket。 |
|Location|String|oss-cn-beiing|OSS的服务区。 |
|Object|String|test.mp4|OSS的Object。 |
|PrimaryKey|String|fb712a6890464059b1b2ea7c8647be16|视频唯一主键。 |
|NextPageToken|String|ae0fd49c0840e14daf0d66a75b8369ec|下一页token。 |
|RequestId|String|25818875-5F78-4A13-BEF6-D7393642CA58|请求ID。 |

## 示例

请求示例

```
http(s)://[Endpoint]/?Action=ListFpShotFiles
&<公共请求参数>
```

正常返回示例

`XML`格式

```
<RequestId>25818875-5F78-4A13-BEF6-D7393642CA58</RequestId>
<NextPageToken>ae0fd49c0840e14daf0d66a75b8369ec</NextPageToken>
<FpShotFileList>
    <FpShotFile>
        <PrimaryKey>fb712a6890464059b1b2ea7c8647be16</PrimaryKey>
        <FileId>41e6536e4f2250e2e9bf26cdea19bd7a</FileId>
        <InputFile>
            <Bucket>oss-test</Bucket>
            <Object>test.mp4</Object>
            <Location>oss-cn-beiing</Location>
        </InputFile>
    </FpShotFile>
</FpShotFileList>
```

`JSON`格式

```
{
    "RequestId": "25818875-5F78-4A13-BEF6-D7393642CA58",
    "NextPageToken": "ae0fd49c0840e14daf0d66a75b8369ec",
    "FpShotFileList": {
        "FpShotFile": {
            "PrimaryKey": "fb712a6890464059b1b2ea7c8647be16",
            "FileId": "41e6536e4f2250e2e9bf26cdea19bd7a",
            "InputFile": {
                "Bucket": "oss-test",
                "Object": "test.mp4",
                "Location": "oss-cn-beiing"
            }
        }
    }
}
```

## 错误码

|HttpCode|错误码|错误信息|描述|
|--------|---|----|--|
|500|InternalError|The operation has failed due to some unknown error, exception or failure.|内部错误，偶发请重试。|
|400|InvalidParameter.OutOfRange|The specified parameter %s is out of range.|参数无效超出指定范围|

访问[错误中心](https://error-center.aliyun.com/status/product/Mts)查看更多错误码。

