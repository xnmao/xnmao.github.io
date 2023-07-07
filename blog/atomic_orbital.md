---
layout: default
---

## 使用sympy绘制原子轨道等值线图

```python
import numpy as np
import matplotlib.pyplot as plt
from sympy import symbols, lambdify
from sympy.functions import Znm


def set_3d_axes_equal(ax, ratio=0.5):
    xmin, xmax = ax.get_xlim3d()
    ymin, ymax = ax.get_ylim3d()
    zmin, zmax = ax.get_zlim3d()
    x_0, y_0, z_0 = np.mean(((xmin, xmax), (ymin, ymax), (zmin, zmax)), axis=1)
    plot_radius = ratio*max([xmax-xmin, ymax-ymin, zmax-zmin])
    ax.set_xlim3d([x_0-plot_radius, x_0+plot_radius])
    ax.set_ylim3d([y_0-plot_radius, y_0+plot_radius])
    ax.set_zlim3d([z_0-plot_radius, z_0+plot_radius])

def sph2cart(r, theta, phi): # 球坐标和直角坐标的三维变换
    if np.any(r<0):
        print('r>=0!') # 向径范围[0, +∞)
    if np.any(theta<0) or np.any(theta>np.pi):
        print('0<=theta<=pi!') # 与z+的夹角范围[0, π]
    if np.any(phi<0) or np.any(phi>2*np.pi):
        print('0<=phi<=2pi!') # 与x+的夹角范围[0, 2π]
    return (r*np.sin(theta)*np.cos(phi), r*np.sin(theta)*np.sin(phi), r*np.cos(theta))

def _angular_func(n, m): # 生成角度函数
    theta, phi = symbols(('theta', 'phi'))
    return lambdify([theta, phi], Znm(n, m, theta, phi).expand(func=True), modules='numpy')

def angular_func(n, m, theta, phi): # 角度函数
    f = _angular_func(n, m)
    return f(theta, phi).real # 去掉虚部

def plot_angular(l, m, ax, spa=50, cmap='jet'): # 绘制波函数
    spa = complex(0, spa) # 格点
    theta, phi = np.mgrid[0:np.pi:spa, 0:2*np.pi:2*spa]
    Ylm = angular_func(l, m, theta, phi)
    ax.plot_surface(*sph2cart(np.abs(Ylm), theta, phi), lw=2, cmap=plt.get_cmap(cmap), alpha=.8)
    # ax.plot_wireframe(*sph2cart(np.abs(Ylm), theta, phi), lw=2, cmap=plt.get_cmap(cmap), alpha=.8)
    set_3d_axes_equal(ax)
    ax.set_xlabel('x')
    ax.set_ylabel('y')
    ax.set_zlabel('z')
    ax.set_box_aspect((1, 1, 1))


if __name__ == '__main__':
    l, m = 2, -1 # 角量子数, 磁量子数
    fig = plt.figure()
    ax = fig.add_subplot(1, 1, 1, projection='3d')
    plot_angular(l=l, m=m, ax=ax)
    plt.show()
```

[[Back]](../)
