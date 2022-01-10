---
layout: default
---

## 电催化微观动力学建模

### 设计ORR反应过程

1. O2从本体溶液中扩散到电极附近<center><img src="https://latex.codecogs.com/svg.image?\mathrm{O}_{2}(\mathrm{aq})&space;\underset{k_{-1}}{\stackrel{k_{1}}{\rightleftharpoons}}&space;\mathrm{O}_{2}(\mathrm{dl})" title="\mathrm{O}_{2}(\mathrm{aq}) \underset{k_{-1}}{\stackrel{k_{1}}{\rightleftharpoons}} \mathrm{O}_{2}(\mathrm{dl})" /></center>
2. O2从电极附近的溶液中移到电极上，形成吸附在反应位点A的\*O2<center><img src="https://latex.codecogs.com/svg.image?\mathrm{O}_{2}(\mathrm{dl})&plus;*_{\mathrm{A}}&space;\underset{k_{-2}}{\stackrel{k_{2}}{\rightleftharpoons}}&space;\mathrm{O}_{2}&space;*_{\mathrm{A}}" title="\mathrm{O}_{2}(\mathrm{dl})+*_{\mathrm{A}} \underset{k_{-2}}{\stackrel{k_{2}}{\rightleftharpoons}} \mathrm{O}_{2} *_{\mathrm{A}}" /></center>
3. H+和已经被吸附在反应位点A上的\*O2反应生成\*OOH中间体<center><img src="https://latex.codecogs.com/svg.image?\mathrm{O}_{2}&space;*_{\mathrm{A}}&plus;\mathrm{H}^{&plus;}&plus;\mathrm{e}^{-}&space;\underset{k_{-3}}{\stackrel{k_{3}}{\rightleftharpoons}}&space;\mathrm{OOH}&space;*_{\mathrm{A}}" title="\mathrm{O}_{2} *_{\mathrm{A}}+\mathrm{H}^{+}+\mathrm{e}^{-} \underset{k_{-3}}{\stackrel{k_{3}}{\rightleftharpoons}} \mathrm{OOH} *_{\mathrm{A}}" /></center>
4. H+和已经被吸附在反应位点A上的\*OOH中间体反应生成\*O中间体和H2O<center><img src="https://latex.codecogs.com/svg.image?\mathrm{OOH}&space;*_{\mathrm{A}}&plus;\mathrm{H}^{&plus;}&plus;\mathrm{e}^{-}&space;\underset{k_{-4}}{\stackrel{k_{4}}{\rightleftharpoons}}&space;\mathrm{O}&space;*_{\mathrm{A}}&plus;\mathrm{H}_{2}&space;\mathrm{O}" title="\mathrm{OOH} *_{\mathrm{A}}+\mathrm{H}^{+}+\mathrm{e}^{-} \underset{k_{-4}}{\stackrel{k_{4}}{\rightleftharpoons}} \mathrm{O} *_{\mathrm{A}}+\mathrm{H}_{2} \mathrm{O}" /></center>
5. H+和已经被吸附在反应位点A上的\*O中间体反应生成\*OH中间体<center><img src="https://latex.codecogs.com/svg.image?\mathrm{O}&space;*_{\mathrm{A}}&plus;\mathrm{H}^{&plus;}&plus;\mathrm{e}^{-}&space;\underset{k_{-5}}{\stackrel{k_{5}}{\rightleftharpoons}}&space;\mathrm{OH}&space;*_{\mathrm{A}}" title="\mathrm{O} *_{\mathrm{A}}+\mathrm{H}^{+}+\mathrm{e}^{-} \underset{k_{-5}}{\stackrel{k_{5}}{\rightleftharpoons}} \mathrm{OH} *_{\mathrm{A}}" /></center>
6. H+和已经被吸附在反应位点A上的\*OH中间体反应生成H2O<center><img src="https://latex.codecogs.com/svg.image?\mathrm{OH}&space;*_{\mathrm{A}}&plus;\mathrm{H}^{&plus;}&plus;\mathrm{e}^{-}&space;\underset{k_{-6}}{\stackrel{k_{6}}{\rightleftharpoons}}&space;*_{\mathrm{A}}&plus;\mathrm{H}_{2}&space;\mathrm{O}" title="\mathrm{OH} *_{\mathrm{A}}+\mathrm{H}^{+}+\mathrm{e}^{-} \underset{k_{-6}}{\stackrel{k_{6}}{\rightleftharpoons}} *_{\mathrm{A}}+\mathrm{H}_{2} \mathrm{O}" /></center>

### 建立微分方程

