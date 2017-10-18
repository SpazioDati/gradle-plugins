# Spaziodati's gradle-plugins
Gradle script plugins

## Usage

Add to your `build.gradle`

```
buildscript {
    apply from: 'https://raw.githubusercontent.com/SpazioDati/gradle-plugins/master/<name>.deps.gradle', to: buildscript
}
apply from: 'https://raw.githubusercontent.com/SpazioDati/gradle-plugins/master/<name>.gradle'
```

## Commons
- add `gitCommit` property by fetching git sha
- new task `processDockerfile` that process any file matching
`src/**/*Dockerfile` with tag replacing and put the processed
version in `build/*Dockerfile`. This task is executed after `processResources` task.


## Java commons

- Configure java 8 and related properties
- add shadow build by default
- process resources with tag replace (like maven)
- new task `addBuildProperties` that create a file
`<project-name>-build.properties` that contains project version, git sha,
timestamp, and, if available, the env variable `BUILD_ID`. The file is
added to resources that will be included in the jar.

So you can put your Dockerfile in `src/` and write something like this:

```
...
ADD build/libs/myproject-@version@-all.jar /myproject
ENV MYPROJECT_VERSION "@version@"
CMD exec java -cp /myproject/*jar myproject.Main
```

## Release

It uses and pre-configures the release plugin
[net.researchgate:gradle-release](https://github.com/researchgate/gradle-release)

### Prerequisites

  - Your develop and master branches are up-to-date (git pull)
  - You are on develop branch
  - Your git account can push to the repo

### New release

`gradle release`

then you will be asked for the new release version and the new version for the develop branch
