---
title: "Gossip"
sequence: "105"
---

说明：Gossip 算法每个节点都是对等的，即没有角色之分。
Gossip 算法中的每个节点都会将数据改动告诉其他节点（类似传八卦）。
有话说得好："最多通过六个人你就能认识全世界任何一个陌生人"，因此数据改动的消息很快就会传遍整个集群。

步骤：

- 集群启动
- 某节点收到数据改动，并将改动传播给其他 4 个节点，传播路径表示为较粗的 4 条线
- 收到数据改动的节点重复上面的过程直到所有的节点都被感染