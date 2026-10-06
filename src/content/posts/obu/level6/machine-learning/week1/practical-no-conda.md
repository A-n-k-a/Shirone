---
title: "Python and Jupyter Setup (without Anaconda)"
published: 2026-09-30
publishedAt: 2026-09-30T09:00:00+08:00
description: "由于 Anaconda 臃肿且不便于卸载，故介绍一种使用 Python 原生 venv 的方法来搭建课程所需环境。"
image: "./149071758.jpg"
tags: ["Python", "Jupyter"]
category: "Machine Learning"
draft: false
pinned: false
lang: zh_CN
---

由于 Anaconda 臃肿且不便于卸载，故介绍一种使用 Python 原生 venv 的方法来搭建课程所需环境。如果你希望查看老师的版本，请点击[这里](../practical/)。此处以 Ubuntu Server 26.04 LTS 为例。

:::steps{title=""}

1. 安装 venv

    若发行版或系统自带 venv 可跳过此步。

    ```bash
    sudo apt install python3-venv
    ```

2. 为这门课创建独立环境

    ```bash
    mkdir CHC6089
    cd CHC6089
    python3 -m venv ml_chc6089
    source ml_chc6089/bin/activate
    ```

    激活后，终端前面通常会出现：

    ```bash
    (ml_chc6089)
    ```

3. 安装课程需要的包

    ```bash
    pip install numpy pandas matplotlib scikit-learn jupyterlab notebook ipykernel
    ```

4. 注册 Jupyter kernel

    讲义本身也要求把课程环境注册成 `Python (ML CHC6089)`。

    ```bash
    python -m ipykernel install \
    --user \
    --name ml_chc6089 \
    --display-name "Python (ML CHC6089)"
    ```

    预期输出类似于：

    ```bash
    Installed kernelspec ml_chc6089 in /home/anka/.local/share/jupyter/kernels/ml_chc6089
    ```

5. 验证安装

    ```bash
    python -c "import numpy, pandas, sklearn, matplotlib; print('OK')"
    ```

6. 启动服务

    ```bash
    jupyter lab --no-browser --ip=127.0.0.1 --port=8888
    ```

    若希望从非本地IP访问，可将监听IP设为 `0.0.0.0` ；监听端口默认为 `8888` ，可根据情况修改。启动后可在终端中看到访问地址（如： `http://localhost:8888/lab?token=xxxxxxxxxxxx` ），用浏览器打开即可。

:::

数据集方面，讲义要求把 `chronic_kidney_disease.csv` 和 Week 1 notebook 放在同一个目录，而且暂时不要修改或预处理它。

例如：

```file-tree title="示例文件结构"
CHC6089
├── ml_chc6089/
│   ├── bin/
│   │   ├── activate
│   │   ├── activate.csh
│   │   ├── activate.fish
│   │   ├── Activate.ps1
│   │   ├── cffi-gen-src
│   │   ├── debugpy
│   │   ├── debugpy-adapter
│   │   ├── f2py
│   │   ├── fonttools
│   │   ├── httpx
│   │   ├── idna
│   │   ├── ipython
│   │   ├── ipython3
│   │   ├── jlpm
│   │   ├── jsonpointer
│   │   ├── jsonschema
│   │   ├── jupyter
│   │   ├── jupyter-builder
│   │   ├── jupyter-dejavu
│   │   ├── jupyter-events
│   │   ├── jupyter-execute
│   │   ├── jupyter-kernel
│   │   ├── jupyter-kernelspec
│   │   ├── jupyter-lab
│   │   ├── jupyter-labextension
│   │   ├── jupyter-labhub
│   │   ├── jupyter-migrate
│   │   ├── jupyter-nbconvert
│   │   ├── jupyter-notebook
│   │   ├── jupyter-run
│   │   ├── jupyter-server
│   │   ├── jupyter-troubleshoot
│   │   ├── jupyter-trust
│   │   ├── mistune
│   │   ├── normalizer
│   │   ├── numpy-config
│   │   ├── pip
│   │   ├── pip3
│   │   ├── pip3.14
│   │   ├── pybabel
│   │   ├── pyftmerge
│   │   ├── pyftsubset
│   │   ├── pygmentize
│   │   ├── pyjson5
│   │   ├── python -> python3
│   │   ├── python3 -> /usr/bin/python3
│   │   ├── python3.14 -> python3
│   │   ├── send2trash
│   │   ├── ttx
│   │   ├── wsdump
│   │   └── 𝜋thon -> python3
│   ├── etc
│   │   └── jupyter/
│   ├── include/
│   ├── lib
│   │   └── python3.14/
│   ├── lib64 -> lib/
│   ├── pyvenv.cfg
│   └── share
│       ├── applications/
│       ├── icons/
│       ├── jupyter/
│       └── man/
└── Week1
    ├── week1.ipynb
    └── chronic_kidney_disease.csv
```

讲义最后还要求验证当前 Python 环境。需要在 notebook 中运行：

```python
import sys
import numpy as np
import pandas as pd
import sklearn
import matplotlib

print("Python executable:", sys.executable)
print("Python:", sys.version.split()[0])
print("NumPy:", np.__version__)
print("pandas:", pd.__version__)
print("scikit-learn:", sklearn.__version__)
print("Matplotlib:", matplotlib.__version__)
```

注：PyPI 已经不再支持 XML-RPC 的 `search` 方法，JupyterLab 4.6.4 的扩展管理器无法正常使用，需要手动安装扩展。例如安装中文语言包：

```bash
pip install jupyterlab-language-pack-zh-CN
```

安装完成后重启 JupyterLab。

更多扩展可在 https://pypi.org 通过搜索 `jupyterlab` 找到。
