---
layout: default
---

## 使用ASE构建邻接矩阵

### 定义
基于原子对象的初始编号，给出哪个原子连接哪个原子的矩阵。
可用于图神经网络。

### 方法
```python
from ase.neighborlist import natural_cutoffs, NeighborList
from ase.build import molecule

atoms = molecule('CH3CH2OH')

cutoffs = natural_cutoffs(atoms)
nl = NeighborList(cutoffs, self_interaction=False, bothways=True)
nl.update(atoms)
matrix = nl.get_connectivity_matrix(sparse=False)

print(matrix)
```

```shell
[[0 1 0 0 0 0 1 1 1]
 [1 0 1 0 1 1 0 0 0]
 [0 1 0 1 0 0 0 0 0]
 [0 0 1 0 0 0 0 0 0]
 [0 1 0 0 0 0 0 0 0]
 [0 1 0 0 0 0 0 0 0]
 [1 0 0 0 0 0 0 0 0]
 [1 0 0 0 0 0 0 0 0]
 [1 0 0 0 0 0 0 0 0]]
```
使用这个可以获得n行n列的矩阵，n为原子的总数。第0行第1列的值为1，代表0号原子和1号原子之间成化学键。同样地，第1行第0列的值为1，其意义与第0行第1列相同。是因为我们设置了`bothways=True`。
第0行第0列的值，定义原子自己和自己是否算作成键，当前显示0是因为我们设置了`self_interaction=False`。

### 参考
<https://wiki.fysik.dtu.dk/ase/ase/neighborlist.html#ase.neighborlist.get_connectivity_matrix>

[[Back]](../)
