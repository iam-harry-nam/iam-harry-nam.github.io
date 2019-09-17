---
title: "ConsistencyException: Directory 'path_name/20190916' present in the metadata but not s3"
date: 2019-09-18 01:00:00
category: ["AWS", "Trouble Shooting"]
tag: ["ConsistencyException",
        "Spark",
        "Metadata",
        "S3",
        "EMRFS",
        "Hadoop"]
---

_Trouble Shooting_

I got `ConsistencyException` this message during spark job,

```
ERROR yarn.ApplicationMaster: User class threw exception: com.amazon.ws.emr.hadoop.fs.consistency.exception.ConsistencyException: Directory 'path_name/datetime=20190916' present in the metadata but not s3
```

After searching google, some people resolved with emrfs command  
```emrfs delete s3://path```

But I can't do emrfs cli since EC2 key pair issue.

And I found another solution that trying to put `ignore s3 consistent` option to `spark-submit`.

```
spark.hadoop.fs.s3.consistent=false
spark.hadoop.fs.s3.consistent.throwExceptionOnInconsistency=false
```

This way is not a complete solution because this code is defence code of consistent check.  
But if this spark job is a single job, and this spark job is not running at the same time, it is okay to turn off emrfs.

