---
layout: post
title: Using Attribute Converters for Enums
---
# Using AttributeConverter for Enums

`javax.ws.rs.core` 패키지에 `Link` 라는 클래스가 있는지 오늘에서야 알았다.
(직접 만들어 쓴 경우가 한번밖에 없어서 다행이다. :))

만들고 있는 클래스에 행복하게 넣어봤다.

```java
public abstract class BaseEntity {

    public List<Link> getLinks() {
        if (links == null) {
            links = new ArrayList<>();
        }
        return links;
    }

    @XmlElement(name = "link");
    @XmlAdapter(Link.JaxbAdapter.class);
    private List<Link> links;
}
```

Namespace 부분에 문제가 발생했다. `package-info.java` 에 다음과 같은 내용이 있었는데,

```java
@XmlSchema(
        attributeFormDefault = XmlNsForm.UNQUALIFIED,
        elementFormDefault = XmlNsForm.QUALIFIED,
        namespace = XmlConstants.NS_URI_BANKING,
        xmlns = {
            @XmlNs(prefix = XMLConstants.DEFAULT_NS_PREFIX, // default namespace
                   namespaceURI = XmlConstants.NS_URI_BANKING),
            @XmlNs(prefix = "xsi",
                   namespaceURI = XMLConstants.W3C_XML_SCHEMA_INSTANCE_NS_URI)
        }
)
@XmlAccessorType(XmlAccessType.NONE)
```
`Link.JaxbLink` 클래스의 namespace가 `''` 이라서 문제가 되었다.

## `NamespacedJaxbLink.java`
```java
public class NamespacedJaxbLink {

    public NamespacedJaxbLink(final JaxbLink jaxbLink) {
        super();
        this.jaxbLink = requireNonNull(jaxbLink, "jaxbLink is null");
    }

    @XmlAttribute
    public URI getUri() {
        return jaxbLink.getUri();
    }

    @XmlAnyAttribute
    public Map<QName, Object> getParams() {
        return jaxbLink.getParams();
    }

    public JaxbLink toJaxbLink() {
        return new JaxbLink(getUri(), getParams());
    }

    private final JaxbLink jaxbLink;
}
```

## `NamespacedJaxbLinkAdapter.java`

```java
public class NamespacedJaxbLinkAdapter
        extends XmlAdapter<NamespacedJaxbLink, Link> {

    @Override
    public NamespacedJaxbLink marshal(final Link v) {
        return new NamespacedJaxbLink(jaxbAdapter.marshal(v));
    }

    @Override
    public Link unmarshal(final NamespacedJaxbLink v) {
        return jaxbAdapter.unmarshal(v.toJaxbLink());
    }

    private final JaxbAdapter jaxbAdapter = new JaxbAdapter();
}
```
