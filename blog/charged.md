---
layout: default
---

## 带电离子的自由能校正

### 参考文献
[Niu 2020](<https://doi.org/10.1002/adfm.202008533>)
[Liu 2019](<https://doi.org/10.1021/acscatal.9b02179>)
[Guo 2018](<https://doi.org/10.1021/acscatal.7b01371>)
[Calle-Vallejo 2013](<https://doi.org/10.1039/C2CP44620K>)

### 为什么
在电催化硝酸盐还原NO3RR（electrocatalytic nitrate reduction）的理论计算中，自由能相对于溶液中的<img src="https://latex.codecogs.com/svg.image?\inline&space;\mathrm{NO}_{3}^{-}" title="\inline \mathrm{NO}_{3}^{-}" />离子能量。但是，DFT计算带电离子是相当不靠谱的。所以，<img src="https://latex.codecogs.com/svg.image?\inline&space;\mathrm{NO}_{3}^{-}" title="\inline \mathrm{NO}_{3}^{-}" />的自由能需要从气相<img src="https://latex.codecogs.com/svg.image?\inline&space;\mathrm{HNO}_{3}" title="\inline \mathrm{HNO}_{3}" />的自由能推导。DFT可以计算电中性气相分子<img src="https://latex.codecogs.com/svg.image?\inline&space;\mathrm{HNO}_{3}" title="\inline \mathrm{HNO}_{3}" />。

### 所以
根据[Niu(2020)](<https://doi.org/10.1002/adfm.202008533>)在[Supporting Information](<https://onlinelibrary.wiley.com/action/downloadSupplement?doi=10.1002%2Fadfm.202008533&file=adfm202008533-sup-0001-SuppMat.pdf>)在Page S2中给出的描述，<img src="https://latex.codecogs.com/svg.image?\inline&space;\mathrm{NO}_{3}^{-}" title="\inline \mathrm{NO}_{3}^{-}" />从如下两步反应得到：
<center><img src="https://latex.codecogs.com/svg.image?\mathrm{HNO}_{3}(\mathrm{g})&space;\overset{1}{\rightarrow}&space;\mathrm{HNO}_{3}(\mathrm{l})&space;" title="\mathrm{HNO}_{3}(\mathrm{g}) \overset{1}{\rightarrow} \mathrm{HNO}_{3}(\mathrm{l}) " /></center>
<center><img src="https://latex.codecogs.com/svg.image?\mathrm{HNO}_{3}(\mathrm{l})&space;\overset{2}{\rightarrow}&space;\mathrm{H}^{&plus;}(\mathrm{aq})&plus;\mathrm{NO}_{3}^{-}(\mathrm{aq})" title="\mathrm{HNO}_{3}(\mathrm{l}) \overset{2}{\rightarrow} \mathrm{H}^{+}(\mathrm{aq})+\mathrm{NO}_{3}^{-}(\mathrm{aq})" /></center>
接下来就只需要计算这两步反应的标准摩尔吉布斯反应自由能之和，就可以得到<img src="https://latex.codecogs.com/svg.image?\inline&space;\mathrm{NO}_{3}^{-}" title="\inline \mathrm{NO}_{3}^{-}" />相对于<img src="https://latex.codecogs.com/svg.image?\inline&space;\mathrm{HNO}_{3}" title="\inline \mathrm{HNO}_{3}" />的吉布斯自由能变化值。

计算第1步反应的自由能，只需要参考[CRC Handbook of Chemistry and Physics](<https://hbcp.chemnetbase.com/faces/contents/ContentsSearch.xhtml>)手册的5-29页，分别得到<img src="https://latex.codecogs.com/svg.image?\inline&space;\mathrm{HNO}_{3}(\mathrm{l})" title="\inline \mathrm{HNO}_{3}(\mathrm{l})" />和<img src="https://latex.codecogs.com/svg.image?\inline&space;\mathrm{HNO}_{3}(\mathrm{g})" title="\inline \mathrm{HNO}_{3}(\mathrm{g})" />的标准摩尔吉布斯生成自由能，单位<img src="https://latex.codecogs.com/svg.image?\inline&space;\mathrm{kJ\!\cdot\!mol^{-1}}" title="\inline \mathrm{kJ\!\cdot\!mol^{-1}}" />，摘录如下：

| Species | State |   G   |
|:-------:|:-----:|:-----:|
|   HNO3  |   l   | -80.7 |
|   HNO3  |   g   | -73.5 |

代入数据，计算第1步反应的吉布斯自由能变化值，单位eV：
```python
from ase.units import kJ, J, mol

G_HNO3_l = -80.7*kJ/mol
G_HNO3_g = -73.5*kJ/mol

G_1 = G_HNO3_l - G_HNO3_g
print(G_1) # -0.07462274093792332
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
H_H_aq = 0*kJ/mol
S_H_aq = 0*J/mol
H_H2_g = 0*kJ/mol
S_H2_g = 130.680*J/mol
T = 298.15

n_H_aq = 1
n_H2_g = -0.5

G_H_aq = (n_H_aq*H_H_aq+n_H2_g*H_H2_g) - T*(n_H_aq*S_H_aq+n_H2_g*S_H2_g)
print(G_H_aq) # 0.20190758966157468
```
计算出<img src="https://latex.codecogs.com/svg.image?\inline&space;\Delta_{\mathrm{f}}&space;G_{\mathrm{m}}^{\ominus}(\mathrm{H}^{&plus;})" title="\inline \Delta_{\mathrm{f}} G_{\mathrm{m}}^{\ominus}(\mathrm{H}^{+})" />为`(0-0.5*0)-298.15*(0-0.5*130.680)*1e-03`
同样地，根据这个反应式
<center><img src="https://latex.codecogs.com/svg.image?\frac{1}{2}\mathrm{N}_{2}(\mathrm{g},~p^{\ominus})&space;&plus;&space;\frac{3}{2}\mathrm{O}_{2}(\mathrm{g},~p^{\ominus})&space;&plus;&space;e^{-}&space;\rightarrow&space;\mathrm{NO}_{3}^{-}(\mathrm{aq},~p^{\ominus})" title="\frac{1}{2}\mathrm{N}_{2}(\mathrm{g},~p^{\ominus}) + \frac{3}{2}\mathrm{O}_{2}(\mathrm{g},~p^{\ominus}) + e^{-} \rightarrow \mathrm{NO}_{3}^{-}(\mathrm{aq},~p^{\ominus})" /></center>
即计算
<center><img src="https://latex.codecogs.com/svg.image?\Delta_{\mathrm{f}}&space;G_{\mathrm{m}}^{\ominus}(\mathrm{NO}_{3}^{-})&space;=&space;\Delta_{\mathrm{f}}&space;H_{\mathrm{m}}^{\ominus}(\mathrm{NO}_{3}^{-})&space;-&space;\frac{1}{2}\Delta_{\mathrm{f}}&space;H_{\mathrm{m}}^{\ominus}(\mathrm{N}_{2})&space;-&space;\frac{3}{2}\Delta_{\mathrm{f}}&space;H_{\mathrm{m}}^{\ominus}(\mathrm{O}_{2})&space;-&space;T\left(\Delta&space;S_{\mathrm{m}}^{\ominus}(\mathrm{NO}_{3}^{-})&space;-&space;\frac{1}{2}\Delta&space;S_{\mathrm{m}}^{\ominus}(\mathrm{N}_{2})&space;-&space;\frac{3}{2}\Delta&space;S_{\mathrm{m}}^{\ominus}(\mathrm{O}_{2})\right)" title="\Delta_{\mathrm{f}} G_{\mathrm{m}}^{\ominus}(\mathrm{NO}_{3}^{-}) = \Delta_{\mathrm{f}} H_{\mathrm{m}}^{\ominus}(\mathrm{NO}_{3}^{-}) - \frac{1}{2}\Delta_{\mathrm{f}} H_{\mathrm{m}}^{\ominus}(\mathrm{N}_{2}) - \frac{3}{2}\Delta_{\mathrm{f}} H_{\mathrm{m}}^{\ominus}(\mathrm{O}_{2}) - T\left(\Delta S_{\mathrm{m}}^{\ominus}(\mathrm{NO}_{3}^{-}) - \frac{1}{2}\Delta S_{\mathrm{m}}^{\ominus}(\mathrm{N}_{2}) - \frac{3}{2}\Delta S_{\mathrm{m}}^{\ominus}(\mathrm{O}_{2})\right)" /></center>
代入数据
```python
H_NO3_aq = -206.85*kJ/mol
S_NO3_aq = 146.70*J/mol
H_N2_g = 0*kJ/mol
S_N2_g = 191.609*J/mol
H_O2_g = 0*kJ/mol
S_O2_g = 205.152*J/mol
T = 298.15

n_NO3_aq = 1
n_N2_g = -0.5
n_O2_g = -1.5

G_NO3_aq = (n_NO3_aq*H_NO3_aq+n_N2_g*H_N2_g+n_O2_g*H_O2_g) - T*(n_NO3_aq*S_NO3_aq+n_N2_g*S_N2_g+n_O2_g*S_O2_g)
print(G_NO3_aq) # -1.3502092622062178
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

所以，根据反应式2，我们计算出电离能为30.09，
```python
G_2 = G_NO3_aq + G_H_aq - G_HNO3_l
print(G_2) # -0.3119051178654192
```
即0.312 eV。

### 参考
Sander, R.: Compilation of Henry's law constants (version 4.0) for water as solvent, Atmos. Chem. Phys., 15, 4399–4981, [https://doi.org/10.5194/acp-15-4399-2015](<https://acp.copernicus.org/articles/15/4399/2015/>), 2015.
[亨利定律常数表](<https://max.book118.com/html/2017/0528/109971917.shtm>)

[[Back]](../)
