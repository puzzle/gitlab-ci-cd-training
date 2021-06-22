---
title: "2. Pipeline structure"
weight: 2
sectionnumber: 2
---

In this lab you will learn how to define and structure a delivery pipeline for GitLab CI/CD.


## Task {{% param sectionnumber %}}.1: Create GitLab CI/CD configuration file

The GitLab CI/CD pipeline configuration has to be placed in a [YAML](https://en.wikipedia.org/wiki/YAML) file named `.gitlab-ci.yml`.

Create an empty file:

Place
: At the root of your git repository with the example application source code.

Filename
: `.gitlab-ci.yml`


## Task {{% param sectionnumber %}}.2: Create pipeline structure

GitLab CI reference: <https://docs.gitlab.com/ee/ci/yaml/>

The pipeline has basically two parts, the header with global settings followed by the stages.
Therefore are two basic concepts within the pipeline, jobs ans stages.

**Jobs**, which define what to do. For example, jobs that compile or test code.

**Stages**, which define when to run the jobs. For example, stages that run tests after stages that compile the code. Beware taht every job in the same stage is running concurrently.

Let's create a minimal pipeline. Add the following content to the `.gitlab-ci.yml` file.

{{< highlight yaml >}}{{< readfile file="manifests/02.0/.gitlab-ci.yml" >}}{{< /highlight >}}

Commit and push the changes.


### Stages

The global settings part contains stage definition.

{{< highlight yaml "hl_lines=1-2" >}}{{< readfile file="manifests/02.0/.gitlab-ci.yml" >}}{{< /highlight >}}

Stages are ...

<!-- TODO -->


### Jobs

Jobs are the most fundamental element of a GitLab pipeline.
You just defined your first job. It's name is `info`.

{{< highlight yaml "hl_lines=4-7" >}}{{< readfile file="manifests/02.0/.gitlab-ci.yml" >}}{{< /highlight >}}

Jobs are

* Defined with constraints stating under what conditions they should be executed.
* Top-level elements with an arbitrary name and must contain at least the script clause.
* Not limited in how many can be defined.

<!-- TODO -->

## Task {{% param sectionnumber %}}.3: Check pipeline execution

Go to your GitLab project and check the pipelines under `CI/CD` --> `Pipelines`.


<!-- TODO

* [ ] status
* [ ] jobs
* [ ] logs

 -->

Do you find the expected echo string?

<!--
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
-->
