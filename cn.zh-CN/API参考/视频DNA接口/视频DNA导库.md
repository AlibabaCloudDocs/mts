# 视频DNA导库 {#reference_mdn_lhl_lfb .reference}

目前提供视频DNA导库功能，需用户提供需导入DNA库的视频文件OSS路径列表。

列表既定格式如下：

```
{“Bucket”:”mts-video-daily-bucket”,”Location”:”oss-test”,”Object”:”fingerprint/功守道片段1.mp4”,”PrimaryKey”:”3e34ac649945b53a1b0f863ce030d395”}
```

您也可以参考 对应序列化java类 [FpImportOSSEntity](cn.zh-CN/API参考/视频DNA接口/附录/DNA库初始化工具/FpImportOSSEntity.md#) 和示例文件 [listImport.txt](cn.zh-CN/API参考/视频DNA接口/附录/DNA库初始化工具/listImport.txt.md#)。

