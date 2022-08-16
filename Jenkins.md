* Jenkins is a self-contained, open source automation server which can be used to automate all sorts of tasks related to building, testing, and delivering or deploying software.

* JENKINS_HOME directory is /var/lib/jenkins.

* It will stores the all the stuff created in jenkins.

* Jenkins is a Cron/Scheduler on Steriods fine tuned for Continuous Integration and Continuous Deployment.

* Plugin is an addon to jenkins, which provides functionality on the jenkins ui.

* There are lot of plugins available and also if required you can create your own extensions by using JAVA language.

* Installing plugin is not equal to installing software on the jenkins server.

* The configurations are stored as xml file under /var/lib/jenkins/jobs/<job-name>/config.xml.

* Jenkins backup can be taken from JENKINS_HOME directory.

* By using set command we can get the list of ENVIRONMENT Variables.

* Ant is a kind of build tool used to create configuration file 'build.xml'

* By adding some of the steps in post build actions, can archive the build artifacts locally in the Jenkins server.

* Plugun installation :
	1. Online installation: Manage jenkins -> Manage plugins, from this we can install the required plugin.
	2. Offline installation:  Majorily available with two extensions
					-> .jpi (jenkins plugin interface)
					-> .hpi (hudson plugin interface)
				--> Manage Jenkins -> Plugins -> Advanced and upload plugin 

* Periodic Backup plugin is installed to get the jenkins backup & restore.
	--> Once the plugin is installed navigate to Manage Jenkins => Uncategorized => Periodic Backup Manager => configure.
	--> then we can see backup now &restore options. 

* User Administration:
		Manage jenkins -> configure global security
	security realms:
		1. Delegate to servlet container:
			--> This option can be used only when you are running your jenkins server from a servlet container such as Tomcat.
			--> Enabling this option allows jenkins to authenticate user using servelt container realm (tomcat-users.xml)
		2. Jenkins own user database:
			--> This is default option, jenkins stores all the information inside xml files in JENKINS_HOME_DIRECTORY
		3. LDAP:
			--> This is one of the most widely used authentication methods in most organization 
			--> In this settings we connect jenkins to the LDAP Server (Active Directory) of your organization
		4. Unix user/group database:
			--> The following options works if Jenkins master is installed on Unix/Linux Machine
			--> When enabled, Jenkins delegates the authentication to the underlying OS.
			--> So all the users/groups that are configured on the OS get access to jenkins
			--> Ensure all user on the underlying OS have access to /etc/shadow file "sudo chmod g+r /etc/shadow"

* Creating a new user in jenkins:  Manage Jenkins => Manage Users => Create User

* Matrix-based security: This is one of the most widely use Authorization methods in Jenkins 

* Jenkins build stability can be understand by sun & cloud notation
		--> Sun represents 100% build stability (no build failures)
		--> Cloud represents failures

* Types of project:
	--> Free-style project
	--> Pipeline project
	--> Multi configuration project
	--> Folder project
	--> Multibranch pipeline project
	--> Organization folder project

* Jenkins Pipeline (or simply "Pipeline" with a capital "P") is a suite of plugins which supports implementing and integrating continuous delivery pipelines into Jenkins.

* Pipeline provides an extensible set of tools for modeling simple-to-complex delivery pipelines "as code" via the Pipeline domain-specific language (DSL) syntax.

* Key aspects of Jenkins Pipeline:
		--> Pipeline: A Pipeline is a user-defined model of a CD pipeline. A Pipeline�s code defines your entire build process, which typically includes stages for building an application, testing it and then delivering it.
		--> Node: A node is a machine which is part of the Jenkins environment and is capable of executing a Pipeline.
		--> Stage: A stage block defines a conceptually distinct subset of tasks performed through the entire Pipeline (e.g. "Build", "Test" and "Deploy" stages), which is used by many plugins to visualize or present Jenkins Pipeline status/progress.
		--> Step: A single task. Fundamentally, a step tells Jenkins what to do at a particular point in time.

* Jenkins2 Pipelines are two categories: 
                 1. Scripted Pipelines
				 2. Declarative Pipelines

