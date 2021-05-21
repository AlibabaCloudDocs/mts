# How do I perform API transcoding?

## Background

When workflows can not meet user requirements, users need to judge their business logic and use the API to submit transcoding tasks. For example, not all videos require transcoding; and different videos need different transcoding configurations.

## Benefits

-   Customizes business logic and flexibly submit transcoding tasks.

-   Supports powerful functions such as transcoding, encapsulation, watermarking, supports HLS-AES128 standard encryption, editing and other functions.

-   Supports sending execution information to the specified message queue or message notification upon completion of the transcoding task.

-   Supports URL playback.


## Limits

-   A transcoding task generates an output file that allows tasks to be submitted in batch.

-   API transcoding supports HLS-AES128 standard encryption. Currently, Alibaba Cloud private encryption is not supported.

-   API transcoding supports URL playback, but does not support media ID playback. Users need to associate multiple output of multiple definition in multiple formats to achieve the logic of automatic switching between different definition and supporting multiple formats.


## Preparation

-   Custom transcoding template \(as needed\), log on to the [MPS console](https://mts.console.aliyun.com/?spm=a2c4g.11186623.2.4.6f9251fbBWEbgK#/vod/settings/transcode) for configuration.

-   Custom watermark template \(as needed\), log on to the [MPS console](https://mts.console.aliyun.com/?spm=a2c4g.11186623.2.5.6f9251fbBWEbgK#/vod/settings/transcode) for configuration.


## Procedure

1.  Upload input files to OSS \(Multiple upload options: OSS console, OSS related uploading tools and upload SDK\).
2.  [Set MPS Queue notification](/intl.en-US/User Guide/Transcoding message notifications.md).
3.  [Submit transcoding task]().
4.  After getting the message, call the “QueryTranscodingJob” interface to query the task execution result and get the output file URL.
5.  Video playback via URL.

## Set up an application to add watermarks to the video

[Java source code download.](http://docs-aliyun.cn-hangzhou.oss.aliyun-inc.com/assets/attach/59368/cn_zh/1505138223690/mts-demo-java.tgz?spm=a2c4g.11186623.2.10.6f9251fbBWEbgK&file=mts-demo-java.tgz)

