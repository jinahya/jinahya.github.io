---
layout: post
title: Using XML Converters for Enums
---
# Using XML Converters for Enums

```java
public abstract class EnumXmlAdapter<ValueType, E extends Enum<E>>
        extends XmlAdapter<ValueType, E> {
}
```

```java
public class DayOfWeekXmlAdapter extends EnumXmlAdapter<Integer, DayOfWeek> {

    @Override
    public DayOfWeek unmarshal(final Integer v) throws Exception {
        return ofNullable(v).map(DayOfWeek::of).orElse(null);
    }

    @Override
    public Integer marshal(final DayOfWeek v) throws Exception {
        return ofNullable(v).map(DayOfWeek::getValue).orElse(null);
    }
}
```
