---
layout: post
title: Python注释说明
categories: [Python, usage]
tags: [python, python-usage, python-docstring]
author:
  name: zhaozl1123
  link: https://github.com/zhaozl1123
---

以 <kbd>commonMethods_zhaozl</kbd> 为例

### 1.库的结构
```bash
├── commonMethods_zhaozl
│   ├── __init__.py
│   ├── __version__.py
│   ├── core.py
│   └── toolbox
│       ├── __init__.py
│       ├── Method_bounceAnalyzer.py
│       └── Method_bpNetworkRun.py
│       └── ...
```
- 对package的注释在库根部的__init__.py中进行
- 对Core的注释在库根部的__init__.py中进行、在core.py的头部进行
- 对Toolbox的注释在库根部的__init__.py中进行、在Toolbox根部的__init__.py中进行
- 类的注释在类所处的.py文件头部，对本.py文件中的类、类的方法、类的函数、普通函数进行说明类的方法、类的函数在其定义后进行说明
- 函数注释在其定义后进行说明


### 2.库 > \__init__\.py
{% highlight python %}
"""
Core
----------
* code2Name: 通过输入词典对传入code进行转译同时使用_verbose控制是否显示对字典的预检验
* printWithColor: 打印具有颜色和特定格式的字符串

###################################################
对Core内的函数进行说明，此内容可以完全复制core.py头部的内容
###################################################

Toolbox
----------
* mysqlOperator: mysql数据库操作， 包括创建table、添加列、新增数据、更新数据、查询数据
* trendAnalyzer:
    ** trendAnalyzer: 使用三阶滑动平均与一阶导对输入数据的快速/缓慢的上升/下降状态进行判断

    ** trendPredict: 通过不断输入一时间序列的数值，顺序地对所定义窗口1内的数值进行三阶滑动平均处理，并计算所定义窗口2内的时序数据一阶导，通过对所定义窗口3内一阶导数据均值进行判断，以确定原始数据的上升/下降情况，包括：是否处理上升/下降状态，是否处于快速/慢速变化状态

###################################################
#####对Toolbox内的库文件及其中的类与方法或函数等进行说明，此内容可以完全复制每个库文件头部的内容
###################################################
"""

from .core import *

###################################################
##### 引入Core的内容
###################################################
{% endhighlight %}

### 3.库 > core.py
{% highlight python %}
"""
Functions
----------
* code2Name: 通过输入词典对传入code进行转译同时使用_verbose控制是否显示对字典的预检验

###################################################
对Core内的函数进行说明，此内容与Package > __init__.py的相应内容完全一致
###################################################

Classes
----------
* code2Name: 通过输入词典对传入code进行转译同时使用_verbose控制是否显示对字典的预检验

###################################################
对Core内的函数进行说明，此内容与Package > __init__.py的相应内容完全一致
###################################################

Example
----------
>>> from commonMethods_zhaozl import code2Name, printWithColor

###################################################
如何引入Core内容的示例
###################################################
"""
{% endhighlight %}

### 4.库 > toolbox > \__init__\.py
{% highlight python %}
"""
Classes
----------
* timeTrans: 通过输入list(int)或者int形式的时间戳unixTimestamp，与形如'%Y/%m/%d %H:%M:%S'的formation，对时间戳进行计算并输出string

* trendAnalyzer:

    ** trendAnalyzer: 使用三阶滑动平均与一阶导对输入数据的快速/缓慢的上升/下降状态进行判断

    ** trendPredict: 通过不断输入一时间序列的数值，顺序地对所定义窗口1内的数值进行三阶滑动平均处理，并计算所定义窗口2内的时序数据一阶导，通过对所定义窗口3内一阶导数据均值进行判断，以确定原始数据的上升/下降情况，包括：是否处理上升/下降状态，是否处于快速/慢速变化状态

###################################################
对toolbox内的函数进行说明，此内容与Package > toolbox > Methods_XXX.py头部的相应内容完全一致
###################################################

from . import *

###################################################
引入toolbox中的所有内容
###################################################
"""
{% endhighlight %}

### 5.库 > toolbox > Methods_XXX.py
{% highlight python %}
"""
包括bounceAnalyzer

###################################################
对Methods_XXX内的类、函数进行说明
###################################################

Classes
----------
bounceAnalyzer: 包括一种方法
    * updateAndDetermine: 对新传入的数据进行缓存记录，通过平均值计算等方法对跳变状态与持续跳变状态进行判断
        -- *逻辑描述见方法说明*

###################################################
对toolbox内的函数进行说明，此内容与Package > toolbox > __init__.py头部的相应内容完全一致
###################################################

Example
----------
>>> from commonMethods_zhaozl.toolbox.Method_bounceAnalyzer import bounceAnalyzer

"""
{% endhighlight %}

### 6.包的注释
包：作为库的组成部分，其中定义了一个或多个类、函数或变量。库 > 包 > 类/函数/变量
{% highlight python %}
"""
包括bounceAnalyzer

Classes
----------
bounceAnalyzer: 包括一种方法
    * updateAndDetermine: 对新传入的数据进行缓存记录，通过平均值计算等方法对跳变状态与持续跳变状态进行判断
        -- *逻辑描述见方法说明*

Example
----------
>>> from commonMethods_zhaozl.toolbox.Method_bounceAnalyzer import bounceAnalyzer

"""
{% endhighlight %}





