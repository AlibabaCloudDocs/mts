# FpImportOSSEntity

本文介绍对应序列化Java类FpImportOSSEntity列表格式。

```

package com.aliyun.mts.domain.handler.fpimport.util;


import com.alibaba.fastjson.annotation.JSONField;


public class FpImportOSSEntity {
@JSONField(name = "PrimaryKey")
private String primaryKey;
@JSONField(name = "Location")
private String location;
@JSONField(name = "Bucket")
private String bucket;
@JSONField(name = "Object")
private String object;


public FpImportOSSEntity() {}


public String getPrimaryKey() {
return primaryKey;
}


public void setPrimaryKey(String primaryKey) {
this.primaryKey = primaryKey;
}


public String getLocation() {
return location;
}


public void setLocation(String location) {
this.location = location;
}


public String getBucket() {
return bucket;
}


public void setBucket(String bucket) {
this.bucket = bucket;
}


public String getObject() {
return object;
}


public void setObject(String object) {
this.object = object;
}
}

            
```

