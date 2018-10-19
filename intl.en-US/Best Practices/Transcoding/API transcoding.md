# API transcoding {#concept_bsj_kgg_x2b .concept}

## Background {#section_fzj_ygg_x2b .section}

When workflows can not meet user requirements, users need to judge their business logic and use the API to submit transcoding tasks. For example, not all videos require transcoding; and different videos need different transcoding configurations.

## Advantage {#section_xsh_zgg_x2b .section}

-   Customizes business logic and flexibly submit transcoding tasks.

-   Supports powerful functions such as transcoding, encapsulation, watermarking, supports HLS-AES128 standard encryption, editing and other functions.

-   Supports sending execution information to the specified message queue or message notification upon completion of the transcoding task.

-   Supports URL playback.


## Restrictions {#section_i3q_4hg_x2b .section}

-   A transcoding task generates an output file that allows tasks to be submitted in batch.

-   API transcoding supports HLS-AES128 standard encryption. Currently, Alibaba Cloud private encryption is not supported.

-   API transcoding supports URL playback, but does not support media ID playback. Users need to associate multiple output of multiple definition in multiple formats to achieve the logic of automatic switching between different definition and supporting multiple formats.


## Preparation {#section_fqb_rhg_x2b .section}

-   Custom transcoding template \(as needed\), log on to the [MPS console](https://partners-intl.aliyun.com/login-required#/mts) for configuration.

-   Custom watermark template \(as needed\), log on to the [MPS console](https://partners-intl.aliyun.com/login-required#/mts) for configuration.


## Procedure {#section_ggb_thg_x2b .section}

1.  [Upload input files to OSS](reseller.en-US/Best Practices/Upload videos.md#) \(Multiple upload options: OSS console, OSS related uploading tools and upload SDK\).

2.  [Set MPS Queue notification](../../../../reseller.en-US/User Guide/Transcoding message notifications.md#).

3.  [Submit transcoding task](../../../../reseller.en-US/User Guide/Submit a transcoding task.md#).

4.  After getting the message, call the “QueryTranscodingJob” interface to query the task execution result and get the output file URL.

5.  6.  7.  
## Set up an application to add watermarks to the video {#section_evd_5hg_x2b .section}

[Java source code download.](http://docs-aliyun.cn-hangzhou.oss.aliyun-inc.com/assets/attach/59368/cn_zh/1505138223690/mts-demo-java.tgz?spm=a2c4g.11186623.2.10.6f9251fbBWEbgK&file=mts-demo-java.tgz)

