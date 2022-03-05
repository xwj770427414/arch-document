# arch

[![arch](https://bashtage.github.io/arch/doc/_static/images/color-logo-256.png)](https://github.com/bashtage/arch)

- 在学习arch的过程中发现一直缺乏有效**中文文档**，而R语言有很多相似的成熟的包，方便学习和研究使用，逐步对arch文档进行翻译并存档。
- 自回归条件异方差（ARCH）和其他工具金融计量经济学，用Python编写（使用Cython和/或Numba以提高效率）

| Metric                     |                                                                                                                                                                                                                                          |
| :------------------------- | :--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Latest Release**         | [![PyPI version](https://badge.fury.io/py/arch.svg)](https://badge.fury.io/py/arch)                                                                                                                                                      |
|                            | [![conda-forge version](https://anaconda.org/conda-forge/arch-py/badges/version.svg)](https://anaconda.org/conda-forge/arch-py)                                                                                          |
| **Continuous Integration** | [![Build Status](https://dev.azure.com/kevinksheppard0207/kevinksheppard/_apis/build/status/bashtage.arch?branchName=main)](https://dev.azure.com/kevinksheppard0207/kevinksheppard/_build/latest?definitionId=1&branchName=main)        |
|                            | [![Appveyor Build Status](https://ci.appveyor.com/api/projects/status/nmt02u7jwcgx7i2x?svg=true)](https://ci.appveyor.com/project/bashtage/arch/branch/main)                                                                             |
| **Coverage**               | [![codecov](https://codecov.io/gh/bashtage/arch/branch/main/graph/badge.svg)](https://codecov.io/gh/bashtage/arch)                                                                                                                       |
| **Code Quality**           | [![Code Quality: Python](https://img.shields.io/lgtm/grade/python/g/bashtage/arch.svg?logo=lgtm&logoWidth=18)](https://lgtm.com/projects/g/bashtage/arch/context:python)                                                                 |
|                            | [![Total Alerts](https://img.shields.io/lgtm/alerts/g/bashtage/arch.svg?logo=lgtm&logoWidth=18)](https://lgtm.com/projects/g/bashtage/arch/alerts)                                                                                       |
|                            | [![Codacy Badge](https://api.codacy.com/project/badge/Grade/93f6fd90209842bf97fd20fda8db70ef)](https://www.codacy.com/manual/bashtage/arch?utm_source=github.com&utm_medium=referral&utm_content=bashtage/arch&utm_campaign=Badge_Grade) |
|                            | [![codebeat badge](https://codebeat.co/badges/18a78c15-d74b-4820-b56d-72f7e4087532)](https://codebeat.co/projects/github-com-bashtage-arch-main)                                                                                         |
| **Citation**               | [![DOI](https://zenodo.org/badge/doi/10.5281/zenodo.593254.svg)](https://doi.org/10.5281/zenodo.593254)                                                                                                                                  |
| **Documentation**          | [![Documentation Status](https://readthedocs.org/projects/arch/badge/?version=latest)](https://arch.readthedocs.org/en/latest/)                                                                                                           |

## 模块目录

- [arch](#arch)
  - [模块目录](#模块目录)
    - [Python 3](#python-3)
  - [文档](#文档)
  - [关于ARCH的更多信息](#关于arch的更多信息)
  - [实例](#实例)
    - [波动率建模 Volatility Modeling](#波动率建模-volatility-modeling)
    - [单位根检验](#单位根检验)
    - [协整检验和分析 Cointegration Testing and Analysis](#协整检验和分析-cointegration-testing-and-analysis)
    - [Bootstrap](#bootstrap)
    - [多重对比程序 Multiple Comparison Procedures](#多重对比程序-multiple-comparison-procedures)
    - [长期协方差估计 Long-run Covariance Estimation](#长期协方差估计-long-run-covariance-estimation)
  - [依赖](#依赖)
    - [可选依赖](#可选依赖)
  - [安装](#安装)
    - [pip](#pip)
    - [Anaconda](#anaconda)
    - [Windows](#windows)

### Python 3

`arch`是仅支持Python 3。`Version 4.8`是支持Python 2.7的最终版本。

## 文档
Main branch的文档被托管在[my github pages](https://bashtage.github.io/arch/).

Released的文档被托管在[read the docs](https://arch.readthedocs.org/en/latest/).

## 关于ARCH的更多信息

关于ARCH和相关模型的更多信息，可在[Kevin Sheppard's](https://www.kevinsheppard.com)网站的注释和研究中获得。

## 实例

### 波动率建模 Volatility Modeling

- 均值模型 Mean models
  - Constant mean
  - Heterogeneous Autoregression (HAR)
  - Autoregression (AR)
  - Zero mean
  - Models with and without exogenous regressors
- 波动率模型 Volatility models
  - ARCH
  - GARCH
  - TARCH
  - EGARCH
  - EWMA/RiskMetrics
- 分布 Distributions
  - Normal
  - Student's T
  - Generalized Error Distribution

请参考[univariate volatility example notebook](https://nbviewer.ipython.org/github/bashtage/arch/blob/main/examples/univariate_volatility_modeling.ipynb)以获得更完整的概览。

```python
import datetime as dt
import pandas_datareader.data as web
st = dt.datetime(1990,1,1)
en = dt.datetime(2014,1,1)
data = web.get_data_yahoo('^FTSE', start=st, end=en)
returns = 100 * data['Adj Close'].pct_change().dropna()

from arch import arch_model
am = arch_model(returns)
res = am.fit()
```
### 单位根检验

- Augmented Dickey-Fuller
- Dickey-Fuller GLS
- Phillips-Perron
- KPSS
- Zivot-Andrews
- Variance Ratio tests

请参考[unit root testing example notebook](https://nbviewer.ipython.org/github/bashtage/arch/blob/main/examples/unitroot_examples.ipynb)中检验序列单位根。

### 协整检验和分析 Cointegration Testing and Analysis

- 检验 Test
  - Engle-Granger Test
  - Phillips-Ouliaris Test
- 协整向量估计 Cointegration Vector Estimation
  - Canonical Cointegrating Regression 
  - Dynamic OLS
  - Fully Modified OLS

请参考[cointegration testing example notebook](https://nbviewer.ipython.org/github/bashtage/arch/blob/main/examples/unitroot_cointegration_examples.ipynb)中序列的协整检验样例

### Bootstrap

- Bootstraps
  - IID Bootstrap
  - Stationary Bootstrap
  - Circular Block Bootstrap
  - Moving Block Bootstrap
- 方法 Methods
  - 置信区间构建 Confidence interval construction
  - 协方差估计 Covariance estimation
  - Apply method to estimate model across bootstraps
  - Generic Bootstrap iterator

请参考[bootstrap example notebook](https://nbviewer.ipython.org/github/bashtage/arch/blob/main/examples/bootstrap_examples.ipynb)中，关于夏普比率的bootstrapping样例和来自statsmodels的Probit模型的bootstrapping样例。

```python
# Import data
import datetime as dt
import pandas as pd
import numpy as np
import pandas_datareader.data as web
start = dt.datetime(1951,1,1)
end = dt.datetime(2014,1,1)
sp500 = web.get_data_yahoo('^GSPC', start=start, end=end)
start = sp500.index.min()
end = sp500.index.max()
monthly_dates = pd.date_range(start, end, freq='M')
monthly = sp500.reindex(monthly_dates, method='ffill')
returns = 100 * monthly['Adj Close'].pct_change().dropna()

# Function to compute parameters
def sharpe_ratio(x):
    mu, sigma = 12 * x.mean(), np.sqrt(12 * x.var())
    return np.array([mu, sigma, mu / sigma])

# Bootstrap confidence intervals
from arch.bootstrap import IIDBootstrap
bs = IIDBootstrap(returns)
ci = bs.conf_int(sharpe_ratio, 1000, method='percentile')
```

### 多重对比程序 Multiple Comparison Procedures

- Test of Superior Predictive Ability (SPA), also known as the Reality
  Check or Bootstrap Data Snooper
- Stepwise (StepM)
- Model Confidence Set (MCS)

请参考[multiple comparison example notebook](https://nbviewer.ipython.org/github/bashtage/arch/blob/main/examples/multiple-comparison_examples.ipynb)中多重对比程序的样例


### 长期协方差估计 Long-run Covariance Estimation

基于核的长期协方差估计方法包括Bartlett核，在计量经济学中被称为Newey-West。自动bandwidth选择可用于所有的协方差估计器的自动bandwidth选择。

```python
from arch.covariance.kernel import Bartlett
from arch.data import nasdaq
data = nasdaq.load()
returns = data[["Adj Close"]].pct_change().dropna()

cov_est = Bartlett(returns ** 2)
# Get the long-run covariance
cov_est.cov.long_run
```

## 依赖

这些依赖反映了测试环境，`arch`可能将与其旧版本一起工作。

- Python (3.7+)
- NumPy (1.17+)
- SciPy (1.3+)
- Pandas (1.0+)
- statsmodels (0.11+)
- matplotlib (3+), optional
- property-cached (1.6.4+), optional

### 可选依赖

- 如果有Numba (0.49+)**且**在安装时不构建二进制模块，其将被使用。为了确保不构建这些模块，你必须设置环境变量``ARCH_NO_BINARY=1``，并且不使用wheel进行安装。
  
```shell
export ARCH_NO_BINARY=1
pip install arch --no-binary arch
```

或者在Windows中使用Powershell

```powershell
$env:ARCH_NO_BINARY=1
pip install arch --no-binary arch
```

如果你已经在本地克隆了版本库，你可以在不构建二进制模块的情况下安装

```shell
python setup.py install --no-binary
```

或通过设置环境变量 ``ARCH_NO_BINARY=1``.

- 运行notebooks需要jupyter notebook。

## 安装
带有编译器的标准安装需要Cython。如果你没有安装编译器，`arch`仍可以安装。此时你会看到一个警告，但可以忽略它。如果你没有安装编译器，强烈建议使用`numba`。

### pip
Releases版本在PyPI上可以找到，并可以用`pip`安装。

```shell
pip install arch
```

```shell
export ARCH_NO_BINARY=1
pip install arch --no-binary arch
```
你也可以从GitHub上安装最新的版本

```bash
pip install git+https://github.com/bashtage/arch.git
```

设置环境变量`ARCH_NO_BINARY=1`可以用来禁用扩展程序的编译。

### Anaconda

`conda` 用户可以从conda-forge中安装,

```bash
conda install arch-py -c conda-forge
```

**注意** : conda-forge中的名称为`arch-py`.

### Windows

当使用Python 3.7或更高版本时，使用Visual Studio的社区版构建扩展很简单。当已安装`numba`时不需要构建，因为即时编译代码 (numba) 的运行速度和提前编译的扩展一样快。