# HLS数据加密 {#concept_qjy_vgw_y2b .concept}

## 使用场景 {#section_pn1_q2x_y2b .section}

-   HLS标准数据加密适用于“对视频进行简单的保护”的，可以简单的防止非法下载和非法传播。

-   如果对安全有强需求，请开启工作流中的数据加密。详情参见 [数据加密](https://help.aliyun.com/document_detail/50114.html)。


## 使用限制 {#section_g2p_52x_y2b .section}

HLS标准数据加密需要使用SubmitJobs接口，工作流中不可使用。

## 示例代码依赖 {#section_avt_v2x_y2b .section}

-   MPS SDK详情参见 [安装](https://help.aliyun.com/document_detail/55736.html)。
-   其他依赖。

    ```
    <dependency>
        <groupId>com.alibaba</groupId>
        <artifactId>fastjson</artifactId>
        <version>1.2.25</version
    </dependency>
    <dependency>
        <groupId>commons-codec</groupId>
        <artifactId>commons-codec</artifactId>
        <version>1.9</version>
    </dependency>
    ```


## 示例代码 {#section_lxy_xfx_y2b .section}

```
package com.aliyun
import com.alibaba.fastjson.JSONArray;
import com.alibaba.fastjson.JSONObject;
import com.aliyuncs.DefaultAcsClient;
import com.aliyuncs.exceptions.ClientException;
import com.aliyuncs.mts.model.v20140618.QueryJobListRequest;
import com.aliyuncs.mts.model.v20140618.QueryJobListResponse;
import com.aliyuncs.mts.model.v20140618.SubmitJobsRequest;
import com.aliyuncs.mts.model.v20140618.SubmitJobsResponse;
import com.aliyuncs.profile.DefaultProfile;
import org.apache.commons.codec.binary.Base64;
public class DataEncryptionDemo {
    private DefaultAcsClient client = null;
    private final String REGION = "cn-shanghai"; //按需配置
    private final String MTS_ENDPOINT = "mts.cn-shanghai.aliyuncs.com"; //按需配置
    private final String ID="idid"; //按需配置
    private final String KEY ="keykey"; //按需配置
    private final String LOCATION = "oss-cn-shanghai"; //按需配置
    private final String INPUT_BUCKET = "input-bucket"; //按需配置
    private final String OUTPUT_BUCKET = "output-bucket"; //按需配置
    private final String PIPELINE_ID = "pipelineId"; //按需配置
    public DataEncryptionDemo() throws ClientException {
        DefaultProfile.addEndpoint(REGION, REGION, "Mts", MTS_ENDPOINT);
        this.client = new DefaultAcsClient(DefaultProfile.getProfile(REGION, ID, KEY));
    }
    private JSONObject getInputFile() {
        JSONObject inputFile = new JSONObject();
        inputFile.put("Location", LOCATION);
        inputFile.put("Bucket", INPUT_BUCKET);
        inputFile.put("Object", "uploadvideo/test.flv");
        return inputFile;
    }
    private JSONArray getOutputs() {
        JSONArray outputs = new JSONArray();
        outputs.add(getOutput());
        return outputs;
    }
    private JSONObject getOutput() {
        JSONObject output = new JSONObject();
        output.put("OutputObject", "BaseTest/hls-encryption.m3u8");
        output.put("TemplateId", "S00000001-100020");
        output.put("Encryption", getEncryptionConfigs());
        return output;
    }
    private JSONObject getEncryptionConfigs() {
        JSONObject encryption = new JSONObject();
        encryption.put("Type", "hls-aes-128");
        encryption.put("Key", Base64.encodeBase64URLSafeString("encryptionkey123".getBytes()));
        encryption.put("KeyUri", Base64.encodeBase64URLSafeString("http://demo.aliyuncs.com/document/hls128.key".getBytes()));
        encryption.put("KeyType", "Base64");
        return encryption;
    }
    private String submitJobs() throws ClientException {
        JSONObject inputFile = getInputFile();
        SubmitJobsRequest request = new SubmitJobsRequest();
        request.setInput(inputFile.toJSONString());
        request.setOutputLocation(LOCATION);
        request.setOutputBucket(OUTPUT_BUCKET);
        request.setOutputs(getOutputs().toJSONString());
        request.setPipelineId(PIPELINE_ID);
        SubmitJobsResponse reponse = this.client.getAcsResponse(request);
        System.out.println(JSONObject.toJSONString(reponse.getJobResultList()));
        return reponse.getJobResultList().get(0).getJob().getJobId();
    }
    public static void main(String[] args) throws ClientException {
        DataEncryptionDemo demo = new DataEncryptionDemo();
        String jobId= demo.submitJobs();
    }
 }
```

