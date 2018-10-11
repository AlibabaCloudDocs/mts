# QueryMediaList {#reference_try_ymh_y2b .reference}

The QueryMediaList API queries media sets by media IDs.

## Request parameters {#section_iqn_qbt_x2b .section}

|Parameters|Type|Required or not|Description|
|:---------|:---|:--------------|:----------|
|Action|String|Yes|API of the action, system required parameter. Value: QueryMediaList|
|MediaIds|String|Yes|A list of file names,separated by commas \(,\). A maximum of 10 file names can be entered.

|
|IncludePlayList|Boolean|No|Whether the results contain a playlist.-   Optional values: true or false.
-   Default value: false.

|
|IncludeSnapshotList|Boolean|No|Whether the results contain a screenshot list.-   Optional values: true or false.
-   Default value: false.

|
|IncludeMediaInfo|Boolean|No|Whether the results contain media information. Optional values: True/False; default value: False.|

## Response parameters {#section_ogh_wbt_x2b .section}

|Parameter|Type|Description|
|:--------|:---|:----------|
|MediaList|[Media](https://help.aliyun.com/document_detail/29251.html#Media)\[\]|Media list|
|NonExistMediaIds|String\[\]|A list of nonexistent media IDs|

## Examples {#section_gpq_zbt_x2b .section}

Request example

```
http://mts.cn-hangzhou.aliyuncs.com?MediaIds=3e1cd21131a94525be55acf65888bf46&<public parameter>
```

Response example

XML

```
<QueryMediaListResponse>
      <NonExistMediaIds/>
      <MediaList>
        <Media>
          <CoverURL>http://zzyoutputbucket.oss-cn-hangzhou.aliyuncs.com/47b42486019c4f688bf144c1a6ba059a%2F0.jpg</CoverURL>
          <Format>mov,mp4,m4a,3gp,3g2,mj2</Format>
          <PublishState>Published</PublishState>
          <File>
            <State>Normal</State>
            <URL>http://zzzinput-test.oss-cn-hangzhou.aliyuncs.com/output-2016-01-07-09%3A37%3A17.mp485191.mp4</URL>
          </File>
          <Height>1080</Height>
          <MediaId>3e1cd21131a94525be55acf65888bf46</MediaId>
          <Title>output-2016-01-07-09:37:17.mp485191.mp4</Title>
          <CreationTime>2016-09-14T08:30:33Z</CreationTime>
          <RunIdList>
            <RunId>47b42486019c4f688bf144c1a6ba059a</RunId>
          </RunIdList>
          <CateId>0</CateId>
          <MediaInfo>
            <Format/>
            <Streams/>
          </MediaInfo>
          <Duration>7.965000</Duration>
          <Width>1920</Width>
          <Fps>25.0</Fps>
          <Bitrate>2659.326</Bitrate>
          <Size>2647692</Size>
        </Media>
      </MediaList>
      <RequestId>2F6D69DE-DAD0-4D8A-BB2C-DACAE76D60E3</RequestId>
    </QueryMediaListResponse>
```

JSON

```
{
        "NonExistMediaIds": {
            "MediaId": [ ]
        }, 
        "MediaList": {
            "Media": [
                {
                    "CoverURL": "http://zzyoutputbucket.oss-cn-hangzhou.aliyuncs.com/47b42486019c4f688bf144c1a6ba059a%2F0.jpg", 
                    "Format": "mov,mp4,m4a,3gp,3g2,mj2", 
                    "PublishState": "Published", 
                    "File": {
                        "State": "Normal", 
                        "URL": "http://zzzinput-test.oss-cn-hangzhou.aliyuncs.com/output-2016-01-07-09%3A37%3A17.mp485191.mp4"
                    }, 
                    "Height": "1080", 
                    "MediaId": "3e1cd21131a94525be55acf65888bf46", 
                    "Title": "output-2016-01-07-09:37:17.mp485191.mp4", 
                    "CreationTime": "2016-09-14T08:30:33Z", 
                    "RunIdList": {
                        "RunId": [
                            "47b42486019c4f688bf144c1a6ba059a"
                        ]
                    }, 
                    "CateId": 0, 
                    "MediaInfo": {
                        "Format": { }, 
                        "Streams": { }
                    }, 
                    "Duration": "7.965000", 
                    "Width": "1920", 
                    "Fps": "25.0", 
                    "Bitrate": "2659.326", 
                    "Size": "2647692"
                }
            ]
        }, 
        "RequestId": "F1C8B6C4-1E47-4423-9BC8-2F5DDBD892DC"
    }
```

