### 1. Optional

**insight:** 避免没有必要的 null 值检查

判 null 的表达式转换为：

```java
Optional<String> optOrNull = Optional.ofNullable(null);
System.out.println(optOrNull.isPresent()); // 输出：false
```

更优雅的使用：`ifPresent()` 与 lambda 表达式的配合使用

```java
Optional<String> opt = Optional.of("xxx");
opt.ifPresent(str -> System.out.println(str.length()));
```

Optional 正确获取值的方式：`orElseGet` 支持函数式编程

```java
String name = Optional.ofNullable(name).orElseGet(OrElseOptionalDemo::getDefaultValue);
```

### 2. Lambda表达式

> `@FunctionalInterface`
>
> Note that instances of functional interfaces can be created with lambda expressions, method references, or constructor references.

### 参考链接

- [Java 8 Optional最佳指南：解决空指针问题的优雅之选 | 二哥的Java进阶之路 (javabetter.cn)](https://javabetter.cn/java8/optional.html)



