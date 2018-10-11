# Workflows and media {#concept_tmq_yrj_z2b .concept}

This article introduces several basic concepts and relationships for MPS to help developers better understand and use media processing service.

Concept description:

-   Media

    Media includes one input video/audio media file and all the relevant output file, such as transcoding/screenshots/media info/AI tags. Input files and media have a one-to-one relationship and are uniquely identified by the Media ID.

    Media Files

    The Media Files is a collection of all media, with media being the smallest unit for media files.

-   Workflow

    Workflow is a like a factory that automates the production of media, it is uniquely identified by a MediaWorkflowId.

    **Note:** Media Workflow also refers to the workflow.

    -   Event

        Each node in the workflow is called an activity. According to actual requirements, it can be run in parallel \(for example, the task A, B, C\) or in a serialized manner \(for example: the task A1, A2\). In addition to the initial input activity and the final release reporting activity, activities supports various types of tasks, such as transcoding tasks and screenshot tasks.

        -   Starting input activity

            Configure the triggering path of the storage associated with the workflow, and automatically trigger the task running whenever the video/audio multi-media file is uploaded to the corresponding path.

        -   Finishing post reporting activities

            After the workflow finished running, it sends an implementation message. The running result contains the absolute address of the media ID and the multi-media file, so that the specific multi-media file can be run.

        -   Task activity

            All parameters supported by the task can be configured in the task activity.

    -   Matching rules

        For example, the uploaded file is `http://bucket.oss-cn-hangzhou.aliyuncs.com/A/B/C/test1.flv`, the result of the configured triggering path are as follows:

        |Path|Matching or not|
        |:---|:--------------|
        |[http://bucket.oss-cn-hangzhou.aliyuncs.com/A/B/C/](http://bucket.oss-cn-hangzhou.aliyuncs.com/A/B/C/?spm=a2c4g.11186623.2.5.7bac67e3tFgvaJ)|Yes|
        |[http://bucket.oss-cn-hangzhou.aliyuncs.com/A/B/C2/](http://bucket.oss-cn-hangzhou.aliyuncs.com/A/B/C2/?spm=a2c4g.11186623.2.6.7bac67e3tFgvaJ)|No|
        |[http://bucket.oss-cn-hangzhou.aliyuncs.com/A/B/](http://bucket.oss-cn-hangzhou.aliyuncs.com/A/B/?spm=a2c4g.11186623.2.7.7bac67e3tFgvaJ)|Yes|
        |[http://bucket.oss-cn-hangzhou.aliyuncs.com/A/B2/](http://bucket.oss-cn-hangzhou.aliyuncs.com/A/B2/?spm=a2c4g.11186623.2.8.7bac67e3tFgvaJ)|No|
        |[http://bucket.oss-cn-hangzhou.aliyuncs.com/A/](http://bucket.oss-cn-hangzhou.aliyuncs.com/A/?spm=a2c4g.11186623.2.9.7bac67e3tFgvaJ)|Yes|
        |[http://bucket.oss-cn-hangzhou.aliyuncs.com/A2/B/C/](http://bucket.oss-cn-hangzhou.aliyuncs.com/A2/B/C/?spm=a2c4g.11186623.2.10.7bac67e3tFgvaJ)|No|
        |[http://bucket.oss-cn-hangzhou.aliyuncs.com/A/B/C/test](http://bucket.oss-cn-hangzhou.aliyuncs.com/A/B/C/test?spm=a2c4g.11186623.2.11.7bac67e3tFgvaJ)|Yes|
        |[http://bucket.oss-cn-hangzhou.aliyuncs.com/A/B/C/test2](http://bucket.oss-cn-hangzhou.aliyuncs.com/A/B/C/test2?spm=a2c4g.11186623.2.12.7bac67e3tFgvaJ)|No|

    -   Extension matching rules

        The automatic triggering mechanism during uploading checks the file extension to avoid generating ineffective data \(such as pdf, word files and other files\).

        **Note:** API manual triggering mechaism does not check the extension.

        The files does not have the extension \(file does not include extension separator “.”\), or the extension conforms to the following rules:

        -   Video

            3gp, asf, avi, dat, dv, flv, f4v, gif, m2t, m3u8, m4v, mj2, mjpeg, mkv, mov, mp4, mpe, mpg, mpeg, mts, ogg, qt, rm, rmvb, swf, ts, vob, wmv, webm

        -   Audio

            aac, ac3, acm, amr, ape, caf, flac, m4a, mp3, ra, wav, wma, aiff

    -   Workflow running

        Each time you upload a matching multi-media file, it is triggered once. If the same multi-media file is uploaded for multiple times, multiple runnings are triggered. Each running has a unique RunId identifier.

        In addition to the automatic triggering mechanism when uploading, the workflow targets stored multi-media files in storage and also provides a manual API triggering mechanism. Each call to the API triggers a running.

    -   User data

        You can enter custom user data parameters \(for example, commodity IDs\) each time you run. The custom user data parameters are then returned in the message notification without the need to record the absolute path of the media ID or multi-media file in the business system. Meanwhile, you can use custom user data, such as commodity IDs, to associate the business system.


