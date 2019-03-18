# 查询视频DNA导库结果 {#reference_odd_yhl_lfb .reference}

在导库完成后，通过此接口可以查询导库视频比对结果。

## 请求参数 {#section_zsr_b3l_lfb .section}

|名称|类型|是否必选|描述|
|:-|:-|:---|:-|
|Action|String|是|操作接口名，系统规定参数，取值： QueryFpImportResult|
|StartTime|Long|否|查询起始unix时间戳，如：1538230742。默认：当前时间前一天。

|
|EndTime|Long|否|查询结束unix时间戳，如：1538230743。默认：当前时间。

|
|PageSize|Long|否|用于分页查询，指定每页返回多少记录。默认：86400

|
|PageIndex|Long|否|用于分页查询，指定返回第几页数据。默认：不分页，查询全部。

|

## 返回参数 {#section_dl1_f3l_lfb .section}

|名称|类型|描述|
|:-|:-|:-|
|LogCount|Long|当次查询得到的日志个数。|
|FpResultLogInfoList|FpResultLogInfo\[\]|导库结果日志，参见 [数据类型FpResultLogInfo](intl.zh-CN/API参考/视频DNA接口/数据类型.md#)|
|PageInfo|PageInfo|查询结果页信息，参见 [数据类型PageInfo](intl.zh-CN/API参考/视频DNA接口/数据类型.md#)|

## 示例 {#section_u5r_p3l_lfb .section}

**请求示例**

```
http://mts.cn-shanghai.aliyuncs.com?Action=QueryFpImportResult<公共参数>
```

**返回示例**

XML

```
<QueryFpImportResultResponse>
    <RequestId>
        25818875-5F78-4A13-BEF6-D7393642CA58
    </RequestId>
    <LogCount>6</LogCount>
    <FpResultLogInfoList list="true">
        <FpResultLogInfo>
            <LogPath>cdnlog-hz-public.oss-cn-hangzhou.aliyuncs.com/mts.fingerprint/helloworld/20180923/helloworld_2018_09_23.gz?Expires=1538836455\u0026OSSAccessKeyId=test\u0026Signature=QaxYPBk3PF546A8OSZS%2FxR0gVR8%3D</LogPath>
            <LogName>helloworld.gz</LogName>
            <LogStartTime>1537632000</LogStartTime>
            <LogEndTime>1537718400</LogEndTime>
            <LogSize>7059473</LogSize>
            <CreateTime>1538015556</CreateTime>
        </FpResultLogInfo>
    </FpResultLogInfoList>
    <PageInfo>
        <PageIndex>-1</PageIndex>
        <PageSize>86400</PageSize>
        <Total>6</Total>
    </PageInfo>
</QueryFpImportResultResponse>
```

JSON

```
{
  "RequestId": "C0415F74-E6A4-4E00-ADFC-482A6894E05B",
  "LogCount": 6,
  "FpResultLogInfoList": [
    {
      "LogPath": "cdnlog-hz-public.oss-cn-hangzhou.aliyuncs.com/mts.fingerprint/helloworld/20180923/helloworld_2018_09_2.gz?Expires=1538836455\u0026OSSAccessKeyId=test\u0026Signature=QaxYPBk3PF546A8OSZS%2FxR0gVR8%3D",
      "LogName": "helloworld.gz",
      "LogStartTime": 1537632000,
      "LogEndTime": 1537718400,
      "LogSize": 7059473,
      "CreateTime": 1538015556,
     }
      ]
      "PageInfo": {
        "PageIndex": -1,
        "PageSize": 86400,
        "Total": 6
   }
}
```

