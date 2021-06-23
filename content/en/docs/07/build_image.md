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

  This Job builds the container image defined by the Dockerfile in your source code. In the real world, the resulting container image would now be pushed into a container registry for simplicity reasons, whe skip this step in our pipeline.

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

{{% details title="solution" mode-switcher="normalexpertmode" %}}

The new stage is defined at the end of our `.gitlab-ci.yml`, we also need to add the package stage to the stage list and define the new variables.

{{< highlight yaml "hl_lines=5 10-12 35-45" >}}{{< readfile file="manifests/07.0/.gitlab-ci.yml" >}}{{< /highlight >}}

{{% /details %}}

{{% alert title="Warning" color="secondary" %}}
As mentioned in the variables Lab sensitive Data like for example `DOCKER_USERNAME` and `DOCKER_PASSWORD` should never be stored as plain variable within a pipeline definition. Such variables can be defined on Projects, Groups and Instances in the Gitlab Webconsole (eg. Project Settings --> CICD --> Variables). During a pipeline run Gitlab will take care that sensitive data never shows up in logs and can be leaked in such a way.
{{% /alert %}}


## Task {{% param sectionnumber %}}.2: Check the pipeline

Go to your GitLab project and check the pipelines under `CI/CD` 🠒 `Pipelines`.

Check that the image build job was successful.

<!-- TODO 

* [ ] docker login und push als Theorie erklären?

-->
