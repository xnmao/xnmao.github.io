---
layout: default
---

## 使用sympy绘制原子轨道

```python
import numpy as np
import matplotlib.pyplot as plt
%matplotlib auto
from mpl_toolkits.mplot3d import Axes3D

from sympy import symbols, lambdify
from sympy.functions import Znm


def set_3d_axes_equal(ax, ratio=0.5):
    x_limits, y_limits, z_limits = ax.get_xlim3d(), ax.get_ylim3d(), ax.get_zlim3d()
    x_range, y_range, z_range = abs(x_limits[1]-x_limits[0]), abs(y_limits[1]-y_limits[0]), abs(z_limits[1]-z_limits[0])

    x_middle, y_middle, z_middle = np.mean(x_limits), np.mean(y_limits), np.mean(z_limits)
    plot_radius = ratio*max([x_range, y_range, z_range])
    
    ax.set_xlim3d([x_middle-plot_radius, x_middle+plot_radius])
    ax.set_ylim3d([y_middle-plot_radius, y_middle+plot_radius])
    ax.set_zlim3d([z_middle-plot_radius, z_middle+plot_radius])

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

def plot_angular(l, m, ax, spa=30, cmap='jet'): # 绘制波函数

    spa = complex(0, spa) # 格点
    theta, phi = np.mgrid[0:np.pi:spa, 0:2*np.pi:2*spa]
    Ylm = angular_func(l, m, theta, phi)
    ax.plot_surface(*sph2cart(np.abs(Ylm), theta, phi), lw=2, cmap=plt.get_cmap(cmap), alpha=.8)
#     ax.plot_wireframe(*sph2cart(np.abs(Ylm), theta, phi), lw=2, cmap=plt.get_cmap(cmap), alpha=.8)

    ax.set_xlabel('x', labelpad=-10)
    ax.set_ylabel('y', labelpad=-10)
    ax.set_zlabel('z', labelpad=-10)
    ax.set_xlim((-0.6, 0.6))
    ax.set_ylim((-0.6, 0.6))
    ax.set_zlim((-0.6, 0.6))
    ax.set_xticks([-0.5, 0.0, 0.5])
    ax.set_yticks([-0.5, 0.0, 0.5])
    ax.set_zticks([-0.5, 0.0, 0.5])
    ax.set_xticklabels([])
    ax.set_yticklabels([])
    ax.set_zticklabels([])
    set_3d_axes_equal(ax, ratio=0.5)

if __name__ == '__main__':
    fig = plt.figure(figsize=(6, 4))
    ax = fig.add_subplot(1, 1, 1, projection='3d')
    ax.set_box_aspect((1, 1, 1))
    plot_angular(l=2, m=1, ax=ax)
    plt.show()
```

[[Back]](../)
