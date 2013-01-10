Using GitHub as a Personal Maven Repository
=====

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


4. you can email to me  .

	
