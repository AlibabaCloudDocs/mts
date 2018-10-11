# ListAllMediaBucket {#reference_a5b_5qh_y2b .reference}

Lists all the media buckets in the library.

## Request parameters {#section_iqn_qbt_x2b .section}

|Parameters|Type|Required or not|Description|
|:---------|:---|:--------------|:----------|
|Action|String|Yes|Operation interface name, system-defined parameter, value: ListAllMediaBucket|

## Response parameters {#section_ogh_wbt_x2b .section}

|Parameter|Type|Description|
|:--------|:---|:----------|
|MediaBucket|[MediaBucket](https://help.aliyun.com/document_detail/29251.html#MediaBucket)\[\]|Media Bucket List|

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