* Scripted pipelines: 
	--> When Jenkins introduced pipeline as a code, the code was primarily a Groovy script with Jenkins-Specific DSL Steps inserted.
	--> Program�s flow was managed by Groovy constructs. Error reporting and checking were based on Groovy program execution rather than what 
you are attempting to do with Jenkins.
	-->E.g.
node {  
    stage('Build') { 
        // 
    }
    stage('Test') { 
        // 
    }
    stage('Deploy') { 
        // 
    }
}

* Declarative Pipelines:
	--> CloudBees, the enterprise company introduced and enhanced programming syntax for pipelines-as-code.
	--> In most of the cases the user is presented with direct error message, instead of scan through Groovy trace backs when an error occures
	--> This syntax adds a clear, expected structure to pipelines as well as enhanced DSL Elements and constructs.
	--> E.g. 
pipeline {
    agent any 
    stages {
        stage('Build') { 
            steps {
                // 
            }
        }
        stage('Test') { 
            steps {
                // 
            }
        }
        stage('Deploy') { 
            steps {
                // 
            }
        }
    }
}


* Plugin:
	1. Git
	2. Ant
	3. Gradle
	4. LDAP
	5. Email Extension
	6. Easy Installation
	7. Jira Jenkins Plugin
	8. JUnit Plugin
	9. Amazon EC2
* Manage and assign roles:
	--> Global roles
	--> Item roles
	--> Node roles
* Agent: An agent is typically a machine, or container, which connects to a Jenkins controller and executes tasks when directed by the controller.

* Artifact: An immutable file generated during a Build or Pipeline run which is archived onto the Jenkins Controller for later retrieval by users.

* Build: Result of a single execution of a job

* Cloud: A System Configuration which provides dynamic Agent provisioning and allocation, such as that provided by the Azure VM Agents or Amazon EC2 plugins.

* Controller: The central, coordinating process which stores configuration, loads plugins, and renders the various user interfaces for Jenkins.

* Core: The primary Jenkins application (jenkins.war) which provides the basic web UI, configuration, and foundation upon which Plugins can be built.

* Downstream: A configured Pipeline or job which is triggered as part of the execution of a separate Pipeline or Job.

* Executor: A slot for execution of work defined by a Pipeline or job on a Node. A Node may have zero or more Executors configured which corresponds to how many concurrent Jobs or Pipelines are able to execute on that Node.

* Fingerprint: A hash considered globally unique to track the usage of an Artifact or other entity across multiple Pipelines or jobs.

* Folder: An organizational container for Pipelines and/or jobs, similar to folders on a file system.

* Item: An entity in the web UI corresponding to either a: Folder, Pipeline, or job.

* Jenkins URL: The main url for the jenkins application, as visited by a user. e.g. https://ci.jenkins.io/

* Job: A user-configured description of work which Jenkins should perform, such as building a piece of software, etc.

* Label: User-defined text for grouping Agents, typically by similar functionality or capability. For example linux for Linux-based agents or docker for Docker-capable agents.

* LTS: A long-term support Release line of Jenkins products, becoming available for downloads every 12 weeks.

* Master: A deprecated term, synonymous with Controller.

* Node: A machine which is part of the Jenkins environment and capable of executing Pipelines or jobs. Both the Controller and Agents are considered to be Nodes.

* Project: A deprecated term, synonymous with job.

* Pipeline: A user-defined model of a continuous delivery pipeline, for more read the Pipeline chapter in this handbook.

* Plugin: An extension to Jenkins functionality provided separately from Jenkins Core.

* Publisher: Part of a Build after the completion of all configured Steps which publishes reports, sends notifications, etc. A publisher may report Stable or Unstable result depending on the result of its processing and its configuration. For example, if a JUnit test fails, then the whole JUnit publisher may report the build result as Unstable.

* Resource Root URL: A secondary url used to serve potentially untrusted content (especially build artifacts). This url is distinct from the Jenkins URL.

* Release: An event, indicating availability of Jenkins distribution products or one of Jenkins plugins. Jenkins products belong either to LTS or weekly Release lines.

* Stage: stage is part of Pipeline, and used for defining a conceptually distinct subset of the entire Pipeline, for example: "Build", "Test", and "Deploy", which is used by many plugins to visualize or present Jenkins Pipeline status/progress.

