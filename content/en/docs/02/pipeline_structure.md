---
title: "2. Pipeline structure"
weight: 2
sectionnumber: 2
---

In this lab you will learn how to define and structure a delivery pipeline for GitLab CI/CD.


## Task {{% param sectionnumber %}}.1: Create GitLab CI/CD configuration file

The GitLab CI/CD pipeline configuration has to be placed in a [YAML](https://en.wikipedia.org/wiki/YAML) file named `.gitlab-ci.yml`.

Create an empty `.gitlab-ci.yml` file in the root directory of your repository.


## Task {{% param sectionnumber %}}.2: Create pipeline structure

GitLab CI reference: <https://docs.gitlab.com/ee/ci/yaml/>

The pipeline has basically two parts, the header with global settings followed by the stages.

There exist two basic concepts within the pipeline, jobs and stages.


**Jobs**, which define what to do. For example, jobs that compile or test code.

**Stages**, which define when to run the jobs. For example, stages that run tests after stages that compile the code. Beware that every job in the same stage is running concurrently.

Let's create a minimal pipeline. First we need to change to the correct directory, the root directory of the cloned repository. (from [Lab 1.3](../../01/getting_started/#task-13-clone-the-git-repository))

Open GitBash Terminal and change the directory:

```bash
cd <root-directory-of-the-git-repo>
```
{{% alert title="Info" color="primary" %}}
Replace `<root-directory-of-the-git-repo>` with the actual path to the cloned repository. eg. `~/gitlabcicd-training/example-spring-boot-helloworld`
{{% /alert %}}

Create a new file `.gitlab-ci.yml` and add the following content to it. It must be located directly in the root directory of the repository.

```bash
vim .gitlab-ci.yml
```

{{< readfile file="manifests/02.0/.gitlab-ci.yml" code="true" lang="yaml" >}}


{{% alert title="Info" color="primary" %}}
You can also use your favorite editor instead of `vim`.
{{% /alert %}}

Commit and push the changes.

{{% details title="hint" mode-switcher="normalexpertmode" %}}

```bash
git add .
git commit -m "Add minimal pipeline"
git push origin master
```

{{% /details %}}

Our first pipeline is pretty simple, it has one stage with one job, which only executes a script that echos something during the pipeline run.


### Stages

The global settings part contains stage definition.

{{< readAndHighlight file="manifests/02.0/.gitlab-ci.yml" code="true" lang="yaml" highlight="hl_lines=1 2">}}


### Jobs

Jobs are the most fundamental element of a GitLab pipeline.
You just defined your first job. It's name is `info`.

{{< readAndHighlight file="manifests/02.0/.gitlab-ci.yml" code="true" lang="yaml" highlight="hl_lines=4-7">}}

Jobs are ...

* top-level elements with an arbitrary name and must contain at least the script clause
* defined with constraints stating under what conditions they should be executed
* not limited in how many that can be defined


## Task {{% param sectionnumber %}}.3: Check pipeline execution

Go to your GitLab project and check the pipelines under `CI/CD` --> `Pipelines`.

The pipeline at the top of the table is the one that has been triggered by your latest commit.

Clicking on the status or the pipeline number brings you to the pipeline detail view. This page has an overview and tabs for pipeline view, dependencies, jobs and test results. The tabs may vary depending on the version of your GitLab instance. The job logs are available on the job detail view.

Do you find the expected echo string?


## {{% param sectionnumber %}}.4: Lab contents

At the end of this day you should have an fully working pipeline with several stages and jobs

![Pipeline Complete](../complete_pipeline.png)
