---
title: "7. Container Image build"
weight: 7
sectionnumber: 7
---

This lab covers packaging the application by building a Container Image.


## Task {{% param sectionnumber %}}.1: Create Image build stage

Image builds are done inside a package stage.

Create a new job with the following configuration which runs inside the new `package` stage:

* job name: `build_image`
* image: `diemobiliar.azurecr.io/dlp-cicd-dockercli-image:254`
* Add a tag block to select a suitable Runner
  ```yaml
  tags:
    - build
    - mobiliar
  ```
* Add a service block to enable the Docker in Docker builds
  ```yaml
  services:
    - docker:dind
  ```
* before_script: `docker info`
* script:
  ```yaml
  - docker build --no-cache -t $IMAGE_NAME .
  - IMAGE_PATH=$IMAGE_HOST/$IMAGE_REPOSITORY/$IMAGE_NAME:${CI_COMMIT_SHA:0:8}
  - echo "docker image path is - $IMAGE_PATH"
  - docker tag $IMAGE_NAME $IMAGE_PATH
  # - docker login -u ${DOCKER_USERNAME} -p ${DOCKER_PASSWORD} ${IMAGE_HOST}
  # - docker push $IMAGE_PATH
  ```


<!-- TODO
Mobi builder Image hier und im .gitlab-ci.yml raus nehmen und vom Teacher angeben lassen.
-->

  This Job builds the container image defined by the Dockerfile in your source code. In the real world, the resulting container image would now be pushed into a container registry for simplicity reasons, we skip this step in our pipeline.

<!-- TODO

* [ ] mobi specific tags!!

  tags:
    - mobiliar
    - build
* [ ] Bestpractices secrets anhand DOCKER_USERNAME und DOCKER_PASSWORT erklären, wo abspeichern, damit die nicht ausgelesen werden können. Variables

-->

Did you see the required variables inside the script? Also add the following variables to the variables block:

* IMAGE_HOST: 'quay.io'
* IMAGE_REPOSITORY: 'puzzle'
* IMAGE_NAME: 'example-spring-boot'

{{< details title="solution" mode-switcher="normalexpertmode" >}}

The new stage is defined at the end of our `.gitlab-ci.yml`, we also need to add the package stage to the stage list and define the new variables.

{{% readAndHighlight file="/manifests/07.0/.gitlab-ci.yml" code="true" lang="yaml" highlight="hl_lines=5 10-12 39-53" %}}

{{< /details >}}

{{% alert title="Warning" color="secondary" %}}
As mentioned in the variables Lab sensitive data, for example `DOCKER_USERNAME` and `DOCKER_PASSWORD` should never be stored as plain variable within a pipeline definition. Such variables can be defined on Projects, Groups and Instances in the Gitlab Web Console (e.g. Project Settings --> CI/CD --> Variables). During a pipeline run Gitlab will take care that sensitive data never shows up in logs and can be leaked in such a way.
{{% /alert %}}


## Task {{% param sectionnumber %}}.2: Check the pipeline

Go to your GitLab project and check the pipelines under `CI/CD` --> `Pipelines`.

Check that the image build job was successful.

<!-- TODO

* [ ] docker login und push als Theorie erklären?

-->
