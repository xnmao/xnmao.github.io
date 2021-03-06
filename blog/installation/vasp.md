---
layout: default
---

### VASP

#### 操作步骤
1. 解压缩`vasp.5.4.4.tar.gz`文件
```shell
$ tar -xf vasp.5.4.4.tar.gz
```
2. 从模板创建`makefile.include`文件
```shell
$ cd vasp.5.4.4/
$ cp arch/makefile.include.linux_intel makefile.include
```
3. 编辑`makefile.include`文件，`CPP_OPTIONS`中追加`-Dsol_compat`参数（用于对应VASP5.4.4版本的VASPsol），`FFLAGS`中追加`-xHOST`参数（计算提速）
```shell
FFLAGS     = -assume byterecl -w -xHOST
```
4. 添加VASPsol文件
```shell
$ cd ../
$ git clone git@github.com:henniggroup/VASPsol.git
$ cp VASPsol/src/solvation.F vasp.5.4.4/src/
$ patch vasp.5.4.4/src/pot.F VASPsol/src/patches/pbz_patch_541
```
5. 编译VASP
```shell
$ cd vasp.5.4.4/
$ make std gam ncl
```

#### 参考链接
1. [Building VASP\* with Intel® oneAPI Base and HPC Toolkits](<https://www.intel.com/content/www/us/en/developer/articles/technical/building-vasp-with-intel-mkl-and-intel-compilers.html>)
2. [VASP的最简单的安装方法](<http://bbs.keinsci.com/thread-11812-1-1.html>)
3. [云极高性能计算-操作指南-VASP安装](<https://docs.ucloud.cn/epc/vasp>)
4. [A Ubuntu based installation of VASP](<https://www.vasp.at/wiki/index.php/A_Ubuntu_based_installation_of_VASP>)
5. [GNU 编译 VASP.5.4.1 +VTST +VASPsol](<https://zhuanlan.zhihu.com/p/336559314>)
6. [VASPsol Solid/Liquid Interfaces for DFT code VASP](<https://github.com/henniggroup/VASPsol>)

[[Back]](../tools.md)
