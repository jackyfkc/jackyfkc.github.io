LogCabin
---

LogCabin is a distributed storage system built on Raft that provides a small amount of highly replicated, consistent storage


Structure
---

* Server
    * RaftService.cc 实现 RPC 协议, RequestVote, AppendEntries, InstallSnapshot

    * ServerStats.cc 统计服务信息, 主要用于诊断, 排查问题



Reference
---

* [Github Source Code](https://github.com/logcabin/logcabin)
