---
title: "Python, Anaconda and Jupyter Setup"
published: 2026-09-30
publishedAt: 2026-09-30T08:10:00+08:00
description: "Goal: prepare a simple, reliable Python environment for the machine-learning practicals."
image: "./136908557.png"
tags: ["Python", "Jupyter"]
category: "Machine Learning"
draft: false
pinned: false
lang: en
---

> Goal: prepare a simple, reliable Python environment for the machine-learning practicals.

由于 Anaconda 臃肿且不便于卸载，故介绍一种使用 Python 原生 venv 的方法来搭建课程所需环境。[去看看](../practical-no-conda/)

## 1. What you need

- A Windows, macOS or Linux computer with internet access.
- Anaconda Distribution, which includes Python, conda, Jupyter and common data-science packages.
- JupyterLab or Jupyter Notebook for running the practical notebooks.
- Core libraries used in this module: NumPy, pandas, Matplotlib and scikit-learn.

## 2. Download and install Anaconda Distribution

Official download page: https://www.anaconda.com/download
1. Open the official Anaconda download page and select the installer for your operating system.
2. Run the installer. For most students, the default installation options are suitable.
3. After installation, open Anaconda Navigator or Anaconda Prompt/Terminal to confirm that Anaconda is available.

```mermaid
flowchart LR
    A["1 Download"] --> B["2 Install"]
    B --> C["3 Open Anaconda"]
    C --> D["4 Verify"]
```

## 3. Create a module environment

Creating a separate Conda environment optional but highly recommended. It keeps the packages used in this module organized and helps prevent conflicts with packages used in other projects.

Create the environment:

```bash
conda create --name ml_chc6089 python
```

Activate the environment:

```bash
conda activate ml_chc6089
```

To leave the environment later:

```bash
conda deactivate
```

## 4. Connect the Conda environment to Jupyter

Jupyter runs notebook code through a kernel. Register the module environment as a Jupyter kernel so that students can clearly select the correct Python environment.

Activate the module environment:

```bash
conda activate ml_chc6089
```

Install the kernel package:

```bash
conda install ipykernel
```

Register the environment as a Jupyter kernel:

```bash
python -m ipykernel install --user --name ml_chc6089 --display-name "Python (ML CHC6089)"
```

After opening Jupyter, select the kernel named "Python (ML CHC6089)".

## 5. Install/verify the required packages

Anaconda Distribution already includes many common packages. If anything is missing in your module environment, install the core packages with:

```bash
conda install numpy pandas matplotlib scikit-learn jupyterlab notebook
```

We will install additional libraries later only when they are needed for a specific topic.

## 6. Launch Jupyter

Option A — JupyterLab (recommended interface):

```bash
jupyter lab
```

Option B — Classic Jupyter Notebook:

```bash
jupyter notebook
```

Jupyter normally opens in your default web browser. Keep the terminal/Anaconda Prompt window open while Jupyter is running.

## 7. Verify your setup

Create a new Python notebook and run the following cell:

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

Check the "Python executable" path. It should contain `ml_chc6089`. If it does not, change the notebook kernel to "Python (ML CHC6089)".

## 8. Common problems

| Problem                                | What to try                                                                                                                                                    |
| -------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| "conda" is not recognised              | Open Anaconda Prompt/Anaconda Terminal<br>instead of a normal terminal, or restart the<br>computer after installation.                                         |
| Jupyter opens in the wrong environment | Choose Kernel → Change Kernel → <br>"Python (ML CHC6089)", <br>then run `import sys`;<br>`print(sys.executable)` <br>to confirm the path contains<br>`ml_chc6089`. |
| A package is missing                   | Activate `ml_chc6089` and install the missing<br>package with `conda install <package>` or <br>`pip install <package>`.                                        |
| Windows ARM/Snapdragon computer        | Anaconda Distribution support may differ by<br>architecture. Ask the instructor before <br>changing the setup.                                                     |


## 9. Before the Week 1 seminar

- Make sure Jupyter opens successfully.
- Download the file `chronic_kidney_disease.csv` provided for the seminar.
- Place the dataset in the same folder as your Week 1 notebook.
- Do not preprocess or modify the dataset yet. In Week 1 we will first learn how to understand it.

Source: [week1seminar.zip](https://vle.zycdut.net/sites/student.zy.cdut.edu.cn/files/attachments/week1seminar.zip)
