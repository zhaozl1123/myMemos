---
title: Markdown语法
date: 2022-01-29 09:51:00 +0800
categories: [markdown, formula]
tags: [markdown, markdown-formula]
pin: true
toc: true
comments: true
mermaid: true
math: true
author:
  name: zhaozl1123
  link: https://github.com/zhaozl1123
---

### ==基本要求==

Markdown公式使用\$符号包围 ，如 \$ 公式 \$，且\$前后不允许空格

#### 在Markdown中，使用格式如下：

```
$$
max(a) - min(a) = mean(a)
$$
```

效果：
$$
max(a) - min(a) = mean(a)
$$

#### 在Pycharm中，使用格式如下：

```
.. math:: $x[max(X) - min(X)] \\div { average(X) }$

:math:`(max(X) - min(X)) \\div { avg(X) }`
```

效果

```
x[max(X) − min(X)]÷average(X)

(max(X) − min(X))÷avg(X)
```

### ==常用符号==

| Markdown | 效果 |
| ---- | ---- |
| \pm | $\pm$ |
|\times|$$\times$$|
|\div|$\div$|
|\sum_{i=0}^n \frac{1}{i^2}|$\sum_{i=0}^n \frac{1}{i^2}$|
|\prod_{i=0}^n|$\prod_{i=0}^n$|
|\neq|$\neq$|
|\backslash|$\backslash$|
|\leq|$\leq$|
|\geq|$\geq$|
|\cdot|$\cdot$|
|\ast|$\ast$|
|\star|$\star$|
|\rightarrow|$\rightarrow$|
|\mid|$\mid$|
|\&infin;|&infin;|
|\cdots|$\cdots$|
|\ddots|$\ddots$|
|\vdots|$\vdots$|
|||
|||
|||
|||
|||
|||
|||

### ==公式方法==

| Markdown | 效果 |
| ---- | ---- |
| X^2 | $X^2$ |
|X_2|$X_2$|
|{X_1}^2|${X_1}^2$|
|{X_1}^{ab}|${X_1}^{ab}$|
|X_{ab}|$X_{ab}$|
|\frac{7x+5}{1+y^2}|$\frac{7x+5}{1+y^2}$|
|\sqrt{2}|$\sqrt{2 }$|
|\sqrt[n]{3}|$\sqrt[n]{3}$|
|\vec{a} \cdot \vec{b}=0|$\vec{a} \cdot \vec{b}=0$|
|\overline{a+b+c+d}|$\overline{a+b+c+d}$|
|\underline{a+b+c+d}|$\underline{a+b+c+d}$|
|\overbrace{a+\underbrace{b+c}{1.0}+d}^{2.0}|$\overbrace{a+\underbrace{b+c}{1.0}+d}^{2.0}$|
|||
|||
|||

### ==积分==

|Markdown|效果|
|----|----|
|\int|$\int$|
|\iint|$\iint$|
|\iiint|$\iiint$|
|\int_m^n|$\int_m^n$|
|\int_01x2dx|$\int_01x2dx$|
|\rightarrow|$\rightarrow$|
|\lim_{n\rightarrow+\infty}\frac{1}{n}|$\lim_{n\rightarrow+\infty}\frac{1}{n}$$|
|\infty|$\infty$|
|\nabla|$\nabla$|
|||

### ==集合==

|Markdown|效果|
|----|----|
|\emptyset|$\emptyset$|
|\in|$\in$|
|\notin|$\notin$|
|\subset|$\subset$|
|\supset|$\supset$|
|\subseteq|$\subseteq$|
|\supseteq|$\supseteq$|
|\bigcap|$\bigcap$|
|\bigcup|$\bigcup$|
|\bigvee|$\bigvee$|
|\bigwedge|$\bigwedge$|
|\biguplus|$\biguplus$|
|\bigsqcup|$\bigsqcup$|
|||
|||
|||

### ==逻辑==

|Markdown|效果|
|----|----|
|\because|\because|
|\therefore|\therefore|
|\forall|\forall|
|\exists|\exists|
|\not=|\not=|
|\not>|\not>|
|\not\subset|\not\subset|
|||
|||
|||
|||