### 7.类的注释
{% highlight python %}
"""
包括一种方法

* updateAndDetermine: 对新传入的数据进行缓存记录，通过平均值计算等方法对跳变状态与持续跳变状态进行判断
    -- *逻辑描述见方法说明*

[1] 参数
----------
sampleRecorderSize:
    int, 对象所接收的传入数据的记录尺寸, optional, default 10
determineThreshold:
    float, 新传入数据与本期数据进入前窗口（sampleRecorderSize）内数据均值的差值的报警限, optional, default 0.01
bounceStatusRecorderSize:
    int, 最近是否发生跳变的状态记录的尺寸, optional, default 50
keepBounceDetermineSize:
    int, 最近是否发生持续跳变的状态记录的尺寸,不可大于bounceStatusRecorderSize, :math:`this \\le\\ bounceStatusRecorderSize`, optional, default bounceStatusRecorderSize
keepBounceDetermineThreshold:
    float, 当监测到窗口（keepBounceDetermineSize）内发生了跳变的情况的百分比, optional, default 0.4, 触发条件是：
        :math:`窗口内跳变发生次数 \\ge\\ 窗口内发生了跳变的情况的百分比 \\times\\ 最近是否发生跳变的状态记录的尺寸`

[2] 方法
----------
updateAndDetermine:
    对新传入的数据进行缓存记录，通过平均值计算等方法对跳变状态与持续跳变状态进行判断

[3] 返回
-------
sampleRecorder:
    list, 对象所接收的传入数据的记录
average_lastTime:
    float, 本期数据进入前窗口（sampleRecorderSize）内数据的均值
average_thisTime:
    float, 本期数据进入后窗口（sampleRecorderSize）内数据的均值
bounceStatus:
    0/1, 当期是否发生了数据跳变的判断结论, 1：发生 0：未发生
bounceStatusRecorder:
    list[0/1], 最近窗口（bounceStatusRecorderSize）内是否发生跳变的状态记录
keepBounceStatus:
    0/1, 最近是否发生持续跳变的判断结论, 1：发生 0：未发生

[4] 示例1
--------
>>> status = []
>>> bounceStatus = []
>>> analyzerObj = bounceAnalyzer(_determineDistance=0.2)
>>> for i in range(dataQuant):
>>>     analyzerObj.updateAndDetermine(temper1[i])
>>>     average_lastTime_all.append(analyzerObj.average_lastTime)
>>>     status.append(analyzerObj.bounceStatus)
>>>     bounceStatus.append(analyzerObj.keepBounceStatus)
"""

{% endhighlight %}


### 8.函数的注释
```python
"""
对新传入的数据进行缓存记录，通过平均值计算等方法对跳变状态与持续跳变状态进行判断

[1] 逻辑说明
-----------
输入一个测量值，对其进行滑动窗口的记录。计算记录该数据前后的窗口数据均值

当输入测量值与记录该数据前窗口内数据均值的绝对值达到某一门限值时，触发【跳变】报警：
    :math:`|avg_lastTime - value_thisTime| \\ge\\ k_0`

对是否跳变报警情况进行滑动窗口记录，并根据用以判断是否发生持续跳变的数据窗口尺寸取出近期数个判断结果

当 *跳变发生率* 达到某一门限值时，触发【持续跳变】报警：
    :math:`ratio \\ge\\ k_1`

[2] 参数
--------
_sampleCache:
    float, 新传入的数据
"""
```


### **函数**
```python
"""
:param _records: list[list], 需要绘制在1#Y轴的数据, 可以为多个列表
:param _status: list, 需要绘制在2#Y轴的数据
:param _size: int, -1 表示绘制全量数据, default, -1
:return: None
"""
```

### **类**
```python
"""
……

[1] 参数
----------
_attribute:
    类型, 描述1,描述2, 可选项, 默认值 
_attribute:
    str, 进度条样式, 一个字符, optional, default "="

[2] 方法
----------
_method:
    ……

[3] 返回
-------
out1:
    ……

out2:
    ……

[4] 示例1
--------
>>> ……

[5] 示例2
--------
>>> ……

[6] 备注
-----
* ……

"""

```
### **包**

```python
"""
包括trendAnalyzer, trendPredict两个类

Classes
----------
trendAnalyzer: 使用三阶滑动平均与一阶导对输入数据的快速/缓慢的上升/下降状态进行判断

trendPredict: 通过不断输入一时间序列的数值，顺序地对所定义窗口1内的数值进行三阶滑动平均处理，并计算所定义窗口2内的时序数据一阶导，通过对所定义窗口3内一阶导数据均值进行判断，以确定原始数据的上升/下降情况，包括：是否处理上升/下降状态，是否处于快速/慢速    变化状态

Example
----------
>>> from Method_trendAnalyzer import trendAnalyzer, trendPredict

"""
```