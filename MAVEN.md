* Maven is a tool that can be used to create and manage any Java-based project.

* It is used for project build, as well as for managing dependencies and documentation.

* When you need a quick way to generate documentation from source code, this is the tool you use. It helps in compiling source code, and then packaging it into JAR or ZIP files.

* POM - Project Object Model

Elements of pom.xml file:

1. Project:
	=>The root element of the pom.xml file is the project.

2. ModelVersion:
	=>It identifies which version of the POM model you're working with.For Maven 2 and Maven 3 use version 4.0.0.

3. GroupId:
	=>It is the project group's identifier. It is unique, and you will most likely use a group ID that is similar to the project's root Java package name.

4. ArtifactId:
	=>It is used for naming the project you're working on.

5. version:
	=>The version number of the project is contained in the version element. If your project has been released in multiple versions, it is 
helpful to list the versions.

Other Pom.xml File Elements

6. Dependencies:
	=>This element is used to establish a project's dependency list.

7. Dependency:
	=>Dependency is used inside the dependencies tag to define a dependency. The groupId, artifactId, and version of each dependency are 
listed.

8. Name:
	=>This element is used to give our Maven project a name.

9. Scope:
	=>This element is used to specify the scope of this maven project, which can include compile, runtime, test, among other things.

10. Packaging:
	=>The packaging element is used to package our project into a JAR, WAR, and other output formats.

* Super POM: This is Maven�s default POM. All the POMs inherit from a parent or default.

core concepts of Maven :

1. POM Files:
	=> Project Object Model (POM) files are XML files.
	=> Include information about the project and configuration used by Maven to construct the project, such as dependencies, source directory, plugin, goals, and so on.
	=> To complete its configuration and functions, Maven reads the pom.xml file.

2. Dependencies and Repositories:
	=> Repositories are folders containing bundled JAR files, and dependencies are external Java libraries necessary for Project. 
	=> Maven retrieves dependencies from a central Maven repository and places them in your local repository if they aren't found in the local
          Maven repository.

3. Build Life Cycles, Phases, and Goals:
	=>A build life cycle is made up of a series of build phases, each of which contains a set of goals. 

4. Build Profiles:
	=>Build Profiles are a set of configuration parameters that allow you to build your project using a variety of setups.

5. Build Plugins: 
	=>Build Plugins are used to accomplish a certain task.A plugin can be added to the POM file. Maven comes with various pre-installed plugins, but you can also write your own in Java.

* Types of Maven repositories:
	1. Local repository:
		=> Local repository is a directory on the developer's device. 
		=> The local repository contains all of Maven's dependencies. 
		=> Even though several projects rely on dependencies, Maven only needs to download them once.

	2. Central Repository:
		=> The Maven community has built the central Maven repository. 
		=> Maven searches this central repository for any dependencies that aren't available in your local repository. 
		=> The dependencies are subsequently downloaded into your local repository by Maven.
	
	3. Remote Repository:
		=> Maven may download dependencies from a remote repository hosted on a web server.
		=> It is frequently used to host internal organization projects. 
		=> The dependencies are subsequently downloaded into your local repository by Maven.

     -> Maven scans these repositories for dependencies. Maven looks in the Local repository first, 
	then the Central repository, and finally the Remote repository if the Remote repository is 
	defined in the POM.

* Phases of the default life cycle:

	1.Validate: 
		=> Make sure the project is correct and that you have all of the necessary information.

	2.Test: 
		=> Test the compiled source code using an appropriate unit testing framework. These tests should not demand that the code be 
                  packed or deployed; instead, take the compiled code and package it in a manner that can be distributed, such as a JAR.

	3.Compile: 
		=> Compile the project's source code.

	4.Verify: 
		=> Perform any necessary checks on integration test findings to ensure that quality criteria are met.

	5.Install: 
		=> Adds the package to the local repository, allowing it to be used as a dependency in other projects.
	6.Deploy: 
		=> Copies the entire package to the remote repository for sharing with other developers and organizations, and is done in the 
                   build environment.

* Built-in build life cycles:

	1.Clean: 
		=>The clean lifecycle is in charge of project cleaning.

	2.Default: 
		=>The project deployment is handled by the default lifecycle.

	3.Site: 
		=>The creation of the project's site documentation is referred to as the site lifecycle.
	
* Maven Plugins are used for:

	=>Creating JAR files.
	=>Creating WAR files.
	=>Compiling the source code files.
	=>Unit testing of the code.
	=>Creating the project documentation.
	=>Creating project reports.

* Maven plugins are divided into two categories:

	1. Build plugins:  
		=>These plugins are used throughout the build process and are configured in the pom.xml file's <build/> element.
	2. Reporting plugins: 
		=>These plugins are configured in the pom.xml's <reporting/> element and run during stage generation.

* Maven's inheritance order:

	-->Settings
	-->CLI parameters
	-->Parent POM
	-->Project POM

--> A snapshot is a specific version of a project that shows the most recent development copy of the project being worked on.

--> Maven saves all of the JARs, dependency files, and other things it downloads in the Maven local repository. All of the artifacts are kept 
    locally in the Maven local repository, which is a folder on the local machine.

* Maven build profiles are:

	1.Per-User: This is defined in the Maven settings.xml file.
	2.Per Project: This is defined in the project�s pom.xml.
	3.Global: This is defined in the global Maven settings.xml file.

* Maven build profiles can be activated or triggered in the following ways:

	-->Using explicit commands
	-->Maven settings
	-->On the basis of environment variables
	-->Configuration of the operating system
	-->Present/missing files



