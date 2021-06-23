---
title: "8. Build Options"
weight: 8
sectionnumber: 8
---

In this section we'll talk about global pipeline configuration.
There are differnt options for global pipeline configuration. This helps to reduce code duplication over different projects.


## Task {{% param sectionnumber %}}.1: Global pipeline configuration

You can set global defaults for some keywords. Jobs that do not define one or more of the listed keywords use the value defined in the default: section.

These job keywords can be defined inside a `default:` section:

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

```yaml

default:
  before_script:
    - "This will be executed as default if no other before scipt is set"

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

This produces following output:

```bash
This will be executed as default if no other before scipt is set
This script executes first. When it completes, the jobs `after_script` executes.

This script executes before the script block
This script executes first. When it completes, the jobs `after_script` executes.
Execute this script after the normal script.
```


## Task {{% param sectionnumber %}}.2: Global pipeline configuration lab

* Create the default job
* Create a global timeout of 15 minutes
* Add a retry number of 2 times to the `info` job


## Task {{% param sectionnumber %}}.3: Global pipeline configuration solution

{{% details title="solution" mode-switcher="normalexpertmode" %}}

{{< highlight yaml "hl_lines=12-13 17" >}}{{< readfile file="manifests/08.0/.gitlab-ci.yml" >}}{{< /highlight >}}

{{% /details %}}


<!-- TODO 


-->

