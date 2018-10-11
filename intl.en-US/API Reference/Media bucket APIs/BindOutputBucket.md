# BindOutputBucket {#reference_x12_lqh_y2b .reference}

Bind the library to theoutput media bucket.

## Request parameters {#section_iqn_qbt_x2b .section}

|Parameters|Type|Required or not|Description|
|:---------|:---|:--------------|:----------|
|Action|String|Yes|Operation interface name, system-defined parameter, value: BindOutputBucket|
|Bucket|String|Yes|The media library outputs Bucket name, no more than 64 bytes.|

## Response parameters {#section_ogh_wbt_x2b .section}

None

## Examples {#section_gpq_zbt_x2b .section}

Request example

```
http://mts.cn-hangzhou.aliyuncs.com?Bucket=watermark-zzz&<Public parameters>
```

Response example

XML

```
<Error>
      <RequestId>0A23F656-D3E6-4222-A2E8-449AD48C031D</RequestId>
      <Code>Bucket.AlreadyBind</Code>
      <Message>Bucket "watermark-zzz" already binded to media store,can not bind twice</Message>
    </Error>
```

JSON

```
{
    "RequestId": "1DB03A02-C3E1-429C-A3DA-4BFDC4294534", 
    "Code": "Bucket.AlreadyBind", 
    "Message": "Bucket \"watermark-zzz\" already binded to media store,can not bind twice "
}
```

