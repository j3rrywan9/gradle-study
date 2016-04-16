# Learning Gradle

## Installation
You can download one of the Gradle distributions from the Gradle website.

For running Gradle, firstly add the environment variable **GRADLE_HOME**. This should point to the unpacked files from the Gradle website. Next add **$GRADLE_HOME/bin** to your PATH environment variable.

You run Gradle via the **gradle** command. To check if Gradle is properly installed just type **gradle -v**. The output shows the Gradle version and also the local environment configuration.

## Using the Gradle
When you run the **gradle** command, it looks for a build file in the current directory. You can use the **-b** option to select another build file.

## The Gradle Wrapper
If a Gradle project has set up the Wrapper (and we recommand all projects do so), you can execute the build using one of the following commands from the root of the project:
* **./gradlew \<task\>**
* **gradle \<task\>**

Each Wrapper is tied to a specific version of Gradle, so when you first run one of the commands above for a given Gradle version, it will download the corresponding Gradle distribution and use it to execute the build.

Not only does this mean that you don't have to manually install Gradle yourself, but you are also sure to use the version of Gradle that the build is designed for.

The Wrapper is something you **should** check into version control. By distributing the Wrapper with your project, anyone can work with it without needing to install Gradle beforehand.

You install the Wrapper into your project by running the wrapper task. This task is always available, even if you don't add it to your build. To specify a Gradle version use **--gradle-version** on the command line.
