Storm 内幕
---

这里讲述 Storm 的工作机制；主要针对版本 2.0, 2.0 与之前版本的一个很大区别是核心模块全用 Java 重写，替代之前的 Clojure


对于一个完全新的系统，我们如何去深入了解它呢？我一般会如下去做

0. 下载 Storm，安装部署，先起一个 Demo，从用户的角度了解它

1. 搜索引擎查找作者发表的论文或文章，博客等

2. 官方网站找文档（通常内容是比较可靠的）


通过以上 3 步，我们可以大概知道 Storm 的发展历程，主要设计思想，整体架构. 

从测试的角度来看，以上都是通过黑盒的方式去熟悉系统，接下来我们可以考虑开始阅读源码了. 阅读的目的：一是了解 Storm 的工作机制， 二是可以了解别人使用Java 的方式, 期望从中学到一些好的经验


阅读源码是件着实费心费力的事，所以掌握一定的技巧是有必要的，一般分 2 种做法

**自顶向下**
    
了解整个 Storm 整体架构，代码结构，然后分而治之，分 Nimbus, Supervisor, UI, LogViewer

Nimbus 的高可用 HA，调度 Scheduler

Supervisor Worker Executor 


**自底向上**

熟悉基本功能模块，比如 Storm 配置，日志 log4J，指标收集 DropWizard，组件间通信 Netty 等

带着问题去阅读，从 Jira, Stackoverflow 上可以看到 Storm 相关的一些 issue 或者 bug，可以从它们入手，来熟悉代码



## 附录

* Storm 依赖的三方库

