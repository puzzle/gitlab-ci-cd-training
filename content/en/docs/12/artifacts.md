---
title: "12. Artifacts"
weight: 12
sectionnumber: 12
---

Jobs can output an archive of files and directories. This output is known as a job artifact.
You can download job artifacts by using the GitLab UI.

Example of an artifact definition:

```yaml
pdf:
  script: xelatex mycv.tex
  artifacts:
    paths:
      - mycv.pdf
    expire_in: 1 week
```

The `paths` keyword determines which files to add to the job artifacts. All paths to files and directories are relative to the repository where the job was created.

The `expire_in` keyword determines how long GitLab keeps the job artifacts. You can also use the UI to keep job artifacts from expiring. If `expire_in` is not defined, the instance-wide setting is used.

{{% alert color="primary" %}}
**GitLab References**

[GitLab `artifacts` keyword](https://docs.gitlab.com/ee/ci/yaml/README.html#artifacts)

{{% /alert %}}


## Task {{% param sectionnumber %}}.1: Artifacts Lab

* Add an `artifacts` section to the `build_image` job
* Add an artifact with the name `container-scanning-report_<identifier>.txt`
* Define the artifact `paths` pointing to file that the Trivy command writes.
* Set a retention time of 30 days for the artifacts

{{% alert title="Hint" color="primary" %}}
For the identifier, use the Short Commit SHA from the predefined GitLab variables.

For the `paths` file path see the output flag (-o) of the Trivy command of the previous lab.
{{% /alert %}}


## Task {{% param sectionnumber %}}.2: Artifacts Lab solution

Updated `.gitlab-ci.yml` file for this lab:

{{< details title="show solution" mode-switcher="normalexpertmode" >}}

{{% readAndHighlight file="/manifests/12.0/.gitlab-ci.yml" code="true" lang="yaml" highlight="hl_lines=74-78" %}}

{{< /details >}}


### Download Job Artifacts

The defined artifact can be found on the `build_image` Job detail page of this Pipeline. Find the `Job artifacts` section on the right side beside the `Job log`.

Click on `Download` to get the Trivy report file and open it to see the report.


## Task {{% param sectionnumber %}}.3: Pipeline Artifacts Lab

Go to your pipeline `Build` --> `Pipelines` and click on the download menu ⍗ to see the downloadable artifacts.

Then download them and open the JUnit test report.

![Download artifacts](../download_artifacts.png)
