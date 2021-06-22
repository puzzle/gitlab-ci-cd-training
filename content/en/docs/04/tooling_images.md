---
title: "4. Tooling Images"
weight: 4
sectionnumber: 4
---

How to choose and use the right Container Image.


## Task {{% param sectionnumber %}}.1: Choosing tooling images

To build an application or to deploy it, specific languages, frameworks or tools are needed.

Therefore we need to find the right Container Image.

Good sources for Container Images are trusted registries like [Red Hat](https://catalog.redhat.com/software/containers/explore).
You can also use official Images from the software company developing the needed tool.

For tools and languages it is a good starting point to check the [Pre-Built CircleCI Docker Images](Pre-Built CircleCI Docker Image).

{{% alert  color="primary" %}}
Using freely available Container Images is risky. Be aware of the security constraints.
{{% /alert %}}

<!-- TODO 
* [ ] how to check Images?
-->


## Task {{% param sectionnumber %}}.2: Build the application

The example source is a Java 11 application. For that we use the [openjdk-11](https://catalog.redhat.com/software/containers/ubi8/openjdk-11/5dd6a4b45a13461646f677f4) Image from Red Hat.

Create a new job inside `.gitlab-ci.yml` with the following configuration:

* job name: `build_application`
* stage: `build`
* image: `registry.access.redhat.com/ubi8/openjdk-11:latest`
* script:`./gradlew assemble`

Don't forget to add the `build` stage to the stages list.


<!-- TODO 

* [ ] mobi specific tags!!

  tags:
    - mobiliar
    - build

-->


## Task {{% param sectionnumber %}}.3: Check the pipeline

The pipeline should now look like this:

{{< highlight yaml "hl_lines=3 10-17" >}}{{< readfile file="manifests/04.0/.gitlab-ci.yml" >}}{{< /highlight >}}

After committing the changes a new pipeline starts using the updated configuration.


Go to your GitLab project and check the pipelines under `CI/CD` --> `Pipelines`.

The Java 11 application is build using the [Gradle Build Tool](https://gradle.org/)

See the Gradle build that should succeed.

```s
Starting a Gradle Daemon (subsequent builds will be faster)
> Task :compileJava
> Task :processResources
> Task :classes
> Task :bootJarMainClassName
> Task :bootJar
> Task :jar
> Task :assemble
BUILD SUCCESSFUL in 39s
5 actionable tasks: 5 executed
Cleaning up file based variables
00:00
Job succeeded
```