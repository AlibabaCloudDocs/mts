# 查询媒体-使用OSS文件地址 {#reference_ev3_lnh_y2b .reference}

使用OSS文件地址查询媒体。

## 请求参数 {#section_iqn_qbt_x2b .section}

|名称|类型|是否必须|描述|
|:-|:-|:---|:-|
|Action|String|是|操作接口名，系统规定参数，取值：QueryMediaListByURL|
|FileURLs|String|是|文件地址。-   用逗号分隔，最多10个。
-   URL遵循 RFC 3,986（UTF8编码，并对保留字符进行URLEncode），不超过3,200字节。

|
|IncludePlayList|Boolean|否|结果是否包含播放信息。-   范围：true、false。
-   默认值：false

|
|IncludeSnapshotList|Boolean|否|结果是否包含截图信息。-   范围：true、false。
-   默认值：false

|
|IncludeMediaInfo|Boolean|否|结果是否包含媒体信息。-   范围：true、false。
-   默认值：false

|

## 返回参数 {#section_ogh_wbt_x2b .section}

|名称|类型|描述|
|:-|:-|:-|
|MediaList|[Media](intl.zh-CN/API参考/数据类型.md#)\[\]|媒体列表|
|NonExistFileURLs|String\[\]|不存在的媒体列表|

## 示例 {#section_gpq_zbt_x2b .section}

请求示例

```
http://mts.cn-hangzhou.aliyuncs.com?FileURLs=http%3A%2F%2Fzzzinput-test.oss-cn-hangzhou.aliyuncs.com%2Foutput-2016-01-07-09%253A37%253A17.mp485191.mp4&<公共参数>
```

返回示例

XML

```
<QueryMediaListByURLResponse>
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
      <RequestId>135F7C8D-1E90-4163-8475-15497039B59D</RequestId>
      <NonExistFileURLs/>
    </QueryMediaListByURLResponse>
```

JSON

```
{
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
        "RequestId": "96E71ED6-491D-4515-9AB2-AB06AFF71F70", 
        "NonExistFileURLs": {
            "FileURL": [ ]
        }
    }
```

