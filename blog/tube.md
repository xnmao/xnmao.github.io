---
layout: default
---

## 构建BC3纳米管

通过把二维单层BC3卷成筒状，构建三维BC3纳米管周期性模型
```python
from ase.build import graphene
from ase.visualize import view
import numpy as np

# primitive HEX2D
atoms = graphene(a=2.59615, size=(2, 2, 1)) # lattice parameter
atoms.symbols[[0, 3]] = 'B'

# HEX2D to RECT
# a==b!=c; alpha==beta==90, gamma==120 -> a!=b!=c; alpha==beta==gamma==90
atoms = atoms.repeat((2, 2, 1))
cell = atoms.get_cell()
atoms.set_cell(((0.5, 0, 0), (0, 1, 0), (0, 0, 1))*cell)
scaled_positions = atoms.get_scaled_positions(wrap=False)
eps = 1e-03 # delete mirror atoms
atoms = atoms[((scaled_positions>-eps)&(scaled_positions<1-eps)).all(axis=1)]

index = 0 # 卷曲方向(0或1)
size = 20 # 截面圆包含重复单元数(控制管径)

# to supercell
rep = [1, 1, 1]
rep[index] = size
atoms = atoms.repeat(rep)

# roll up
X = atoms.get_positions()[:, index]
r = 0.5/np.pi*atoms.get_cell()[index, index] # radius
atoms.positions[:, index] = r*(1-np.cos(X/r)) # theta = length_of_arc/radius
atoms.positions[:, 2] = r*np.sin(X/r)

# fancy
atoms.center(vacuum=7.5, axis=[index, 2]) # add vacuum
atoms.set_pbc((True, True, True))

# save
# view(atoms)
atoms.write('tube.cif')
```

[[Back]](../)
