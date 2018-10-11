# BindInputBucket {#reference_mpp_dqh_y2b .reference}

Binds the library to the input media bucket .

**Note:** Behavior: After the library is bound to this Bucket, if the user completes the operation such as calling PutObject, a corresponding notification will be triggered and sent to MPS. It can be understood as adding a new trigger-like function on this OSS Bucket so that whenever there is an uploaded or deleted file in this Bucket, MPS will be notified to handle it.

## Request parameters {#section_iqn_qbt_x2b .section}

|Parameters|Type|Required or not|Description|
|:---------|:---|:--------------|:----------|
|Action|String|Yes|Operation interface name, system-defined parameter, value: BindInputBucket|
|Bucket|String|Yes|Bucket name, no more than 64 bytes|

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
<BindInputBucketResponse>
  <RequestId>740DD2EF-5452-4990-970D-5E3D87BFF201</RequestId>
</BindInputBucketResponse>
```

JSON

```
{
  "RequestId":"740DD2EF-5452-4990-970D-5E3D87BFF201"
  }
```

