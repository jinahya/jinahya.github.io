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
## find
```java
public static Property findNamed(final EntityManager entityManager,
                                 final String name) {
    final TypedQuery typedQuery
        = entityManager.createNamedQuery("Property.find", Property.class);
    typedQuery.setParameter("name", name);
    try {
        return typedQuery.getSingleResult();
    } catch (final NoResultException nre) {
        return null;
    }
}

public static Property findCriteria(final EntityManager entityManager,
                                      final String name) {
    final CriteriaBuilder criteriaBuilder
        = entityManager.getCriteriaBuilder();
    final CriteriaQuery criteriaQuery
        = criteriaBuilder.createQuery(Property.class);
    final Root<Property> property = criteriaQuery.from(Property.class);
    criteriaQuery.select(property);
    criteriaQuery.where(criteriaBuilder.equal(property.get(Property_.name), name));
    final TypedQuery typedQuery
        = entityManager.createQuery(criteriaQuery);
    try {
        return typedQuery.getSingleResult();
    } catch (final NoResultException nre) {
        return null;
    }
}

public static Property find(final EntityManager entityManager,
                            final String name) {
    if (current().nextBoolean()) {
        return findNamed(entityManager, name);
    }
    return findCriteria(entityManager, name);
}
```
