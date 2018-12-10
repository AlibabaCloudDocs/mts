# 如何创建Java版Widevine工作流 {#concept_drn_kqc_bgb .concept}

本文介绍如何创建Java版Widevine工作流。

## 使用限制 {#section_ljh_zqc_bgb .section}

-   使用Widevine前，请联系您的商务经理，开通服务并获取产品报价。
-   播放视频需集成Web播放器。

## 安装 {#section_azw_brc_bgb .section}

-   MPS SDK安装，参见 [安装](../../../../cn.zh-CN/SDK参考/媒体转码SDK/Java SDK/安装.md#)。
-   创建三个容器格式为mpd的三路不同分辨率的转码模版，参见 [创建模版](../../../../cn.zh-CN/API参考/自定义转码模板接口/新增自定义转码模版.md#)。

## 示例代码 {#section_qk5_hrc_bgb .section}

```
package com.aliyun.smallcode.workflow;

import com.aliyuncs.DefaultAcsClient;
import com.aliyuncs.exceptions.ClientException;
import com.aliyuncs.mts.model.v20140618.AddMediaWorkflowRequest;
import com.aliyuncs.mts.model.v20140618.AddMediaWorkflowResponse;
import com.aliyuncs.profile.DefaultProfile;

public class WidevineWorkflow {
    final String REGION_ID = "cn-hangzhou";
    final String ACCESS_KEY_ID = "id";
    final String ACCESS_KEY_SECRET = "key";
    final String ENCRYPTION_TYPE = "Widevine";
    final String PIPELINE_ID = "<PipelineId>";
    final String OSS_LOCATION = "oss-" + REGION_ID;
    final String INPUT_BUCKET = "<InputBucket>"; //输入bucket
    final String INPUT_PATH = "<InputPath>"; //如 "HLS-Encryption"
    final String OUTPUT_BUCKET = "<OutputBucket>"; //输出bucket
    final String OUTPUT_PATH = "<OutputPath>"; //输出bucket
    final String MPD_360P_TEMPLATE = "templateid";
    final String MPD_480P_TEMPLATE = "templateid";
    final String MPD_720P_TEMPLATE = "templateid";
    
    private DefaultAcsClient client;
  
    public  String WORKFLOW_TEMPLATE = "{" +
            "  \"Activities\": {" +
            "    \"video-group\": {" +
            "      \"Name\": \"video-group\"," +
            "      \"Parameters\": {" +
            "        \"AdaptationSet\": \"{\\\"Group\\\":\\\"VideoGroup\\\"}\"" +
            "      }," +
            "      \"Type\": \"VideoGroup\"" +
            "    }," +
            "    \"act-start\": {" +
            "      \"Name\": \"act-start\"," +
            "      \"Parameters\": {" +
            "        \"PipelineId\": \"PIPELINE_ID\"," +
            "        \"InputFile\": \"{\\\"Bucket\\\":\\\"INPUT_BUCKET\\\",\\\"Location\\\":\\\"OSS_LOCATION\\\",\\\"ObjectPrefix\\\":\\\"INPUT_PATH/\\\"}\"" +
            "      }," +
            "      \"Type\": \"Start\"" +
            "    }," +
            "    \"audio-cn-group\": {" +
            "      \"Name\": \"audio-cn-group\"," +
            "      \"Parameters\": {" +
            "        \"AdaptationSet\": \"{\\\"Lang\\\":\\\"chinese\\\", \\\"Group\\\":\\\"AudioGroupChinese\\\"}\"" +
            "      }," +
            "      \"Type\": \"AudioGroup\"" +
            "    }," +
            "    \"audioCNTransNode\": {" +
            "      \"Name\": \"audioCNTransNode\"," +
            "      \"Parameters\": {" +
            "        \"Outputs\": \"[{\\\"TemplateId\\\":\\\"MPD_360P_TEMPLATE\\\",\\\"AudioStreamMap\\\":\\\"0:a:0\\\",\\\"Video\\\":{\\\"Remove\\\":\\\"true\\\"},\\\"Encryption\\\":{\\\"Type\\\":\\\"ENCRYPTION_TYPE\\\"}}]\"," +
            "        \"Representation\": \"{\\\"Id\\\":\\\"chinese128k\\\", \\\"URI\\\":\\\"audiocn/cn-abc.mpd\\\"}\"" +
            "      }," +
            "      \"Type\": \"Transcode\"" +
            "    }," +
            "    \"act-package\": {" +
            "      \"Name\": \"act-package\"," +
            "      \"Parameters\": {" +
            "        \"Output\": \"{\\\"Bucket\\\": \\\"OUTPUT_BUCKET\\\",\\\"Location\\\": \\\"OSS_LOCATION\\\",\\\"MasterPlayListName\\\": \\\"INPUT_PATH/{MediaId}/{RunId}/master.mpd\\\"}\"," +
            "        \"Protocol\": \"dash\"" +
            "      }," +
            "      \"Type\": \"PackageConfig\"" +
            "    }," +
            "    \"videoTransLD\": {" +
            "      \"Name\": \"videoTransLD\"," +
            "      \"Parameters\": {" +
            "        \"Outputs\": \"[{\\\"TemplateId\\\":\\\"MPD_360P_TEMPLATE\\\",\\\"Audio\\\":{\\\"Remove\\\":\\\"true\\\"},\\\"Encryption\\\":{\\\"Type\\\":\\\"ENCRYPTION_TYPE\\\"}}]\"," +
            "        \"Representation\": \"{\\\"Id\\\":\\\"360p\\\", \\\"URI\\\":\\\"videoLD/xx.mpd\\\"}\"" +
            "      }," +
            "      \"Type\": \"Transcode\"" +
            "    }," +
            "    \"act-report\": {" +
            "      \"Name\": \"act-report\"," +
            "      \"Parameters\": {" +
            "        \"PublishType\": \"Auto\"" +
            "      }," +
            "      \"Type\": \"Report\"" +
            "    }," +
            "    \"generateMasterPlayListAct\": {" +
            "      \"Name\": \"generateMasterPlayListAct\"," +
            "      \"Parameters\": {}," +
            "      \"Type\": \"GenerateMasterPlayList\"" +
            "    }," +
            "    \"videoTransSD\": {" +
            "      \"Name\": \"videoTransSD\"," +
            "      \"Parameters\": {" +
            "        \"Outputs\": \"[{\\\"TemplateId\\\":\\\"MPD_480P_TEMPLATE\\\",\\\"Audio\\\":{\\\"Remove\\\":\\\"true\\\"}, \\\"Encryption\\\":{\\\"Type\\\":\\\"ENCRYPTION_TYPE\\\"}}]\"," +
            "        \"Representation\": \"{\\\"Id\\\":\\\"480p\\\", \\\"URI\\\":\\\"videoSD/xx.mpd\\\"}\"" +
            "      }," +
            "      \"Type\": \"Transcode\"" +
            "    }," +
            "    \"videoTransHD\": {" +
            "      \"Name\": \"videoTransHD\"," +
            "      \"Parameters\": {" +
            "        \"Outputs\": \"[{\\\"TemplateId\\\":\\\"MPD_720P_TEMPLATE\\\",\\\"Audio\\\":{\\\"Remove\\\":\\\"true\\\"},\\\"Encryption\\\":{\\\"Type\\\":\\\"ENCRYPTION_TYPE\\\"}}]\"," +
            "        \"Representation\": \"{\\\"Id\\\":\\\"720p\\\", \\\"URI\\\":\\\"videoHD/xx.mpd\\\"}\"" +
            "      }," +
            "      \"Type\": \"Transcode\"" +
            "    }" +
            "   }," +
            "  \"Dependencies\": {" +
            "    \"video-group\": [\"videoTransLD\", \"videoTransSD\", \"videoTransHD\"]," +
            "    \"act-start\": [\"act-package\"]," +
            "    \"audio-cn-group\": [\"audioCNTransNode\"]," +
            "    \"audioCNTransNode\": [\"generateMasterPlayListAct\"]," +
            "    \"act-package\": [\"audio-cn-group\", \"video-group\"]," +
            "    \"videoTransLD\": [\"generateMasterPlayListAct\"]," +
            "    \"act-report\": []," +
            "    \"generateMasterPlayListAct\": [\"act-report\"]," +
            "    \"videoTransSD\": [\"generateMasterPlayListAct\"]," +
            "    \"videoTransHD\": [\"generateMasterPlayListAct\"]" +
            "  }" +
            "}";


    public WidevineWorkflow() {
        DefaultProfile profile = DefaultProfile.getProfile(REGION_ID, ACCESS_KEY_ID, ACCESS_KEY_SECRET);
        this.client = new DefaultAcsClient(profile);
    }

    public  void createWorkflow() throws ClientException {

        String widevineWorkflow = WORKFLOW_TEMPLATE.replace("PIPELINE_ID", PIPELINE_ID).replace("INPUT_BUCKET", INPUT_BUCKET).replace("OSS_LOCATION", OSS_LOCATION)
                .replace("INPUT_PATH", INPUT_PATH).replace("OUTPUT_BUCKET", OUTPUT_BUCKET).replace("OUTPUT_PATH", OUTPUT_PATH).replace("ENCRYPTION_TYPE", ENCRYPTION_TYPE)
                .replace("MPD_360P_TEMPLATE", MPD_360P_TEMPLATE).replace("MPD_480P_TEMPLATE", MPD_480P_TEMPLATE).replace("MPD_720P_TEMPLATE", MPD_720P_TEMPLATE);
        System.out.println(widevineWorkflow);
        AddMediaWorkflowRequest addMediaWorkflowRequest = new AddMediaWorkflowRequest();
        addMediaWorkflowRequest.setTopology(widevineWorkflow);
        addMediaWorkflowRequest.setName("WidevineWF");
        AddMediaWorkflowResponse response = this.client.getAcsResponse(addMediaWorkflowRequest);
        System.out.println(response.getMediaWorkflow().getMediaWorkflowId());
    }

    public static void main(String[] args) throws ClientException {
        new WidevineWorkflow().createWorkflow();
    }
}
```

