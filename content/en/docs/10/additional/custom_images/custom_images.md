---
title: "10.2.1 Custom Images"
weight: 1021
sectionnumber: 10
---

There are several reasons to create your own Docker image with all containing tools and ....

* Chache build dependencies
* Speedup your pipeline
* Integrate customs tools
* Avoid code duplication across your pipeline


## Task {{% param sectionnumber %}}.2.1: Create a custom image

In this example we're going to create a custom Docker image which contains kubectl and helm for deploying Helm charts into a Kubernetes cluster.
Create a new file called `Dockerfile` in your workspace and copy-paste followig content.

{{< highlight docker "hl_lines=" >}}{{< readfile file="manifests/04.0/additional/Dockerfile" >}}{{< /highlight >}}

{{% alert title="Info" color="primary" %}}
If you dont have Docker installed on your machine, you can skip this step and go further to section 4.2
{{% /alert %}}


To build the Dockerfile with following command:

```bash
docker build -t <your-registry>/k8-custom-tools:latest .
```

And then push the image into the registry

```bash
docker push <your-registry>/k8-custom-tools:latest
```


## Task {{% param sectionnumber %}}.2.2: Use your custom image

Now you can reference your custom image with the `image` keyword in your `.gitlab-ci.yml`

{{< highlight yaml "hl_lines=19-24" >}}{{< readfile file="manifests/04.0/additional/.gitlab-ci.yml" >}}{{< /highlight >}}
