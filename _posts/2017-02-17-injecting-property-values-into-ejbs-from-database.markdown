---
layout: post
title: Injecting Property Values into EJBs from Database
---
# References
* [Inject Java Properties in Java EE Using CDI
](http://piotrnowicki.com/2012/06/inject-java-properties-in-java-ee-using-cdi/)

# Property.java
```java
@Entity
@NamedQueries({
@NamedQuery(name = "Property.find",
            query = "SELECT p FROM Property AS p WHERE p.name = :name")
})
public class Property {

    @Basic(optional = false)
    @Column(name = "NAME", nullable = false, unique = true)
    @NotNull
    private String name;

    @Basic(Optional = false)
    @Column(name = "VALUE_", nullable = false)
    @NotNull
    private String value = "";
}
```