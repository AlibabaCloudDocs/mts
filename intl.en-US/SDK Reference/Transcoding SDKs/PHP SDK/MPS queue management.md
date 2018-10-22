# MPS queue management {#concept_upd_dk2_z2b .concept}

The system automatically creates an MPS queue when you open the MPS service. You can also use interfaces to manage MPS queue \(pipeline\). For example, SearchPipeline, QueryPipelineList, UpdatePipeline.

## Search MPS queue {#section_v1m_fk2_z2b .section}

You can use the SearchPipeline interface to search the MPS queue information.

```
$region = '<region>';
    $accessKeyId = '<accessKeyId>';
    $accessKeySecret = '<accessKeySecret>';
    $profile = DefaultProfile::getProfile($region, $accessKeyId, $accessKeySecret);
    $client = new DefaultAcsClient($profile);
    $request = new Mts\SearchPipelineRequest();
    // If an error occurs, it can throw ClientException or ServerException.
    $response = $client->getAcsResponse($request);
    $pipelines = $response->PipelineList->Pipeline;
    foreach ($pipelines as $pipeline) {
        echo 'pipeline id:' . $pipeline->Id . ', name:' . $pipeline->Name . ', state:' . $pipeline->State . "\n";
    }
```

## Query MPS queue {#section_jnb_hk2_z2b .section}

If you have the pipelineId, you can use pipelineId to call QueryPipelineList interface to query MPS queue information.

```
$region = '<region>';
    $accessKeyId = '<accessKeyId>';
    $accessKeySecret = '<accessKeySecret>';
    // The known pipeline ID, separated by comma (,)
    $pipelineIds = '<pipelineIds>';
    $profile = DefaultProfile::getProfile($region, $accessKeyId, $accessKeySecret);
    $client = new DefaultAcsClient($profile);
    $request = new Mts\QueryPipelineListRequest();
    $request->setPipelineIds($pipelineIds);
    // If an error occurs, it can throw ClientException or ServerException.
    $response = $client->getAcsResponse($request);
    $pipelines = $response->PipelineList->Pipeline;
    foreach ($pipelines as $pipeline) {
        echo 'pipeline id:' . $pipeline->Id . ', name:' . $pipeline->Name . ', state:' . $pipeline->State . "\n";
    }
```

## Update MPS queue {#section_ktx_jk2_z2b .section}

Use the UpdatePipeline interface to update MPS queue information, including MPS queue name and status. The status includes Active and Paused.

```
$region = '<region>';
    $accessKeyId = '<accessKeyId>';
    $accessKeySecret = '<accessKeySecret>';
    $profile = DefaultProfile::getProfile($region, $accessKeyId, $accessKeySecret);
    $client = new DefaultAcsClient($profile);
    $request = new Mts\SearchPipelineRequest();
    // If an error occurs, it can throw ClientException or ServerException.
    $response = $client->getAcsResponse($request);
    $pipelines = $response->PipelineList->Pipeline;
    $pipeline = $pipelines[0];
    $request = new Mts\UpdatePipelineRequest();
    $request->setPipelineId($pipeline->Id);
    $request->setName($pipeline->Name);
    $request->setState($pipeline->State == 'Paused' ? 'Active' : 'Paused');
    $response = $client->getAcsResponse($request);
    $pipeline = $response->Pipeline;
    echo 'pipeline id:' . $pipeline->Id . ', name:' . $pipeline->Name . ', state:' . $pipeline->State . "\n";
```

