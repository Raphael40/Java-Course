# Setup your machine

In this section:

-   What is a JDK?
-   How to install a JDK
-   Setup Intellij or Visual Studio Code

## What is a JDK?

In order to run Java code on our machine we need three things;

1. A `Java Virtual Machine` (**JVM**). The JVM is a runtime that hosts Java programs. It compiles Java into Java bytecode and then interprets the bytecode to run it on the underlying hardware platform. This conversion is why it is easy to run Java on Windows, Linux and iOS.
2. A `Java Runtime Environment` (**JRE**) which is a package of tools that runs Java programs by creating the JVMs and loading programs into them.
3. A `Java Development Kit` (**JDK**) which provides the tools necessary to write and develop Java programs that can be executed and run by the JRE and JVM. This includes a version of the language Java.

Conveniently, the JVM and JRE come as part of the JDK installation.

## Install a JDK

There are multiple JDK versions available. It is recommended to choose an LTS version (Long Term Support). Both 17 and 21 are LTS versions and both are suitable for this course. I have chosen 21.

To make things more confusing, there are also multiple distributions of each version. Popular ones include Oracle and Adoptium. Again, for this course it shouldn't really make a difference as the core features are the same.

You can download the Adoptium JDK [here](https://adoptium.net/en-GB/).

Or the Oracle JDK [here](https://www.oracle.com/java/technologies/downloads/#java21)

To verify the installation type `java --version` into your terminal:

```
java --version

>> openjdk 17.0.5 2022-10-18
>> OpenJDK Runtime Environment Temurin-17.0.5+8 (build 17.0.5+8)
>> OpenJDK 64-Bit Server VM Temurin-17.0.5+8 (build 17.0.5+8, mixed mode)
```

## IntelliJ Idea

IntelliJ is an integrated development environment designed spcifially for Java and Kotlin development created by JetBrains. Once you have installed it you can specify the location of the JDK you have downloaded and configure Intellij to run your Java code from inside InteliJ's own system.

Download and install the free version of IntelliJ from here: [https://www.jetbrains.com/idea/download/?section=windows](https://www.jetbrains.com/idea/download/?section=windows) (You may need to scroll down the page for the free, open source community version).

Once installed it will prompt you to connect your JDK (and you can even download a JDK through it if you haven't got one already).

<div style="text-align: center;" >
    <img src="images/jetbrains.svg" alt="vscode logo" width="200"/>
</div>

## Visual Studio Code

This course uses InttelliJ because configuration is significantly easier but it's good to know that if you ever find yourself using [VSCode](https://code.visualstudio.com/Download) over IntelliJ, you can install the [Extension Pack for Java VSCode](https://marketplace.visualstudio.com/items?itemName=vscjava.vscode-java-pack). Search for `vscjava.vscode-java-pack` in extensions to find it.

<div style="text-align: center;" >
    <img src="images/vscode.svg" alt="vscode logo" width="800"/>
</div>

---

At this point you should have a JDK installed (17 or 21) and IntelliJ.

In the next section we are going to run our first program and look at Java classes.

### References

https://whichjdk.com/

---

[back](../README.md) <span style="float: right;">[next](../03_java-fundamentals/README.md)</span>
