---
title: "3. Pipeline basics"
weight: 3
sectionnumber: 3
---

In this section we will tech you the basics on working with GitLab CI/CD pipelines.
As we learned in the previous chapter, each Job must consist at least a `script` section.

{{% alert color="primary" %}}
**GitLab References**

[GitLab script keyword](https://docs.gitlab.com/ee/ci/yaml/README.html#script)

[GitLab before_script keyword](https://docs.gitlab.com/ee/ci/yaml/README.html#before_script)

[GitLab after_script keyword](https://docs.gitlab.com/ee/ci/yaml/README.html#after_script)
{{% /alert %}}


## Task {{% param sectionnumber %}}.1: Implicit data import

The content of the git repository is implicit imported into the pipeline's workspace. So you don't have to clone anything.


## Task {{% param sectionnumber %}}.2: Execute single commands

Inside a job we want to define the work that is done. The easiest way is to add a command. You already used a command inside the `info` job.

{{< highlight yaml "hl_lines=7" >}}{{< readfile file="manifests/03.0/.gitlab-ci.yml" >}}{{< /highlight >}}


## Task {{% param sectionnumber %}}.3: Define scripts

You can split long commands into multiline commands to improve readability with `|` (literal) and `>` (folded)
For example:

```yaml
job:
  script:
    - |
      echo "First command line."
      echo "Second command line."
      echo "Third command line."
```

See more details on the [GitLab CI/CD script syntax](https://docs.gitlab.com/ee/ci/yaml/script.html) documentation.


## Task {{% param sectionnumber %}}.4: Before and after scripts

Add additional behavior executed before or after the main script.


### Task {{% param sectionnumber %}}.4.1: Before Script execution

Use `before_script` to define an array of commands that should run before each job, but after artifacts are restored.

Scripts you specify in `before_script` are concatenated with any scripts you specify in the main script. The combine scripts execute together in a single shell.


### Task {{% param sectionnumber %}}.4.2: After Script execution

Use `after_script` to define an array of commands that run after each job, including failed jobs.

If a job times out or is cancelled, the `after_script` commands do not execute.

Scripts you specify in `after_script` execute in a new shell, separate from any before_script or script scripts. As a result, they:

* Have a current working directory set back to the default.
* Have no access to changes done by scripts defined in before_script or script, including:
  * Command aliases and variables exported in script scripts.
  * Changes outside of the working tree (depending on the runner executor), like software installed by a before_script or script script.
* Have a separate timeout, which is hard coded to 5 minutes. See the related issue for details.
* Don’t affect the job’s exit code. If the script section succeeds and the after_script times out or fails, the job exits with code 0 (Job Succeeded).

```yaml
job:
  before_script:
    - echo "This script executes before the script block"
  script:
    - echo "This script executes first. When it completes, the job's `after_script` executes."
  after_script:
    - echo "Execute this script after the normal script."
```

This produces following output:

```bash
This script executes before the script block
This script executes first. When it completes, the job's `after_script` executes.
Execute this script after the normal script.
```
