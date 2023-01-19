---
title: "5. Variables"
weight: 5
sectionnumber: 5
---

In GitLab CI/CD, variables can be used to customize jobs by defining and storing values. When using variables there is no need to hard code values. In GitLab, CI/CD variables can be defined by going to `Settings` --> `CI/CD` --> `Variables`  or by simply defining them in the .gitlab-ci.yml file.

Variables are useful for configuring third-party services for different environments, such as testing, staging, production, etc. Modify the services attached to those environments by simply changing the variable that points to the API endpoint the services need to use. Also use variables to configure jobs and then make them available as environment variables within the jobs when they run.

As pointed out before, you can define variables in your `gitlab-ci.yml`. You can reuse this variable within your pipeline across different jobs and stages.

If you want to reuse a variable across different Projects or Groups, you can define them through your GitLab instance (`Settings` --> `CI/CD` --> `Variables`)

In this lab we will talk about the variables in the `gitlab-ci.yml` file only.

{{% alert color="primary" %}}
**GitLab References**

[GitLab Variables](https://docs.gitlab.com/ee/ci/variables/)

[GitLab Variables keyword](https://docs.gitlab.com/ee/ci/yaml/README.html#variables)
{{% /alert %}}


## {{% param sectionnumber %}}.1: Define and access custom Variables

To create a custom variable in the `.gitlab-ci.yml` file, define the variable and value with variable keywords in the top level section.

Global variables can be defined in the variables section:
```yaml
variables:
  FOO: BAR
```

You can later reference this variable elsewhere in your `.gitlab-ci.yml` file. For example
```yaml
  - echo "Hello Foo ${FOO}"
```

Output:
```bash
hello Foo Bar
```
{{% alert title="Warning" color="secondary" %}}Never store sensitive information like passwords directly in the `.gitlab-ci.yml` file. {{% /alert %}}
<!-- TODO -->

## {{% param sectionnumber %}}.2: Predefined Variables


There is a set of predefined GitLab Variables which you can reference in your `.gitlab-ci.yml` script.
Each of these variables has the `CI_` prefix, such as:

* `CI_COMMIT_BRANCH` The commit branch name. Available in branch pipelines, including pipelines for the default branch. Not available in merge request pipelines or tag pipelines.
* `CI_PROJECT_NAME` The name of the directory for the project. For example if the project URL is gitlab.example.com/group-name/project-1, CI_PROJECT_NAME is project-1.
* `CI_COMMIT_MESSAGE` The full commit message.

Under the following link you can find a full list of all available predefined GitLab variables.
https://docs.gitlab.com/ee/ci/variables/predefined_variables.html


## Task {{% param sectionnumber %}}.3: Variables Lab

Define the following two global variables in your `.gitlab-ci.yml`

* GIT_STRATEGY = clone
* COMPILE = false

The `GIT_STRATEGY` defines how the git repository is fetched during a pipeline run; valid options are `clone`, `fetch` or `none`.
The `COMPILE` variable disable project compilation and dependency fetching for the security analyser.


To define global variables within a pipeline, add the variables block to the `.gitlab-ci.yml`.

{{< readAndHighlight file="manifests/05.0/05.3/.gitlab-ci.yml" code="true" lang="yaml" highlight="hl_lines=5-7">}}


Commit and push your changes. Check that the pipeline finishes without problems. The output is the same as in the previous lab.


## {{% param sectionnumber %}}.4: Secret and protected Variables

In some cases you need to store sensitive information in a variable. Instead of defining the variable directly in the `.gitlab-ci.yml` you can create a secret variable in the GitLab project settings.

To add a new secret variable, navigate in the main menu to `Settings` --> `CI/CD` --> `Variables` --> `Expand` --> `Add variable`

Flags:

* **Protected variable** You can protect a project, group or instance CI/CD variable so it is only passed to pipelines running on protected branches or protected tags
* **Mask variable** You can mask a variable so the value of the variable doesn't display in job logs.


## Task {{% param sectionnumber %}}.5: Secret and protected Variables Lab

Define following two secret variables in your project

* USERNAME = fooser
* PASSWORD = bassword
  * as a masked variable

Then add a new script line at the end of the info job with following command `echo "Username is ${USERNAME} with password ${PASSWORD}"`

Run the pipeline again and navigate to the info job log output. You should see the following line

`Username is fooser with password [MASKED]`


To define secret variables within a pipeline, add the variables within the project settings and add the script block to the `.gitlab-ci.yml`.

{{< readAndHighlight file="manifests/05.0/05.5/.gitlab-ci.yml" code="true" lang="yaml" highlight="hl_lines=13">}}


Commit and push your changes.

How is the protected variable masked in the job log?
