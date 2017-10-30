# Build Script

## Projects and tasks

Everything in Gradle sits on top of two basic concepts: *projects* and *tasks*.

Every Gradle build is made up of one or more projects.
What a project represents depends on what it is that you are doing with Gradle.
A project does not necessarily represent a thing to be built.
It might represent a thing to be done, such as deploying your application to staging or production environments.
Don’t worry if this seems a little vague for now.
Gradle’s build-by-convention support adds a more concrete definition for what a project is.

Each project is made up of one or more tasks.
A task represents some atomic piece of work which a build performs.
This might be compiling some classes, creating a JAR, generating Javadoc, or publishing some archives to a repository.

## Hello world

You run a Gradle build using the `gradle` command.
The `gradle` command looks for a file called `build.gradle` in the current directory.
We call this `build.gradle` file a *build script*, although strictly speaking it is a build configuration script, as we will see later.
The build script defines a project and its tasks.

To try this out, create the following build script named build.gradle.
```gradle
task hello {
  doLast {
    println 'Hello world!'
  }
}
```

## Build scripts are code

Gradle's build scripts give you the full power of Groovy.
```gradle
task upper {
  doLast {
    String someString = 'mY_nAmE'
    println "Original: " + someString
    println "Upper case: " + someString.toUpperCase()
  }
}
```

## Task dependencies

You can declare tasks that depend on other tasks.
```gradle
task hello {
  doLast {
    println 'Hello, world!'
  }
}

task intro(dependsOn: hello) {
  doLast {
    println "I'm Gradle"
  }
}
```

## Dynamic tasks

The power of Groovy can be used for more than defining what a task does.
For example, you can also use it to dynamically create tasks.

## Manipulating existing tasks

## Default tasks

Gradle allows you to define one or more default tasks that are executed if no other tasks are specified.