# Jupyter notebook

## 1. 本地配置

- 打开 cmd 输入命令` jupyter notebook --generate-config`可以看到生成文件的路径，这个就是生成的配置文件jupyter_notebook_config.py 

- 打开后找到这个地方删除前面的’#‘ 然后填写自己的路径，保存，启动 jupyter notebook（区分路径字符/ 和\）

  <font color='blue'>`c.NotebooApp.notebook_dir = 'F:\note'`</font>

- windows快捷方式的属性修改，要利用上面的py配置，去掉后面的%USERFILE%
  ![img](assets/Image(7).png)



## 2. nbex插件安装

**jupyter_contrib_nbextension**包括content、自动补全提示等

[Github项目网址](https://github.com/ipython-contrib/jupyter_contrib_nbextensions/tree/master/docs)

[效果展示和参考](https://www.cnblogs.com/likedata/p/11225252.html)





## 3. Jupyter notebook 选用conda的虚拟环境kernel

[nb_conda_kernels](https://github.com/Anaconda-Platform/nb_conda_kernels)用于在notebook选择本机不同的虚拟环境kernel
建议：

- 在base环境安装

- 启动

  ```shell
  conda activate base
  jupyter notebook
  ```

  

