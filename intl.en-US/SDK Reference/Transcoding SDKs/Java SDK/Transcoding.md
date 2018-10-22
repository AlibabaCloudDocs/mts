# Transcoding {#concept_x5h_vfw_y2b .concept}

1.  Create AcsClient instance.

    ```
    DefaultProfile profile = DefaultProfile.getProfile(
                 mpsRegionId,      // region ID
                 accessKeyId,      // AccessKey ID of RAM account
                 accessKeySecret); // Access Key Secret of RAM account
    IAcsClient client = new DefaultAcsClient(profile);
    ```

2.  Create request, and set parameters.

    ```
    SubmitJobsRequest request = new SubmitJobsRequest();
    ```

3.  Transcoding parameters.
    -   Input

        ```
        JSONObject input = new JSONObject();
        input.put("Location", ossLocation);
        input.put("Bucket", ossBucket);
        input.put("Object", URLEncoder.encode(ossInputObject, "utf-8"));
        request.setInput(input.toJSONString());
        ```

    -   Output

        ```
        String outputOSSObject = URLEncoder.encode(ossOutputObject, "utf-8");
        JSONObject output = new JSONObject();
        output.put("OutputObject", outputOSSObject);
        ```

        -   Container

            ```
            JSONObject container = new JSONObject();
            container.put("Format", "mp4");
            output.put("Container", container.toJSONString());
            ```

        -   Video

            ```
            JSONObject video = new JSONObject();
            video.put("Codec", "H. 264");
            video.put("Bitrate", "1500");
            video.put("Width", "1280");
            video.put("Fps", "25");
            output.put("Video", video.toJSONString());
            ```

        -   Audio

            ```
            JSONObject audio = new JSONObject();
            audio.put("Codec", "AAC");
            audio.put("Bitrate", "128");
            audio.put("Channels", "2");
            audio.put("Samplerate", "44100");
            output.put("Audio", audio.toJSONString());
            ```

        -   TemplateId

            ```
            output.put("TemplateId", templateId);
            ```

    -   PipelineId

        ```
        request.setPipelineId(pipelineId);
        ```

4.  Initiate API request and display returned value.

    ```
    SubmitJobsResponse response;
    response = client.getAcsResponse(request);
    System.out.println("RequestId is:"+response.getRequestId());
    if (response.getJobResultList().get(0).getSuccess()) {
     System.out.println("JobId is:" + response.getJobResultList().get(0).getJob().getJobId());
    } else {
     System.out.println("SubmitJobs Failed code:" + response.getJobResultList().get(0).getCode() +
                        " message:" + response.getJobResultList().get(0).getMessage());
    }
    ```


Full codes

```
import java.io.UnsupportedEncodingException;
import java.net.URLEncoder;
import com.alibaba.fastjson.JSONArray;
import com.alibaba.fastjson.JSONObject;
import com.aliyuncs.profile.DefaultProfile;
import com.aliyuncs.DefaultAcsClient;
import com.aliyuncs.IAcsClient;
import com.aliyuncs.exceptions.ClientException;
import com.aliyuncs.exceptions.ServerException;
import com.aliyuncs.mts.model.v20140618.*;
public class SimpleTranscode {
    private static String accessKeyId = "xxx";
    private static String accessKeySecret = "xxx";
    private static String mpsRegionId = "cn-hangzhou";
    private static String pipelineId = "xxx";
    private static String templateId = "S00000001-200010";
    private static String ossLocation = "oss-cn-hangzhou";
    private static String ossBucket = "xxx";
    private static String ossInputObject = "input.mp4";
    private static String ossOutputObject = "output.mp4";
    public static void main(String[] args) {
        // Create DefaultAcsClient instance and complete initialization
        DefaultProfile profile = DefaultProfile.getProfile(
                mpsRegionId,      //  region D
                accessKeyId,      //AccessKey ID of RAM account
                accessKeySecret); // Access Key Secret of RAM account
        IAcsClient client = new DefaultAcsClient(profile);
        // Create API request and set parameters
        SubmitJobsRequest request = new SubmitJobsRequest();
        // Input
        JSONObject input = new JSONObject();
        input.put("Location", ossLocation);
        input.put("Bucket", ossBucket);
        try {
            input.put("Object", URLEncoder.encode(ossInputObject, "utf-8"));
        } catch (UnsupportedEncodingException e) {
            throw new RuntimeException("input URL encode failed");
        }
        request.setInput(input.toJSONString());
        // Output
        String outputOSSObject;
        try {
            outputOSSObject = URLEncoder.encode(ossOutputObject, "utf-8");
        } catch (UnsupportedEncodingException e) {
            throw new RuntimeException("output URL encode failed");
        }
        JSONObject output = new JSONObject();
        output.put("OutputObject", outputOSSObject);
        // Ouput->Container
        JSONObject container = new JSONObject();
        container.put("Format", "mp4");
        output.put("Container", container.toJSONString());
        // Ouput->Video
        JSONObject video = new JSONObject();
        video.put("Codec", "H. 264");
        video.put("Bitrate", "1500");
        video.put("Width", "1280");
        video.put("Fps", "25");
        output.put("Video", video.toJSONString());
        // Ouput->Audio
        JSONObject audio = new JSONObject();
        audio.put("Codec", "AAC");
        audio.put("Bitrate", "128");
        audio.put("Channels", "2");
        audio.put("Samplerate", "44100");
        output.put("Audio", audio.toJSONString());
        // Ouput->TemplateId
        output.put("TemplateId", templateId);
        JSONArray outputs = new JSONArray();
        outputs.add(output);
        request.setOutputs(outputs.toJSONString());
        request.setOutputBucket(ossBucket);
        request.setOutputLocation(ossLocation);
        // PipelineId
        request.setPipelineId(pipelineId);
        // Initiate request and handle response or exceptions
        SubmitJobsResponse response;
        try {
            response = client.getAcsResponse(request);
            System.out.println("RequestId is:"+response.getRequestId());
            if (response.getJobResultList().get(0).getSuccess()) {
                System.out.println("JobId is:" + response.getJobResultList().get(0).getJob().getJobId());
            } else {
                System.out.println("SubmitJobs Failed code:" + response.getJobResultList().get(0).getCode() +
                                   " message:" + response.getJobResultList().get(0).getMessage());
            }
        } catch (ServerException e) {
            e.printStackTrace();
        } catch (ClientException e) {
            e.printStackTrace();
        }
    }
}
```

