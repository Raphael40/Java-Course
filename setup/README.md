# Get up and running

## Install a JDK

In order to develop apps with Java we need three things;

1. A Java code compiler called the 'Java Virtual Machine'. The JVM is a runtime that hosts Java programs. It works by compiling Java into Java bytecode and then interpreting the bytecode to run it on the underlying hardware platform. This is why it is easy to run Java on Windows, Linux and iOS.
2. A 'Java Runtime Environment' (JRE) which is a package of tools that runs Java programs by creating the JVMs and loading programs into them.
3. A 'Java Development Kit' (JDK) which provides the tools necessary to write/develop the Java programs that can be executed and run by the JRE and JVM. This includes a version of the language Java.

Luckily, since being able to run Java programs is a part of being able to develop a Java program, the JVM and JRE come as part of the JDk so we only need to install a JDK.

In this course we are going to use JDK 17 because it is the most recent version with long term support.
You can download it for MacOS, Linux, and Windows [here](https://www.oracle.com/java/technologies/downloads/#java17)
If you have a package manager like Homebrew you can use it to easily install a JDK.

To verify the installation type this:

```
java --version

// which should yeild an output like this:

openjdk 17.0.5 2022-10-18
OpenJDK Runtime Environment Temurin-17.0.5+8 (build 17.0.5+8)
OpenJDK 64-Bit Server VM Temurin-17.0.5+8 (build 17.0.5+8, mixed mode)
```

Next we want to install IntelliJ

## Installing IntelliJ

IntelliJ is an integrated development environment like Visual Studio Code but designed spcifially for Java development. Once you have installed it you can specify the location of the JDK you have downloaded and configure Intellij to run your Java code from inside InteliJ.

Download and install the free version of IntelliJ from here: [https://www.jetbrains.com/idea/download/?section=windows](https://www.jetbrains.com/idea/download/?section=windows)

You now have two ways to run your Java files. Directly in the terminal with the command:

```
java yourFile.java
```

Or run your code in IntelliJ by selecting the green arrow, printing the output in the IntelliJ tool bar.

## In the next step we are going to make some files and look at the basic syntax of Java

[next](../java-fundamentals/README.MD)

---

## [back](../README.md)
