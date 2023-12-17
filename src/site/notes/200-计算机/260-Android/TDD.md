---
{"dg-publish":true,"permalink":"/200-计算机/260-Android/TDD/","tags":["Android/Test"],"noteIcon":""}
---



TDD，全称为测试驱动开发（Test-Driven Development），是一种软件开发方法论。在 TDD 中，开发人员通过编写测试用例来指导和驱动软件的开发过程。

## TDD

> Test-Driven Development  
> 测试驱动开发  
> 写代码只为修复失败了的测试

### 核心

> 强调现在，拒绝过度设计

### 周期

> 测试-编码-重构

![](https://i.imgur.com/5V2dJsk.png)


## ATDD
- Acceptance [[200-计算机/260-Android/TDD\|TDD]]验收测试驱动开发
- 看得见摸得着的软件
- 建立信任及信心
- 客户做主
- 培养共同语言

## **AAA测试**
```plaintext
@Test
fun `test`() {
    //Assemble 创建测试所需的所有对象和变量
    //Act 执行要测试的行为
    //Assert  测试最终结果
}
```

>


## 参考资料
[TDD in Android : Test Driven Development Tutorial with Android | BrowserStack](https://www.browserstack.com/guide/tdd-in-android)
[Android单元测试学习之 Junit4_51CTO博客_junit单元测试步骤](https://blog.51cto.com/u_15719342/5475388)
[Test-Driven Development with Android - WWT](https://www.wwt.com/blog/test-driven-development-with-android)