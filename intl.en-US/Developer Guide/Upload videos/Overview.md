# Overview {#concept_wk4_vtt_1fb .concept}

## Upload {#section_etw_xtt_1fb .section}

Provides upload SDK, supports the web version \(JavaScript\) and mobile versions \(Android and iOS\).

Uploads a video file using the console or a third-party tool.

## Features {#section_x2w_25t_1fb .section}

Provides user-friendly APIs. You only need to specify the location to store local and OSS files.

Supports resumable upload, multi-file queue, ultra-large files, recovery from network anomalies, and security mechanisms.

A media workflow is automatically triggered.

## Media workflow triggering. {#section_gk2_j5t_1fb .section}

After a multimedia file is uploaded to the input bucket and path specified by the media workflow, the media workflow is automatically executed based on the specified process.

The following conditions must be met when an OSS file is uploaded to automatically trigger a media workflow:

-   Match the media workflow.

    For more information about workflow triggering and matching rules, see [Add media](../../../../reseller.en-US/API Reference/Media APIs/AddMedia.md#). The workflow is in the `Activated` state.

-   Match the file name extension.

    Triggering requirement is that the file is a multi-media file, Media Files service determines through the extension of a file. The file does not contain an extension \(the file name does not contain the extension separator "."\) or the extension meets the following rules:

    -   Video

        3gp, asf, avi, dat, dv, flv, f4v, gif, m2t, m3u8, m4v, mj2, mjpeg, mkv, mov, mp4, mpe, mpg, mpeg, mts, ogg, qt, rm, rmvb, swf, ts, vob, wmv and webm.

    -   Audio

        aac, ac3, acm, amr, ape, caf, flac, m4a, mp3, ra, wav, wma and aiff.

-   Specify media attributes.

    You can specify media attributes, including the title, tag, description, category, cover URL, and custom data, to trigger a media workflow. For more information about the attribute description, see “Request parameters” in [Add Media](../../../../reseller.en-US/API Reference/Media APIs/AddMedia.md#).


## Security {#section_rv4_p5t_1fb .section}

In normal cases, a video file is directly uploaded using a client. In this case, the AccessKey must be securely stored on the client. Once being disclosed, the AccessKey is exposed to high risk and hard to be replaced. We recommend that the client access an application to obtain the AccessKey and use the [Token](../../../../reseller.en-US/Developer Guide/API reference (STS)/Introduction.md#) provided by RAM.

## Recommended process. {#section_ymq_t5t_1fb .section}

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/11385/153993559811314_en-US.png)

1.  Request the token.

    Before each time a file is uploaded, you can use a video application \(in App or web mode\) to access the application service of the business end. The application service obtains a token from RAM and sends it back to the video application. This ensures the security, implements identity verification and permission control, and records your upload history.

    Before using a token, [Set a subaccount and permissions](reseller.en-US/Developer Guide/Upload videos/Set a subaccount and authorization.md#).

    For more information, see [Java sample code](reseller.en-US/Developer Guide/Upload videos/Request security token - Java sample code.md#). \( For more information about how to use the token in other languages, see [STS documentation](../../../../reseller.en-US/Developer Guide/API reference (STS)/Introduction.md#)\).

2.  Upload a file.

    After integrating the upload SDK to the video application, you can upload files using the obtained token. For more information, see [Usage instruction](../../../../reseller.en-US/SDK Reference/Upload SDK/Instructions for use.md#).

    -   Web.

        As JavaScript files are stored in an application or CDN domain and video files are stored in an OSS domain, a cross-region request is involved when a JavaScript file is uploaded. In this case, [Set CORS](reseller.en-US/Developer Guide/Upload videos/Set CORS.md#).

        [JavaScript](../../../../reseller.en-US/SDK Reference/Upload SDK/JavaScript version.md#)

    -   Mobile.

        [Android](../../../../reseller.en-US/SDK Reference/Upload SDK/Android version.md#)

        [iOS](../../../../reseller.en-US/SDK Reference/Upload SDK/iOS version.md#)


