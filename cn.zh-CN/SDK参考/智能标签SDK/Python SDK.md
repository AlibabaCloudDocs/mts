# Python SDK

阿里云Python SDK推荐的pip安装方式：

-   Python 2.x

    ```
    ```
    pip install aliyun-python-sdk-core
    pip install aliyun-python-sdk-mts
    ```
    ```

-   Python 3.x

    ```
    ```
    pip install aliyun-python-sdk-core-v3
    pip install aliyun-python-sdk-mts
    ```
    ```


## 提交智能标签作业

```
#!/usr/bin/env python
#coding=utf-8

from aliyunsdkcore.client import AcsClient
from aliyunsdkcore.acs_exception.exceptions import ClientException
from aliyunsdkcore.acs_exception.exceptions import ServerException
from aliyunsdkmts.request.v20140618.SubmitSmarttagJobRequest import SubmitSmarttagJobRequest

# 创建AcsClient实例。
client = AcsClient('<accessKeyId>', '<accessSecret>', 'cn-beijing')

# 创建request，并设置参数。
request = SubmitSmarttagJobRequest()
request.set_accept_format('json')
request.set_Title("<yourTitle>")
request.set_Content("<yourContent>")
request.set_PipelineId("")
request.set_Input("http://xxx.mp4")

# 接收请求结果response。
response = client.do_action_with_exception(request)
# python2:  print(response) 
print(str(response, encoding='utf-8'))
```

## 查询智能标签作业

```
#!/usr/bin/env python
#coding=utf-8

from aliyunsdkcore.client import AcsClient
from aliyunsdkcore.acs_exception.exceptions import ClientException
from aliyunsdkcore.acs_exception.exceptions import ServerException
from aliyunsdkmts.request.v20140618.QuerySmarttagJobRequest import QuerySmarttagJobRequest

# 创建AcsClient实例。
client = AcsClient('<accessKeyId>', '<accessSecret>', 'cn-beijing')

# 创建request，并设置参数。
request = QuerySmarttagJobRequest()
request.set_accept_format('json')
request.set_JobId("<JobId>")

# 接收请求结果response。
response = client.do_action_with_exception(request)
# python2:  print(response) 
print(str(response, encoding='utf-8'))
```

## 添加模板

```
#!/usr/bin/env python
#coding=utf-8

from aliyunsdkcore.client import AcsClient
from aliyunsdkcore.acs_exception.exceptions import ClientException
from aliyunsdkcore.acs_exception.exceptions import ServerException
from aliyunsdkmts.request.v20140618.AddSmarttagTemplateRequest import AddSmarttagTemplateRequest

# 创建AcsClient实例。
client = AcsClient('<accessKeyId>', '<accessSecret>', 'cn-beijing')

# 创建request，并设置参数。
request = AddSmarttagTemplateRequest()
request.set_accept_format('json')
request.set_Industry("media")
request.set_Scene("search")
request.set_AnalyseTypes("ocr,asr,classification,shows,face,role,object,tvstation,action,emotion,landmark,scene")
request.set_TemplateName("test")
request.set_FaceCategoryIds("politician,sensitive,celebrity")
request.set_IsDefault(False)

# 接收请求结果response。
response = client.do_action_with_exception(request)
# python2:  print(response) 
print(str(response, encoding='utf-8'))
```

## 查询模板

```
#!/usr/bin/env python
#coding=utf-8

from aliyunsdkcore.client import AcsClient
from aliyunsdkcore.acs_exception.exceptions import ClientException
from aliyunsdkcore.acs_exception.exceptions import ServerException
from aliyunsdkmts.request.v20140618.QuerySmarttagTemplateListRequest import QuerySmarttagTemplateListRequest

# 创建AcsClient实例。
client = AcsClient('<accessKeyId>', '<accessSecret>', 'cn-beijing')

# 创建request，并设置参数。
request = QuerySmarttagTemplateListRequest()
request.set_accept_format('json')
request.set_TemplateId("6407")

# 接收请求结果response。
response = client.do_action_with_exception(request)
# python2:  print(response) 
print(str(response, encoding='utf-8'))
```

## 更新模板

```
#!/usr/bin/env python
#coding=utf-8

from aliyunsdkcore.client import AcsClient
from aliyunsdkcore.acs_exception.exceptions import ClientException
from aliyunsdkcore.acs_exception.exceptions import ServerException
from aliyunsdkmts.request.v20140618.UpdateSmarttagTemplateRequest import UpdateSmarttagTemplateRequest

# 创建AcsClient实例。
client = AcsClient('<accessKeyId>', '<accessSecret>', 'cn-beijing')

# 创建request，并设置参数。
request = UpdateSmarttagTemplateRequest()
request.set_accept_format('json')
request.set_TemplateName("update测试")
request.set_TemplateId("6407")

# 接收请求结果response。
response = client.do_action_with_exception(request)
# python2:  print(response) 
print(str(response, encoding='utf-8'))
```

