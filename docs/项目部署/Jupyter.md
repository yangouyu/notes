# Jupyter安装
jupyter 及其插件的安装
```bash
conda create -n jupyter python=3.8                            // 创建环境
conda activate jupyter                                        // 激活新环境
conda install notebook                                        // 安装jupyter
conda install -c conda-forge jupyter_contrib_nbextensions     // 安装插件，失败用pip
jupyter notebook --notebook-dir=/path/to/your/directory       // 启动jupyter
```
# 给Jupyter创建新环境
```bash 
conda create -n newenv python=3.8                                                               // 创建新环境
conda activate newenv                                                                           // 进入新环境
conda install ipykernel                                                                         // 安装内核
python -m ipykernel install --user --name=newenv --display-name="Python (newenv)"  
```

# 查看Jupyter环境
```bash 
jupyter kernelspec list                                        // 查看所有内核
jupyter kernelspec uninstall kernel_name                       // 卸载内核
```