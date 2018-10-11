# QuerySnapshotJobList {#reference_e1f_jng_y2b .reference}

After screenshot tasks are submitted, Media Processing asynchronously takes screenshots. This API can be used to query the screenshot task results.

## Request parameters {#section_iqn_qbt_x2b .section}

|Parameters|Type|Required or not|Description|
|:---------|:---|:--------------|:----------|
|Action|String|Yes|API of the action, system required parameter. Value: QuerySnapshotJobList|
|SnapshotJobIds|String|Yes|List of screenshot task IDs.A maximum of 10 screenshot task IDs can be entered.

|

## Response parameters {#section_ogh_wbt_x2b .section}

|Parameter|Type|Description|
|:--------|:---|:----------|
|SnapshotJobList|AliyunSnapshotJob\[\]|List of screenshot tasks.|
|NonExistSnapshotJobIds|String\[\]|List of non-existing screenshot task IDs. If no data exists, this structure is not returned.|

## Examples {#section_gpq_zbt_x2b .section}

Request example

```
http://mts.cn-hangzhou.aliyuncs.com?Action=QuerySnapshotJobList&SnapshotJobIds=88c6ca184c0e47098a5b665e2a126797&<Public parameter>
```

Response example

XML

```
<QuerySnapshotJobListResponse>
        <RequestId>
            25818875-5F78-4A13-BEF6-D7393642CA58
        </RequestId>
        <SnapshotJobList list="true">
                <SnapshotJob>
                    <Id>88c6ca184c0e47098a5b665e2a126797</Id>
                    <State>Success</State>
                    <Code> </Code>
                    <Message> </Message>
                    <SnapshotConfig>
                       <OutputFile>
                         <Bucket>example-001</Bucket>
                         <Location>oss-cn-hangzhou</Location>
                         <Object>example.png</Object>
                       </OutputFile>
                       <Time>4</Time>
                    </SnapshotConfig>
                    <PipelineId>88c6ca184c0e47098a5b665e2a126797</PipelineId>
                    <UserData>testid-001</UserData>
                    <CreationTime>2014-01-10T12:00:00Z</CreationTime>
                </SnapshotJob>
        </SnapshotJobList>
    </QuerySnapshotJobListResponse>
```

JSON

```
{
        "RequestId": "25818875-5F78-4A13-BEF6-D7393642CA58",
        "SnapshotJobList": {
            "SnapshotJob": [{
                 "Id": "88c6ca184c0e47098a5b665e2a126797",
                 "State": "Success",
                 "Code": "",
                 "Message": "",
                 "SnapshotConfig": {
                     "OutputFile": {
                        "Bucket": "example-001",
                        "Location": "oss-cn-hangzhou",
                        "Object": "example.png "
                     },
                     "Time": "5"
                  },
                  "PipelineId": "88c6ca184c0e47098a5b665e2a126797",
                  "UserData": "testid-001",
                  "CreationTime": "2014-01-10T12:00:00Z"
            }]
            }
    }
```

