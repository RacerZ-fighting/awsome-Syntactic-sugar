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

- Lambda 配合 forEach 方法使用：

  ```java
  // 循环遍历 map 当中的键值对 (var, value) 并执行 lambda 表达式
  fact.forEach(((var, value) -> {
              target.update(var, meetValue(value, target.get(var)));
          }));
  ```

- Predicate: 接受一个输入参数返回一个布尔值结果

- Consumer: 接受一个输入参数并且无返回的操作

- Function: 接受一个输入参数 T，返回一个结果 R

### 3. Streams 流

```cpp
// 代码片段截取自 Tai-e [https://github.com/pascal-lab/Tai-e]
ir.getParams()
		.stream()
		.filter(Exps::holdsInt)
		.forEach(p -> entryFact.update(p, Value.getNAC()));
```

`filter()` 方法接收的是一个 Predicate 类型的参数，`forEach()` 方法接收的是一个 Consumer 类型的参数

```java
Stream<Integer> stream = list.stream().map(String::length);
        stream.forEach(System.out::println);

cfg.getOutEdgesOf(stmt)
                    .stream()
                    .filter(edge -> !isUnreachableEdge(edge, constants))   // 在遍历 CFG 时，我们不进入相应的不可达分支
                    .map(Edge::getTarget)
                    .forEach(target -> {
                        if (!isVisited.contains(target)) {
                            queue.add(target);
                        }
                    });
```

`map()` 方法接收的是一个 Function 类型的参数

```java
boolean anyMatchFlag = list.stream().anyMatch(element -> element.contains("王"));
///
return switchStmt.getCaseValues()
                     .stream()
                     .anyMatch(x -> x == v);
```

`anyMatch()`，只要有一个元素匹配传入的条件，就返回 true

```java
String[] strArray = list.stream().toArray(String[]::new);	
List<Integer> list1 = list.stream().map(String::length).collect(Collectors.toList());
List<String> list2 = list.stream().collect(Collectors.toCollection(ArrayList::new));
String str = list.stream().collect(Collectors.joining(", ")).toString();
```

把一个集合按照某种规则转成另外一个集合的时候，可以配套使用 `map()` 方法和 `collect()` 方法

```java
Value value = edge.getReturnVars()
                        .stream()
                        .map(returnOut::get)    // 拿到 fact value
                        .reduce(Value.getUndef(), cp::meetValue);
```

`reduce()` 可以合并流的元素并产生单个值，左面为初始化的值，右边为迭代的函数

### 参考链接

- [Java 8 Optional最佳指南：解决空指针问题的优雅之选 | 二哥的Java进阶之路 (javabetter.cn)](https://javabetter.cn/java8/optional.html)



