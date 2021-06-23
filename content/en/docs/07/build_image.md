---
title: "7. Container Image build"
weight: 7
sectionnumber: 7
---

This lab covers packaging the application by building a Container Image.


## Task {{% param sectionnumber %}}.1: Create Image build stage

Image builds are done inside a package stage.

Create a new job with the following configuration that runs inside the new `package` stage:

* job name: `build_image`
* before_script: `docker info`
* script:
  ```yaml
  - docker build --no-cache -t $IMAGE_NAME .
  - IMAGE_PATH=$IMAGE_HOST/$IMAGE_REPOSITORY/$IMAGE_NAME:${CI_COMMIT_SHA:0:8}
  - echo "docker image path is - $IMAGE_PATH"
  - docker tag $IMAGE_NAME $IMAGE_PATH
  # - docker push $IMAGE_PATH
  ```

<!-- TODO 

* [ ] mobi specific tags!!

  tags:
    - mobiliar
    - build

-->

Did you see the required variables inside the script? Add the following variables:

* IMAGE_HOST: 'quay.io'
* IMAGE_REPOSITORY: 'puzzle'
* IMAGE_NAME: 'example-spring-boot'

{{% details title="job hint" mode-switcher="normalexpertmode" %}}

{{< highlight yaml "hl_lines=33-45" >}}{{< readfile file="manifests/07.0/.gitlab-ci.yml" >}}{{< /highlight >}}

{{% /details %}}


## Task {{% param sectionnumber %}}.2: Check the pipeline

Go to your GitLab project and check the pipelines under `CI/CD` 🠒 `Pipelines`.

Check that the image build job was successful.

<!-- TODO 

* [ ] docker login und push als Theorie erklären?

-->
