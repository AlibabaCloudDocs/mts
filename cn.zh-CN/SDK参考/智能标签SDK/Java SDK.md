# Java SDK

mts的Java SDK版本需要在2.7.6版本及以上。如果使用maven管理Java依赖包，您可以在工程pom.xml文件中添加下面依赖。

```
<dependency>
    <groupId>com.aliyun</groupId>
    <artifactId>aliyun-java-sdk-core</artifactId>
    <version>4.5.3</version>
</dependency>

<dependency>
    <groupId>com.aliyun</groupId>
    <artifactId>aliyun-java-sdk-mts</artifactId>
    <version>2.7.6</version>
</dependency>
```

## 提交智能标签作业

```
import com.aliyuncs.DefaultAcsClient;
import com.aliyuncs.IAcsClient;
import com.aliyuncs.exceptions.ClientException;
import com.aliyuncs.exceptions.ServerException;
import com.aliyuncs.http.FormatType;
import com.aliyuncs.profile.DefaultProfile;
import com.google.gson.Gson;
import java.util.*;
import com.aliyuncs.mts.model.v20140618.*;

public class SubmitSmarttagJob {

    public static void main(String[] args) {
        // 创建IAcsClient实例，需要补充AK信息和需要使用的服务区域，区域以beijing为例。
        DefaultProfile profile = DefaultProfile.getProfile("cn-beijing", "<accessKeyId>", "<accessSecret>");
        IAcsClient client = new DefaultAcsClient(profile);

        // 创建request，并设置参数。
        SubmitSmarttagJobRequest request = new SubmitSmarttagJobRequest();
        request.setInput("oss://xxx.mp4");      // 需要分析的文件OSS地址
        request.setPipelineId("");              // 管道ID，若填空，表示默认管道
        request.setTitle("<yourTitle>");        // 文件标题
        request.setContent("<yourContent>");    // 文件内容描述，选填
        request.setAcceptFormat(FormatType.JSON);

        try {
            // 接收请求结果response。
            SubmitSmarttagJobResponse response = client.getAcsResponse(request);
            System.out.println(new Gson().toJson(response));
        } catch (ServerException e) {
            e.printStackTrace();
        } catch (ClientException e) {
            System.out.println("ErrCode:" + e.getErrCode());
            System.out.println("ErrMsg:" + e.getErrMsg());
            System.out.println("RequestId:" + e.getRequestId());
        }

    }
}
```

## 查询智能标签作业

```
import com.aliyuncs.DefaultAcsClient;
import com.aliyuncs.IAcsClient;
import com.aliyuncs.exceptions.ClientException;
import com.aliyuncs.exceptions.ServerException;
import com.aliyuncs.profile.DefaultProfile;
import com.google.gson.Gson;
import java.util.*;
import com.aliyuncs.mts.model.v20140618.*;

public class QuerySmarttagJob {

    public static void main(String[] args) {
        // 创建IAcsClient实例，需要补充AK信息和需要使用的服务区域，区域以beijing为例。
        DefaultProfile profile = DefaultProfile.getProfile("cn-beijing", "<accessKeyId>", "<accessSecret>");
        IAcsClient client = new DefaultAcsClient(profile);

        // 创建request，并设置参数。
        QuerySmarttagJobRequest request = new QuerySmarttagJobRequest();
        request.setJobId("<JobId>");

        try {
            // 接收请求结果response。
            QuerySmarttagJobResponse response = client.getAcsResponse(request);
            System.out.println(new Gson().toJson(response));
        } catch (ServerException e) {
            e.printStackTrace();
        } catch (ClientException e) {
            System.out.println("ErrCode:" + e.getErrCode());
            System.out.println("ErrMsg:" + e.getErrMsg());
            System.out.println("RequestId:" + e.getRequestId());
        }

    }
}
```

## 添加模板

