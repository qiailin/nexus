Using GitHub as a Personal Maven Repository
=====

name : qiailin

email: qiailin@gmail.com

qq:172794299

Sometime you are in need for a maven repository accessible from the net which is under your control. Reasons might be:

    a 3rd-party lib is not on Maven central or the desired version is missing
    you built modules/libraries which will be included in your other projects
    …
With the following steps you will be able to serve any artifact from a public GitHub repository by just added a few lines into your pom.xml. I personally wasted quite an amount of time on this topic so I guess I’ll save it here – for you and me.

Ready? Let’s start!

In our example we’ll use our GitHub repository to server a file which is not available at Maven Central as the time of writing.
1. Creating the GitHub repository

Follow this link and create a new repository named mavenrepo.

You could as well choose a different name but then you will have to change every occurance in the following steps. Your call.
2. Creating the content for this repository

Change into the folder where the new repository will be lying on your disk. From here you will be able to push changes into your remote repository and thus update your artifacts.
bash :
---------------------------------------------------------------
1. Creating the GitHub repository

Follow this link "https://github.com/new" and create a new repository named nexus.

You could as well choose a different name but then you will have to change every occurance in the following steps. Your call.
------------------------------------------------------------------
2. Creating the content for this repository

git clone git@github.com:qiailin/nexus.git 

#clone a project form github

mkdir releases snapshots

#empty dirs can't be added to git

touch releases/README

touch snapshots/README

git add .

git commit -m "init nexu setup"

git push origin master

Cool, your local maven repository is waiting for it’s first artifact.
-----------------------------------------------------------------
3. Creating the first artifact

Now you have to change to the location of your artifact-to-be.

if you want to seeing the detail info , you can view releases/readme

and the snapshot/readme . 

thanks  .

eg:


 qiailin@localhost:~/development/nexus$ git add .
qiailin@localhost:~/development/nexus$ git commit -m "mysql library"
[master 69a1099] mysql library
 9 files changed, 26 insertions(+)
 create mode 100644 releases/mysql/mysql-connector-java/5.1.22/mysql-connector-java-5.1.22.jar
 create mode 100644 releases/mysql/mysql-connector-java/5.1.22/mysql-connector-java-5.1.22.jar.md5
 create mode 100644 releases/mysql/mysql-connector-java/5.1.22/mysql-connector-java-5.1.22.jar.sha1
 create mode 100644 releases/mysql/mysql-connector-java/5.1.22/mysql-connector-java-5.1.22.pom
 create mode 100644 releases/mysql/mysql-connector-java/5.1.22/mysql-connector-java-5.1.22.pom.md5
 create mode 100644 releases/mysql/mysql-connector-java/5.1.22/mysql-connector-java-5.1.22.pom.sha1
 create mode 100644 releases/mysql/mysql-connector-java/maven-metadata.xml
 create mode 100644 releases/mysql/mysql-connector-java/maven-metadata.xml.md5
 create mode 100644 releases/mysql/mysql-connector-java/maven-metadata.xml.sha1
qiailin@localhost:~/development/nexus$ git push origin master
Counting objects: 17, done.
Delta compression using up to 4 threads.
Compressing objects: 100% (8/8), done.
Writing objects: 100% (15/15), 779.85 KiB, done.
Total 15 (delta 0), reused 0 (delta 0)
To git@github.com:qiailin/nexus.git
   da3f9d7..69a1099  master -> master
