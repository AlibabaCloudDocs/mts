# Preset template details

This document introduces preset narrowband HDTM templates, preset static templates, preset smart templates and template ID rules.

## Preset narrowband HDTM templates

**Note:** Preset narrowband HDTM templates are a type of transcoding templates unique to Alibaba Cloud Media Processing. While maintaining the same video definition as common transcoding templates, they provide a lower bit rate to reduce your costs.

|Template ID|Template Name|Chinese name|Container formats|Bit rate range|Resolution-Width|
|:----------|:------------|:-----------|:----------------|:-------------|:---------------|
|S00000003-200050|MP4-FHD-NarrowBandHDV2|MP4-FHD-Narrowband HDTM 2.0|MP4|≤3000|1920|
|S00000003-200040|MP4-HD-NarrowBandHDV2|MP4-SD-Narrowband HDTM 2.0|MP4|≤1500|1280|
|S00000003-200030|MP4-SD-NarrowBandHDV2|MP4-LD-Narrowband HDTM2.0|MP4|≤800|848|
|S00000003-200020|MP4-LD-NarrowBandHDV2|MP4-LD-Narrowband HDTM2.0|MP4|≤400|640|
|S00000002-000070|FLV-4K-NarrowBandHDV1|FLV-4K-Narrowband HDTM|FLV|≤8000|3840|
|S00000002-000060|FLV-2K-NarrowBandHDV1|FLV-2K-Narrowband HDTM|FLV|≤4000|2048|
|S00000002-000050|FLV-FHD-NarrowBandHDV1|FLV-FHD-Narrowband HDTM|FLV|≤3000|1920|
|S00000002-000040|FLV-HD-NarrowBandHDV1|FLV-HD-Narrowband HDTM|FLV|≤1500|1280|
|S00000002-000030|FLV-SD-NarrowBandHDV1|FLV-SD-Narrowband HDTM|FLV|≤800|848|
|S00000002-000020|FLV-LD-NarrowBandHDV1|FLV-LD-Narrowband HDTM|FLV|≤400|640|
|S00000002-100070|M3U8-4K-NarrowBandHDV1|M3U8-4K-Narrowband HDTM|M3U8|≤8000|3840|
|S00000002-100060|M3U8-2K-NarrowBandHDV1|M3U8-2K-Narrowband HDTM|M3U8|≤4000|2048|
|S00000002-100050|M3U8-FHD-NarrowBandHDV1|M3U8-FHD-Narrowband HDTM|M3U8|≤3000|1920|
|S00000002-100040|M3U8-HD-NarrowBandHDV1|M3U8-HD-Narrowband HDTM|M3U8|≤1500|1280|
|S00000002-100030|M3U8-SD-NarrowBandHDV1|M3U8-SD-Narrowband HDTM|M3U8|≤800|848|
|S00000002-100020|M3U8-LD-NarrowBandHDV1|M3U8-LD-Narrowband HDTM|M3U8|≤400|640|
|S00000002-200070|MP4-4K-NarrowBandHDV1|MP4-4K-Narrowband HDTM|MP4|≤8000|3840|
|S00000002-200060|MP4-2K-NarrowBandHDV1|MP4-2K-Narrowband HDTM|MP4|≤4000|2048|
|S00000002-200050|MP4-FHD-NarrowBandHDV1|MP4-FHD-Narrowband HDTM|MP4|≤3000|1920|
|S00000002-200040|MP4-HD-NarrowBandHDV1|MP4-HD-Narrowband HDTM|MP4|≤1500|1280|
|S00000002-200030|MP4-SD-NarrowBandHDV1|MP4-SD-Narrowband HDTM|MP4|≤800|848|
|S00000002-200020|MP4-LD-NarrowBandHDV1|MP4-LD-Narrowband HDTM2.0|MP4|≤400|640|

## Preset static templates

Compared with a preset smart template, a preset static template does not have to be analyzed before being called. Preset static templates include video transcoding templates, audio MP3 transcoding templates, and conversion and encapsulation templates.