```
import com.aliyuncs.DefaultAcsClient;
import com.aliyuncs.IAcsClient;
import com.aliyuncs.exceptions.ClientException;
import com.aliyuncs.exceptions.ServerException;
import com.aliyuncs.profile.DefaultProfile;
import com.google.gson.Gson;
import java.util.*;
import com.aliyuncs.mts.model.v20140618.*;

public class AddSmarttagTemplate {

    public static void main(String[] args) {
        // 创建IAcsClient实例，需要补充AK信息和需要使用的服务区域，区域以beijing为例。
        DefaultProfile profile = DefaultProfile.getProfile("cn-beijing", "<accessKeyId>", "<accessSecret>");
        IAcsClient client = new DefaultAcsClient(profile);

        // 创建request，并设置参数。
        AddSmarttagTemplateRequest request = new AddSmarttagTemplateRequest();
        request.setIndustry("media");
        request.setScene("search");
        request.setAnalyseTypes("ocr,asr,classification,shows,face,role,object,tvstation,action,emotion,landmark,scene");
        request.setTemplateName("test");
        request.setFaceCategoryIds("politician,sensitive,celebrity");
        request.setIsDefault(false);

        try {
            // 接收请求结果response。
            AddSmarttagTemplateResponse response = client.getAcsResponse(request);
            System.out.println(new Gson().toJson(response));
        } catch (ServerException e) {
            e.printStackTrace();
        } catch (ClientException e) {
            System.out.println("ErrCode:" + e.getErrCode());
            System.out.println("ErrMsg:" + e.getErrMsg());
            System.out.println("RequestId:" + e.getRequestId());
        }

    }
}
```

## 查询模板

```
import com.aliyuncs.DefaultAcsClient;
import com.aliyuncs.IAcsClient;
import com.aliyuncs.exceptions.ClientException;
import com.aliyuncs.exceptions.ServerException;
import com.aliyuncs.profile.DefaultProfile;
import com.google.gson.Gson;
import java.util.*;
import com.aliyuncs.mts.model.v20140618.*;

public class QuerySmarttagTemplateList {

    public static void main(String[] args) {
        // 创建IAcsClient实例，需要补充AK信息和需要使用的服务区域，区域以beijing为例。
        DefaultProfile profile = DefaultProfile.getProfile("cn-beijing", "<accessKeyId>", "<accessSecret>");
        IAcsClient client = new DefaultAcsClient(profile);

        // 创建request，并设置参数。
        QuerySmarttagTemplateListRequest request = new QuerySmarttagTemplateListRequest();
        request.setTemplateId("6407");

        try {
            // 接收请求结果response。
            QuerySmarttagTemplateListResponse response = client.getAcsResponse(request);
            System.out.println(new Gson().toJson(response));
        } catch (ServerException e) {
            e.printStackTrace();
        } catch (ClientException e) {
            System.out.println("ErrCode:" + e.getErrCode());
            System.out.println("ErrMsg:" + e.getErrMsg());
            System.out.println("RequestId:" + e.getRequestId());
        }

    }
}
```

## 更新模板

```
import com.aliyuncs.DefaultAcsClient;
import com.aliyuncs.IAcsClient;
import com.aliyuncs.exceptions.ClientException;
import com.aliyuncs.exceptions.ServerException;
import com.aliyuncs.profile.DefaultProfile;
import com.google.gson.Gson;
import java.util.*;
import com.aliyuncs.mts.model.v20140618.*;

public class UpdateSmarttagTemplate {

    public static void main(String[] args) {
        // 创建IAcsClient实例，需要补充AK信息和需要使用的服务区域，区域以beijing为例。
        DefaultProfile profile = DefaultProfile.getProfile("cn-beijing", "<accessKeyId>", "<accessSecret>");
        IAcsClient client = new DefaultAcsClient(profile);

        // 创建request，并设置参数。
        UpdateSmarttagTemplateRequest request = new UpdateSmarttagTemplateRequest();
        request.setTemplateName("update测试");
        request.setTemplateId("6407");

        try {
            // 接收请求结果response。
            UpdateSmarttagTemplateResponse response = client.getAcsResponse(request);
            System.out.println(new Gson().toJson(response));
        } catch (ServerException e) {
            e.printStackTrace();
        } catch (ClientException e) {
            System.out.println("ErrCode:" + e.getErrCode());
            System.out.println("ErrMsg:" + e.getErrMsg());
            System.out.println("RequestId:" + e.getRequestId());
        }

    }
}
```

