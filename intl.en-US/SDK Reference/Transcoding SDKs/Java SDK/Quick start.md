# Quick start {#concept_q4q_hfw_y2b .concept}

This article describes the Java SDK quick start process.

1.  Create AcsClient instance.

    ```
    DefaultProfile profile = DefaultProfile.getProfile(
                 mpsRegionId,      // region ID
                 accessKeyId,      //AccessKey ID of RAM account
                 accessKeySecret); //Access Key Secret of RAM account
    IAcsClient client = new DefaultAcsClient(profile);
    ```

2.  Create request, and set parameters.

    ```
    SubmitJobsRequest request = new SubmitJobsRequest();
    ```

3.  Initiate API request, and display the return value.

    ```
    response = client.getAcsResponse(request);
    System.out.println("PipelineName is:" + response.getPipelineList().get(0).getName());
    System.out.println("PipelineId is:" + response.getPipelineList().get(0).getId());
    ```


Full code

```
import com.aliyuncs.profile.DefaultProfile;
import com.aliyuncs.DefaultAcsClient;
import com.aliyuncs.IAcsClient;
import com.aliyuncs.exceptions.ClientException;
import com.aliyuncs.exceptions.ServerException;
import com.aliyuncs.mts.model.v20140618.*;
public class Quick {
    private static String accessKeyId = "xxx";
    private static String accessKeySecret = "xxx";
    private static String[] mpsRegionIds = new String[] {
            "cn-hangzhou", "cn-beijing","cn-shenzhen", "cn-shanghai",
            "cn-hongkong", "us-west-1", "ap-southeast-1", "ap-northeast-1",
            "eu-central-1", "ap-south-1"
    };
    public static void main(String[] args) {
        for (String mpsRegionId : mpsRegionIds) {
            System.out.println("region id is:" + mpsRegionId);
            // Create DefaultAcsClient instance and finish initialization
            DefaultProfile profile = DefaultProfile.getProfile(
                    mpsRegionId,      // region  ID
                    accessKeyId,      // AccessKey ID of RAM account
                    accessKeySecret); // Access Key Secret of RAM account
            IAcsClient client = new DefaultAcsClient(profile);
            // Create API request and set parameters
            SearchPipelineRequest request = new SearchPipelineRequest();
            //initiate request and handle response or exceptions
            SearchPipelineResponse response;
            try {
                response = client.getAcsResponse(request);
                System.out.println("PipelineName is:" + response.getPipelineList().get(0).getName());
                System.out.println("PipelineId is:" + response.getPipelineList().get(0).getId());
            } catch (ServerException e) {
                e.printStackTrace();
            } catch (ClientException e) {
                e.printStackTrace();
            }
        }
    }
}
```

