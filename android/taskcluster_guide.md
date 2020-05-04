# Taskcluster guide

This guide is designed to help you get started with [Taskcluster](https://firefox-ci-tc.services.mozilla.com/), the Continuous Integration system we use, and to introduce you to some intermediate topics.
- [Getting Started](#getting-started)
- [HOWTOs](#howtos)

## Getting Started
Are you totally new to Taskcluster or Taskgraph? Check out this [3-minute-video](https://johanlorenzo.github.io/blog/2019/10/24/taskgraph-is-now-deployed-to-the-biggest-mozilla-mobile-projects.html). If you want an overview of Taskgraph, you can read the blog post attached to it.

If you have any questions regarding Taskcluster or Taskgraph, feel free to join #releaseduty-mobile on Mozilla's Slack instance.

## HOWTOs

### How do I test some changes I make under the `taskcluster/` folder?

The easy way: create a PR and you will get results in minutes. If you want to test your changes locally, have a look at the [README of Taskgraph](https://hg.mozilla.org/ci/taskgraph/file/tip/README.rst).

### How do I see test results?

* On PRs: the status badge will let you know whether it is green, running, or broken.
* On the master branch: Treeherder is a great tool to have an overview. Here are the links for:
  * [fenix](https://treeherder.mozilla.org/#/jobs?repo=fenix)
  * [android-components](https://treeherder.mozilla.org/#/jobs?repo=android-components)
  * [reference-browser](https://treeherder.mozilla.org/#/jobs?repo=reference-browser)
* More generally: the status badge attached to each commit on Github will point you to each task run. For instance, here is a link to one of Fenix's release branch: https://github.com/mozilla-mobile/fenix/commits/releases/v5.0

### How do I find the latest nightly?

If you are interested in just getting the latest APKs, use these links:
  * [fenix](https://firefox-ci-tc.services.mozilla.com/tasks/index/project.mobile.fenix.v2.nightly/latest)
  * [android-components](https://firefox-ci-tc.services.mozilla.com/tasks/index/mobile.v2.android-components.nightly.latest) (choose the component you are interested in)
  * [reference-browser](https://firefox-ci-tc.services.mozilla.com/tasks/index/project.mobile.reference-browser.v3.nightly/latest)

If you want to understand why something is wrong with nightly:
 1. click on one of the aforementioned Treeherder links
 1. type `nightly` in the search bar at the top right corner and press `Enter` => this will filter out any non-nightly job
 1. check if there are any non-green jobs. If none are displayed, do not hesitate to load more results by clicking on one of the `get next` buttons.

### How do I run a staging nightly/release on PRs?

It is easy! Just create a new file called `try_task_config.json` at the root of the repository and it will change what graph taskgraph generates. For instance

```json
{
    "parameters": {
        "optimize_target_tasks": true,
        "target_tasks_method": "nightly"
    },
    "version": 2
}
```

will generate a nightly graph on your PR. You can know what `target_tasks_method` to provide by looking at the `@_target_task()` sections in `target_tasks.py`. E.g: [target_tasks.py in Fenix](https://github.com/mozilla-mobile/fenix/blob/824dedb19588a9052b03ad162155c62ecd08e316/taskcluster/fenix_taskgraph/target_tasks.py#L29).

⚠️ Do not forget to remove this file before merging your patch.
