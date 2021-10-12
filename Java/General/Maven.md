# Maven

Maven automates tasks like downloading dependencies, putting additional jars on a class path, compiling source code into binary code, running tests, packaging compiled code into deployable artifacts (Ex: JAR, WAR, ZIP), and deploying these artifacts to an application server or repository.

## Why Maven?

* **Archetypes: **Templates supplied by maven that help avoid as much configuration as possible
* **Dependency Management: **Maven automatically updates, downloads, and validates the compatibility of dependencies as well as reporting their closures (transitive dependencies)
* **Isolation between dependencies and plugins: **Project dependencies are retrieved from the *dependency repositories* while plugin's dependencies are retrieved from the *plugin repositories*, which results in less conflicts when plugins start to download additional dependencies.
* **Central Repository System: **Project dependencies can be loaded from the local file system or public repositories, such as **Maven Central**

## Project Object Model

### POM

A Maven project's configuration is done via a *Project Object Model (POM)*, which is a `pom.xml` file. The POM describes the project, manages dependencies, and configures plugins for building the software.

### Project identifiers

**Coordinates: **A set of identifiers used to uniquely identify a project and specify ow the project artifact should be packaged

#### Identifiers

* **`groudId`:** Unique name of the company or group that created the project (`com.springframework`, `org.springframework`)
* **`artifactId`:** Unique name of the project
* **`version`:** Version of the project (Ex: `0.1.SNAPSHOT`, `1.0.RELEASE`)
* **`packaging`:** Packaging method (Ex: WAR, JAR, ZIP)

### Dependencies

The external libraries that a project uses. Maven ensures that the libraries are automatically downloaded from a central repository so they don't have to be stored locally.

#### Benefits of Dependencies:

* Less storage used by reducing number of downloads off remote repositories
* Makes checking out a project quicker
* Provides an effective platform for exchanging binary artifacts within an organization and beyond without the need for building artifact from source every time

#### Example

```
<dependency>
    <groupId>org.springframework</groudId>
    <artifactId>spring-core</artifactId>
    <version>4.3.5.RELEASE</version>
</dependency>
```

### Repository

Used to hold build artifacts and dependencies. The default local repository is in the `.m2/repository` folder.

If an artifact or plugin is available in the local repository, Maven uses it. Otherwise, it is downloaded from a central repository and stored in the local repository.  **Maven Central** is the default central repository.

Some libraries are not available at the central repository but at another one. For those libraries, you need to provide the URL to the alternate repository in the POM:

```
<repositories>
    <repository>
    	<id>JBoss repository</id>
	    <url>repository.jboss.org/nexus/content			/groups/public/</url>
    </repository>
</repositories>
    
```

### Properties

Custom properties that make the POM file easier to read and maintain. 

Maven properties are value-placeholders and are accusable anywhere in the `pom.xml` file using `${`*name*`}`. 

```
<properties>
    <spring.version>4.3.5.RELEASE</spring.version>
</properties>

<dependencies>
    <dependency>
        <groupId>org.springframework</groupId>
        <artifactId>spring-core</artifactId>
        <version>${spring.version}</version>
    </dependency>
    <dependency>
        <groupId>org.springframework</groupId>
        <artifactId>spring-context</artifactId>
        <version>${spring.version}</version>
    </dependency>
</dependencies>
```

### Build

Provides information about the default maven goal, the directory for the compiled project, and final name of the application

The default output folder for the compiled artifacts is named *target*, and the final name of the packaged artifact consist of the *`artifactId`* and the *`version`*.

```
<build>
    <defaultGoal>install</defaultGoal>
    <directory>${basedir}/target</directory>
    <finalName>${artifactId}-${version}</finalName>
    <filters>
      <filter>filters/filter1.properties</filter>
    </filters>
    //...
</build>
```

### Profiles

A set of configuration values. Using profiles, you can customize the build for different environments such as Production/Test/Development

```
<profiles>
    <profile>
        <id>production</id>
        <build>
            <plugins>
                <plugin>
                //...
                </plugin>
            </plugins>
        </build>
    </profile>
    <profile>
        <id>development</id>
        <activation>
            <activeByDefault>true</activeByDefault>
        </activation>
        <build>
            <plugins>
                <plugin>
                //...
                </plugin>
            </plugins>
        </build>
     </profile>
 </profiles>
```

## Maven Build Lifecycles

Each Maven build follows a specified lifecycle.

The lifecycle phases are:

* **validate: **checks the correctness of the project
* **compile: **compiles the provided source code into binary artifacts
* **test: **executes unit tests
* **package: **packages compiled code into an archive file
* **integration test: **executes additional tests, which require the packaging
* **verify: **checks if the package is valid
* **install: **installs the package file into the local Maven repository
* **deploy: **deploys the package file to a remote server or repository

### Plugins and Goals

A Maven plugin is a collection of one or more goals. Goals are executed in phases, which helps to determine the order in which the goals are executed.

To go through any of the processes, the command `mvn <phase>` is used.

Goals provided by plugins can be associated with different phases of the lifecycle

