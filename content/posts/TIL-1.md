---
title: "TIL 1"
date: 2021-09-20T12:32:57+05:30
tags: [til]
---

### FactoryBean
An amazing way to instantiate your beans based on different situations or conditions.

Example use case: I want a specific implementation of an interface based on some launch date. I can define that in the factory.

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

References:
* [What is factory bean](https://spring.io/blog/2011/08/09/what-s-a-factorybean)
* [SO question where code snippet was taken](https://stackoverflow.com/questions/34679026/conditional-ref-in-spring-beans)

### Caffeinate
Keep your mac from falling asleep

1. Open terminal
2. Run the command

```bash
caffeinate -d
```
