# Instructions for use {#concept_lhr_2dq_y2b .concept}

The upload SDK provides the file list management and upload control functions. File list management allows you to add, delete, cancel, resume, retrieve, and clear files. Upload control allows you to start, stop, pause, and resume file upload. The SDK provides callback events to monitor the status and progress changes during upload.

## Upload process {#section_zlz_fdq_y2b .section}

**Initialize the upload SDK** \> **Select a file** \> **Add the file to the list** \> **Start upload** \> **Upload completion events**.

-   Initialize the upload SDK

    The AccessKey and token can be used to grant permissions during initialization. Considering the security of the AccessKey stored on the client, it is recommended that the AccessKey be used only for testing and the token be used in the production environment. For details, see [Developer guide \> Upload a video file \> Overview](https://help.aliyun.com/document_detail/42615.html).

-   Select a file

    Select a local file to be uploaded.

-   Add the file to the list

    Add all files to be uploaded to the list using addFile.

-   Start upload.

    Call start to start the upload process.

-   Upload completion events

    The events include OnUploadSucceed and OnUploadFailed.


## Concepts and descriptions {#section_x5q_ldq_y2b .section}

-   Multipart upload and status

    The SDK uses the multipart upload mode, in which the status is valid only for one execution. If the app exits due to a specific reason \(for example, shutdown, closing the browser page, closing the app, or abnormal app exit\), the file must be uploaded again.

-   Authorization expiration

    The token is only valid for a certain period. After the token expires, the upload process is interrupted and cannot be automatically resumed. To resume upload, obtain a new token from the backend and call the resumeUploadWithAuth function.

-   Switching between a 3G/4G network and a Wi-Fi network on the mobile end

    To avoid traffic waste on 3G/4G networks, when the app switches to a 3G/4G network, it must automatically detect the network and call pause to suspend upload. After the app detects that a Wi-Fi network is used, it calls resume to resume upload.

-   The SDKs of the following three types of terminals are provided:

    -   [HTML5](https://help.aliyun.com/document_detail/48471.html): It can be integrated to PC browsers. The development language is JavaScript.

    -   [iOS](https://help.aliyun.com/document_detail/48473.html): It can be integrated to iOS apps in the language of Object-C.

    -   [Android](https://help.aliyun.com/document_detail/48474.html): It can be integrated to Android apps in the language of Java.


## Features {#section_wvr_mdq_y2b .section}

File list management

|API|Description|
|:--|:----------|
|addFile|Adds a file to the list. Files are uploaded in order of addition.|
|deleteFile|Deletes a file from the list.|
|cancelFile|Cancels a file in the list but does not delete the file from the list. After this API is used, upload of this file is skipped \(not supported by the JavaScript version\).|
|resumeFile|Resumes the status of the file that is canceled in the list \(not supported by the JavaScript version\). This API is not used to resume upload.|
|listFiles|Obtains the list.|
|clearFiles|Clears the list. After this API is used, upload stops and files, even the files being uploaded, are cleared \(not supported by the JavaScript version\).|

Upload control

|API|Description|
|:--|:----------|
|start|Starts upload.|
|stop|Stop uploading|
|pause|Stops upload \(JavaScript version is not supported\).|
|resume|Pauses upload \(not supported by the JavaScript version\).|
|resumeUploadWithToken|Uses a new token to resume upload after the existing token expires.|

Callback events

|Event|Description|
|:----|:----------|
|OnUploadStarted|This event is triggered when upload of each file starts.|
|OnUploadSucceed|Upload succeeds.|
|OnUploadFailed|Upload fails. If resumable errors occur, for example the network has an exception or times out, the file upload can be resumed. If non-resumable errors occur, for example the upload credential is incorrect or the file does not exist, the file upload fails.|
|OnUploadProgress|The upload progress report. This event is triggered when multipart upload succeeds.|
|OnUploadTokenExpired|The token times out. To resume upload, obtain a new token from the server and call the resumeUploadWithToken function.|
|OnUploadRetry|This event is triggered when the status switches from normal to abnormal during upload For example, the network has an exception or times out \(not supported by the JavaScript version\).|
|OnUploadRetryResume|This event is triggered when the status is resumed from abnormal to normal during upload \(not supported by the JavaScript version\).|

