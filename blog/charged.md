---
layout: default
---

## 带电离子的自由能校正方法

电催化硝酸盐还原NO3RR（electrocatalytic nitrate reduction）的理论计算所考虑的吉布斯自由能，是相对于溶液中的<img src="https://latex.codecogs.com/svg.image?\inline&space;\mathrm{NO}_{3}^{-}" title="\inline \mathrm{NO}_{3}^{-}" />离子能量。但是，DFT计算带电离子是相当不靠谱的。所以，<img src="https://latex.codecogs.com/svg.image?\inline&space;\mathrm{NO}_{3}^{-}" title="\inline \mathrm{NO}_{3}^{-}" />的自由能需要从气相<img src="https://latex.codecogs.com/svg.image?\inline&space;\mathrm{HNO}_{3}" title="\inline \mathrm{HNO}_{3}" />的自由能推导。DFT可以计算电中性气相分子<img src="https://latex.codecogs.com/svg.image?\inline&space;\mathrm{HNO}_{3}" title="\inline \mathrm{HNO}_{3}" />。NO3RR相关文献可参考[Niu(2020)](<https://doi.org/10.1002/adfm.202008533>)、[Liu(2019)](<https://doi.org/10.1021/acscatal.9b02179>)、[Guo(2018)](<https://doi.org/10.1021/acscatal.7b01371>)、[Calle-Vallejo(2013)](<https://doi.org/10.1039/C2CP44620K>)。这篇文章的目的是复现[Niu(2020)](<https://doi.org/10.1002/adfm.202008533>)在[Supporting Information](<https://onlinelibrary.wiley.com/action/downloadSupplement?doi=10.1002%2Fadfm.202008533&file=adfm202008533-sup-0001-SuppMat.pdf>)的Page S2中给出的计算方法。

### 计算细节
根据[Niu(2020)](<https://doi.org/10.1002/adfm.202008533>)在[Supporting Information](<https://onlinelibrary.wiley.com/action/downloadSupplement?doi=10.1002%2Fadfm.202008533&file=adfm202008533-sup-0001-SuppMat.pdf>)的Page S2中给出的描述，设计如下两步反应得到<img src="https://latex.codecogs.com/svg.image?\inline&space;\mathrm{NO}_{3}^{-}" title="\inline \mathrm{NO}_{3}^{-}" />：
<center><img src="https://latex.codecogs.com/svg.image?\mathrm{HNO}_{3}(\mathrm{g})&space;\overset{1}{\rightarrow}&space;\mathrm{HNO}_{3}(\mathrm{l})&space;" title="\mathrm{HNO}_{3}(\mathrm{g}) \overset{1}{\rightarrow} \mathrm{HNO}_{3}(\mathrm{l}) " /></center>
<center><img src="https://latex.codecogs.com/svg.image?\mathrm{HNO}_{3}(\mathrm{l})&space;\overset{2}{\rightarrow}&space;\mathrm{H}^{&plus;}(\mathrm{aq})&plus;\mathrm{NO}_{3}^{-}(\mathrm{aq})" title="\mathrm{HNO}_{3}(\mathrm{l}) \overset{2}{\rightarrow} \mathrm{H}^{+}(\mathrm{aq})+\mathrm{NO}_{3}^{-}(\mathrm{aq})" /></center>
接下来就只需要计算这两步反应的标准摩尔反应吉布斯自由能<img src="https://latex.codecogs.com/svg.image?\inline&space;\Delta_{\mathrm{r}}&space;G_{\mathrm{m}}^{\ominus}" title="\inline \Delta_{\mathrm{r}} G_{\mathrm{m}}^{\ominus}" />之和，就可以得到<img src="https://latex.codecogs.com/svg.image?\inline&space;\mathrm{NO}_{3}^{-}" title="\inline \mathrm{NO}_{3}^{-}" />相对于<img src="https://latex.codecogs.com/svg.image?\inline&space;\mathrm{HNO}_{3}" title="\inline \mathrm{HNO}_{3}" />的吉布斯自由能变化值。

计算第1步反应的<img src="https://latex.codecogs.com/svg.image?\inline&space;\Delta_{\mathrm{r}}&space;G_{\mathrm{m}}^{\ominus}" title="\inline \Delta_{\mathrm{r}} G_{\mathrm{m}}^{\ominus}" />，只需要参考[CRC Handbook of Chemistry and Physics](<https://hbcp.chemnetbase.com/faces/contents/ContentsSearch.xhtml>)手册中STANDARD THERMODYNAMIC PROPERTIES OF CHEMICAL SUBSTANCES的5-29页，分别得到<img src="https://latex.codecogs.com/svg.image?\inline&space;\mathrm{HNO}_{3}(\mathrm{l})" title="\inline \mathrm{HNO}_{3}(\mathrm{l})" />和<img src="https://latex.codecogs.com/svg.image?\inline&space;\mathrm{HNO}_{3}(\mathrm{g})" title="\inline \mathrm{HNO}_{3}(\mathrm{g})" />的标准摩尔生成吉布斯自由能<img src="https://latex.codecogs.com/svg.image?\inline&space;\Delta_{\mathrm{f}}&space;G_{\mathrm{m}}^{\ominus}" title="\inline \Delta_{\mathrm{f}} G_{\mathrm{m}}^{\ominus}" />，单位<img src="https://latex.codecogs.com/svg.image?\inline&space;\mathrm{kJ\!\cdot\!mol^{-1}}" title="\inline \mathrm{kJ\!\cdot\!mol^{-1}}" />，摘录如下：

| Species | State |   G   |
|:-------:|:-----:|:-----:|
|   HNO3  |   l   | -80.7 |
|   HNO3  |   g   | -73.5 |

单位换算：
```python
# taken from the 2014 version of the CODATA suggestions
mol = 6.022140857e23
e = 1.6021766208e-19 # C
kJ = 1000.0/e # eV
J = kJ/1000
K = 1.0
```
代入数据，计算第1步反应的<img src="https://latex.codecogs.com/svg.image?\inline&space;\Delta_{\mathrm{r}}&space;G_{\mathrm{m}}^{\ominus}" title="\inline \Delta_{\mathrm{r}} G_{\mathrm{m}}^{\ominus}" />，单位eV：
```python
G_HNO3_l = -80.7*kJ/mol
G_HNO3_g = -73.5*kJ/mol

G_1 = G_HNO3_l - G_HNO3_g
print(G_1) # -0.07462274093792332
```

计算第2步反应的<img src="https://latex.codecogs.com/svg.image?\inline&space;\Delta_{\mathrm{r}}&space;G_{\mathrm{m}}^{\ominus}" title="\inline \Delta_{\mathrm{r}} G_{\mathrm{m}}^{\ominus}" />，需要参考[CRC Handbook of Chemistry and Physics](<https://hbcp.chemnetbase.com/faces/contents/ContentsSearch.xhtml>)手册中CODATA KEY VALUES FOR THERMODYNAMICS的5-1页和STANDARD THERMODYNAMIC PROPERTIES OF CHEMICAL SUBSTANCES的5-29页。标准摩尔吉布斯生成焓<img src="https://latex.codecogs.com/svg.image?\inline&space;\Delta_{\mathrm{f}}&space;H_{\mathrm{m}}^{\ominus}" title="\inline \Delta_{\mathrm{f}} H_{\mathrm{m}}^{\ominus}" />（单位<img src="https://latex.codecogs.com/svg.image?\inline&space;\mathrm{kJ\!\cdot\!mol^{-1}}" title="\inline \mathrm{kJ\!\cdot\!mol^{-1}}" />）、标准摩尔熵<img src="https://latex.codecogs.com/svg.image?\inline&space;\Delta&space;S_{\mathrm{m}}^{\ominus}" title="\inline \Delta S_{\mathrm{m}}^{\ominus}" />（单位<img src="https://latex.codecogs.com/svg.image?\inline&space;\mathrm{J\!\cdot\!mol^{-1}\!\cdot\!K^{-1}}" title="\inline \mathrm{J\!\cdot\!mol^{-1}\!\cdot\!K^{-1}}" />）、标准摩尔生成吉布斯自由能<img src="https://latex.codecogs.com/svg.image?\inline&space;\Delta_{\mathrm{f}}&space;G_{\mathrm{m}}^{\ominus}" title="\inline \Delta_{\mathrm{f}} G_{\mathrm{m}}^{\ominus}" />（单位<img src="https://latex.codecogs.com/svg.image?\inline&space;\mathrm{kJ\!\cdot\!mol^{-1}}" title="\inline \mathrm{kJ\!\cdot\!mol^{-1}}" />），摘录如下：

| Species | State |        H       |        S        |   G   | Page |
|:-------:|:-----:|:--------------:|:---------------:|:-----:|:----:|
|    H+   |   aq  |        0       |        0        |       |  5-1 |
|    H2   |   g   |        0       | 130.680 ± 0.003 |       |  5-1 |
|   NO3-  |   aq  | -206.85 ± 0.40 |  146.70 ± 0.40  |       |  5-1 |
|    N2   |   g   |        0       | 191.609 ± 0.004 |       |  5-1 |
|    O2   |   g   |        0       | 205.152 ± 0.005 |       |  5-1 |
|   HNO3  |   l   |     -174.1     |      155.6      | -80.7 | 5-29 |

手册没有给出某些物质的<img src="https://latex.codecogs.com/svg.image?\inline&space;\Delta_{\mathrm{f}}&space;G_{\mathrm{m}}^{\ominus}" title="\inline \Delta_{\mathrm{f}} G_{\mathrm{m}}^{\ominus}" />值。所以，我们需要从标准摩尔生成吉布斯自由能的定义出发，计算<img src="https://latex.codecogs.com/svg.image?\inline&space;\Delta_{\mathrm{f}}&space;G_{\mathrm{m}}^{\ominus}(\mathrm{H}^{&plus;})" title="\inline \Delta_{\mathrm{f}} G_{\mathrm{m}}^{\ominus}(\mathrm{H}^{+})" />和<img src="https://latex.codecogs.com/svg.image?\inline&space;\Delta_{\mathrm{f}}&space;G_{\mathrm{m}}^{\ominus}(\mathrm{NO}_{3}^{-})" title="\inline \Delta_{\mathrm{f}} G_{\mathrm{m}}^{\ominus}(\mathrm{NO}_{3}^{-})" />。根据如下反应：
<center><img src="https://latex.codecogs.com/svg.image?\frac{1}{2}\mathrm{H}_{2}(\mathrm{g},~p^{\ominus})&space;\rightarrow&space;\mathrm{H}^{&plus;}(\mathrm{aq},~p^{\ominus})&space;&plus;&space;e^{-}" title="\frac{1}{2}\mathrm{H}_{2}(\mathrm{g},~p^{\ominus}) \rightarrow \mathrm{H}^{+}(\mathrm{aq},~p^{\ominus}) + e^{-}" /></center>
可计算：
<center><img src="https://latex.codecogs.com/svg.image?\Delta_{\mathrm{f}}&space;G_{\mathrm{m}}^{\ominus}(\mathrm{H}^{&plus;})&space;=&space;\Delta_{\mathrm{f}}&space;H_{\mathrm{m}}^{\ominus}(\mathrm{H}^{&plus;})&space;-&space;\frac{1}{2}\Delta_{\mathrm{f}}&space;H_{\mathrm{m}}^{\ominus}(\mathrm{H}_{2})&space;-&space;T\left(\Delta&space;S_{\mathrm{m}}^{\ominus}(\mathrm{H}^{&plus;})&space;-&space;\frac{1}{2}\Delta&space;S_{\mathrm{m}}^{\ominus}(\mathrm{H}_{2})\right)" title="\Delta_{\mathrm{f}} G_{\mathrm{m}}^{\ominus}(\mathrm{H}^{+}) = \Delta_{\mathrm{f}} H_{\mathrm{m}}^{\ominus}(\mathrm{H}^{+}) - \frac{1}{2}\Delta_{\mathrm{f}} H_{\mathrm{m}}^{\ominus}(\mathrm{H}_{2}) - T\left(\Delta S_{\mathrm{m}}^{\ominus}(\mathrm{H}^{+}) - \frac{1}{2}\Delta S_{\mathrm{m}}^{\ominus}(\mathrm{H}_{2})\right)" /></center>
代入数据：
```python
H_H_aq = 0*kJ/mol
S_H_aq = 0*J/mol/K
H_H2_g = 0*kJ/mol
S_H2_g = 130.680*J/mol/K
T = 298.15*K

n_H_aq = 1
n_H2_g = -0.5

G_H_aq = (n_H_aq*H_H_aq+n_H2_g*H_H2_g) - T*(n_H_aq*S_H_aq+n_H2_g*S_H2_g)
print(G_H_aq) # 0.20190758966157468
```
计算得到<img src="https://latex.codecogs.com/svg.image?\inline&space;\Delta_{\mathrm{f}}&space;G_{\mathrm{m}}^{\ominus}(\mathrm{H}^{&plus;})" title="\inline \Delta_{\mathrm{f}} G_{\mathrm{m}}^{\ominus}(\mathrm{H}^{+})" />为0.202 eV，即19.5 <img src="https://latex.codecogs.com/svg.image?\inline&space;\mathrm{kJ\!\cdot\!mol^{-1}}" title="\inline \mathrm{kJ\!\cdot\!mol^{-1}}" />。

同样地，根据如下反应：
<center><img src="https://latex.codecogs.com/svg.image?\frac{1}{2}\mathrm{N}_{2}(\mathrm{g},~p^{\ominus})&space;&plus;&space;\frac{3}{2}\mathrm{O}_{2}(\mathrm{g},~p^{\ominus})&space;&plus;&space;e^{-}&space;\rightarrow&space;\mathrm{NO}_{3}^{-}(\mathrm{aq},~p^{\ominus})" title="\frac{1}{2}\mathrm{N}_{2}(\mathrm{g},~p^{\ominus}) + \frac{3}{2}\mathrm{O}_{2}(\mathrm{g},~p^{\ominus}) + e^{-} \rightarrow \mathrm{NO}_{3}^{-}(\mathrm{aq},~p^{\ominus})" /></center>
可计算：
<center><img src="https://latex.codecogs.com/svg.image?\Delta_{\mathrm{f}}&space;G_{\mathrm{m}}^{\ominus}(\mathrm{NO}_{3}^{-})&space;=&space;\Delta_{\mathrm{f}}&space;H_{\mathrm{m}}^{\ominus}(\mathrm{NO}_{3}^{-})&space;-&space;\frac{1}{2}\Delta_{\mathrm{f}}&space;H_{\mathrm{m}}^{\ominus}(\mathrm{N}_{2})&space;-&space;\frac{3}{2}\Delta_{\mathrm{f}}&space;H_{\mathrm{m}}^{\ominus}(\mathrm{O}_{2})&space;-&space;T\left(\Delta&space;S_{\mathrm{m}}^{\ominus}(\mathrm{NO}_{3}^{-})&space;-&space;\frac{1}{2}\Delta&space;S_{\mathrm{m}}^{\ominus}(\mathrm{N}_{2})&space;-&space;\frac{3}{2}\Delta&space;S_{\mathrm{m}}^{\ominus}(\mathrm{O}_{2})\right)" title="\Delta_{\mathrm{f}} G_{\mathrm{m}}^{\ominus}(\mathrm{NO}_{3}^{-}) = \Delta_{\mathrm{f}} H_{\mathrm{m}}^{\ominus}(\mathrm{NO}_{3}^{-}) - \frac{1}{2}\Delta_{\mathrm{f}} H_{\mathrm{m}}^{\ominus}(\mathrm{N}_{2}) - \frac{3}{2}\Delta_{\mathrm{f}} H_{\mathrm{m}}^{\ominus}(\mathrm{O}_{2}) - T\left(\Delta S_{\mathrm{m}}^{\ominus}(\mathrm{NO}_{3}^{-}) - \frac{1}{2}\Delta S_{\mathrm{m}}^{\ominus}(\mathrm{N}_{2}) - \frac{3}{2}\Delta S_{\mathrm{m}}^{\ominus}(\mathrm{O}_{2})\right)" /></center>
代入数据：
```python
H_NO3_aq = -206.85*kJ/mol
S_NO3_aq = 146.70*J/mol/K
H_N2_g = 0*kJ/mol
S_N2_g = 191.609*J/mol/K
H_O2_g = 0*kJ/mol
S_O2_g = 205.152*J/mol/K
T = 298.15*K

n_NO3_aq = 1
n_N2_g = -0.5
n_O2_g = -1.5

G_NO3_aq = (n_NO3_aq*H_NO3_aq+n_N2_g*H_N2_g+n_O2_g*H_O2_g) - T*(n_NO3_aq*S_NO3_aq+n_N2_g*S_N2_g+n_O2_g*S_O2_g)
print(G_NO3_aq) # -1.3502092622062178
```
计算得到<img src="https://latex.codecogs.com/svg.image?\inline&space;\Delta_{\mathrm{f}}&space;G_{\mathrm{m}}^{\ominus}(\mathrm{NO}_{3}^{-})" title="\inline \Delta_{\mathrm{f}} G_{\mathrm{m}}^{\ominus}(\mathrm{NO}_{3}^{-})" />为-1.350 eV，即-130.3 <img src="https://latex.codecogs.com/svg.image?\inline&space;\mathrm{kJ\!\cdot\!mol^{-1}}" title="\inline \mathrm{kJ\!\cdot\!mol^{-1}}" />。

完成这张表格：

| Species | State |        H       |        S        |    G   |
|:-------:|:-----:|:--------------:|:---------------:|:------:|
|    H+   |   aq  |        0       |        0        |  19.5  |
|    H2   |   g   |        0       | 130.680 ± 0.003 |    0   |
|   NO3-  |   aq  | -206.85 ± 0.40 |  146.70 ± 0.40  | -130.3 |
|    N2   |   g   |        0       | 191.609 ± 0.004 |    0   |
|    O2   |   g   |        0       | 205.152 ± 0.005 |    0   |
|   HNO3  |   l   |     -174.1     |      155.6      |  -80.7 |

已经得到<img src="https://latex.codecogs.com/svg.image?\inline&space;\Delta_{\mathrm{f}}&space;G_{\mathrm{m}}^{\ominus}(\mathrm{H}^{&plus;})" title="\inline \Delta_{\mathrm{f}} G_{\mathrm{m}}^{\ominus}(\mathrm{H}^{+})" />、<img src="https://latex.codecogs.com/svg.image?\inline&space;\Delta_{\mathrm{f}}&space;G_{\mathrm{m}}^{\ominus}(\mathrm{NO}_{3}^{-})" title="\inline \Delta_{\mathrm{f}} G_{\mathrm{m}}^{\ominus}(\mathrm{NO}_{3}^{-})" />和<img src="https://latex.codecogs.com/svg.image?\inline&space;\mathrm{HNO}_{3}(\mathrm{l})" title="\inline \mathrm{HNO}_{3}(\mathrm{l})" />，可计算第2步反应的<img src="https://latex.codecogs.com/svg.image?\inline&space;\Delta_{\mathrm{r}}&space;G_{\mathrm{m}}^{\ominus}" title="\inline \Delta_{\mathrm{r}} G_{\mathrm{m}}^{\ominus}" />，单位eV：
```python
G_2 = G_NO3_aq + G_H_aq - G_HNO3_l
print(G_2) # -0.3119051178654192
```

最终，对两步反应的<img src="https://latex.codecogs.com/svg.image?\inline&space;\Delta_{\mathrm{r}}&space;G_{\mathrm{m}}^{\ominus}" title="\inline \Delta_{\mathrm{r}} G_{\mathrm{m}}^{\ominus}" />求和，即可得到<img src="https://latex.codecogs.com/svg.image?\inline&space;\mathrm{NO}_{3}^{-}" title="\inline \mathrm{NO}_{3}^{-}" />相对于<img src="https://latex.codecogs.com/svg.image?\inline&space;\mathrm{HNO}_{3}" title="\inline \mathrm{HNO}_{3}" />的吉布斯自由能差值，单位eV：
```python
G_corr = G_1 + G_2
print(G_corr) # -0.3865278588033425
```
即，DFT计算<img src="https://latex.codecogs.com/svg.image?\inline&space;\mathrm{HNO}_{3}" title="\inline \mathrm{HNO}_{3}" />的吉布斯自由能，减去0.387 eV，可得<img src="https://latex.codecogs.com/svg.image?\inline&space;\mathrm{NO}_{3}^{-}" title="\inline \mathrm{NO}_{3}^{-}" />的吉布斯自由能。

### 疑问

#### 为什么要设计两步反应
物种<img src="https://latex.codecogs.com/svg.image?\inline&space;\mathrm{HNO}_{3}(\mathrm{l})" title="\inline \mathrm{HNO}_{3}(\mathrm{l})" />的能量在计算过程中是被消掉的。如果我使用总反应方程式：
<center><img src="https://latex.codecogs.com/svg.image?\inline&space;\mathrm{HNO}_{3}(\mathrm{g})&space;\rightarrow&space;\mathrm{H}^{&plus;}(\mathrm{aq})&plus;\mathrm{NO}_{3}^{-}(\mathrm{aq})" title="\inline \mathrm{HNO}_{3}(\mathrm{g}) \rightarrow \mathrm{H}^{+}(\mathrm{aq})+\mathrm{NO}_{3}^{-}(\mathrm{aq})" /></center>
计算结果是一样的。那考虑<img src="https://latex.codecogs.com/svg.image?\inline&space;\mathrm{HNO}_{3}" title="\inline \mathrm{HNO}_{3}" />的相变有什么意义呢？

#### 这个方法本身有何意义
我发现只有NO3RR的理论计算会强调使用<img src="https://latex.codecogs.com/svg.image?\inline&space;\mathrm{NO}_{3}^{-}" title="\inline \mathrm{NO}_{3}^{-}" />的能量而不是<img src="https://latex.codecogs.com/svg.image?\inline&space;\mathrm{HNO}_{3}" title="\inline \mathrm{HNO}_{3}" />的能量。

参考态的能量需要基于同一标准。比如，中性溶液中CO2被还原成HCOOH。即使溶液中实际存在的是碳酸根和甲酸根，Nørskov的方法也是基于酸性假设，计算CO2和HCOOH的能量。因为它们在RHE标度上，热力学关系是始终不变的。同样地，HNO3和产物NH3在RHE标度上，热力学关系也应是不变的。那为什么要强调<img src="https://latex.codecogs.com/svg.image?\inline&space;\mathrm{NO}_{3}^{-}" title="\inline \mathrm{NO}_{3}^{-}" />呢？

Nørskov**似乎**还没有做过NO3RR相关工作。

[[Back]](../)
