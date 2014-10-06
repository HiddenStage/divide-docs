Help - App Engine
===========
## Using Apache Maven with App Engine
We recommend using Maven to install and configure the App Engine SDK.

## Common commands
Upload your App Engine code:
```
mvn appengine:update
```
Start a local development server:
```
mvn appengine:devserver
```
Update indexes:
```
mvn appengine:update_indexes
```
[All goals](https://cloud.google.com/appengine/docs/java/tools/maven#app_engine_maven_plugin_goals)

## Known issues with Divide.io
* Queries to App Engine only work with String data types.
 * **Workaround:** Store all data types that need to be queries as Strings.
* Greater than, less than, and similar queries currently fail to remote App Engine, but works on local DB. 
 * **[Workaround](https://github.com/HiddenStage/divide/issues/6#issuecomment-57958620)**

## Links
* [App Engine - Java Docs](https://cloud.google.com/appengine/docs/java/)
* [App Engine - Using Maven](https://cloud.google.com/appengine/docs/java/tools/maven)
