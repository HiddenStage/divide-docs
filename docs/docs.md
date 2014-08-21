Divide.io Documentation
===========

**Currently in alpha. Not intended for production use at this time.**

#### Introduction

Divide.io is an open source Backend-as-a-Service (BaaS). It provides tools to easily, securely, and efficiently communicate between your app and a server. It handles data storage, user registration & management, and push notifications.

#### Server
Built on Jersey, it can be deployed to any J2EE server that supports javax.ws.rs.core.Application. DAO implementations are independent and can be written/plugged in for the situation.

```java
public class SomeApplication extends AuthApplication<OrientDBDao> {

    private String encryptionKey = "someKeyForSynchronousEncryption";

    public SomeApplication() {
    	// dao class
        super(OrientDBDao.class, encryptionKey);
    }
    
    public SomeApplication() {
        // dao instance
        super(new OrientDBDao(), encryptionKey);
    }
}
```
#### Client (Android)
```java
public class MyApplication extends Application {

    @Override
    public void onCreate(){
        Backend.init(this,"http://authenticator-test.appspot.com/api/");
    }
}
```
#### Create and Save an Object
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
// create Query
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