## 删除模板

```
#!/usr/bin/env python
#coding=utf-8

from aliyunsdkcore.client import AcsClient
from aliyunsdkcore.acs_exception.exceptions import ClientException
from aliyunsdkcore.acs_exception.exceptions import ServerException
from aliyunsdkmts.request.v20140618.DeleteSmarttagTemplateRequest import DeleteSmarttagTemplateRequest

# 创建AcsClient实例。
client = AcsClient('<accessKeyId>', '<accessSecret>', 'cn-beijing')

# 创建request，并设置参数。
request = DeleteSmarttagTemplateRequest()
request.set_accept_format('json')
request.set_TemplateId("6407")

# 接收请求结果response。
response = client.do_action_with_exception(request)
# python2:  print(response) 
print(str(response, encoding='utf-8'))
```

## 注册自定义人脸

```
#!/usr/bin/env python
#coding=utf-8

from aliyunsdkcore.client import AcsClient
from aliyunsdkcore.acs_exception.exceptions import ClientException
from aliyunsdkcore.acs_exception.exceptions import ServerException
from aliyunsdkmts.request.v20140618.RegisterCustomFaceRequest import RegisterCustomFaceRequest

# 创建AcsClient实例。
client = AcsClient('<accessKeyId>', '<accessSecret>', 'cn-beijing')

# 创建request，并设置参数。
request = RegisterCustomFaceRequest()
request.set_accept_format('json')
request.set_PersonId("<yourPersonId>")
request.set_ImageUrl("http://xxxxx.jpeg")
request.set_CategoryId("<yourCategoryId>")

# 接收请求结果response。
response = client.do_action_with_exception(request)
# python2:  print(response) 
print(str(response, encoding='utf-8'))
```

## 注销自定义人脸

```
#!/usr/bin/env python
#coding=utf-8

from aliyunsdkcore.client import AcsClient
from aliyunsdkcore.acs_exception.exceptions import ClientException
from aliyunsdkcore.acs_exception.exceptions import ServerException
from aliyunsdkmts.request.v20140618.UnregisterCustomFaceRequest import UnregisterCustomFaceRequest

# 创建AcsClient实例。
client = AcsClient('<accessKeyId>', '<accessSecret>', 'cn-beijing')

# 创建request，并设置参数。
request = UnregisterCustomFaceRequest()
request.set_accept_format('json')
request.set_PersonId("<yourPersonId>")
request.set_FaceId("<FaceId>")
request.set_CategoryId("<yourCategoryId>")

# 接收请求结果response。
response = client.do_action_with_exception(request)
# python2:  print(response) 
print(str(response, encoding='utf-8'))
```

## 添加自定义人物库或人物标签

```
#!/usr/bin/env python
#coding=utf-8

from aliyunsdkcore.client import AcsClient
from aliyunsdkcore.acs_exception.exceptions import ClientException
from aliyunsdkcore.acs_exception.exceptions import ServerException
from aliyunsdkmts.request.v20140618.TagCustomPersonRequest import TagCustomPersonRequest

# 创建AcsClient实例。
client = AcsClient('<accessKeyId>', '<accessSecret>', 'cn-beijing')

# 创建request，并设置参数。
request = TagCustomPersonRequest()
request.set_accept_format('json')
request.set_CategoryId("<yourCategoryId>")
request.set_CategoryName("<yourCategoryaName>")
request.set_CategoryDescription("<yourCategoryDescription>")

# 接收请求结果response。
response = client.do_action_with_exception(request)
# python2:  print(response) 
print(str(response, encoding='utf-8'))
```

## 列出⼈物库所有⼈物和⼈脸信息

```
#!/usr/bin/env python
#coding=utf-8

from aliyunsdkcore.client import AcsClient
from aliyunsdkcore.acs_exception.exceptions import ClientException
from aliyunsdkcore.acs_exception.exceptions import ServerException
from aliyunsdkmts.request.v20140618.ListCustomPersonsRequest import ListCustomPersonsRequest

# 创建AcsClient实例。
client = AcsClient('<accessKeyId>', '<accessSecret>', 'cn-beijing')

# 创建request，并设置参数。
request = ListCustomPersonsRequest()
request.set_accept_format('json')
request.set_CategoryId("<yourCategoryId>")
request.set_PersonId("<yourPersonId>")

# 接收请求结果response。
response = client.do_action_with_exception(request)
# python2:  print(response) 
print(str(response, encoding='utf-8'))
```

