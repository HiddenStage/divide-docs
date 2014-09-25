Android Documentation
===========

#### Initialization
First you need to initialize your backend. Luckily, all you need is your production URL. If you would like to test your app in a development environment, put your development URL in the last parameter of the `Backend.init` method. 

```java
public class MyApplication extends Application {

    @Override
    public void onCreate(){
        // Context, production URL, development URL
        Backend.init(this,"http://authenticator-test.appspot.com/api/","");
    }
}
```

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
