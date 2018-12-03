# How do I perform workflow transcoding? {#concept_x5d_xhg_x2b .concept}

## Background {#section_gwv_bjg_x2b .section}

One input file corresponds to multiple output files \(different resolutions, different formats, etc.\). A commonly used video processing flow can be created quickly through the console graphic interface.

## Advantages {#section_n34_cjg_x2b .section}

-   Simple and easy to use, once video upload has completed, transcoding tasks are automatically triggered.

-   Supports multiple functions such as screenshots, transcoding, encapsulation, watermarking, editing and other functions.

-   Supports sending workflow execution message to the specified MPS queue or message notification upon beginning and ending the workflow.

-   Media Files to offer you audio and video management capabilities. Media ID associates outputs of multiple definition in multiple formats. When using the MediaID for playback, automatic switch among multiple definitions can be achieved , and multiple formats are supported.

-   Supports both URL and MediaID playback.


For more information, see [Developing process of workflows](../../../../reseller.en-US/Developer Guide/Developing process of workflows.md#).

## Restrictions {#section_obn_jjg_x2b .section}

-   A workflow can only be configured with only one input path, the workflow processes handle all videos in this path.

-   Videos uploaded to the input directory will trigger workflow transcoding. Currently, only simple conditional transcoding scenarios are supported, and some complex business logic cannot be supported.

-   The workflow supports Alibaba Cloud private encryption, but HLS-AES128 standard encryption is not yet supported.


## Preparation {#section_pzl_kjg_x2b .section}

-   [Custom transcoding template \(As needed\)](../../../../reseller.en-US/User Guide/Settings.md#).
-   [Custom watermark template \(As needed\)](../../../../reseller.en-US/User Guide/Settings.md#).

## Procedure {#section_oym_ljg_x2b .section}

1.  [Add Input/Output Media Bucket](../../../../reseller.en-US/User Guide/Library/Library settings.md#).
2.  [Create a workflow](../../../../reseller.en-US/User Guide/Library/Workflows.md#). In the workflow, you can customize parameters for screenshots, transcoding, conversion and encapsulation, watermark, encryption, editing and other functions.
3.  Enable the CDN acceleration function \(optional\): If you need to enable Content Distribution Acceleration for your domain name, see [Domain name management](../../../../reseller.en-US/User Guide/Library/Domain name management.md#).
4.  [Upload videos](reseller.en-US/Best Practices/How do I upload a video?.md#): You can use the MPS console or OSS related upload tools to upload a video file. In addition, an upload SDK that covers all platforms is provided. For details, see Upload SDK usage instructions, Upload SDK downloading.
5.  [Manage videos](../../../../reseller.en-US/User Guide/Library/Video management.md#).

## Set up a video transcoding application {#section_z15_qjg_x2b .section}

[Download JAVA source code.](http://docs-aliyun.cn-hangzhou.oss.aliyun-inc.com/assets/attach/58040/cn_zh/1502865915040/mts-demo-java.tgz?spm=a2c4g.11186623.2.13.3d6343afYT4hd0&file=mts-demo-java.tgz)