## 删除模板

```
import com.aliyuncs.DefaultAcsClient;
import com.aliyuncs.IAcsClient;
import com.aliyuncs.exceptions.ClientException;
import com.aliyuncs.exceptions.ServerException;
import com.aliyuncs.profile.DefaultProfile;
import com.google.gson.Gson;
import java.util.*;
import com.aliyuncs.mts.model.v20140618.*;

public class DeleteSmarttagTemplate {

    public static void main(String[] args) {
        // 创建IAcsClient实例，需要补充AK信息和需要使用的服务区域，区域以beijing为例。
        DefaultProfile profile = DefaultProfile.getProfile("cn-beijing", "<accessKeyId>", "<accessSecret>");
        IAcsClient client = new DefaultAcsClient(profile);

        // 创建request，并设置参数。
        DeleteSmarttagTemplateRequest request = new DeleteSmarttagTemplateRequest();
        request.setTemplateId("6407");

        try {
            // 接收请求结果response。
            DeleteSmarttagTemplateResponse response = client.getAcsResponse(request);
            System.out.println(new Gson().toJson(response));
        } catch (ServerException e) {
            e.printStackTrace();
        } catch (ClientException e) {
            System.out.println("ErrCode:" + e.getErrCode());
            System.out.println("ErrMsg:" + e.getErrMsg());
            System.out.println("RequestId:" + e.getRequestId());
        }

    }
}
```

## 注册自定义人脸

```
import com.aliyuncs.DefaultAcsClient;
import com.aliyuncs.IAcsClient;
import com.aliyuncs.exceptions.ClientException;
import com.aliyuncs.exceptions.ServerException;
import com.aliyuncs.profile.DefaultProfile;
import com.google.gson.Gson;
import java.util.*;
import com.aliyuncs.mts.model.v20140618.*;

public class RegisterCustomFace {

    public static void main(String[] args) {
        // 创建IAcsClient实例，需要补充AK信息和需要使用的服务区域，区域以beijing为例。
        DefaultProfile profile = DefaultProfile.getProfile("cn-beijing", "<accessKeyId>", "<accessSecret>");
        IAcsClient client = new DefaultAcsClient(profile);

        // 创建request，并设置参数。
        RegisterCustomFaceRequest request = new RegisterCustomFaceRequest();
        request.setPersonId("<yourPersonId>");
        request.setImageUrl("http://xxxxx.jpeg");
        request.setCategoryId("<yourCategoryId>");

        try {
            // 接收请求结果response。
            RegisterCustomFaceResponse response = client.getAcsResponse(request);
            System.out.println(new Gson().toJson(response));
        } catch (ServerException e) {
            e.printStackTrace();
        } catch (ClientException e) {
            System.out.println("ErrCode:" + e.getErrCode());
            System.out.println("ErrMsg:" + e.getErrMsg());
            System.out.println("RequestId:" + e.getRequestId());
        }

    }
}
```

## 注销自定义人脸

