---
layout: default
---

## pH对CO2RR热力学的影响

酸性条件下，电催化CO2RR可生成HCOOH，但中性/碱性条件下，HCOOH会解离。
本文分析了HCOOH的解离如何影响电催化CO2RR的反应自由能变化。

感谢Michael博士。

酸性条件下电催化<img src="https://latex.codecogs.com/svg.image?\inline&space;\mathrm{CO}_{2}" title="\inline \mathrm{CO}_{2}" />还原为HCOOH，氢源是质子
<center><img src="https://latex.codecogs.com/svg.image?\mathrm{CO}_{2}&space;&plus;&space;2\mathrm{H}^{&plus;}&space;&plus;&space;2e^{-}&space;\rightleftharpoons&space;\mathrm{HCOOH}(g)" title="\mathrm{CO}_{2} + 2\mathrm{H}^{+} + 2e^{-} \rightleftharpoons \mathrm{HCOOH}(g)" /></center>

中性/碱性条件下，氢源是水
<center><img src="https://latex.codecogs.com/svg.image?\mathrm{CO}_{2}&space;&plus;&space;2\mathrm{H}_{2}\mathrm{O}&space;&plus;&space;2e^{-}&space;\rightleftharpoons&space;\mathrm{HCOOH}&space;&plus;&space;2\mathrm{OH}^{-}" title="\mathrm{CO}_{2} + 2\mathrm{H}_{2}\mathrm{O} + 2e^{-} \rightleftharpoons \mathrm{HCOOH} + 2\mathrm{OH}^{-}" /></center>

HCOOH可发生解离，即
<center><img src="https://latex.codecogs.com/svg.image?\mathrm{HCOOH}&space;\rightleftharpoons&space;\mathrm{HCOO}^{-}&space;&plus;&space;\mathrm{H}^{&plus;}" title="\mathrm{HCOOH} \rightleftharpoons \mathrm{HCOO}^{-} + \mathrm{H}^{+}" /></center>

所以中性/碱性条件下的反应式为，
<img src="https://latex.codecogs.com/svg.image?\mathrm{CO}_{2}&space;&plus;&space;\mathrm{H}_{2}\mathrm{O}&space;&plus;&space;2e^{-}&space;\rightleftharpoons&space;\mathrm{HCOO}^{-}&space;&plus;&space;\mathrm{OH}^{-}" title="\mathrm{CO}_{2} + \mathrm{H}_{2}\mathrm{O} + 2e^{-} \rightleftharpoons \mathrm{HCOO}^{-} + \mathrm{OH}^{-}" />

因此，酸性碱性条件下自由能的差别由HCOOH和甲酸根的自由能差值决定。
<center><img src="https://latex.codecogs.com/svg.image?\mathrm{HCOOH}&space;\rightleftharpoons&space;\mathrm{HCOO}^{-}&space;&plus;&space;\mathrm{H}^{&plus;}" title="\mathrm{HCOOH} \rightleftharpoons \mathrm{HCOO}^{-} + \mathrm{H}^{+}" /></center>
上式的<img src="https://latex.codecogs.com/svg.image?\inline&space;\mathrm{p}K_{\mathrm{a}}" title="\inline \mathrm{p}K_{\mathrm{a}}" />为3.75
然后根据
<center><img src="https://latex.codecogs.com/svg.image?K&space;=&space;\exp\left(-\frac{\Delta&space;G}{k_{\mathrm{B}}T}\right)" title="K = \exp\left(-\frac{\Delta G}{k_{\mathrm{B}}T}\right)" /></center>
可以得出该反应的自由能变化值为-0.222 eV
```python
import numpy as np
from ase.units import kB

T = 298.15
pKa = 3.75 # HCOOH, CRC Page 5-92

dG = -kB*T*pKa*np.log(10)
print(dG) # -0.2218474860175924
```
所以甲酸根的能量比HCOOH更负约0.222 eV，即，
<center><img src="https://latex.codecogs.com/svg.image?E_{\mathrm{HCOO}^{-}}&space;=&space;E_{\mathrm{HCOOH}}&space;-&space;0.222\&space;\mathrm{eV}" title="E_{\mathrm{HCOO}^{-}} = E_{\mathrm{HCOOH}} - 0.222\ \mathrm{eV}" /></center>


[[Back]](../)
