---
{"dg-publish":true,"permalink":"/200-计算机/260-Android/MVC/","tags":["Android/架构"],"noteIcon":""}
---

一种代码很耦合的架构，业务逻辑、数据处理、UI交互逻辑全部都杂糅在单个的Activity中。
导致Activity异常的臃肿，动不动就是几百上千行。且耦合性太强不便于维护和复用。通常修改UI时，业务逻辑和数据处理也要跟着变动。
## Model
主要负责处理数据

## View
主要指XML文件

## Controller
主要负责处理业务逻辑，通常都是指☞[[200-计算机/260-Android/Activity\|Activity]]和[[200-计算机/260-Android/Fragment\|Fragment]]。