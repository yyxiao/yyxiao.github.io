---
bg: "tools.jpg"
layout: post
title:  "JobClient 里 submitJob(JobConf) 和 runJob(JobConf) 的区别"
crawlertitle: "About Hadoop"
summary: "submitJob与runJob"
date:   2017-01-01 08:10:47
categories: posts
tags: ['Hadoop']
author: Xander
---

Hadoop提交 Job到JobTracker的时候，需要通过JobClient.runJob(JobConf) 或者 JobClient.submitJob(JobConf) 这两个静态方法来提交。但是这两个方法，前者和后者是有区别的。

查看API中的文档解释：

### runJob

~~~
//Utility that submits a job, then polls for progress until the job is complete.
//(runJob是同步的，提交任务后要等待处理直到完成以后)
public static RunningJob runJob(JobConf job) throws IOException {
    JobClient jc = new JobClient(job);
    RunningJob rj = jc.submitJob(job);

    try {
        if(!jc.monitorAndPrintJob(job, rj)) {
            LOG.info("Job Failed: " + rj.getFailureInfo());
            throw new IOException("Job failed!");
        }
    } catch (InterruptedException var4) {
        Thread.currentThread().interrupt();
    }

    return rj;
}
~~~

### submitJob

~~~
//Submit a job to the MR system. This returns a handle to the RunningJob which can be used to track the running-job.
//(submitJob是异步的，会返回一个处理中的RuningJob的handle，然后等有资源的时候，才会真正的去执行提交的任务。)
public RunningJob submitJob(JobConf job) throws FileNotFoundException, IOException {
    try {
        return this.submitJobInternal(job);
    } catch (InterruptedException var3) {
        throw new IOException("interrupted", var3);
    } catch (ClassNotFoundException var4) {
        throw new IOException("class not found", var4);
    }
}
~~~