qiailin@localhost:~/development/nexus$ cd ~
qiailin@localhost:~$ cd workspaces
qiailin@localhost:~/workspaces$ ls
j2ee
qiailin@localhost:~/workspaces$ cd j2ee
qiailin@localhost:~/workspaces/j2ee$ ls
qiailin-nexus-demo
qiailin@localhost:~/workspaces/j2ee$ cd qi*
qiailin@localhost:~/workspaces/j2ee/qiailin-nexus-demo$ ls
pom.xml  pom.xml~  src  target
qiailin@localhost:~/workspaces/j2ee/qiailin-nexus-demo$ mvn clean
[INFO] Scanning for projects...
[INFO]                                                                         
[INFO] ------------------------------------------------------------------------
[INFO] Building qiailin-nexus-demo 0.0.1-SNAPSHOT
[INFO] ------------------------------------------------------------------------
[INFO] 
[INFO] --- maven-clean-plugin:2.4.1:clean (default-clean) @ qiailin-nexus-demo ---
[INFO] Deleting /home/qiailin/workspaces/j2ee/qiailin-nexus-demo/target
[INFO] ------------------------------------------------------------------------
[INFO] BUILD SUCCESS
[INFO] ------------------------------------------------------------------------
[INFO] Total time: 0.277s
[INFO] Finished at: Fri Jan 11 00:18:10 CST 2013
[INFO] Final Memory: 2M/89M
[INFO] ------------------------------------------------------------------------
qiailin@localhost:~/workspaces/j2ee/qiailin-nexus-demo$ mvn -DaltDeploymentRepository=qiailin-snapshots::default::file:/home/qiailin/development/nexus/snapshots clean deploy
[INFO] Scanning for projects...
[INFO]                                                                         
[INFO] ------------------------------------------------------------------------
[INFO] Building qiailin-nexus-demo 0.0.1-SNAPSHOT
[INFO] ------------------------------------------------------------------------
Downloading: http://repo.maven.apache.org/maven2/org/apache/maven/plugins/maven-surefire-plugin/2.10/maven-surefire-plugin-2.10.pom
Downloaded: http://repo.maven.apache.org/maven2/org/apache/maven/plugins/maven-surefire-plugin/2.10/maven-surefire-plugin-2.10.pom (11 KB at 11.3 KB/sec)
Downloading: http://repo.maven.apache.org/maven2/org/apache/maven/surefire/surefire/2.10/surefire-2.10.pom
Downloaded: http://repo.maven.apache.org/maven2/org/apache/maven/surefire/surefire/2.10/surefire-2.10.pom (12 KB at 27.9 KB/sec)
Downloading: http://repo.maven.apache.org/maven2/org/apache/maven/maven-parent/20/maven-parent-20.pom
Downloaded: http://repo.maven.apache.org/maven2/org/apache/maven/maven-parent/20/maven-parent-20.pom (25 KB at 39.2 KB/sec)
Downloading: http://repo.maven.apache.org/maven2/org/apache/apache/9/apache-9.pom
Downloaded: http://repo.maven.apache.org/maven2/org/apache/apache/9/apache-9.pom (15 KB at 36.2 KB/sec)
Downloading: http://repo.maven.apache.org/maven2/org/apache/maven/plugins/maven-surefire-plugin/2.10/maven-surefire-plugin-2.10.jar
Downloaded: http://repo.maven.apache.org/maven2/org/apache/maven/plugins/maven-surefire-plugin/2.10/maven-surefire-plugin-2.10.jar (30 KB at 47.2 KB/sec)
Downloading: http://repo.maven.apache.org/maven2/org/apache/maven/plugins/maven-jar-plugin/2.3.2/maven-jar-plugin-2.3.2.pom
Downloaded: http://repo.maven.apache.org/maven2/org/apache/maven/plugins/maven-jar-plugin/2.3.2/maven-jar-plugin-2.3.2.pom (6 KB at 13.5 KB/sec)
Downloading: http://repo.maven.apache.org/maven2/org/apache/maven/plugins/maven-plugins/21/maven-plugins-21.pom
Downloaded: http://repo.maven.apache.org/maven2/org/apache/maven/plugins/maven-plugins/21/maven-plugins-21.pom (13 KB at 29.2 KB/sec)
Downloading: http://repo.maven.apache.org/maven2/org/apache/maven/plugins/maven-jar-plugin/2.3.2/maven-jar-plugin-2.3.2.jar
Downloaded: http://repo.maven.apache.org/maven2/org/apache/maven/plugins/maven-jar-plugin/2.3.2/maven-jar-plugin-2.3.2.jar (32 KB at 51.6 KB/sec)
[INFO] 
[INFO] --- maven-clean-plugin:2.4.1:clean (default-clean) @ qiailin-nexus-demo ---
[INFO] 
[INFO] --- maven-resources-plugin:2.4.3:resources (default-resources) @ qiailin-nexus-demo ---
[INFO] Using 'UTF-8' encoding to copy filtered resources.
[INFO] skip non existing resourceDirectory /home/qiailin/workspaces/j2ee/qiailin-nexus-demo/src/main/resources
[INFO] 
[INFO] --- maven-compiler-plugin:2.3.2:compile (default-compile) @ qiailin-nexus-demo ---
[INFO] Compiling 1 source file to /home/qiailin/workspaces/j2ee/qiailin-nexus-demo/target/classes
[INFO] 
[INFO] --- maven-resources-plugin:2.4.3:testResources (default-testResources) @ qiailin-nexus-demo ---
[INFO] Using 'UTF-8' encoding to copy filtered resources.
[INFO] skip non existing resourceDirectory /home/qiailin/workspaces/j2ee/qiailin-nexus-demo/src/test/resources
[INFO] 
[INFO] --- maven-compiler-plugin:2.3.2:testCompile (default-testCompile) @ qiailin-nexus-demo ---
[INFO] Compiling 1 source file to /home/qiailin/workspaces/j2ee/qiailin-nexus-demo/target/test-classes
[INFO] 
[INFO] --- maven-surefire-plugin:2.10:test (default-test) @ qiailin-nexus-demo ---
Downloading: http://repo.maven.apache.org/maven2/org/apache/maven/maven-plugin-api/2.0.9/maven-plugin-api-2.0.9.pom
Downloaded: http://repo.maven.apache.org/maven2/org/apache/maven/maven-plugin-api/2.0.9/maven-plugin-api-2.0.9.pom (2 KB at 3.6 KB/sec)
Downloading: http://repo.maven.apache.org/maven2/org/apache/maven/maven/2.0.9/maven-2.0.9.pom
Downloaded: http://repo.maven.apache.org/maven2/org/apache/maven/maven/2.0.9/maven-2.0.9.pom (19 KB at 30.4 KB/sec)
Downloading: http://repo.maven.apache.org/maven2/org/apache/maven/maven-parent/8/maven-parent-8.pom
Downloaded: http://repo.maven.apache.org/maven2/org/apache/maven/maven-parent/8/maven-parent-8.pom (24 KB at 38.6 KB/sec)
Downloading: http://repo.maven.apache.org/maven2/org/apache/apache/4/apache-4.pom
Downloaded: http://repo.maven.apache.org/maven2/org/apache/apache/4/apache-4.pom (5 KB at 10.6 KB/sec)
Downloading: http://repo.maven.apache.org/maven2/org/apache/maven/surefire/surefire-booter/2.10/surefire-booter-2.10.pom
Downloaded: http://repo.maven.apache.org/maven2/org/apache/maven/surefire/surefire-booter/2.10/surefire-booter-2.10.pom (3 KB at 6.3 KB/sec)
Downloading: http://repo.maven.apache.org/maven2/org/apache/maven/surefire/surefire-api/2.10/surefire-api-2.10.pom
Downloaded: http://repo.maven.apache.org/maven2/org/apache/maven/surefire/surefire-api/2.10/surefire-api-2.10.pom (3 KB at 5.5 KB/sec)
Downloading: http://repo.maven.apache.org/maven2/org/apache/maven/surefire/maven-surefire-common/2.10/maven-surefire-common-2.10.pom
Downloaded: http://repo.maven.apache.org/maven2/org/apache/maven/surefire/maven-surefire-common/2.10/maven-surefire-common-2.10.pom (4 KB at 9.5 KB/sec)
Downloading: http://repo.maven.apache.org/maven2/org/codehaus/plexus/plexus-utils/2.1/plexus-utils-2.1.pom
Downloaded: http://repo.maven.apache.org/maven2/org/codehaus/plexus/plexus-utils/2.1/plexus-utils-2.1.pom (4 KB at 9.8 KB/sec)
Downloading: http://repo.maven.apache.org/maven2/org/sonatype/spice/spice-parent/16/spice-parent-16.pom
Downloaded: http://repo.maven.apache.org/maven2/org/sonatype/spice/spice-parent/16/spice-parent-16.pom (9 KB at 18.6 KB/sec)
Downloading: http://repo.maven.apache.org/maven2/org/sonatype/forge/forge-parent/5/forge-parent-5.pom
Downloaded: http://repo.maven.apache.org/maven2/org/sonatype/forge/forge-parent/5/forge-parent-5.pom (9 KB at 19.9 KB/sec)
Downloading: http://repo.maven.apache.org/maven2/org/apache/maven/maven-artifact/2.0.9/maven-artifact-2.0.9.pom
Downloaded: http://repo.maven.apache.org/maven2/org/apache/maven/maven-artifact/2.0.9/maven-artifact-2.0.9.pom (2 KB at 3.5 KB/sec)
Downloading: http://repo.maven.apache.org/maven2/org/apache/maven/maven-project/2.0.9/maven-project-2.0.9.pom
Downloaded: http://repo.maven.apache.org/maven2/org/apache/maven/maven-project/2.0.9/maven-project-2.0.9.pom (3 KB at 6.5 KB/sec)
Downloading: http://repo.maven.apache.org/maven2/org/apache/maven/maven-settings/2.0.9/maven-settings-2.0.9.pom
Downloaded: http://repo.maven.apache.org/maven2/org/apache/maven/maven-settings/2.0.9/maven-settings-2.0.9.pom (3 KB at 2.4 KB/sec)
Downloading: http://repo.maven.apache.org/maven2/org/apache/maven/maven-model/2.0.9/maven-model-2.0.9.pom
Downloaded: http://repo.maven.apache.org/maven2/org/apache/maven/maven-model/2.0.9/maven-model-2.0.9.pom (4 KB at 7.4 KB/sec)
Downloading: http://repo.maven.apache.org/maven2/org/apache/maven/maven-profile/2.0.9/maven-profile-2.0.9.pom
Downloaded: http://repo.maven.apache.org/maven2/org/apache/maven/maven-profile/2.0.9/maven-profile-2.0.9.pom (3 KB at 4.9 KB/sec)
Downloading: http://repo.maven.apache.org/maven2/org/apache/maven/maven-artifact-manager/2.0.9/maven-artifact-manager-2.0.9.pom
Downloaded: http://repo.maven.apache.org/maven2/org/apache/maven/maven-artifact-manager/2.0.9/maven-artifact-manager-2.0.9.pom (3 KB at 6.3 KB/sec)
Downloading: http://repo.maven.apache.org/maven2/org/apache/maven/maven-repository-metadata/2.0.9/maven-repository-metadata-2.0.9.pom
Downloaded: http://repo.maven.apache.org/maven2/org/apache/maven/maven-repository-metadata/2.0.9/maven-repository-metadata-2.0.9.pom (2 KB at 4.4 KB/sec)
Downloading: http://repo.maven.apache.org/maven2/org/apache/maven/maven-plugin-registry/2.0.9/maven-plugin-registry-2.0.9.pom
Downloaded: http://repo.maven.apache.org/maven2/org/apache/maven/maven-plugin-registry/2.0.9/maven-plugin-registry-2.0.9.pom (2 KB at 4.8 KB/sec)
Downloading: http://repo.maven.apache.org/maven2/org/apache/maven/maven-core/2.0.9/maven-core-2.0.9.pom
Downloaded: http://repo.maven.apache.org/maven2/org/apache/maven/maven-core/2.0.9/maven-core-2.0.9.pom (8 KB at 18.7 KB/sec)
Downloading: http://repo.maven.apache.org/maven2/org/apache/maven/maven-plugin-parameter-documenter/2.0.9/maven-plugin-parameter-documenter-2.0.9.pom
Downloaded: http://repo.maven.apache.org/maven2/org/apache/maven/maven-plugin-parameter-documenter/2.0.9/maven-plugin-parameter-documenter-2.0.9.pom (2 KB at 4.8 KB/sec)
Downloading: http://repo.maven.apache.org/maven2/org/apache/maven/reporting/maven-reporting-api/2.0.9/maven-reporting-api-2.0.9.pom
Downloaded: http://repo.maven.apache.org/maven2/org/apache/maven/reporting/maven-reporting-api/2.0.9/maven-reporting-api-2.0.9.pom (2 KB at 4.3 KB/sec)
Downloading: http://repo.maven.apache.org/maven2/org/apache/maven/reporting/maven-reporting/2.0.9/maven-reporting-2.0.9.pom
Downloaded: http://repo.maven.apache.org/maven2/org/apache/maven/reporting/maven-reporting/2.0.9/maven-reporting-2.0.9.pom (2 KB at 3.5 KB/sec)
Downloading: http://repo.maven.apache.org/maven2/org/apache/maven/maven-error-diagnostics/2.0.9/maven-error-diagnostics-2.0.9.pom
Downloaded: http://repo.maven.apache.org/maven2/org/apache/maven/maven-error-diagnostics/2.0.9/maven-error-diagnostics-2.0.9.pom (2 KB at 4.1 KB/sec)
Downloading: http://repo.maven.apache.org/maven2/org/apache/maven/maven-plugin-descriptor/2.0.9/maven-plugin-descriptor-2.0.9.pom
Downloaded: http://repo.maven.apache.org/maven2/org/apache/maven/maven-plugin-descriptor/2.0.9/maven-plugin-descriptor-2.0.9.pom (3 KB at 4.8 KB/sec)
Downloading: http://repo.maven.apache.org/maven2/org/apache/maven/maven-monitor/2.0.9/maven-monitor-2.0.9.pom
Downloaded: http://repo.maven.apache.org/maven2/org/apache/maven/maven-monitor/2.0.9/maven-monitor-2.0.9.pom (2 KB at 3.1 KB/sec)
Downloading: http://repo.maven.apache.org/maven2/org/apache/maven/maven-toolchain/2.0.9/maven-toolchain-2.0.9.pom
Downloaded: http://repo.maven.apache.org/maven2/org/apache/maven/maven-toolchain/2.0.9/maven-toolchain-2.0.9.pom (4 KB at 8.4 KB/sec)
Downloading: http://repo.maven.apache.org/maven2/org/apache/maven/shared/maven-common-artifact-filters/1.3/maven-common-artifact-filters-1.3.pom
Downloaded: http://repo.maven.apache.org/maven2/org/apache/maven/shared/maven-common-artifact-filters/1.3/maven-common-artifact-filters-1.3.pom (4 KB at 8.7 KB/sec)
Downloading: http://repo.maven.apache.org/maven2/org/apache/maven/shared/maven-shared-components/12/maven-shared-components-12.pom
Downloaded: http://repo.maven.apache.org/maven2/org/apache/maven/shared/maven-shared-components/12/maven-shared-components-12.pom (10 KB at 22.2 KB/sec)
Downloading: http://repo.maven.apache.org/maven2/org/apache/maven/maven-parent/13/maven-parent-13.pom
Downloaded: http://repo.maven.apache.org/maven2/org/apache/maven/maven-parent/13/maven-parent-13.pom (23 KB at 35.4 KB/sec)
Downloading: http://repo.maven.apache.org/maven2/org/apache/apache/6/apache-6.pom
Downloaded: http://repo.maven.apache.org/maven2/org/apache/apache/6/apache-6.pom (13 KB at 29.0 KB/sec)
Downloading: http://repo.maven.apache.org/maven2/org/codehaus/plexus/plexus-container-default/1.0-alpha-9/plexus-container-default-1.0-alpha-9.pom
Downloaded: http://repo.maven.apache.org/maven2/org/codehaus/plexus/plexus-container-default/1.0-alpha-9/plexus-container-default-1.0-alpha-9.pom (2 KB at 2.9 KB/sec)
Downloading: http://repo.maven.apache.org/maven2/org/apache/maven/surefire/surefire-booter/2.10/surefire-booter-2.10.jar
Downloading: http://repo.maven.apache.org/maven2/org/apache/maven/surefire/surefire-api/2.10/surefire-api-2.10.jar
Downloading: http://repo.maven.apache.org/maven2/org/apache/maven/shared/maven-common-artifact-filters/1.3/maven-common-artifact-filters-1.3.jar
Downloading: http://repo.maven.apache.org/maven2/org/codehaus/plexus/plexus-utils/2.1/plexus-utils-2.1.jar
Downloading: http://repo.maven.apache.org/maven2/org/apache/maven/surefire/maven-surefire-common/2.10/maven-surefire-common-2.10.jar
Downloaded: http://repo.maven.apache.org/maven2/org/apache/maven/surefire/surefire-booter/2.10/surefire-booter-2.10.jar (34 KB at 42.8 KB/sec)
Downloading: http://repo.maven.apache.org/maven2/org/apache/maven/reporting/maven-reporting-api/2.0.9/maven-reporting-api-2.0.9.jar
Downloaded: http://repo.maven.apache.org/maven2/org/apache/maven/shared/maven-common-artifact-filters/1.3/maven-common-artifact-filters-1.3.jar (31 KB at 35.4 KB/sec)
Downloaded: http://repo.maven.apache.org/maven2/org/apache/maven/reporting/maven-reporting-api/2.0.9/maven-reporting-api-2.0.9.jar (10 KB at 23.3 KB/sec)
Downloaded: http://repo.maven.apache.org/maven2/org/apache/maven/surefire/maven-surefire-common/2.10/maven-surefire-common-2.10.jar (60 KB at 27.5 KB/sec)
Downloaded: http://repo.maven.apache.org/maven2/org/apache/maven/surefire/surefire-api/2.10/surefire-api-2.10.jar (158 KB at 50.0 KB/sec)
Downloaded: http://repo.maven.apache.org/maven2/org/codehaus/plexus/plexus-utils/2.1/plexus-utils-2.1.jar (220 KB at 59.5 KB/sec)
[INFO] Surefire report directory: /home/qiailin/workspaces/j2ee/qiailin-nexus-demo/target/surefire-reports
Downloading: http://repo.maven.apache.org/maven2/org/apache/maven/surefire/surefire-junit3/2.10/surefire-junit3-2.10.pom
Downloaded: http://repo.maven.apache.org/maven2/org/apache/maven/surefire/surefire-junit3/2.10/surefire-junit3-2.10.pom (2 KB at 4.0 KB/sec)
Downloading: http://repo.maven.apache.org/maven2/org/apache/maven/surefire/surefire-providers/2.10/surefire-providers-2.10.pom
Downloaded: http://repo.maven.apache.org/maven2/org/apache/maven/surefire/surefire-providers/2.10/surefire-providers-2.10.pom (3 KB at 5.5 KB/sec)
Downloading: http://repo.maven.apache.org/maven2/org/apache/maven/surefire/surefire-junit3/2.10/surefire-junit3-2.10.jar
Downloaded: http://repo.maven.apache.org/maven2/org/apache/maven/surefire/surefire-junit3/2.10/surefire-junit3-2.10.jar (26 KB at 41.6 KB/sec)

