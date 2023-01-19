---
title: "8. Build Options"
weight: 8
sectionnumber: 8
---


In this section we'll talk about global pipeline configuration.
There are different options for global pipeline configuration. This helps to reduce code duplication in your pipeline.


## {{% param sectionnumber %}}.1: Global pipeline configuration default

You can set global defaults for some keywords. Jobs that do not define one or more of the listed keywords use the value defined in the `default` section, therefore you can simply overwrite default values, by specifying the values explicitly in a job.

There are a couple of default settings you can define inside a `default` section:

* `after_script`
* `artifacts`
* `before_script`
* `cache`
* `image`
* `interruptible`
* `retry`
* `services`
* `tags`
* `timeout`

Let's have a look at an example

```yaml

default:
  before_script:
    - "This will be executed as default if no other before script is set"

job1:
  script:
    - echo "This script executes first. When it completes, the job's `after_script` executes."

job2:
  before_script:
    - echo "This script executes before the script block"
  script:
    - echo "This script executes first. When it completes, the job's `after_script` executes."
  after_script:
    - echo "Execute this script after the normal script."
```

This produces the following output:

```bash
This will be executed as default if no other before script is set
This script executes first. When it completes, the jobs `after_script` executes.

This script executes before the script block
This script executes first. When it completes, the jobs `after_script` executes.
Execute this script after the normal script.
```


## Task {{% param sectionnumber %}}.2: Global pipeline configuration lab

In this task you're going to configure several things for your pipeline.

* Create the default section
* Create a global timeout of 5 minutes.
* Add a retry number of 2 times to the `info` job, this means, that the job will be retried to succeed twice.

Edit the `.gitlab-ci.yml`, commit and push your changes and then verify the output of the pipeline run.


## Solution

Updated `.gitlab-ci.yml` file for this lab:

{{% details title="show solution" mode-switcher="normalexpertmode" %}}


{{< readAndHighlight file="manifests/08.0/.gitlab-ci.yml" code="true" lang="yaml" highlight="hl_lines=14-15 19">}}

{{% /details %}}
