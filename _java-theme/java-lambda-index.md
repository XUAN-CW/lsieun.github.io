---
title: "Java Lambda"
sequence: "lambda"
---

{%
assign filtered_posts = site.java-theme |
where_exp: "item", "item.url contains '/java-theme/lambda/'" |
sort: "sequence"
%}
<ol>
    {% for post in filtered_posts %}
    {% assign num = post.sequence | abs %}
    <li>
        <a href="{{ post.url }}">{{ post.title }}</a>
    </li>
    {% endfor %}
</ol>

## Reference

- [Translation of Lambda Expressions](http://cr.openjdk.java.net/~briangoetz/lambda/lambda-translation.html)

Baeldung

- [Functional Interfaces in Java 8](https://www.baeldung.com/java-8-functional-interfaces)
- [Lambda Expressions and Functional Interfaces: Tips and Best Practices](https://www.baeldung.com/java-8-lambda-expressions-tips)
- [Java 8 – Powerful Comparison with Lambdas](https://www.baeldung.com/java-8-sort-lambda)
- [Exceptions in Java 8 Lambda Expressions](https://www.baeldung.com/java-lambda-exceptions)
- [Guide to Java BiFunction Interface](https://www.baeldung.com/java-bifunction-interface)
- [Why Do Local Variables Used in Lambdas Have to Be Final or Effectively Final?](https://www.baeldung.com/java-lambda-effectively-final-local-variables)
- [Java 11 Local Variable Syntax for Lambda Parameters](https://www.baeldung.com/java-var-lambda-params)
- [Exceptions in Lambda Expression Using Vavr](https://www.baeldung.com/exceptions-using-vavr)
- [Java Stream Filter with Lambda Expression](https://www.baeldung.com/java-stream-filter-lambda)
- [Log4j 2 and Lambda Expressions](https://www.baeldung.com/log4j-2-lazy-logging)
- [Introduction to Lambda Behave](https://www.baeldung.com/lambda-behave)

Github

- [eugenp/tutorials](https://github.com/eugenp/tutorials/tree/master/core-java-modules/core-java-lambdas)

