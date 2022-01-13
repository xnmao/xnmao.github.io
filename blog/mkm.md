---
layout: default
---

## 电催化ORR微观动力学计算

### 设计ORR反应过程

1. O2从本体溶液中扩散到电极附近<center><img src="https://latex.codecogs.com/svg.image?\mathrm{O}_{2}(\mathrm{aq})&space;\underset{k_{-1}}{\stackrel{k_{1}}{\rightleftharpoons}}&space;\mathrm{O}_{2}(\mathrm{dl})" title="\mathrm{O}_{2}(\mathrm{aq}) \underset{k_{-1}}{\stackrel{k_{1}}{\rightleftharpoons}} \mathrm{O}_{2}(\mathrm{dl})" /></center>
2. O2从电极附近的溶液中移到电极上，形成吸附在反应位点A的\*O2<center><img src="https://latex.codecogs.com/svg.image?\mathrm{O}_{2}(\mathrm{dl})&plus;*_{\mathrm{A}}&space;\underset{k_{-2}}{\stackrel{k_{2}}{\rightleftharpoons}}&space;\mathrm{O}_{2}&space;*_{\mathrm{A}}" title="\mathrm{O}_{2}(\mathrm{dl})+*_{\mathrm{A}} \underset{k_{-2}}{\stackrel{k_{2}}{\rightleftharpoons}} \mathrm{O}_{2} *_{\mathrm{A}}" /></center>
3. H+和已经被吸附在反应位点A上的\*O2反应生成\*OOH中间体<center><img src="https://latex.codecogs.com/svg.image?\mathrm{O}_{2}&space;*_{\mathrm{A}}&plus;\mathrm{H}^{&plus;}&plus;e^{-}&space;\underset{k_{-3}}{\stackrel{k_{3}}{\rightleftharpoons}}&space;\mathrm{OOH}&space;*_{\mathrm{A}}" title="\mathrm{O}_{2} *_{\mathrm{A}}+\mathrm{H}^{+}+e^{-} \underset{k_{-3}}{\stackrel{k_{3}}{\rightleftharpoons}} \mathrm{OOH} *_{\mathrm{A}}" /></center>
4. H+和已经被吸附在反应位点A上的\*OOH中间体反应生成\*O中间体和H2O<center><img src="https://latex.codecogs.com/svg.image?\mathrm{OOH}&space;*_{\mathrm{A}}&plus;\mathrm{H}^{&plus;}&plus;e^{-}&space;\underset{k_{-4}}{\stackrel{k_{4}}{\rightleftharpoons}}&space;\mathrm{O}&space;*_{\mathrm{A}}&plus;\mathrm{H}_{2}&space;\mathrm{O}" title="\mathrm{OOH} *_{\mathrm{A}}+\mathrm{H}^{+}+e^{-} \underset{k_{-4}}{\stackrel{k_{4}}{\rightleftharpoons}} \mathrm{O} *_{\mathrm{A}}+\mathrm{H}_{2} \mathrm{O}" /></center>
5. H+和已经被吸附在反应位点A上的\*O中间体反应生成\*OH中间体<center><img src="https://latex.codecogs.com/svg.image?\mathrm{O}&space;*_{\mathrm{A}}&plus;\mathrm{H}^{&plus;}&plus;e^{-}&space;\underset{k_{-5}}{\stackrel{k_{5}}{\rightleftharpoons}}&space;\mathrm{OH}&space;*_{\mathrm{A}}" title="\mathrm{O} *_{\mathrm{A}}+\mathrm{H}^{+}+e^{-} \underset{k_{-5}}{\stackrel{k_{5}}{\rightleftharpoons}} \mathrm{OH} *_{\mathrm{A}}" /></center>
6. H+和已经被吸附在反应位点A上的\*OH中间体反应生成H2O<center><img src="https://latex.codecogs.com/svg.image?\mathrm{OH}&space;*_{\mathrm{A}}&plus;\mathrm{H}^{&plus;}&plus;e^{-}&space;\underset{k_{-6}}{\stackrel{k_{6}}{\rightleftharpoons}}&space;*_{\mathrm{A}}&plus;\mathrm{H}_{2}&space;\mathrm{O}" title="\mathrm{OH} *_{\mathrm{A}}+\mathrm{H}^{+}+e^{-} \underset{k_{-6}}{\stackrel{k_{6}}{\rightleftharpoons}} *_{\mathrm{A}}+\mathrm{H}_{2} \mathrm{O}" /></center>

