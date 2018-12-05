# Overview {#concept_ymt_f2y_w2b .concept}

## Purpose {#section_pgr_q2y_w2b .section}

This article describes how to initialize the library, set the media bucket and link the CDN domain name to the **Output Media Bucket**. Besides, it describes how to set media workflows, upload, and manage video files.

## Target readers {#section_esz_s2y_w2b .section}

This User Guide \> Library is a reference for those who want to:

-   Learn about library settings.

-   Link a CDN domain name to the **Output Media Bucket**.

-   Upload and manage video files.


## Library management process {#section_xfd_l2y_w2b .section}

1.  [Library settings.](reseller.en-US/User Guide/Library/Library settings.md#)

    After MPS is activated, initialize the library and set the**Input Media Bucket** and **Output Media Bucket** in **Library**.

2.  [Manage a domain name.](reseller.en-US/User Guide/Library/Domain name management.md#)

    Set a CDN domain name for the OSS Bucket which the **Output Media Bucket** is linked to.

3.  [Set media workflows.](reseller.en-US/User Guide/Library/Workflows.md#)

    Workflows support transcoding, encapsulating, watermarking, encryption, and editing functions. It helps you to construct a rapid and flexible cloud-based audio or video handling process on demand.

    Each workflow is linked to a path of the **Input Media Bucket**. When an audio or video file is uploaded to the path or to its sub-directory, the workflow is automatically triggered to perform preset processing operations and save the processing result to the specified path of the **Output Media Bucket**.

4.  [Upload video files and execute workflows.](reseller.en-US/User Guide/Library/Video file upload and workflow execution.md#)

    You can use the MPS console or OSS related upload tools to upload a video file and run workfows.

5.  [Manage videos.](reseller.en-US/User Guide/Library/Video management.md#)

    You can manage your video files through **Media Files** such as publishing and deleting videos, set the title, tag, category, and other information for a media file; or search for a media file using the information. In addition, the **Media Files** contains the format, duration, bit rate, frame rate, resolution, and other metadata of each media file. It also displays the OSS storage URL and CDN domain URL of each resource, and supports online preview and playback for each source.


