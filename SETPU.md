## 1. 准备运行环境
### 1.1 安装 Anaconda
```bash
wget https://repo.anaconda.com/archive/Anaconda3-2023.03-1-Linux-x86_64.sh  
sudo chmod 777 https://repo.anaconda.com/archive/Anaconda3-2023.03-1-Linux-x86_64.sh  
sudo ./Anaconda3-2023.03-1-Linux-x86_64.sh  
```
### 1.2 创建虚拟环境
创建虚拟环境并指定python的版本号为3.8  
```
conda create -n qlora pip python=3.8
```
激活虚拟环境
```
conda activate qlora
```
### 1.3 安装 Guanaco 依赖库
在qlora项目下，执行：
```
pip install -r requirements.txt
```
## 3. 准备 训练数据
## 4. 修改训练参数
## 5. 执行训练
