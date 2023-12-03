---
{"dg-publish":true,"permalink":"/Junit5/","tags":["Android/Test"],"noteIcon":""}
---

JUnit5 是一个用于进行 Java 单元测试的开源测试框架。它是 JUnit 测试框架的最新版本。

## 常用注解

| 注解 | 说明 | 
| --- | --- | 
| `@Test` | 标记一个测试方法。 |
| `@BeforeEach` | 在每个测试方法之前执行的方法。 | 
| `@AfterEach` | 在每个测试方法之后执行的方法。 | 
| `@BeforeAll` | 在所有测试方法之前执行的方法（静态方法）。 |
| `@AfterAll` | 在所有测试方法之后执行的方法（静态方法）。 | 
| `@DisplayName` | 为测试类或测试方法提供自定义的显示名称。 | 
| `@Disabled` | 禁用一个测试类或测试方法。 |
| `@RepeatedTest` | 标记一个重复执行的测试方法。 | 
| `@ParameterizedTest` | 标记一个参数化测试方法。 |
| `@ValueSource` | 提供一个简单的值源，用于参数化测试。 |
| `@CsvSource` | 提供一个 CSV 格式的值源，用于参数化测试。 |
| `@MethodSource` | 提供一个方法引用作为值源，用于参数化测试。 |
| `@Timeout` | 设置测试方法的超时时间。 |
| `@Tag` | 为测试方法添加标签，用于分组、筛选或排除测试。 |
| `@Nested` | 嵌套测试类，用于组织和管理相关的测试。 | 
| `@TestInstance` | 控制测试实例的生命周期。 |
| `@TestFactory` | 提供一个工厂方法来动态生成测试用例。 |
| `@ExtendWith` | 注册扩展，用于自定义测试行为和功能。 |


## 断言
| 断言 | 说明 |
| --- | --- |
| `assertEquals(expected, actual)` | 判断两个值是否相等。 | 
| `assertNotEquals(expected, actual)` | 判断两个值是否不相等。 |
| `assertTrue(condition)` | 判断给定条件是否为真。 |
| `assertFalse(condition)` | 判断给定条件是否为假。 | 
| `assertNull(object)` | 判断给定对象是否为 null。 |
| `assertNotNull(object)` | 判断给定对象是否不为 null。 |
| `assertSame(expected, actual)` | 判断两个对象是否为同一个引用。 |
| `assertNotSame(expected, actual)` | 判断两个对象是否不是同一个引用。 | 
| `assertArrayEquals(expectedArray, actualArray)` | 判断两个数组是否相等。 | 
| `assertIterableEquals(expectedIterable, actualIterable)` | 判断两个可迭代对象是否相等。 |
| `assertThrows(expectedException, executable)` | 判断给定的代码块是否抛出了预期的异常。 |
| `assertTimeout(duration, executable)` | 判断给定的代码块是否在指定的时间内执行完成。 | 
| `assertAll(executables)` | 用于同时执行多个断言，并将所有断言的结果收集起来。 |


## Android项目中集成
在`app`目录下的`gradl`文件中添加如下依赖：
```
testImplementation 'org.junit.jupiter:junit-jupiter-api:5.7.1'  
testRuntimeOnly 'org.junit.jupiter:junit-jupiter-engine:5.7.1'
```

## 参考资料
