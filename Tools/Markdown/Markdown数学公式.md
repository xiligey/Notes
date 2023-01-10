## 大括号里多行公式

$$
f(n) =\begin{cases}n/2,  & \text{if $n$ is even} \\\\3n+1, & \text{if $n$ is odd}\end{cases}
$$

## 数学公式按等号对齐

$$
\begin{aligned} J(\theta )&=\frac{1}{2}{{\left( X\theta -y\right)}^{T}}\left( X\theta -y \right)\\ & =\frac{1}{2}\left( {{\theta }^{T}}{{X}^{T}}-{{y}^{T}} \right)\left(X\theta -y \right)\\ &=\frac{1}{2}\left( {{\theta }^{T}}{{X}^{T}}X\theta -{{\theta}^{T}}{{X}^{T}}y-{{y}^{T}}X\theta -{{y}^{T}}y \right) \end{aligned} \tag 3
$$

## 行内与独行

1. 行内公式：将公式插入到本行内，符号：`$公式内容$`，如：*xyz*
2. 独行公式：将公式插入到新的一行内，并且居中，符号：`$$公式内容$$`，如：

*y* = *αx* + *β*

## 上标、下标与组合

1. 上标符号，`x^4` ：$x^4$
2. 下标符号，`x_2` ：$x_2$
3. 组合符号，`x_{i,j}` ：$x_{i,j}$

## 汉字、字体与格式

1. 汉字形式，符号：`\mbox{}`，如 
2. 字体控制，`\displaystyle \frac{x+y}{y+z}`  $\displaystyle \frac{x+y}{y+z}$
3. 下划线符号，`\underline{x+y}`  $\underline{x+y}$
4. 标签，`y=ax+b\tag{11}`  

$$
y=ax+b\tag{11}
$$

1. 上大括号，`\overbrace{a+b+c+d}^{2.0}`  
   
    $$
    \overbrace{a+b+c+d}^{2.0}
    $$
    
2. 下大括号，`a+\underbrace{b+c}_{1.0}+d` 
   
    $$
    a+\underbrace{b+c}_{1.0}+d
    $$
    
3. 上位符号，`\vec{x}\stackrel{\mathrm{def}}{=}{x_1,\dots,x_n}`
   
    $$
    \vec{x}\stackrel{\mathrm{def}}{=}{x_1,\dots,x_n}
    $$
    

## 占位符

1. 两个quad空格，`x \qquad y`，如：$x \qquad y$
2. quad空格，`x \quad y` $x \quad y$
3. 大空格，`x \ y` *$x \ y$*
4. 中空格，`x \: y` $x \: y$
5. 小空格，符号`\,`，如：*x*, *y*
6. 没有空格，符号``，如：*xy*
7. 紧贴，符号`\!`，如：*x*​*y*

## 定界符与组合

1. 括号，符号：`（）\big(\big) \Big(\Big) \bigg(\bigg) \Bigg(\Bigg)`，如：()()()()()
2. 中括号，符号：`[]`，如：[*x* + *y*]
3. 大括号，符号：`\{ \}`，如：{*x* + *y*}
4. 自适应括号，符号：`\left \right`，如：(*x*)，$\left(xz}\right)$
5. 组合公式，符号：`{上位公式 \choose 下位公式}`，如：${n+1 \choose k}={n \choose k}+{n \choose k-1}$
6. 组合公式，符号：`{上位公式 \\atop 下位公式}`，如：$\sum_{k_0,k_1,\ldots>0 \atop k_0+k_1+\cdots=n}A_{k_0}A_{k_1}\cdots$

## 四则运算