-------------------------------------------------------
 T E S T S
-------------------------------------------------------
Running qiailin.nexus.demo.AppTest
Tests run: 1, Failures: 0, Errors: 0, Skipped: 0, Time elapsed: 0.016 sec

Results :

Tests run: 1, Failures: 0, Errors: 0, Skipped: 0

[INFO] 
[INFO] --- maven-jar-plugin:2.3.2:jar (default-jar) @ qiailin-nexus-demo ---
Downloading: http://repo.maven.apache.org/maven2/org/apache/maven/maven-archiver/2.4.2/maven-archiver-2.4.2.pom
Downloaded: http://repo.maven.apache.org/maven2/org/apache/maven/maven-archiver/2.4.2/maven-archiver-2.4.2.pom (4 KB at 9.4 KB/sec)
Downloading: http://repo.maven.apache.org/maven2/org/apache/maven/shared/maven-shared-components/16/maven-shared-components-16.pom
Downloaded: http://repo.maven.apache.org/maven2/org/apache/maven/shared/maven-shared-components/16/maven-shared-components-16.pom (9 KB at 21.5 KB/sec)
Downloading: http://repo.maven.apache.org/maven2/org/apache/maven/maven-parent/19/maven-parent-19.pom
Downloaded: http://repo.maven.apache.org/maven2/org/apache/maven/maven-parent/19/maven-parent-19.pom (25 KB at 38.9 KB/sec)
Downloading: http://repo.maven.apache.org/maven2/org/codehaus/plexus/plexus-archiver/2.0.1/plexus-archiver-2.0.1.pom
Downloaded: http://repo.maven.apache.org/maven2/org/codehaus/plexus/plexus-archiver/2.0.1/plexus-archiver-2.0.1.pom (3 KB at 6.7 KB/sec)
Downloading: http://repo.maven.apache.org/maven2/org/sonatype/spice/spice-parent/17/spice-parent-17.pom
Downloaded: http://repo.maven.apache.org/maven2/org/sonatype/spice/spice-parent/17/spice-parent-17.pom (7 KB at 14.0 KB/sec)
Downloading: http://repo.maven.apache.org/maven2/org/sonatype/forge/forge-parent/10/forge-parent-10.pom
Downloaded: http://repo.maven.apache.org/maven2/org/sonatype/forge/forge-parent/10/forge-parent-10.pom (14 KB at 30.1 KB/sec)
Downloading: http://repo.maven.apache.org/maven2/org/codehaus/plexus/plexus-utils/3.0/plexus-utils-3.0.pom
Downloaded: http://repo.maven.apache.org/maven2/org/codehaus/plexus/plexus-utils/3.0/plexus-utils-3.0.pom (4 KB at 9.1 KB/sec)
Downloading: http://repo.maven.apache.org/maven2/org/codehaus/plexus/plexus-io/2.0.1/plexus-io-2.0.1.pom
Downloaded: http://repo.maven.apache.org/maven2/org/codehaus/plexus/plexus-io/2.0.1/plexus-io-2.0.1.pom (2 KB at 4.2 KB/sec)
Downloading: http://repo.maven.apache.org/maven2/org/codehaus/plexus/plexus-components/1.1.19/plexus-components-1.1.19.pom
Downloaded: http://repo.maven.apache.org/maven2/org/codehaus/plexus/plexus-components/1.1.19/plexus-components-1.1.19.pom (3 KB at 6.5 KB/sec)
Downloading: http://repo.maven.apache.org/maven2/org/codehaus/plexus/plexus/3.0.1/plexus-3.0.1.pom
Downloaded: http://repo.maven.apache.org/maven2/org/codehaus/plexus/plexus/3.0.1/plexus-3.0.1.pom (19 KB at 42.4 KB/sec)
Downloading: http://repo.maven.apache.org/maven2/commons-lang/commons-lang/2.1/commons-lang-2.1.pom
Downloaded: http://repo.maven.apache.org/maven2/commons-lang/commons-lang/2.1/commons-lang-2.1.pom (10 KB at 23.6 KB/sec)
Downloading: http://repo.maven.apache.org/maven2/org/apache/maven/maven-archiver/2.4.2/maven-archiver-2.4.2.jar
Downloading: http://repo.maven.apache.org/maven2/org/codehaus/plexus/plexus-archiver/2.0.1/plexus-archiver-2.0.1.jar
Downloading: http://repo.maven.apache.org/maven2/commons-lang/commons-lang/2.1/commons-lang-2.1.jar
Downloading: http://repo.maven.apache.org/maven2/org/codehaus/plexus/plexus-io/2.0.1/plexus-io-2.0.1.jar
Downloading: http://repo.maven.apache.org/maven2/org/codehaus/plexus/plexus-utils/3.0/plexus-utils-3.0.jar
Downloaded: http://repo.maven.apache.org/maven2/org/apache/maven/maven-archiver/2.4.2/maven-archiver-2.4.2.jar (20 KB at 44.9 KB/sec)
Downloaded: http://repo.maven.apache.org/maven2/org/codehaus/plexus/plexus-io/2.0.1/plexus-io-2.0.1.jar (57 KB at 25.8 KB/sec)
Downloaded: http://repo.maven.apache.org/maven2/org/codehaus/plexus/plexus-utils/3.0/plexus-utils-3.0.jar (221 KB at 74.5 KB/sec)
Downloaded: http://repo.maven.apache.org/maven2/org/codehaus/plexus/plexus-archiver/2.0.1/plexus-archiver-2.0.1.jar (176 KB at 35.5 KB/sec)
Downloaded: http://repo.maven.apache.org/maven2/commons-lang/commons-lang/2.1/commons-lang-2.1.jar (203 KB at 40.9 KB/sec)
[INFO] Building jar: /home/qiailin/workspaces/j2ee/qiailin-nexus-demo/target/qiailin-nexus-demo.jar
[INFO] 
[INFO] --- maven-install-plugin:2.3.1:install (default-install) @ qiailin-nexus-demo ---
Downloading: http://repo.maven.apache.org/maven2/org/codehaus/plexus/plexus-digest/1.0/plexus-digest-1.0.pom
Downloaded: http://repo.maven.apache.org/maven2/org/codehaus/plexus/plexus-digest/1.0/plexus-digest-1.0.pom (2 KB at 2.5 KB/sec)
Downloading: http://repo.maven.apache.org/maven2/org/codehaus/plexus/plexus-components/1.1.7/plexus-components-1.1.7.pom
Downloaded: http://repo.maven.apache.org/maven2/org/codehaus/plexus/plexus-components/1.1.7/plexus-components-1.1.7.pom (5 KB at 11.9 KB/sec)
Downloading: http://repo.maven.apache.org/maven2/org/codehaus/plexus/plexus/1.0.8/plexus-1.0.8.pom
Downloaded: http://repo.maven.apache.org/maven2/org/codehaus/plexus/plexus/1.0.8/plexus-1.0.8.pom (8 KB at 11.7 KB/sec)
Downloading: http://repo.maven.apache.org/maven2/org/codehaus/plexus/plexus-container-default/1.0-alpha-8/plexus-container-default-1.0-alpha-8.pom
Downloaded: http://repo.maven.apache.org/maven2/org/codehaus/plexus/plexus-container-default/1.0-alpha-8/plexus-container-default-1.0-alpha-8.pom (8 KB at 11.7 KB/sec)
Downloading: http://repo.maven.apache.org/maven2/org/codehaus/plexus/plexus-digest/1.0/plexus-digest-1.0.jar
Downloaded: http://repo.maven.apache.org/maven2/org/codehaus/plexus/plexus-digest/1.0/plexus-digest-1.0.jar (12 KB at 18.5 KB/sec)
[INFO] Installing /home/qiailin/workspaces/j2ee/qiailin-nexus-demo/target/qiailin-nexus-demo.jar to /home/qiailin/development/repository/qiailin-nexus/qiailin-nexus-demo/0.0.1-SNAPSHOT/qiailin-nexus-demo-0.0.1-SNAPSHOT.jar
[INFO] Installing /home/qiailin/workspaces/j2ee/qiailin-nexus-demo/pom.xml to /home/qiailin/development/repository/qiailin-nexus/qiailin-nexus-demo/0.0.1-SNAPSHOT/qiailin-nexus-demo-0.0.1-SNAPSHOT.pom
[INFO] 
[INFO] --- maven-deploy-plugin:2.7:deploy (default-deploy) @ qiailin-nexus-demo ---
[INFO] Using alternate deployment repository qiailin-snapshots::default::file:/home/qiailin/development/nexus/snapshots
Downloading: file:/home/qiailin/development/nexus/snapshots/qiailin-nexus/qiailin-nexus-demo/0.0.1-SNAPSHOT/maven-metadata.xml
Uploading: file:/home/qiailin/development/nexus/snapshots/qiailin-nexus/qiailin-nexus-demo/0.0.1-SNAPSHOT/qiailin-nexus-demo-0.0.1-20130110.161904-1.jar
Uploaded: file:/home/qiailin/development/nexus/snapshots/qiailin-nexus/qiailin-nexus-demo/0.0.1-SNAPSHOT/qiailin-nexus-demo-0.0.1-20130110.161904-1.jar (3 KB at 1322.3 KB/sec)
Uploading: file:/home/qiailin/development/nexus/snapshots/qiailin-nexus/qiailin-nexus-demo/0.0.1-SNAPSHOT/qiailin-nexus-demo-0.0.1-20130110.161904-1.pom
Uploaded: file:/home/qiailin/development/nexus/snapshots/qiailin-nexus/qiailin-nexus-demo/0.0.1-SNAPSHOT/qiailin-nexus-demo-0.0.1-20130110.161904-1.pom (3 KB at 2274.4 KB/sec)
Downloading: file:/home/qiailin/development/nexus/snapshots/qiailin-nexus/qiailin-nexus-demo/maven-metadata.xml
Uploading: file:/home/qiailin/development/nexus/snapshots/qiailin-nexus/qiailin-nexus-demo/0.0.1-SNAPSHOT/maven-metadata.xml
Uploaded: file:/home/qiailin/development/nexus/snapshots/qiailin-nexus/qiailin-nexus-demo/0.0.1-SNAPSHOT/maven-metadata.xml (781 B)
Uploading: file:/home/qiailin/development/nexus/snapshots/qiailin-nexus/qiailin-nexus-demo/maven-metadata.xml
Uploaded: file:/home/qiailin/development/nexus/snapshots/qiailin-nexus/qiailin-nexus-demo/maven-metadata.xml (291 B at 284.2 KB/sec)
[INFO] ------------------------------------------------------------------------
[INFO] BUILD SUCCESS
[INFO] ------------------------------------------------------------------------
[INFO] Total time: 39.398s
[INFO] Finished at: Fri Jan 11 00:19:04 CST 2013
[INFO] Final Memory: 11M/85M
[INFO] ------------------------------------------------------------------------
qiailin@localhost:~/workspaces/j2ee/qiailin-nexus-demo$ cd ..
qiailin@localhost:~/workspaces/j2ee$ cd ..
qiailin@localhost:~/workspaces$ cd ..
qiailin@localhost:~$ cd de*
qiailin@localhost:~/development$ ls
nexus  repository  three  无标题文档  无标题文档~
qiailin@localhost:~/development$ cd nexus
qiailin@localhost:~/development/nexus$ ls
README.md  releases  snapshots
qiailin@localhost:~/development/nexus$ git add .
qiailin@localhost:~/development/nexus$ git commit -m "the snapshots deply"
[master 56cc8db] the snapshots deply
 15 files changed, 175 insertions(+)
 create mode 100644 releases/README~
 create mode 100644 snapshots/README~
 create mode 100644 snapshots/qiailin-nexus/qiailin-nexus-demo/0.0.1-SNAPSHOT/maven-metadata.xml
 create mode 100644 snapshots/qiailin-nexus/qiailin-nexus-demo/0.0.1-SNAPSHOT/maven-metadata.xml.md5
 create mode 100644 snapshots/qiailin-nexus/qiailin-nexus-demo/0.0.1-SNAPSHOT/maven-metadata.xml.sha1
 create mode 100644 snapshots/qiailin-nexus/qiailin-nexus-demo/0.0.1-SNAPSHOT/qiailin-nexus-demo-0.0.1-20130110.161904-1.jar
 create mode 100644 snapshots/qiailin-nexus/qiailin-nexus-demo/0.0.1-SNAPSHOT/qiailin-nexus-demo-0.0.1-20130110.161904-1.jar.md5
 create mode 100644 snapshots/qiailin-nexus/qiailin-nexus-demo/0.0.1-SNAPSHOT/qiailin-nexus-demo-0.0.1-20130110.161904-1.jar.sha1
 create mode 100644 snapshots/qiailin-nexus/qiailin-nexus-demo/0.0.1-SNAPSHOT/qiailin-nexus-demo-0.0.1-20130110.161904-1.pom
 create mode 100644 snapshots/qiailin-nexus/qiailin-nexus-demo/0.0.1-SNAPSHOT/qiailin-nexus-demo-0.0.1-20130110.161904-1.pom.md5
 create mode 100644 snapshots/qiailin-nexus/qiailin-nexus-demo/0.0.1-SNAPSHOT/qiailin-nexus-demo-0.0.1-20130110.161904-1.pom.sha1
 create mode 100644 snapshots/qiailin-nexus/qiailin-nexus-demo/maven-metadata.xml
 create mode 100644 snapshots/qiailin-nexus/qiailin-nexus-demo/maven-metadata.xml.md5
 create mode 100644 snapshots/qiailin-nexus/qiailin-nexus-demo/maven-metadata.xml.sha1
