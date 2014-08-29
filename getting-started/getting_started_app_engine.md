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
Your application will now be created.

