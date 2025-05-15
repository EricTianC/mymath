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

然后双击安装包完成安装即可 （如需安装到自己指定的目录，建议先选择以管理员模式运行）。

### 基础使用方法

安装完成后，可以直接当作普通应用点击桌面或开始菜单图标开始运行。或者在 Windows Terminal 中输入 `julia` 指令.

随后，你会看到 Julia 的 REPL (read-eval-print-loop) 界面，类似于 Python.

REPL 下有许多便捷功能，

1. 通过输入类似 `\div` + `<tab>` 的方式可以快捷输入 Unicode 字符 (大概和 LaTeX 的中的表示相同，中间有些比较有趣的例子可以自行探索一下).
2. 显示 `julia>` 时是常规状态，可以输入 `?` 切换到帮助状态，此时输入变量名、函数名等可以显示相应文档.

#### 数值运算

与 Python 一样，Julia 也采用动态类型 (但需要注意的是，类型在 Julia 程序中充当着比较重要的角色，这点也许稍后会解释).

基础运算和 Python