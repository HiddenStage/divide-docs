Getting started - App Engine
===========
##Introduction
This tutorial will help you get started using Divide.io with [Google App Engine](https://developers.google.com/appengine/). App Engine is a cloud services platform which scales as you gain users, making it a great fit as a backend for a mobile app.

Before we begin, App Engine recommends using Java 7 and Maven 3.1 or greater.  If you need help setting this up, [click here](https://developers.google.com/appengine/docs/java/gettingstarted/setup).

##Step 1
Change to a directory where you want your project on your local machine.

##Step 2
From the command line invoke Maven as follows:
```
mvn archetype:generate
```

##Step 3
When prompted to Choose a number or apply filter, supply the value `com.google.appengine.archetypes:skeleton-archetype` to display a short list of archetypes matching the filter.

##Step 4
When prompted to Choose a number or apply filter, supply the number displayed for the value `remote -> com.google.appengine.archetypes:appengine-skeleton-archetype`, which currently is the number 1.

##Step 5
When prompted to Define value for property 'groupId', supply a package name for your backend i.e. `io.divide.backend`.

##Step 6
When prompted to Define value for property 'artifactId', supply the name of your application i.e. `sample`.

##Step 7
When prompted to Define value for property 'version', accept the default value by pressing enter.

##Step 8
When prompted to Define value for property 'package', accept the default value by pressing enter.

##Step 9
When prompted to confirm your choices, accept the default value (Y).

##Step 10
Wait for the project to finish generating. At this point, the basic project layout with required files is complete. Inside the directory where you created the project, you'll have a subdirectory named `sample`, which contains a `pom.xml` file and two subdirectories: `sample-ear` and `sample-war`, similar to the layout shown here:

![](https://raw.githubusercontent.com/HiddenStage/divide-docs/master/getting-started/images/appengine_dir.png)

We'll describe what to do inside these two subdirectories later. (Notice that the location where you'll add your own Java source code is inside sample-war/src/main/java.)

Now you are ready to configure the project.

Configuring the project
===========

To configure the project:

1. You'll need a project ID in order to deploy your app to production App Engine. Create a new project as follows:
  1. Visit [Google Developers Console](https://console.developers.google.com/) in your web browser, and click Create Project.
  2. Supply the project name Guestbook and accept the project ID that is auto-generated for you.
  3. Click **Create**.
Make a note of the project ID, since you'll need it in the next step.
2. Return to the terminal window for your Maven project, and edit the file `sample/sample-ear/src/main/application/META-INF/appengine-application.xml`, so that the element `<application>` contains the project ID you just obtained above.
3. Edit `sample/pom.xml` in the main application directory so that `<appengine.target.version>` inside the `<properties>` element points to the most recent App Engine SDK version. Currently, this is 1.9.10.
Your completed work should look like this:

```
<properties>
  <project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>
  <appengine.target.version>1.9.10</appengine.target.version>
</properties>
```

4. In the main app directory `sample`, invoke Maven as follows to make sure the project is buildable:
5. 
```
mvn clean install
```

You should get a success message `[INFO] BUILD SUCCESS`.

You are now ready to add your own application code and UI.
