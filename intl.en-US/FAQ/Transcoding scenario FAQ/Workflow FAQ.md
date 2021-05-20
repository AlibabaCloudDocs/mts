Workflow FAQ 
=================================

in this paper, a workflow can be used in the common problems and the solution of the corresponding method. 

How do I upload a file? {#h2--1}
--------------------------------

You can upload files through the ApsaraVideo for Media Processing console or the graphical management tools provided by OSS. It supports multipart upload, resumable upload upload and batch upload. 

* [console]()

  

* [OSS graphical management tool upload](https://help.aliyun.com/document_detail/61872.html?spm=a2c4g.11186623.2.23.4db4656bHjI8BI)

  




Is the transcoding operation automatically performed after audio and video files are uploaded? {#h2--2}
-------------------------------------------------------------------------------------------------------

file extension within a specified range of file upload is followed by automatically trigger the workflow, which then performs the. 

When creating a media workflow, you need to specify the input file path of the workflow. When the audio and video files with the following suffixes under the path are uploaded, the service will automatically trigger the media workflow and perform various operations set in the media workflow for this input file. 

**Files with file suffixes in the following ranges can automatically trigger workflow execution:** 

* Videos:

  3gp、asf、avi、dat、dv、flv、f4v、gif、m2t、m3u8、m4v、mj2、mjpeg、mkv、mov、mp4、mpe、mpg、mpeg、mts、ogg、qt、rm、rmvb、swf、ts、vob、wmv、webm
  

* Audio

  aac、ac3、acm、amr、ape、caf、flac、m4a、mp3、ra、wav、wma、aiff
  




**Matching rules triggered by workflow execution:** 

If the path of the uploaded file contains the input path of the workflow setting, the workflow will be triggered, for example:
**Notice**

If the input path of workflow A is the AA/BB directory under BucketA, the upload to AA/BB/a.mp4 under BucketA and the upload to AA/BB/CC/b.flv under BucketA will trigger workflow A. When a workflow is disabled, execution is not automatically triggered. 

Can the video be uploaded to the media workflow input path through the OSS tool and then transcoding is activated? {#h2--oss-3}
-------------------------------------------------------------------------------------------------------------------------------

Yes, you can. The service is automatically triggered according to the OSS input position of the specified workflow when the file is uploaded. There is no limit to the upload method. It is possible to use the console, API and OSS client tools. However, when the workflow is disabled, the execution will not be automatically triggered. 

After the video is uploaded, the corresponding video cannot be found in the media library? 
---------------------------------------------------------------------------------------------------------------

* Only videos that trigger transcoding through workflow are displayed in the media library, but API-triggered videos are not displayed.

  

* Please confirm whether the video upload is successful. If the corresponding transcoding task ID is not found in OSS file transcoding management, please confirm whether the video is successfully uploaded to the OSS input path configured by the workflow.

  

* Please confirm whether you have uploaded a video with the same name. When uploading a video with the same name, no new media will be generated. Please search for media by video name in the media library.

  




What operations are supported by media workflows? {#h2--4}
----------------------------------------------------------

Currently, media workflow supports operations such as screenshots, transcoding, template analysis, and release management. 

How to name the output file of the transcoding node in the media workflow? {#h2--5}
-----------------------------------------------------------------------------------

Because the media workflow provides convenience for the processing of batch files, it also brings the naming problem of output file names. For your convenience, the system provides the following variables for you to choose from:

* {RunId}: media workflow execution ID

  

* {ObjectPrefix}: original file path without bucket information

  

* {FileName}: Original file name without extension

  

* {ExtName}: the original file extension

  




For example, when the input file is `http://a.oss-cn-hangzhou.aliyuncs.com/news/video/foooo.mp4`, the three variable values related to the original file are:

* {ObjectPrefix}:news/video/

  

* {FileName}:foooo

  

* {ExtName}:.mp4

  




You can set the output Object to: `vod/{ObjectPrefix}{FileName}_HD.flv`, the output Object after the input file is transcoded is: `vod/news/video/foooo_HD.flv`

in addition the screenshot node adds a unique variable:

* {SnapshotTime}: screenshot time, unit: milliseconds

  




What message modes are supported by media workflows? {#h2--6}
-------------------------------------------------------------

Media workflow supports Message Service **queues** and **notifications** . You can configure them on input nodes. When the media workflow is executed, it will trigger execution and send messages according to the set queue or notification topic at the end of execution. 

How do I obtain the URL of the playback address after the video transcoding is completed? {#h2--url-7}
------------------------------------------------------------------------------------------------------

You can manage videos on the **console** - **Media Library** page. You can access the video details page through the **management** link of each video. You can see the OSS address and Alibaba Cloud Content Delivery Network acceleration address of each output (if the OSS bucket has a configuration Alibaba Cloud Content Delivery Network). In addition, you can obtain the video programmatically through the SDK. For more information, see [Media details](/intl.en-US/Developer Guide/Media library management/Media details.md). 

Does the queue or notification mechanism bound on the transcoding pipeline take effect at the same time when the media workflow is executed? {#h2--8}
-----------------------------------------------------------------------------------------------------------------------------------------------------

The current media workflow triggers the execution of jobs, ignoring the message mechanism bound on the transcoding pipeline. 

Why is the Alibaba Cloud Content Delivery Network address of the transcoded output file unable to play preview on the console? {#h2--cdn-9}
-------------------------------------------------------------------------------------------------------------------------------------------

This situation is generally caused by your Alibaba Cloud Content Delivery Network domain name not being resolved to the corresponding CNAME. You can query the CNAME configuration of your domain name by using the following command:

    nslookup -type=cname [Your Domain Name]



CNAME settings. For more information, see [Domain name management](/intl.en-US/User Guide/Domain name management.md). 

Why does the transcoded M3U8 file fail to play preview on the console? {#h2--m3u8-10}
-------------------------------------------------------------------------------------

first of all, `output media Bucket` the read-write permissions for the needs to be set to **public read** . 

Secondly, because the console uses Alibaba Cloud Flash player, you need to place the crossdomain.xml file under the root directory of the bucket where the M3U8 file is located. The file contains the domain name where the player is located, otherwise it cannot be played. 

In order for the console to preview and play your M3U8 file normally, please place the crossdomain.xml file with the following contents under the Bucket root directory where the M3U8 file is located:

    <?xml version="1.0" encoding="UTF-8"?> <cross-domain-policy xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:noNamespaceSchemaLocation="http://www.adobe.com/xml/schemas/PolicyFile.xsd"> <allow-access-from domain="*.alicdn.com"/> </cross-domain-policy>



The `*.alicdn.com` is the domain name where the console player is located. If you use another Flash player, add a new allow-access-from domain record to the domain name where the player is located. 
