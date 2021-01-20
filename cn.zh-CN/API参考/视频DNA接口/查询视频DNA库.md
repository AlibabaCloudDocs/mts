# 查询视频DNA库

提交新建视频DNA库后，视频DNA服务会进行DNA库新建，通过此接口可以查询DNA库状态信息。

## 请求参数

|名称|类型|是否必选|描述|
|:-|:-|:---|:-|
|Action|String|是|操作接口名，系统规定参数，取值：ListFpShotDB|
|FpDBIds|String|是|DNA库ID列表，最多一次查10个，ID之间用“,”分隔。|

## 返回参数

|名称|类型|描述|
|:-|:-|:-|
|FpShotDBList|FpShotDB\[\]|视频DNA库。|
|NonExistIds|String\[\]|不存在的DNA库ID列表，无数据时该结构不返回。|

## 示例

**请求示例**

```
https://mts.cn-shanghai.aliyuncs.com?Action=ListFpShotDB&FpDBIds=%2288c6ca184c0e47098a5b665e2a126797%22<公共参数>
```

**返回示例**

XML

```
<?xml version='1.0' encoding='UTF-8'?>
<ListFpShotDBResponse>
    <RequestId>
        25818875-5F78-4A13-BEF6-D7393642CA58
    </RequestId>
    <FpShotDBList list="true">
        <FpShotDB>
            <FpDBId>88c6ca184c0e47098a5b665e2a126797</FpDBId>
            <Name>test</Name>
            <ModelId>1</ModelId>
            <Status>offline</Status>
            <Description></Description>
        <FpShotDB>
    </FpShotDBList>
</ListFpShotDBResponse>
```

JSON

```
{
  "RequestId": "25818875-5F78-4A13-BEF6-D7393642CA58",
  "NonExistIds": [
    "ae687c02fe944327ba9631e50da23128"
  ],
  "FpShotDBList": [
     "FpShotDB": {
        "FpDBId":""88c6ca184c0e47098a5b665e2a126797",
        "Name":""test",
        "ModelId":"1",
        "Status":"offline",
        "Description":"",
    }
  ]
}
```

