---
layout: default
---

### oneMKL & HPC Toolkit

#### 操作步骤
1. 下载[Intel® oneAPI Math Kernel Library](<https://www.intel.com/content/www/us/en/developer/articles/tool/oneapi-standalone-components.html#onemkl>)安装包。找到Intel oneAPI Math Kernel Library for Linux，复制链接地址，运行
```shell
$ wget https://registrationcenter-download.intel.com/akdlm/irc_nas/18483/l_onemkl_p_2022.0.2.136_offline.sh
```
2. 下载[Intel® oneAPI HPC Toolkit](<https://www.intel.com/content/www/us/en/developer/tools/oneapi/hpc-toolkit-download.html>)安装包（Linux -> Online & Offline (recommended) -> Offline）。在Command Line Download找到
```shell
$ wget https://registrationcenter-download.intel.com/akdlm/irc_nas/18479/l_HPCKit_p_2022.1.2.117_offline.sh
```
运行该命令。
3. 安装oneMKL，即运行
```shell
$ bash l_onemkl_p_2022.0.2.136_offline.sh
```
4. 安装HPC Toolkit，即运行
```shell
$ bash l_HPCKit_p_2022.1.2.117_offline.sh
```
5. 在`~/.bashrc`中添加命令
```shell
. ~/intel/oneapi/setvars.sh
```

#### 参考链接
* [Linux下安装Intel oneAPI](<https://mp.weixin.qq.com/s/7pQETkrDO1C83vQjKQqI4w>)

[[Back]](../tools.md)
