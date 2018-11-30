# 如何进行API转码 {#concept_bsj_kgg_x2b .concept}

## 背景 {#section_fzj_ygg_x2b .section}

工作流无法满足用户场景时，需用户自己判断业务逻辑，使用API提交转码任务。例如：并不是所有的视频都需要转码，不同视频需要设置不同的转码配置。

## 优势 {#section_xsh_zgg_x2b .section}

-   自定义业务逻辑，灵活提交转码作业。

-   功能强大，支持转码、转封装、水印、支持HLS-AES128标准加密、剪辑等功能。

-   转码任务执行完成，支持向指定的消息队列或消息通知发送执行信息。

-   支持URL播放。


## 使用限制 {#section_i3q_4hg_x2b .section}

-   一个转码作业生成一个输出文件，允许批量提交作业。

-   API转码支持HLS-AES128标准加密，暂不支持阿里云私有加密。

-   API转码支持URL播放，不支持媒体ID播放。需用户自己关联多个格式的多个清晰度输出，实现多清晰度自动切换、多格式支持等逻辑。


## 准备 {#section_fqb_rhg_x2b .section}

-   自定义转码模板（按需），进入[媒体处理控制台](https://mts.console.aliyun.com/?spm=a2c4g.11186623.2.4.6f9251fbBWEbgK#/vod/settings/transcode) 设置。

-   自定义水印模板（按需），进入[媒体处理控制台](https://mts.console.aliyun.com/?spm=a2c4g.11186623.2.5.6f9251fbBWEbgK#/vod/settings/transcode) 设置。


## 操作步骤 {#section_ggb_thg_x2b .section}

1.  输入文件 [上传到OSS](intl.zh-CN/最佳实践/如何上传视频.md#)（多种上传方案：OSS控制台上传，使用OSS相关上传工具上传，上传SDK）。

2.  [设置管道消息队列通知](../../../../intl.zh-CN/用户指南/转码消息通知.md#)。

3.  [提交转码任务](../../../../intl.zh-CN/用户指南/提交转码作业.md#)。

4.  在获取到消息后，调用“查询转码作业”接口查询作业执行结果，获取输出文件URL。

5.  6.  通过URL播放视频。

7.  
## 搭建一个给视频添加水印的应用服务 {#section_evd_5hg_x2b .section}

[JAVA源代码下载](http://docs-aliyun.cn-hangzhou.oss.aliyun-inc.com/assets/attach/59368/cn_zh/1505138223690/mts-demo-java.tgz?spm=a2c4g.11186623.2.10.6f9251fbBWEbgK&file=mts-demo-java.tgz)

