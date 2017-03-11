---
layout: post
title: Effective Java Recipes
---

## Effective Java: Programming Language Guide
* [amazon.com](https://www.amazon.com/Effective-Java-Programming-Language-Guide/dp/0201310058)

---
---

## Effective Java: Second Edition
* [amazon.com](https://www.amazon.com/Effective-Java-2nd-Joshua-Bloch/dp/0321356683)

---

### Chapter 1 Introduction

---

### Chapter 2 Creating and Destroying Objects

#### Item 1: Consider static factory methods instead of constructors

#### Item 2: Consider a builder when faced with many constructor parameters

#### Item 3: Enforce the singleton property with a private constructor or an enum type

#### Item 4: Enforce noninstantiability with a private constructor

#### Item 5: Avoid creating unnecessary objects

#### Item 6: Eliminate obsolute object references

#### Item 7: Avoid finializers

---

### Chapter 3 Methods Common to All Objects

#### Item 8: Obey the general contract when overriding `equals`

#### Item 9: Always override `hashCode` when you override `equals`

#### Item 10: Always override `toString`

#### Item 11: Override `clone` judiciously

#### Item 12: Consider implementing `Comparable`

---

### Chapter 4 Classes and Interfaces

----

### Chapter 5 Generics

#### Item 23: Don't use raw types in new code

##### References
* [Langer, Angelika. Java Generics FAQs — Frequently Asked Questions. 2008.](http://www.angelikalanger.com/GenericsFAQ/JavaGenericsFAQ.html)
* [Naftalin, Maurice, and Philip Wadler. Java Generics and Collections. O’Reilly Media, Inc., Sebastopol, CA, 2007. ISBN: 0596527756.](http://shop.oreilly.com/product/9780596527754.do)

#### Item 24: Eliminate unchecked warnings

#### Item 25: Prefer lists to arrays

##### covariant vs. invariant

##### reifiable vs. non-reifiable

##### References
* [Liskov substitution principle](https://en.wikipedia.org/wiki/Liskov_substitution_principle) (Wikipedia)
* [Covariance and contravariance (computer science)](https://en.wikipedia.org/wiki/Covariance_and_contravariance_(computer_science)) (Wikipedia)
* [Covariance, Invariance and Contravariance explained in plain English?](http://stackoverflow.com/q/8481301/330457) (Stackoverflow)
* [Erasure vs reification](http://beust.com/weblog/2011/07/29/erasure-vs-reification/) (Otaku, Cedric's blog)

#### Item 26: Favor generic types

#### Item 27: Favor generic methods

#### Item 28: Use bounded wildcards to increase API flexibility

#### Item 29: Consider typesafe heterogeneous containers

---

### Chapter 6 Enums and Annotations

#### Item 30: Use enums instead of `int` constant

#### Item 31: Use instance fields instead of ordinals

#### Item 32: Use `EnumSet` instead of bit fields

#### Item 33: Use `EnumMap` instead of ordinal indexing

#### Item 34: Emulate extensible enums with interfaces

#### Item 35: Prefer annotations to naming patterns

#### Item 36: Consistently use the `Override` annotation

#### Item 37: Use marker interface to define types

---

### Appendix: Items Corresponding to First Edition

---

### References

---

### Index
