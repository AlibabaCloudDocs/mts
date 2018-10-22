# Splicing and simple cutting {#concept_cfb_2jc_z2b .concept}

1.  Create AcsClient instance.

    ```
    client = AcsClient(access_key_id, access_key_secret, mps_region_id);
    ```

2.  Create request and set parameters.

    ```
    request = SubmitJobsRequest.SubmitJobsRequest()
    request.set_accept_format('json')
    ```

3.  Sets transcode parameters.
    -   Input

        ```
        job_input = {'Location': oss_location,
                'Bucket': oss_bucket,
                'Object': quote(head_object) }
         request.set_Input(json.dumps(job_input))
        ```

    -   Output

        ```
        output = {'OutputObject': quote(oss_output_object)}
        ```

        -   Video

            ```
            output['Video'] = {'Width': 1280,
                               'Height': 720}
            ```

        -   MergeList

            ```
            merge_video = {'MergeURL': 'http://%s.%s.aliyuncs.com/%s'%(oss_bucket, oss_location, quote(oss_input_object))}
             merge_tail = {'MergeURL': 'http://%s.%s.aliyuncs.com/%s'%(oss_bucket, oss_location, quote(tail_object))}
             output['MergeList'] = [merge_video, merge_tail]
            ```

4.  Initiate API request and display returned value.

    ```
    response_str = client.do_action_with_exception(request)
      response = json.loads(response_str)
      print 'RequestId is:', response['RequestId']
      if response['JobResultList']['JobResult'][0]['Success']:
          print 'JobId is:', response['JobResultList']['JobResult'][0]['Job']['JobId']
      else:
          print ('SubmitJobs Failed code:',
                 response['JobResultList']['JobResult'][0]['Code'],
                 'message:',
                 response['JobResultList']['JobResult'][0]['Message'])
    ```


Full codes

```
# -*- coding: utf8 -*-
import json
from urllib import quote
from aliyunsdkcore.client import AcsClient
from aliyunsdkmts.request.v20140618 import SubmitJobsRequest
access_key_id = 'xxx'
access_key_secret = 'xxx'
mps_region_id = 'cn-hangzhou'
pipeline_id = 'xxx'
template_id = 'S00000001-200030'
oss_location = 'oss-cn-hangzhou'
oss_bucket = 'xxx'
oss_input_object = 'input.mp4'
oss_output_object = 'output.mp4'
head_object = 'head.mp4'
tail_object = 'tail.mp4'
# AcsClient
client = AcsClient(access_key_id, access_key_secret, mps_region_id);
# request
request = SubmitJobsRequest.SubmitJobsRequest()
request.set_accept_format('json')
# Input
job_input = {'Location': oss_location,
             'Bucket': oss_bucket,
             'Object': quote(head_object) }
request.set_Input(json.dumps(job_input))
# Output
output = {'OutputObject': quote(oss_output_object)}
# Ouput->TemplateId
output['TemplateId'] = template_id
# Ouput->Video
output['Video'] = {'Width': 1280,
                   'Height': 720}
# Output->MergeList
merge_video = {'MergeURL': 'http://%s.%s.aliyuncs.com/%s'%(oss_bucket, oss_location, quote(oss_input_object))}
merge_tail = {'MergeURL': 'http://%s.%s.aliyuncs.com/%s'%(oss_bucket, oss_location, quote(tail_object))}
output['MergeList'] = [merge_video, merge_tail]
# Outputs
outputs = [output]
request.set_Outputs(json.dumps(outputs))
request.set_OutputBucket(oss_bucket)
request.set_OutputLocation(oss_location)
# PipelineId
request.set_PipelineId(pipeline_id)
# call api
response_str = client.do_action_with_exception(request)
response = json.loads(response_str)
print 'RequestId is:', response['RequestId']
if response['JobResultList']['JobResult'][0]['Success']:
    print 'JobId is:', response['JobResultList']['JobResult'][0]['Job']['JobId']
else:
    print ('SubmitJobs Failed code:',
           response['JobResultList']['JobResult'][0]['Code'],
           ' message:',
           response['JobResultList']['JobResult'][0]['Message'])
```

