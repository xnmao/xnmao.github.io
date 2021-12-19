---
layout: default
---

## 构建碳纳米管

通过把二维单层石墨烯卷成筒状，构建三维碳纳米管周期性模型
```python
from ase.build import graphene
from ase.visualize import view
import numpy as np

# HEX2D to RECT
atoms = graphene(a=2.46, size=(2, 2, 1)) # lattice parameter
atoms.cell[0] = atoms.get_distance(0, 4, vector=True)
atoms.cell[1] = atoms.get_distance(1, 6, vector=True)*3
atoms = atoms[[0, 1, 6, 3]]

index = 0 # 石墨烯卷曲方向(0或1)
size = 50 # 碳管截面圆包含重复单元数(控制管径)

# to supercell
rep = [1, 1, 1]
rep[index] = size
atoms = atoms.repeat(rep)

# roll up
l = atoms.get_cell()[index, index]*0.5 # circumference*0.5
X = atoms.get_positions()[:, index]
r = l/np.pi # radius
atoms.positions[:, index] = l/np.pi*(1-np.cos(X/r)) # theta = length_of_arc/radius
atoms.positions[:, 2] = l/np.pi*np.sin(X/r)

# fancy
atoms.center(vacuum=7.5, axis=[index, 2]) # add vacuum
atoms.set_pbc((True, True, True))

# save
# view(atoms)
atoms.write('tube.cif')
```

[[Back]](../)
