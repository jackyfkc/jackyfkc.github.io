Leader Election 选举
---

* Select one server to act as leader

* Detect crashes, choose new leader


## Introduction

Raft uses a `heartbeat` mechanism to trigger leader election. When server start up, they begin as `followers`.

Raft 使用心跳机制来触发 leader 选举. 当服务启动时, 其状态为 follower.

To begin an election, a `follower` increment its current term and transitions to `candidate` state. It then votes for itself and issues `RequestVote` RPC in parallel to each of the other servers in the cluster.

* A `candidate` wins an election if it receivers votes from `a majority of` the servers if the full cluster for the same term

* Each server will vote for `at most one` candidate in a given term, on a first-come-first-served basis

* Raft uses randomized `election timeouts` to ensure that `split votes` are rare and that they are resolved quickly


在 Raft 中有二个超时设置控制着 Leader 选举. 第一个是 election timeout, 决定了一个 follower 等待成为 candidate 的时间. election timeout 在某个区间内取随机值 (通常是 150ms, 300ms).

Follower 在等待完 election timeout 时间后, follower 会开始一轮新的选举: follower 将当前 term 加 1, 并且切换到 candidate 状态. 它选举自己并发送 RequestVote RPC 请求给集群的其他节点.


## Election Restriction

In any leader-based consensus algorithm, the leader must eventually store all of committed log entries.

Raft uses the voting process to prevent a candidate from winning an election unless its log contains all committed entries.