### 联立微分方程组

#### 反应速率常数
由过渡态理论计算反应速率常数
<center><img src="https://latex.codecogs.com/svg.image?k_{i}=\frac{k_{\mathrm{B}}&space;T}{h}&space;\exp&space;\left(-\frac{G_{a,&space;i}}{k_{\mathrm{B}}&space;T}\right)" title="k_{i}=\frac{k_{\mathrm{B}} T}{h} \exp \left(-\frac{G_{a, i}}{k_{\mathrm{B}} T}\right)" /></center>
其中<img src="https://latex.codecogs.com/svg.image?G_{a,i}" title="G_{a,i}" />是**活化自由能**，包含活化焓和活化熵校正。这个值不易得到。通常可以忽略活化熵，使用Arrhenius经验公式表达反应速率常数
<center><img src="https://latex.codecogs.com/svg.image?k_{i}=\nu_{i}&space;\exp&space;\left(-\frac{E_{a,&space;i}}{k_{\mathrm{B}}&space;T}\right)" title="k_{i}=\nu_{i} \exp \left(-\frac{E_{a, i}}{k_{\mathrm{B}} T}\right)" /></center>
其中，<img src="https://latex.codecogs.com/svg.image?E_{a,i}" title="E_{a,i}" />是活化能，可以使用NEB方法计算过渡态电子能量获得，<img src="https://latex.codecogs.com/svg.image?\nu_{i}" title="\nu_{i}" />是指前因子（pre-exponential factor），单位<img src="https://latex.codecogs.com/svg.image?\mathrm{s}^{-1}" title="\mathrm{s}^{-1}" />。<img src="https://latex.codecogs.com/svg.image?\nu_{i}" title="\nu_{i}" />越小，对应反应步骤的时间尺度越大（慢）。由于溶剂重组（solvent reorganisation），吸附/脱附步骤的<img src="https://latex.codecogs.com/svg.image?\nu_{i}" title="\nu_{i}" />取值会比中间体反应步骤小几个数量级。对于ORR反应，<img src="https://latex.codecogs.com/svg.image?\nu_{i}" title="\nu_{i}" />取值建议参考[Hansen 2014](<https://doi.org/10.1021/jp4100608>)的Table 2。

相比于化学步骤，电化学步骤的反应速率常数计算公式中，还包含外加电势<img src="https://latex.codecogs.com/svg.image?U" title="U" />的推动力
<center><img src="https://latex.codecogs.com/svg.image?k_{i}=\frac{k_{\mathrm{B}}&space;T}{h}&space;\exp&space;\left(-\frac{G_{a,&space;i}^{0}}{k_{\mathrm{B}}&space;T}\right)&space;\exp&space;\left(-\frac{e&space;\beta_{i}\left(U-U_{i}^{0}\right)}{k_{\mathrm{B}}&space;T}\right)" title="k_{i}=\frac{k_{\mathrm{B}} T}{h} \exp \left(-\frac{G_{a, i}^{0}}{k_{\mathrm{B}} T}\right) \exp \left(-\frac{e \beta_{i}\left(U-U_{i}^{0}\right)}{k_{\mathrm{B}} T}\right)" /></center>
类似地，使用Arrhenius经验公式的形式改写为
<center><img src="https://latex.codecogs.com/svg.image?k_{i}=A_{i}&space;\exp&space;\left(-\frac{E_{a,&space;i}^{0}}{k_{\mathrm{B}}&space;T}\right)&space;\exp&space;\left(-\frac{e&space;\beta_{i}\left(U-U_{i}^{0}\right)}{k_{\mathrm{B}}&space;T}\right)" title="k_{i}=A_{i} \exp \left(-\frac{E_{a, i}^{0}}{k_{\mathrm{B}} T}\right) \exp \left(-\frac{e \beta_{i}\left(U-U_{i}^{0}\right)}{k_{\mathrm{B}} T}\right)" /></center>
其中，<img src="https://latex.codecogs.com/svg.image?U_{i}^{0}" title="U_{i}^{0}" />是可逆电势，从反应自由能<img src="https://latex.codecogs.com/svg.image?\Delta&space;G_{i}^{0}" title="\Delta G_{i}^{0}" />计算得到
<center><img src="https://latex.codecogs.com/svg.image?U_{i}^{0}=-\frac{\Delta&space;G_{i}^{0}}{e}" title="U_{i}^{0}=-\frac{\Delta G_{i}^{0}}{e}" /></center>
<img src="https://latex.codecogs.com/svg.image?\beta_{i}" title="\beta_{i}" />是对称因子（symmetric factor），也称传递系数（transfer coefficient）。它与过渡态附近的对称性相关，通常被认为大约在0.5左右，即当在过渡态处反应物和生成物的斜率绝对值一样，则对称因子为0.5。相关内容可参考[Tripković 2010](<https://doi.org/10.1016/j.electacta.2010.02.056>)，[「Transfer Coefficient究竟是什么？」](<https://zhuanlan.zhihu.com/p/54101241>)。  
<img src="https://latex.codecogs.com/svg.image?E_{a,i}^{0}" title="E_{a,i}^{0}" />是活化能。计算电化学步骤的活化能通常要考虑较为复杂的显式溶剂模型，因为反应前后基底上吸附的中间体化学组分发生了改变（多1个或少1个氢原子）。它带一个上标0，是指可以**假设**活化能是常数。参考[Tripković 2010](<https://doi.org/10.1016/j.electacta.2010.02.056>)，对于**ORR过程**的质子转移，电化学步骤的<img src="https://latex.codecogs.com/svg.image?E_{a,i}^{0}" title="E_{a,i}^{0}" />可以全部设置为0.26 eV。  
<img src="https://latex.codecogs.com/svg.image?A_{i}" title="A_{i}" />是有效指前因子（effective pre-exponential factor），取决于溶剂重组的时间尺度。根据[Wang 2019](<https://doi.org/10.1021/jacs.9b07712>)在[Supporting Information](<https://pubs.acs.org/doi/suppl/10.1021/jacs.9b07712/suppl_file/ja9b07712_si_001.pdf>) Page S5中给出的解释，可以估计<img src="https://latex.codecogs.com/svg.image?A_{i}" title="A_{i}" />为<img src="https://latex.codecogs.com/svg.image?1.23\times10^{9}\&space;\mathrm{s}^{-1}" title="1.23\times10^{9}\ \mathrm{s}^{-1}" />。

#### 微观可逆性原理
微观粒子系统具有时间反演的对称性，如将时间<img src="https://latex.codecogs.com/svg.image?t" title="t" />用<img src="https://latex.codecogs.com/svg.image?-t" title="-t" />代替，则对正向运动方程的解和对逆向运动方程的解完全相同，只是二者相差一个正负符号。逆过程就按原来的路程返回，就像把电影胶片逆向倒放一遍一样。因此，从微观的角度看，若正向反应是允许的，则其逆向反应亦应该是允许的。达平衡时，正逆反应的速率相等，逆反应速率常数为
<center><img src="https://latex.codecogs.com/svg.image?k_{-i}=\frac{k_{i}}{K_{i}}" title="k_{-i}=\frac{k_{i}}{K_{i}}" /></center>
其中，平衡常数从反应自由能<img src="https://latex.codecogs.com/svg.image?\Delta&space;G_{i}" title="\Delta G_{i}" />计算得到
<center><img src="https://latex.codecogs.com/svg.image?K_{i}=\exp&space;\left(-\frac{\Delta&space;G_{i}}{k_{\mathrm{B}}&space;T}\right)" title="K_{i}=\exp \left(-\frac{\Delta G_{i}}{k_{\mathrm{B}} T}\right)" /></center>

#### 质量作用定律（law of mass action）
基元反应的速率与反应物浓度（含有相应的指数）的乘积成正比，其中各浓度的指数就是反应式中各反应物质的计量系数。净的右向反应速率取决于正向及逆向反应速率的总结果，即
<center><img src="https://latex.codecogs.com/svg.image?r_{1}&space;=&space;k_{1}&space;x_{\mathrm{O}_{2}(\mathrm{aq})}-k_{-1}&space;x_{\mathrm{O}_{2}(\mathrm{dl})}" title="r_{1} = k_{1} x_{\mathrm{O}_{2}(\mathrm{aq})}-k_{-1} x_{\mathrm{O}_{2}(\mathrm{dl})}" /></center>
<center><img src="https://latex.codecogs.com/svg.image?r_{2}&space;=&space;k_{2}&space;x_{\mathrm{O}_{2}(\mathrm{dl})}&space;\theta_{*_{\mathrm{A}}}-k_{-2}&space;\theta_{\mathrm{O}_{2}&space;*_{\mathrm{A}}}" title="r_{2} = k_{2} x_{\mathrm{O}_{2}(\mathrm{dl})} \theta_{*_{\mathrm{A}}}-k_{-2} \theta_{\mathrm{O}_{2} *_{\mathrm{A}}}" /></center>
<center><img src="https://latex.codecogs.com/svg.image?r_{3}&space;=&space;k_{3}&space;\theta_{\mathrm{O}_{2}&space;*_{\mathrm{A}}}-k_{-3}&space;\theta_{\mathrm{OOH}&space;*_{\mathrm{A}}}" title="r_{3} = k_{3} \theta_{\mathrm{O}_{2} *_{\mathrm{A}}}-k_{-3} \theta_{\mathrm{OOH} *_{\mathrm{A}}}" /></center>
<center><img src="https://latex.codecogs.com/svg.image?r_{4}&space;=&space;k_{4}&space;\theta_{\mathrm{OOH}&space;*_{\mathrm{A}}}-k_{-4}&space;x_{\mathrm{H}_{2}&space;\mathrm{O}}&space;\theta_{\mathrm{O}&space;*_{\mathrm{A}}}" title="r_{4} = k_{4} \theta_{\mathrm{OOH} *_{\mathrm{A}}}-k_{-4} x_{\mathrm{H}_{2} \mathrm{O}} \theta_{\mathrm{O} *_{\mathrm{A}}}" /></center>
<center><img src="https://latex.codecogs.com/svg.image?r_{5}&space;=&space;k_{5}&space;\theta_{\mathrm{O}&space;*_{\mathrm{A}}}-k_{-5}&space;\theta_{\mathrm{OH}&space;*_{\mathrm{A}}}" title="r_{5} = k_{5} \theta_{\mathrm{O} *_{\mathrm{A}}}-k_{-5} \theta_{\mathrm{OH} *_{\mathrm{A}}}" /></center>
<center><img src="https://latex.codecogs.com/svg.image?r_{6}&space;=&space;k_{6}&space;\theta_{\mathrm{OH}&space;*_{\mathrm{A}}}-k_{-6}&space;\theta_{*_{\mathrm{A}}}&space;x_{\mathrm{H}_{2}&space;\mathrm{O}}" title="r_{6} = k_{6} \theta_{\mathrm{OH} *_{\mathrm{A}}}-k_{-6} \theta_{*_{\mathrm{A}}} x_{\mathrm{H}_{2} \mathrm{O}}" /></center>

#### 稳态近似法（steady state approximation method）
可以近似地认为在反应达到稳定状态后，中间体的浓度基本上不随时间而变化。对ORR过程中产生的中间体作稳态近似，得
<center><img src="https://latex.codecogs.com/svg.image?\frac{\partial&space;x_{\mathrm{O}_{2}(\mathrm{dl})}}{\partial&space;t}&space;=&space;r_{1}-r_{2}&space;=&space;0" title="\frac{\partial x_{\mathrm{O}_{2}(\mathrm{dl})}}{\partial t} = r_{1}-r_{2} = 0" /></center>
<center><img src="https://latex.codecogs.com/svg.image?\frac{\partial&space;\theta_{*_{\mathrm{A}}}}{\partial&space;t}&space;=&space;r_{6}-r_{2}&space;=&space;0" title="\frac{\partial \theta_{*_{\mathrm{A}}}}{\partial t} = r_{6}-r_{2} = 0" /></center>
<center><img src="https://latex.codecogs.com/svg.image?\frac{\partial&space;\theta_{\mathrm{O}_{2}&space;*_\mathrm{A}}}{\partial&space;t}&space;=&space;r_{2}-r_{3}&space;=&space;0" title="\frac{\partial \theta_{\mathrm{O}_{2} *_\mathrm{A}}}{\partial t} = r_{2}-r_{3} = 0" /></center>
<center><img src="https://latex.codecogs.com/svg.image?\frac{\partial&space;\theta_{\mathrm{OOH}&space;*_{\mathrm{A}}}}{\partial&space;t}&space;=&space;r_{3}-r_{4}&space;=&space;0" title="\frac{\partial \theta_{\mathrm{OOH} *_{\mathrm{A}}}}{\partial t} = r_{3}-r_{4} = 0" /></center>
<center><img src="https://latex.codecogs.com/svg.image?\frac{\partial&space;\theta_{\mathrm{O}&space;*_{\mathrm{A}}}}{\partial&space;t}&space;=&space;r_{4}-r_{5}&space;=&space;0" title="\frac{\partial \theta_{\mathrm{O} *_{\mathrm{A}}}}{\partial t} = r_{4}-r_{5} = 0" /></center>
<center><img src="https://latex.codecogs.com/svg.image?\frac{\partial&space;\theta_{\mathrm{OH}&space;*_{\mathrm{A}}}}{\partial&space;t}&space;=&space;r_{5}-r_{6}&space;=&space;0" title="\frac{\partial \theta_{\mathrm{OH} *_{\mathrm{A}}}}{\partial t} = r_{5}-r_{6} = 0" /></center>
*Note 1: 一组完整的催化反应历程，一定会包含每个中间体的消除步骤。否则，没有消除的中间体随时间变化率一定不等于0，就不能构成稳态平衡，比如支链爆炸。*  
*Note 2: 稳态平衡下，中间体随时间变化率为0，意味着表面催化反应的整个过程中，表面位点的化学环境都是保持不变的，而不会有任意一个中间体存在独立的化学环境。*

#### 表面位点守恒（conservation of surface sites）
所有反应中间体占据1个位点，覆盖度之和（包括空位点）为100%
<center><img src="https://latex.codecogs.com/svg.image?\theta_{*_{\mathrm{A}}}&plus;\theta_{\mathrm{O}_{2}&space;*_\mathrm{A}}&plus;\theta_{\mathrm{OOH}&space;*_{\mathrm{A}}}&plus;\theta_{\mathrm{O}&space;*_{\mathrm{A}}}&plus;\theta_{\mathrm{OH}&space;*_{\mathrm{A}}}=1" title="\theta_{*_{\mathrm{A}}}+\theta_{\mathrm{O}_{2} *_\mathrm{A}}+\theta_{\mathrm{OOH} *_{\mathrm{A}}}+\theta_{\mathrm{O} *_{\mathrm{A}}}+\theta_{\mathrm{OH} *_{\mathrm{A}}}=1" /></center>

#### 速控步近似
在一系列的连续反应（consecutive reaction）中，若其中有一步反应的速率最慢，它控制了总反应的速率，使反应的速率基本等于最慢一步的速率，则这最慢的一步反应称为速控步（rate controlling step）或决速步RDS（rate determining step）。例如，我们算得第3步的反应速率最小，则有总反应的速率为
<center><img src="https://latex.codecogs.com/svg.image?r&space;=&space;r_{3}&space;=&space;k_{3}&space;\theta_{\mathrm{O}_{2}&space;*_{\mathrm{A}}}-k_{-3}&space;\theta_{\mathrm{OOH}&space;*_{\mathrm{A}}}" title="r = r_{3} = k_{3} \theta_{\mathrm{O}_{2} *_{\mathrm{A}}}-k_{-3} \theta_{\mathrm{OOH} *_{\mathrm{A}}}" /></center>
式中存在两个中间产物的浓度项<img src="https://latex.codecogs.com/svg.image?\theta_{\mathrm{O}_{2}&space;*_{\mathrm{A}}}" title="\theta_{\mathrm{O}_{2} *_{\mathrm{A}}}" />和<img src="https://latex.codecogs.com/svg.image?\theta_{\mathrm{OOH}&space;*_{\mathrm{A}}}" title="\theta_{\mathrm{OOH} *_{\mathrm{A}}}" />，可通过平衡假设（equilibrium hypothesis）求出它们的值。即，假定其余快速平衡反应正、逆向反应间的平衡关系依然存在，从而可以利用平衡常数<img src="https://latex.codecogs.com/svg.image?K_{i}" title="K_{i}" />及反应物浓度来求出中间产物的浓度
<center><img src="https://latex.codecogs.com/svg.image?r_{1}&space;=&space;k_{1}&space;x_{\mathrm{O}_{2}(\mathrm{aq})}-k_{-1}&space;x_{\mathrm{O}_{2}(\mathrm{dl})}&space;=&space;0" title="r_{1} = k_{1} x_{\mathrm{O}_{2}(\mathrm{aq})}-k_{-1} x_{\mathrm{O}_{2}(\mathrm{dl})} = 0" /></center>
<center><img src="https://latex.codecogs.com/svg.image?r_{2}&space;=&space;k_{2}&space;x_{\mathrm{O}_{2}(\mathrm{dl})}&space;\theta_{*_{\mathrm{A}}}-k_{-2}&space;\theta_{\mathrm{O}_{2}&space;*_{\mathrm{A}}}&space;=&space;0" title="r_{2} = k_{2} x_{\mathrm{O}_{2}(\mathrm{dl})} \theta_{*_{\mathrm{A}}}-k_{-2} \theta_{\mathrm{O}_{2} *_{\mathrm{A}}} = 0" /></center>
<center><img src="https://latex.codecogs.com/svg.image?r_{4}&space;=&space;k_{4}&space;\theta_{\mathrm{OOH}&space;*_{\mathrm{A}}}-k_{-4}&space;x_{\mathrm{H}_{2}&space;\mathrm{O}}&space;\theta_{\mathrm{O}&space;*_{\mathrm{A}}}&space;=&space;0" title="r_{4} = k_{4} \theta_{\mathrm{OOH} *_{\mathrm{A}}}-k_{-4} x_{\mathrm{H}_{2} \mathrm{O}} \theta_{\mathrm{O} *_{\mathrm{A}}} = 0" /></center>
<center><img src="https://latex.codecogs.com/svg.image?r_{5}&space;=&space;k_{5}&space;\theta_{\mathrm{O}&space;*_{\mathrm{A}}}-k_{-5}&space;\theta_{\mathrm{OH}&space;*_{\mathrm{A}}}&space;=&space;0" title="r_{5} = k_{5} \theta_{\mathrm{O} *_{\mathrm{A}}}-k_{-5} \theta_{\mathrm{OH} *_{\mathrm{A}}} = 0" /></center>
<center><img src="https://latex.codecogs.com/svg.image?r_{6}&space;=&space;k_{6}&space;\theta_{\mathrm{OH}&space;*_{\mathrm{A}}}-k_{-6}&space;\theta_{*_{\mathrm{A}}}&space;x_{\mathrm{H}_{2}&space;\mathrm{O}}&space;=&space;0" title="r_{6} = k_{6} \theta_{\mathrm{OH} *_{\mathrm{A}}}-k_{-6} \theta_{*_{\mathrm{A}}} x_{\mathrm{H}_{2} \mathrm{O}} = 0" /></center>
注意，我们当前设计的ORR反应过程是一组连续反应。如果考虑平行反应（parallel reaction），如存在第7步与第4步是两个平行反应，则还须比较<img src="https://latex.codecogs.com/svg.image?r_{7}" title="r_{7}" />与<img src="https://latex.codecogs.com/svg.image?r_{4}" title="r_{4}" />，由更快一步的速率决定反应的路径。

转换频率TOF（turnover frequency）是指，在单位时间（秒）内，每个活性位点转化的分子数目
<center><img src="https://latex.codecogs.com/svg.image?\mathrm{TOF}_{\mathrm{H}^{&plus;}}=\mathrm{TOF}_{e^{-}}=-4r" title="\mathrm{TOF}_{\mathrm{H}^{+}}=\mathrm{TOF}_{e^{-}}=-4r" /></center>
<center><img src="https://latex.codecogs.com/svg.image?\mathrm{TOF}_{\mathrm{O}_{2}}=-r" title="\mathrm{TOF}_{\mathrm{O}_{2}}=-r" /></center>
<center><img src="https://latex.codecogs.com/svg.image?\mathrm{TOF}_{\mathrm{H}_{2}\mathrm{O}}=2r" title="\mathrm{TOF}_{\mathrm{H}_{2}\mathrm{O}}=2r" /></center>

### 求解速率方程
动力学模型是一组耦合的常微分方程组ODEs（ordinary differential equations），使用[CatMAP](<https://catmap.readthedocs.io/en/latest/index.html>)进行数值求解，代码在本文最后一节**使用CatMAP求解速率方程**给出。

### 计算电流密度
单位面积电极上通过的电流
<center><img src="https://latex.codecogs.com/svg.image?j=e&space;\rho&space;\mathrm{TOF}_{e^{-}}" title="j=e \rho \mathrm{TOF}_{e^{-}}" /></center>
其中，<img src="https://latex.codecogs.com/svg.image?\rho" title="\rho" />是表面活性位点密度，即单位面积上有多少个反应位点。对于**ORR on Pt(111)**，根据积分电荷（integrated charge），[Wang 2004](<https://doi.org/10.1021/jp037593v>)得出原子覆盖率（atomic coverage）为1/3。Pt的晶格常数为<img src="https://latex.codecogs.com/svg.image?a=2.77\&space;\mathrm{\AA}&space;" title="a=2.77\ \mathrm{\AA} " />，则包含1个Pt原子的Pt(111)1×1原胞表面积<img src="https://latex.codecogs.com/svg.image?A=6.65\&space;\mathrm{\AA}^{2}" title="A=6.65\ \mathrm{\AA}^{2}" />，该表面上有1/3个反应位点，即得表面活性位点密度<img src="https://latex.codecogs.com/svg.image?\rho=(1/3)/A" title="\rho=(1/3)/A" />。

*Note 3: 计算表面活性位点密度时，又出现了coverage的概念，这与速率方程中的coverage似乎是容易混淆的。这里稍微区分一下它们的不同：1) 速率方程中的覆盖度，倾向于强调在1个位点上，每个中间体在这个位点都有一个覆盖率值，我把它们理解为统计意义上的出现概率，而所有状态之和为100%；2) 活性位点密度中的覆盖度，倾向于强调表面上的金属原子位点中有百分之多少成为了反应位点，分母为实际的表面金属原子位点总数。*

### 使用CatMAP求解速率方程

#### 输入文件

##### `ORR_input.txt`文件
数据来自[Hansen 2014](<https://doi.org/10.1021/jp4100608>)
```
surface_name	site_name	species_name	formation_energy	bulk_structure	frequencies	other_parameters	reference
None	gas	pe	0.00	None	[]	[]	gas phase calcs
None	gas	H2O	0.00	None	[]	[]	Hansen 2014
None	gas	O2	5.19	None	[]	[]	Hansen 2014
Pt	dl	O2	5.19	fcc	[]	[]	Hansen 2014
Pt	a	O2	4.99	fcc	[]	[]	Hansen 2014
Pt	a	OOH	3.91	fcc	[]	[]	Hansen 2014
Pt	a	O	1.70	fcc	[]	[]	Hansen 2014
Pt	a	OH	0.75	fcc	[]	[]	Hansen 2014
Pt	dl	*	0.00	fcc	[]	[]	Hansen 2014
```
使用[Nørskov 2004](<https://doi.org/10.1021/jp047349j>)提出的computational hydrogen electrode (CHE) model，可以画出free-energy diagram如下图所示
<center><img src="../graphic/ORR/free_energy_diagram.svg" title="FED" width="75%"/></center>

##### `ORR.mkm`文件
mkm文件中包含构建微观动力学模型所需要的所有参数。
```python
scaler = 'ThermodynamicScaler' # use T/p/U as descriptors and treat energetics as a constant

rxn_expressions = [
    'O2_g + *_dl <-> O2_dl; prefactor=8e5',                    # rxn 1 - O2 to O2 in double layer
    '*_a + O2_dl -> O2_a + *_dl; prefactor=1e8',               # rxn 2 - O2 double layer adsorption to a
    'O2_a + pe_g -> ^0.26eV_a -> OOH_a; prefactor=1e9',        # rxn 3 - O2 -> OOH on a
    'OOH_a + pe_g -> ^0.26eV_a -> O_a + H2O_g; prefactor=1e9', # rxn 4 - OOH -> O + H2O on a
    'O_a + pe_g -> ^0.26eV_a -> OH_a; prefactor=1e9',          # rxn 5 - O -> OH on a
    'OH_a + pe_g -> ^0.26eV_a -> *_a + H2O_g; prefactor=1e9',  # rxn 6 - OH -> H2O on a
]

surface_names = ['Pt',]

descriptor_names= ['voltage', 'temperature'] # voltage/temperature/pressure
descriptor_ranges = [[0., 1.23], [298.15, 298.15]]
resolution = [151, 1]

beta = 0.5

species_definitions = {}
# assume heine's free energy numbers are already pressure-corrected
species_definitions['H2O_g'] = {'pressure': 1.}
species_definitions['O2_g'] = {'pressure': 2.34e-05}
species_definitions['pe_g'] = {'pressure': 1.}

species_definitions['a'] = {'site_names': ['a'], 'total': 1.}
species_definitions['dl'] = {'site_names': ['dl'], 'total': 1.}

data_file = 'ORR.pkl'
input_file = 'ORR_input.txt'

gas_thermo_mode = 'frozen_gas'
adsorbate_thermo_mode = 'frozen_adsorbate'
electrochemical_thermo_mode = 'simple_electrochemical'

decimal_precision = 200
tolerance = 1e-50
max_rootfinding_iterations = 1000
max_bisections = 5
```
在代码中，<img src="https://latex.codecogs.com/svg.image?\mathrm{O}_{2}" title="\mathrm{O}_{2}" />从本体溶液中扩散到电极附近被写作一个化学步骤。因此，双电层（double layer）成为了一个“反应位点”。额外的位点守恒被隐性地包含在ORR过程中
<center><img src="https://latex.codecogs.com/svg.image?\theta_{*\left(\mathrm{dl}\right)}&plus;\theta_{\mathrm{O}_{2}\left(\mathrm{dl}\right)}=1" title="\theta_{*\left(\mathrm{dl}\right)}+\theta_{\mathrm{O}_{2}\left(\mathrm{dl}\right)}=1" /></center>
注意，化学式中的上下标和特殊符号，在代码中为了表达得更加严谨，可能与文献表述略有出入。\*不是位点，而是None/没有吸附的意思，A和dl才是位点名称。

##### `mkm_job.py`文件
py文件设定输入输出，运行微观动力学计算
```python
from catmap import ReactionModel, analyze
import numpy as np
from ase.build import fcc111
from ase.units import C, m

##### run model #####
model = ReactionModel(
    setup_file='ORR.mkm',
    output_variables=['coverage', 'turnover_frequency',]
)
model.run()

vm = analyze.VectorMap(model)
##### plot TOF #####
vm.plot_variable = 'turnover_frequency'
labels = vm.get_labels()
pts_cols = vm.get_pts_cols()
print(labels)
# ['H2O_g', 'O2_g', 'pe_g']

U = pts_cols[0]
i_pe = labels.index('pe_g') # 电子的索引
TOF_pe = np.array(pts_cols[1][i_pe])

cm = 1e-02*m
e = 10**3/C # elementary charge in mC

area = np.linalg.norm(np.cross(*fcc111('Pt', (1, 1, 1)).get_cell()[:2])) # 表面积
area /= cm**2 # cm^-2
rho = (1/3)/area # 每个1*1原胞表面有1/3个反应位点
j = e*rho*TOF_pe # mA cm^-2

##### plot coverage #####
vm.plot_variable = 'coverage'
labels = vm.get_labels()
pts_cols = vm.get_pts_cols()
print(labels)
# ['O2_a', 'OH_a', 'OOH_a', 'O_a', 'O2_dl']

U = pts_cols[0]
i = 1 # OH_a
label = labels[i]
theta = pts_cols[1][i]
```

#### 计算结果
计算电流密度重现了[Hansen 2014](<https://doi.org/10.1021/jp4100608>)的结果。图b使用的数据与图a相同，只是为了计算Tafel斜率而作的进一步处理。
<center><img src="../graphic/ORR/current_density.svg" title="current density" width="95%"/></center>
尽可能考虑完整的反应网络，包括其它反应路径、其它反应位点、其它反应产物，以及传质（扩散）等物理过程，可以使理论计算结果更加贴合实验现象。如有副产物，即可通过计算法拉第效率揭示产物选择性。

不同外加电势下的理论覆盖度。图b使用的数据与图a相同，在log10标度下可以清晰地显示微量物种的覆盖度。
<center><img src="../graphic/ORR/coverages.svg" title="coverages" width="95%"/></center>
某物种A具有较高的覆盖度，代表该物种A难以转化为其它物种而使A大量地滞留在表面。A到其它物种的转化步骤成为决速步。

[[Back]](../)
