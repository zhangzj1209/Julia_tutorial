# 《Julia 1.7.3 程序语言》

## 0、Julia软件安装

### 0-1、学习资源
- Julia主网站：[https://julialang.org/](https://julialang.org)
- Julia官方文档：[https://docs.julialang.org/en/v1/](https://docs.julialang.org/en/v1/)
- Julia扩展包查找：[https://juliahub.com/ui/Packages](https://juliahub.com/ui/Packages)
- 清华大学开源软件镜像网站：[https://mirror.tuna.tsinghua.edu.cn/help/julia/](https://help.mirrors.cernet.edu.cn/julia/)

### 0-2、Julia命令行程序的安装和使用
- 下载和解压`julia`软件包
  ```bash
  wget https://julialang-s3.julialang.org/bin/linux/x64/1.7/julia-1.7.3-linux-x86_64.tar.gz
  tar zxvf julia-1.7.3-linux-x86_64.tar.gz
  ```

- 添加**环境变量**
  ```bash
  vim ~/.bashrc
  export PATH="$PATH:/data/ustc/julia-1.7.3/bin"
  source ~/.bashrc
  ```

- 将`Julia`添加到`Jupyter Notebook`
  ```julia
  import Pkg
  Pkg.add("IJulia")
  ```


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
- 查看`julia`的配置情况：
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
- `julia`源程序用`.jl`作为扩展名，运行**当前目录下**的`my_program.jl`：
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
    cd /data/ustc/
    ```
  - **i-search模式**：在Julia模式下同时按`Ctrl`键+`R`键可进入i-search模式（同时按`Ctrl`键+`C`键可退出i-search模式）。
  - **pacakge模式**：在Julia模式下键入`]`可进入pacakge模式（按`Backspace`可退出pacakge模式），可通过运行如下命令来管理Package：
    - `help`：查看Package。
    - `status`：查看安装的Package列表。
    - `add xxx`：安装某个Package。
    - `build xxx`：使Package能够运行。
    - `update xxx`：更新Package到新版本。
    - `remove xxx`：删除Package。

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
- `divrem(x, y)`：同时返回`x`除以`y`的商和余数。
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
  | `readlines()` | 读取所有行成为一个数组 |

- **数学函数**
  | 数学函数 | 意义（返回值） |
  | - | - |
  | `round(x)` | 返回数字的四舍五入值，如`round(4.7)`返回5 |
  | `floor(x)` | 返回数字的下舍整数，如`floor(4.9)`返回4 |
  | `ceil(x)` | 返回数字的上入整数，如`ceil(4.1)`返回5 |
  | `trunc(x)` | 返回数字的向0整数，如`ceil(2.3)`返回2 |
  | `gcd(x,y...)` | 返回x,y,...的最大公约数 |
  | `lcm(x,y...)` | 返回x,y,...的最小公倍数 |
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
  - 任何传入参数和自变量必须放在圆括号中；
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
### 6-1、数组
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

### 6-2、元组
- **定义元组**
  ```julia
  tup1 = (1, 2, 3)  # 当元组仅含一个元素时，需在元素后添加逗号
  tup2 = ()         # 定义空元组
  ```

### 6-3、字典
- **定义字典**
  ```julia
  dict1 = Dict("name"=>"zhang", "age"=>"10")
  ```

- **访问字典的值和键**
  ```julia
  println("Name: ", dict1["name"])
  ```

- **修改字典**
  ```julia
  dict1["age"] = "20"
  ```

### 6-4、集合
- **定义集合**
  ```julia
  a = Set([1, 2, 3])
  a = Set()          # 创建空集合
  ```


## 7、矩阵操作
### 7-1、矩阵的创建与索引
- **创建矩阵**
  ```julia
  matrix1 = [1 2 3; 4 5 6]
  matrix2 = rand(1:10, 3, 4)  # 创建3×4的随机矩阵
  matrix3 = ones(4, 5)        # 创建全1矩阵
  matrix4 = zeros(5, 6)       # 创建全0矩阵
  ```

### 7-2、矩阵的拼接
- **横向拼接**
  ```julia
  a = ones(3, 2)
  b = zeros(3, 2)
  c = [a b]  或  c = hcat([a, b]...)
  ```

- **纵向拼接**
  ```julia
  a = ones(3, 2)
  b = zeros(3, 2)
  c = [a; b]  或  c = vcat([a, b]...)
  ```

### 7-3、矩阵的运算
- **矩阵加法、矩阵减法**
  ```julia
  A = rand(2, 3)
  B = rand(2, 3)
  C = A + B
  D = A - B
  ```

- **矩阵转置**
  ```julia
  A = rand(2, 3)
  B = A'
  ```

- **矩阵数乘**
  ```julia
  A = rand(2, 3)
  B = 3 * A
  ```

- **矩阵乘法**
  ```julia
  A = rand(2, 3)
  B = rand(3, 4)
  C = A * B
  ```

### 7-4、矩阵的函数应用
- **矩阵的基本函数**
  - `typeof()`：矩阵的类型。
  - `eltype()`：矩阵中元素的类型。
  - `length()`：矩阵中元素的个数。
  - `ndims()`：矩阵的维度。
  - `size()`：矩阵的行数和列数。

- **矩阵的其它创建函数**
  ```julia
  a = trues(3, 4)       # 创建3×4的元素全true的矩阵
  b = falses(3, 4)      # 创建3×4的元素全false的矩阵
  c = reshape(a, 4, 3)  # 重新设置矩阵大小为4×3
  d = copy(b)           # 复制矩阵
  ```

- **矩阵的函数运算**
  ```julia
  x1 = randn(6, 4)    # 创建一个正态分布矩阵
  x2 = round.(x1)     # 对矩阵x1进行四舍五入运算，round与()之间加一个.表示对矩阵进行操作
  x3 = abs.(x1)       # 对矩阵x1取绝对值
  x4 = sqrt.(x3)      # 对矩阵x3取平方根
  x5 = sin.(x1)       # 对矩阵x1进行正弦运算
  ```


## 8、文件操作
### 8-1、文件的基本操作
- **文件的创建**
  ```julia
  open(filename, keyword)  # filename为创建的文件名，kerword为创建文件的关键字
  ```
  `kerword`的参数及意义：
  - `w`：打开文件只用于写入。若文件已存在，则删除原有内容并从头开始编辑。
  - `w+`：打开文件用于读写。若文件已存在，则删除原有内容并从头开始编辑。
  - `a`：打开文件用于追加。若文件已存在，则新内容将会被写入到已有内容之后。
  - `a+`：打开文件用于读写。若文件已存在，则新内容将会被写入到已有内容之后。
  - `r`：打开文件只读。
  - `r+`：打开文件用于读写。

- **写入文件内容**
  ```julia
  txt = open("myfile.txt", "w")
  write(txt, "hello world!")
  close(txt)
  ```

- **读取文件内容**
  ```julia
  readlines("mybook.txt")  # 读取打开文件中的所有内容
  readline("mybook.txt")   # 读取打开文件的第一行
  read("mybook.txt", String)
  ```

### 8-2、文件中的矩阵操作
- **把矩阵写入文件**
  ```julia
  using DelimitedFiles
  matrix1 = rand(1:100, 10, 8)
  mya = open("my_matrix.txt", "w")
  writedlm(mya, matrix1, "\t")
  close(mya)
  ```

- **从文件中读取矩阵内容**
  ```julia
  using DelimitedFiles
  myb = open("my_matrix.txt", "r")
  readdlm(myb)
  ```

## 9、Julia的日期和时间
```julia
using Dates
```

### 9-1、`Date()`函数
- **创建日期的方式**
  ```julia
  my_t = Date(2019,4,11)       # 2019-04-11 
  ```

- **获取创建日期的年、月、日信息**
  ```julia
  t = Date(2019,4,11)          # 2019-04-11
  y = Dates.year(t)            # 2019
  m = Dates.month(t)           # 4
  d = Dates.day(t)             # 11

  ym = Dates.yearmonth(t)      # (2019, 4)
  md = Dates.monthday(t)       # (4, 11)
  ymd = Dates.yearmonthday(t)  # (2019, 4, 11)

  Y = Dates.Year(t)            # 2019 years
  M = Dates.Month(t)           # 4 months
  D = Dates.Day(t)             # 11 days
  ```

- **获取星期几的信息**
  ```julia
  t = Date(2019,4,11)          # 2019-04-11
  w = Dates.dayofweek(t)       # 4
  we = Dates.dayname(t)        # Thursday
  ```

- **获取月份的信息**
  ```julia
  t = Date(2019,4,11)          # 2019-04-11
  m = Dates.month(t)           # 4
  me = Dates.monthname(t)      # April
  ```

- **获取年份和季节信息**
  ```julia
  t = Date(2019,4,11)          # 2019-04-11
  x1 = Dates.dayofyear(t)      # 101   (该日期为整年的第101天)
  x2 = Dates.isleapyear(t)     # false (该年不是闰年)
  x3 = Dates.quarterofyear(t)  # 2     (该日期在第2季度)
  ```

### 9-2、`DateTime()`函数
- **创建日期时间的方式**
  ```julia
  t = DateTime(2019,4,11,12,5,3,2)  # 2019-04-11T12:05:03.002
  ```

- **获取日期时间的信息**
  ```julia
  t = DateTime(2019,4,11,12,5,3,2)  # 2019-04-11T12:05:03.002
  y = Dates.year(t)                 # 2019
  m = Dates.month(t)                # 4
  d = Dates.day(t)                  # 11
  H = Dates.hour(t)                 # 12
  M = Dates.minute(t)               # 5
  S = Dates.second(t)               # 3
  MS = Dates.millisecond(t)         # 2
  ```

### 9-3、时间运算
- **`Date()`函数和`DateTime()`函数的运算**
  ```julia
  t = DateTime(2019,4,11,12,5,3,2)  # 2019-04-11T12:05:03.002
  t1 = t + Dates.Hour(2)            # 2019-04-11T14:05:03.002
  ```

### 9-4、时间序列
- **时间序列实例**
  ```julia
  Starttime = Date(2018,1,1)
  Endtime   = Date(2018,1,31)
  Timestep  = Dates.Day(1)
  d = collect(Starttime:Timestep:Endtime)
  ```







  
