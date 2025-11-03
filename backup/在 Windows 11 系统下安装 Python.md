==在 Windows 11 系统下安装 Python（“蟒蛇” 通常指 Anaconda 或 Miniconda，这里以 Anaconda 为例）以及 PyTorch（包含 CUDA 和 cuDNN）的详细步骤==
**一、安装 Anaconda（Python 发行版）**
1. 下载 Anaconda
访问官网：[Anaconda 下载页](https://www.anaconda.com/download)
选择 Windows 版本（64 位，根据系统选择，通常是 64-Bit Graphical Installer）
建议下载 Python 3.9 及以上版本（兼容性更好）
2. 安装 Anaconda
双击安装包，点击 “Next” 直到出现安装选项：
勾选 “Add Anaconda3 to my PATH environment variable”（关键！否则需手动配置环境变量）
其他选项默认（安装路径建议默认，或自定义到非系统盘，路径不要有中文 / 空格）
点击 “Install” 完成安装，最后取消勾选 “Learn more about Anaconda Cloud” 并关闭。
3. 验证安装
按下 Win + R，输入 cmd 打开命令提示符
输入 conda --version，若显示版本号（如 conda 23.11.0），则安装成功
---
**二、安装 CUDA（NVIDIA 显卡加速工具）**
1. 检查显卡是否支持 CUDA
按下 Win + R，输入 dxdiag，切换到 “显示” 选项卡，查看显卡型号（需为 NVIDIA 显卡，如 RTX 3060、GTX 1650 等）
访问 NVIDIA 显卡支持列表，确认显卡属于 “CUDA-Enabled GPUs”
2. 下载并安装 CUDA Toolkit
打开 [PyTorch 官网](https://pytorch.org)，查看当前推荐的 CUDA 版本（例如 12.1，需与后续 PyTorch 版本匹配）
访问 [CUDA 下载页](https://developer.nvidia.com/cuda-toolkit-archive)，选择对应版本（如 12.1）：
操作系统：Windows
架构：x86_64
安装方式：exe (local)
版本：默认最新子版本
下载后双击安装：
选择 “自定义安装”（推荐），取消勾选不需要的组件（如 Visual Studio Integration，若已安装 VS 可保留）
安装路径默认即可（通常为 C:\Program Files\NVIDIA GPU Computing Toolkit\CUDA\v12.1）
安装完成后，关闭窗口。
3. 验证 CUDA 安装
打开命令提示符，输入 nvcc --version，若显示版本信息（如 Cuda compilation tools, release 12.1），则安装成功
---
**三、安装 cuDNN（CUDA 深度神经网络库）**
1. 下载 cuDNN
访问 [cuDNN 下载页](https://developer.nvidia.com/cudnn-downloads)，需注册 NVIDIA 账号并登录
选择与已安装 CUDA 版本匹配的 cuDNN（例如 CUDA 12.1 对应 cuDNN v8.9.x for CUDA 12.x）
下载 “cuDNN Library for Windows (x86_64)” 的 zip 压缩包
2. 安装 cuDNN
解压下载的 zip 包，得到 cuda 文件夹，内含 bin、include、lib 三个子文件夹
将这三个文件夹复制到 CUDA 安装目录（例如 C:\Program Files\NVIDIA GPU Computing Toolkit\CUDA\v12.1），覆盖同名文件夹（确认权限允许）
3. 配置 cuDNN 环境变量
右键 “此电脑” → “属性” → “高级系统设置” → “环境变量”
在 “系统变量” 中找到 Path，点击 “编辑”，添加 cuDNN 的 bin 路径（例如 C:\Program Files\NVIDIA GPU Computing Toolkit\CUDA\v12.1\bin）
点击 “确定” 保存，关闭所有窗口。
---
**四、安装 PyTorch（带 GPU 支持）**
1. 创建虚拟环境（可选但推荐）
打开命令提示符，输入以下命令创建一个独立环境（避免依赖冲突）：
*bash
conda create -n pytorch-gpu python=3.10  # 环境名 pytorch-gpu，Python 版本 3.10
conda activate pytorch-gpu  # 激活环境（命令行前会显示 (pytorch-gpu)）*
2. 安装 PyTorch
打开 [PyTorch 官网](https://pytorch.org)，根据配置选择安装命令：
PyTorch Build：Stable (2.1.0 或最新稳定版)
Your OS：Windows
Package：Conda
Language：Python
Compute Platform：CUDA 12.1（选择与之前安装的 CUDA 版本一致）
复制生成的命令（例如）：
*bash
conda install pytorch torchvision torchaudio pytorch-cuda=12.1 -c pytorch -c nvidia*
在激活的虚拟环境中粘贴并运行，等待安装完成（需联网，可能耗时较长）。
---
**五、验证 PyTorch GPU 支持**
在命令提示符中（确保已激活 pytorch-gpu 环境），输入 python 进入 Python 交互模式
输入以下代码：
*python
import torch
print(torch.__version__)  # 查看 PyTorch 版本
print(torch.cuda.is_available())  # 检查 GPU 是否可用，返回 True 则成功
print(torch.cuda.get_device_name(0))  # 显示显卡型号*
若输出 True 且显示显卡型号，则 PyTorch 已成功关联 CUDA 和 cuDNN。
==常见问题解决==
若 nvcc --version 失败：检查 CUDA 环境变量是否配置，或重新安装 CUDA 并勾选 “添加到 PATH”
若 torch.cuda.is_available() 返回 False：确认 CUDA、cuDNN 版本与 PyTorch 匹配，或显卡不支持 CUDA（需改用 CPU 版本 PyTorch）
安装速度慢：可添加国内镜像源（如清华镜像），命令：
*bash
conda config --add channels https://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/free/
conda config --add channels https://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/main/
conda config --add channels https://mirrors.tuna.tsinghua.edu.cn/anaconda/cloud/pytorch/*
按以上步骤操作，即可在 Windows 11 下完成 Python（Anaconda）、PyTorch 及 GPU 加速环境的安装。
