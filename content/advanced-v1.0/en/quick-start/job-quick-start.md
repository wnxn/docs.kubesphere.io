---
title: "Create a Job to compute π to 2000 places"
---

## Objective

This tutorial describes the basic features of a Job by creating a parallel task to perform a simple calculation and outputting PI to 2000 decimal as an example.

## Prerequisites

- You need to create a workspace and project, see the [Admin Quick Start](../admin-quick-start) if not yet.
- You need to sign in with `project-regular` and enter into the corresponding project.

## Estimated Time

About 10 minutes.

## Example

### Create a Job

Enter into the project, navigate to **Wordloads → Jobs**, then click **Create Job**.

![Create a Job](/demo3-create-job-en.png)

#### Step 1: Basic information

Fill in the basic information, e.g. `Name : job-demo`. Then choose **Next** when you're done. 

![basic information](/demo3-job-basic-en.png)

#### Step 2: Job Settings

Fill the job settings with the following values of the screenshot.

- Back Off Limit：set to 5 (default to 6); Maximum retry count before mark the build task as failed; 
- Completions：set to 4 (default to 1); Expected number of completed build tasks;
- Parallelism：set to 2 (default to 1); Expected maximum number of parallel build tasks;
- Active Deadline Seconds：set to 200; The timeout of the running build tasks.

![job-setting](/demo-job-setting-en.png)

#### Step 3: Pod Template

Leave the [RestartPolicy](https://kubernetes.io/docs/concepts/workloads/Pods/pod-lifecycle/#restart-policy) as **Never**, then click **Add Container**.

![Add Container](https://pek3b.qingstor.com/kubesphere-docs/png/20190326142614.png)

Fill in the Pod Template, Container Name can be customized by the user, fill in the image with `perl`, other blanks could be remained default values.

Choose **Advanced Options**.

Then click **Add Command**, add the following four lines of commands in sequence, that is, perform a simple calculation and outputting the Pi to 2000 decimal.

```bash
# Command
perl
-Mbignum=bpi
-wle
print bpi(2000)
```

Then choose **Save** and click **Next** when you're done.

![Advanced Options](/job-demo-container-en.png) 


#### Step 4: Label Settings

Skip the Volume Settings and click **Next** to the **Label Settings**. We simply keep the default label settings as `app: job-demo`.

Then choose **Create** when you're done, you will be able to see the job-demo has been created successfully which displays running.

![Created successfully](/demo3-job-list-en.png)

### Verifying the Job

1. Enter into the `job-demo` and view the execution records, we can see it displays "completed (4/4)" and there are four Pods completed running, since the `completions` are set to four in the Step 2.

![Job execution record](/demo3-job-execution-record-en.png)

2. Switch to the **Resource Status**, we can easily find that there are 4 Pods generated by the `job-demo`. Since the **Parallelism** is set to 2, the Job will create 2 Pods in advance, then continue to create 2 Pods in parallel, finally 4 Pods will be created at the end of the Job.

![job creation details](/demo3-job-creation-details-en.png)

3. View one of the Pod, e.g. `job-demo-7vkcz`, then click `Container Logs` to view its container logs. 

![job-details](/demo3-job-container-en.png)

4. Then you will be able to see the container logs outputting page which display PI to 2000 decimal.

![container-log](/demo3-container-log-en.png)


