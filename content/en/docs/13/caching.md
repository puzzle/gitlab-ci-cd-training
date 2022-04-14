---
title: "13. Caching & Caching policies"
weight: 13
sectionnumber: 13
---

A delivery pipeline normally works with the method:
* build
* test
* publish

In Gitlab CI every job is indipendent from each other. This means build artifacts are not accessable between jobs.
How to you overcome the necessity of building the artifact or downloading metadata in every job of the `.gitlab-ci.yml`?

GitLab CI offers the concept of caching. 

{{% alert color="primary" %}}
**GitLab References**

[GitLab caching](https://docs.gitlab.com/ee/ci/caching/)
[GitLab caching - lifecycles](https://docs.gitlab.com/ee/ci/caching/#common-use-cases-for-caches/)

{{% /alert %}}

This option does save defined directory in you workspace and make the accessable for other jobs.

Example of a cache definition:

```yaml
cache:
  key: "persistent-files"
  paths:
    - build/
    - .cache/
```

In the example a cache named *persistent-files* is created and it contains files from the build and .cache directories.
GitLab now creates a persistent-files.zip file and uploads it to a save location. Every job that refers to the cache-key *persistent-files* will now download the zip file and extracts the content to the project directory.
altogether: with the keyword `key` you can define the life cycle of a cache.

## {{% param sectionnumber %}}.1: create cache in build and test jobs

In this task you have to create a cache that can be used during the build of the current commit.
* create cache in build_application and test_application job with the commit id as the cache-key

Edit the `.gitlab-ci.yml`, commit and push your changes and then verify the output of the pipeline run.

## Solution

Updated `.gitlab-ci.yml` file for this lab:

{{% details title="show solution" mode-switcher="normalexpertmode" %}}

{{< highlight yaml "hl_lines=38-42 53-57" >}}{{< readfile file="manifests/13.0/.gitlab-ci.yml" >}}{{< /highlight >}}

{{% /details %}}


## {{% param sectionnumber %}}.1: cache policies

If you control the output of your build_application