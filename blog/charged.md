---
layout: default
---

## 带电离子的自由能校正

### 参考文献
[Niu 2020](<https://doi.org/10.1002/adfm.202008533>)
[Liu 2019](<https://doi.org/10.1021/acscatal.9b02179>)
[Guo 2018](<https://doi.org/10.1021/acscatal.7b01371>)

### 为什么
电催化硝酸盐还原electrocatalytic nitrate reduction (NO3RR)的理论计算中涉及NO3-带电体系的计算，这个带电体系的能量是如何来的。

### 所以
考虑NO3是怎么来的
<center><img src="https://latex.codecogs.com/svg.image?\mathrm{HNO}_{3}(\mathrm{g})&space;\rightarrow&space;\mathrm{HNO}_{3}(\mathrm{l})" title="\mathrm{HNO}_{3}(\mathrm{g}) \rightarrow \mathrm{HNO}_{3}(\mathrm{l})" /></center>
<center><img src="https://latex.codecogs.com/svg.image?\mathrm{HNO}_{3}(\mathrm{l})&space;\rightarrow&space;\mathrm{H}^{&plus;}(\mathrm{aq})&plus;\mathrm{NO}_{3}^{-}(\mathrm{aq})" title="\mathrm{HNO}_{3}(\mathrm{l}) \rightarrow \mathrm{H}^{+}(\mathrm{aq})+\mathrm{NO}_{3}^{-}(\mathrm{aq})" /></center>
这样我们就从DFT可计算的气态HNO3，得到了NO3-物质。
接下来我们去计算它们的能量。
第一步反应参考CRC P5-29，摘录如下

| Species | State |   G   |
|:-------:|:-----:|:-----:|
|   HNO3  |   l   | -80.7 |
|   HNO3  |   g   | -73.5 |

由此可得，第一步反应的吉布斯自由能为
```python
from ase.units import kJ, mol
(-73.5-(-80.7))*kJ/mol
# 0.07462274093792334
```

接下来，我们从CRC P5-1和P5-29摘录数据如下

| Species | State |        H       |        S        |   G   | Page |
|:-------:|:-----:|:--------------:|:---------------:|:-----:|:----:|
|    H+   |   aq  |        0       |        0        |       |  5-1 |
|    H2   |   g   |        0       | 130.680 ± 0.003 |       |  5-1 |
|   NO3-  |   aq  | -206.85 ± 0.40 |  146.70 ± 0.40  |       |  5-1 |
|    N2   |   g   |        0       | 191.609 ± 0.004 |       |  5-1 |
|    O2   |   g   |        0       | 205.152 ± 0.005 |       |  5-1 |
|   HNO3  |   l   |     -174.1     |      155.6      | -80.7 | 5-29 |

我们发现，有些数据的<img src="https://latex.codecogs.com/svg.image?\inline&space;\Delta_{\mathrm{f}}&space;G_{\mathrm{m}}^{\ominus}" title="\inline \Delta_{\mathrm{f}} G_{\mathrm{m}}^{\ominus}" />没有给出，所以我们需要计算它们
标准摩尔吉布斯生成自由能的定义是从最稳定的单质给出，因此，我们可以根据这个反应式
<center><img src="https://latex.codecogs.com/svg.image?\frac{1}{2}\mathrm{H}_{2}(\mathrm{g},~p^{\ominus})&space;\rightarrow&space;\mathrm{H}^{&plus;}(\mathrm{aq},~p^{\ominus})&space;&plus;&space;e^{-}" title="\frac{1}{2}\mathrm{H}_{2}(\mathrm{g},~p^{\ominus}) \rightarrow \mathrm{H}^{+}(\mathrm{aq},~p^{\ominus}) + e^{-}" /></center>
即计算
<center><img src="https://latex.codecogs.com/svg.image?\Delta_{\mathrm{f}}&space;G_{\mathrm{m}}^{\ominus}(\mathrm{H}^{&plus;})&space;=&space;\Delta_{\mathrm{f}}&space;H_{\mathrm{m}}^{\ominus}(\mathrm{H}^{&plus;})&space;-&space;\frac{1}{2}\Delta_{\mathrm{f}}&space;H_{\mathrm{m}}^{\ominus}(\mathrm{H}_{2})&space;-&space;T\left(\Delta&space;S_{\mathrm{m}}^{\ominus}(\mathrm{H}^{&plus;})&space;-&space;\frac{1}{2}\Delta&space;S_{\mathrm{m}}^{\ominus}(\mathrm{H}_{2})\right)" title="\Delta_{\mathrm{f}} G_{\mathrm{m}}^{\ominus}(\mathrm{H}^{+}) = \Delta_{\mathrm{f}} H_{\mathrm{m}}^{\ominus}(\mathrm{H}^{+}) - \frac{1}{2}\Delta_{\mathrm{f}} H_{\mathrm{m}}^{\ominus}(\mathrm{H}_{2}) - T\left(\Delta S_{\mathrm{m}}^{\ominus}(\mathrm{H}^{+}) - \frac{1}{2}\Delta S_{\mathrm{m}}^{\ominus}(\mathrm{H}_{2})\right)" /></center>
代入数据
```python
H_H = 0*kJ/mol
S_H = 0*J/mol
H_H2 = 0*kJ/mol
S_H2 = 130.680*J/mol
T = 298.15

n_H = 1
n_H2 = -0.5

G_H = (n_H*H_H+n_H2*H_H2) - T*(n_H*S_H+n_H2*S_H2)
print(G_H) # 0.20190758966157468
```
计算出<img src="https://latex.codecogs.com/svg.image?\inline&space;\Delta_{\mathrm{f}}&space;G_{\mathrm{m}}^{\ominus}(\mathrm{H}^{&plus;})" title="\inline \Delta_{\mathrm{f}} G_{\mathrm{m}}^{\ominus}(\mathrm{H}^{+})" />为`(0-0.5*0)-298.15*(0-0.5*130.680)*1e-03`
同样地，根据这个反应式
<center><img src="https://latex.codecogs.com/svg.image?\frac{1}{2}\mathrm{N}_{2}(\mathrm{g},~p^{\ominus})&space;&plus;&space;\frac{3}{2}\mathrm{O}_{2}(\mathrm{g},~p^{\ominus})&space;&plus;&space;e^{-}&space;\rightarrow&space;\mathrm{NO}_{3}^{-}(\mathrm{aq},~p^{\ominus})" title="\frac{1}{2}\mathrm{N}_{2}(\mathrm{g},~p^{\ominus}) + \frac{3}{2}\mathrm{O}_{2}(\mathrm{g},~p^{\ominus}) + e^{-} \rightarrow \mathrm{NO}_{3}^{-}(\mathrm{aq},~p^{\ominus})" /></center>
即计算
<center><img src="https://latex.codecogs.com/svg.image?\Delta_{\mathrm{f}}&space;G_{\mathrm{m}}^{\ominus}(\mathrm{NO}_{3}^{-})&space;=&space;\Delta_{\mathrm{f}}&space;H_{\mathrm{m}}^{\ominus}(\mathrm{NO}_{3}^{-})&space;-&space;\frac{1}{2}\Delta_{\mathrm{f}}&space;H_{\mathrm{m}}^{\ominus}(\mathrm{N}_{2})&space;-&space;\frac{3}{2}\Delta_{\mathrm{f}}&space;H_{\mathrm{m}}^{\ominus}(\mathrm{O}_{2})&space;-&space;T\left(\Delta&space;S_{\mathrm{m}}^{\ominus}(\mathrm{NO}_{3}^{-})&space;-&space;\frac{1}{2}\Delta&space;S_{\mathrm{m}}^{\ominus}(\mathrm{N}_{2})&space;-&space;\frac{3}{2}\Delta&space;S_{\mathrm{m}}^{\ominus}(\mathrm{O}_{2})\right)" title="\Delta_{\mathrm{f}} G_{\mathrm{m}}^{\ominus}(\mathrm{NO}_{3}^{-}) = \Delta_{\mathrm{f}} H_{\mathrm{m}}^{\ominus}(\mathrm{NO}_{3}^{-}) - \frac{1}{2}\Delta_{\mathrm{f}} H_{\mathrm{m}}^{\ominus}(\mathrm{N}_{2}) - \frac{3}{2}\Delta_{\mathrm{f}} H_{\mathrm{m}}^{\ominus}(\mathrm{O}_{2}) - T\left(\Delta S_{\mathrm{m}}^{\ominus}(\mathrm{NO}_{3}^{-}) - \frac{1}{2}\Delta S_{\mathrm{m}}^{\ominus}(\mathrm{N}_{2}) - \frac{3}{2}\Delta S_{\mathrm{m}}^{\ominus}(\mathrm{O}_{2})\right)" /></center>
代入数据
```python
H_NO3 = -206.85*kJ/mol
S_NO3 = 146.70*J/mol
H_N2 = 0*kJ/mol
S_N2 = 191.609*J/mol
H_O2 = 0*kJ/mol
S_O2 = 205.152*J/mol
T = 298.15

n_NO3 = 1
n_N2 = -0.5
n_O2 = -1.5

G_NO3 = (n_NO3*H_NO3+n_N2*H_N2+n_O2*H_O2) - T*(n_NO3*S_NO3+n_N2*S_N2+n_O2*S_O2)
print(G_NO3) # -1.3502092622062178
```
计算出<img src="https://latex.codecogs.com/svg.image?\inline&space;\Delta_{\mathrm{f}}&space;G_{\mathrm{m}}^{\ominus}(\mathrm{NO}_{3}^{-})" title="\inline \Delta_{\mathrm{f}} G_{\mathrm{m}}^{\ominus}(\mathrm{NO}_{3}^{-})" />为`(-206.85-0.5*0-1.5*0)-298.15*(146.70-0.5*191.609-1.5*205.152)*1e-03`

然后我们就可以填完这张表格

| Species | State |        H       |        S        |    G    | Page |
|:-------:|:-----:|:--------------:|:---------------:|:-------:|:----:|
|    H+   |   aq  |        0       |        0        | 19.4811 |  5-1 |
|    H2   |   g   |        0       | 130.680 ± 0.003 |         |  5-1 |
|   NO3-  |   aq  | -206.85 ± 0.40 |  146.70 ± 0.40  | -130.28 |  5-1 |
|    N2   |   g   |        0       | 191.609 ± 0.004 |         |  5-1 |
|    O2   |   g   |        0       | 205.152 ± 0.005 |         |  5-1 |
|   HNO3  |   l   |     -174.1     |      155.6      |  -80.7  | 5-29 |

所以，根据反应式2，我们计算出电离能为30.09，即0.312 eV。

### 参考
Sander, R.: Compilation of Henry's law constants (version 4.0) for water as solvent, Atmos. Chem. Phys., 15, 4399–4981, [https://doi.org/10.5194/acp-15-4399-2015](<https://acp.copernicus.org/articles/15/4399/2015/>), 2015.
[亨利定律常数表](<https://max.book118.com/html/2017/0528/109971917.shtm>)

[[Back]](../)
