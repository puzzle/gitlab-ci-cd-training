---
title: "1. CHANGEME Sample Chapter"
weight: 1
sectionnumber: 1
---

## Title 1


```yaml
#GitLab CI reference: https://docs.gitlab.com/ee/ci/yaml/
#3. Gitlab Pipelines
image: registry.puzzle.ch/docker.io/alpine:latest

stages: #3. GitLab Stages
  - info

info: #3. GitLab Jobs
  stage: info
  script: #2. First Steps Scripts 
    - echo "Hello World"

build:
  stage: build

build_container:
  stage: build

```