* Step: A single task; fundamentally steps tell Jenkins what to do inside of a Pipeline or job.

* Trigger: A criteria for triggering a new Pipeline run or job.

* Update Center: Hosted inventory of plugins and plugin metadata to enable plugin installation from within Jenkins.

* Upstream: A configured Pipeline or job which triggers a separate Pipeline or Job as part of its execution.

* Workspace: A disposable directory on the file system of a Node where work can be done by a Pipeline or job. Workspaces are typically left in place after a Build or Pipeline run completes unless specific Workspace cleanup policies have been put in place on the Jenkins Controller.

Build Status:
-------------
* Aborted: The Build was interrupted before it reaches its expected end. For example, the user has stopped it manually or there was a time-out.

* Failed: The Build had a fatal error.

* Stable: The Build was Successful and no Publisher reports it as Unstable.

* Successful: The Build has no compilation errors.

* Unstable: The Build had some errors but they were not fatal. A Build is unstable if it was built successfully and one or more publishers report it unstable. For example if the JUnit publisher is configured and a test fails then the Build will be marked unstable.

* A Pipeline that has failing tests will be marked as "UNSTABLE", denoted by yellow in the web UI. That is distinct from the "FAILED" state, denoted by red.

* When there are test failures, it is often useful to grab built artifacts from Jenkins for local analysis and investigation. This is easily done with the archiveArtifacts step and a file-globbing expression.

* 











*******
sudo rtpt update
sudo apt install openjdk-11-jdk -y
jenkins installation from documentation
open jenkins page
install pulgins
setting necessary permission:
-----------------------------
sudo -i
visudo --> jenkins ALL=(ALL:ALL) NOPASSWD:ALL
su jenkins
cd ~
pwd (ans-/var/lib/jenkins)
sudo apt update
exit
exit
-------------------------

configuring jenkins node:
-------------------------
connect to node using node publicip
sudo nano /etc/ssh/sshd_config --> passwordauthentication yes
sudo service sshd restart
sudo adduser priya
sudo cat /etc/passwd
sudo visudo --> priya ALL=(ALL:ALL) NOPASSWD:ALL
su priya
cd ~
pwd
sudo apt update
sudo apt install openjdk-11-jdk -y
install maven
vi ~/.bashrc --> export JAVA_HOME=/usr/lib/jvm/java-11-openjdk-amd64
source ~/.bashrc or exit
su priya
cd ~
echo $JAVA_HOME
cd /tmp
wget https://dlcdn.apache.org/maven/maven-3/3.8.4/binaries/apache-maven-3.8.4-bin.tar.gz
tar -xvzf apache-maven-3.8.5-bin.tar.gz
sudo cp -r apache-maven-3.8.5/ /usr/local
vi ~/.bashrc --> export M2_HOME='/usr/local/apache-maven-3.8.4'
	     --> export PATH=$PATH:$M2_HOME/bin
sudo
configuration
-------------
jenkins --> manage jenkins --> 	manage nodes and clouds --> new node

node name & permanent agent
exit
exit
*login with user priya
java -version
echo $JAVA_HOME
echo $M2_HOME
mvn --version
git --version


git branch scripted 
git branch declarative
git checkout scripted
pipeline {
    agent { label 'jdk11-mvn3.8.4' }
    triggers { upstream(upstreamProjects: '', threshold: hudson.model.Result.SUCCESS) }
    stages {
        stage('scm') {
            steps {
                git 'https://github.com/GitPracticeRepo/java11-examples.git'
            }
        }
        stage('build') {
            steps {
                sh '/usr/local/apache-maven-3.8.4/bin/mvn clean package'
            }
        }


node('build-jdk11-mvn3.8.5-1') {
    stage('git'){
        git branch: 'scripted', url: 'https://github.com/supriyajagadeesh/spring-petclinic.git'
    }

    stage('build') {
        sh '''
            echo "PATH=${PATH}"
            echo "M2_HOME=${M2_HOME}"
        '''
        sh '/usr/local/apache-maven-3.8.5/bin/mvn clean package'
    }
    stage('archive') {
        archiveArtifacts artifacts: 'target/*.jar', followSymlinks: false
    }
    stage('publish test reports') {
        junit '**/TEST-*.xml'
    }
}

