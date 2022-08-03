---
layout: default
---

## pH对CO2RR热力学的影响

酸性条件下，电催化<img src="https://latex.codecogs.com/svg.image?\inline&space;\mathrm{CO}_{2}\mathrm{RR}" title="\inline \mathrm{CO}_{2}\mathrm{RR}" />可生成HCOOH，但中性/碱性条件下，HCOOH会解离。
本文旨在分析HCOOH的解离如何影响电催化<img src="https://latex.codecogs.com/svg.image?\inline&space;\mathrm{CO}_{2}\mathrm{RR}" title="\inline \mathrm{CO}_{2}\mathrm{RR}" />的反应自由能变化。

感谢Michael博士！

酸性条件下电催化<img src="https://latex.codecogs.com/svg.image?\inline&space;\mathrm{CO}_{2}" title="\inline \mathrm{CO}_{2}" />还原为HCOOH，氢源是质子，甲酸盐的主要存在形式是HCOOH
<center><img src="https://latex.codecogs.com/svg.image?\mathrm{CO}_{2}&space;&plus;&space;2\mathrm{H}^{&plus;}&space;&plus;&space;2e^{-}&space;\rightleftharpoons&space;\mathrm{HCOOH}" title="\mathrm{CO}_{2} + 2\mathrm{H}^{+} + 2e^{-} \rightleftharpoons \mathrm{HCOOH}" /></center>

中性/碱性条件下，氢源是水，甲酸盐的主要存在形式是<img src="https://latex.codecogs.com/svg.image?\inline&space;\mathrm{HCOO}^{-}" title="\inline \mathrm{HCOO}^{-}" />
<center><img src="https://latex.codecogs.com/svg.image?\mathrm{CO}_{2}&space;&plus;&space;\mathrm{H}_{2}\mathrm{O}&space;&plus;&space;2e^{-}&space;\rightleftharpoons&space;\mathrm{HCOO}^{-}&space;&plus;&space;\mathrm{OH}^{-}" title="\mathrm{CO}_{2} + \mathrm{H}_{2}\mathrm{O} + 2e^{-} \rightleftharpoons \mathrm{HCOO}^{-} + \mathrm{OH}^{-}" /></center>

因此，这两种条件下电催化<img src="https://latex.codecogs.com/svg.image?\inline&space;\mathrm{CO}_{2}\mathrm{RR}" title="\inline \mathrm{CO}_{2}\mathrm{RR}" />自由能的差别主要来自于HCOOH和<img src="https://latex.codecogs.com/svg.image?\inline&space;\mathrm{HCOO}^{-}" title="\inline \mathrm{HCOO}^{-}" />的能量差。

HCOOH可直接解离生成<img src="https://latex.codecogs.com/svg.image?\inline&space;\mathrm{HCOO}^{-}" title="\inline \mathrm{HCOO}^{-}" />
<center><img src="https://latex.codecogs.com/svg.image?\mathrm{HCOOH}&space;\rightleftharpoons&space;\mathrm{HCOO}^{-}&space;&plus;&space;\mathrm{H}^{&plus;}" title="\mathrm{HCOOH} \rightleftharpoons \mathrm{HCOO}^{-} + \mathrm{H}^{+}" /></center>

上式的<img src="https://latex.codecogs.com/svg.image?\inline&space;\mathrm{p}K_{\mathrm{a}}" title="\inline \mathrm{p}K_{\mathrm{a}}" />等于3.75。然后可根据反应平衡常数和反应自由能的关系式，即
<center><img src="https://latex.codecogs.com/svg.image?K&space;=&space;\exp\left(-\frac{\Delta&space;G}{k_{\mathrm{B}}T}\right)" title="K = \exp\left(-\frac{\Delta G}{k_{\mathrm{B}}T}\right)" /></center>
得该解离过程的反应自由能为-0.222 eV。

```python
import numpy as np
from ase.units import kB

T = 298.15
pKa = 3.75 # HCOOH, CRC Page 5-92

dG = -kB*T*pKa*np.log(10)
print(dG) # -0.2218474860175924
```

所以<img src="https://latex.codecogs.com/svg.image?\inline&space;\mathrm{HCOO}^{-}" title="\inline \mathrm{HCOO}^{-}" />的能量比HCOOH更负约0.222 eV，即
<center><img src="https://latex.codecogs.com/svg.image?G_{\mathrm{HCOO}^{-}}&space;=&space;G_{\mathrm{HCOOH}}&space;-&space;0.222\&space;\mathrm{eV}" title="G_{\mathrm{HCOO}^{-}} = G_{\mathrm{HCOOH}} - 0.222\ \mathrm{eV}" /></center>

[[Back]](../)
