# UpdateMedia {#reference_zjd_qxg_y2b .reference}

The UpdateMedia API updates media set basic information, such as the title, description, and category. This API implements full update. Each attribute must be set; otherwise, it is overwritten by a null value.

## Request parameters {#section_iqn_qbt_x2b .section}

|Parameters|Type|Required or not|Description|
|:---------|:---|:--------------|:----------|
|Action|String|Yes|操作接口名，系统规定参数，API API of the action, system required parameter. Value: UpdateMedia|
|MediaId|String|Yes|Media ID.|
|Title|String|No|Media title.-   If not set, this parameter is cleared.
-   The parameter value consists of up to 128 UTF-8 encoded bytes.

|
|Description|String|No|Description.-   If not set, this parameter is cleared.
-   The parameter value consists of up to 1,024 UTF-8 encoded bytes.

|
|CateId|Long|No|Category ID.-   If not set, this parameter is cleared.
-   The parameter value cannot be negative.

|
|Tags|String|No|List of labels.-   Multiple tags must be separated by commas \(,\). Up to 16 tags can be entered.
-   The name of a single tag consists of up to 32 bytes.
-   The tag name is encoded by UTF-8.

|
|CoverURL|String|No|Cover.-   The URL format follows the RFC 2396 standard and is subject to UTF-8 encoding and URL encoding.
-   A URL consists of up to 3,200 bytes.

|

## Response parameters {#section_ogh_wbt_x2b .section}

|Parameter|Type|Description|
|:--------|:---|:----------|
|Media|[Media](https://help.aliyun.com/document_detail/29251.html#Media)|Media|

## Examples {#section_gpq_zbt_x2b .section}

Request example

```
http://mts.cn-hangzhou.aliyuncs.com?Title=hello&<public parameter>
```

Response example

XML

```
<UpdateMediaResponse>
      <Media>
        <Format>mov,mp4,m4a,3gp,3g2,mj2</Format>
        <PublishState>Published</PublishState>
        <File>
          <State>Normal</State>
          <URL>http://zzzinput-test.oss-cn-hangzhou.aliyuncs.com/output-2016-01-07-09%3A37%3A17.mp485191.mp4</URL>
        </File>
        <Height>1080</Height>
        <MediaId>3e1cd21131a94525be55acf65888bf46</MediaId>
        <Title>hello</Title>
        <CreationTime>2016-09-14T08:30:33Z</CreationTime>
        <RunIdList>
          <RunId>47b42486019c4f688bf144c1a6ba059a</RunId>
        </RunIdList>
        <CateId>0</CateId>
        <Duration>7.965000</Duration>
        <Width>1920</Width>
        <Fps>25.0</Fps>
        <Bitrate>2659.326</Bitrate>
        <Size>2647692</Size>
      </Media>
      <RequestId>C876E3A4-4CA1-40E7-BB29-D541E6B9D9D9</RequestId>
    </UpdateMediaResponse>
```

JSON

```
{
        "Media": {
            "Format": "mov,mp4,m4a,3gp,3g2,mj2", 
            "PublishState": "Published", 
            "File": {
                "State": "Normal", 
                "URL": "http://zzzinput-test.oss-cn-hangzhou.aliyuncs.com/output-2016-01-07-09%3A37%3A17.mp485191.mp4"
            }, 
            "Height": "1080", 
            "MediaId": "3e1cd21131a94525be55acf65888bf46", 
            "Title": "hello", 
            "CreationTime": "2016-09-14T08:30:33Z", 
            "RunIdList": {
                "RunId": [
                    "47b42486019c4f688bf144c1a6ba059a"
                ]
            }, 
            "CateId": 0, 
            "Duration": "7.965000", 
            "Width": "1920", 
            "Fps": "25.0", 
            "Bitrate": "2659.326", 
            "Size": "2647692"
        }, 
        "RequestId": "C481C0BC-FD8F-448B-8C67-1C48716764D1"
    }
```

