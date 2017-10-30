# Dependency Management

## What is dependency management?

Very roughly, dependency management is made up of two pieces.
Firstly, Gradle needs to know about the things that your project needs to build or run, in order to find them.
We call these incoming files the *dependencies* of the project.
Secondly, Gradle needs to build and upload the things that your project produces.
We call these outgoing files the *publications* of the project.
Let’s look at these two pieces in more detail:

Most projects are not completely self-contained.
They need files built by other projects in order to be compiled or tested and so on.

These incoming files form the dependencies of the project.
Gradle allows you to tell it what the dependencies of your project are, so that it can take care of finding these dependencies, and making them available in your build.
The dependencies might need to be downloaded from a remote Maven or Ivy repository, or located in a local directory, or may need to be built by another project in the same multi-project build.
We call this process *dependency resolution*.

With Gradle, you simply declare the "names" of your dependencies, and other layers determine where to get those dependencies from.

Often, the dependencies of a project will themselves have dependencies.
For example, Hibernate core requires several other libraries to be present on the classpath with it runs.
So, when Gradle runs the tests for your project, it also needs to find these dependencies and make them available.
We call these *transitive dependencies*.

The main purpose of most projects is to build some files that are to be used outside the project.
For example, if your project produces a Java library, you need to build a jar, and maybe a source jar and some documentation, and publish them somewhere.

These outgoing files form the publications of the project.
Gradle also takes care of this important work for you.
You declare the publications of your project, and Gradle take care of building them and publishing them somewhere.
Exactly what “publishing” means depends on what you want to do.
You might want to copy the files to a local directory, or upload them to a remote Maven or Ivy repository.
Or you might use the files in another project in the same multi-project build.
We call this process *publication*.

## Declaring your dependencies

```gradle
apply plugin: 'java'

repositories {
  mavenCentral()
}

dependencies {
  compile group: 'org.hibernate', name: 'hibernate-core', version: '5.2.8.Final'
  testCompile group: 'junit', name: 'junit', version: '4.+'
}
```
This build script says a few things about the project.
It also tells Gradle to look in the Maven central repository for any dependencies that are required.

## Dependency configurations

A Configuration is a named set of dependencies and artifacts.
There are three main purposes for a Configuration:

* Declaring Dependencies

The plugin uses configurations to make it easy for build authors to declare what other subprojects or external artifacts are needed for various purposes during the execution of tasks defined by the plugin.

* Resolving Dependencies

The plugin uses configurations to find (and possibly download) inputs to to the tasks it defines.

* Exposing Artifacts for Consumption

The plugin uses configurations to define what artifacts it generates for other projects to consume.

With those three purposes in mind, let’s take a look at a few of the standard configurations defined by the Java Library Plugin.

* implementation

The dependencies required to compile the production source of the project, but which are not part of the api exposed by the project.
This configuration is an example of a configuration used for Declaring Dependencies.

* runtimeClasspath

The dependencies required by the production classes at runtime.
By default, this includes the dependencies declared in the api, implementation, and runtimeOnly configurations.
This configuration is an example of a configuration used for Resolving Dependencies, and as such, users should never declare dependencies directly in the runtimeClasspath configuration.

* apiElements

The dependencies which are part of this project’s externally consumable API as well as the classes which are defined in this project which should be consumable by other projects.
This configuration is an example of Exposing Artifacts for Consumption.

Various plugins add further standard configurations.
You can also define your own custom configurations to use in your build.

