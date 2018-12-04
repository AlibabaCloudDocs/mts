# 创建HLS标准加密工作流 {#concept_lwg_3fx_y2b .concept}

## 简介 {#section_vjf_mfx_y2b .section}

示例调用API进行创建HLS标准加密工作流。创建工作流，参见 [新增媒体工作流](../../../../intl.zh-CN/API参考/媒体工作流接口/新增媒体工作流.md#)。

## 示例代码依赖 {#section_q2v_mfx_y2b .section}

-   MPS SDK，参见 [安装](intl.zh-CN/SDK参考/媒体转码SDK/Java SDK/安装.md#)。
-   其他依赖。

    ```
    <dependency>
        <groupId>com.alibaba</groupId>
        <artifactId>fastjson</artifactId>
        <version>1.2.25</version
    </dependency>
    ```


## 示例代码 {#section_yrn_bgx_y2b .section}

```
package com.aliyun.smallcode;
import com.alibaba.fastjson.JSONArray;
import com.alibaba.fastjson.JSONObject;
import com.aliyuncs.DefaultAcsClient;
import com.aliyuncs.exceptions.ClientException;
import com.aliyuncs.mts.model.v20140618.AddMediaWorkflowRequest;
import com.aliyuncs.mts.model.v20140618.AddMediaWorkflowResponse;
import com.aliyuncs.profile.DefaultProfile;
public class MediaHls {
    final String REGION_ID = "<region>";
    final String ACCESS_KEY_ID = "<accessKeyId>";
    final String ACCESS_KEY_SECRET = "<accessKeySecret>";
    final String PIPELINE_ID = "<PipelineId>";
    final String TEMPLATE_ID = "S00000001-100020"; //转码模版ID，m3u8模版，按需配置
    final String OSS_LOCATION = "<OssLocation>";
    final String INPUT_BUCKET = "<InputBucket>"; //输入bucket
    final String INPUT_PATH = "<InputPath>"; //如 "HLS-Encryption"
    final String OUTPUT_BUCKET = "<OutputBucket>"; //输出bucket
    final String ENCRYPTION_TYPE = "hls-aes-128";
    final String HLS_KEY_URI = "<解密密钥的URI>"; //如http://decrypt.testdomain.com
    final String ACT_START = "Act-Start";
    final String ACT_ENCRYPTION = "Act-HLS-Encryption";
    final String ACT_REPORT = "Act-Report";
    private DefaultAcsClient client;
    public MediaHls() {
        DefaultProfile profile = DefaultProfile.getProfile(REGION_ID, ACCESS_KEY_ID, ACCESS_KEY_SECRET);
        this.client = new DefaultAcsClient(profile);
    }
    public AddMediaWorkflowResponse addMediaWorkflow() throws ClientException {
        AddMediaWorkflowRequest request = new AddMediaWorkflowRequest();
        request.setTopology(createWorkflow().toJSONString());
        request.setName("HLS加密工作流");
        return this.client.getAcsResponse(request);
    }
    private JSONObject createWorkflow() {
        JSONObject workflow = new JSONObject();
        JSONObject activities = new JSONObject();
        activities.put(ACT_START, createStartActivity());
        activities.put(ACT_ENCRYPTION, createTrancodeActivity());
        activities.put(ACT_REPORT, createReportActivity());
        workflow.put("Activities", activities);
        workflow.put("Dependencies", createDependencies());
        return workflow;
    }
    private JSONObject createStartActivity() {
        JSONObject startActivity = new JSONObject();
        startActivity.put("Name", ACT_START);
        startActivity.put("Type", "Start");
        startActivity.put("Parameters", buildStartParameters());
        return startActivity;
    }
    private JSONObject buildStartParameters() {
        JSONObject parameters = new JSONObject();
        parameters.put("PipelineId", PIPELINE_ID);
        parameters.put("InputFile", buildInputFile());
        return parameters;
    }
    private JSONObject buildInputFile() {
        JSONObject inputFile = new JSONObject();
        inputFile.put("Bucket", INPUT_BUCKET);
        inputFile.put("Location", OSS_LOCATION);
        inputFile.put("ObjectPrefix", INPUT_PATH);
        return inputFile;
    }
    private JSONObject createTrancodeActivity() {
        JSONObject transcodeActivity = new JSONObject();
        transcodeActivity.put("Name", ACT_ENCRYPTION);
        transcodeActivity.put("Type", "Transcode");
        transcodeActivity.put("Parameters", buildTranscodeParameters());
        return transcodeActivity;
    }
    private JSONObject buildTranscodeParameters() {
        JSONObject transcodeParamters = new JSONObject();
        transcodeParamters.put("OutputBucket", OUTPUT_BUCKET);
        transcodeParamters.put("OutputLocation", OSS_LOCATION);
        transcodeParamters.put("Outputs", buildOutputsConfig());
        return transcodeParamters;
    }
    private JSONArray buildOutputsConfig() {
        JSONArray outputs = new JSONArray();
        JSONObject output = new JSONObject();
        output.put("ObjectRegex", ACT_ENCRYPTION + "/{RunId}/{FileName}");
        output.put("TemplateId", TEMPLATE_ID);
        output.put("Encryption", buildEncryption());
        outputs.add(output);
        return outputs;
    }
    private JSONObject buildEncryption() {
        JSONObject encryption = new JSONObject();
        encryption.put("Type", ENCRYPTION_TYPE);
        encryption.put("KeyUri", HLS_KEY_URI);
        return encryption;
    }
    private JSONObject createReportActivity() {
        JSONObject reportActivity = new JSONObject();
        reportActivity.put("Name", ACT_REPORT);
        reportActivity.put("Parameters", new JSONObject());
        reportActivity.put("Type", "Report");
        return  reportActivity;
    }
    private JSONObject createDependencies() {
        JSONObject dependencies = new JSONObject();
        JSONArray subActivityOfStart = new JSONArray();
        subActivityOfStart.add(ACT_ENCRYPTION);
        dependencies.put(ACT_START, subActivityOfStart);
        JSONArray subActivityOfTranscode = new JSONArray();
        subActivityOfTranscode.add(ACT_REPORT);
        dependencies.put(ACT_ENCRYPTION, subActivityOfTranscode);
        dependencies.put(ACT_REPORT, new JSONArray());
        return dependencies;
    }
    public static void main(String[] args) throws ClientException {
        MediaHls mediaHls = new MediaHls();
        AddMediaWorkflowResponse response = mediaHls.addMediaWorkflow();
        System.out.println(JSONObject.toJSONString(response));
    }
}
```

