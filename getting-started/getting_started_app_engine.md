Getting started - App Engine
===========
##Step 1
Clone the divide-server-sample repository via git by running the following in your command line:

```
git clone https://github.com/HiddenStage/divide-server-sample.git
```
##Step 2
Change the package name (and corresponding directory names) from `io.divide.server.sample` to your own package name. 
##Step 3
Change the encryption key to something secure. We recommend using a random password generator.
##Step 4
Now you need to create your App Engine instance.

1. Visit [Google Developers Console](https://console.developers.google.com/) in your web browser, and click Create Project.
2. Supply the project name Sample and accept the project ID that is auto-generated for you.
3. Click **Create**.

Make a note of the project ID, since you'll need it in the next step.
##Step 5
Return to your local project. In `src/main/webapp/WEB-INF/appengine-web.xml`, put your project ID from Step 4 in the `application` tag. (Replace `authenticator-test`)
##Step 6
In `src/main/webapp/WEB-INF/web.xml`, put your parent class in the `param-value` tag. (Replace `io.divide.server.sample.SomeApplication`)
##Step 7
Run `mvn clean install` to build the project and download all necessary library files.
##Step 8
Go to the root directory and run  `mvn appengine:update` to upload your project to App Engine. You may be asked to login to your Google account in this step
##Step 9
**Congrats!** Your backend is now up and running. 

Your production URL is `https://your-project-id.appspot.com/api/`. 

**Note:** App Engine supports SSL natively, so make sure you prefix your URL with `https://` for added security.

##Links
* [Server documentation](http://www.divide.io/docs/server)
* [App Engine Help](https://github.com/HiddenStage/divide-docs/blob/master/help/help_app_engine.md)
* [Javadocs](http://hiddenstage.github.io/divide-docs/javadocs/)
* [Sample Server app](https://github.com/HiddenStage/divide-server-sample)
