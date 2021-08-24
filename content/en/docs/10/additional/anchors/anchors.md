---
title: "10.3.1 Anchors"
weight: 1031
sectionnumber: 10
---


## Task {{% param sectionnumber %}}.2.1: Anchors

Instead of copy code around in your `.gitlab-ci.yml` file you can use [YAML-Anchors](https://docs.gitlab.com/ee/ci/yaml/#anchors) to avoid code duplications.

There are two uses cases for YAML anchors:

* You can use YAML anchors with script, before_script, and after_script to use predefined commands in multiple jobs:
* Use YAML anchors with variables to repeat assignment of variables across multiple jobs. You can also use YAML anchors when a job requires a specific variables block that would otherwise override the global variables.

{{% alert title="Info" color="warning" %}}
If you need shared functionalities across different projects, the you should use include/extends instead of YAML anchors!
{{% /alert %}}

This example shows the usage of YAML anchors with scripts.

{{< highlight yaml "hl_lines=" >}}{{< readfile file="manifests/10.0/additional/anchors/.gitlab-ci.yml" >}}{{< /highlight >}}
