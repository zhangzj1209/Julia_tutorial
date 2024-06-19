# 《Julia 1.7 程序语言》

## 1、概述

### 1-1、命令行运行`julia`启动交互式会话（REPL）
```bash
$ julia
  
               _
   _       _ _(_)_     |  Documentation: https://docs.julialang.org
  (_)     | (_) (_)    |
   _ _   _| |_  __ _   |  Type "?" for help, "]?" for Pkg help.
  | | | | | | |/ _` |  |
  | | |_| | | | (_| |  |  Version 1.7.3 (2022-05-06)
 _/ |\__'_|_|_|\__'_|  |  Official https://julialang.org/ release
|__/                   |

julia> 
```

### 1-2、`julia`基本命令
- 查看`julia`的配置情况
  ```julia
  julia> versioninfo()
  ```
  
- 显示当前工作路径：
  ```julia
  julia> pwd()
  ```
  
- 更改工作目录：
  ```julia
  julia> cd("/data/ustc/")
  ```

### 1-3、利用REPL执行源文件
- `julia`源程序用`.jl`作为扩展名，运行当前目录下的`my_program.jl`：
  ```julia
  julia> include("my_program.jl")
  ```

### 1-4、REPL的提示模式
- REPL的5种提示模式：
  - **Julia模式**：第一行开头为`julia>`的模式，为REPL的默认操作模式。
  - **Help模式**：在Julia模式下键入`?`可进入Help模式查看帮助文档（按`Backspace`可退出Help模式）。如在`help?>`后输入：
    ```julia
    print()
    ```
  - **Shell模式**：在Julia模式下键入`;`可进入Shell模式（按`Backspace`可退出Shell模式）。如在`shell>`后输入：
    ```julia
    cd /data/ustc
    ```
  - **i-search模式**：在Julia模式下同时按`Ctrl`键+`R`键可进入i-search模式（同时按`Ctrl`键+`C`键可退出i-search模式）。
  - **pacakge模式**：在Julia模式下键入`]`可进入pacakge模式（按`Backspace`可退出pacakge模式），可通过运行如下命令来管理Package：
    - `help`：查看Package
    - `status`：查看安装的Package列表
    - `add xxx`：安装某个Package
    - `build xxx`：使Package能够运行
    - `update xxx`：更新Package到新版本
    - `remove xxx`：删除Package

### 1-5、REPL中的快捷键与注意事项
- 同时按`Ctrl`键+`D`键或输入`exit()`可退出REPL。
- 同时按`Ctrl`键+`C`键可中止当前正在运行的耗时较长的程序。
- 在REPL中，在代码的结尾加上`;`，则其结果不会被显示。
- 变量`ans`总会储存最新一行执行代码的结果。


## 2、数据类型与基本运算

### 2-1、常量与变量
- 常量的关键字是`const`
  ```julia
  const e = 2.71828182845904523536
  const pi = 3.14159265358979323846
  ```
- 变量类型
  ```julia
  x = 10           # 整型变量
  y = -10.0        # 浮点型变量
  z = 1 + 2im      # 复数变量
  k = 2//3         # 有理数变量
  name = "zhang"   # 字符串变量
  myc = 'A'        # 字符变量
  ```

### 2-2、整数与浮点数
- `julia`中的整数可直接写成`-123`。
- `julia`中的浮点数可直接写成`0.123`，也可直接写成科学记数法形式`1.23e-1`。
- `julia`中的复数可直接写成`1+2im`。
- `julia`中的字符用单引号`''`表示，字符串用双引号`“”`或三重双引号`""""""`表示。
- 用`typeof()`求某个值的类型：
  ```julia
  # 64位系统：
  julia> typeof(-123)
  Int64

  julia> typeof(1.23e-1)
  Float64

  julia> typeof(1+2im)
  Complex{Int64}

  julia> typeof('A')
  Char

  julia> typeof("ustc")
  String
  ```

### 2-3、四则运算
| 表达式 | 说明 |  
| - | - |
| `-x` | 取相反数 |   
| `x + y` | 加法 |
| `x - y` | 减法 |
| `x * y` | 乘法 |
| `x / y` | 除法 |
| `x ÷ y` | 取`x / y`的整数部分 |
| `x \ y` | 反向除法，等价于`y / x` |
| `x ^ y` | `x`的`y`次幂 |
| `x % y` | 取余数，等价于`rem(x,y)` |

其中，`÷`的输入方法为键入`\div`后按`Tab`，如此还可输入`α`(\alpha)、`π`(\pi)、`∑`(\sum)、`≥`(\ge)、`≤`(\le)、`≠`(\ne)、`∈`(\in)等。

### 2-4、数学函数
- 常见等数学函数有：`log`，`exp`，`sqrt`，`sin`，`cos`，`tan`等。
- `divrem(x, y)`：同时返回`x`除以`y`等商和余数。
- `round(Int, x)`将`x`四舍五入到整数，`round(x, digits=2)`将`x`四舍五入到2位小数，`round(x)`将`x`四舍五入到0位小数的浮点数。
- `floor(Int, x)`求小于等于`x`的最大整数，`floor(x)`返回小于等于`x`的最大整数对应的浮点值。
- `ceil(Int, x)`求大于等于`x`的最大整数，`ceil(x)`返回大于等于`x`的最大整数对应的浮点值。
- `factorial(n)`计算阶乘。

### 2-5、字符串的其他操作
- `*`连接两个字符串：
  ```julia
  julia> "julia_" * "tutorial"
  "julia_tutorial"
  ```

- `^`表示字符串重复：
  ```julia
  julia> "program" ^ 3
  "programprogramprogram"
  ```


## 3、流程控制与逻辑运算
### 3-1、运算符
- **关系运算符**
  | 等于 | 不等于 | 大于 | 小于 | 大于等于 | 小于等于 |
  | - | - | - | - | - | - |
  | `==` | `!=` | `>` | `<` | `>=` | `<=` |
  
- **逻辑运算符**
  | 运算符 | 逻辑表达式 | 意义 |
  | - | - | - |
  | `&&` | `x && y` | 如果两个操作数都非零，则条件为真 |
  | `\|\|` | `x \|\| y` | 如果两个操作数中有任意一个非零，则条件为真 |
  | `!` | `! x` | 逆转操作数的逻辑状态 |
  
  逻辑运算符优先级低于关系运算符；逻辑运算符内部优先级为`!` > `&&` > `||`。

### 3-2、if
- **一般格式**
  ```julia
  if 条件1
      ......
  elseif 条件2
      ......
  else
      ......
  end
  ```
  
- **嵌套if**
  ```julia
  if 条件1
      ......
      if 条件2
          ......
      elseif 条件3
          ......
      else
          ......
      end
  elseif 条件4
      ......
  else
      ......
  end
  ```
  
### 3-3、条件运算符及条件表达式
- 三元运算符`? :`，其构成的条件表达式为：
  ```julia
  表达式1 ? 表达式2 : 表达式3
  ```
  若`表达式1`的值为真，则返回`表达式2`的值，否则返回`表达式3`的值。

### 3-4、复合表达式
- **`begin`块**
  ```julia
  t = begin
      x = 15
      y = 12
      z = 6
      x * y - z
  end
  ```
- **链**
  ```julia
  x = ( a = 2 ;
        b = 3 ;
        c = 6 ;
        a*b+c
  )
  ```

### 3-5、异常处理
- **`try...catch`语句**
  ```julia
  try
      sqrt(-2)
  catch
      println("只有非负数才能求平方根！")
  ```
- **`try...finally`语句**  
  无论程序如何退出，`finally`语句总被执行。
  ```julia
  try
      sqrt(-2)
  catch
      println("只有非负数才能求平方根！")
  finally
      println("我是finally语句！")
  ```


## 4、循环
- **`while`循环**
  ```julia
  while 表达式
      语句
  end
  ```
  在`julia`中没有`do...while`语句。
  
- **`for`循环**
  ```julia
  for 迭代变量 in 可迭代对象
      语句
  end
  ```
  可迭代对象包含：字符串、序列、数组、迭代器等。
  
- **`for`循环中的`range()`函数**
  ```julia
  range(start, stop[, step])
  ```
  
- **`break`和`continue`语句**
  - 使用`break`语句可以跳出`while`或`for`的本层循环。
  - 使用`continue`语句可以跳出当前迭代并继续到下一迭代。


## 5、函数与模块
### 5-1、内置函数
- **基本内置函数**
  | 函数 | 意义 |
  | - | - |
  | `println()` | 打印（结束自动换行） |
  | `readline()` | 读取一行 |
  | `readlines()` | 读取所有行为一个数组 |

- **数学函数**
  | 数学函数 | 意义（返回值） |
  | - | - |
  | `round(x)` | 返回数字的四舍五入值，如`round(4.7)`返回5 |
  | `floor(x)` | 返回数字的下舍整数，如`floor(4.9)`返回4 |
  | `ceil(x)` | 返回数字的上入整数，如`ceil(4.1)`返回5 |
  | `trunc(x)` | 返回数字的向0整数，如`ceil(2.3)`返回2 |
  | `gcd(x,y...)` | 返回x,y,...的最大公约数 |
  | `lcm(x,y...)` | 返回x,y,...的最小共倍数 |
  | `cos(x)` | 返回x弧度的余弦值 |
  | `sin(x)` | 返回x弧度的正弦值 |
  | `abs(x)` | 返回数字的绝对值 |
  | `sign(x)` | 返回数学符号，即-1，0，1 |
  | `sqrt(x)` | 返回x的平方根 |
  | `cbrt(x)` | 返回x的立方根 |
  | `exp(x)` | 返回e的x次幂 |
  | `Log(b,x)` | 返回以b为基数的x的对数 |
  | `max(x1, x2, ...)` | 返回参数或序列的最大值 |
  | `min(x1, x2, ...)` | 返回参数或序列的最小值 |
  
- **随机函数**
  | 随机函数 | 意义（返回值） |
  | - | - |
  | `rand()` | 随机产生0～1的浮点数，可指定行、列数，产生**均匀分布**数 |
  | `randn()` | 随机产生0～1的浮点数，可指定行、列数，产生**正态分布**数 |

- **字符函数**
  | 字符函数 | 意义 |
  | - | - |
  | `Char()` | 将数字转换为字符 |
  | `Int()` | 将字符转换为数字 |

- **字符串函数**
  | 字符串函数 | 意义 |
  | - | - |
  | `SubString(string,start,end)` | 截取字符串中的一部分 |
  | `length(string)` | 获取字符串长度 |
  | `string(a,b)` | 连接字符串a和b |
  | `occursion(str,string)` | 判断字符或字符串str是否在字符串string中，是则返回True，否则返回False |
  
### 5-2、自定义函数
- **`julia`自定义函数的规则**：
  - 函数代码块以`function`关键词开头，后接函数标识符名称和圆括号`()`；
  - 任何传入参数和自变量必须放在园括号中；
  - 函数返回值默认最后一个表达式的值，若不想有返回值，则在最后一行加`nothing`；
  - 一旦运行`return`语句，其后的语句不再运行；
  - 函数结束的标志为`end`。
  ```julia
  function 函数名 (参数列表)
      函数体
  end
  ```

- **函数调用**
  若如下函数内容写在`julia_test_5_2.jl`中，
  ```julia
  function f(x,y)
      if x > 0
          return (x-y)
      elseif x < 0
          return (x+y)
      else 
          return x*y
      end
  end
  ```
  则通过`include("julia_test_5_2.jl")`可调用该函数。
  
### 5-3、模块
模块是一个包含所有定义的函数和变量的文件。

- **模块定义**
  ```julia
  module my_module1
      export my2
      
      function my1()
          println("Good !!!")
      end
      
      function my2(name)
          println("My name is ", name)
      end
  end
  ```
  
- **模块调用**
  ```julia
  using my_module1
  ```


## 6、特征数据类型
#### 6-1、数组
- **创建数组**
  ```julia
  array1 = [1, 3, 5, 7]
  ```

- **修改数组**
  ```julia
  array1[2] = 10
  ```
  使用`push!(array1, 20)`可在数组后添加新数组项。

- **删除数组**
  使用`deleteat!(array1, 3)`可删除数组的第三个数字。

#### 6-2、元组
- **定义元组**
  ```julia
  tup1 = (1, 2, 3)
  ```















  
