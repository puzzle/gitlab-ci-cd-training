---
title: "10.3.1 Anchors"
weight: 1031
sectionnumber: 10
---


## Task {{% param sectionnumber %}}.2.1: Anchors

Instead of copy code around in your `.gitlab-ci.yml` file you can use [YAML-Anchors](https://docs.gitlab.com/ee/ci/yaml/#anchors) to avoid code duplications

{{% alert title="Info" color="warning" %}}
If you need sahred functionalities across different projects, the you should use include/extends instead of YAML anchors!
{{% /alert %}}
