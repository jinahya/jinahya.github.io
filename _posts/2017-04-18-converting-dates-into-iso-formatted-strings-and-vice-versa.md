---
layout: post
title: Converting Dates into ISO formatted Strings and vice versa
categories: programming
tags: java date time
---
```java
public static String dateToFormatted(final Date date) {
    return ofNullable(date).map(Date::toInstant).map(ISO_INSTANT::format)
            .orElse(null);
}

public static Date dateFromFormatted(final String formatted) {
    return ofNullable(formatted).map(ISO_INSTANT::parse).map(Instant::from)
            .map(Date::from).orElse(null);
}
```
