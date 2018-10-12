# ListMedia {#reference_aj2_xnh_y2b .reference}

The ListMedia API lists all media resources, which are sorted by creation time in descending order.

## Request parameters {#section_iqn_qbt_x2b .section}

|Parameters|Type|Required or not|Description|
|:---------|:---|:--------------|:----------|
|Action|String|Yes|API of the action, system required parameter. Value: ListMedia|
|NextPageToken|String|No|Identifier of the next page, which is a 32-bit UUID.|
|MaximumPageSize|Long|No|Maximum number of media workflow execution instances that can be returned.-   Value range: \[1, 100\].
-   Default value: 10.

|
|From|String|No|Start time.-   The date format follows the ISO8601 standard and uses UTC time.
-   Format: YYYY-MM-DDThh:mm:ssZ.
-   Example: 2014-01-10T12:00:00Z \(January 10, 2014 at 20:00:00, Beijing time\).

 |
|To|String|No|End time.-   The date format follows the ISO8601 standard and uses UTC time.
-   Format: YYYY-MM-DDThh:mm:ssZ.
-   Example: 2014-01-11T12:00:00Z \(January 11, 2014 at 20:00:00, Beijing time\).

|

## Response parameters {#section_ogh_wbt_x2b .section}

|Parameter|Type|Description|
|:--------|:---|:----------|
|MediaList|[Media](reseller.en-US/API Reference/Data types.md#)\[\]|Media list|
|NextPageToken|String|Identifier of the next page, which is a 32-bit UUID|

## Examples {#section_gpq_zbt_x2b .section}

Request example

```
http://mts.cn-hangzhou.aliyuncs.com/?From=2014-01-10T12%3A00%3A00Z&To=2014-01-11T12%3A00%3A00Z&Action=ListMedia&<public parameter
```

Response example

XML

```
<LisMediaResponse>
    <RequestId>58CBF1B8-048C-4550-B59C-F6EA57A8CEB6</RequestId>
    <NextPageToken>8c6ca184c0e47098a5b665e2a126797</NextPageToken>
    <MediaList list="true">
        <Media>
          <CreationTime>2016-09-20T05:26:48Z</CreationTime>
          <CoverURL>http://zzzinput-test.oss-cn-hangzhou.aliyuncs.com/tail_comm-33.jpg</CoverURL>
          <RunIdList>
            <RunId>2490402d4a204f899a64473844e50a24</RunId>
          </RunIdList>
          <CateId>0</CateId>
          <Description>tag1,tag2</Description>
          <PublishState>UnPublish</PublishState>
          <File>
            <State>Normal</State>
            <URL>http://zzzinput-test.oss-cn-hangzhou.aliyuncs.com/tail_comm-493.mp4</URL>
          </File>
          <MediaId>b2cb1183559e49ad81e767045624b9b8</MediaId>
          <Title>10</Title>
        </Media>           
      </MediaList>
</LisMediaResponse>
```

JSON

```
{
    "NextPageToken":"8c6ca184c0e47098a5b665e2a126797",
    "RequestId":"06CB45EF-903C-4464-A812-AD276948D5BB",
    "MediaList":{
          "Media": [
                {
                    "CreationTime": "2016-09-20T05:26:48Z", 
                    "CoverURL": "http://zzzinput-test.oss-cn-hangzhou.aliyuncs.com/tail_comm-33.jpg", 
                    "RunIdList": {
                        "RunId": [
                            "2490402d4a204f899a64473844e50a24"
                        ]
                    }, 
                    "CateId": 0, 
                    "Description": "tag1,tag2", 
                    "PublishState": "UnPublish", 
                    "File": {
                        "State": "Normal", 
                        "URL": "http://zzzinput-test.oss-cn-hangzhou.aliyuncs.com/tail_comm-493.mp4"
                    }, 
                    "MediaId": "b2cb1183559e49ad81e767045624b9b8", 
                    "Title": "10"
                }
            ]
    }
```

