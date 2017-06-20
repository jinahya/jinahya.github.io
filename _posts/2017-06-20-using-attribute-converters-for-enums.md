---
layout: post
title: Using Attribute Converters for Enums
---
# Using Attribute Converters for Enums

```java
public interface EnumAttributeConverter<E extends Enum<E>, Y>
        extends AttributeConverter<E, Y> {

}
```

```java
public class DayOfWeekIntegerConverter
        implements EnumAttributeConverter<DayOfWeek, Integer> {

    @Override
    public Integer convertToDatabaseColumn(final DayOfWeek attribute) {
        return ofNullable(attribute).map(DayOfWeek::getValue).orElse(null);
    }

    @Override
    public DayOfWeek convertToEntityAttribute(final Integer dbData) {
        return ofNullable(dbData).map(DayOfWeek::of).orElse(null);
    }
}
```
