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

## Java commons

- Configure java 8 and related properties
- add shadow build by default
- add `gitCommit` property by fetching git sha
- process resources with tag replace (like maven)
- new task `addBuildProperties` that create a file
`<project-name>-build.properties` that contains project version, git sha,
timestamp, and, if available, the env variable `BUILD_ID`. The file is 
added to resources that will be included in the jar.
- new task `processDockerfile` that process any file matching 
`src/**/*Dockerfile` with tag replacing and put the processed 
version in `build/*Dockerfile`. This task is executed after `jar` task.

So you can put your Dockerfile in `src/` and write something like this:

```
... 
ADD build/libs/myproject-@version@-all.jar /myproject
ENV MYPROJECT_VERSION "@version@"
CMD exec java -cp /myproject/*jar myproject.Main
```

