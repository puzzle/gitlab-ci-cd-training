---
title: "1. Getting started"
weight: 1
sectionnumber: 1
---

In this lab we're going to show you some basic GitLab CI concepts and commands.

For the lab we use the [example-spring-boot-helloworld](https://github.com/appuio/example-spring-boot-helloworld) Java project. We're going to show how to test, build and deploy this sample application within a GitLab CI pipeline.

The lab covers several topics such as:

* Build a Java application with maven
* Run Unit tests within your Pipeline
* Create Docker images
* Security features of GitLab
* How to extend your pipeline with Templates

To get started we create a [git](https://git-scm.com/) repository holding an example application.


## Task {{% param sectionnumber %}}.1: Open the GitLab Webconsole

The first thing, we're going to do is to login into the GitLab Webconsole and verify whether you have access to the correct group or not.

{{% alert title="Info" color="primary" %}}
Your Trainer will provide you the correct URL.
Also if you need help logging into GitLab ask the trainers for help.
{{% /alert %}}

Explore the different elements in the web console:

* the menu (top left corner)
  * click menu --> groups --> your groups to display the groups you're in.
* the projects view, what projects you have access to.
* your user profile (click on the avatar on the top right corner).


## Task {{% param sectionnumber %}}.2: Create the GitLab Project

Open GitLab click `New project/repository` --> `Import Project` and select **`Repo by URL`**.

{{% alert title="Hint" color="primary" %}}
You can also use the main navigation. `Menu` --> `Projects` --> `Create new project` --> `Import Project`
{{% /alert %}}

* **Git repository URL**: https://github.com/appuio/example-spring-boot-helloworld.git
* **Username & Password**: Leave empty
* **Project URL**: <!-- TODO -->
* **Visibility Level**: Private

![GitLab Import](../import_project.png)

And then click on `Create project` and wait until the Project is imported.

Next have a look at the newly created project and explore the repository view:

* Source Code
* Commits
* Project Settings
* ...


## Task {{% param sectionnumber %}}.3: Clone the Git repository

The new created repository is the base for the following labs. During the hands-on part, we'll create a CI/CD Pipeline step by step and we'll have to create and edit files in the repository.

Therefore, we recommend you clone the repository to your local machine and make the changes locally, then commit and push them like you learned in the git training yesterday.

1. Open the Repository / Project view and click the blue `Clone` button.
1. Copy the `Https` url to your Clipboard (eg. `https://gitlab.com/<group>/example-spring-boot-helloworld.git`)
1. Open your preferred command line (GitBash on Windows) and navigate into your projects directory and create a directory for the contents of this lab  for example `gitlabcicd-training`.
   * `mkdir ~/gitlabcicd-training`
1. Change into the newly created directory and clone your Repository
   * `cd ~/gitlabcicd-training`
   * `git clone https://gitlab.com/<group>/example-spring-boot-helloworld.git`


{{% alert title="Info" color="primary" %}}
If you have trouble logging in via command line, ask your Trainer for help.
{{% /alert %}}

As an alternative, you can also edit files in the repository directly via the GitLab web console.
Simply click the `Web IDE` button and commit your changes directly from the Web IDE.
