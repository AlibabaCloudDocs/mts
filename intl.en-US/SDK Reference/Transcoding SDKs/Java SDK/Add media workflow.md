# Add media workflow

The user can assemble activities provided by MPS, such as transcode activity and screenshot activity into a topology. The topology is as follows:

Topology type

```
package com.aliyun.mts;
import com.alibaba.fastjson.annotation.JSONField;
import java.util.List;
import java.util.Map;
public class Topology {
    @JSONField(name = "Activities")
    private Map<String, Activity> activities;
    @JSONField(name = "Dependencies")
    private Map<String, List<String>> dependencies;
    public Map<String, List<String>> dependencies() {
        return this.getDependencies();
    }
    public Topology() {
    }
    public Topology(Map<String, Activity> activities, Map<String, List<String>> dependencies) {
        this.setActivities(activities);
        this.setDependencies(dependencies);
    }
    public Map<String, Activity> getActivities() {
        return activities;
    }
    public Map<String, List<String>> getDependencies() {
        return dependencies;
    }
    public void setActivities(Map<String, Activity> activities) {
        this.activities = activities;
    }
    public void setDependencies(Map<String, List<String>> dependencies) {
        this.dependencies = dependencies;
    }
}
```

ActivityType enumeration type

```
package com.aliyun.mts;
/**
 * Created by zhongyizengzy on 18/3/22.
 */
public enum ActivityType {
    Start, Transcode, Snapshot, MediaInfo, Analysis, Cover, Summary, Censor, Report, UploadVerify, GenerateMasterPlayList, AudioGroup, SubtitleGroup, PackageConfig
}
```

Activity type

```
package com.aliyun.mts;
import com.alibaba.fastjson.annotation.JSONField;
import java.util.Map;
public class Activity {
    @JSONField(name = "Type")
    private String type;
    @JSONField(name = "Parameters")
    private Map<String, String> parameters;
    public Activity() {
    }
    public Map<String, String> parameters() {
        return this.getParameters();
    }
    public Activity(String type, Map<String, String> parameters) {
        this.setType(type);
        this.setParameters(parameters);
    }
    public String getType() {
        return type;
    }
    public Map<String, String> getParameters() {
        return parameters;
    }
    public void setType(String type) {
        this.type = type;
    }
    public void setParameters(Map<String, String> parameters) {
        this.parameters = parameters;
    }
}
```

AddMediaWorkflow type

```
package com.aliyun.mts;
import com.alibaba.fastjson.JSONArray;
import com.alibaba.fastjson.JSONObject;
import com.aliyuncs.DefaultAcsClient;
import com.aliyuncs.exceptions.ClientException;
import com.aliyuncs.exceptions.ServerException;
import com.aliyuncs.mts.model.v20140618. AddMediaWorkflowRequest;
import com.aliyuncs.mts.model.v20140618. AddMediaWorkflowResponse;
import com.aliyuncs.profile.DefaultProfile;
import org.apache.commons.lang.exception.ExceptionUtils;
import java.io.UnsupportedEncodingException;
import java.net.URLEncoder;
import java.util.ArrayList;
import java.util.Arrays;
import java.util.HashMap;
import java.util.List;
public class AddMediaWorkflow {
    //Step 1 .set region:cn-hangzhou\cn-shenzhen\cn-shanghai\cn-beijing
    private static final String REGION = "cn-shenzhen";
    private static final String OSS_REGION = "oss-cn-shenzhen";
    private static final String mtsEndpoint = "mts." + REGION + ".aliyuncs.com";
    //Step 2.set accesskey & keySecret
    private static String accessKeyId = "";
    private static String accessKeySecret = "";
    //Step 3.set mps transcoding queue id
    private static String PIPELINE_ID = "38bba54d524448be92d277caaa8da118";
    private static DefaultAcsClient aliyunClient;
    static {
        try {
            DefaultProfile.addEndpoint(REGION, REGION, "Mts", mtsEndpoint);
        } catch (ClientException e) {
            System.out.print(ExceptionUtils.getStackTrace(e));
            System.exit(1);
        }
        aliyunClient = new DefaultAcsClient(DefaultProfile.getProfile(REGION, accessKeyId, accessKeySecret));
    }
    public static void main(String[] args) throws ClientException {
        AddMediaWorkflowRequest request = new AddMediaWorkflowRequest();
        request.setName("Sequential-workflow");
        Topology topology = new Topology();
        HashMap<String, Activity> activities = new HashMap<String, Activity>();
        Activity startNode = new Activity();
        startNode.setType(ActivityType.Start.name());
        HashMap<String, String> startNodeParameters = new HashMap<String, String>();
        JSONObject inputFile = new JSONObject();
        inputFile.put("Bucket", "mtb-sz-in");
        inputFile.put("Location", OSS_REGION);
        inputFile.put("ObjectPrefix", "media/");
        startNodeParameters.put("InputFile", inputFile.toString());
        startNodeParameters.put("PipelineId", PIPELINE_ID);
        startNode.setParameters(startNodeParameters);
        activities.put("startNode", startNode);
        Activity transcode = new Activity();
        transcode.setType(ActivityType.Transcode.name());
        HashMap<String, String> transcodingParameters = new HashMap<String, String>();
        JSONArray outputs = new JSONArray();
        JSONObject output = new JSONObject();
        try {
            output.put("OutputObject", URLEncoder.encode("transcode/{ObjectPrefix}/{FileName}.{ ExtName}", "UTF-8"));
        } catch (UnsupportedEncodingException e) {
            System.exit(1);
        }
        output.put("TemplateId", "S00000001-000070");
        outputs.add(output);
        transcodingParameters.put("Outputs", outputs.toJSONString());
        transcodingParameters.put("OutputBucket", "mtb-sz-out");
        transcodingParameters.put("OutputLocation", OSS_REGION);
        transcode.setParameters(transcodingParameters);
        activities.put("transcodingNode", transcode);
        Activity report = new Activity();
        report.setType(ActivityType.Report.name());
        HashMap<String, String> reportParameters = new HashMap<String, String>();
        report.setParameters(reportParameters);
        activities.put("reportNode", report);
        topology.setActivities(activities);
        HashMap<String, List<String>> dependencies = new HashMap<String, List<String>>();
        dependencies.put("startNode", Arrays.asList("transcodingNode"));
        dependencies.put("transcodingNode", Arrays.asList("reportNode"));
        dependencies.put("reportNode", new ArrayList<String>());
        topology.setDependencies(dependencies);
        request.setTopology(JSONObject.toJSONString(topology));
        try {
            AddMediaWorkflowResponse response = aliyunClient.getAcsResponse(request);
            System.out.println(JSONObject.toJSONString(response));
        } catch (ServerException e) {
            System.out.println("Code:" + e.getErrCode() + " Msg:" + e.getMessage());
        } catch (ClientException e) {
            System.out.println("Code:" + e.getErrCode() + " Msg:" + e.getMessage());
        }
    }
}
```