-   Video transcoding templates

    A video transcoding template basically controls the resolution when duly controlling the bit rate. Each preset static template outputs a fixed preset resolution width. The resolution height scales down at the original aspect ratio.

    Preset static templates - video transcoding templates

    |Template ID|Template name|Chinese name|Container format|Video bit rate \(Kbps\)|Audio bit rate \(Kbps\)|Resolution-width|Remarks|
    |:----------|:------------|:-----------|:---------------|:----------------------|:----------------------|:---------------|:------|
    |S00000001-000070|FLV-4K|FLV-4K|FLV|6000|160|3840|Flash video|
    |S00000001-000060|FLV-2K|FLV-2K|FLV|3500|160|2048|Flash video|
    |S00000001-000040|FLV-FHD|FLV-FHD|FLV|3000|160|1920|Flash video|
    |S00000001-000030|FLV-HD|FLV-HD|FLV|1800|128|1280|Flash video|
    |S00000001-000020|FLV-SD|FLV-SD|FLV|800|80|848|Flash video|
    |S00000001-000010|FLV-LD|FLV-LD|FLV|400|64|640|Flash video|
    |S00000001-100070|M3U8-4K|M3U8-4K|M3U8|6000|160|3840|Applicable to Web, iOS devices \(iPhone 4 or later and iPad\), and Android devices \(Android 3.0 or later\)|
    |S00000001-100060|M3U8-2K|M3U8-2K|M3U8|3500|160|2048|Applicable to Web, iOS devices \(iPhone 4 or later and iPad\), and Android devices \(Android 3.0 or later\)|
    |S00000001-100040|M3U8-FHD|M3U8-FHD|M3U8|3000|160|1920|Applicable to Web, iOS devices \(iPhone 4 or later and iPad\), and Android devices \(Android 3.0 or later\)|
    |S00000001-100030|M3U8-HD|M3U8-HD|M3U8|1800|128|1280|Applicable to Web, iOS devices \(iPhone 4 or later and iPad\), and Android devices \(Android 3.0 or later\)|
    |S00000001-100020|M3U8-SD|M3U8-SD|M3U8|800|80|848|Applicable to Web, iOS devices \(iPhone 4 or later and iPad\), and Android devices \(Android 3.0 or later\)|
    |S00000001-100010|M3U8-LD|M3U8-LD|M3U8|400|64|640|Applicable to Web, iOS devices \(iPhone 4 or later and iPad\), and Android devices \(Android 3.0 or later\)|
    |S00000001-200070|MP4-4K|MP4-4K|MP4|6000|160|3840|Applicable to Web and mobile devices \(iOS and Android\)|
    |S00000001-200060|MP4-2K|MP4-2K|MP4|3500|160|2048|Applicable to Web and mobile devices \(iOS and Android\)|
    |S00000001-200040|MP4-FHD|MP4-FHD|MP4|3000|160|1920|Applicable to Web and mobile devices \(iOS and Android\)|
    |S00000001-200030|MP4-HD|MP4-HD|MP4|1800|128|1280|Applicable to Web and mobile devices \(iOS and Android\)|
    |S00000001-200020|MP4-SD|MP4-SD|MP4|800|80|848|Applicable to Web and mobile devices \(iOS and Android\)|
    |S00000001-200010|MP4-LD|MP4-LD|MP4|400|64|640|Applicable to Web and mobile devices \(iOS and Android\)|
    |S00000001-000070|FLV-4K|FLV-4K|FLV|6000|160|3840|Flash video|
    |S00000001-000060|FLV-2K|FLV-2K|FLV|3500|160|2048|Flash video|
    |S00000001-000040|FLV-FHD|FLV-FHD|FLV|3000|160|1920|Flash video|
    |S00000001-000030|FLV-HD|FLV-HD|FLV|1800|128|1280|Flash video|
    |S00000001-000020|FLV-SD|FLV-SD|FLV|800|80|848|Flash video|
    |S00000001-000010|FLV-LD|FLV-LD|FLV|400|64|640|Flash video|
    |S00000001-100070|M3U8-4K|M3U8-4K|M3U8|6000|160|3840|Applicable to Web, iOS devices \(iPhone 4 or later and iPad\), and Android devices \(Android 3.0 or later\)|
    |S00000001-100060|M3U8-2K|M3U8-2K|M3U8|3500|160|2048|Applicable to Web, iOS devices \(iPhone 4 or later and iPad\), and Android devices \(Android 3.0 or later\)|
    |S00000001-100040|M3U8-FHD|M3U8-FHD|M3U8|3000|160|1920|Applicable to Web, iOS devices \(iPhone 4 or later and iPad\), and Android devices \(Android 3.0 or later\)|
    |S00000001-100030|M3U8-HD|M3U8-HD|M3U8|1800|128|1280|Applicable to Web, iOS devices \(iPhone 4 or later and iPad\), and Android devices \(Android 3.0 or later\)|
    |S00000001-100020|M3U8-SD|M3U8-SD|M3U8|800|80|848|Applicable to Web, iOS devices \(iPhone 4 or later and iPad\), and Android devices \(Android 3.0 or later\)|
    |S00000001-100010|M3U8-LD|M3U8-LD|M3U8|400|64|640|Applicable to Web, iOS devices \(iPhone 4 or later and iPad\), and Android devices \(Android 3.0 or later\)|
    |S00000001-200070|MP4-4K|MP4-4K|MP4|6000|160|3840|Applicable to Web and mobile devices \(iOS and Android\)|
    |S00000001-200060|MP4-2K|MP4-2K|MP4|3500|160|2048|Applicable to Web and mobile devices \(iOS and Android\)|
    |S00000001-200040|MP4-FHD|MP4-FHD|MP4|3000|160|1920|Applicable to Web and mobile devices \(iOS and Android\)|
    |S00000001-200030|MP4-HD|MP4-HD|MP4|1800|128|1280|Applicable to Web and mobile devices \(iOS and Android\)|
    |S00000001-200020|MP4-SD|MP4-SD|MP4|800|80|848|Applicable to Web and mobile devices \(iOS and Android\)|
    |S00000001-200010|MP4-LD|MP4-LD|MP4|400|64|640|Applicable to Web and mobile devices \(iOS and Android\)|

