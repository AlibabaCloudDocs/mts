# ListAllMediaBucket {#reference_a5b_5qh_y2b .reference}

Lists all the media buckets in the library.

## Request parameters {#section_iqn_qbt_x2b .section}

|Parameters|Type|Required or not|Description|
|:---------|:---|:--------------|:----------|
|Action|String|Yes|Operation interface name, system-defined parameter. Value: ListAllMediaBucket|
|NextPageToken |String|No|Token of the next page. If you sen a request for the first request, the token will be returned. Add the token when you send a request the second time.|
|MaximumPageSize|Integer|No|The maximum value of media bucket in response of the request.-   Value range: \[1,100\]
-   Default value: 50

|

## Response parameters {#section_ogh_wbt_x2b .section}

|Parameter|Type|Description|
|:--------|:---|:----------|
|MediaBucket|[MediaBucket](reseller.en-US/API Reference/Data types.md#)\[\]|Media Bucket List|
|NextPageToken|String|Query the token of the next page.|

## Example {#section_gpq_zbt_x2b .section}

Request example

```
http://mts.cn-hangzhou.aliyuncs.com?Action=ListAllMediaBucket&<Public parameters>
```

Response example

XML

```
<ListAllMediaBucketResponse>
      <RequestId>79760D91-D3CF-4165-8068-B7E2836EF62A</RequestId>
      <NextPageToken>BohcFbNNj7F0RcUsHx44Qx</NextPageToken>
      <MediaBucketList>
        <MediaBucket>
          <Type>Input</Type>
          <Bucket>watermark-zzz</Bucket>
        </MediaBucket>
        <MediaBucket>
          <Type>Output</Type>
          <Bucket>zzyoutputbucket</Bucket>
        </MediaBucket>
        <MediaBucket>
          <Type>Input</Type>
          <Bucket>zzzinput-test</Bucket>
        </MediaBucket>
      </MediaBucketList>
    </ListAllMediaBucketResponse>
```

JSON

```
{
    "RequestId": "50B35FE9-18B2-45D6-B8C4-99D05E7570F6", 
    "NextPageToken":"BohcFbNNj7F0RcUsHx44Qx"
    "MediaBucketList": {
        "MediaBucket": [
            {
                "Type": "Input", 
                "Bucket": "watermark-zzz"
            }, 
            {
                "Type": "Output", 
                "Bucket": "zzyoutputbucket"
            }, 
            {
                "Type": "Input", 
                "Bucket": "zzzinput-test"
            }
        ]
    }
}
```

