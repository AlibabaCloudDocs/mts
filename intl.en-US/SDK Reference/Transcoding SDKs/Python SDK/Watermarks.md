# Watermarks {#concept_oxd_3cc_z2b .concept}

1.  Create AcsClient instance.

    ```
    client = AcsClient(access_key_id, access_key_secret, mps_region_id);
    ```

2.  Create request, and set parameters.

    ```
    request = SubmitJobsRequest.SubmitJobsRequest()
    request.set_accept_format('json')
    ```

3.  Watermark parameters.
    -   Image watermark

        ```
        image_watermark_input = {
                            'Location': oss_location,
                            'Bucket': oss_bucket,
                            'Object': quote(image_watermark_object)
                            }
         image_watermark = {
                     'WaterMarkTemplateId': watermark_template_id,
                     'Type': 'Image',
                     'InputFile': image_watermark_input,
                     'ReferPos': 'TopRight',
                     'Width': 0.05,
                     'Dx': 0,
                     'Dy': 0
                    }
        ```

    -   Text watermark

        ```
        text_config = {
                  'Content': '5rWL6K+V5paH5a2X5rC05Y2w',
                  'FontName': 'SimSun',
                  'FontSize': 16,
                  'FontColor': 'Red',
                  'FontAlpha': 0.5,
                  'Top': 10,
                  'Left': 10
                 }
         text_watermark = {
                     'WaterMarkTemplateId': watermark_template_id,
                     'Type': 'Text',
                     'TextWaterMark': text_config
                    }
        ```

    -   Video watermark

        ```
        video_watermark_input = {
                            'Location': oss_location,
                            'Bucket': oss_bucket,
                            'Object': quote(video_watermark_object)
                            }
         video_watermark = {
                     'WaterMarkTemplateId': watermark_template_id,
                     'Type': 'Image',
                     'InputFile': video_watermark_input,
                     'ReferPos': 'BottomLeft',
                     'Height': 240,
                     'Dx': 0,
                     'Dy': 0
                    }
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
               ' message:',
               response['JobResultList']['JobResult'][0]['Message'])
    ```


Full codes

```
# -*- coding: utf8 -*-
from pprint import pprint
import json
from urllib import quote
from aliyunsdkcore.client import AcsClient
from aliyunsdkmts.request.v20140618 import SubmitJobsRequest
access_key_id = 'xxx'
access_key_secret = 'xxx'
mps_region_id = 'cn-hangzhou'
pipeline_id = 'xxx'
watermark_template_id = 'xxx'
template_id = 'S00000001-200030'
oss_location = 'oss-cn-hangzhou'
oss_bucket = 'xxx'
oss_input_object = 'input.mp4'
oss_output_object = 'output.mp4'
image_watermark_object = 'logo.png'
video_watermark_object = 'logo.mov'
# AcsClient
client = AcsClient(access_key_id, access_key_secret, mps_region_id);
# request
request = SubmitJobsRequest.SubmitJobsRequest()
request.set_accept_format('json')
# Input
job_input = {'Location': oss_location,
             'Bucket': oss_bucket,
             'Object': quote(oss_input_object) }
request.set_Input(json.dumps(job_input))
# Output
output = {'OutputObject': quote(oss_output_object)}
# Ouput->TemplateId
output['TemplateId'] = template_id
## Image Watermark
image_watermark_input = {'Location': oss_location,
                         'Bucket': oss_bucket,
                         'Object': quote(image_watermark_object) }
image_watermark = {
                  'WaterMarkTemplateId': watermark_template_id,
                  'Type': 'Image',
                  'InputFile': image_watermark_input,
                  'ReferPos': 'TopRight',
                  'Width': 0.05,
                  'Dx': 0,
                  'Dy': 0
                 }
## Text Watermark
text_config = {
               'Content': '5rWL6K+V5paH5a2X5rC05Y2w',
               'FontName': 'SimSun',
               'FontSize': 16,
               'FontColor': 'Red',
               'FontAlpha': 0.5,
               'Top': 10,
               'Left': 10
              }
text_watermark = {
                  'WaterMarkTemplateId': watermark_template_id,
                  'Type': 'Text',
                  'TextWaterMark': text_config
                 }
## Video Watermark
video_watermark_input = {'Location': oss_location,
                         'Bucket': oss_bucket,
                         'Object': quote(video_watermark_object) }
video_watermark = {
                  'WaterMarkTemplateId': watermark_template_id,
                  'Type': 'Image',
                  'InputFile': video_watermark_input,
                  'ReferPos': 'BottomLeft',
                  'Height': 240,
                  'Dx': 0,
                  'Dy': 0
                 }
# Output->Watermarks
watermarks = [image_watermark, text_watermark, video_watermark]
output['WaterMarks'] = watermarks
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

