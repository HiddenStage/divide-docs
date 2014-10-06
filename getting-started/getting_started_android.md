Getting started - Android
===========
##Step 1
Add the following dependencies to your Android project.

**Via Gradle:**

```java
compile 'io.divide:client-android:0.5.3'
compile 'io.divide:client-android-mock:0.5.3'
```

**Via Maven:**

```java
<dependency>
   <groupId>io.divide</groupId>
   <artifactId>client-android</artifactId>
   <version>0.5.3</version>
</dependency>
<dependency>
   <groupId>io.divide</groupId>
   <artifactId>client-mock</artifactId>
   <version>0.5.3</version>
</dependency>
```

##Step 2

Create a new Java class that extends `Application` and initialize Divide.io using your server's URL in the `onCreate` method like so:

```java
public class YourApplication extends Application {

	@Override
	public void onCreate() {
		// Context, production server, debug server
		Backend.init(new AndroidDebugConfig(this, "https://your-project-id.appspot.com/api/", ""));
	}
}
```

##Step 3

**That's it!**

You can now begin using our APIs to send and retrieve data from your backend.

Here is an example of saving a simple string to your backend:

```java
// Get anonymous user
UserUtils.getAnonymousUser(this).toBlocking().first();

BackendObject object = new BackendObject();
object.put("comments", "This is awesome!");

BackendServices
        .remote()
        .save(object)
        .subscribe();
```

##Links
* [Android documentation](http://www.divide.io/docs/android)
* [Javadocs](http://hiddenstage.github.io/divide-docs/javadocs/)
* [Sample Android app](https://github.com/HiddenStage/divide-android-sample)
