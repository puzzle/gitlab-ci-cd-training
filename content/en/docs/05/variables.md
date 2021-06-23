---
title: "5. Variables"
weight: 5
sectionnumber: 5
---

CI/CD variables are a type of environment variable. You can use them to:

Control the behavior of jobs and pipelines.

* Store values you want to re-use.
* Avoid hard-coding values in your .gitlab-ci.yml file.
* You can use predefined CI/CD variables or define custom:

Variables in the .gitlab-ci.yml file.

* Project CI/CD variables.
* Group CI/CD variables.
* Instance CI/CD variables.

In this lab we will talk about the variables in the gitlab-ci.xml file only


## Task {{% param sectionnumber %}}.1: Define and access custom Variables

To create a custom variable in the .gitlab-ci.yml file, define the variable and value with variables keyword in the top level section.

Global variables are def
```yaml
variables:
  FOO: BAR
```

You can later reference this variable elswhere in your gitlab-ci.yml file. For example
```yaml
  - echo "Hello Foo ${FOO}"
```

Output:
```bash
hello Foo Bar
```
{{% alert color="danger" %}}Never store sensitive information like passwords directly in the gitlab-ci.yml file{{% /alert %}}
<!-- TODO -->

## Task {{% param sectionnumber %}}.2: Predefined Variables


There is a set of predefined GitLab Variables which you can reference in your gitlab-ci.yml script
Each of this variable has the `CI_` prefix, such as:

* `CI_COMMIT_BRANCH` The commit branch name. Available in branch pipelines, including pipelines for the default branch. Not available in merge request pipelines or tag pipelines.
* `CI_PROJECT_NAME` The name of the directory for the project. For example if the project URL is gitlab.example.com/group-name/project-1, CI_PROJECT_NAME is project-1.
* `CI_COMMIT_MESSAGE` The full commit message.

Under following link you can find a full list of all available predefined GitLab variables.
https://docs.gitlab.com/ee/ci/variables/predefined_variables.html


## Task {{% param sectionnumber %}}.2: Variables Lab

Define following two global variables in your gitlab-ci.yml

* GIT_STRATEGY = clone
* COMPILE = false


## Task {{% param sectionnumber %}}.4 Variables solution

{{% details title="solution" mode-switcher="normalexpertmode" %}}

{{< highlight yaml "hl_lines=5-7" >}}{{< readfile file="manifests/05.0/.gitlab-ci.yml" >}}{{< /highlight >}}

{{% /details %}}
