# Conda

[TOC]

## 1. Conda与python版本：

[anaconda download link for all versions](https://repo.continuum.io/archive/)

[python版本匹配的anaconda查询，old package lists](https://docs.anaconda.com/anaconda/packages/oldpkglists/)



## 2. Conda下载源

### 2.1 添加源

1. windows-cmd

   添加清华源

   ```shell
   conda config --add channels https://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/free/
   conda config --add channels https://mirrors.tuna.tsinghua.edu.cn/anaconda/cloud/conda-forgeconda 
   conda config --add channels https://mirrors.tuna.tsinghua.edu.cn/anaconda/cloud/msys2/
   # 设置搜索时显示通道地址
   conda config --set show_channel_urls yes
   ```
   
   添加中科大源
   ```shell
   conda config --add channels https://mirrors.ustc.edu.cn/anaconda/pkgs/main/
   conda config --add channels https://mirrors.ustc.edu.cn/anaconda/pkgs/free/
   conda config --add channels https://mirrors.ustc.edu.cn/anaconda/cloud/conda-forge/
   conda config --add channels https://mirrors.ustc.edu.cn/anaconda/cloud/msys2/
   conda config --add channels https://mirrors.ustc.edu.cn/anaconda/cloud/bioconda/
   conda config --add channels https://mirrors.ustc.edu.cn/anaconda/cloud/menpo/
   conda config --set show_channel_urls yes
   ```

​       生成的配置文件`.condarc`位于`C:\Users\username`

2. Linux-terminal
   配置文件同上，编辑文件`vim ~/.condarc`，内容形式如下

   ```
   ssl_verify: true
   show_channel_urls: true
   channels:
     - https://mirrors.tuna.tsinghua.edu.cn/anaconda/cloud/conda-forge
     - https://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/free/
     - https://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/main/
     - https://mirrors.tuna.tsinghua.edu.cn/anaconda/cloud/conda-forge/
     - https://mirrors.tuna.tsinghua.edu.cn/anaconda/cloud//pytorch/
     - defaults
   ```

   


### 2.2 还原默认源

- 直接删除`.condarc`中的`channels`

- 或者`conda config --remove-key channels`

  

## 3. Pip下载源

### 3.1 更换源

- windows

  `C:\Users\username\pip`文件夹，新建pip.init文件

- Linux

  ```
  mkdir ~/.pip
  cd ~/.pip
  vim pip.conf
  ```

文件填充内容：

```ini
[global]
index-url = https://mirrors.aliyun.com/pypi/simple/
[install]
trusted-host=mirrors.aliyun.com
```



## 4. 离线安装包

### 4.1 Pip离线安装包

[Python Extension Packages for Windows - Christoph Gohlke](http://www.lfd.uci.edu/~gohlke/pythonlibs/#pil)

[PyPI - the Python Package Index : Python Package Index](https://pypi.python.org/pypi)

也可copy install过程中显示的download网址

- tar.gz 后缀的文件
  - 解压文件
  - 通过cmd/terminal，进入解压后的根目录
  - 通过python命令安装：<font color='red'>`python setup.py install`</font>，根据安装提示信息，如果有前置依赖，则退出，先安装前置依赖
- whl文件（本质是一个 .zip 包）
  - <font color='red'>`pip install D:\opencv_python-4.1.2.30-cp37-cp37m-win_amd64.whl `</font>

### 4.2 Conda离线安装包

下载tar.bz2包，然后<font color='red'>`conda install --use-local D:\Anaconda3\pkgs\pytorch-1.3.1-py3.6_cuda101_cudnn7_0.tar.bz2`</font>



## 5. Conda虚拟环境管理

[参考](https://www.cnblogs.com/moodlxs/p/11509692.html)

创建虚拟环境的流程：

```shell
# 1、备份
conda create -n backup --clone base

# 2、创建新环境
# 基于备份创建
conda create -n tf2.0 --clone backup
# 创建简洁环境
conda create -n tf2.0 python=3.7

# 3、激活环境
conda activate tf2

# 4、在虚拟环境中安装包，虚拟环境位于Anaconda3/envs中
conda install xxx
pip install xxx

# 5、退出
conda deactivate

# 6、删除
conda remove -n tf2.0 --all
```

其他管理：

- 升级conda：`conda update conda`
- 升级anaconda(需先升级conda)：`conda update anaconda`
- 更新指定包：`conda update xxx`
- 更新所有包：`conda update --all`
- 查看已安装的包：`conda list`
- 删除指定包 `conda remove xxx`



## 6. 环境导入导出

### 6.1 conda导出导入已有环境

导出环境到environment.yaml

```
conda env export > environment.yaml
```

导入环境

```
conda env create -f environment.yaml 
```



### 6.2 pip导出导入已有环境

pip导出安装的库到requirements.txt

```
pip freeze > requirements.txt
```

pip导入requirements.txt中列出的库到系统

```
pip install -r requirements.txt
```



**<font color='red'>Tips</font>**

- 在使用conda虚拟环境时，最好先备份初始的安装环境。
- 后面再新建其他环境时，如需要纯净的环境，基于备份环境clone
- conda移植过来的环境只是安装了原来环境里用conda install等命令直接安装的包，用pip安装的包没有移植过来，需要重新安装。（针对从一个电脑转移到另一个电脑的情况）