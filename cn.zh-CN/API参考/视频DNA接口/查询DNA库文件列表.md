# 查询DNA库文件列表

调用ListFpShotFiles接口查询DNA库文件列表。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Mts&api=ListFpShotFiles&type=RPC&version=2014-06-18)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|ListFpShotFiles|操作接口名，系统规定参数，取值：**ListFpShotFiles**。 |
|NextPageToken|String|否|ae0fd49c0840e14daf0d66a75b83\*\*\*\*|支持分页查询，请求第一页时，NextPageToken为空；请求后续文件时需传入前一页查询结果中的NextPageToken值。 |
|PageSize|Integer|否|20|单页数据个数，默认为20。 |
|FpDBId|String|是|2288c6ca184c0e47098a5b665e2a12\*\*\*\*|DNA库ID。 |

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|RequestId|String|25818875-5F78-4A13-BEF6-D7393642\*\*\*\*|请求ID。 |
|NextPageToken|String|ae0fd49c0840e14daf0d66a75b83\*\*\*\*|下一页token。 |
|FpShotFileList|Array of FpShotFile| |视频DNA文件。参见[数据类型FpShotFile](https://icms.alibaba-inc.com/content/mps/cc2a58?l=1&m=16051&n=23657)。 |
|FpShotFile| | | |
|PrimaryKey|String|fb712a6890464059b1b2ea7c8647\*\*\*\*|视频唯一主键。 |
|InputFile|Object| |作业输入。 |
|Object|String|test.mp4|OSS的Object，最大1024字节。 |
|Location|String|oss-cn-beiing|OSS的服务区域，最大64字节。 |
|Bucket|String|oss-test|OSS的Bucket，3~63字节。 |
|FileId|String|41e6536e4f2250e2e9bf26cdea19\*\*\*\*|视频文件ID。 |

## 示例

请求示例

```
http(s)://[Endpoint]/?Action=ListFpShotFiles
&NextPageToken=ae0fd49c0840e14daf0d66a75b83****
&PageSize=20
&FpDBId=2288c6ca184c0e47098a5b665e2a12****
&公共请求参数
```

正常返回示例

`XML`格式

```
HTTP/1.1 200 OK
Content-Type:application/xml

<ListFpShotFilesResponse>
    <RequestId>25818875-5F78-4A13-BEF6-D7393642CA58</RequestId>
    <NextPageToken>ae0fd49c0840e14daf0d66a75b8369ec</NextPageToken>
    <FpShotFileList>
        <PrimaryKey>fb712a6890464059b1b2ea7c8647be16</PrimaryKey>
        <InputFile>
            <Object>test.mp4</Object>
            <Location>oss-cn-beiing</Location>
            <Bucket>oss-test</Bucket>
        </InputFile>
        <FileId>41e6536e4f2250e2e9bf26cdea19bd7a</FileId>
    </FpShotFileList>
</ListFpShotFilesResponse>
```

`JSON`格式

```
HTTP/1.1 200 OK
Content-Type:application/json

{
  "RequestId" : "25818875-5F78-4A13-BEF6-D7393642CA58",
  "NextPageToken" : "ae0fd49c0840e14daf0d66a75b8369ec",
  "FpShotFileList" : [ {
    "PrimaryKey" : "fb712a6890464059b1b2ea7c8647be16",
    "InputFile" : {
      "Object" : "test.mp4",
      "Location" : "oss-cn-beiing",
      "Bucket" : "oss-test"
    },
    "FileId" : "41e6536e4f2250e2e9bf26cdea19bd7a"
  } ]
}
```

## 错误码

|HttpCode|错误码|错误信息|描述|
|--------|---|----|--|
|400|InvalidParameter.OutOfRange|The specified parameter %s is out of range.|参数无效超出指定范围|
|500|InternalError|The operation has failed due to some unknown error, exception or failure.|内部错误，偶发请重试。|

访问[错误中心](https://error-center.aliyun.com/status/product/Mts)查看更多错误码。

