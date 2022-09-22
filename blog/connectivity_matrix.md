---
layout: default
---

## 使用ASE构建邻接矩阵

### 定义
基于原子对象的初始编号，给出哪个原子连接哪个原子的矩阵。

### 方法
```python
from ase.neighborlist import natural_cutoffs, NeighborList
from ase.build import molecule

atoms = molecule('CH3CH2OH')

cutoffs = natural_cutoffs(atoms)
nl = NeighborList(cutoffs, self_interaction=True, bothways=True)
nl.update(atoms)
matrix = nl.get_connectivity_matrix(sparse=False)

print(matrix)
```

```shell
[[1 1 0 0 0 0 1 1 1]
 [1 1 1 0 1 1 0 0 0]
 [0 1 1 1 0 0 0 0 0]
 [0 0 1 1 0 0 0 0 0]
 [0 1 0 0 1 0 0 0 0]
 [0 1 0 0 0 1 0 0 0]
 [1 0 0 0 0 0 1 0 0]
 [1 0 0 0 0 0 0 1 0]
 [1 0 0 0 0 0 0 0 1]]
```

### 参考
<https://wiki.fysik.dtu.dk/ase/ase/neighborlist.html#ase.neighborlist.get_connectivity_matrix>

[[Back]](../)
