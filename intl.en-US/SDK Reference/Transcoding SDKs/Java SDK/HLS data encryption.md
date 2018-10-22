# HLS data encryption {#concept_qjy_vgw_y2b .concept}

## Scenario {#section_pn1_q2x_y2b .section}

-   HLS standard sata encryption applies to "protect video protection", it can prevent illegal downloads and illegal dissemination.

-   If you have high security requirements, enable Data Encryption function in the workflow. For more information, see [data encryption](https://help.aliyun.com/document_detail/50114.html).


## Limits {#section_g2p_52x_y2b .section}

HLS标准数据加密需要使用SubmitJobs接口，工作流中不可使用。

## Code example {#section_avt_v2x_y2b .section}

-   For more information about MPS SDK, [Installation](https://help.aliyun.com/document_detail/55736.html).
-   Other code examples

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


## Code example {#section_lxy_xfx_y2b .section}

```
package com.aliyun
import com.alibaba.fastjson.JSONArray;
import com.alibaba.fastjson.JSONObject;
import com.aliyuncs.DefaultAcsClient;
import com.aliyuncs.exceptions.ClientException;
import com.aliyuncs.mts.model.v20140618. QueryJobListRequest;
import com.aliyuncs.mts.model.v20140618. QueryJobListResponse;
import com.aliyuncs.mts.model.v20140618. SubmitJobsRequest;
import com.aliyuncs.mts.model.v20140618. SubmitJobsResponse;
import com.aliyuncs.profile.DefaultProfile;
import org.apache.commons.codec.binary.Base64;
public class DataEncryptionDemo {
    private DefaultAcsClient client = null;
    private final String REGION = "cn-shanghai"; //set as needed
    private final String MTS_ENDPOINT = "mts.cn-shanghai.aliyuncs.com"; //set as needed
    private final String ID="idid"; //set as needed
    private final String KEY ="keykey"; //set as needed
    private final String LOCATION = "oss-cn-shanghai"; //set as needed
    private final String INPUT_BUCKET = "input-bucket"; //set as needed
    private final String OUTPUT_BUCKET = "output-bucket"; //set as needed
    private final String PIPELINE_ID = "pipelineId"; //set as needed
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