#### 反应速率常数
1. 对于化学反应<center><img src="https://latex.codecogs.com/svg.image?k_{i}=\frac{k_{\mathrm{B}}&space;T}{h}&space;\exp&space;\left(-\frac{G_{a,&space;i}}{k_{\mathrm{B}}&space;T}\right)" title="k_{i}=\frac{k_{\mathrm{B}} T}{h} \exp \left(-\frac{G_{a, i}}{k_{\mathrm{B}} T}\right)" /></center>
2. 写成包含指前因子的形式<center><img src="https://latex.codecogs.com/svg.image?k_{i}=\nu_{i}&space;\exp&space;\left(-\frac{E_{a,&space;i}}{k_{\mathrm{B}}&space;T}\right)" title="k_{i}=\nu_{i} \exp \left(-\frac{E_{a, i}}{k_{\mathrm{B}} T}\right)" /></center>
2. 对于电化学反应<center><img src="https://latex.codecogs.com/svg.image?k_{i}=\frac{k_{\mathrm{B}}&space;T}{h}&space;\exp&space;\left(-\frac{G_{a,&space;i}^{0}}{k_{\mathrm{B}}&space;T}\right)&space;\exp&space;\left(-\frac{e&space;\beta_{i}\left(U-U_{i}^{0}\right)}{k_{\mathrm{B}}&space;T}\right)" title="k_{i}=\frac{k_{\mathrm{B}} T}{h} \exp \left(-\frac{G_{a, i}^{0}}{k_{\mathrm{B}} T}\right) \exp \left(-\frac{e \beta_{i}\left(U-U_{i}^{0}\right)}{k_{\mathrm{B}} T}\right)" /></center>
3. 重新写一遍<center><img src="https://latex.codecogs.com/svg.image?k_{i}=A_{i}&space;\exp&space;\left(-\frac{E_{a,&space;i}^{0}}{k_{\mathrm{B}}&space;T}\right)&space;\exp&space;\left(-\frac{e&space;\beta_{i}\left(U-U_{i}^{0}\right)}{k_{\mathrm{B}}&space;T}\right)" title="k_{i}=A_{i} \exp \left(-\frac{E_{a, i}^{0}}{k_{\mathrm{B}} T}\right) \exp \left(-\frac{e \beta_{i}\left(U-U_{i}^{0}\right)}{k_{\mathrm{B}} T}\right)" /></center>
4. 逆反应速率常数<center><img src="https://latex.codecogs.com/svg.image?k_{-i}=\frac{k_{i}}{K_{i}}" title="k_{-i}=\frac{k_{i}}{K_{i}}" /></center>
5. 平衡常数<center><img src="https://latex.codecogs.com/svg.image?K_{i}=\exp&space;\left(-\frac{\Delta&space;G_{i}}{k_{\mathrm{B}}&space;T}\right)" title="K_{i}=\exp \left(-\frac{\Delta G_{i}}{k_{\mathrm{B}} T}\right)" /></center>

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

#### 表面位点守恒（conservation of surface sites）
假设所有反应中间体占据1个位点，即
<center><img src="https://latex.codecogs.com/svg.image?\theta_{*_{\mathrm{A}}}&plus;\theta_{\mathrm{O}_{2}&space;*_\mathrm{A}}&plus;\theta_{\mathrm{OOH}&space;*_{\mathrm{A}}}&plus;\theta_{\mathrm{O}&space;*_{\mathrm{A}}}&plus;\theta_{\mathrm{OH}&space;*_{\mathrm{A}}}=1" title="\theta_{*_{\mathrm{A}}}+\theta_{\mathrm{O}_{2} *_\mathrm{A}}+\theta_{\mathrm{OOH} *_{\mathrm{A}}}+\theta_{\mathrm{O} *_{\mathrm{A}}}+\theta_{\mathrm{OH} *_{\mathrm{A}}}=1" /></center>

#### 求解速率方程

#### 速控步近似
在一系列的连续反应中，若其中有一步反应的速率最慢，它控制了总反应的速率，使反应的速率基本等于最慢一步的速率，则这最慢的一步反应称为速控步（rate controlling step）或决速步（rate determining step），即
<center><img src="https://latex.codecogs.com/svg.image?r=\max\left(r_{1},r_{2},r_{3},r_{4},r_{5},r_{6}\right)" title="r=\max\left(r_{1},r_{2},r_{3},r_{4},r_{5},r_{6}\right)" /></center>
根据总反应，
<center><img src="https://latex.codecogs.com/svg.image?\mathrm{TOF}_{\mathrm{H}^{&plus;}}=\mathrm{TOF}_{e^{-}}=-4r" title="\mathrm{TOF}_{\mathrm{H}^{+}}=\mathrm{TOF}_{e^{-}}=-4r" /></center>
<center><img src="https://latex.codecogs.com/svg.image?\mathrm{TOF}_{\mathrm{O}_{2}}=-r" title="\mathrm{TOF}_{\mathrm{O}_{2}}=-r" /></center>
<center><img src="https://latex.codecogs.com/svg.image?\mathrm{TOF}_{\mathrm{H}_{2}\mathrm{O}}=2r" title="\mathrm{TOF}_{\mathrm{H}_{2}\mathrm{O}}=2r" /></center>

#### 计算电流密度
单位面积电极上通过的电流
<center><img src="https://latex.codecogs.com/svg.image?j=e&space;\rho&space;\mathrm{TOF}_{e^{-}}" title="j=e \rho \mathrm{TOF}_{e^{-}}" /></center>

### 使用CatMAP求解

#### 输入文件

##### `ORR_input.txt`文件
```
surface_name	site_name	species_name	formation_energy	bulk_structure	frequencies	other_parameters	reference
None	gas	pe	0.0	None	[]	[]	gas phase calcs
None	gas	H2O	0.0	None	[]	[]	Hansen 2014
None	gas	O2	5.19	None	[]	[]	Hansen 2014
Pt	a	O2	4.99	fcc	[]	[]	Hansen 2014
Pt	dl	O2	5.19	fcc	[]	[]	Hansen 2014
Pt	a	OOH	3.91	fcc	[]	[]	Hansen 2014
Pt	a	O	1.7	fcc	[]	[]	Hansen 2014
Pt	a	OH	0.75	fcc	[]	[]	Hansen 2014
Pt	dl	*	0.0	fcc	[]	[]	Hansen 2014
```
![FED](../graphic/ORR/free_energy_diagram.svg)

##### `ORR.mkm`文件
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

##### `mkm_job.py`文件

#### 计算结果
电流密度
<img src="../graphic/ORR/current_density.svg" title="current density" width="85%" align=center />
覆盖度
<img src="../graphic/ORR/coverages.svg" title="coverages" width="85%" align=center />

[[Back]](../)
