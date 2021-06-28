---
title: "1. Getting started"
weight: 1
sectionnumber: 1
---

In this lab we're going to show you some basics GitLab CI concpets and commands.

For the lab we use the [example-spring-boot-helloworld](https://github.com/appuio/example-spring-boot-helloworld) Java project. We're going to show how to test, build and deploy this sample application within a GitLab CI pipeline.

The lab covers several topics such as:

* Build a Java application with maven
* Run Unit tests within your Pipeline
* Create Docker images
* Security features of GitLab
* How to extend your pipeline with Templates

To get started we create a [git](https://git-scm.com/) repository holding an example application.


## Task {{% param sectionnumber %}}.1: Create the GitLab Project

Open GitLab and navigate to `Project` 🠒 `Import Project` and select `Repo by URL`

* **Git repository URL**: https://github.com/appuio/example-spring-boot-helloworld.git
* **Username & Password**: Leave empty
* **Project URL**: <!-- TODO -->
* **Visibility Level**: Private

![Gitlab Import](../import_project.png)

And then click on `Create project`
