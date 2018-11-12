# 创建Java版ChinaDRM工作流 {#concept_jww_wxg_tfb .concept}

本文介绍如何创建Java版ChinaDRM工作流。

## 使用限制 {#section_r1c_fyg_tfb .section}

-   使用ChinaDRM前，请联系您的商务经理，开通服务并获取产品报价。
-   播放视频需集成阿里云播放器SDK，目前仅支持Android与iOS移动端播放。

## 安装 {#section_vmc_hyg_tfb .section}

MPS SDK详情参见 [安装](../../../../cn.zh-CN/SDK参考/媒体转码SDK/Java SDK/安装.md#)。

## 示例代码 {#section_fdd_ryg_tfb .section}

```
import com.aliyuncs.DefaultAcsClient;
import com.aliyuncs.exceptions.ClientException;
import com.aliyuncs.mts.model.v20140618.AddMediaWorkflowRequest;
import com.aliyuncs.mts.model.v20140618.AddMediaWorkflowResponse;
import com.aliyuncs.profile.DefaultProfile;

public class ChinaDRMWorkflow {
    //以下变量均以实际情况进行替换
    final String REGION_ID = "cn-shanghai";
    final String ACCESS_KEY_ID = "idid"; 
    final String ACCESS_KEY_SECRET = "keykey";
    final String PIPELINE_ID = "pipelineid";
    final String OSS_LOCATION = "oss-" + REGION_ID;
    final String INPUT_BUCKET = "inputbucket"; //输入bucket,
    final String INPUT_PATH = "inputpath"; //输入媒体的路径
    final String OUTPUT_BUCKET = "outputbucket"; //输出bucket
    final String OUTPUT_PATH = "outputpath"; //输出媒体的路径
    final String ENCRYPTION_TYPE = "ChinaDRM";
    private DefaultAcsClient client;

    public static String WORKFLOW_TEMPLATE = "{" +
        "  \"Activities\": {" +
        "    \"Act-Start\": {" +
        "      \"Name\": \"Act-Start\"," +
        "      \"Parameters\": {" +
        "        \"PipelineId\": \"PIPELINE_ID\"," +
        "        \"InputFile\": \"{\\\"Bucket\\\":\\\"INPUT_BUCKET\\\",\\\"Location\\\":\\\"OSS_LOCATION\\\",\\\"Object\\\":\\\"INPUT_PATH\\\"}\"" +
        "      }," +
        "      \"Type\": \"Start\"" +
        "    }," +
        "    \"Act-ChinaDRM-LD\": {" +
        "      \"Name\": \"Act-ChinaDRM-LD\"," +
        "      \"Parameters\": {" +
        "        \"Outputs\": \"[{\\\"Object\\\":\\\"OUTPUT_PATH/{MediaId}/{RunId}/LD/{FileName}\\\",\\\"Encryption\\\":{\\\"Type\\\":\\\"ENCRYPTION_TYPE\\\"},\\\"TemplateId\\\":\\\"S00000001-100010\\\"}]\"," +
        "        \"OutputBucket\": \"OUTPUT_BUCKET\"," +
        "        \"OutputLocation\": \"OSS_LOCATION\"" +
        "      }," +
        "      \"Type\": \"Transcode\"" +
        "    }," +
        "    \"Act-ChinaDRM-SD\": {" +
        "      \"Name\": \"Act-ChinaDRM-SD\"," +
        "      \"Parameters\": {" +
        "        \"Outputs\": \"[{\\\"Object\\\":\\\"OUTPUT_PATH/{MediaId}/{RunId}/SD/{FileName}\\\",\\\"Encryption\\\":{\\\"Type\\\":\\\"ENCRYPTION_TYPE\\\"},\\\"TemplateId\\\":\\\"S00000001-100020\\\"}]\"," +
        "        \"OutputBucket\": \"OUTPUT_BUCKET\"," +
        "        \"OutputLocation\": \"OSS_LOCATION\"" +
        "      }," +
        "      \"Type\": \"Transcode\"" +
        "    }," +
        "    \"Act-ChinaDRM-HD\": {" +
        "      \"Name\": \"Act-ChinaDRM-HD\"," +
        "      \"Parameters\": {" +
        "        \"Outputs\": \"[{\\\"Object\\\":\\\"OUTPUT_PATH/{MediaId}/{RunId}/HD/{FileName}\\\",\\\"Encryption\\\":{\\\"Type\\\":\\\"ENCRYPTION_TYPE\\\"},\\\"TemplateId\\\":\\\"S00000001-100030\\\"}]\"," +
        "        \"OutputBucket\": \"OUTPUT_BUCKET\"," +
        "        \"OutputLocation\": \"OSS_LOCATION\"" +
        "      }," +
        "      \"Type\": \"Transcode\"" +
        "    }," +
        "    \"Act-Report\": {" +
        "      \"Name\": \"Act-Report\"," +
        "      \"Parameters\": {" +
        "        \"PublishType\": \"Auto\"" +
        "      }," +
        "      \"Type\": \"Report\"" +
        "    }" +
        "  }," +
        "  \"Dependencies\": {" +
        "    \"Act-ChinaDRM-LD\": [" +
        "      \"Act-Report\"" +
        "    ]," +
        "    \"Act-ChinaDRM-HD\": [" +
        "      \"Act-Report\"" +
        "    ]," +
        "    \"Act-Start\": [" +
        "      \"Act-ChinaDRM-SD\"," +
        "      \"Act-ChinaDRM-HD\"," +
        "      \"Act-ChinaDRM-LD\"" +
        "    ]," +
        "    \"Act-Report\": []," +
        "    \"Act-ChinaDRM-SD\": [" +
        "      \"Act-Report\"" +
        "    ]" +
        "  }" +
        "}";

    public void createWorkflow() throws ClientException {
        String chinaDRMWorkflow = WORKFLOW_TEMPLATE.replace("PIPELINE_ID", PIPELINE_ID).replace("INPUT_BUCKET", INPUT_BUCKET).replace("OSS_LOCATION", OSS_LOCATION)
            .replace("INPUT_PATH", INPUT_PATH).replace("OUTPUT_BUCKET", OUTPUT_BUCKET).replace("OUTPUT_PATH", OUTPUT_PATH).replace("ENCRYPTION_TYPE", ENCRYPTION_TYPE);
        System.out.println(chinaDRMWorkflow);
        AddMediaWorkflowRequest addMediaWorkflowRequest = new AddMediaWorkflowRequest();
        addMediaWorkflowRequest.setTopology(chinaDRMWorkflow);
        addMediaWorkflowRequest.setName("ChinaDRM");
        AddMediaWorkflowResponse response = this.client.getAcsResponse(addMediaWorkflowRequest);
        System.out.println(response.getMediaWorkflow().getMediaWorkflowId());
    }   

    public ChinaDRMWorkflow() {
        DefaultProfile profile = DefaultProfile.getProfile(REGION_ID, ACCESS_KEY_ID, ACCESS_KEY_SECRET);
        this.client = new DefaultAcsClient(profile);
    }

    public static void main(String[] args) throws ClientException {
        new ChinaDRMWorkflow().createWorkflow();
    }
}
```

