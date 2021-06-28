---
title: "12. Artifacts"
weight: 12
sectionnumber: 12
---

Jobs can output an archive of files and directories. This output is known as a job artifact.

You can download job artifacts by using the GitLab UI.


## Task {{% param sectionnumber %}}.1: Artifacts Lab

* Add a `artifacts` section to the `build_image` job
* Add a artifact wth the name `container-scanning-report_<identifier>.json`
* Store the artefact under following path `reports/container-scanning-report_<identifier>.json`
* For the identifier use the Short Commit SHA from the predefined GitLab variables.
* Set a retention time of 30 days for the artifacts

{{% details title="solution" mode-switcher="normalexpertmode" %}}

{{< highlight yaml "hl_lines=59-63" >}}{{< readfile file="manifests/12.0/.gitlab-ci.yml" >}}{{< /highlight >}}

{{% /details %}}


## Task {{% param sectionnumber %}}.2 Artifacts Lab solution

Go to your pipeline `CI/CD` --> `Pipeline` and click on the ⋮ to see the downloadable artifacts.
Then download and open the junit test report.

![Download artifacts](../download_artifacts.png)
