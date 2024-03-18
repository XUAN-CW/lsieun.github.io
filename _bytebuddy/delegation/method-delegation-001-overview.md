---
title: "Method Delegation: Overview"
sequence: "101"
---

{:refdef: style="text-align: center;"}
![](/assets/images/beauty/mirror-mirror-on-the-wall.jpg)
{:refdef}

TODO：

- [ ] @RuntimeType 是做什么用的呢？ 被 @RuntimeType 标记的方法，就是拦截的方法；此时方法签名或返回值，可以与被拦截方法不一致
- [ ] 代理的目标：
    - [ ] 可以 delegation 给类，也可以 delegation 到具体的对象
- [ ] 寻找匹配的方法
  - [ ] 完全匹配
  - [ ] 不完全匹配
  - [ ] 注解
- 不使用 `@SuperCall`，而使用 call.invoke(instance) 会限入递归循环，无法退出
- 动态修改入参 
  - @Morph
- @SuperClass 不能用 redefine，因为 redefine 不保留原始方法


我觉得，方法有返回值，是“多数情况”，返回 `void` 可以看成是特殊情况。

