Getting started for Android
===========
##Step 1
Add the following dependencies to your Android project.

Via Gradle:
```java
compile 'io.divide:client-android:0.5.2'
compile 'io.divide:client-android-mock:0.5.2'
```
Via Maven:
```java
<dependency>
    <groupId>io.divide</groupId>
    <artifactId>client-android</artifactId>
    <version>0.5.2</version>
</dependency>
<dependency>
    <groupId>io.divide</groupId>
    <artifactId>client-mock</artifactId>
    <version>0.5.2</version>
</dependency>
```
##Step 2
Create a new Java class that extends `Application` and initialize Divide.io in the `onCreate` method like so:
```java
public class YourApplication extends Application {

	@Override
	public void onCreate() {
		Backend.init(new AndroidDebugConfig(this, "http://your-backend-server.appspot.com/api/", ""));
	}
}
```
