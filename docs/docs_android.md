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
Credential users are users who register with a username and password to your app. Data stays linked to a user's account, which means it can persist across multiple devices as long as the user signs in.

**Note:** Passwords are encrypted over the network and stored on the server via bcrypt. We do recommend SSL for added security.

##### Signing Up
The following will sign a user up to your service. All it requires is an email, username, and password (Strings).

```java
// Synchronous 
BackendUser.signUp(email, username, password);

// Asynchronous 
BackendUser.signUpInBackground(email, username, password);
```

##### Logging in
Once a user has an account, you can sign them in by using the following methods.

```java
// Synchronous 
BackendUser.signin(username, password);

// Asynchronous
BackendUser.loginInBackground(username, password);
```

We'll be changing the login calls to a consistant name in the next release :)

##### Logging out

```java
BackendUser.logOut();
```

##### Anonymous Users
If your app doesn't need to have users with usernames and passwords, you can use anonymous users. Anonymous users have all of the same functionalities as credential users except they aren't persistant across devices.

Creating anonymous users is easy. Simply put the following before any other call to the backend.

```java
// Synchronous 
UserUtils.getAnonymousUser(this).toBlocking().first();

// Asynchronous
UserUtils.getAnonymousUser(this).subscribe();
```

This call will check to see if a user is associated with the current device, and if so will log them in automatically. If no account is associated, it will automatically create an account and log in the user.

You might want to use anonymous users over credential users if you don't need to persist data across devices or if you don't need to associate data with a particular user.

#### Create and Save an Object
Creating and saving an Object is easy. Simply create a new `BackendObject` instance, store primative types to it, then store it as shown below. `.remote()` saves the object to your backend and `.local()` stores the object to a local database.

```java
BackendObject object = new BackendObject();

// add values, will be serialized with GSON
object.put("somePrimative1",1);             // int
object.put("somePrimative2",1L);            // long
object.put("somePrimative3","Some string"); // String
object.put("someObject",new Object());      // Some POJO...etc.

// store remotely async
BackendServices
	.remote()
	.save(object)
	.subscribe();
        
// store locally async
BackendServices
	.local()
	.save(object);
```

// get, save, delete, exists, count

#### Queries

##### Building a query
Building queries in Divide.io are built to be structured like a standard SQL query. For instance, if you want to get receive the first 10 records from the BackendObject class, your query would be:

```java
Query query = new QueryBuilder()
    .select()
    .from(BackendObject.class)
    .limit(10)
    .build();
```

If you'd like to receive all objects from the Pizza class which have more than 2 toppings, your query would be:

```java
Query query = new QueryBuilder()
    .select()
    .from(Pizza.class)
    .where("NumberOfToppings", OPERAND.GREATER_THAN, "2")
    .build();
```

##### Running a query
Now that you've built your Query, here's how you run your query against your backend asyncronously:

```java
// Retrieve the first 10 records from the BackendObject class
Query query = new QueryBuilder()
    .select()
    .from(BackendObject.class)
    .limit(10).build();

// Run query against remote server
BackendServices.remote()
    .query(BackendObject.class, query)
    .subscribe(new Action1<Collection<BackendObject>>() {
           @Override
           public void call(Collection<BackendObject> objects) {
 	     		// do something with objects
           }
     });
```

And here's how to query your local database:

```java
// Retrieve the all objects with more than 2 toppings from the Pizza class
Query query = new QueryBuilder()
    .select()
    .from(Pizza.class)
    .where("NumberOfToppings", OPERAND.GREATER_THAN, "2")
    .build();
     
// Run query against local server
BackendServices.local()
    .query(Pizza.class, query)});
```

#### Extending BackendObject

```java
public class Pizza extends BackendObject {
    String type;
    int numOfToppings;

    public Pizza() {
        super(Pizza.class);
    }

    public void setType(String type) {
        this.put("Type", type);
    }

    public String getType() {
        return this.get(String.class, "Type");
    }

    public void setNumOfToppings(int numOfToppings) {
        this.put("NumberOfToppings", numOfToppings);
    }

    public int getNumOfToppings() {
        return this.get(Integer.class, "NumberOfToppings");
    }
}
```

#### Libraries used
* [RxJava](https://github.com/ReactiveX/RxJava)
* [Retrofit](http://square.github.io/retrofit/)


#### Links
* [Javadocs](http://hiddenstage.github.io/divide-docs/javadocs/)
* [Sample Android app](https://github.com/HiddenStage/divide-android-sample)
