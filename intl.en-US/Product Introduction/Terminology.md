# Terminology {#concept_gh2_vhp_w2b .concept}

This article introduces terminology related to MPS.

## Core concepts {#section_wws_zhp_w2b .section}

Region

A region is an Alibaba Cloud service node. By deploying services in different Alibaba Cloud regions, you can bring your services closer to your users for lower access latency and a better user experience.

OSS

OSS stands for Alibaba Cloud Object Storage Service. MPS transcodes media files stored in OSS and the output files are also stored in OSS.

Local file

A Local file is a media file locally stored on your device and not yet uploaded to OSS.

Input task

In MPS, an input task refers to an input file.

Input file

An input file is a media file you have stored in OSS. A local file uploaded to OSS can also serve as an input file.

Output Specification

Output specification is composed of a set of elements including the template ID, watermark list, and output file.

Output file

An output file is the media file or file set output by MPS and stored in OSS.

Task

Here, a task refers to a transcoding task by default. A single transcoding task is composed of one input task and one output specification. It is identified by a unique ID. When submitting a task, you must specify the MPS queue. The scheduling engine schedules tasks in the MPS queue to the transcoding system, which performs the transcoding operation. In addition, MPS performs several other special types of tasks: analysis tasks, screenshot tasks, and media information tasks. These tasks perform template analysis, screenshots, and media information retrieval functions, respectively. These tasks do not occupy MPS queue resources.

MPS queue

The MPS queue is a task queue. When transcoding tasks enter the MPS queue, they are scheduled for transcoding by MPS. An MPS queue can be in active or suspended status. If it is in suspended status, the queue tasks are not scheduled by MPS until the MPS queue enters the active status, but tasks with transcoding in progress are not affected.

Custom template

A custom template \(Template for short\) is a set of custom transcoding parameters, including audio, video, and container parameters. Each template is identified by a unique ID. You can create templates in each service region, where they will be used for all transcoding jobs in their respective regions.

Preset template

A preset template is an intelligent transcoding template inherent in MPS. The template can be used to dynamically adjust the transcoding settings based on the features of an input file, to provide users with the optimal output file under specific bandwidth conditions. For a list of preset templates supported by MPS, see [Preset templates](../../../../reseller.en-US/API Reference/Appendix/Preset template details.md#).

Analysis task

Analysis task Because of the differences between input files \(resolution, bit rate and other\), not all preset templates are suitable for all input files. Therefore, before using a preset template, you must call the `SubmitAnalysisJob`\(`SubmitAnalysisJob`\) interface to submit an analysis task. The result of an analysis task is a list of preset templates that can be used on a given input file. You can call the`QueryAnalysisJobList`interface \(`QueryAnalysisJobList`）to obtain this list. Only the preset templates in the list returned by the analysis task have parameters suitable to the output of the submitted transcoding task. If you specify a preset template not in this list, the submitted transcoding task will fail.

Watermark

Watermark MPS supports up to four static watermarks on an output file. You can set the watermark position, offset, size, and other relatively fixed parameters as a watermark template. To apply a watermark to an output video, set a watermark template and content parameter in the output configuration.

Watermark template

A watermark A watermark setting consists of a variable parameter \(watermark content\) and a set of relatively fixed parameters \(watermark position, offset, and size\). The latter parameters constitute a watermark template with a unique ID.

Screenshot task

A screenshot task creates a JPG format screenshot from the specified time of the input video file.

MediaInfoJob

A MediaInfoJob retrieves media information.

## Transcoding process {#section_s2y_yvp_w2b .section}

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/11339/15392586779828_en-US.png)

