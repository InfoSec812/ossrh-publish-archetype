# OSSRH Publishing Archetype

## Overview

This archetype is for generating a Java project which can be easily published to Maven Central. Using this archetype
will generate a Maven POM file which will use the Sonatype Staging Plugin to publish this project to Maven Central. 
Following the instructions below will allow users of this archetype to easily publish their artifacts.

## Prerequisites
* [Maven](http://maven.apache.org/)
* [Java](http://java.net/)
* [GPG](https://www.gnupg.org/)

## Getting Started
1. Follow the [Initial Setup](http://central.sonatype.org/pages/ossrh-guide.html) guide for creating a user account
  1. Create an account on the [Sonatype JIRA site](https://issues.sonatype.org/secure/Signup!default.jspa)
  2. Create a [new ticket](https://issues.sonatype.org/secure/CreateIssue.jspa?issuetype=21&pid=10134) for your project on the Sonatype JIRA
  3. Wait for a RESOLVED response to your ticket
2. Add your JIRA credentials to your Maven settings.xml file

    ```xml
    <settings>
      <servers>
        <server>
          <id>ossrh</id>
          <username>YOUR OSSRH Username</username>
          <password>YOUR OSSRH Password</password>
        </server>
      </servers>
    </settings>
    ```
3. Generate your new project using this archetype:

    ```bash
    mvn archetype:generate -DarchetypeGroupId=com.zanclus -DarchetypeArtifactId=ossrh-publish-archetype
    ```
4. Modify the pom.xml from the generated project and ensure that you populate the required information as shown below:

    ```xml
    <name>YOUR PROJECT NAME</name>
    <description>YOUR PROJECT DESCRIPTION</description>
    <url>WEB SITE FOR YOUR PROJECT</url>
    <developers>
      <developer>
        <name>YOUR NAME</name>
        <!-- OPTIONAL:
        <url></url>
        <email></email>
        <id></id>
        <organization></organization>
        <organizationUrl></organizationUrl>
        <roles></roles>
        <timezone></timezone>
        <properties></properties>
        -->
      </developer>
    </developers>
    <scm>
      <url>YOUR PROJECT VERSION CONTROL URL</url>
      <developerConnection>scm:git:ssh://HOSTNAME/PROJECT.git</developerConnection>
    </scm>
    <licenses>
      <license>
        <distribution>repo</distribution>
        <name>YOUR PROJECT LICENSE NAME</name>
      </license>
    </licenses>
    ```
5. [Create a GPG key](http://central.sonatype.org/pages/working-with-pgp-signatures.html) for signing your artifacts

## Deploying A Snapshot Release
1. Add "-SNAPSHOT" to the end of the version in the Maven POM file
2. From the command-line, execute:

```bash
mvn clean deploy
```

## Deploying A Public Release
1. Ensure that the version in the POM file does not contain "-SNAPSHOT"
2. From the command-line, execute:

```bash
mvn clean deploy
```

## Troubleshooting

When/If you have a problem deploying to central, it is likely because you did not provide the required information
or artifacts. At a minimum, projects deployed to central MUST HAVE:

* JavaDoc AND Source JARs
* Artifact Signatures
* Correct Coordinates
* Project Name, Description and URL
* License Information
* Developer Information
* SCM Information
