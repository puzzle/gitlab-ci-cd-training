---
title: "10. Shared functionality"
weight: 10
sectionnumber: 10
---

In this section we'll talk about how to include GitLab templates and other code snippets into your project.
This helps you to avoid code duplications and gives you the ability to store, share and reuse your pipeline code. Even across different projects.


## Task {{% param sectionnumber %}}.1: Include keyword

Use `include` to include external YAML files in your CI/CD configuration. You can break down one long gitlab-ci.yml file into multiple files to increase readability, or reduce duplication of the same configuration in multiple places.


You can also store template files in a central repository and include them in projects.

include requires the external YAML file to have the extensions `.yml` or `.yaml`, otherwise the external file is not included.

You can’t use YAML anchors across different YAML files sourced by include. You can only refer to anchors in the same file. To reuse configuration from different YAML files, use !reference tags or the extends keyword.

| Keyword   | Method                                                         |
|-----------|----------------------------------------------------------------|
| local     | Include a file from the local project repository.              |
| file      | Include a file from a different project repository.            |
| remote    | Include a file from a remote URL. Must be publicly accessible. |
| template  | Include templates that are provided by GitLab.                 |


## Task {{% param sectionnumber %}}.2: Shared functionality Lab

In this lab we will show you how to extend a job with an other job from a shared template.
Execute following tasks

* Define a new job named `deploy_to_k8s`
* Include the repository template with the local keyword. Use the predefined Gitlab Enviorments variable to set the `project` field value
* Extend the job with `.kubectl` from the template.
* Add a script section in the job with following command `kubectl version`  

{{% details title="solution" mode-switcher="normalexpertmode" %}}

{{< highlight yaml "hl_lines=8-10 64-70" >}}{{< readfile file="manifests/10.0/.gitlab-ci.yml" >}}{{< /highlight >}}

{{% /details %}}
