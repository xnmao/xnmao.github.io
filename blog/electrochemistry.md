---
layout: default
---

## 电化学笔记

### 电极材料的稳定性评估

#### 在反应条件下材料是否会溶解为离子
参考文献[RuN2 Monolayer: A Highly Efficient Electrocatalyst for Oxygen Reduction Reaction](<https://doi.org/10.1021/acsami.0c11824>)的Supporting Information中，Page S2-S3给出了RuN2在酸性ORR条件下是否溶解的判断依据，对应文章3.1节倒数第2段的讨论。  
公式中，U^0，即standard dissolution potential，对应金属Ru的值为0.46 V，这个值可以从CRC Handbook of Chemistry and Physics手册的5-78页查到。  
公式后半部分相当于使用体相的Ru作为参比，计算了RuN2的Ru缺陷形成能。然后除以转移电子数，其数值等于溶液中一个Ru离子所带正电荷数。  
计算得到的U\_dis为0.10 V，将该数值与工作电位对比，如果它高于工作电位，则材料稳定。在这个工作中，ORR的理论工作电位是-η (-0.33 V)，低于U\_dis，因此材料稳定。  
现在，我有两个问题：
1. 这个公式可以通过kTln[H+]外推到碱性条件吗？可以的话，如何修改公式，这样得到的结果会不会与酸性条件相同？
2. ORR的工作电位怎么理解？为什么不与0 V或者applied potential 1.23 V对比？在HER/OER/CO2RR中，都是直接与理论过电势对比吗？

[[Back]](../)
