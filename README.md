# Learning Gradle

## Installation

You can download one of the Gradle distributions from the Gradle website.

For running Gradle, firstly add the environment variable **GRADLE_HOME**.
This should point to the unpacked files from the Gradle website.
Next add **$GRADLE_HOME/bin** to your PATH environment variable.

You run Gradle via the `gradle` command.
To check if Gradle is properly installed just type `gradle -v`.
The output shows the Gradle version and also the local environment configuration.

## Using the Gradle

When you run the `gradle` command, it looks for a build file in the current directory.
You can use the `-b` option to select another build file.

## [The Gradle Wrapper](gradle_wrapper.md)

## [Dependency Management](dependency_management.md)

## [Build Script](build_script.md)

## Build Init Plugin

The Gradle Build Init plugin can be used to bootstrap the process of creating a new Gradle build.
It supports creating brand new projects of different types as well as converting existing builds (e.g. an Apache Maven build) to be Gradle builds.

## Writing Build Scripts

### The Gradle build language

Gradle provides a DSL for describing builds.
This build language is based on Groovy, with some additions to make it easier to describe a build.

### The Project API

For each project in the build, Gradle creates an object of type **Project** and associates this Project object with the build script.
As the build script executes, it configures this Project object:
* Any method you call in your build script which is not defined in the build script, is delegated to the Project object.
* Any property you access in your build script which is not defined in the build script, is delegated to the Project object.

### The Script API

### Declaring variables

#### Local variables

#### Extra properties

All enhanced objects in Gradle's domain model can hold extra user-defined properties.
Extra properties can be added, read and set via the owning object's **ext** property.
Alternatively, an **ext** block can be used to add multiple properties at once.

### More about Tasks

#### Defining tasks

#### Locating tasks

#### Configuring tasks

#### Adding dependencies to a task

## Dependency Management

### Repositories

Gradle repository management, based on Apache Ivy, gives you a lot of freedom regarding repository layout and retrieval policies.
Additionally Gradle provides various convenience method to add pre-configured repositories.

#### Maven central repository

To add the [central Maven 2 repository](http://repo1.maven.org/maven2) simply add this to your build script:
```gradle
repositories {
	mavenCentral()
}
```

#### Maven JCenter repository

#### Maven repositories

For adding a custom Maven repository you can do:
```gradle
repositories {
	maven {
		url "http://repo.mycompany.com/maven2"
	}
}
```

## Java Quickstart

Gradle solves this problem through the use of plugins.
A plugin is an extension to Gradle which configures your project in some way, typically by adding some pre-configured tasks which together do something useful.
Gradle ships with a number of plugins, and you can easily write your own and share them with others.
One such plugin is the Java plugin.
This plugin adds some tasks to your project which will compile and unit test your Java source code, and bundle it into a JAR file.

### A basic Java project

To use the Java plugin, add the following to your build script:
```gradle
apply plugin: 'java'
```
This is all you need to define a Java project.
This will apply the Java plugin to your project, which adds a number of tasks to your project.

## The Java Plugin

### Source sets

The Java plugin introduces the concept of a source set.
A source set is simply a group of source files which are compiled and executed together.
These source files may include Java source files and resource files.
Other plugins add the ability to include Groovy and Scala source files in a source set.

One use for source sets is to group source files into logical groups which describe their purpose.

The Java plugin defines two standard source sets, called **main** and **test**.

### Tasks

The Java plugin adds a number of tasks to your project, as shown below.
* **classes** Depends on the **compileJava** task and the **processResources** task.
Assembles the production classes and resources directories.

### Project layout

## Groovy Quickstart

### A basic Groovy project

To use the Groovy plugin, add the following to your build script:
```gradle
apply plugin: 'groovy'
```
This will also apply the Java plugin to the project, if it has not already been applied.
The Groovy plugin extends the **compile** task to look for source files in directory **src/main/groovy**, and the **compileTest** task to look for test source files in directory **src/test/groovy**.

To use the Groovy compilation tasks, you must also declare the Groovy version to use and where to find the Groovy libraries.
You do this by adding a dependency to the groovy configuration.
The **compile** configuration inherits this dependency, so the Groovy libraries will be included in classpath when compiling Groovy and Java source.

## The IDEA Plugin

The IDEA plugin generates files that are used by IntelliJ IDEA, thus making it possible to open the project from IDEA (File - Open Project).
Both external dependencies (including associated source and Javadoc files) and project dependencies are considered.

### Usage

To use the IDEA plugin, include this in your build script:
```gradle
apply plugin: 'idea'
```
The IDEA plugin adds a number of tasks to your project.
The main tasks that you will use are the **idea** and **cleanIdea** tasks.

### Tasks

The IDEA plugin adds the tasks shown below to a project.
Notice that the **clean** task does not depend on the **cleanIdeaWorkspace** task.

### Configuration

[IdeaProject](https://docs.gradle.org/current/dsl/org.gradle.plugins.ide.idea.model.IdeaProject.html)

Allows configuring project information

[IdeaModule](https://docs.gradle.org/current/dsl/org.gradle.plugins.ide.idea.model.IdeaModule.html)

Allows configuring module information

