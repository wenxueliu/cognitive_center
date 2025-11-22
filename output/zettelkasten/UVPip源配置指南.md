---
title: UVPip源配置指南
type: note
permalink: zettelkasten/uv-pip-源配置指南
---

# UV Pip源配置指南

UV 是一个快速的 Python 包安装器，配置国内镜像源可以显著提升下载速度。

## 永久生效

```bash
# 推荐使用清华源
echo 'export UV_DEFAULT_INDEX="pypi.tuna.tsinghua.edu.cn/simple"' >> ~/.bashrc

# 或者用阿里源
echo 'export UV_DEFAULT_INDEX="mirrors.aliyun.com/pypi/simple"' >> ~/.bashrc

# 让配置立即生效
source ~/.bashrc
```

## 临时使用

如果不希望永久修改环境变量，可以临时使用镜像源：

```bash
# 临时使用清华源安装包
UV_DEFAULT_INDEX="pypi.tuna.tsinghua.edu.cn/simple" uv install package-name

# 临时使用阿里源安装包  
UV_DEFAULT_INDEX="mirrors.aliyun.com/pypi/simple" uv install package-name
```

## 验证配置

```bash
# 检查环境变量
env | grep UV_DEFAULT_INDEX

# 测试下载速度
uv install numpy pandas scipy
```