1. 加法运算，符号：`+`，如：*x* + *y* = *z*
2. 减法运算，符号：``，如：*x* − *y* = *z*
3. 加减运算，符号：`\pm`，如：*x* ± *y* = *z*
4. 减加运算，符号：`\mp`，如：*x* ∓ *y* = *z*
5. 乘法运算，符号：`\times`，如：*x* × *y* = *z*
6. 点乘运算，符号：`\cdot`，如：*x* ⋅ *y* = *z*
7. 星乘运算，符号：`\ast`，如：*x* * *y* = *z*
8. 除法运算，符号：`\div`，如：*x* ÷ *y* = *z*
9. 斜法运算，符号：`/`，如：*x*/*y* = *z*
10. 分式表示，符号：`\frac{分子}{分母}`，如：$\frac{x+y}{y+z}$
11. 分式表示，符号：`{分子} \voer {分母}`，如：${x+y} \over {y+z}$
12. 绝对值表示，符号：`|`，如：|*x* + *y*|

## 高级运算

1. 平均数运算，符号：`\overline{算式}`，如：$\overline{xyz}$
2. 开二次方运算，符号：`\sqrt`，如：$\sqrt x$
3. 开方运算，符号：`\sqrt[开方数]{被开方数}`，如：$\sqrt[3]{x+y}$
4. 对数运算，符号：`\log`，如：log (*x*)
5. 极限运算，符号：`\lim`，如：$\lim^{x \to \infty}_{y \to 0}{\frac{x}{y}}$
6. 极限运算，符号：`\displaystyle \lim`，如：$\displaystyle \lim^{x \to \infty}_{y \to 0}{\frac{x}{y}}$
7. 求和运算，符号：`\sum`，如：$\sum^{x \to \infty}_{y \to 0}{\frac{x}{y}}$
8. 求和运算，符号：`\displaystyle \sum`，如：$\displaystyle \sum^{x \to \infty}_{y \to 0}{\frac{x}{y}}$
9. 求积运输，符号： `\prod`，如：$\prod_{i=1}^nx_i$
10. 积分运算，符号：`\int`，如：∫*xdx*
    
    0
    
    ∞
    
11. 积分运算，符号：`\displaystyle \int`，如：$\displaystyle \int_1 ^{10}x^2$    
12. 微分运算，符号：`\partial`，如：$\frac{\partial x}{\partial y}$
13. 矩阵表示，符号：`\begin{matrix} \end{matrix}`，如：

$$\left[ \begin{matrix} 1 &2 &\cdots &4\\5 &6 &\cdots &8\\\vdots &\vdots &\ddots &\vdots\\13 &14 &\cdots &16\end{matrix} \right]$$

## 逻辑运算

1. 等于运算，符号：`=`，如：*x* + *y* = *z*
2. 大于运算，符号：`>`，如：*x* + *y* > *z*
3. 小于运算，符号：`<`，如：*x* + *y* < *z*
4. 大于等于运算，符号：`\geq`，如：*x* + *y* ≥ *z*
5. 小于等于运算，符号：`\leq`，如：*x* + *y* ≤ *z*
6. 不等于运算，符号：`\neq`，如：*x* + *y* ≠ *z*
7. 不大于等于运算，符号：`\ngeq`，如：*x* + *y* ≱ *z*
8. 不大于等于运算，符号：`\not\geq`，如： $x+y \not\geq z$
9. 不小于等于运算，符号：`\nleq`，如：*x* + *y* ≰ *z*
10. 不小于等于运算，符号：`\not\leq`，如：$x+y \not\leq z$
11. 约等于运算，符号：`\approx`，如：*x* + *y* ≈ *z*
12. 恒定等于运算，符号：`\equiv`，如：*x* + *y* ≡ *z*
13. 加减，符号: `\pm`，如：*x* ± *y*

## 集合运算

1. 属于运算，符号：`\in`，如：*x* ∈ *y*
2. 不属于运算，符号：`\notin`，如：*x* ∉ *y*
3. 不属于运算，符号：`\not\in`，如：*x* ∉ *y*
4. 子集运算，符号：`\subset`，如：*x* ⊂ *y*
5. 子集运算，符号：`\supset`，如：*x* ⊃ *y*
6. 真子集运算，符号：`\subseteq`，如：*x* ⊆ *y*
7. 非真子集运算，符号：`\subsetneq`，如*x* ⊊ *y*
8. 真子集运算，符号：`\supseteq`，如：*x* ⊇ *y*
9. 非真子集运算，符号：`\supsetneq`，如：*x* ⊋ *y*
10. 非子集运算，符号：`\not\subset`，如：*x* ⊄ *y*
11. 非子集运算，符号：`\not\supset`，如：*x* ⊅ *y*
12. 并集运算，符号：`\cup`，如：*x* ∪ *y*
13. 交集运算，符号：`\cap`，如：*x* ∩ *y*
14. 差集运算，符号：`\setminus`，如：*x* \ *y*
15. 同或运算，符号：`\bigodot`，如：*x*⨀*y*
16. 同与运算，符号：`\bigotimes`，如：*x*⨂*y*
17. 实数集合，`\mathbb{R}` $\mathbb R$
18. 自然数集合，符号：`\mathbb{Z}`，如：ℤ
19. 空集，符号：`\emptyset`，如：∅

## 数学符号

1. 无穷，符号：`\infty`，如：∞
2. 虚数，符号：`\imath`，如：ı
3. 虚数，符号：`\jmath`，如：ȷ
4. 数学符号，符号`\hat{a}`，如：*â*
5. 数学符号，符号`\check{a}`，如：*ǎ*
6. 数学符号，符号`\breve{a}`，如：*ă*
7. 数学符号，符号`\tilde{a}`，如：*ã*
8. 数学符号，符号`\bar{a}`，如：*ā*
9. 矢量符号，符号`\vec{a}`，如：*á*
10. 数学符号，符号`\acute{a}`，如*á*
11. 数学符号，符号`\grave{a}`，如：*à*
12. 数学符号，符号`\mathring{a}`，如：*å*
13. 一阶导数符号，符号`\dot{a}`，如：*ȧ*
14. 二阶导数符号，符号`\ddot{a}`，如：$\ddot{a}$
15. 上箭头，符号：`\uparrow`，如：↑
16. 上箭头，符号：`\Uparrow`，如：⇑
17. 下箭头，符号：`\downarrow`，如：↓
18. 下箭头，符号：`\Downarrow`，如⇓
19. 左箭头，符号：`\leftarrow`，如：←
20. 左箭头，符号：`\Leftarrow`，如：⇐
21. 右箭头，符号：`\rightarrow`，如：→
22. 右箭头，符号：`\Rightarrow`，如：⇒
23. 底端对齐的省略号，符号：`\ldots`，如：1, 2, …, *n*
24. 中线对齐的省略号，符号：`\cdots`，如：*x* + *x* + ⋯ + *x*
    
    1
    
    2
    
    2
    
    2
    
    *n*
    
    2
    
25. 竖直对齐的省略号，符号：`\vdots`，如：⋮
26. 斜对齐的省略号，符号：`\ddots`，如：⋱

## 希腊字母

| 字母 | 实现 | 字母 1 | 实现 1 |
| --- | --- | --- | --- |
| A | A | α | α |
| B | B | β | β |
| Γ | Γ | γ | γ |
| Δ | Δ | δ | δ |
| E | E | ϵ | ϵ |
| Z | Z | ζ | ζ |
| H | H | η | η |
| Θ | Θ | θ | θ |
| I | I | ι | ι |
| K | K | κ | κ |
| Λ | Λ | λ | λ |
| M | M | μ | μ |
| N | N | ν | ν |
| Ξ | Ξ | ξ | ξ |
| O | O | ο | $\omicron$ |
| Π | Π | π | π |
| P | P | ρ | ρ |
| Σ | Σ | σ | σ |
| T | T | τ | τ |
| Υ | Υ | υ | υ |
| Φ | Φ | ϕ | ϕ |
| X | X | χ | χ |
| Ψ | Ψ | ψ | ψ |
| Ω | Ω | ω | ω |
