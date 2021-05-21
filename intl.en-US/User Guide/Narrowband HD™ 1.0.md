# Narrowband HD™ 1.0

Based on Alibaba Cloud’s exclusive transcoding technology, Narrowband HDTM1.0 intelligently analyzes each scenario, action, content, and texture of a video to ensure a lower bit rate and bandwidth cost to a certain extend with the same video quality.

## Use a workflow to trigger Narrowband HDTM1.0 based transcoding.

1.  [Activate MPS](/intl.en-US/Quick Start/Activate MPS.md).
2.  [Set the Input/Output Media Bucket](/intl.en-US/Quick Start/Library quick start guide.md).
3.  Set a workflow, and select **NarrowbandHD Template Presets** on the **Transcode** node \(The template name ends with **NarrowBandHD**\).

    ![](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/5560421951/p10007.png)

    ![](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/5560421951/p10008.png)

    For more information about workflow configuration, see [Library quick start guide](/intl.en-US/Quick Start/Library quick start guide.md).

4.  Upload a media file. For more information, see [Library quick start guide](/intl.en-US/Quick Start/Library quick start guide.md).

## Use an API to trigger Narrowband HDTM 1.0 based transcoding.

When using the transcoding task submission API [SubmitJobs](/intl.en-US/API Reference/Transcoding APIs/SubmitJobs.md), set TemplateId in Output to [ID of the preset Narrowband HD template](/intl.en-US/API Reference/Appendix/Preset template details.md).

## Use the console to create a transcoding task to trigger Narrowband HDTM 1.0 based transcoding

When [Submitting a transcoding task](/intl.en-US/Quick Start/Transcoding task submission quick start guide.md), select the Narrowband HDTM 1.0 transcoding template.

