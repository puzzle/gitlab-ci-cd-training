---
title: "12. Artifacts"
weight: 12
sectionnumber: 12
---

Jobs can output an archive of files and directories. This output is known as a job artifact.

You can download job artifacts by using the GitLab UI.


## Task {{% param sectionnumber %}}.2: Artifacts Lab

* Add a `artifacts` section to the `build_image` job
* Add a artifact wth the name `container-scanning-report_<identifier>.json`
* Store the artefact under following path `reports/container-scanning-report_<identifier>.json`
* For the identifier use the Short Commit SHA from the predefined GitLab variables.
* Set a retention time of 30 days for the artifacts


## Task {{% param sectionnumber %}}.3 Artifacts Lab solution

{{< highlight yaml "hl_lines=56-60" >}}{{< readfile file="manifests/012.0/.gitlab-ci.yml" >}}{{< /highlight >}}
