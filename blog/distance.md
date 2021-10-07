---
layout: default
---

## 使用Python求解点到直线的距离

（百度搜到的代码洋洋洒洒有20行，一点不pythonic）

已知：
1. 点的坐标：(a, b)
2. 直线方程：y-y0 = k\*(x-x0)

求该点到该直线的距离

代码如下：
```python
import numpy as np
d = np.cross((1, k), (x-x0, y-y0))/np.linalg.norm((1, k))
```
这样就可以得到点到直线的距离为`abs(d)`

[back](./)
