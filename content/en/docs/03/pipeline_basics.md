---
title: "3. Pipeline basics"
weight: 3
sectionnumber: 3
---

In this section, we will teach you the basics of working with GitLab CI/CD pipelines.
As we learned in the previous chapter, each Job must consist of at least one `script` section.

{{% alert color="primary" %}}
**GitLab References**

[GitLab script keyword](https://docs.gitlab.com/ee/ci/yaml/README.html#script)

[GitLab before_script keyword](https://docs.gitlab.com/ee/ci/yaml/README.html#before_script)

[GitLab after_script keyword](https://docs.gitlab.com/ee/ci/yaml/README.html#after_script)

[GitLab tags keyword](https://docs.gitlab.com/ee/ci/yaml/index.html#tags)

{{% /alert %}}


## {{% param sectionnumber %}}.1: Implicit data import

The content of the git repository is implicit imported into the pipeline's work space. So you don't have to clone anything.


## {{% param sectionnumber %}}.2: Execute single commands

Inside a job we want to define the work that is done. The easiest way is to add a command. You already used a command inside the `info` job.

{{< readAndHighlight file="/manifests/03.0/.gitlab-ci.yml" code="true" lang="yaml" highlight="hl_lines=7">}}


## {{% param sectionnumber %}}.3: Define scripts

You can split long commands into multi line commands to improve readability with `|` (literal) and `>` (folded)
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


## {{% param sectionnumber %}}.4: Before and after scripts

Add additional behavior executed before or after the main script.


### {{% param sectionnumber %}}.4.1: Before Script execution

Use `before_script` to define an array of commands that should run before each job, but after artifacts are restored.

Scripts you specify in `before_script` are concatenated with any scripts you specify in the main script. The combined scripts execute together in a single shell.


### {{% param sectionnumber %}}.4.2: After Script execution

Use `after_script` to define an array of commands that run after each job, including failed jobs.

If a job times out or is canceled, the `after_script` commands do not execute.

Scripts you specify in `after_script` execute in a new shell, separated from any `before_script` or `script` scripts. As a result, they:

* Have a current working directory set back to the default.
* Have no access to changes done by scripts defined in `before_script` or `script`, including:
  * Command aliases and variables exported in `script` scripts.
  * Changes outside of the working tree (depending on the runner executor), like software installed by a `before_script` or `script` script.
* Have a separate timeout, which is hard coded to 5 minutes. See the related issue for details.
* Don’t affect the job’s exit code. If the script section succeeds and the `after_script` times out or fails, the job exits with code 0 (Job Succeeded).

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


### {{% param sectionnumber %}}.5: Runner Tags

What is a GitLab runner? A runner is an isolated (virtual) machine that picks up builds through the coordinator API of GitLab CI. A runner can be specific to a certain project or serve any project in GitLab CI. A runner that serves all projects is called a shared runner. You can setup multiple runners with different capabilities for different use-cases. Use tags to select a specific runner from the list of all runners that are available for the project. For example, if you have an OS X runner with tag osx and a Windows runner with tag windows, you can run a job on each platform:

```yaml
windows job:
  stage:
  - build
  tags:
  - windows
  script:
  - echo Hello, %USERNAME%!

osx job:
  stage:
  - build
  tags:
  - osx
  script:
  - echo "Hello, $USER!"
```

{{% alert title="Warning" color="secondary" %}}In the following labs you need set the correct tags to choose a suitable runner. This will vary from environment to environment. Please ask your instructor for the matching runner tags.
{{% /alert %}}
