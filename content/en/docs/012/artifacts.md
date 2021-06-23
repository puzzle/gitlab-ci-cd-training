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


## Task {{% param sectionnumber %}}.2: Artifacts Lab

* Add a `artifacts` section to the `build_image` job
* Add a artifact wth the name `container-scanning-report_<identifier>.json`
* Store the artefact under following path `reports/container-scanning-report_<identifier>.json`
* For the identifier use the Short Commit SHA from the predefined GitLab variables.
* Set a retention time of 30 days for the artifacts


## Task {{% param sectionnumber %}}.3 Artifacts Lab solution

{{< highlight yaml "hl_lines=59-63" >}}{{< readfile file="manifests/012.0/.gitlab-ci.yml" >}}{{< /highlight >}}


## Task {{% param sectionnumber %}}.3 Artifacts Lab solution

Go to your pipeline `CI/CD` 🠒 `Pipeline` and click on the ⋮ to see the downloadable artefacts.
Then download and open the junit test report.

![Download artifacts](../download_artifacts.png)
