# Quick start

1.  Create AcsClient instance.

    ```
    client = AcsClient(access_key_id, access_key_secret, mps_region_id);
    ```

2.  Create request and set parameters.

    ```
    request = SubmitJobsRequest.SubmitJobsRequest()
    request.set_accept_format('json')
    ```

3.  Initiate API request and display returned value.

    ```
    response_str = client.do_action_with_exception(request)
    response = json.loads(response_str)
    print 'PipelineName is:', response['PipelineList']['Pipeline'][0]['Name']
    print 'PipelineId is:', response['PipelineList']['Pipeline'][0]['Id']
    ```


Full code

```
# -*- coding: utf8 -*-
import json
from aliyunsdkcore.client import AcsClient
from aliyunsdkmts.request.v20140618 import SearchPipelineRequest
access_key_id = 'xxx'
access_key_secret = 'xxx'
mps_region_ids = ['cn-hangzhou', 'cn-beijing', 'cn-shenzhen', 'cn-shanghai',
                      'cn-hongkong', 'us-west-1', 'ap-southeast-1',
                      'ap-northeast-1', 'eu-central-1', 'ap-south-1']
for mps_region_id in mps_region_ids:
    print 'region is:', mps_region_id
    # Create AcsClient instance
    client = AcsClient(access_key_id, access_key_secret, mps_region_id)
    # Create request, and set parameters
    request = SearchPipelineRequest.SearchPipelineRequest()
    request.set_accept_format('json')
    # Initiate API request and diaplay returned value
    response_str = client.do_action_with_exception(request)
    response = json.loads(response_str)
    print 'PipelineName is:', response['PipelineList']['Pipeline'][0]['Name']
    print 'PipelineId is:', response['PipelineList']['Pipeline'][0]['Id']
```

