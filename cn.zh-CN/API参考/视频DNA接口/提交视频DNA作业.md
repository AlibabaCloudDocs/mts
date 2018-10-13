# 提交视频DNA作业 {#concept_an5_w1l_lfb .concept}

异步接口。查询视频库中是否存在相同或者相近的DNA结果。不保证接口返回时结果已经生成，结果完成后将发送异步消息。

## 请求参数 {#section_a2s_fbl_lfb .section}

|名称|类型|是否必选|描述|
|:-|:-|:---|:-|
|Action|String|是|操作接口名，系统规定参数，取值：SubmitFpShotJob|
|Input|String|是|作业输入文件OSS地址，Json对象，参见 [InputFile详情](cn.zh-CN/API参考/视频DNA接口/附录/参数详情.md#)。例如：\{“Bucket”:”example-bucket”,“Location”:”oss-cn-shanghai”,“Object”:”example.flv”\}

|
|PipelineId|String|是|管道ID，用于绑定消息通知。|
|FpShotConfig|String|是|视频DNA配置，参见 [FpShotConfig详情](cn.zh-CN/API参考/视频DNA接口/附录/参数详情.md#)。Json对象。例如：\{“PrimaryKey”:”12345”, “SaveType”: “save”\}

|
|UserData|String|否|用户自定义数据，最大长度128个字节。|

## 返回参数 {#section_qqr_kbl_lfb .section}

|名称|类型|描述|
|:-|:-|:-|
|JobId|String|视频DNA作业ID。|

**异步通知消息参数**

|名称|类型|描述|
|:-|:-|:-|
|Type|String|消息类型，FpShot。|
|FpShotJobNotify|AliyunFpShotJobNotify|视频DNA作业，参见 [数据类型AliyunFpShotJobNotify](cn.zh-CN/API参考/视频DNA接口/数据类型.md#)。|
|UserData|String|用户自定义数据。|

## 示例 {#section_q15_l2l_lfb .section}

**请求示例**

```
https://mts.cn-shanghai.aliyuncs.com?Action=SubmitFpShotJob&Input=%7b%22Bucket%22%3a%22example-bucket%22%2c%22Location%22%3a%22oss-cn-shanghai%22%2c%22Object%22%3a%22example.flv%22%7d&FpShotConfig=%7b%22SaveType%22%3a%22save%22<公共参数>
```

**返回示例**

XML

```
<?xml version='1.0' encoding='UTF-8'?>
<SubmitFpShotJobResponse>
    <RequestId>
        25818875-5F78-4A13-BEF6-D7393642CA58
    </RequestId>
    <JobId>88c6ca184c0e47098a5b665e2a126797</JobId>
</SubmitFpShotJobResponse>
```

JSON

```
{
  "RequestId": "25818875-5F78-4A13-BEF6-D7393642CA58",
  "JobId": "88c6ca184c0e47098a5b665e2a126797"
}
```

