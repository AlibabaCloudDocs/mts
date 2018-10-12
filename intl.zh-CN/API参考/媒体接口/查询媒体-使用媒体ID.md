# 查询媒体-使用媒体ID {#reference_try_ymh_y2b .reference}

查询媒体列表。

## 请求参数 {#section_iqn_qbt_x2b .section}

|名称|类型|是否必须|描述|
|:-|:-|:---|:-|
|Action|String|是|操作接口名，系统规定参数，取值：QueryMediaList|
|MediaIds|String|是|文件列表。用逗号分隔，最多10个

|
|IncludePlayList|Boolean|否|结果是否包含播放信息。-   范围：true、false。
-   默认值：false

|
|IncludeSnapshotList|Boolean|否|结果是否包含截图信息。-   范围：true、false。
-   默认值：false

|
|IncludeMediaInfo|Boolean|否|结果是否包含媒体信息，范围：true、false，默认值：false|

## 返回参数 {#section_ogh_wbt_x2b .section}

|名称|类型|描述|
|:-|:-|:-|
|MediaList|[Media](intl.zh-CN/API参考/数据类型.md#)\[\]|媒体列表|
|NonExistMediaIds|String\[\]|不存在的MediaId列表|

## 示例 {#section_gpq_zbt_x2b .section}

请求示例

```
http://mts.cn-hangzhou.aliyuncs.com?MediaIds=3e1cd21131a94525be55acf65888bf46&<公共参数>
```

返回示例

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

