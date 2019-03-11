FAQ
---

* Zookeeper 集群可以只有 2 个节点吗?

    可以, 但是不推荐这么做; ZK 默认需要过半数的节点才可以正常工作, 如果集群只有 2 个节点, 那么 1 个节点故障, 就会导致整个集群无法工作; 因此 ZK 建议集群至少有 3 个节点, 以容忍 1 个节点故障;

    此外建议节点个数应为奇数; 3 个节点的集群和 4 个节点的集群都只能容许 1 个节点的故障, 但前者的仲裁数量为 2, 后者为 3; 因为写操作的吞吐量取决于仲裁数量的大小的缘故, 3 个(奇数)节点的配置相对更优

    https://stackoverflow.com/questions/49077857/can-two-machines-be-used-for-zookeeper-cluster/49106044#49106044

    相关代码见 Github [parseDynamicConfig() in QuorumPeerConfig.java](https://github.com/apache/zookeeper/blob/master/src/java/main/org/apache/zookeeper/server/quorum/QuorumPeerConfig.java#L643)

