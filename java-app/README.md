# Lab 1: Building and Packaging Java Applications with Gradle

This lab demonstrates how to build, test, and run a Java application using Gradle.

## Prerequisites

- **Java 11 or 17** (Java 11 recommended for compatibility)
- **Git** (to clone the repository)
- **Internet connection** (to download dependencies)

## Complete Automation Script

Run all steps (install Gradle, clone, test, build, run, verify) using the script below:

```bash
# Install Java 11 if needed
    sudo apt update && sudo apt install openjdk-11-jdk -y
````

##### Install Gradle (snap, latest version)
````bash
sudo snap install gradle --classic
export PATH="/snap/bin:$PATH"
```````
##### Clone the repository
````bash

git clone https://github.com/Ibrahim-Adel15/build1.git
cd build1
````
##### Run unit tests
````bash
gradle test
`````
##### Build the JAR artifact
````bash
gradle build
`````

##### Run the application
````bash
java -jar build/libs/ivolve-app.jar
````

# Verify it worked
![](Screenshot%202026-04-13%20212945.png)