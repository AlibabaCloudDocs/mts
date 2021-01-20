# 提交新建视频DNA库

异步接口。提交新建视频DNA库任务，返回新建DNA库信息，待DNA库新建完成后DNA库状态会更新为active。

## 请求参数

|名称|类型|是否必选|描述|
|:-|:-|:---|:-|
|Action|String|是|操作接口名，系统规定参数，取值：CreateFpShotDB|
|Name|String|是|DNA库名称。|
|Description|String|否|DNA库描述。|
|ModelId|String|否|DNA库模型id，视频DNA ModelId为1，音频DNA ModelId为3。|

## 返回参数

|名称|类型|描述|
|:-|:-|:-|
|FpShotDB|FpShotDB|视频DNA库。|

## 示例

**请求示例**

```
https://mts.cn-shanghai.aliyuncs.com?Action=CreateFpShotDB&Name=test<公共参数>
```

**返回示例**

XML

```
<?xml version='1.0' encoding='UTF-8'?>
<CreateFpShotDBResponse>
    <RequestId>
        25818875-5F78-4A13-BEF6-D7393642CA58
    </RequestId>
    <FpShotDB>
            <FpDBId>88c6ca184c0e47098a5b665e2a126797</FpDBId>
            <Name>test</Name>
            <ModelId>1</ModelId>
            <Status>offline</Status>
            <Description></Description>
    <FpShotDB>
</CreateFpShotDBResponse>
```

JSON

```
{
  "RequestId": "25818875-5F78-4A13-BEF6-D7393642CA58",
  "FpShotDB": {
        "FpDBId":""88c6ca184c0e47098a5b665e2a126797",
        "Name":""test",
        "ModelId":"1",
        "Status":"offline",
        "Description":"",
    }
}
```

