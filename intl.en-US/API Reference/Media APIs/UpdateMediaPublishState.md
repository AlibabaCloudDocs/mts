# UpdateMediaPublishState {#reference_nzm_3mh_y2b .reference}

The UpdateMediaPublishState API updates the status of media publishing. Publishing is equivalent to setting all media resources to be played. The screenshot file access permission inherits the access permission on the bucket that stores the screenshot file. Media resources that are not published are set to Private.

## Request parameters {#section_iqn_qbt_x2b .section}

|Parameters|Type|Required or not|Description|
|:---------|:---|:--------------|:----------|
|Action|String|Yes|API of the action, system required parameter. Value: UpdateMediaPublishState|
|MediaId|String|Yes|Media ID.|
|Publish|Boolean|Yes|Publication status,which can be True or False.

|

Rules of media publication status transition:

-   Default status:

    The default status of media publication is “Initial”. A media file is in the default status under two conditions:

    -   Add media

        After a media file is generated \(a media workflow is also triggered\) for the first time, the media file is neither published nor unpublished while workflow execution is in progress. The media file is in “Initial” state. After workflow execution is complete, the media file is set to a definite state \(according to the workflow configuration\).

    -   Delete media

        After a media file is deleted, the publication status is meaningless and the file is in “Initial” state. To restore the deleted media file to the library, execute a workflow on the file as new media.

-   Migration rules:

    |Caller|Current status|Status after transition|Allowed or not|
    |:-----|:-------------|:----------------------|:-------------|
    |API|Initial|Published|No|
    |API|Initial|Unpublished|No|
    |API|Published|Unpublished|Yes|
    |API|Unpublished|Published|Yes|
    |Workflow execution|Initial|Published|Yes|
    |Workflow execution|Initial|Unpublished|Yes|
    |Workflow execution|Published|Unpublished|No|
    |Workflow execution|Unpublished|Published|No|


## Response parameters {#section_ogh_wbt_x2b .section}

None

## Examples {#section_gpq_zbt_x2b .section}

Request example

```
http://mts.cn-hangzhou.aliyuncs.com?Publish=True&<public parameter>
```

Response example

XML

```
<UpdateMediaPublishStateResponse>
      <RequestId>179F447A-B688-4268-9662-9ECC43B235BF</RequestId>
    </UpdateMediaPublishStateResponse>
```

JSON

```
{
    "RequestId":"D591D0DE-8341-4C51-A519-8BF68498DDDC"
    }
```

