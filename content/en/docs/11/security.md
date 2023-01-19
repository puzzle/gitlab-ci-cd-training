---
title: "11. Security"
weight: 11
sectionnumber: 11
---

GitLab offers a wide support for security issues. In this lab, we will cover the GitLabs internal security templates first, and then we will show you how to include custom security tools into your pipeline.


## Task {{% param sectionnumber %}}.1: Security Template Lab

In this lab we will show you how to extend a job with another job from a shared template.
Execute following tasks

* Include the template `Security/SAST.gitlab-ci.yml`
* Include the template `templates/Secret-Detection.yml` from the same repository
* Include the template `Security/License-Scanning.gitlab-ci.yml`

Go to your GitLab project and check the pipeline for this lab. You should find the additional Jobs on the pipeline overview.


## {{% param sectionnumber %}}.2: Security Template Lab Solution

Updated `.gitlab-ci.yml` file for this lab:


{{< readAndHighlight file="manifests/11.0/11.1/.gitlab-ci.yml" code="true" lang="yaml" highlight="hl_lines=10-14">}}



## Task {{% param sectionnumber %}}.3: Let the pipeline fail

To test the Secret Detection template we add a secret in our sample project. Create a new file in the root directory called `private_key` and copy the following content into it.

```txt
-----BEGIN OPENSSH PRIVATE KEY-----
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
-----END OPENSSH PRIVATE KEY-----
```

Commit and push the changes to trigger the pipeline.

Now the pipeline should fail because the GitLab Secret Analyzer will find a private key inside our repository.

![security_pipeline_fail](../security_pipeline_fail.png)

Here you see the failed pipeline. By clicking ⋮ on the right side you can download the job artifacts. To get the report of the failed job, click on `Download secret_detection_default_branch:secret_detection artifact`. We will learn more on artifacts in the next lab.

{{% alert title="Warning" color="secondary" %}}If you ever push a secret into a repository, **YOU MUST CONSIDER THIS SECRET AS INSECURE**. Remove the secret from the repository and change all related secrets!{{% /alert %}}

Now remove the private key from the repository to execute the next steps.


## Task {{% param sectionnumber %}}.4: Custom security tooling

In this section we'll show you how to use custom security tools in your pipeline. For this example we use [Trivy](https://github.com/aquasecurity/trivy), a local Docker image security scanner.

Extend the existing `build_image` job inside `.gitlab-ci.yml` with the following configuration:

Add following commands into the `before_script` block to download Trivy:

```bash
export TRIVY_VERSION=$(wget -qO - "https://api.github.com/repos/aquasecurity/trivy/releases/latest" | grep '"tag_name":' | sed -E 's/.*"v([^"]+)".*/\1/')
echo $TRIVY_VERSION
wget --no-verbose https://github.com/aquasecurity/trivy/releases/download/v${TRIVY_VERSION}/trivy_${TRIVY_VERSION}_Linux-64bit.tar.gz -O - | tar  -zxvf -
```

Then call Trivy in the `script` block (after the build command):

```bash
mkdir -p reports
./trivy i --exit-code 0 --severity CRITICAL -o reports/container-scanning-report_$CI_COMMIT_SHORT_SHA.txt $IMAGE_NAME
```

Commit and push the code to rerun the pipeline.

Check the Trivy log output of the `build_image` Job.

{{% alert title="Info" color="secondary" %}}
You would do the security scanning in a separate job. Here we do not have an Image Registry to store the Container Image. This would be used to retrieve the Container Image in the next Job to do the scanning.
{{% /alert %}}


## {{% param sectionnumber %}}.5: Custom security tooling Solution

Updated `.gitlab-ci.yml` file for this lab:


{{< readAndHighlight file="manifests/11.0/11.4/.gitlab-ci.yml" code="true" lang="yaml" highlight="hl_lines=62-64 67-68">}}

