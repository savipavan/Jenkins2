# Jenkins2
Automate builds
Deployments
Testing
new Pipeline functionality

Pre-requisites:Automating builds & Deployments of software

2.1 Setting up Jenkins
----------------------
First Integration Tools CrusiseControl

Jenkins.io/doc/pipeline

Why Use Jenkins? - 
CRON on Steroids(Cron Wikipedia)
Automate Mundanity
 - Dev to prod
 - Continous Integration
 - Contimous Delivery

Reliable, Fast feedback

Simple Setup

Confident

Before Jenkins
--------------
https://en.wikipedia.org/wiki/jenkins_(software)
https://creativecommons.org/lincenses/by-sa/3.0/

2001 - CruiseControl - Builds(java), CCNet(dotnet), XML

Summer 2004 - Hudson Inception - Kohsuke Kawaguchi @Sun

2005 - Hudson Released

2007 - Popularity Growing - Replacement for CruiseControl

2009 - Oracle Acquires Sun - Amid recession
2010 - Acquisition Complete
Late 2010 - Tension - Issues over governance between contributors and oracle
Dec 2010 - Trademark Dispute : Oracle applies for trademark for Hudson.
Jan 2011 - Jenkins Born - Project renamed to Jenkins by community vote. Who forked?

2014 - Survey - Most of Community uses Jenkins
2014 - CloudBees - CloudBees shifts from Paas to focus on Jenkins SaaS Jenkins'16
April 2016 - Jenkins 2 Released - Pipeline plugin enabled by default. CD shift.

How to Use This couse:
----------------------
Follow Along
Work through included examples
Apply to your own projects

This course is divided in to 5 modules
1. Setting Up Jenkins
2. Creating Application Builds
3. Testing and Continuous Integration
4. Finding and Managing Plugins
5. Building Continous Delivery Pipelines

Setting up Jenkins : Installaing with Jenkins2
----------------------------------------------
https://jenkins.io --> download Jenkins --> 2 options (LTS or Weekly Release) - 2.7.1.war file

before we run we need to make sure Java installed on the system . Java 8 is recommended

Open the Downloads --> run the command "java -jar jenkins.war" 

on Internet Explorer : open localhost:8080

on the command prompt will show you the admin password

copy the password --> paste in IE --> click on install plugins suggested

jenkins doesnot have database, hence all the configurations are getting stored in Data Directory

ls ~/.jenkins/
if we need to uninstall then we can remove the folder and re-run the java jar command again so that system build new jenkins steup

--Create First Admin User --> Start using Jenkins
- Authentication and autherization

Running Jenkins with Docker 
---------------------------
https://hub.docker.com/library/jenkins/

Search official repository for 'jenkins'

search for how to use this image

over to the terminal:
docker run -p 8090:8080 -p 50000:50000 jenkins:2.7.1

open localhost:8090 in IE

Advantages of running Jenkins in Docker is we can run multiple versions and test the jenkins functionality

3. Creating Application Builds
building our application code

Anatomy of the Build process :

Clone application code from Git Repo --> in to local directory(work space) --> Compile --> run unit test --> package up the result

Cloning the code from github
-----------------------------
g0t4/jenkins2-course-spring-boot/spring-boot-samples-spring-boot-sample-atmosphere

clone this repo --> open the directory --> cd spring-boot-sample folder --> 
jenkins2-course-spring-boot/spring-boot-samples/spring-boot-sample-atomosphere

--Download Maven and manually building the project
--------------------------------------------------
tree .

- pom.xml file
src

maven.apache.org
Download and run the Maven

once you install then check the version
mvn -v

3.3.9

compile source code and generate class file

mvn compile
- we can see build sucess in the command prompt

-- perform on test on the application
mvn test
 - it can show test successfull
 
 -- pakcage phase
 mvn package
  -- it will generate jar file and show that Build success
  
  jar file location
  ls target/

-- Automating this process

on Jenkins login --> click on create a new job --> give a name and pick the type of job --> select Freestyle Project --> click on source code management --> select github --> paste the repository URL --> by default create -- master branch  --> click on Build --> click on Add build step --> select invoke top-level Maven targets --> select Invoke top-Level Maven targets --> type compile --> click on Advanced --> paste in to POM folder(spring-boot-samples/spring-boot-atomosphere/pom.xml)

Open the project view --> click on configure --> 

click on Build Now --> click on status --> click on console output --> 

open the ouput on workspace
(Users/wesdemos/.jenkins/workspace/atomsphere)

cd Users/wesdemos/.jenkins/workspace/atomsphere
cd spring-boot-samples-atomosphere

-- Browsing workspace inside Jenkins
------------------------------------
Job  is alot like template
Builds are instances associated with the template

click on Back to Project --> click on Workspace --> folder view

chmge configureation --> click on configure -->click on Build --> type package --> save

comback to project view --> click on Build now --> we can see the job number 2 --> open 

if we getting some issues with Maven and check/make sure Maven is included in the path

--Archiving Artifacts:
----------------------
got the workspace build --> 
work space is not specific to build nor jb. it is specific to project

click on configure  --> post-build actions --> Add post-build action --> Archive the artifacts --> specify which files to archive --> paste the path and put the target
(spring-boot-samples/spring-boot-sample-atmosphere/target/.*jar)
* - indicates all jar files in the folder
--save 

run Build Now -- we will see Last Successful Artifacts --> click on Build Now --> 

--Cleaning up Past builds
-------------------------
ls -alR target/

mvn package/

ls -alR target/

mvn clean
-- deleting the junk files

comback to project level --> clean pacakge --> save and apply -- build now
all files will be deleted and updated with new builds

--> project level --> configure --> Build Environment --> check 'Delete workspace before build starts

click on trend and see timeline status(how long build it takes)

Dashboard -- we can run the build

Troubleshooting Build failures:
------------------------------
We can find out our bill fail status as Red in job
click on workspace --> click on build 10 --> open console output --> click on project --> resolve the issue

FATAL : command execution failed -- if this error comes we need to check whether maven is working fine or not?

Challenge and Importing Job config.xml Files
--------------------------------------------
https://gist.github.com/got4/12d888d0ce9e40b79d8454dabdad7033

https://git.io/vKSVZ
What if am I config xml

copy config.xml
cd /.jenkins/jobs/ there we can find config.xml and other build details

ls

ls atmosphere/
make a new directory
mkdir atmosphere2

copy the .xml file to atmosphere2 directory

cp ~/jenkins2/exercises/m2/config.xml atmosphere2/.

go the Jenkins Dashboard --> Manage Jenkins --> Reload Configuration from Disk


