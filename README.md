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

time: 12:30
