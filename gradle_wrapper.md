# The Gradle Wrapper

Most tools require installation on your computer before you can use them.
If the installation is easy, you may think that’s fine.
But it can be an unnecessary burden on the users of the build.
Equally importantly, will the user install the right version of the tool for the build?
What if they’re building an old version of the software?

The Gradle Wrapper (henceforth referred to as the “Wrapper”) solves both these problems and is the preferred way of starting a Gradle build.

## Executing a build with the Wrapper

If a Gradle project has set up the Wrapper (and we recommend all projects do so), you can execute the build using one of the following commands from the root of the project:
* **./gradlew \<task\>**
* **gradle \<task\>**

Each Wrapper is tied to a specific version of Gradle, so when you first run one of the commands above for a given Gradle version, it will download the corresponding Gradle distribution and use it to execute the build.

Not only does this mean that you don't have to manually install Gradle yourself, but you are also sure to use the version of Gradle that the build is designed for.
This makes your historical builds more reliable.

## Adding the Wrapper to a project

The Wrapper is something you **should** check into version control.
By distributing the Wrapper with your project, anyone can work with it without needing to install Gradle beforehand.

You install the Wrapper into your project by running the wrapper task.
This task is always available, even if you don't add it to your build.
To specify a Gradle version use `--gradle-version` on the command line.
By default, the Wrapper will use a bin distribution.
