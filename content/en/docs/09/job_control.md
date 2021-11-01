---
title: "9. Job control"
weight: 9
sectionnumber: 9
---

In this section wel show you different options how to control the job execution. Sometimes some jobs will be used only in certain branches, or for example you will execute a stage only if the commit is tagged with a [Semver number](https://semver.org/).


{{% alert color="primary" %}}
**GitLab References**

[GitLab `only` / `except` keyword](https://docs.gitlab.com/ee/ci/yaml/README.html#only--except)

[GitLab `when` keyword](https://docs.gitlab.com/ee/ci/yaml/README.html#when)

[GitLab `allow_failure` keyword](https://docs.gitlab.com/ee/ci/yaml/README.html#allow_failure)
{{% /alert %}}


## {{% param sectionnumber %}}.1: Job control

You can use `only` and `except` to control when to add jobs to pipelines.

Use only to define when a job runs.
Use except to define when a job does not run.

Use the only:refs and except:refs keywords to control when to add jobs to a pipeline based on branch names or pipeline types.


## {{% param sectionnumber %}}.2: Execution control

| Keyword    | Method                                                                                                                                    |
|------------|-------------------------------------------------------------------------------------------------------------------------------------------|
| on_sucess  | **(default)** - Execute job only when all jobs in earlier stages succeed, or are considered successful because they have allow_failure: true. |
| on_failure | Execute job only when at least one job in an earlier stage fails.                                                                         |
| always     | Execute job regardless of the status of jobs in earlier stages.                                                                           |
| manual     | Execute job manually.                                                                                                                     |
| delayed    | Delay the execution of a job for a specified duration                                                                                     |
| never      | Don’t execute job.                                                                                                                        |


## {{% param sectionnumber %}}.3: Failure control

Use `allow_failure` when you want to let a job fail without impacting the rest of the CI suite. The default value is false, except for manual jobs that use the `when: manual` syntax.


## Task {{% param sectionnumber %}}.4: Job control lab

* Add a new Job named `deploy_to_prod` to a new `deploy` stage
* Add a manual pipeline gate to make sure a manual action is required to execute this job
* Add a new Job execution rule, the job should run only on the `release` branch
* Add a script block with a simple `echo` command

Commit and push these changes to the main branch and go to `CI/CD` --> `Pipelines` and check the pipeline status. You may notice that the job `deploy_to_prod` is not visible. This is because we add an execution rule for the `release` branch only. To fix this, we need to switch back to `Repository` --> `Branches` and create a new branch called `release`.

Now the pipeline should run again and we can see the newly created job. After the pipeline executed successfully, you may notice that the `deploy` step wasn't executed yet and isn't marked with a green tick. This is because we configured the job as a manual action. To trigger this job, we need to select the job and do it manually.

![manual_job](../manual_trigger.png)

{{% alert title="Warning" color="primary" %}}
Switch back to the `main` or `master` branch before beginning the next labs.
{{% /alert %}}


## Solution

Updated `.gitlab-ci.yml` file for this lab:

{{% details title="show solution" mode-switcher="normalexpertmode" %}}

{{< highlight yaml "hl_lines=6 62-68" >}}{{< readfile file="manifests/09.0/.gitlab-ci.yml" >}}{{< /highlight >}}

{{% /details %}}
