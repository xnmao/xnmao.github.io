---
layout: default
---

## 使用Python求解点到直线的距离

（百度搜到的代码洋洋洒洒有20行，一点不pythonic）

已知：
1. 点的坐标：(`a`, `b`)
2. 直线方程：y-`y0` = `k`\*(x-`x0`)

求该点到该直线的距离

代码如下：
```python
import numpy as np

a, b = 4, 4 # 定义点的坐标(4, 4)
k, x0, y0 = 2, 2, 5 # 定义直线方程y-5=2*(x-2)
d = np.cross((1, k), (a-x0, b-y0))/np.linalg.norm((1, k))
print(abs(d)) # 输出点到直线的距离2.236
```

[[Back]](../)
