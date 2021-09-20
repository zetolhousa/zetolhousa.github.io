---
title: "TIL 1"
date: 2021-09-20T12:32:57+05:30
tags: [java, til]
---

### FactoryBean
An amazing way to instantiate your beans based on different situations or conditions.

Example Use case: I want a specific implementation of an interface based on some launch date. I can define that in the factory.

```java
public class MessageFactoryBean implements FactoryBean<MessageInterface> {

    private MessageInterface postcard;
    private MessageInterface letter;

    public MessageInterface getObject() {
        if (your condition here) {
            return letter;
        }
        return postcard;
    }
    // other methods omitted
}
```

Where `MessageInterface` is implemented by `PostCard` and `FormalLetter`.
