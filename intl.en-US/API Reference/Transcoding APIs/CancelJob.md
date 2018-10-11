# CancelJob {#reference_ocb_w2t_x2b .reference}

The CancelJob API cancels transcoding tasks. The API has the following restrictions:

**Note:** 

-   Only tasks in “Submitted” state can be canceled.
-   We recommend that you first call the UpdatePipeline API \(UpdatePipeline\) to set the MPS queue status to Paused to stop task scheduling, and then call this API to cancel the tasks. After canceling the tasks, recover the MPS queue status to Active. In this way, tasks in the MPS queue can be scheduled and executed.

## Request parameters {#section_iqn_qbt_x2b .section}

|Parameters|Type|Required or not|Description|
|:---------|:---|:--------------|:----------|
|Action|String|Yes|API of the action, system required parameter. Value: CancelJob|
|JobId|String|Yes|Task ID.|

## Response parameters {#section_ogh_wbt_x2b .section}

|Parameter|Type|Description|
|:--------|:---|:----------|
|JobId|String|Task ID|

## Examples {#section_gpq_zbt_x2b .section}

Request example

```
http://mts.cn-hangzhou.aliyuncs.com/?Action=CancelJob&JobId=88c6ca184c0e47098a5b665e2a126797&<Public parameters>
```

Response example

XML

```
<CancelJobResponse>
        <RequestId>25818875-5F78-4A13-BEF6-D7393642CA58</RequestId>
        <JobId>88c6ca184c0e47098a5b665e2a126797</JobId>
    </CancelJobResponse>
```

JSON

```
{
        "RequestId": "25818875-5F78-4A13-BEF6-D7393642CA58",
        "JobId": "88c6ca184c0e47098a5b665e2a126797"
    }
```

