# 查询视频DNA作业 {#reference_tzj_sfl_lfb .reference}

提交视频DNA作业后，视频DNA服务会进行DNA对比，通过此接口可以查询作业结果。

## 请求参数 {#section_w4s_xfl_lfb .section}

|名称|类型|是否必选|描述|
|:-|:-|:---|:-|
|Action|String|是|操作接口名，系统规定参数，取值： QueryFpShotJobList|
|JobIds|String|是|作业ID列表，最多一次查10个，ID之间用“,”分隔。|

## 返回参数 {#section_nlk_bgl_lfb .section}

|名称|类型|描述|
|:-|:-|:-|
|FpShotJobList|AliyunFpShotJob\[\]|视频DNA作业。参见 [数据类型AliyunFpShotJob](cn.zh-CN/API参考/视频DNA接口/数据类型.md#)|
|NonExistIds|String\[\]|不存在的作业ID列表，无数据时该结构不返回。|

## 示例 {#section_vmt_3gl_lfb .section}

**请求示例**

```
http://mts.cn-shanghai.aliyuncs.com?Action=QueryFpShotJobList&JobId=%2288c6ca184c0e47098a5b665e2a126797%22<公共参数>
```

**返回示例**

XML

```
<QueryFpShotJobListResponse>
    <RequestId>
        25818875-5F78-4A13-BEF6-D7393642CA58
    </RequestId>
    <FpShotJobList list="true">
        <FpShotJob>
            <Id>88c6ca184c0e47098a5b665e2a126797</Id>
            <PipelineId>88c6ca184c0e47098a5b665e2a126797</PipelineId>
            <UserData>testid-001</UserData>
            <CreationTime>2017-01-10T12:00:00Z</CreationTime>
            <State>Success</State>
            <Code></Code>
            <Message></Message>
            <InputFile>
                <Bucket>oss-test</Bucket>
                <Location>oss-cn-beiing</Location>
                <Object>test.mp4</Object>
            </InputFile>
            <FpShotResult>
                <FpShots list="true">
                    <FpShot>
                        <PrimaryKey>123456</PrimaryKey>
                        <Similarity>0.8914769887924194</Similarity>
                        <FpShotSlices list="true">
                            <FpShotSlice>
                                <Input>
                                    <Start>46.0</Start>
                                    <Duration>48.0</Duration>
                                </Input>
                                <Duplication>
                                    <Start>1260.0</Start>
                                    <Duration>48.0</Duration>
                                </Duplication>
                            </FpShotSlice>
                        </FpShotSlices>
                    </FpShot>
                </FpShots>
            </FpShotResult>
        </FpShotJob>
    </FpShotJobList>
</QueryFpShotJobListResponse>
```

JSON

```
{
  "RequestId": "C0415F74-E6A4-4E00-ADFC-482A6894E05B",
  "NonExistIds": [
    "ae687c02fe944327ba9631e50da23128"
  ],
  "FpShotJobList": [
    {
      "Code": "0",
      "CreationTime": "2017-10-24T17:30:47Z",
      "Id": "5c931d546f314cc4976bb863d457fc1c",
      "InputFile": {
        "Bucket": "oss-test,
        "Location": "oss-cn-shanghai",
        "Object": "mts/test.mp4"
      },
      "Message": "successful",
      "PipelineId": "fb712a6890464059b1b2ea7c8647be16",
      "State": "Success",
      "UserData": "userData",
      "FpShotJobList": {
        "FpShots": [
          {
            "FpShot": [
              {
                "PrimaryKey": "123456",
                "Similarity": "0.8914769887924194",
                "FpShotSlices": [
                  {
                    "FpShotSlice":{
                      "Input" : {
                        "Start":"46.0",
                        "Duration:"48.0"
                      },
                      "Duplication": {
                        "Start": "1260.0",
                        "Duration": "48.0"
                      }
                    }
                  }
                ]
              }
            ]
          }
        ]
      }
    }
  ]
}
```

