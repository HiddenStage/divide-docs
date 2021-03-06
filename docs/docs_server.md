Server Documentation
====================
Built on Jersey, it can be deployed to any J2EE server that supports javax.ws.rs.core.Application. DAO implementations are independent and can be written/plugged in for the situation.

The only thing you need to do for the backend is install our libraries, initialize a DAO class/instance, and provide an encryption key. Follow our Getting Started guides below for step-by-step instructions for various server providers.

#### Getting Started Guides

[Deploy on App Engine](http://www.divide.io/get_started/app_engine)

AWS and more server examples coming soon!

#### Initialization

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

**Be sure to change the encryption key before using in production!** We recommend using a random password generator.

#### Data manipulation
All data stored by Divide.io is stored natively in your backend. You have access to it to do things such as data manipulation, advanced queries, custom APIs, etc.

#### Security
For added security, we recommend all web traffic Divide.io facilitates is via SSL. Many of the server providers support SSL natively, whereas some require you to configure SSL.

#### Libraries used
* [Jersey](https://jersey.java.net/)

#### Links
* [Javadocs](http://hiddenstage.github.io/divide-docs/javadocs/)
* [Sample Server app](https://github.com/HiddenStage/divide-server-sample)
