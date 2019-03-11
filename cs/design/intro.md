架构设计
---

这里讨论大型、复杂的软件系统的设计；这些软件系统的特征是：单个开发者要理解所有方面会非常困难，几乎是不可能的。不准确的说，这些系统的复杂性超出了人类智能的范围。

复杂性常常以层次结构的形式存在。复杂的系统由一些相关的子系统组成，这些子系统又有自己的子系统，如此下去，直到达到某种最低层次的基本组件

复杂系统的架构是它所有的组件及其层次结构的函数

<div class="alert alert-info">
设计的目的是创建一个干净的，相对简单的内部结构，有时候也称为架构...
</div>

### 软件设计方法学

关于复杂系统的设计，不存在所谓的指南手册; 设计这样的系统需要增量和迭代的过程

<div class="alert alert-info">
一个好的设计方法基于牢固的理论基础，同时又提供艺术创新的自由
</div>

* (自顶向下)结构化设计方法
    
    利用算法作为基础构建块来构建复杂系统，适合设计计算密集型的系统

* 面向对象设计方法
    
    利用类和对象（抽象+封装/信息隐藏+层级结构）作为基础构建块；用对象来做模拟是威力强大的，也很直观，这是因为它非常符合我们对身处其中并与之交流的世界的看法。
    推荐阅读 [1] 第 3 章：模块化、对象和状态，[2] 第 2 章：对象模型

* [面向服务设计方法](microservice/intro.md)
    
    系统设计的时候考虑分布式，利用服务作为基础构建块，推荐阅读 [6] Building Microservice 微服务设计


### Design Principle

* Design for Failure

* Design for HA (MTBF & MTTR)

* Design for Scalability

* K.I.S.S (Keep It Simple Stupid)


## 进一步阅读

理论基础

* [1] Structure and Interpretation Of Computer Programs
    
    计算机程序的构造与解释；前三章：构造过程抽象，构造数据抽象，模块化、对象和状态
    
* [2] Grady Booch: Object-oriented Analysis and Design with Applications

    面向对象分析与设计，UML 创始人 Grady Booch 的代表作之一；其第 1 章：复杂性，非常值得一读
    
- - -

工程实践

* [3] Eric S. Raymond: The Art of UNIX Programming
    
    Unix 编程艺术

* [4] 人月神话
    
* [5] The Design of Design: Essays from a Computer Scientist
    
    设计原本

* [6] Building Microservices 微服务设计

- - -

* [7] Beautiful Architecture

* [8] Beautiful Code

* [The Architecture of Open Source Applications](http://aosabook.org/en/index.html)

- - -

Online Blogs

* [Martin Fowler](https://martinfowler.com)

