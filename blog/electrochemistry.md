---
layout: default
---

## 电化学笔记

### 电极材料的稳定性评估

#### 在反应条件下电极材料是否会溶解为离子
参考文献[RuN2 Monolayer: A Highly Efficient Electrocatalyst for Oxygen Reduction Reaction](<https://doi.org/10.1021/acsami.0c11824>)的[Supporting Information](<https://pubs.acs.org/doi/suppl/10.1021/acsami.0c11824/suppl_file/am0c11824_si_001.pdf>)中，Page S2-S3给出了RuN2在酸性ORR条件下是否溶解的判断依据，对应文章3.1节倒数第2段的讨论。  
公式中，<img src="http://latex.codecogs.com/svg.latex?U^{0}" />，即standard dissolution potential，对应金属Ru的值为0.46 V，这个值可以从[CRC Handbook of Chemistry and Physics](<https://hbcp.chemnetbase.com/faces/contents/ContentsSearch.xhtml>)手册的5-78页查到。  
公式后半部分相当于使用体相的Ru作为参比，计算了RuN2的Ru缺陷形成能。然后除以转移电子数，其数值等于溶液中一个Ru离子所带正电荷数。  
计算得到的<img src="http://latex.codecogs.com/svg.latex?U_{\rm{dis}}" />为0.10 V，将该数值与工作电位对比，如果它高于工作电位，则材料稳定。在这个工作中，ORR的理论工作电位是-η (-0.33 V)，低于<img src="http://latex.codecogs.com/svg.latex?U_{\rm{dis}}" />，因此材料稳定。

现在，我有两个问题：1. 这个公式可以通过<img src="http://latex.codecogs.com/svg.latex?k_{\rm{B}}T\ln[\rm{H^{+}}]" />外推到其它pH条件吗？可以的话，如何修改公式？这样得到的结果会不会与酸性条件相同？2. ORR的工作电位怎么理解？为什么不与0 V或者applied potential 1.23-0.33=0.9 V对比？在HER/OER/CO2RR中，都是直接与理论过电势对比吗？

https://doi.org/10.1016/j.electacta.2007.02.082

### 

Previous studies suggested that the effects of one water layer on adsorbates is basically equivalent with more layers.
原句出自
<https://doi.org/10.1021/acs.jpclett.1c03851>
的SI第2页Computational Details的第2段
<https://doi.org/10.1016/j.mtadv.2020.100091>
<https://pubs.acs.org/doi/full/10.1021/acs.jpcc.7b02383>


[[Back]](../)
