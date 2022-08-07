---
layout: default
---

## 塔菲尔斜率推断反应机理

塔菲尔斜率对应于表观电子转移数。表观电子转移数包含基元速控步骤RDS（rate-determining step）的电子转移数<img src="https://latex.codecogs.com/svg.image?\inline&space;\alpha^{\ast}" title="\inline \alpha^{\ast}" />和RDS之前的步骤电子转移数<img src="https://latex.codecogs.com/svg.image?\inline&space;n" title="\inline n" />。
总反应的塔菲尔斜率即等于
<center><img src="https://latex.codecogs.com/svg.image?b&space;=&space;\frac{2.303RT}{\left(\alpha^{\ast}&plus;n\right)F" title="b = \frac{2.303RT}{\left(\alpha^{\ast}+n\right)F" /></center>

如果RDS转移了1个电子，则<img src="https://latex.codecogs.com/svg.image?\inline&space;\alpha^{\ast}" title="\inline \alpha^{\ast}" />等于0.5；如果RDS转移了0个电子，则<img src="https://latex.codecogs.com/svg.image?\inline&space;\alpha^{\ast}" title="\inline \alpha^{\ast}" />等于0。

例如，某电极表面反应的RDS不转移电子（非电化学过程），在RDS之前，已经转移了2个电子。
则可代入方程计算得Tafel斜率的理论值为29.6 mV。
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

反过来，如果实验测得Tafel斜率为112 mV，则可以推测RDS转移了1个电子，并且RDS之前没有电子转移过程。

### 速查手册

| n_electron | reaction | b/mV |     **reaction**    | **b/mV** |
|:----------:|:--------:|:----:|:-------------------:|:--------:|
|      0     | chemical |  NaN | **electrochemical** |  **118** |
|      1     | chemical |  59  | **electrochemical** |  **39**  |
|      2     | chemical |  30  | **electrochemical** |  **24**  |
|      3     | chemical |  20  | **electrochemical** |  **17**  |
|      4     | chemical |  15  | **electrochemical** |  **13**  |
|      5     | chemical |  12  | **electrochemical** |  **11**  |
|      6     | chemical |  10  | **electrochemical** |   **9**  |
|      7     | chemical |   8  | **electrochemical** |   **8**  |
|      8     | chemical |   7  | **electrochemical** |   **7**  |
|      9     | chemical |   7  | **electrochemical** |   **6**  |

[[Back]](../)
