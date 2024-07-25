# Setup your machine

In this lesson:

-   What is a JDK?
-   How to install a JDK
-   Setup Intellij

## What is a JDK?

To run Java code on our machine, we need three things;

1. A `Java Virtual Machine` (**JVM**) to host Java programs. It compiles Java into Java bytecode and then interprets the bytecode to run it on the underlying hardware platform. This conversion is why running Java on Windows, Linux and iOS is easy.
2. A `Java Runtime Environment` (**JRE**) to run Java programs by creating the JVM and loading programs into it.
3. A `Java Development Kit` (**JDK**). This provides the tools necessary to write and develop Java programs that can be executed and run by the JRE and JVM. It includes a version of the language Java.

Conveniently, the JVM and JRE come as part of the JDK installation.

## Install a JDK

Multiple JDK versions are available. It is recommended that you choose an LTS version (Long Term Support). Both 17 and 21 are LTS versions, and both are suitable for this course. I have chosen 21.

To make things more confusing, each version has multiple distributions. Popular ones include Oracle and Adoptium. Your choice shouldn't matter for this course, as the core features are the same.

You can download the Adoptium JDK [here](https://adoptium.net/en-GB/).

Or the Oracle JDK [here](https://www.oracle.com/java/technologies/downloads/#java21).

Feel free to learn more about JDKs and their distributions [here](https://whichjdk.com/). I used the Temurin distribution.

When you have installed your JDK you can verify the installation type `java --version` into your terminal:

```
java --version

>> openjdk 17.0.5 2022-10-18
>> OpenJDK Runtime Environment Temurin-17.0.5+8 (build 17.0.5+8)
>> OpenJDK 64-Bit Server VM Temurin-17.0.5+8 (build 17.0.5+8, mixed mode)
```

## IntelliJ Idea

IntelliJ is an integrated development environment created by JetBrains specifically for Java and Kotlin development. Once you have installed it, you can specify the location of the JDK you have downloaded and configure IntelliJ to run your Java code from inside IntelliJ's own system. You can also manage and install new JDKs onto your machine from IntelliJ.

Download and install the free version of IntelliJ from here: [https://www.jetbrains.com/idea/download/?section=windows](https://www.jetbrains.com/idea/download/?section=windows) (You may need to scroll down the page for the free, open source community version).

<div style="text-align: center;" >
    <img src="images/jetbrains.svg" alt="vscode logo" width="200"/>
</div>

## Visual Studio Code

This course uses InttelliJ and assumes that you are. You can still develop Java apps with [VSCode](https://code.visualstudio.com/Download) but you will need to install the [Extension Pack for Java VSCode](https://marketplace.visualstudio.com/items?itemName=vscjava.vscode-java-pack). Search for `vscjava.vscode-java-pack` in extensions to find it.

<div style="text-align: center;" >
    <img src="images/vscode.svg" alt="vscode logo" width="800"/>
</div>

---

This is a link to the support repo. It contains both starter code for each lesson and the completed code for each lesson. This code is stored on different branches and I will show you how to swap between the branches in the next lesson.
https://github.com/Raphael40/Java-Course-Support-Repo

[Click here if you are not sure how to clone a repository](https://docs.github.com/en/repositories/creating-and-managing-repositories/cloning-a-repository?platform=windows)

Once cloned, open the support repo in IntelliJ.

At this point you should see a README.md file which contains some info on the branches in the repository.

In the next section we are going to run our first program and look at Java classes.

### References

https://whichjdk.com/

---

[back](../README.md) <span style="float: right;">[next](../03_java-fundamentals/README.md)</span>
