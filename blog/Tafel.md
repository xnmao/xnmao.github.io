---
layout: default
---

## 使用Tafel斜率推断反应机理

### 计算公式

Tafel斜率<img src="https://latex.codecogs.com/svg.image?\inline&space;b" title="\inline b" />对应于表观电子转移数。表观电子转移数包含基元速控步骤RDS（rate-determining step）的电子转移数<img src="https://latex.codecogs.com/svg.image?\inline&space;\alpha^{\ast}" title="\inline \alpha^{\ast}" />和基元RDS之前的步骤电子转移总数<img src="https://latex.codecogs.com/svg.image?\inline&space;n" title="\inline n" />。它们的关系式为
<center><img src="https://latex.codecogs.com/svg.image?b&space;=&space;\frac{2.303RT}{\left(\alpha^{\ast}&plus;n\right)F" title="b = \frac{2.303RT}{\left(\alpha^{\ast}+n\right)F" /></center>
如果基元RDS转移了1个电子，则<img src="https://latex.codecogs.com/svg.image?\inline&space;\alpha^{\ast}" title="\inline \alpha^{\ast}" />等于0.5；如果基元RDS转移了0个电子，则<img src="https://latex.codecogs.com/svg.image?\inline&space;\alpha^{\ast}" title="\inline \alpha^{\ast}" />等于0。

### 实际应用

例如，某电极表面电化学反应的基元RDS不转移电子（非电化学过程），且在基元RDS之前的反应步骤中，已经转移了2个电子。则代入方程计算可得Tafel斜率的理论值为29.6 mV。
```python
import numpy as np
from ase.units import kB

def get_Tafel_slope(electron_transfer_in_RDS, n_transferred, T=298.15):
    alpha_ast = 0.5 if electron_transfer_in_RDS else 0
    b = np.log(10)*kB*T/(alpha_ast+n_transferred)
    return b*1e+03 # V -> mV

b = get_Tafel_slope(electron_transfer_in_RDS=False, n_transferred=2)
print(b) # 29.579664802345658
```

反过来可以使用手册速查，如果实验测得Tafel斜率为112 mV，则可以推测基元RDS转移了1个电子，并且基元RDS之前没有转移电子。如果实验测得Tafel斜率是74 mV，这有可能是多个机理混合。

#### 速查手册

n_electron是基元RDS之前的步骤电子转移总数，chem代表基元RDS非电化学基元反应（不转移电子），<u>e-chem</u>代表基元RDS是电化学基元反应（转移1个电子）。

| n_electron | reaction | b/mV |   reaction    |    b/mV    |
|:----------:|:--------:|:----:|:-------------:|:----------:|
|      0     |   chem   |  NaN | <u>e-chem</u> |  <u>118<u> |
|      1     |   chem   |  59  | <u>e-chem</u> |  <u>39<u>  |
|      2     |   chem   |  30  | <u>e-chem</u> |  <u>24<u>  |
|      3     |   chem   |  20  | <u>e-chem</u> |  <u>17<u>  |
|      4     |   chem   |  15  | <u>e-chem</u> |  <u>13<u>  |
|      5     |   chem   |  12  | <u>e-chem</u> |  <u>11<u>  |
|      6     |   chem   |  10  | <u>e-chem</u> |   <u>9<u>  |
|      7     |   chem   |   8  | <u>e-chem</u> |   <u>8<u>  |
|      8     |   chem   |   7  | <u>e-chem</u> |   <u>7<u>  |
|      9     |   chem   |   7  | <u>e-chem</u> |   <u>6<u>  |

### 注意事项

电极表面的化学反应中，中间体的物种变化是一个闭合的循环。反应的第1步不一定是洁净的表面，也有可能被中间体占据。这就有必要对基元反应重新编号，才能正确地计算基元RDS之前的步骤电子转移总数。详见[Exner 2020](<https://pubs.acs.org/doi/10.1021/acscatal.0c03865>)。

### 参考资料

[【电化学】浅谈塔菲尔动力学(Tafel Kinetics)](<https://blog.sciencenet.cn/blog-3436572-1239198.html>)

[[Back]](../)
