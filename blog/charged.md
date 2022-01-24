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

| Species | <img src="https://latex.codecogs.com/svg.image?\inline&space;\Delta_{\mathrm{f}}&space;G_{\mathrm{m}}^{\ominus}/\mathrm{kJ\!\cdot\!mol^{-1}}" title="\inline \Delta_{\mathrm{f}} G_{\mathrm{m}}^{\ominus}/\mathrm{kJ\!\cdot\!mol^{-1}}" /> |
|:---:|:---:|
| <img src="https://latex.codecogs.com/svg.image?\inline&space;\mathrm{HNO}_{3}(\mathrm{l})" title="\inline \mathrm{HNO}_{3}(\mathrm{l})" /> | -80.7 |
| <img src="https://latex.codecogs.com/svg.image?\inline&space;\mathrm{HNO}_{3}(\mathrm{g})" title="\inline \mathrm{HNO}_{3}(\mathrm{g})" /> | -73.5 |

由此可得，第一步反应的吉布斯自由能为
```Python
from ase.units import kJ, mol
(-73.5-(-80.7))*kJ/mol
# 0.07462274093792334
```


### 参考
Sander, R.: Compilation of Henry's law constants (version 4.0) for water as solvent, Atmos. Chem. Phys., 15, 4399–4981, [https://doi.org/10.5194/acp-15-4399-2015](<https://acp.copernicus.org/articles/15/4399/2015/>), 2015.
[亨利定律常数表](<https://max.book118.com/html/2017/0528/109971917.shtm>)

[[Back]](../)