### ==其他==

|Markdown|效果|
|----|----|
|\hat{y}|$\hat{y}$|
|\check{y}|$\check{y}$|
|\breve{y}|$\breve{y}$|
|\&nbsp;|1个空格|
|\&ensp;|2个空格|
|\&emsp;|4个空格|
|\uparrow \downarrow \leftarrow \rightarrow|$\uparrow$$\downarrow$$\leftarrow$$\rightarrow$|
|\Uparrow \Downarrow \Leftarrow \Rightarrow|$\Uparrow$$\Downarrow$$\Leftarrow$$\Rightarrow$|
|\longleftarrow \longrightarrow| $\longleftarrow$$\longrightarrow$|
|\Longleftarrow \Longrightarrow|$\Longleftarrow$$\Longrightarrow$|
|||
|||

### ==方程组==
```
$$
y=
\begin{cases}
-x,\quad x\leq 0\\
x, \quad x>0
\end{cases}
\tag{1}
$$
```

效果
$$
y=
\begin{cases}
-x,\quad x\leq 0\\
x, \quad x>0
\end{cases}
\tag{1}
$$

### ==矩阵==
```
$$
\begin{matrix}
1 & 2 & 3\\
4 & 5 & 6 \\
7 & 8 & 9
\end{matrix}
\tag{1}
$$
```

效果
$$
\begin{matrix}
1 & 2 & 3\\
4 & 5 & 6 \\
7 & 8 & 9
\end{matrix}
\tag{1}
$$

### ==小括号==
```
$$\left(
\begin{matrix}
1 & 2 & 3\\
4 & 5 & 6 \\
7 & 8 & 9
\end{matrix}
\right)
\tag{2}
$$
```

效果
$$
\left(
\begin{matrix}
1 & 2 & 3\\
4 & 5 & 6 \\
7 & 8 & 9
\end{matrix}
\right)
\tag{2}
$$

### ==中括号==
```
$$\left[
\begin{matrix}
1 & 2 & 3\\
4 & 5 & 6 \\
7 & 8 & 9
\end{matrix}
\right]
\tag{3}
$$
```

效果
$$
\left[
\begin{matrix}
1 & 2 & 3\\
4 & 5 & 6 \\
7 & 8 & 9
\end{matrix}
\right]
\tag{3}
$$

### ==大括号==
```
$$\left\{
\begin{matrix}
1 & 2 & 3\\
4 & 5 & 6 \\
7 & 8 & 9
\end{matrix}
\right\}
\tag{4}
$$
```

效果
$$
\left\{
\begin{matrix}
1 & 2 & 3\\
4 & 5 & 6 \\
7 & 8 & 9
\end{matrix}
\right\}
\tag{4}
$$

### ==省略矩阵==
```
$$
\left[
\begin{matrix}
a & b & \cdots & a\\
b & b & \cdots & b\\
\vdots & \vdots & \ddots & \vdots\\
c & c & \cdots & c
\end{matrix}
\right]
\tag{5}
$$
```

效果
$$
\left[
\begin{matrix}
a & b & \cdots & a\\
b & b & \cdots & b\\
\vdots & \vdots & \ddots & \vdots\\
c & c & \cdots & c
\end{matrix}
\right]
\tag{5}
$$

### ==分割矩阵==
```
$$
\left[
\begin{array}{c|cc}
1 & 2 & 3 \\
4 & 5 & 6 \\
7 & 8 & 9
\end{array}
\right]
\tag{6}
$$
```
效果
$$
\left[
\begin{array}{c|cc}
1 & 2 & 3 \\
4 & 5 & 6 \\
7 & 8 & 9
\end{array}
\right]
\tag{6}
$$

```
$$
\left[
    \begin{array}{c|cc}
    1 & 2 & 3 \\ \hline
    4 & 5 & 6 \\
    7 & 8 & 9
    \end{array}
\right]
\tag{7}
$$
```

效果
$$
\left[
    \begin{array}{c|cc}
    1 & 2 & 3 \\ \hline
    4 & 5 & 6 \\
    7 & 8 & 9
    \end{array}
\right]
\tag{7}
$$

