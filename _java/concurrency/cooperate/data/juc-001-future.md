---
title: "JUC Future"
sequence: "101"
---

[UP](/java-concurrency.html)

```java
import java.util.concurrent.ExecutionException;
import java.util.concurrent.ExecutorService;
import java.util.concurrent.Executors;
import java.util.concurrent.Future;

public class HelloWorld {

    public static void main(String[] args) throws ExecutionException, InterruptedException {
        ExecutorService pool = Executors.newSingleThreadExecutor();

        Future<Integer> future = pool.submit(() -> {
            LogUtils.color("calculate result");
            Thread.sleep(1000);
            return 5 * 10;
        });


        LogUtils.color("future class : {}", future.getClass().getName());
        LogUtils.color("future result: {}", future.get());

        pool.shutdown();
    }

}
```

```text
332   [main]             INFO  LogUtils - future class : java.util.concurrent.FutureTask
332   [pool-1-thread-1]  INFO  LogUtils - calculate result
1344  [main]             INFO  LogUtils - future result: 50
```

## Reference

- [Guide to java.util.concurrent.Future](https://www.baeldung.com/java-future)
- [Difference Between a Future and a Promise in Java](https://www.baeldung.com/java-future-vs-promise-comparison)
