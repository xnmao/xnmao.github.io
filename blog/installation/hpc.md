---
layout: default
---

## 超算配置手册

### oneMKL & HPC Toolkit

1. 下载[Intel® oneAPI Math Kernel Library](<https://www.intel.com/content/www/us/en/developer/articles/tool/oneapi-standalone-components.html#onemkl>)安装包。找到Intel oneAPI Math Kernel Library for Linux
```shell
https://www.intel.com/content/www/us/en/developer/articles/tool/oneapi-standalone-components.html#onemkl
```
2. 下载[Intel® oneAPI HPC Toolkit](<https://www.intel.com/content/www/us/en/developer/tools/oneapi/hpc-toolkit-download.html?packages=hpc-toolkit&hpc-toolkit-os=linux&hpc-toolkit-lin=offline>)、[Intel® Fortran Essentials](<https://www.intel.com/content/www/us/en/developer/tools/oneapi/hpc-toolkit-download.html?packages=fortran-essentials&fortran-essentials-os=linux&fortran-essentials-lin=offline>)、[Intel® C++ Essentials](<https://www.intel.com/content/www/us/en/developer/tools/oneapi/hpc-toolkit-download.html?packages=cpp-essentials&cpp-essentials-os=linux&cpp-essentials-lin=offline>)安装包（Linux -> Online & Offline (recommended) -> Offline）。找到`Continue as a Guest (download starts immediately) →`
```shell
https://www.intel.com/content/www/us/en/developer/tools/oneapi/hpc-toolkit-download.html?packages=hpc-toolkit&hpc-toolkit-os=linux&hpc-toolkit-lin=offline
https://www.intel.com/content/www/us/en/developer/tools/oneapi/hpc-toolkit-download.html?packages=fortran-essentials&fortran-essentials-os=linux&fortran-essentials-lin=offline
https://www.intel.com/content/www/us/en/developer/tools/oneapi/hpc-toolkit-download.html?packages=cpp-essentials&cpp-essentials-os=linux&cpp-essentials-lin=offline
```
3. 安装Intel® oneAPI，即运行
```shell
$ bash intel-onemkl-2025.2.0.629_offline.sh
$ bash intel-oneapi-hpc-toolkit-2025.2.0.575_offline.sh
$ bash intel-fortran-essentials-2025.2.0.509_offline.sh
$ bash intel-cpp-essentials-2025.2.0.532_offline.sh
```
4. 在`~/.bashrc`中添加命令
```shell
. ~/intel/oneapi/setvars.sh
```

### Anaconda

1. 下载[Distribution Installer](<https://www.anaconda.com/download/success>)。找到64-Bit (x86) Installer，复制链接地址，运行
```shell
$ wget https://repo.anaconda.com/archive/Anaconda3-2025.06-0-Linux-x86_64.sh
```
2. 安装Anaconda，即运行
```shell
$ bash Anaconda3-2025.06-0-Linux-x86_64.sh
```

### Atomic Simulation Environment

1. 下载最新版本的`.whl`文件
```shell
https://pypi.org/simple/ase/
```
2. 安装ASE，即运行
```shell
pip install ase-3.25.0-py3-none-any.whl
```

### Vienna Ab initio Simulation Package

1. 解压缩`vasp.5.4.4.tar.gz`文件
```shell
$ tar -xf vasp.5.4.4.tar.gz
```
2. 从模板创建`makefile.include`文件
```shell
$ cd vasp.5.4.4/
$ cp arch/makefile.include.linux_intel makefile.include
```
3. 重新编辑`makefile.include`文件，模板如下
```bash
# Precompiler options
CPP_OPTIONS= -DHOST=\"LinuxIFC\"\
             -DMPI -DMPI_BLOCK=8000 \
             -Duse_collective \
             -DscaLAPACK \
             -DCACHE_SIZE=4000 \
             -Davoidalloc \
             -Duse_bse_te \
             -Dtbdyn \
             -Duse_shmem \
             -Dsol_compat

CPP        = fpp -f_com=no -free -w0  $*$(FUFFIX) $*$(SUFFIX) $(CPP_OPTIONS)

FC         = mpiifx
FCL        = mpiifx -mkl=sequential -lstdc++

FREE       = -free -names lowercase

FFLAGS     = -assume byterecl -w -xHOST -traceback -fpp -no-wrap-margin
OFLAG      = -O2
OFLAG_IN   = $(OFLAG)
DEBUG      = -O0

MKL_PATH   = $(MKLROOT)/lib/intel64
BLAS       =
LAPACK     =
BLACS      = -lmkl_blacs_intelmpi_lp64
SCALAPACK  = $(MKL_PATH)/libmkl_scalapack_lp64.a $(BLACS)

OBJECTS    = fftmpiw.o fftmpi_map.o fft3dlib.o fftw3d.o

INCS       =-I$(MKLROOT)/include/fftw

LLIBS      = $(SCALAPACK) $(LAPACK) $(BLAS)


OBJECTS_O1 += fftw3d.o fftmpi.o fftmpiw.o
OBJECTS_O2 += fft3dlib.o

# For what used to be vasp.5.lib
CPP_LIB    = $(CPP)
FC_LIB     = $(FC)
CC_LIB     = icx
CFLAGS_LIB = -O
FFLAGS_LIB = -O1
FREE_LIB   = $(FREE)

OBJECTS_LIB= linpack_double.o getshmem.o

# For the parser library
CXX_PARS   = icpx -std=gnu++98

LIBS       += parser
LLIBS      += -Lparser -lparser -lstdc++

# Normally no need to change this
SRCDIR     = ../../src
BINDIR     = ../../bin

#================================================
# GPU Stuff

CPP_GPU    = -DCUDA_GPU -DRPROMU_CPROJ_OVERLAP -DUSE_PINNED_MEMORY -DCUFFT_MIN=28 -UscaLAPACK

OBJECTS_GPU = fftmpiw.o fftmpi_map.o fft3dlib.o fftw3d_gpu.o fftmpiw_gpu.o

CC         = icx
CXX        = icpx
CFLAGS     = -fPIC -DADD_ -Wall -openmp -DMAGMA_WITH_MKL -DMAGMA_SETAFFINITY -DGPUSHMEM=300 -DHAVE_CUBLAS

CUDA_ROOT  ?= /usr/local/cuda/
NVCC       := $(CUDA_ROOT)/bin/nvcc -ccbin=icc
CUDA_LIB   := -L$(CUDA_ROOT)/lib64 -lnvToolsExt -lcudart -lcuda -lcufft -lcublas

GENCODE_ARCH    := -gencode=arch=compute_30,code=\"sm_30,compute_30\" \
                   -gencode=arch=compute_35,code=\"sm_35,compute_35\" \
                   -gencode=arch=compute_60,code=\"sm_60,compute_60\"

MPI_INC    = $(I_MPI_ROOT)/include64/
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
6. 在`~/vasp`中设置POTCAR
```shell
$ cd ~
$ mkdir vasp
$ unzip mypps.zip
```
7. 在`~/.bashrc`中添加命令
```shell
export VASP_PP_PATH=$HOME/vasp/mypps
export ASE_VASP_VDW=$HOME/vasp/mypps
```
8. 使用`ipython`环境进行单线程测试
```python
from ase.build import bulk
from ase.calculators.vasp import Vasp

atoms = bulk('Au')
atoms.calc = Vasp(command='~/downloads/vasp.5.4.4/bin/vasp_std', directory='sr')
atoms.get_potential_energy()
```
9. 检查计算结果后清除文件夹
```shell
$ cat sr/vasp.out
$ rm -rf sr/
```
10. 编辑并行计算脚本`test.py`
```python
from ase.build import bulk
from ase.calculators.vasp import Vasp

atoms = bulk('Au')
atoms.calc = Vasp(command='mpirun -n 128 ~/downloads/vasp.5.4.4/bin/vasp_std', directory='mr')
atoms.get_potential_energy()
```
9. 编辑并行测试脚本`sub.sh`
```bash
#!/bin/bash
#SBATCH -J test
#SBATCH -o test.out
#SBATCH -e test.err

python test.py
```
10. 提交作业
```shell
$ sbatch -c 128 run.sh
```