# 安装cuda10.1-cudnn-pytorch

## Windows平台

1. 安装vs2015-update3（已安装了vs2013或更高版本直接安装即可）
2. [cuda 10.1](https://developer.nvidia.com/cuda-toolkit-archive-->http://developer.download.nvidia.com/compute/cuda/10.1/Prod/local_installers/cuda_10.1.243_426.00_win10.exe)，自定义安装-->自选目录，完成安装，vs插件集成

![img](assets/Image(1).png)

3. 环境变量设置

![img](assets/Image(2).png)

验证安装成功：cmd输入

```shell
nvcc -V
nvcc: NVIDIA (R) Cuda compiler driverCopyright (c) 2005-2019 NVIDIA CorporationBuilt on Sun_Jul_28_19:12:52_Pacific_Daylight_Time_2019Cuda compilation tools, release 10.1, V10.1.243
```

4. 与cuda10.1匹配的[cuDNN](https://developer.nvidia.com/rdp/cudnn-download)

   ![img](assets/Image(3).png)

   解压后的目录对应放入cuda中，bin->CUDA_BIN，include->CUDA_include，lib->CUDA_lib

5. 安装[anaconda](https://repo.continuum.io/archive/Anaconda3-5.2.0-Windows-x86_64.exe)

6. git: Git-2.21.0-64-bit

7. 安装[pytorch-gpu](https://pytorch.org/get-started/locally)
   ![img](assets/Image(4).png)

   在Anaconda Prompt中运行，结果pytorch下载过于缓慢，直接抽取其中的[url下载链接](https://conda.anaconda.org/pytorch/win-64)下载，然后**本地安装**
  ```shell
  conda install --use-local D:\Anaconda3\pkgs\pytorch-1.3.1-py3.6_cuda101_cudnn7_0.tar.bz2
  ```

  ![img](assets/Image(5).png)

  还需要安装其他的组件：
  ```
  conda install torchvision cudatoolkit=10.1
  ```

  验证安装：
  ```python
  from __future__ import print_function
  import torch
  x = torch.rand(5, 3)
  print(x)
  > tensor([[0.3380, 0.3845, 0.3217],    [0.8337, 0.9050, 0.2650],    [0.2979, 0.7141, 0.9069],    [0.1449, 0.1132, 0.1375],    [0.4675, 0.3947, 0.1426]])
  ```

  验证cuda：
  ```python
  import torch
  torch.cuda.is_available()
  > True 
  ```

8. opencv等

```
conda install -c conda-forge opencv
```
```python
import cv2 # 无报错->成功
```

---

**Tensorflow1.14**与cuda10.0匹配

cuda10.0的安装相同，可以和10.1共存，只是CUDA_PATH不一样![img](assets/Image(6).png)

安装10.0和10.1两个版本，安装时tf时，先修改CUDA_PATH为10.0的地址

**keras:**

```shell
conda activate tf1.14
conda install tensorflow-gpu=1.14.0
# 这里python3.7环境conda中没有源
pip install keras==2.1.3
python
```

```python
import keras
import tensorflow
print(keras.__version__)
print(tensorflow.__version__)
```

