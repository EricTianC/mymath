---
tags:
  - 大物实验
  - 数据处理
  - Julia
---
### 简介
#### 什么是 Julia ?

**Julia** 是一门 "面向科学计算的高性能动态高级程序设计语言“ (百度百科). 
简单来说，就是一群学数学的编程爱好者，因为即想要 Python 的便捷易用，又想要 C 的高效，和 Matlab 中明显、熟悉的数学符号，所以聚在一起创造了 Julia ([Why We Created Julia](https://julialang.org/blog/2012/02/why-we-created-julia/)).

#### 为什么用 Julia ?

Julia 是一门年轻的语言，距第一个正式版本 (1.0.0) 发布才仅仅 7 年时间。但正因如此，Julia 在设计之初就能重分考虑到已有的各种语言使用过程的痛点，并加以避免。

同时，诞生时间短并不意味着 Julia 的库匮乏。虽然相对 Python 包丰富程度还远远不够，但在科学计算领域，Julia 已经有了丰富的生态。

**最重要的一点在于：** 相较于 Python 的 OOP，Julia 采取的多重派发机制能够使得代码逻辑更加清晰、更易扩展、更加易用。再搭配上 Julia 适配于数学的许多语法特点，用 Julia 做科学计算确实会比 Python 更为顺手.

### 安装

访问 Julia 中文社区的 [Download Julia](https://cn.julialang.org/downloads/) 页面，选择对应版本进行下载。（一般而言选择 Windows 一栏的 64-bit 选项即可）

亦可使用镜像站：[https://mirrors.tuna.tsinghua.edu.cn/julia-releases/bin/](https://mirrors.tuna.tsinghua.edu.cn/julia-releases/bin/)

然后双击安装包完成安装即可 （如需安装到自己指定的目录，建议先选择以管理员模式运行）。

也可继续参考 [Julia 软件仓库镜像使用帮助 - MirrorZ Help](https://help.mirrors.cernet.edu.cn/julia/) 进行换源
### 基础使用方法

安装完成后，可以直接当作普通应用点击桌面或开始菜单图标开始运行。或者在 Windows Terminal 中输入 `julia` 指令.

随后，你会看到 Julia 的 REPL (read-eval-print-loop) 界面，类似于 Python.

REPL 下有许多便捷功能，

1. 通过输入类似 `\div` + `<tab>` 的方式可以快捷输入 Unicode 字符 (大概和 LaTeX 的中的表示相同，中间有些比较有趣的例子可以自行探索一下).
2. 显示 `julia>` 时是常规状态，可以输入 `?` 切换到帮助状态，此时输入变量名、函数名等可以显示相应文档; 也可以输入 `]` 切换到包管理状态.

#### 数值运算

与 Python 一样，Julia 也采用动态类型 (但需要注意的是，类型在 Julia 程序中充当着比较重要的角色，这点也许稍后会解释).

基础运算和 Python 大致相同，有部分区别
1. 乘方使用 `a^b` ，而非 `a**b`. (因为可以用 `\xor<tab>` 直接输入异或符号 `⊻`)
2. 在使用 数值 `*` 变量 这种形式的表达式时，可以省略 `*` 号，直接写为 `2x` 这样的形式.

在变量方面
1. Julia 中对 Unicode 的支持很好，你可以放心使用如 `ε₀` 这样的符号做变量名 （不知道如何快捷输入的可以直接进入帮助状态查找).
2. 同时如 `÷` (\div), `∈` (\in) 这样的字符也可以很便利的作为运算符使用。
	例如，输入 `×(a, b) = 2(a+b)` 并回车后，可以观察 `1 × 3` 的结果


#### 复合类型

这里只简要介绍一下 Julia 中独特的线性代数符号

先说矩阵，矩阵由 `[` 与 `]` 括起来，其中每行的元素间由空格隔开，每列由 `;` 隔开.  如可输入 `A = [1 2 3; 4 5 6]`

```julia
julia> A = [1 2 3; 4 5 6]
2×3 Matrix{Int64}:
 1  2  3
 4  5  6
```

矩阵的乘法由 `*` 表示，转置由 `'` 表示. 同时，同大小的矩阵的暗元素运算可用 `.+`，`.-` 这样在运算符前加 `.` 的方式表示.

单列的矩阵同时也是向量 (`Vector`)，可以用 `,` 代替 `;`. 建议在用作列表等通途时用逗号，在需要强调方向及线性代数相关运算时使用分号.

### 大物实验中的 Julia

#### 绘图: Plots.jl

使用 `]add Plots` 一键安装。（记得按退格键回到常规输入状态）

输入命令 `using Plots` 即可开始使用. （第一次使用可能会有一段时间预编译过程）

Plots.jl 的设计目标之一就是符合直觉，通过观察几个示例，你可以自由地举一反三，而这些你灵机一动想出来的用法应该都能奏效. 不过你仍可以查看如 [19 Julia统计图形–Plots库 | Julia语言入门](https://www.math.pku.edu.cn/teachers/lidf/docs/Julia/html/_book/plplots.html#plplots-lines) 这样的资料获取更多参考.

#### 开始使用
在 Julia 中，函数也是一种类型. 比如 `sin`
所以想绘制函数，只需直接将函数传入绘图函数即可

```julia
plot(sin)
```

![[pigsin.svg]]
如果你有两组数据

```julia
xs = 1:10 # 一到十列表的简写
ys = [2k^2 for k in xs] # [2, 8, ...]
```

可用 `scatter(xs, ys)` 做散点图 (对应 `plot` 为折线图)

![[pigquad.svg]]
通过设置参数可以更改图中其它样式，如 `scatter(exp2_l, exp2_t.^2, xlabel="Length", ylabel=L"(30T)^2", legend=false)`  （摘自单摆实验报告)

使用 `savefig("xxx.svg")` 保存当前绘制的图片。同时你也可以选择其它格式，`savefig` 会根据你的文件的后缀名进行自动判断。

通过选择不同的绘图后端 [Backends · Plots](https://docs.juliaplots.org/latest/backends/) ，你可以得到不同的功能特性的绘图。其中使用 `PGFPlots/ PGFPlotsX` 可以将图片保存为 `tikz` 文件直接插入 `tex` 格式的报告中

#### 数据处理

##### 带单位运算: Unitful.jl

`]add Unitful` (退格)
`using Unitful`

同时可以使用 `using Unitful: m, s, N` 导入单位符号，或使用 `u"cm"` 代表单位.

带单位的符号与大部分运算兼容，也与 `Plots.jl` 兼容.

相关函数
- `upreferred(1N)`：转为国际单位制中的基本单位表示
- `uconvert(m, 3.14mm)`: 单位转换
- `ustrip(3s)`: 去除单位
##### 不确定度分析: Measurements.jl

`]add Measurements`
`using Measurements`

使用 `\pm` 打出 `±` ，按直觉使用即可

##### 多项式拟合: Polynomial.jl

对带不确定度的数据（需无单位，使用 ustrip），
使用 pfit = fit(x, y, 1) 即可完成线性（一次）拟合

##### 线性回归: GLM.jl (暂不详细介绍)
##### 非线性拟合: LsqFit.jl

```julia
@. model(t, p) = p[1] * Base.sin(p[2] * t + p[3]) + p[4] # p = [A, ω, φ, C]
# 再使用 curve_fit 调整初始参数即可
```


本篇介绍尚未完善，更多的奇妙用法待你探索. 