-   Conversion and encapsulation templates

    A conversion and encapsulation template does not recode the input media file, but only converts the format of the file. Operations that require recoding, such as watermarking, editing, and joining, are not supported.

    **Note:** Conversion and encapsulation may fail because the sources and formats of input media files are not supported. In this case, transcoding tasks using the conversion and encapsulation template fail to run.

    Preset static templates - conversion and encapsulation templates

    |Template ID|Template name|Chinese name|Container format|
    |:----------|:------------|:-----------|:---------------|
    |S00000001-000000|FLV-COPY|Convert to the FLV format.|FLV|
    |S00000001-100000|M3U8-COPY|M3U8 slice.|M3U8|
    |S00000001-200000|MP4-COPY|Convert to the MP4 format.|MP4|

-   Audio transcoding templates

    Currently, audio transcoding templates only support output in MP3 format and are used to control the bit rate.

    <div data-spm-anchor-id="a2762.11472859.0.i214.23d8203bqpSrG0"\>Preset static templates - audio transcoding templates

    |Template ID|Template name|Chinese name|Container format|Maximum bit rate \(Kbit/s\)|
    |:----------|:------------|:-----------|:---------------|:--------------------------|
    |S00000001-300050|MP3-320|MP3-320|MP3|320|
    |S00000001-300040|MP3-192|MP3-192|MP3|192|
    |S00000001-300030|MP3-160|MP3-160|MP3|160|
    |S00000001-300020|MP3-128|MP3-128|MP3|128|
    |S00000001-300010|MP3-64|MP3-64|MP3|64|

-   Resolution doubling templates

    The output width and height double the input width and height. The output resolution is determined by the width. If the doubled width exceeds the upper threshold, the width takes the upper threshold value, and the height scales down at the original aspect ratio.

    |Template ID|Template name|Chinese name|Container format|Video bit rate \(Kbit/s\)|Audio bit rate \(Kbit/s\)|Resolution-width|Remarks|
    |:----------|:------------|:-----------|:---------------|:------------------------|:------------------------|:---------------|:------|
    |S00000001-400070|MP4-2KTo4K|MP4-2KTo4K|MP4|≤20000|128|≤3840|Applicable to Web and mobile devices \(iOS and Android\)|
    |S00000001-400040|MP4-SDToHD|MP4-SDToHD|MP4|≤6000|128|≤1280|Applicable to Web and mobile devices \(iOS and Android\)|


## Preset smart templates

**Note:** Before you use a preset smart template when submitting a transcoding task, the preset smart template must be analyzed by Media Processing. An OSS file must proactively call the SubmitAnalysisJob API and poll the QueryAnalysisJobList API to obtain a list of preset smart templates available for the OSS file.

Opened preset smart templates for bit rate control are as follows \(the output resolution fluctuates within a certain range because the resolution is optimized based on the input video\):

|Template ID|Template name|Chinese name|Container format|Bit rate range|Resolution|
|:----------|:------------|:-----------|:---------------|:-------------|:---------|
|S00000000-000050|FLV-FHD|FLV-FHD|FLV|2M~4M|\[720p,1080p\]|
|S00000000-000040|FLV-HD|FLV-HD|FLV|1M~2M|≥576p|
|S00000000-000030|FLV-SD|FLV-SD|FLV|500k~1M|≥480p|
|S00000000-000020|FLV-LD|FLV-LD|FLV|<500 Kbit/s|≥270p|
|S00000000-100050|M3U8-FHD|M3U8-FHD|M3U8|2M~4M|\[720p,1080p\]|
|S00000000-100040|M3U8-HD|M3U8-HD|M3U8|1M~2M|≥576p|
|S00000000-100030|M3U8-SD|M3U8-SD|M3U8|500k~1M|≥480p|
|S00000000-100020|M3U8-LD|M3U8-LD|M3U8|<500 Kbit/s|≥270p|
|S00000000-200050|MP4-FHD|MP4-FHD|MP4|2M~4M|\[720p,1080p\]|
|S00000000-200040|MP4-HD|MP4-HD|MP4|1M~2M|≥576p|
|S00000000-200030|MP4-SD|MP4-SD|MP4|500k~1M|≥480p|
|S00000000-200020|MP4-LD|MP4-LD|MP4|<500 Kbit/s|≥270p|

## Template ID rules:

|Serial number of the character in the ID|Definition|
|:---------------------------------------|:---------|
|1|S|
|2~9|reserved|
|10|Separator -|
|11|Category|
|12-15|Serial number|
|16|Minor version|

