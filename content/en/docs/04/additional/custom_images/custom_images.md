---
title: "4.4.1 Custom Images"
weight: 441
sectionnumber: 4
---

There are several reasons to create your own Docker image with all containing tools and ....

* Chache build dependencies
* Speedup your pipeline
* Integrate customs tools
* Avoid code duplication across your pipeline

{{% alert title="Info" color="primary" %}}
To complete this additional lab you must have installed Docker on your local machine.
{{% /alert %}}


## Task {{% param sectionnumber %}}.1: Create a custom image

In this example we're going to create a custom Docker image which contains kubectl and helm for deploying Helm charts into a Kubernetes cluster.
Create a new file called `Dockerfile` in your workspace and copy-paste followig content.

{{< highlight docker "hl_lines=" >}}{{< readfile file="manifests/04.0/additional/Dockerfile" >}}{{< /highlight >}}

**If you dont have Docker installed on your machine, you can skip this step and go further to section 4.2**
To build the Dockerfile with following command:

`docker build -t k8-custom-tools:latest .`

And then push the image into the registry

`docker push k8-custom-tools:latest`


## Task {{% param sectionnumber %}}.2: Use your custom image

{{< highlight yaml "hl_lines=19-24" >}}{{< readfile file="manifests/04.0/additional/.gitlab-ci.yml" >}}{{< /highlight >}}
