# GITHUB ACTIONS

> platform to automate developer workflows.

> _CI/CD tool_ is one of many workflows.

## github

    - platform for open source projects.
    - this projects r publically available to use and contribute to the project.
        - can add new contributors to the project.
        - creats many pull requests.

## organizational tasks

- for example, you created a library to work with date and time in java.
- u have some contributors and users for that library,
- whenever user witness a bug/issue in the library, he can create an _New Issue_ for the same.
- so developer checks whether it is a _minor/major_ issue. developer can also assign the issue to one of the contributors.
- if a contributor fixes the issue, he creates a pull request from the library and pushes the fixed code to the library. thus developer can merge that changes to master branch. then it is ready for the next release.

- so bigger the project gets, more contributors, mroe users for our projects, more new issues, more pull requests.
- in such case, it is better to automate the task as much as possible. for that purpose the _github action_ was created.

## how github actions automate these workflows?.

- When something happens in/to our repository. We can configure automatic actions to get executed in response.
- here the things that happen in repo r called _github events_. for example, **creating pull request, adding contibutors, creating issues, merging branches.**
- so two basic steps to automate workflows.

  1. listening to github events.
  2. trigger workflow depending on the event happened.

for example, if an **Issue Created** which is an event. developer do actions sucha as

    > sort the issue,
    > label it,
    > assign it to the contributors,
    > reproduce the issue.

combination of these actions makes up a _workflow_.

![image](./screenshots/screen1.jpg)

this explains the basic concept of github actions.

---

## CI/CD with github actions

- why use CI/CD tool?

1. if v already hosts code to github, we can use same tool for CI/CD pipeline as well.
2. set up process for CI/CD pipeline is easy.

## Advantage of CI/CD pipeline in github actions

- Integration with other technolgies is important.

![image](./screenshots/screen2.jpg)

- so here v use combination of diff tools in the development process.

- so by using _ci/cd pipeline_, we dont have to install
  all these tools and do configurations for each in our machine.

- Instead, we ask for an environment with all these tools and configurations already available.

---

### Build a workflow for our java gradle application

- first navigate to **Actions** in remote repository.
- choose **Java With Gradle** option.
- Opens a _gradle.yml_ file which is the _workflow file_.

#### Syntax of Workflow file

```yaml
# This workflow will build a Java project with Gradle
# For more information see: https://help.github.com/actions/language-and-framework-guides/building-and-testing-java-with-gradle

name: Java CI with Gradle

on:
  push:
    branches: [master]
  pull_request:
    branches: [master]

jobs:
  build:
    runs-on: ubuntu-latest

    steps:
      - uses: actions/checkout@v2
      - name: Set up JDK 1.8
        uses: actions/setup-java@v1
        with:
          java-version: 1.8
      - name: Grant execute permission for gradlew
        run: chmod +x gradlew
      - name: Build with Gradle
        run: ./gradlew build
```

- **name**: name of workflow which is optional.
- **on**: contains events that triggers the workflow, eg: push, pull request
- **jobs**: actions to be executed when an event happens.

  - **steps**: run commands, set up tasks or run an action.
  - **uses** - selects an _action_. here _checkout_ is the action to be executed. _v2_ is its version.
    eg: _actions/checkout@v2_ . actions are available in the _uses attribute_

  (Checkout Action yaml file)[https://github.com/actions/checkout/blob/main/action.yml]

  - **uses: actions/setup-java@v1
    with:
    java-version: 1.8**

    > another action to setup java with version 1.8. thus v dont have to install/configure java in our machines.

  - **run** : attribute to run a linux command.
    Eg:
    1. **run: chmod +x gradlew** - change permission of gradle file.
    2. **run: ./gradlew build** - build gradle

> all these things are done in same environment.

- rename _gradle.yml_ file to any other name.
- then create a new branch - create a pull requet to master branch.
- click on _build_.

![](./screenshots/screen3.jpg)

1. **Set Up Job**: prepares the job environment.
2. **Post Run action**: things get cleaned up afetr all setup.

---

## where does these jobs gets executed?

1. workflows on github action gets executed on _github servers_. ie. workflows r managed by github.

2. whenever v create a workflow with a set of jobs. each job in that workflow runs in a fresh github server. so one job runs on a single server at a time. but these jobs runs in parallel by default. we can overwrite these by setting _needs_ attribute.

```yaml
jobs:
  build:
    runs-on: ubuntu-latest

    steps:
      - uses: actions/checkout@v2
      - name: Set up JDK 1.8
        uses: actions/setup-java@v1
        with:
          java-version: 1.8
      - name: Grant execute permission for gradlew
        run: chmod +x gradlew
      - name: Build with Gradle
        run: ./gradlew build

  publish:
    needs: build
```

- thus here _publish_ job waits for _build_ to finish execution. in _needs_ attribute we specify _build_ as value.
  thus overriding the default parallel running.

  **runs-on: ubuntu-latest** : github server runs on _Ubuntu_, _Windows_ and _macOS_. for example, if v ships our app to customers having all 3 OS. so first we can test all commits to master branch on all 3 OS.
  make some changes in _runs-on attribute_.

  ```yaml
  runs-on: ${{matrix.os}}
    strategy:
      matrix:
      os: [ubuntu-latest, windows-latest, macOS-latest]
  ```

  - then apply this change.
  - naivgate to github/workflows, open yml file.

---

## build docker image and push to private repo.

- next take java artifact file and build a docker image from it.
- first create an account in dockerhub.
- create a repository.
- to this repository, we push the docker image.
- 