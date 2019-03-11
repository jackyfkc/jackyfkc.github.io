Fault Tolerance
---


## Failure Models

To get a better grasp on how serious a failure actually is, several classification schemes have been developed.

在分布式系统中, 故障可能发生在节点或者通信链路上, 为了区分故障的严重程度, 我们使用一些分类方法, 基于 Cristian 1991 和 Hadzilacos, Toueg 1993 描述的方法


* Byzantine Failures

    也被称为拜占庭故障; 这是最难处理的情况, 一个节点压根就不按照正常程序逻辑执行, 可能会产生随机的输出. 要解决拜占庭式故障需要有同步网络, 并且故障节点必须小于 1/3, 通常只有对可靠性有很高要求时才会考虑通过高冗余率来消除故障.

* Crash-Recovery Failures

    它比 byzantine 类故障加了一个限制, 那就是节点总是按照程序逻辑执行, 结果是正确的. 但是不保证消息返回的时间. 原因可能是 crash 后重启了, 网络中断了, 异步网络中的高延迟. 对于 crash 的情况还要分健忘 (amnesia) 和非健忘的两种情况. 对于健忘的情况, 是指这个 crash 的节点重启后没有完整的保存 crash 之前的状态信息, 非健忘是指这个节点 crash 之前能把状态完整的保存在持久存储上, 启动之后可以再次按照以前的状态继续执行和通信.

* Omission Failures

    比 crash-recovery 多了一个限制, 就是一定要非健忘. 有些算法要求必须是非健忘的. 比如最基本版本的 Paxos 要求节点必须把 ballot number 记录到持久存储中, 一旦 crash, 修复之后必须继续记住之前的 ballot number.

* Crash-Stop failures

    也叫做 crash failure 或者 fail-stop failures, 它比 omission failure 多了一个故障发生后要停止响应的要求. 比如一个节点出现故障后立即停止接受和发送所有消息, 或者网络发生了故障无法进行任何通信, 并且这些故障不会恢复. 简单讲, 一旦发生故障, 这个节点 就不会再和其它节点有任何交互. 就像它的名字描述的那样, crash and stop.


这四种故障中, 拜占庭式故障是非常难以解决的, Leslie Lamport 证明在同步网络下,有办法验证消息真伪, 故障节点不超过 1/3 的情况下才有可能解决


在设计一个分布式系统时，必须考虑清楚要应对的故障类别. Birman 在 Guide to Reliable Distributed Systems 一书中认为，一般来说我们不需要应对拜占庭故障. 他引用了在 Yahoo! 完成的工作，得出一个结论：崩溃失效比 Byzantine Failures 更为常见.


...


## Further Readings

*