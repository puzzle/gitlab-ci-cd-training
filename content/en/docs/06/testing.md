---
title: "6. Application Testing"
weight: 6
sectionnumber: 6
---

In this lab we will run the basic tests of the application.


## Task {{% param sectionnumber %}}.1: Create test stage

Basic application tests (unit tests) are executed inside a test stage.

Create a new job inside `.gitlab-ci.yml` with the following configuration:

* job name: `test_application`
* stage: `test`
* image: `registry.access.redhat.com/ubi8/openjdk-11:latest`
* script:`./gradlew check`

Don't forget to add the `test` stage to the stages list.

<!-- TODO 

* [ ] mobi specific tags!!

  tags:
    - mobiliar
    - build

-->

{{% details title="job hint" mode-switcher="normalexpertmode" %}}

{{< highlight yaml >}}{{< readfile file="manifests/06.0/test-job-base.yml" >}}{{< /highlight >}}

{{% /details %}}


## Task {{% param sectionnumber %}}.2: Check the pipeline

Go to your GitLab project and check the pipelines under `CI/CD` 🠒 `Pipelines`.

Check that the test job was successful.

Do you see the executed tests and the results?

When you see them, tell us please. We only have the return value of the test script to decide if all tests run through or one or more failed. Check the next task to see how we capture the test reports.


## Task {{% param sectionnumber %}}.3: Show test reports

The job can be extended with an `artifacts` configuration. Dev's know that the unit test reports are stored inside the `build/test-results/` folder.

This is the configuration that makes GitLab CI/CD store the test results.

{{< highlight yaml >}}{{< readfile file="manifests/06.0/test-job-reports.yml" >}}{{< /highlight >}}

See also the official documentation: [Unit test reports](https://docs.gitlab.com/ee/ci/unit_test_reports.html#unit-test-reports)


This is the final pipeline that includes unit testing and recording of test results.

{{< highlight yaml "hl_lines=4 17-25" >}}{{< readfile file="manifests/06.0/.gitlab-ci.yml" >}}{{< /highlight >}}
<!-- TODO variables from the previous Lab are missing-->

Navigate to the newest Pipeline inside GitLab. The Tests tab should now show the executed tests.


## Task {{% param sectionnumber %}}.4: Break a test

To show how the pipeline reacts on test failures we change a test to fail.

Open the test class `src/test/java/ch/appuio/techlab/controller/PodRestControllerTest.java`. Change the assertion from **Pod** to **Hoppla**.

{{< highlight yaml >}}
        // then
        assertThat(podDescription, startsWith("Hoppla: "));
{{< /highlight >}}

Commit and push those changes and then check that the pipeline failed and the test results inside the Tests tab have one failure.

{{< highlight yaml "hl_lines=2" >}}
java.lang.AssertionError:
Expected: a string starting with "Hoppla: "
     but: was "Pod: 42"
{{< /highlight >}}

Revert the latest commit to fix the test again.
