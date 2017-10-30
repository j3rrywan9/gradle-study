# The Scala Plugin

The Scala plugin extends the Java plugin to add support for Scala projects.
It can deal with Scala code, mixed Scala and Java code, and even pure Java code (although we don’t necessarily recommend to use it for the latter).
The plugin supports joint compilation, which allows you to freely mix and match Scala and Java code, with dependencies in both directions.
For example, a Scala class can extend a Java class that in turn extends a Scala class.
This makes it possible to use the best language for the job, and to rewrite any class in the other language if needed.

## Usage

To use the Scala plugin, include the following in your build script:
```gradle
apply plugin: 'scala'
```

## Tasks

The Scala plugin adds the following tasks to the project.

## Project layout

### Changing the project layout

Just like the Java plugin, the Scala plugin allows you to configure custom locations for Scala production and test sources.

## Dependency management

Scala projects need to declare a `scala-library` dependency.
This dependency will then be used on compile and runtime class paths.
It will also be used to get hold of the Scala compiler and Scaladoc tool, respectively.

If Scala is used for production code, the `scala-library` dependency should be added to the compile configuration:
```gradle
dependencies {
  compile 'org.scala-lang:scala-library:2.11.8'
  testCompile 'org.scalatest:scalatest_2.11:3.0.0'
  testCompile 'junit:junit:4.12'
}
```

If Scala is only used for test code, the `scala-library` dependency should be added to the testCompile configuration:
```gradle
dependencies {
  testCompile "org.scala-lang:scala-library:2.12.4"
}
```

## Automatic configuration of scalaClasspath

The `ScalaCompile` and `ScalaDoc` tasks consume Scala code in two ways: on their `classpath`, and on their `scalaClasspath`.
The former is used to locate classes referenced by the source code, and will typically contain `scala-library` along with other libraries.
The latter is used to load and execute the Scala compiler and Scaladoc tool, respectively, and should only contain the `scala-compiler` library and its dependencies.

## Source set properties

The Scala plugin adds the following convention properties to each source set in the project.
You can use these properties in your build script as though they were properties of the source set object.

