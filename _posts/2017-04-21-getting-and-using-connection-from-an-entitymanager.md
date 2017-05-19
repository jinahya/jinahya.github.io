---
layout: post
title: Getting and using a Connection from an EntityManager.
categories: programming
tags: java java-ee jpa entitymanager hibernate eclipselink
---

## EclipseLink

As described in [Getting a JDBC Connection from an EntityManager](https://wiki.eclipse.org/EclipseLink/Examples/JPA/EMAPI#Getting_a_JDBC_Connection_from_an_EntityManager), we can [unwrap](http://docs.oracle.com/javaee/7/api/javax/persistence/EntityManager.html#unwrap-java.lang.Class-) an [EntityManager](http://docs.oracle.com/javaee/7/api/javax/persistence/EntityManager.html) into a [Connection](http://docs.oracle.com/javase/8/docs/api/java/sql/Connection.html).

```java
final EntityManagerFactory factory = entityManagerFactory();
final EntityManager manager = factory.createEntityManager();
manager.getTransaction().begin();
try {
    final Connection connection = manager.unwrap(Connection.class);
} catch (final PersistenceException pe) {
    logger.error("failed to unwrap EntityManager into a Connection", pe);
}
manager.getTransaction().commit();
manager.close();
factory.close();
```

## Hibernate

Let's follow this [excellent answer](http://stackoverflow.com/a/7626387/330457) using reflections.

```java
final EntityManagerFactory factory = entityManagerFactory();
final EntityManager manager = factory.createEntityManager();
//manager.getTransaction().begin();
final Class<?> sessionClass;
try {
    sessionClass = Class.forName("org.hibernate.Session");
} catch (final ClassNotFoundException cnfe) {
    //logger.debug("class not found", cnfe);
    return;
}
final Object session = manager.unwrap(sessionClass);
final Class<?> workClass;
try {
    workClass = Class.forName("org.hibernate.jdbc.Work");
} catch (final ClassNotFoundException cnfe) {
    //logger.debug("class not found", cnfe);
    return;
}
final Method executeMethod;
try {
    executeMethod
        = workClass.getMethod("work", Connection.class);
} catch (final NoSuchMethodException nsme) {
    return;
}
final Object workProxy = Proxy.newProxyInstance(
        workClass.getClassLoader(),
        new Class[]{workClass},
        (proxy, method, args) -> {
            if (method.equals(executeMethod)) {
                final Connection connection = (Connection) args[0];
                result.add(function.apply(connection));
            }
            return null;
        }
);
sessionClass.getMethod("doWork", workClass).invoke(session, workProxy);
//manager.getTransaction().commit();
manager.close();
factory.close();
```
