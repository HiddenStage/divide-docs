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
Run `mvn clean install` to build the project and download all necessary library files.
