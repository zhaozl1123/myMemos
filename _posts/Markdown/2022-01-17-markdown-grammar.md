---
title: Markdown语法
date: 2022-01-17 13:47:00 +0800
categories: [markdown, grammar]
tags: [markdown, markdown-grammar]
pin: true
toc: true
comments: true
mermaid: true
math: true
author:
  name: zhaozl1123
  link: https://github.com/zhaozl1123
---



## 标题

```md
# 一级标题
## 二级标题
### 三级标题
#### 四级标题
##### 五级标题
###### 六级标题
```

## 换行

```md
末尾双空格  
或空一行
```


## 标注
*斜体*
_斜体_

**粗体**
__粗体__

***粗斜体***
___粗斜体___

```md
*斜体*
_斜体_

**粗体**
__粗体__

***粗斜体***
___粗斜体___
```


## 分割线
----------
```md
***
* * *
*****
- - -
----------
```


## 删除线
~~删除线~~

```md
~~删除线~~
```


## 下划线
<u>下划线</u>

```md
<u>下划线</u>
```


## 脚注
脚注[^1]
[^1]:这里是脚注1

脚注^[这里是行内脚注]
```md
脚注[^1]
[^1]:这里是脚注1

脚注^[这里是行内脚注]
```


## 上标/下标
上标^上标^  
下标~下标~  

```md
上标^上标^  
下标~下标~  
```


## 列表
1. 第一项
	* 第一项
	+ 第二项
	- 第三项
2. 第二项
3. 第三项
```md
1. 第一项
	* 第一项
	+ 第二项
	- 第三项
2. 第二项
3. 第三项
```


## 引用
* 第一项
    > 菜鸟教程  
    > 学的不仅是技术更是梦想
```md
* 第一项
    > 菜鸟教程/s/s
    > 学的不仅是技术更是梦想
```


## 函数
`printf()`  
<kbd>printf()</kbd>

```md
`printf()`
<kbd>printf()</kbd>
```


## 链接
<https://www.baidu.com>  
[百度](https://www.baidu.com)  
[Bai度][baidu]

[baidu]:https://www.baidu.com
```md
<https://www.baidu.com>  
[百度](https://www.baidu.com)  
[Bai度][baidu]

[baidu]:https://www.baidu.com
```

## 图片

![imgName](https://www.baidu.com/img/PCtm_d9c8750bed0b3c7d089fa7d55720d6cf.png)

```md
![imgName](https://www.baidu.com/img/PCtm_d9c8750bed0b3c7d089fa7d55720d6cf.png)
```


## 表格
```markdown
|col1Name|col2Name|
|:----:|:----:|
|col1Content|col2Content|
```

|col1Name|col2Name|
|:----:|:----:|
|col1Content|col2Content|




## 公式
$$
\frac{a_1 + a_2}{b_1} = a_3 \times a_4
$$
```md
$$
\frac{a_1 + a_2}{b_1} = a_3 \times a_4
$$
```

