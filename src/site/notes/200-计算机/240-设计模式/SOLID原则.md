---
{"dg-publish":true,"permalink":"/200-计算机/240-设计模式/SOLID原则/","tags":["设计模式"],"noteIcon":""}
---



### S：单依职责原则
- Single Responsibility Principle
- 修改一个类的原因只能有一个。

### O：开闭原则
- Open/closed Principle
- 对于扩展，类应该是“开放”的；对于修改，类则应是“封闭”的。

### L：里氏替换原则
- Liskov Substitution Principle
- 当你扩展一个类时， 记住你应该要能在不修改客户端代码的情况下将子类的对象作为父类对象进行传递。

#### 子类方法的参数类型必须与其超类的参数类型相匹配或更加抽象
#### 子类方法的返回值类型必须与超类方法的返回值类型或是其子类别相匹配。
#### 子类中的方法不应抛出基础方法预期之外的异常类型。
#### 子类不应该加强其前置条件。
#### 子类不能削弱其后置条件。

### I：接口隔离原则
- Interface Segregation Principle
- 客户端不应被强迫依赖于其不使用的方法。


### D：依赖倒置原则
- Dependency Inversion Principle
- 高层次的类不应该依赖于低层次的类。 两者都应该依赖于抽象接口。 抽象接口不应依赖于具体实现。 具体实现应该依赖于抽象接口。