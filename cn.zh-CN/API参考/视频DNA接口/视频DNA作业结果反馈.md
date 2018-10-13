# 视频DNA作业结果反馈 {#reference_hpy_tgl_lfb .reference}

反馈视频作业有误结果。

## 请求参数 {#section_srk_wgl_lfb .section}

|名称|类型|是否必选|描述|
|:-|:-|:---|:-|
|Action|String|是|操作接口名，系统规定参数，取值： ReportFpShotJobResult|
|JobId|String|是|作业ID。|
|Result|String|是|作业返回结果。|
|Details|String|是|作业结果问题详情。|

## 返回参数 {#section_czx_zgl_lfb .section}

|名称|类型|描述|
|:-|:-|:-|
|jobId|String|作业ID。|

## 示例 {#section_a5l_2hl_lfb .section}

**请求示例**

```
http://mts.cn-shanghai.aliyuncs.com?Action= ReportFpShotJobResult&JobId=%2288c6ca184c0e47098a5b665e2a126797%22&Result=%22result%22&Details=%22details%22<公共参数>
```

**返回示例**

XML

```
<ReportFpShotJobResponse>
    <RequestId>
        25818875-5F78-4A13-BEF6-D7393642CA58
    </RequestId>
        <JobId>88c6ca184c0e47098a5b665e2a126797</JobId>
</ReportFpShotJobResponse>
```

JSON

```
{
  "RequestId": "25818875-5F78-4A13-BEF6-D7393642CA58",
  "JobId": "88c6ca184c0e47098a5b665e2a126797"
}
```