```
import com.aliyuncs.DefaultAcsClient;
import com.aliyuncs.IAcsClient;
import com.aliyuncs.exceptions.ClientException;
import com.aliyuncs.exceptions.ServerException;
import com.aliyuncs.profile.DefaultProfile;
import com.google.gson.Gson;
import java.util.*;
import com.aliyuncs.mts.model.v20140618.*;

public class UnregisterCustomFace {

    public static void main(String[] args) {
        // 创建IAcsClient实例，需要补充AK信息和需要使用的服务区域，区域以beijing为例。
        DefaultProfile profile = DefaultProfile.getProfile("cn-beijing", "<accessKeyId>", "<accessSecret>");
        IAcsClient client = new DefaultAcsClient(profile);

        // 创建request，并设置参数。
        UnregisterCustomFaceRequest request = new UnregisterCustomFaceRequest();
        request.setPersonId("<yourPersonId>");
        request.setFaceId("<FaceId>");
        request.setCategoryId("<yourCategoryId>");

        try {
            // 接收请求结果response。
            UnregisterCustomFaceResponse response = client.getAcsResponse(request);
            System.out.println(new Gson().toJson(response));
        } catch (ServerException e) {
            e.printStackTrace();
        } catch (ClientException e) {
            System.out.println("ErrCode:" + e.getErrCode());
            System.out.println("ErrMsg:" + e.getErrMsg());
            System.out.println("RequestId:" + e.getRequestId());
        }

    }
}
```

## 添加自定义人物库或人物标签

```
import com.aliyuncs.DefaultAcsClient;
import com.aliyuncs.IAcsClient;
import com.aliyuncs.exceptions.ClientException;
import com.aliyuncs.exceptions.ServerException;
import com.aliyuncs.profile.DefaultProfile;
import com.google.gson.Gson;
import java.util.*;
import com.aliyuncs.mts.model.v20140618.*;

public class TagCustomPerson {

    public static void main(String[] args) {
        // 创建IAcsClient实例，需要补充AK信息和需要使用的服务区域，区域以beijing为例。
        DefaultProfile profile = DefaultProfile.getProfile("cn-beijing", "<accessKeyId>", "<accessSecret>");
        IAcsClient client = new DefaultAcsClient(profile);

        // 创建request，并设置参数。
        TagCustomPersonRequest request = new TagCustomPersonRequest();
        request.setCategoryId("<yourCategoryId>");
        request.setCategoryName("<yourCategoryaName>");
        request.setCategoryDescription("<yourCategoryDescription>");

        try {
            // 接收请求结果response。
            TagCustomPersonResponse response = client.getAcsResponse(request);
            System.out.println(new Gson().toJson(response));
        } catch (ServerException e) {
            e.printStackTrace();
        } catch (ClientException e) {
            System.out.println("ErrCode:" + e.getErrCode());
            System.out.println("ErrMsg:" + e.getErrMsg());
            System.out.println("RequestId:" + e.getRequestId());
        }

    }
}
```

## 列出⼈物库所有⼈物和⼈脸信息

```
import com.aliyuncs.DefaultAcsClient;
import com.aliyuncs.IAcsClient;
import com.aliyuncs.exceptions.ClientException;
import com.aliyuncs.exceptions.ServerException;
import com.aliyuncs.profile.DefaultProfile;
import com.google.gson.Gson;
import java.util.*;
import com.aliyuncs.mts.model.v20140618.*;

public class ListCustomPersons {

    public static void main(String[] args) {
        // 创建IAcsClient实例，需要补充AK信息和需要使用的服务区域，区域以beijing为例。
        DefaultProfile profile = DefaultProfile.getProfile("cn-beijing", "<accessKeyId>", "<accessSecret>");
        IAcsClient client = new DefaultAcsClient(profile);

        // 创建request，并设置参数。
        ListCustomPersonsRequest request = new ListCustomPersonsRequest();
        request.setCategoryId("<yourCategoryId>");
        request.setPersonId("<yourPersonId>");

        try {
            // 接收请求结果response。
            ListCustomPersonsResponse response = client.getAcsResponse(request);
            System.out.println(new Gson().toJson(response));
        } catch (ServerException e) {
            e.printStackTrace();
        } catch (ClientException e) {
            System.out.println("ErrCode:" + e.getErrCode());
            System.out.println("ErrMsg:" + e.getErrMsg());
            System.out.println("RequestId:" + e.getRequestId());
        }

    }
}
```

