# Jupyter安装
jupyter 及其插件的安装
```bash
conda create -n jupyter python=3.8                            // 创建环境
conda activate jupyter                                        // 激活新环境
conda install notebook                                        // 安装jupyter
conda install -c conda-forge jupyter_contrib_nbextensions     // 安装插件，失败用pip
jupyter notebook --notebook-dir=F:\home                       // 启动jupyter
```
# 给Jupyter创建新环境
```bash 
conda create -n newenv python=3.8                                                               // 创建新环境
conda activate newenv                                                                           // 进入新环境
conda install ipykernel                                                                         // 安装内核
python -m ipykernel install --user --name=newenv --display-name="Python (newenv)"  
python -m ipykernel install --name=paddle --display-name "Paddle" --sys-prefix                  // 这个才是全局的
```

# 查看Jupyter环境
```bash 
jupyter kernelspec list                                        // 查看所有内核
jupyter kernelspec uninstall kernel_name                       // 卸载内核
```

# jupyterhub 安装部署
jupyterhub 是单独的一个软件，负责启动多个jupyter，给多个用户使用的，只能部署在linux系统上，因此不要妄想部署在windows上，且不要妄想jupyterhub和jupyter分开部署，因为分开部署jupyterhub就无法控制jupyter。
> 注意：启动jupyterhub要在配置文件目录下配置文件才能有用

生成配置文件的脚本如下：

```bash 
jupyterhub --generate-config
```

经过多次摸索，生成的jupyterhub配置如下：
```python 
# 全局配置，默认就带
c = get_config()

# linux下还是交给PAM做用户管理最方便，直接可以映射到本地存储，还能简单的防止丢失代码
c.JupyterHub.authenticator_class = 'jupyterhub.auth.PAMAuthenticator'
# 一般python都需要结合conda使用，有许多个运行python 的环境，jupyterhub结合conda需要这么配置
c.KernelSpecManager.kernel_spec_class = "nb_conda_kernels.CondaKernelSpec"
# 允许那些用户登录到本软件
c.Authenticator.allowed_users = {'yanguoyu', 'liran'}
# 那个是管理员，目前已知管理员可以在线创建用户
c.Authenticator.admin_users = {'yanguoyu'}
# 在启动Spawner前执行的命令，目的就是找到conda和jupyterhub的conda环境
c.Spawner.cmd = ['/opt/miniconda/bin/conda', 'run', '-n', 'jupyterhub', 'jupyter-labhub']

```

# 额外注意
1. 要在具有cuda和cudnn的镜像中部署，而不是直接在jupyterhub镜像中部署，不然无法使用paddle和pytorch
2. 要结合conda使用的化，也很难，一言难尽。
3. 要将/home文件做映射，以实现用户创建代码的永久保存
4. 最好把config文件单独映射进去，从而可以随意调整配置文件，来探索jupyterhub，因为部署有很多坑要踩，快速配置很重要
```bash 
docker run --gpus all -it -d \
    --name jupyterhub \
    -p 8000:8000 \
    -v F:\jupyterhub_data\home:/home \
    -v F:\jupyterhub_data\config:/srv/jupyterhub \
    nvidia/cuda:11.8.0-cudnn8-runtime-ubuntu20.04 /bin/bash
```