qiailin@localhost:~/development/nexus$ git push origin msater
error: src refspec msater does not match any.
error: failed to push some refs to 'git@github.com:qiailin/nexus.git'
qiailin@localhost:~/development/nexus$ git push origin master
Counting objects: 26, done.
Delta compression using up to 4 threads.
Compressing objects: 100% (13/13), done.
Writing objects: 100% (22/22), 4.49 KiB, done.
Total 22 (delta 2), reused 0 (delta 0)
To git@github.com:qiailin/nexus.git
   69a1099..56cc8db  master -> master
qiailin@localhost:~/development/nexus$ git add .
qiailin@localhost:~/development/nexus$ git commit -m "the readme info"
[master 201e390] the readme info
 2 files changed, 118 insertions(+), 4 deletions(-)
 rewrite README.md (78%)
 create mode 100644 README.md~
qiailin@localhost:~/development/nexus$ git push origin master
Counting objects: 6, done.
Delta compression using up to 4 threads.
Compressing objects: 100% (4/4), done.
Writing objects: 100% (4/4), 1.34 KiB, done.
Total 4 (delta 1), reused 0 (delta 0)
To git@github.com:qiailin/nexus.git
   56cc8db..201e390  master -> master
qiailin@localhost:~/development/nexus$ 

    … name :qiailin
      email:qiailin@gmail.com 
      QQ:172794299
     "https://github.com/qiailin" 以后会定期更新  ，
      第一篇为 nexus，接下来可能会有 SCM 托管项目 源码都会放在上面
 


	
