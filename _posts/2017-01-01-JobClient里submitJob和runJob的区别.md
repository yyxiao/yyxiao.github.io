---
bg: "tools.jpg"
layout: post
title:  "JobClient 里 submitJob(JobConf) 和 runJob(JobConf) 的区别"
crawlertitle: "About Hadoop"
summary: "submitJob与runJob"
date:   2017-01-01 08:10:47
categories: posts
tags: ['大数据','Hadoop']
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

### 应用

JobClient指的是org.apache.hadoop.mapred.JobClient这个类。里面有不少的方法，我这里列举一些我用到的和一些需要注意的方法。

1、JobClient的实例化。这里有2中方法，一种是new JobClient(new JobConf);另外一种是实例化IP地址和端口。

2、通过JobClient获取Job列表。

JobClient.jobsToComplete()返回没有完成和没有失败的Job。换句话说就是在运行的Job。

JobClient.getAllJobs()返回所有的Job，不管是失败还是成功的。

3、获取JobID

JobID是一个Job的唯一标识，如果要获取指定的JobID，那么需要有根据，例如UserName。我这里是通过User来获取JobID。方法是遍历Job，然后找到名称相匹配的Job，然后取出ID。

4、通过线程阻塞的模式来等待Job执行完成。

JobClient.getJob(JobID).waitForCompletion();
