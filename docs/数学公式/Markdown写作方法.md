# MarkDown与Latex

>  注意：Latex是公式排版的一种方法，有众多的公式编辑器支持Latex，MarkDown文本支持Latex公式插入，在写笔记的时候更加方便输入公式相关的内容。

[使用Latex在线编写公式](https://www.latexlive.com/home)

## 插入公式

在MarkDown文本中，通过使用 金钱 符号 对公式进行包围，在显示的时候即可显示出完整的公式信息。

## 插入序列

在公式结尾位置加入`\tag{1.1}`，即可在尾部显示(1.1)，如下所示。

$$
\begin{align}
x = a + b \tag{1.1}
\end{align}
$$

## 公式换行

在公式结尾位置加入`\\ `即可将该位置后面的数据转化到下一行中，如下所示。

$$
\begin{align}
x=\\ a +  b  \tag{1}
\end{align}
$$

## 公式分数

使用`\frac{分子}{分母}`写分式，可以写出来分数。

$$
\begin{align}
x = \frac{a}{b} \tag{2}
\end{align}
$$

> 注意+总结：公式的结构过于复杂， 数学字母太多，不可能记录全部，只能通过在线网站进行构建，长期使用熟练后再脱离公式快速编写。

## 公式格式

### 1. 公式颜色

> 注意：测试发现在公式中，出了{}部分指定的颜色外，{}后面的公式也会是这个颜色，因此在使用颜色功能时需要注意。

如果要改变公式部分文字的颜色，使用`\color{颜色}{公式内容}`即可修改公式中指定字符的颜色。

$$
\begin{align}
\color{red}{x} = \color{green}{a}+\color{blue}{b}\tag{3}
\end{align}
$$

### 2. 公式分支

使用公式对`\begin{align} \end{align}`包括公式，可以使得公式横向对齐。

使用公式对`\begin{cases} \end{cases}`包括公式，输入左侧大括号，包括的内容`\\`换行时不换行整个公式。

$$
\begin{align}
f(x)=\begin{cases}p&{\text{if }}x=1,\\1-p&{\text{if }}x=0,\end{cases} \tag{4}
\end{align} 
$$

### 3. 公式外框

输入 `\boxed{公式}` 在公式加入边框。

$$
\begin{align}
\boxed{E=mc^2} \tag{5}
\end{align} 
$$

### 4. 删除格式

> 这段我没有实现成功，没有示例，后面我要继续测试怎么写，一点一点补充这个文档。

输入`\require{cancel}`允许公式删除，并且使用`\cancel、\bcancel、\xcancel、\cancelto`实现删除线效果。
