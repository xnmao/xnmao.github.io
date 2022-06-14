---
layout: default
---

## 酸碱组分的平衡浓度与分布分数

### 概念
溶液中某酸碱组分的平衡浓度占其总浓度的分数，称为分布分数（distribution fraction），以<img src="https://latex.codecogs.com/svg.image?\inline&space;\delta" title="https://latex.codecogs.com/svg.image?\inline \delta" />表示。

### 应用
可确定阴阳离子浓度，然后估算弱酸溶液的双电层厚度。

### 已知条件
pKa来自CRC
求解过程参考分析化学P116-118

### Python求解过程
```python
import numpy as np
import matplotlib.pyplot as plt


class Distribution_Fraction:

    def __init__(self, pKa=[], pH=np.linspace(0, 14, 301)):
        self.pKa = pKa # pKa1, pKa2, pKa3, ...
        self.pH = pH # pH
        n = len(self.pKa)

        # 计算分布分数
        H = 10.**(-np.array(self.pH))
        Ka = 10.**(-np.array(self.pKa))
        c = np.repeat(Ka.reshape(n, 1), len(pH), axis=1)
        self.delta = [np.prod(c, axis=0),]
        for i in range(-1, -n-1, -1):
            c[i] = H
            self.delta.append(np.prod(c, axis=0))
        self.delta /= np.sum(self.delta, axis=0)

        # 获得化学式
        self.formula = ['A',]
        for i in range(1, n+1):
            self.formula.append(f'H{i:d}A'.replace('H1', 'H'))

    def plot(self, ax): # 绘图
        for formula, delta in zip(self.formula, self.delta):
            ax.plot(self.pH, delta, label=formula)
        ax.legend(fontsize='large')
        ax.axis((0, 14, 0, 1))
        ax.tick_params(labelsize='x-large')
        ax.set_xlabel(r'$\mathregular{pH}$', fontsize='x-large')
        ax.set_ylabel(r'$\delta$', fontsize='x-large')
        return ax


if __name__ == '__main__':

    distribution = Distribution_Fraction(pKa=[6.35, 10.33]) # CRC Page 5-87
    plt.figure(facecolor='w')
    ax = plt.gca()
    distribution.plot(ax=ax)
    plt.savefig('H2CO3.svg', bbox_inches='tight')
```


### 计算结果
碳酸溶液。图例中的A是<img src="https://latex.codecogs.com/svg.image?\inline&space;\mathrm{CO}_{3}^{2-}" title="https://latex.codecogs.com/svg.image?\inline \mathrm{CO}_{3}^{2-}" />
<center><img src="../graphic/distribution_fraction/H2CO3.svg" title="H2CO3" width="95%"/></center>
醋酸溶液。图例中的A是<img src="https://latex.codecogs.com/svg.image?\inline&space;\mathrm{Ac}^{-}" title="https://latex.codecogs.com/svg.image?\inline \mathrm{Ac}^{-}" />
<center><img src="../graphic/distribution_fraction/HAc.svg" title="HAc" width="95%"/></center>
甲酸溶液。图例中的A是<img src="https://latex.codecogs.com/svg.image?\inline&space;\mathrm{HCOO}^{-}" title="https://latex.codecogs.com/svg.image?\inline \mathrm{HCOO}^{-}" />
<center><img src="../graphic/distribution_fraction/HCOOH.svg" title="HCOOH" width="95%"/></center>
氨水。图例中的A是<img src="https://latex.codecogs.com/svg.image?\inline&space;\mathrm{NH}_{3}" title="https://latex.codecogs.com/svg.image?\inline \mathrm{NH}_{3}" />
<center><img src="../graphic/distribution_fraction/NH3.svg" title="NH3" width="95%"/></center>

### 参考
1. Sander, R.: Compilation of Henry's law constants (version 4.0) for water as solvent, Atmos. Chem. Phys., 15, 4399–4981, [https://doi.org/10.5194/acp-15-4399-2015](<https://acp.copernicus.org/articles/15/4399/2015/>), 2015.
2. [亨利定律常数表](<https://max.book118.com/html/2017/0528/109971917.shtm>)
3. [Atkins' Physical Chemistry 11e](<https://global.oup.com/academic/product/atkins-physical-chemistry-11e-9780198817895?q=atkins&lang=en&cc=us>) P152-153

[[Back]](../)
