Android Documentation
===========

#### Initialization
First you'll need to initialize your backend. Luckily, all you need is your production URL. We recommend initializing Divide.io by extending `Application` and putting the following code in `onCreate()`.

```java
public class MyApplication extends Application {

    @Override
    public void onCreate(){
	// Context, production server, debug server
	Backend.init(new AndroidDebugConfig(this, "https://your-backend-server.appspot.com/api/", "")); 
    }
}
```

**Note:** Make sure to add `<uses-permission android:name="android.permission.INTERNET" />` to your AndroidManifest. 

##### Testing in a development environment

If you would like to test your app in a development environment, simply put your development URL (usually a local server) as the last parameter of the `Backend.init` method. 

```java
public class MyApplication extends Application {

    @Override
    public void onCreate(){
	// Context, production server, debug server
	Backend.init(new AndroidDebugConfig(this, "https://your-backend-server.appspot.com/api/", "http://localhost:8888")); 
    }
}
```

#### Users
Divide.io associates every backend call with a particular user. This can be handled in two ways: credential users (users who register and login) or anonymous users. 

**It's important that users are logged in before making any other calls to the backend.** Backend calls while users are not logged in will fail and in some instances will cause your app to crash.

##### Credential Users


##### Anonymous Users
If your app doesn't need to have users with usernames and passwords, you can use anonymous users. Anonymous users have all of the same functionalities as credential users except they aren't persistant across sessions and devices.

Creating anonymous users is easy. Simply put the following before any other call to the backend.

```java
UserUtils.getAnonymousUser(this).toBlocking().first();
```

This call will check to see if a user is associated with the current device, and if so will log them in automatically. If no account is associated, it will automatically create an account and log in the user.

You might want to use anonymous users over credential users if you don't need to persist data across devices or if you don't need to associate data with a particular user.

#### Create and Save an Object
Creating and saving an object is easy. Simply create a new `BackendObject` instance, store primative types to it, then store it as shown below. `.remote()` saves the object to your backend and `.local()` stores the object to your local database.

```java
BackendObject object = new BackendObject();

// add values, will be serialized with GSON
object.put("somePrimative1",1);          // int
object.put("somePrimative2",1L);         // long
object.put("somePrimative3","Some string"); // String
object.put("someObject",new Object());   // Some POJO...etc.

// store remotely async
BackendServices
	.remote()
	.save(object)
	.subscribe();
        
// store locally async
BackendServices
	.local()
	.save(object)
	.subscribe();
```

#### Perform a Query

```java
// Retrieve the first 10 records from the BackendObject class
Query query = new QueryBuilder()
    .select()
    .from(BackendObject.class)
    .limit(10).build();

// run query against remote server
BackendServices.remote()
    .query(BackendObject.class, query)
    .subscribe(new Action1<Collection<BackendObject>>() {
           @Override
           public void call(Collection<BackendObject> objects) {
 	     		// do something with objects
           }
     });
```

#### Links
* [javadocs](http://hiddenstage.github.io/divide-docs/javadocs/)
* [sample Android app](https://github.com/HiddenStage/divide-android-sample)
