# Go语言学习笔记

## 1. 变量

### 1.1 变量使用注意事项

1. 变量表示内存中的一个存储区域

2. 该区域有自己的名称（变量名）和类型（数据类型）

3. Golan变量使用的三种方式

   - 指定变量类型，声明后若不赋值，使用默认值
   - 根据值自行判断变量类型
   - 省略var，注意： =左边的变量不应该是已经声明过的，否则会导致编译错误

4. 多变量声明

   在编程中，有时我们需要一次性声明多个变量，`Golang` 也提供这样的语法

5. 该区域的数据值可以在同一 类型范围内不断变化

6. 变量在同一个作用域内不能重名

7. 注意：变量=变量名+值+数据类型

8. `Golang` 的变量如果没有赋初值，编译器会使用默认值

**一次声明多个变量的方式**

```go
// 方式1
var n1,n2,n3 int
fmt.Println("n1=",n1,"n2=",n2,"n3=",n3)
// 方式2
var n1,name,n3 = 100,"tom",888
fmt.Println("n1=",n1,"name=",name,"n3=",n3)
// 方式3
n1,name,n3 = 100, "tom" ,888
fmt.Println("n1=",n1,"name=",name,"n3=",n3)
```

### 1.2 变量的声明、初始化和赋值

#### 1.2.1 声明变量

​	**基本语法： var 变量名 数据类型**

​		`var a int` 这就是声明了一个变量，变量名是a

​		`var num1 float32` 这也声明了一个变量，表示一个单精度类型的小数，变量名 num1

#### 1.2.2 初始化变量

​		在声明变量的时候，就给值

​		`var a int = 45` 这就是初始化变量a

​		使用细节：如果声明时就直接赋值，可以省略数据类型

​		`var b = 400`

#### 1.2.3 给变量赋值

​		比如你先声明了变量：`var num int`

​		然后，再给值 `num = 780` 这就是给变量赋值

### 1.3  程序中+号的使用

 	1)  当左右两边都是数值型时，则做加法运算
 	2)  当左右两边都是字符串，则做字符串拼接

```go
package main
import "fmt"
func main() {
	var j = 1
	var i = 2
	var r = i + j
	fmt.Println("r=",r)

var str1 = "hud"
var str2 = " is "
var str3 = "handsome"
var str = str1 + str2 + str3
fmt.Println("str:",str)
}

#输出：
r= 3
str: hud is handsome
```

### 1.4 变量的数据类型

每一种数据都定义了明确的数据类型，在内存中分配了不同大小的内存空间

#### 1.4.1 基本数据类型

> 1. 数值型
>
>    - 整数类型（`int,int8,int16,int32,int64,uint,uint8,uint16,uint32,uint64,byte`）	
>
>    - 浮点型 （`float32，float64`）
>
> 2. 字符型（没有专门的字符型，使用byte来保存单个字母字符）
>
> 3. 布尔型（bool）
>
> 4. 字符串（string）

#### 1.4.2 派生/复杂数据类型

> 1. 指针（Pointer）
> 2. 数组
> 3. 结构体（struct）
> 4. 管道（Channel）
> 5. 函数
> 6. 切片（slice）
> 7. 接口（interface）
> 8. map

### 1.5 整数类型

#### 1.5.1 整数的使用细节

1. `Golang` 各整数类型分：**有符号**和**无符号**，int uint的大小和系统有关
2. `Golang`的整形默认声明为int型
3. 如何在程序查看某个变量的字节大小和数据类型
4. `Golang`程序中整型变量在使用时，遵守保小不保大的原则，即：在保证程序正确运行下，尽量使用空间小的数据类型
5. bit：计算机中最小的存储单位。byte：计算机中最基本存储单元

**这里介绍一下如何查看某个变量的数据类型和占用字节大小**

```go
// fmt.Prrintf() 可以用于做格式化的输出
var n1 = 100
fmt.Printf("n1的数据类型:%T\n" , n1)   //这里T代表type
fmt.Printf("n1的占用字节大小:%d" , unsafe.sizeof(n1)) 
输出：
n1的数据类型:int
n1的占用字节大小:8
```

整数：int    无符号整数：uint 

int型是计算最快的一种类型 整型的默认值为0 浮点型的默认值为0.0 

### 1.6 浮点类型

#### 1.6.1 基本介绍

​	浮点类型就是用来存放小数的，浮点类型的分类有：

| 类型            | 占用存储空间 | 表数范围                     |
| :-------------- | ------------ | ---------------------------- |
| 单精度`float32` | 4字节        | -`3.403E38` ~  `3.403E38`    |
| 双精度`float64` | 8字节        | - `1.798E308` ~  `1.798E308` |

**`float64`的精度比`float32`的要准确**

#### 1.6.2 浮点型使用细节

1. `Golang`浮点类型有固定的范围和字段长度，不受具体OS的影响
2. `Golang`的浮点型默认声明为`float64`类型
3. 浮点型常量有两种表示形式
   - 十进制数形式，例如：5.12   .512（必须有小数）
   - 科学计数法形式，例如：5.1234e2 = 5.12 * 10的2次方 5.12E-2 = 5.12/10的2次方
4. 通常情况下，应该使用`float64`，因为他比`float32`精确

### 1.7 字符类型

#### 1.7.1 基本介绍

​	`Golang`中没有专门的字符类型，如果要存储单个字符（字母），一般使用byte来保存

​	字符串就是一串固定长度的字符连接起来的字符序列，Go的字符串是由单个字节连接起来的，也就是说对于传统的字符串是由字符组成的，而go的字符串不同，它是由字节组成的。

#### 1.7.2 案例演示

​	**当我们直接输出byte值的时候，就是输出了对应字符的码值**

```go
	 var c1 byte = 'a'
	 fmt.Println(c1) 

输出：97
```

​	**所以需要使用格式化输出，输出对应的字符**

```go
	 var c1 byte = 'a'
	 fmt.Printf("%c",c1) 

输出：a
```

​	但是在存储一些特殊符号或者中文字符时，可能会出现溢出的情况，查看一下解决方法：

```go
 	 var c1 int = '齐'
	 fmt.Printf("%c\n",c1)
	 fmt.Printf("对应的码值是：%d",c1)  

输出：
齐
对应的码值是：40784
```

#### 1.7.3 字符类型的使用细节

1. 字符常量是用单引号（‘ ’）括起来的单个字符。例如：`var cl byte='a‘`    `var c2 int='中"` `var c3 byte=19`
2. Go中允许使用转义字符\’来将其后的字符转变为特殊字符型常量。例如：`var c3 char=‘\n'`    //   '\n'表示换行符
3. Go语言的字符使用UTF-8编码，如果想查询字符对应的utf8码值http://www.mytju.com/classcode/tools/encode_utf8.asp英文字母-1个字节汉字-3个字节
4. 在Go中，字符的本质是一个整数，直接输出时，是该字符对应的UTF-8编码的码值。
5. 可以直接给某个变量赋一个数字，然后按格式化输出时%c，会输出该数字对应的unicode字符

### 1.8 布尔类型

#### 1.8.1 基本介绍

1. 布尔类型又叫bool类型，bool类型的数据只允许取值true和false
2. bool类型变量占一个字节
3. boolean类型适用于逻辑运算，一般用于程序流程控制

#### 1.8.2 案例演示

```go
	var b = false
	fmt.Println("b:",b)
	fmt.Println("b占用字结为",unsafe.Sizeof(b))
	
输出：
b: false
b占用字结为 1
```

比较简单，这个没什么好说的，再来看个联合判断语句使用

```go
package main
import "fmt"

func main() {
	age := 18
	r := age>=18
	fmt.Printf("r= %v \n",r)
	if r{
		fmt.Println("你成年了")
	} else{
		fmt.Println("你是未成年")
	}
}

输出：
r:= true 
你成年了
```

### 1.9 字符串类型

#### 1.9.1 基本介绍

​	字符串就是一串固定长度的字符连接起来的字符序列。Go的字符串是由单个字节连接起来的，Go语言的字符串使用UTF-8编码标识unicode文本

#### 1.9.2 案例演示

```go
	var sen string = "Derrick Rose--MVP"
	fmt.Println(sen)
	
输出：
Derrick Rose--MVP
```

#### 1.9.3 注意事项和使用细节

1. Go语言的字符串的字节使用`UTF-8`编码标识Unicode文本，这样`Golang`统一使用`UTF-8`编码，乱码问题就不会再困扰程序员。

2. 字符串一旦被赋值了，就不能修改。在`Golang`中字符串是不可变的

3. 字符串的两种表示形式

   - 双引号，会识别转义字符
   - 反引号，以字符串的原生形式输出，包括换行和特殊字符，可以实现**防止攻击**、**输出源代码**等效果

   ```go
   	var str= `
   	    *
   	   ***
   	  *****  `
   	fmt.Println(str)
   
   输出：	  *
   	   ***
   	  *****
   ```

4. 字符串拼接方式

   ```go
   	var str= "hello world"+",and more..."
   	fmt.Println(str)
   	
   输出：
   hello world,and more...
   ```

5. 当一行字符串太长时，需要用到多行字符串，可以如下处理

   这里注意“+”一定要写在上面

   ```go
   	var str= "hello world"+
   	",and more..."
   	fmt.Println(str)
   	
   输出：
   hello world,and more...
   ```

### 1.10 基本数据类型的转换

#### 1.10.1 基本介绍

​	`Golang`和`java`/`c`不同，`Golang`在不同类型的变量之间赋值的时候需要显式赋值。也就是说`Golang`中的**数据类型不能自动转换**

#### 1.10.2 基本语法

​	表达式T(v)将值**v**转换为类型**T**

```
	var i int32 = 100
	var n1 float64 = float64(i)
	var n2 uint8 = uint8(i)
	var n3 int64 = int64(i)
	fmt.Printf("i(int32)=%v\nn1(float64)=%v\nn2(uint8)=%v\nn3(int64)=%v",i,n1,n2,n3)
	
输出：
i(int32)=100
n1(float64)=100
n2(uint8)=100
n3(int64)=100
```

#### 1.10.3 细节说明

1. `Golang`中的数据类型转换可以是从表示范围大**表示范围大**，也可以从**表示范围大**-->**表示范围小**
2. 被转换的是**变量存储的数据**（即值），变量本身的数据类型并没有变化
3. 在转换中，比如将`int64`转成`int8`【-128~127】，编译时候不会报错，只是转换的结果是按溢出处理

#### 1.10.4 基本数据类型和string的转换

​	在程序开发中，我们经常需要将基本数据类型转成string类型，或者将string类型转成基本数据类型

**基本类型转string类型**

##### 方式1：`fmt.Spritntf("%参数",表达式)`

1. 参数需要和表达式的数据类型相匹配

2. `fmt.Spritntf`会返回转换后的字符串（`Sprintf`根据format参数生成格式化的字符串并返回该字符串。）

3. 案例演示：

   ```go
   	var num1 int = 66
   	var num2 float64 = 3.141592653
   	var b bool = true
   	var mychar byte = 'q'
   	var str string //空的string
   	// 使用fmt.Sprintf()进行转换
   	str = fmt.Sprintf("%d",num1)
   	fmt.Printf("str type: %T str=%v\n",str,str)
   	
   	str = fmt.Sprintf("%f",num2)
   	fmt.Printf("str type: %T str=%v\n",str,str)
   	
   	str = fmt.Sprintf("%t",b)    // %t表示布尔值输出
   	fmt.Printf("str type: %T str=%v\n",str,str)
   
   	str = fmt.Sprintf("%c",mychar)
   	fmt.Printf("str type: %T str=%v\n",str,str)
   
   输出:
   str type: string str=66
   str type: string str=3.141593
   str type: string str=true
   str type: string str=q
   ```

##### 方式2：使用`strconv`包的函数

```go
	var num3 int64 = 66
	var str string
	str = strconv.FormatInt(num3,10)
	fmt.Printf("str type:%T str=%q\n",str,str)
输出：
str type:string str="66"
```

#### 1.10.5 string类型转基本数据类型

- 使用`strconv`包的函数

  > [func ParseBool(str string) (value bool, err error)](https://go-zh.org/pkg/strconv/#ParseBool)
  >
  > [func ParseFloat(s string, bitSize int) (f float64, err error)](https://go-zh.org/pkg/strconv/#ParseFloat)
  >
  > [func ParseInt(s string, base int, bitSize int) (i int64, err error)](https://go-zh.org/pkg/strconv/#ParseInt)
  >
  > [func ParseUint(s string, base int, bitSize int) (n uint64, err error)](https://go-zh.org/pkg/strconv/#ParseUint)

- 使用`strconv.Itoa()`函数

  ```go
  	var num5 int = 77
  	str = strconv.Itoa(num5)
  	fmt.Printf("str type:%T str=%q\n",str,str)
  	
  输出：
  str type:string str="77"
  ```


- 演示`Golang`中的string类型转为基本数据类型

```go
func main(){
	var str string = "true"
	var b bool
	b , _ = strconv.ParseBool(str)
	fmt.Printf("type: %T  %v",b,b) 

输出：
type: bool  true
```

这里做一个很简单说明，关于上面的 `b ,  _`

​		`strconv.ParseBool(str)`会返回两个值（`value bool,err error`）,因为只想接收到 `value bool`,不想获取`err`，所以使用“_”进行忽略。

##### func [ParseInt](https://github.com/golang/go/blob/master/src/strconv/atoi.go?name=release#150)

```go
func ParseInt(s string, base int, bitSize int) (i int64, err error)
```

> 返回字符串表示的整数值，接受正负号。
>
> base指定进制（2到36），如果base为0，则会从字符串前置判断，"`0x`"是16进制，"0"是8进制，否则是10进制；
>
> `bitSize`指定结果必须能无溢出赋值的整数类型，0、8、16、32、64 分别代表 `int`、`int8`、`int16`、`int32`、`int64`；返回的err是*`NumErr`类型的，如果语法有误，`err.Error` = `ErrSyntax`；如果结果超出类型范围`err.Error` = `ErrRange`。

```go
	var str2 string = "199866"
	var n1 int64
	n1 , _ =strconv.ParseInt(str2,10,0)
	fmt.Printf("type: %T  %v",n1,n1) 

输出：
type: int64  199866
```

#### 1.11 类型推导

我们在声明变量时候，可以根据初始化值进行类型推导，从而省略类型

```go
package main
func main(){
	var name = "Hud"
	var site = "www.pornhub.com"
    var age = 30
}
```

#### 1.12 一次性初始化多个变量

```go
package main
func main(){
	var name，site，age = "Hud" ，"www.pornhub.com"， 30
}
```

#### 1.13 短变量声明

**在函数内部可以使用`：=`运算符对变量进行声明和初始化**

```go
package main
func main(){
    name := "Hud"
    site := "www.pornhub.com"
    age := 30
}
```

> 注意：这种方法只适合在函数内部，函数外面不能使用

#### 1.14  匿名变量

​		如果我们接收到多个变量，有些变量使用不到，我们可以使用"_"进行接收，这个在前面的`PraseInt`里面已经演示过了，这种变量叫做匿名变量。

```go
	var str2 string = "199866"
	var n1 int64
	n1 , _ =strconv.ParseInt(str2,10,0)
	fmt.Printf("type: %T  %v",n1,n1) 

输出：
type: int64  199866
```

#### 1.15 以二进制、八进制或十六进制浮点数的格式定义数字

```go
package main
import "fmt"

func main() {
	// 十进制
	var a int = 10
	fmt.Printf("%d \n",a)  	//10
	fmt.Printf("%b \n",a)	//1010 表示二进制的10

	// 八进制 以0开头
	var b int = 077
	fmt.Printf("%o \n",b)	//77

	// 十六进制 以0x开头
	var c int = 0xff
	fmt.Printf("%x \n",c) 	//ff
	fmt.Printf("%X \n",c) 	//FF
}

输出结果：
10 
1010 
77 
ff 
FF 
```

> **二进制：%b**
>
> **八进制：%o**
>
> **十进制：%d**
>
> **十六进制：%x/%X**

## 2. 常量

​	常量，就是在**程序编译阶段**就确定下来的值，而程序在**运行时**则无法改变该值。在`Golang`中，常量可以是数值类型（包括整型、浮点型和复数类型）、布尔类型、字符串类型等。

### 2.1 定义常量的语法

​	定义一个常量使用`const`关键字，语法格式如下:

```go
const constantName [type] = value
```

`const`: 定义常量关键字

`constName`：常量名称

`type`：常量类型

`value`：常量的值

#### 实例

```go
package main

func main() {
	const PI float64 = 3.141592657
	const Pi = 3.1415	// 可以省略类型

	const(
		width = 100
		length = 200
	)
	
	const i , j = 1 , 2
	const a , b , c = 1 , 2 , "bro"
}
```

#### `iota`声明中间插队

​	`iota`也是一个常量，但是会被更改

```go
package main
import "fmt"
func main() {
	const(
		a1 = iota  //0
 		_	//1
		a2 = iota
		a3 = 10
		a4 = iota
	)

		fmt.Printf("a1: %v\n",a1)
		fmt.Printf("a2: %v\n",a2)
		fmt.Printf("a3: %v\n",a3)
		fmt.Printf("a4: %v\n",a4)
}

输出：
a1: 0
a2: 2
a3: 10
a4: 4
```

## 3. Golang`的格式化输出

**下面的实例使用到的结构体**

```go
type Website struct(
	Name string
)
// 定义结构变量
var site = Website{Name:"Hud9866"}
```

### 3.1 占位符

#### 3.1.1 普通占位符

| 占位符 | 说明                           | 输出                                    |
| ------ | ------------------------------ | --------------------------------------- |
| %v     | 相应值的默认格式               | `Printf("%v",site)  Printf("%+v",site)` |
| %#v    | 相应值的go语法表示             | `Printf("%#v",site)`                    |
| %T     | 相应值的类型的go语法表示       | `Printf("%T",site)`                     |
| %%     | 字面上的百分号，并非值的占位符 | `Printf("%%")`                          |

```go
package main
import "fmt"
type WebSite struct {
	Name string
}
func main() {
	site := WebSite{Name: "Hud9866"}
	fmt.Printf("site: %v\n",site)	
	fmt.Printf("site: %+v\n",site)
	fmt.Printf("site: %#v\n",site)	
	fmt.Printf("site(type): %T\n",site)	
}

输出：
site: {Hud9866}
site: {Name:Hud9866}
site: main.WebSite{Name:"Hud9866"}
site(type): main.WebSite
```

#### 3.1.2 布尔占位符

| 占位符 | 说明          | 举例输出            |
| ------ | ------------- | ------------------- |
| %t     | true或者false | `Printf("%t",true)` |

```go
package main
import "fmt"

func main() {
	b := false
	fmt.Printf("b:=%t\n",b)
	fmt.Printf("type of b:%T",b)
}

输出：
b:=false
type of b:bool
```

#### 3.1.2 整数占位符

| 占位符 | 说明                                       | 举例                | 输出   |
| ------ | ------------------------------------------ | ------------------- | ------ |
| %b     | 二进制表示                                 | Printf("%b",5)      | 101    |
| %c     | 相应Unicode码点所表示的字符                | Printf("%c",0x4E2D) | 中     |
| %d     | 十进制表示                                 | Printf("%d",0x12)   | 18     |
| %o     | 八进制表示                                 | Printf("%o",10)     | 12     |
| %q     | 单引号围绕的字符字面值，由Go语法安全的转义 | Printf("%q",0x4E2D) | '中'   |
| %x     | 十六进制表示，字母形式为小写a-f            | Printf("%x",13)     | d      |
| %X     | 十六进制表示，字母形式为小写A-F            | Printf("%X",13)     | D      |
| %U     | Unicode格式，U+1234，等同于"U+%04X"        | Printf("%U",0x4E2D) | U+4E2D |

```go
package main
import "fmt"
func main() {
	fmt.Printf("%d\n", 5)
	fmt.Printf("%c\n",0x4E2D)
	fmt.Printf("%d\n",0x12)
	fmt.Printf("%o\n",10)
	fmt.Printf("%q\n",0x4E2D)
	fmt.Printf("%x\n",13)
	fmt.Printf("%X\n",13)
	fmt.Printf("%U",0x4E2D)
}

输出：
5
中
18
12
'中'
d
D
U+4E2D
```

#### 3.1.3 浮点数和复数的组成部分（实部和虚部）

| 占位符 | 说明                                                         | 举例                 | 输出             |
| ------ | ------------------------------------------------------------ | -------------------- | :--------------- |
| %b     | 无小数部分的，指数为2 的幂的科学计数法，与`FormatFloat`的'b'转换格式一致 | `Printf("%b",3.14)`  | `7070671679p-51` |
| %e     | 科学计数法                                                   | `Printf("%e",1.2)`   | `1.200000e+00`   |
| %E     | 科学计数法                                                   | `Printf("%E",1.2)`   | `1.200000E+00`   |
| %f     | 有小数点而无指数                                             | `Printf("%f",1.234)` | `1.234000`       |
| %g     | 根据情况选择%e或者%f以产生更紧凑的(无末尾的0)输出            | `Printf("%g",1.23)`  | `1.23`           |
| %G     | 根据情况选择%E或者%f以产生更紧凑的(无末尾的0)输出            | `Printf("%G",1.23)`  | `1.23`           |

#### 3.1.4 字符串与字节切片

| 占位符 | 说明                                     | 举例                             | 输出           |
| ------ | ---------------------------------------- | -------------------------------- | -------------- |
| %s     | 输出字符串表示(string类型或者[]byte)     | `Printf("%s",[]byte("Hud9866"))` | `Hud9866`      |
| %q     | 双引号围绕的字符串，由`Golang`安全的转义 | `Printf("%q","齐天宇9866")`      | `"齐天宇9866"` |
| %x     | 十六进制，小写字母，每字节两个字符       | `Printf("%x","Hud")`             | `515459`       |
| %X     | 十六进制，大写字母，每字节两个字符       | `Printf("%X","Hud")`             | `515459`       |

#### 3.1.5 指针

| 占位符 | 说明                 | 举例                                       | 输出 |
| ------ | -------------------- | ------------------------------------------ | ---- |
| %p     | 十六进制表示前缀为0x | Printf("i: %p\n", p)`` | `i: 0xc0000180a8` |      |

```go
package main
import "fmt"
func main() {
	x := 100
	p :=&x
	fmt.Printf("i: %p\n", p)
}

输出：
i: 0xc0000180a8
```

## 4. `Golang`运算符

**Go语言内置的运算符有：**

1. 算数运算符
2. 关系运算符
3. 逻辑运算符
4. 位运算符
5. 赋值运算符

### 4.1 算数运算符

| 运算符 | 描述 |
| ------ | ---- |
| +      | 相加 |
| -      | 相减 |
| *      | 相乘 |
| /      | 相除 |
| %      | 求余 |

注意：`++`（自增）和`--`（自减）在`Golang`中是单独的语句，并不是运算符

**实例**

```goa + b=30
package main
import "fmt"
func main() {
	a := 10
	b := 20
		fmt.Printf("a + b=%v\n", a+b)
		fmt.Printf("a - b=%v\n", a-b)
		fmt.Printf("a * b=%v\n", a*b)
		fmt.Printf("a / b=%v\n", a/b)
		fmt.Printf("a %% b=%v\n", a%b)
	a++
	fmt.Printf("a:%v\n", a)
	b--
	fmt.Printf("b:%v\n", b)
}

输出：
a + b=30
a - b=-10
a * b=200
a / b=0
a % b=10
a:11
b:19
```

### 4.2 关系运算符

| 运算符 | 描述                                                        |
| ------ | ----------------------------------------------------------- |
| ==     | 检查两个值是否相等，如果相等返回True，否则返回False         |
| !=     | 检查两个值是否不相等，如果不相等返回True，否则返回False     |
| >      | 检查左边的值是否大于右值，如果是返回True，否则返回False     |
| >=     | 检查左边的值是否大于等于右值，如果是返回True，否则返回False |
| <      | 检查左边的值是否小于右值，如果是返回True，否则返回False     |
| <=     | 检查左边的值是否小于等于右值，如果是返回True，否则返回False |

**实例**

```go
package main
import "fmt"
func main() {
	
	a := 10
	b := 20
		fmt.Printf("a:=%v b:=%v\n", a,b)
		fmt.Printf("\n")
		fmt.Printf("a > b:  %v\n",a>b)
		fmt.Printf("a = b:  %v\n",a==b)
		fmt.Printf("a >= b: %v\n",a>=b)
		fmt.Printf("a != b: %v\n",a!=b)
		fmt.Printf("a < b:  %v\n",a<b)
		fmt.Printf("a <= b: %v\n",a<=b)
}

输出：
a:=10 b:=20

a > b:  false
a = b:  false
a >= b: false
a != b: true
a < b:  true
a <= b: true
```

### 4.3 逻辑运算符

| 运算符 | 描述                                                         |
| ------ | ------------------------------------------------------------ |
| &&     | 逻辑AND运算符，如果两边的操作数都为True则为True，否则为False |
| \|\|   | 逻辑OR运算符，如果两边的操作数有一个为True则为True，否则为False |
| !      | 逻辑NOT运算符，如果条件为True，则为False，否则为True         |

**实例**

```go
package main
import "fmt"
func main() {
	a := true
	b := false
		fmt.Printf("a := %v  b := %v\n", a,b)
		fmt.Printf("a && b : %v\n", (a&&b))
		fmt.Printf("a || b : %v\n", (a||b))
		fmt.Printf("  !a   : %v\n", (!a))
		fmt.Printf("  !b   : %v\n", (!b))
}

输出：
a := true  b := false
a && b : false
a || b : true
  !a   : false
  !b   : true
```

### 4.4 位运算符

| 运算符 | 描述                                                         |
| ------ | ------------------------------------------------------------ |
| &      | 参与运算的两数各对应二进位相与（两位均为1才为1）             |
| \|     | 参与运算的两数各对应二进位相或（两位有一个为1则为1）         |
| ^      | 参与运算的两数各对应二进位相异或（两位不一样则为1）          |
| <<     | 左移n位就是乘以2的n次方，"a<<b"就是把a的各二进制位全部左移b位，高位丢弃，低位补0 |
| >>     | 右移n位就是除以2的n次方，"a>>b"就是 把a的二进制位全部右移b位 |

**实例**

```go
package main
import "fmt"
func main() {
	a := 5	//0101
	fmt.Printf("a: %b	 ", a)
	b := 10	//1010
	fmt.Printf("b: %b\n", b)
		fmt.Printf("(a  &  b) : %v %b\n ", (a&b),(a|b))
		fmt.Printf("(a  |  b) : %v %b\n ", (a|b),(a|b))
		fmt.Printf("(a  ^  b) : %v %b\n ", (a^b),(a^b))
		fmt.Printf("(a  >> 2) : %v %b\n ", (a>>b),(a>>b))
		fmt.Printf("(a  << b) : %v %b\n ", (a<<b),(a<<b))
}

输出：
a: 101  	b: 1010
(a  &  b) : 0 1111
 (a  |  b) : 15 1111
 (a  ^  b) : 15 1111
 (a  >> b) : 0 0
 (a  << b) : 5120 1010000000000
```



### 4.5 赋值运算符

| 运算符 | 描述                                       |
| ------ | ------------------------------------------ |
| =      | 简单运算符，将一个表达式的值赋值给一个左值 |
| +=     | 相加之后再赋值                             |
| -=     | 相减之后再赋值                             |
| *=     | 相乘之后再赋值                             |
| /=     | 相除之后再赋值                             |
| %=     | 求余之后再赋值                             |
| <<=    | 左移之后再赋值                             |
| >>=    | 右移之后再赋值                             |
| &=     | 按位与后再赋值                             |
| \|=    | 按位或后再赋值                             |
| ^=     | 按位异或后再赋值                           |

**实例**

```go
package main
import "fmt"
func main() {
	var a int = 100
	fmt.Printf("a := %v\n", a)
	a += 1
	fmt.Printf("a+=1,a:=%v\n", a)
	a -= 1
	fmt.Printf("a-=1,a:=%v\n", a)
	a *= 2
	fmt.Printf("a*=2,a:=%v\n", a)
	a /= 2
	fmt.Printf("a/=2,a:=%v\n", a)
}

输出：
a := 100
a+=1,a:=101
a-=1,a:=100
a*=2,a:=200
a/=2,a:=100
```



## 5. `Golang`语言中的流程控制



### 5.1 go语言中的条件

------

​	**条件语句**是用来判断给定的条件是否满足，并根据判断的结果决定执行的语句。



### 5.2 go语言中的条件语句包含如下几种情况

------

1. **if语句**：`if`语句由一个布尔表达式后紧跟一个或多个语句组成。
2. **if…else语句**：`if`语句后可以使用可选的`else`语句，`else`语句中的表达式在布尔表达式值为`False`时执行。
3. **if嵌套语句**：你可以在`if`或`else if`语句中嵌入一个`if`或者多个`else if`语句
4. **switch语句**：`switch`语句用于基于你不同条件执行不同动作
5. **select语句：**`select`语句类似于`switch`语句，但是`select`会随机执行一个可运行的`case`，如果没有`case`可运行，他将会阻塞，直到有`case`可以运行。



### 5.3 go语言中的循环语句

------

go语言中的循环只有**for循环**，去除了`while`、`do while`循环，使用起来更加简洁

1. `for`循环
2. `for range`循环



### 5.4 go语言中的流程控制关键字

------

1. `break`
2. `continue`
3. `goto`



## 6. 流程控制实例

### 6.1 `golang`中的if语句

```go
if 布尔表达式{
    /* 布尔表达式为true时执行 */
}
```

#### **if语句实例演示**

```go
package main
import "fmt"
func test1(){
	var flag = true
	if flag {
		fmt.Println("flag is true\n")
	}
	fmt.Println("程序运行结束")
}

func main() {
	test1()
}

运行结果:
flag is true

程序运行结束
```

**根据年龄判断是否成年**

```go
package main
import "fmt"
func test2(){
	var age = 20
	if age >= 18{
		fmt.Println("你成年了")
	}
	fmt.Println("程序运行结束")
}

func main(){
	test2()
}

运行结果：
你成年了
程序运行结束
```

**初始变量可以声明在布尔表达式里面，注意它的作用域**

```go
package main
import "fmt"
func test3(){
	if age := 20 ; age >= 18 {
		fmt.Println("你是成年人~")
		}
	fmt.Println("程序运行结束")
}
func main() {
	test3()
}

运行结果：
你是成年人~
程序运行结束
```

**Go语言if语句使用提示**

1. 不需要使用括号将**条件包含起来**
2. 大括号{}必须存在，即使只有一行语句
3. 左括号必须在`if` 或者`else` 的同一行
4. 在`if`之后，条件语句之前，可以添加变量初始化语句，使用`;`进行分隔

### 6.2 `golang`中的if else语句

go语言中的if else语句可以**根据给定条件二选一**

```go
if 布尔表达式{
	// 在布尔表达式为True时执行
}else{
	// 在布尔表达式为false时执行
}
```

#### **go语言if else实例**

**比较两个数的大小**

```go
package main
import "fmt"

func f1() {
	a := 1
	b := 2
	if a > b {
		fmt.Printf("\"a>b\": %v\n","a>b")
	} else {
		fmt.Printf("\"a<=b\" : %v\n","a<b")
	}
}
func main() {
	f1()
}

运行结果：
"a<=b" : a<b
```

**判断一个数是奇数还是偶数**

```go
package main
import "fmt"
func f2(){
	var s int 
	fmt.Println("请输入一个数字：")
	fmt.Scan(&s)

	if s%2 == 0{
		fmt.Println("这是一个偶数")
	} else {
		fmt.Println("这是一个奇数")
	}
}
func main() {
	f2()
}

输出：
请输入一个数字：
7
这是一个奇数
```

### 6.3  `golang`中的if else if 语句

go语言if语句可以进行多重嵌套使用，进行多重判断

**go语言中的if else if语法**

```go
if 布尔表达式1 {
	// do something
} else if 布尔表达式2 {
	// do something
} else {
  // catch-all or default
}
```

#### **go语言中的if else if语法实例**

**根据分数判断等级**

```go
func f5(){
	fmt.Println("Enter your score")
	var score int
	fmt.Scan(&score)
	if score >=60 && score <= 70{
		fmt.Printf("your score is %v level: C\n",score)
	} else if score > 70 && score <=90{
		fmt.Printf("your score is %v level: B\n",score)
	} else {
		fmt.Printf("your score is %v level: A\n",score)
	}
}
func main() {
	f5()
}

输出：
Enter your score
80
your score is 80 level: B
```

**输入星期几的第一个字母来判断是星期几，如果第一个字母一样，判断第二个字母**

```go
package main
import "fmt"
func f6() {
	// Monday Tuesday Wednesday Thursday Friday Saturday Sunday
	var c string
	fmt.Println("请输入一个字符：")
	fmt.Scan(&c)

	if c == "S" {
		fmt.Println("输入第二个字符")
		fmt.Scan(&c)
		if c == "a" {
		fmt.Println("Saturday")	
		}else if c == "u" {
			fmt.Println("Sunday")
		}else {
			fmt.Println("输入有误")
		}
	} else if c == "F"{
		fmt.Println("Friday")
	} else if c == "M"{
		fmt.Println("Monday")
	} else if c == "T" {
		fmt.Println("输入第二个字符：")
		fmt.Scan(&c)
		if c == "u" {
			fmt.Println("Tuesday")
		}else if c == "h"{
			fmt.Println("Thursday")
		}else {
			fmt.Println("输入错误")
		} 
	} else if c == "W" {
		fmt.Println("Wednesday")
	}else {
		fmt.Println("输入错误")
	}
}
func main() {
	f6()
}

输出：
请输入一个字符：
T
输入第二个字符：
h
Thursday
请输入一个字符：
F
Friday
```

### 6.4  `golang`中嵌套if语句

go语言if语句可以嵌套多级进行判断

**go语言if嵌套语法**

```go
if 布尔表达式1 {
	//在布尔表达式1为true时执行
if 布尔表达式2 {
  // 布尔表达式2为true时执行
  }
}
```

#### **go语言if嵌套实例**

**判断三个数字的大小** 

```go
package main
import "fmt"
func f1(){
	var a,b,c int
	fmt.Println("请输入三个个数字：")
	fmt.Scan(&a,&b,&c)
	if a>b {
		if a>c{
			fmt.Printf("max:%v", a)
		}
	}else {
		if b > c{
			fmt.Printf("max:%v", b)
		}else{
			fmt.Printf("max:%v", c)
		}
	}
}	
func main() {
	f1()
}

输出：
请输入三个个数字：
9 8 6
max:9
```

**判断是男生还是女生，以及是否成年**

```go
func main() {
	f2()
}
func f2(){
	var gender string 
	var age int
	fmt.Println("请输入你的性别：")
	fmt.Scan(&gender)
	fmt.Println("请输入你的年龄：")
	fmt.Scan(&age)
	if gender == "男" {
		if age >= 18 {
			fmt.Println("你是一个成年的男性")
		}else {
			fmt.Println("你是一个还没成年的小男孩")
		}
	}else {
		if age >= 18 {
			fmt.Println("你是个成年女人")
		}else {
			fmt.Println("你还是个没成年的小女孩")
		}
	}
}

输出：
请输入你的性别：
男
请输入你的年龄：
24
你是一个成年的男性
请输入你的性别：
女
请输入你的年龄：
3
你还是个没成年的小女孩
```

### 6.5 `golang`中的switch语句

go语言中的switch语句，可以非常容易的判断多个值的情况。

**go语言中的switch语句语法**

```go
switch var1 {
	case val1:
	 ...
	 case val2 :
	 ...
	 default
}
```

#### go语言中switch语句实例

**判断成绩**

```go
package main
import "fmt"
func main() {
	f1()
}
func f1() {
	var a string
	fmt.Println("输入等级")
	fmt.Scan(&a)
	switch a {
	case "A" :
		fmt.Println("优秀")
	case "B" :
		fmt.Println("良好")
	case "C" :
		fmt.Println("中等")
	case "D" :
		fmt.Println("及格")
	default  :
		fmt.Println("不及格")
	}
}

输出：
输入等级
A
优秀
输入等级
D
及格
```

**case也可以是条件表达式**

```go
func f3() {
	var score int
	fmt.Println("输入你的成绩：")
	fmt.Scan(&score)
	switch {
	case score >= 90:
		fmt.Println("成绩很棒")
	case score < 90 && score >= 80:
		fmt.Println("还需努力学习")
	default:
		fmt.Println("别学了 你已经废了")
	}
}

输出：
输入你的成绩：
89
还需努力学习
输入你的成绩：
99
成绩很棒
输入你的成绩：
45
别学了 你已经废了
```

**`fallthrough`可以执行满足条件下的一个`case`**

```go
func f4() {
	a :=100
	switch a{
	case 100:
		fmt.Println("100")
		fallthrough
	case 200:
		fmt.Println("200")
	case 300:
		fmt.Println("300")
	default:
		fmt.Println("other")
	}
}

输出：
100
200
```

#### Go语言中`switch`语句的注意事项：

1. 支持多条件匹配
2. 不同的`case`之间不使用`break`分隔，默认只会执行一个case
3. 如果想要执行多个`case`，需要使用`fallthrough`关键字，也可用`break`终止
4. 分支还可以使用表达式，例如：`a<10` 

## 7. `Golang`中的for循环

go语言中的`for`循环，只有`for`关键字，去除了像其他语言中的`while`和`do while`

**go语言for循环语法**

```go
for 初始语句;条件表达式;结束语句 {
		循环体语句
}
```

**注意：for表达式不用加括号**

#### go语言for循环实例

**循环从1输出到10**

```go
package main
import "fmt"

func main() {
	f1()
	fmt.Println("")
	f2()
}

func f1() {
	for i := 1; i <= 10 ; i++ {
		fmt.Printf("%v", i)
	} 
}

func f2() {
	i := 1
	for  i <= 11 {
		fmt.Printf("%v", i)
		i++
	} 
} 

输出：
12345678910
1234567891011
```

> 上面实例中的`f2()`说明：初始条件和这个结束条件都可以省略（写在别的地方）

**永真循环：一直执行**

```go
package main
import "fmt"
func main() {
	f3()
}
func f3() {
	for {
		fmt.Println("我在一直执行！")
	}
}

输出：
我在一直执行！
我在一直执行！
我在一直执行！
...
```

## 8. `Golang`的for range循环

go语言中可以使用`for range`遍历数组、切片、字符串、map及通道（channel）。通过`for range`遍历的返回值有以下的规律：

1. 数组、切片、字符串返回**索引和值**
1. map返回值和键
1. 通道(channel)只返回通道内的值

#### **go语言`for range`实例**

**循环数组**

```go
package main
import "fmt"
func main() {
	f1()
}
func f1() {
	var a = [5]int{1,2,3,4,5}
	for i , v := range a{
			fmt.Printf("i: %d , v: %v\n", i,v)
		}
}

输出：
i: 0 , v: 1
i: 1 , v: 2
i: 2 , v: 3
i: 3 , v: 4
i: 4 , v: 5
```

```go
package main
import "fmt"
func main() {
	f2()
}
func f2(){
	var s = []int{1,2,3,4,5,6}	//声明切片
	for _, v := range s {
		fmt.Printf("v: %v\n", v)
	}
}

输出：
v: 1
v: 2
v: 3
v: 4
v: 5
v: 6
```

```go
func f3(){
	//key : value
	var m = make(map[string]string,0)	//创建map
	m["name"] = "Hud"
	m["age"] = "24"
	m["e-mail"] = "qitianyu2007@126.com"
	for key , value := range m {
		fmt.Printf("%v : %v\n ", key,value)
	}
}

输出：
name : Hud
age : 24
e-mail : qitianyu2007@126.com
```

## 9.  `golang`流程控制关键字

### 9.1 break

`break`语句可以结束`for`、`switch`和`select`的代码块

#### go语言使用break注意事项

1. 单独在`select`中使用`break`和不使用`break`没什么区别。
2. 单独在表达式`switch`语句，并且没有`fallthrough`，使用`break`和不使用`break`没什么区别。
3. 单独在表达式`switch`语句，并且有`fallthrough`，使用`break`能够终止`fallthough`后面的case语句的执行
4. 带标签的`break`，可以跳出多层`switch/select`作用域，让`break`更加灵活，写法更加简单灵活，不需要使用控制变量一层一层跳出循环，没有带`break`的总股本发跳出当前语句块

#### go语言break关键字实例

**跳出for循环**

```go
func f4(){
	for i := 0;i <= 5; i++{
		
		fmt.Printf("%v\n", i)
		if i==5{
			break
		}
	}
}

输出：
0
1
2
3
4
5
```

**跳出switch循环**

```
func f5(){
	i := 2
	switch i {
	case 1:
		fmt.Println("等于1")
		break
	case 2:
		fmt.Println("等于2")
		break
		fallthrough
	case 3:
		fmt.Println("等于3")
		break
	default:
		fmt.Println("不关心")
		break
		
	}
}

输出：
等于2
```

如果注释掉`fallthrough`上面的`break`，运行结果:

```go
等于2
等于3
```

**跳转至标签处**

```go
func f6(){
My_Label:
	for i:=0;i<=10;i++{
		if i==5{
			break My_Label
		}
		fmt.Printf("%v\n",i)
	}
	fmt.Println("end...")
}

输出：
0
1
2
3
4
end...
```

### 9.2 goto

`goto`语句通过标签进行代码间的**无条件跳转**，`goto`语句可以在快速跳出循环、避免重复退出上有一定的帮助。Go语言中使用`goto`语句能简化一些代码的实现过程，例如双层嵌套的`for`循环要退出时：

**go语言关键字`goto`实例**

```go
func f2(){
	
	a := 0
if a ==1 {
	goto Label1
}else{
		fmt.Println("other")
	}
Label1:
	fmt.Println("this is label of goto")
}

输出：

```



## 10. `golang`关键字`continue`

`continue`只能用在循环当中，在go中只能用在`for`循环中，他可以终止本次循环，执行下一次循环

在`continue`语句后面添加标签时，表示开始标签对应的循环

**输出偶数**

```go
package main
import "fmt"
func main() {
	for i := 0; i < 10; i++ {
		if i%2==0{
			fmt.Printf("%v\n", i)
		}else{
			continue
		}
	}
}

输出：
0
2
4
6
8
```

## 11. `golang`数组

数组是相同**数据类型的**一组数据的集合，数组一旦定义长度不能修改，数组可以通过**下标**（或者叫**索引**）来访问元素。

**go语言数组的定义**

数组的定义语法：

```go
var variable_name [Size] variable_type
```

- `variable_name`:数组名称
- `Size`：数组长度，必须是常量
- `variable_type`：数组保存元素的类型

**实例**

```go
package main
import "fmt"
func main() {
	var a1 [2]int
	var a2 [5]string
	fmt.Printf("a1: %T\n", a1)
	fmt.Printf("a2: %T\n", a2)
	fmt.Printf("a1: %v\n", a1)
	fmt.Printf("a2: %v\n", a2)
}

输出：
a1: [2]int
a2: [5]string
a1: [0 0]
a2: [    ]
```

**go语言数组的初始化**

初始化，就是给数组元素赋值，没有初始化的数组，**默认元素值都是零值**，布尔类型是`false`，字符串类型是空字符串

```go
func f2()  {
	var a1 = [3]int{1,2}	//int类型 只定义两个值
	fmt.Printf("a1: %v", a1)
	var a2 = [2]string{"hello"} //字符串类型 定义一个值
	fmt.Printf("a2: %v", a2)
    var a3 = [2]bool{true}	//布尔类型变量
	fmt.Printf("a3: %v", a3)
}

输出：
a1: [1 2 0]a2: [hello ]a3: [true false]
```

**省略数组长度**

数组长度可以省略，使用`...`代替

```go
func f3()  {
	var a = [...]int{1,2,3}
	var s = [...]string{"hello","world"}
	var b = [...]bool{false,true}

	a1 := [...]int{1,2}

	fmt.Printf("a: %v\n", a)
	fmt.Printf("s: %v\n", s)
	fmt.Printf("b: %v\n", b)
	fmt.Printf("a1: %v\n", a1)
}

输出：
a: [1 2 3]
s: [hello world]
b: [false true]
a1: [1 2]
```

 **打印数组长度**

```go
func f4()  {
	var a = [3]int{1,2,3}
	fmt.Printf("length: %v", len(a))
}

输出：
length: 3
```

**根据数组长度遍历数组**

可以根据数组的长度，通过`for`循环的方式来遍历数组，数组的长度可以使用`len`函数获得

```go
func f5()  {
	var a = [5]int{1,2,3,4,5}
	for i := 0; i<len(a); i++ {
		fmt.Printf("%v\n", a[i])
	}

for _, v := range a {			//用for range遍历数组
	fmt.Printf("v:%v\n",v)
}
}

输出：
1
2
3
4
5
v:1
v:2
v:3
v:4
v:5
```

### 11.1 数组的应用

#### 11.1.1 冒泡排序

```go
// 改进的冒泡排序算法
func AdvBubbleSort(a []int) []int {
	flag := false
	for i := len(a) - 1; i > 0; i-- {
		for j := 0; j < i; j++ {
			flag = false
			if a[j] > a[j+1] {
				a[j], a[j+1] = a[j+1], a[j]
				flag = true
			}
		}
		if !flag {
			break
		}
	}
	return a
}
func main() {
	a := []int{1, 3, 2, 9, 4}
	fmt.Printf("AdvBubbleSort(a): %v\n", AdvBubbleSort(a))
}

输出：
AdvBubbleSort(a): [1 2 3 4 9]
```

#### 11.1.2 快速排序

```go
package main

import "fmt"

func quickSort(a []int, left, right int) {
	if left < right {
		loc := partition(a, left, right)
		quickSort(a, left, loc-1)
		quickSort(a, loc+1, right)
	}
}

func partition(a []int, left, right int) int {
	i := left + 1
	j := right
	for i < j {
		if a[i] > a[left] {
			a[i], a[j] = a[j], a[i]
			j--
		} else {
			i++
		}
	}
	if a[i] >= a[left] {
		i--
	}

	a[i], a[left] = a[left], a[i]
	return i
}

func main() {
	arr := []int{6, 8, 3, 9, 4, 5, 7}
	quickSort(arr, 0, len(arr)-1)
	fmt.Printf("arr: %v\n", arr)
}

输出：
arr: [3 4 5 6 7 8 9]
```



### 11.2 go语言list

​	列表是一种非连续的存储容器，由多个节点组成，节点通过一些变量记录彼此之间的关系，列表有多种实现方法，如单链表、双链表等。

​	在Go语言中，列表使用 container/list 包来实现，内部的实现原理是双链表，列表能够高效地进行任意位置的元素插入和删除操作。

- #### 初始化列表

  list 的初始化有两种方法：分别是使用 New() 函数和 var 关键字声明，两种方法的初始化效果都是一致的。

  1) **通过 container/list 包的 New() 函数初始化 list**

  ```go
  变量名 := list.New()
  ```

  ​	2.**通过 var 关键字声明初始化 list**

  ```go
  var 变量名 list.List
  ```

  列表与切片和 map 不同的是，列表并没有具体元素类型的限制，因此，列表的元素可以是任意类型，这既带来了便利，也引来一些问题，例如给列表中放入了一个 interface{} 类型的值，取出值后，如果要将 interface{} 转换为其他类型将会发生宕机。

  

- #### 在列表中插入元素

  双链表支持从队列前方或后方插入元素，分别对应的方法是 **`PushFront`** 和 **`PushBack`**。

  #### 提示

  这两个方法都会返回一个 **`*list.Element`** 结构，如果在以后的使用中需要删除插入的元素，则只能通过 **`*list.Element`** 配合 **`Remove()`** 方法进行删除，这种方法可以让删除更加效率化，同时也是双链表特性之一。

  下面代码展示如何给 list 添加元素：

  ```go
  l := list.New()
  
  l.PushBack("fist")
  l.PushFront(67)
  ```

  列表插入元素的方法如下表所示。

  | 方  法                                                | 功  能                                            |
  | ----------------------------------------------------- | ------------------------------------------------- |
  | InsertAfter(v interface {}, mark * Element) * Element | 在 mark 点之后插入元素，mark 点由其他插入函数提供 |
  | InsertBefore(v interface {}, mark * Element) *Element | 在 mark 点之前插入元素，mark 点由其他插入函数提供 |
  | PushBackList(other *List)                             | 添加 other 列表元素到尾部                         |
  | PushFrontList(other *List)                            | 添加 other 列表元素到头部                         |

  

- #### 从列表中删除元素

  列表插入函数的返回值会提供一个 **`*list.Element`** 结构，这个结构记录着列表元素的值以及与其他节点之间的关系等信息，从列表中删除元素时，需要用到这个结构进行快速删除。

  ```go
  package main
  import "container/list"
  func main() {
      l := list.New()
      // 尾部添加
      l.PushBack("canon")
      // 头部添加
      l.PushFront(67)
      // 尾部添加后保存元素句柄
      element := l.PushBack("fist")
      // 在fist之后添加high
      l.InsertAfter("high", element)
      // 在fist之前添加noon
      l.InsertBefore("noon", element)
      // 使用
      l.Remove(element)
  }
  ```

  | 操作内容                        | 列表元素                    |
  | ------------------------------- | --------------------------- |
  | l.PushBack("canon")             | canon                       |
  | l.PushFront(67)                 | 67, canon                   |
  | element := l.PushBack("fist")   | 67, canon, fist             |
  | l.InsertAfter("high", element)  | 67, canon, fist, high       |
  | l.InsertBefore("noon", element) | 67, canon, noon, fist, high |
  | l.Remove(element)               | 67, canon, noon, high       |



- #### 遍历列表——访问列表的每一个元素

  遍历双链表需要配合 Front() 函数获取头元素，遍历时只要元素不为空就可以继续进行，每一次遍历都会调用元素的 Next() 函数，代码如下所示。

  ```go
  package main
  
  import (
  	"container/list"
  	"fmt"
  )
  
  func main() {
  	// var a list.List
  	b := list.New()
  	b.PushBack("a")
  	b.PushFront(3)
  
  	//遍历链表
  	for i:=b.Front();i!=nil;i = i.Next(){
  		fmt.Println(i.Value)
  	}
  }
  
  输出：
  3
  a
  ```

  

## 12. `Golang`切片

前面学习了数组，数组是固定长度，可以容纳相同数据类型的元素的集合。当长度固定时，使用还是带来一些限制。例如：我们申请的长度太大浪费内存，太小又不够用。

鉴于上述的原因，我们有了go语言的切片，可以把切片理解为：可变长度的数组，其实他的底层就是使用数组实现的，增加了自动扩容功能。切片（Slice）是一个拥有相同类型元素的可变长度的序列。

### 12.1 Go语言切片的语法

声明一个切片和声明一个数组类似，只要不添加长度就可以了。

```go
var identifier []type
```

切片是引用类型，可以使用`make`函数来创建切片

```go
var slice []type = make([]type,len)
//可以简写为
slice1 := make([]type,len)
```

也可以指定容量，其中capicity为可选参数。

```go
make([]T,length,capicity)
```

其中 Type 是指切片的元素类型，length指的是为这个类型分配多少个元素，capicity为预分配的元素数量，这个值设定后不影响 length，只是能提前分配空间，降低多次分配空间造成的性能问题。

#### 三种创建方式

- **方式一**
  **对已经创建好的数组进行引用：**

```go
package main

import "fmt"

func main() {
	// 方式一
	arr := [5]int{1, 2, 3, 4, 5}
	slice := arr[:3]
	fmt.Printf("slice: %v\n", slice)
}
```

- **方式二**

​		**使用内置函数make进行创建**

```go
package main

import "fmt"

func main() {
	slice := make([]int, 5, 10)
	for i := 0; i < 5; i++ {
		slice[i] = i + 1
	}
	fmt.Printf("slice: %v\n", slice)
}

输出：
slice: [1 2 3 4 5]
```

- **方式三**

​		**定义一个切片，直接就指定具体数组，使用原理和`make`类似**

```go
package main

import "fmt"

func main() {
	var slice []int = []int{1, 2, 3, 4, 5}
	fmt.Printf("slice: %v\n", slice)
}

输出：
slice: [1 2 3 4 5]
```

**切片作为引用类型，会改变原有的数组，其中切片指向对应数组所在的地址：**

```go
package main

import "fmt"

func main() {
	s := []int{1, 2, 3, 4}
	fmt.Printf("s: %v\n", s)
	slice := s[:3]
	fmt.Println(&s[0])			// 打印s的第一个元素地址
	fmt.Println(&slice[0])		// 打印slice切片第一个元素地址，是引用的数组s
	slice[1] = 9
	fmt.Printf("slice: %v\n", slice)
	fmt.Printf("s: %v\n", s)	// 原数组相应位置的值也发生了改变
}

输出：
s: [1 2 3 4]
0xc00000c1e0
0xc00000c1e0
slice: [1 9 3]
s: [1 9 3 4]
```



### 12.2  Go语言切片实例

```go
package main
import "fmt"
func main() {
	var name []string
	var numbers []int
	fmt.Printf("names: %v\n", name)
	fmt.Printf("numbers: %v\n", numbers)
	fmt.Println(name == nil)
	fmt.Println(numbers == nil)
}

输出：
names: []
numbers: []
true
true
```

****

```go
func f2()  {
	var s1 = make([]int,2)
	fmt.Printf("s1: %v\n", s1)
}

输出：
s1: [0 0]
```

### 12.3 Go语言切片的长度和容量

切片拥有自己的长度和容量，我们可以使用内置的`len()`函数求长度，使用内置的`cap()`函数求切片的容量

```go
func f3()  {
	var name = []string{"Hud","Monica"}
	var numbers = []int {66,64}
	fmt.Printf("len: %d  cap:%d\n", len(name),cap(name))
	fmt.Printf("len: %d  cap:%d\n", len(numbers),cap(numbers))

	var s1 = make([]string,2,3)
	fmt.Printf("len: %d  cap:%d\n", len(s1),cap(s1))
}

输出：
len: 2  cap:2
len: 2  cap:2
len: 2  cap:3
```

### 12.4 Go语言切片的初始化

切片的初始化方法很多，可以直接初始化，也可以使用数组初始化等

**直接初始化**

```go
func f4()  {
	s := []int{1,2,3,4}
	fmt.Printf("s: %v", s)
}

输出：
s: [1 2 3 4]
```

**使用数组初始化**

```go
func f5()  {
	arr := [3]int{1,2,3}
	s1 := arr[:]
	fmt.Printf("s1: %v", s1)
}

输出：
s1: [1 2 3]
```

**使用数组部分元素进行初始化（切片表达式）**

切片的底层就是一个**数组**，所以我们可以**基于数组通过切片表达式得到切片**。切片表达式中的low和high表示一个索引范围（**左包含，右不包含**），得到的切片长度=high-low，容量等于得到的切片的底层数组的容量。

```go
func f6()  {
	arr := [...]int{1,2,3,4,5,6,7,8,9}
	s1 := arr[2:5]
	fmt.Printf("s1:%v\n", s1)
	s2 := arr[2:]
	fmt.Printf("s2:%v\n", s2)
	s3 := arr[:3]
	fmt.Printf("s3:%v\n", s3)
    s4 := arr[:]
	fmt.Printf("s4:%v\n", s4)
}

输出：
s1:[3 4 5]
s2:[3 4 5 6 7 8 9]
s3:[1 2 3]
s4:[1 2 3 4 5 6 7 8 9]
```

```go
func f7()  {
	var s1 = []int{1,2,3,4,5}
	l := len(s1)
	for i := 0; i < l; i++ {
		fmt.Printf("s1[%v] : %v\n", i,s1[i])
	}
}

输出：
s1[0] : 1
s1[1] : 2
s1[2] : 3
s1[3] : 4
s1[4] : 5
```

```go
func f8()  {
		var s1 = []int{8,9,10,11,12}
	for i, v := range s1 {
		fmt.Printf("i: %v\n", i)
		fmt.Printf("v: %v\n", v)
		
	}
}

输出：
i: 0
v: 8
i: 1
v: 9
i: 2
v: 10
i: 3
v: 11
i: 4
v: 12
```

### 12.5 Go语言切片元素的添加和删除

切片是一个动态数组，可以使用`append()`函数添加元素，`golang`中并没有删除切片元素的专用方法，我们可以使用切片本身的特性来删除元素，由于切片是引用类型，通过赋值的方式，会修改原有内容，`golang`提供了`copy()`函数来拷贝切片

**添加元素**

```go
func f9()  {
	s1 := []int{}
	s1 = append(s1,1)
	s1 = append(s1,2)
	s1 = append(s1,3)
	s1 = append(s1,3,4,5)
	fmt.Printf("s1: %v\n", s1)

	s3 := []int{3,4,5}
	s4 := []int{1,2}
	s4 = append(s4,s3...)
	fmt.Printf("s4: %v\n", s4)
}

输出：
s1: [1 2 3 3 4 5]
s4: [1 2 3 4 5]
```

**删除元素**

```go
//删除元素
func f10()  {
	s1 := []int{1,2,3,4,5}
	//删除索引为2的元素
	s1 = append(s1[:2],s1[3:]...)
	fmt.Printf("s1: %v", s1)
}

输出：
s1: [1 2 4 5]
```

公式：要从切片a中删除索引为`index`的元素，操作方法是

```go
a = append(a[:index],[index:]...)
```

**修改元素**

直接根据切片的索引，就可以修改相应的元素

```
func f11()  {
	s1 := []int{1,2,3,4,5}
	s1[2]=6
	fmt.Printf("s1: %v", s1)
}

输出：
s1: [1 2 6 4 5]
```

**元素查找**

```go
func f12()  {
	s1 := []int{1,2,3,4,5}
	var key = 2
	for i,v := range s1 {
		if v == key{
			fmt.Printf("s1[%v]: %v", i,v)
		}
	}
}

输出：
s1[1]: 2
```

## 13. `Golang` map

`map`是一种`key:value`键值对的数据结构容器，`map`内部实现是哈希表（`hash`）

`map`最重要的一点是通过`key`来快速检索数据，key类似于索引，指向数据的值

`map`是引用类型的

### 13.1 `map`的语法格式

可以使用内建函数`make()`也可以使用`map`关键字来定义`map`

```go
// 声明变量 默认map是nil
var map_variable map[key_data_type]value_data_type
// 使用make函数
map_variable = make(map[key_data_type]value_data_type)
```

`map_variable`：map变量名称

`key_data_type`：key的数据类型

`value_data_type`：值的数据类型

**实例**

声明一个保存个人信息的`map`

```go
package main
import "fmt"
func main() {
	m1 := make(map[string]string)
	m1["name"] = "Hud"
	m1["age"] = "24"
	m1["e-mail"] = "qitianyu2007@126.com"
	fmt.Printf("m1: %v\n", m1)

	m2 := map[string]string{
		"name" : "James",
		"age" : "37",
		"team" : "Lakers",
	}
	fmt.Printf("m2: %v", m2)
}

输出：
m1: map[age:24 e-mail:qitianyu2007@126.com name:Hud]
m2: map[age:37 name:James team:Lakers]
```

### 13.2 访问map

可以通过下标key获得其值，例如：

```go
func f2()  {
	m1 := make(map[string]string)
	m1["name"] = "Hud"
	m1["age"] = "24"
	m1["e-mail"] = "qitianyu2007@126.com"

	name :=m1["name"]
	age :=m1["age"]
	email :=m1["e-mail"]
	fmt.Printf("name: %v\n", name)
	fmt.Printf("age: %v\n", age)
	fmt.Printf("e-mail: %v\n", email)
}

输出:
name: Hud
age: 24
e-mail: qitianyu2007@126.com
```

### 13.2 判断某个键是否存在

go语言中有一个判断map中键是否存在的特殊写法，格式如下：

```go
value ,ok :=map[key]
```

如果`ok`为`true`，存在；否则，不存在。

**实例**

```go
func f3()  {
	m1 := map[string]string{
		"name" : "James",
		"age" : "37",
		"team" : "Lakers",
	}
	var k1 = "name"
	var k2 = "age1"
	v,ok := m1[k1]
	fmt.Printf("value: %v\n", v)
	fmt.Printf("ok: %v\n", ok)
	fmt.Println("------------")
	v,ok = m1[k2]
	fmt.Printf("value: %v\n", v)
	fmt.Printf("ok: %v\n", ok)
}

输出：
value: James
ok:true
------------
value:
ok: false
```

### 13.3 `golang`遍历map

可以使用`for range`循环进行map遍历，得到`key`和`value`值

**遍历key**

```go
func f4()  {
	m1 := map[string]string{
		"name" : "James",
		"age" : "37",
		"team" : "Lakers",
	}
	for key := range m1{
		fmt.Printf("%v\n", key)		
	}
}

输出：
name
age
team
```

**遍历key&value**

```go
func f5(){
	m1 := make(map[string]string)
	m1["name"] = "Hud"
	m1["age"] = "24"
	m1["e-mail"] = "qitianyu2007@126.com"
	
	for key , value := range m1 {
		fmt.Println(key + ":" + value)
	}
}

输出：
age:24
e-mail:qitianyu2007@126.com
name:Hud
```

### 13.4 map切片的使用

切片的数据类型如果是`map`，则成为`map`切片，这样使用则map个数就可以动态变化了。

## 14. `Golang`函数

### 14.1 `golang`函数简介

函数是`golang`中的**一级公民**，我们把所有的功能单元都定义在函数中，可以重复使用。函数包含函数的名称、参数列表和返回值类型，这些构成了函数的签名(signature)。

**go语言中函数的特性**

1. go语言中有三种函数：普通函数、匿名函数（没有名称的函数）、方法（定义在struct上的函数）
2. go语言中不允许函数重载（overload），也就是说不允许函数同名
3. go语言中的函数不能嵌套函数，但是可以嵌套匿名函数
4. 函数是一个值，可以将函数赋值给变量，使得这个变量也成为函数
5. 函数可以作为参数传递给另一个函数
6. 函数的返回值可以是一个函数
7. 函数调用的时候，如果有参数传递给函数，则先拷贝参数的副本，再将副本传递给参数
8. 函数参数可以没有名称

**go语言中函数的定义和调用**

函数在使用之前必须先定义，可以调用函数来完成某个任务。函数可以重复调用，从而达到代码重用。

**go语言函数定义语法**

```go
func function_name([parameter list])[return_types]{
    //函数体
}
```

语法解析：

- `func`：函数由`func`开始声明
- `function_name`：函数名称，函数名称和参数列表一起构成了函数签名
- `[parameter list]`：参数列表，参数就像一个占位符，当函数被调用时，你可以将值传递给参数，这个值被称为实际参数。参数列表指定的是参数类型、顺序以及参数的个数。参数是可选的，也就是说函数也可以不包含参数。
- `[return_types]`：返回类型，函数返回一列值，`[return_types]`是该值的数据类型。有些功能不需要返回值，在这种情况下，`[return_types]`就不是必须的
- 函数体：函数定义的代码合集

### 14.2 go语言函数定义实例

**定义一个求和函数**

```go
package main
import "fmt"
func main() {
	var a int
	a = sum(2,3)
	fmt.Printf("a: %v", a)
}
func sum(a int,b int) (sum int) {
	sum = a + b
	return sum
}

输出：
a: 5
```

**定义一个比较大小的函数**

```go
package main
import "fmt"
func main() {
	var max int
	max = com(6,3)
	fmt.Printf("max: %v", max)
}

func com(a int,b int) (max int)  {
	if a>=b{
		max =a
}else{
		max = b
	}
 return max
}

输出：
max: 6
```

### 14.3 `golang`函数的返回值

函数可以有0或多个返回值，返回值需要指定数据类型，返回值通过`return`关键字来指定

`return`可以有参数，也可以没有参数，有些返回值可以有名称，也可以没有名称。go中的函数可以有多个返回值

**go语言返回值实例**

**●没有返回值**

```go
func f1(){
	fmt.Println("我只用来输出，不返回")
}
```

**●有一个返回值**

```go
func sum(a int,b int) (sum int) {
	sum = a + b
	return sum
}
```

**●多个返回值，且在return中指定返回的内容**

```go
func f2() (name string,age int) {
	name = "Hud"
	age = 24
	return name , age		// 直接return也可以
}
package main
import "fmt"
func main() {
	name , age := f2()
	fmt.Printf("name: %v\n", name)
	fmt.Printf("age: %v", age)
}
```

**●return覆盖命名返回值，返回值名称没有被使用**

```
func f4()(name string,age int){
	n := "Hud"
	a := 24
	return n,a
}
```

函数返回值过多的时候呢，例如有4个以上的返回值，应当将这些返回值收集到容器中，然后以返回容器的方式去返回。例如同类型的返回值可以放进slice，不同类型的返回值可以放进map

但当函数由多个返回值，且其中某个或者某几个返回值不想使用，可以通过下划线`'_'`来丢弃这些返回值，例如下面的这个`f3()`函数，有两个返回值，调用该函数时，丢弃了一个返回值，只保留了一个返回值。

```go
func f3() (int ,int) {
	return 1,3
}
package main
import "fmt"
func main() {
	_ , x := f3()
	fmt.Printf("x: %v", x)
}

输出：
x: 3
```

### 14.4 `golang`函数的参数

go语言可以有0或者多个参数，参数需要指定数据类型。

声明函数时的参数列表叫做形参，调用时传递的参数叫做实参。

go语言是通过**传值的方式传参**的，意味着传递给函数的是拷贝后的副本，所以函数内部访问、修改的也是这个副本。

go语言可以使用**变长参数**，有时候并不能确定参数的个数，可以使用**变长参数**，可以在函数定义语句的参数部分使用`ARGS...TYPE`的方式，这时会将`...`代表的参数全部保存到一个名为`ARGS`的`slice`中，注意这些参数的数据类型都是`TYPE`。

**go语言函数的参数实例**

go语言传参

```go
//  形参列表
func f4(a int,b int)int{
	if a > b{
		return a
	}else{
		return b
	}
}

package main
import "fmt"
func main() {
	// 实参列表
	r := f4(17,8)
	fmt.Printf("r: %v\n", r)
}
```

 **变长参数**

```go
func f5(args...int)  {
	for _, v := range args {
		fmt.Printf("v: %v\n", v)
	}
}
package main
import "fmt"
func main() {
	f5(1,2,3,4,5)
	f5(4,5,6)
}

输出：
v: 1
v: 2
v: 3
v: 4
v: 5
v: 4
v: 5
v: 6
```

### 14.5 `golang`函数类型与函数变量

可以使用`type`关键字来定义一个函数类型，语法格式如下：

```go
type fun func(int,int)int
```

上面的语句定义了一个`fun`函数类型，他是一种函数类型，这种函数接收两个`int`类型的的参数并且返回一个`int`类型的返回值。

下面我们定义两个这样结构的两个函数，一个求和，另一个比较大小

```go
func sum (a int,b int) int{
		return a+b
}
func max(a int , b int)int {
	if a>b{
		return a
	}else{
		return b
	}
}
```

下面定义一个`fun`函数类型，把`sum`和`max`赋值给它

```go
package main
import "fmt"

func main() {
	type f1 func(int,int) int
	var ff f1
	ff = sum
	r := ff(1,2)
	fmt.Printf("r: %v", r)
}

输出：
r: 3
```

### 14.6 `golang`高阶函数

go语言的函数可以作为函数的参数，传递给另外一个函数，还可以作为另外一个函数的返回值进行返回

**go语言函数作为参数**

```go
package main
import "fmt"
func main() {
	f1("Hud",sayHello)
}

func sayHello(name string)  {
	fmt.Printf("Hello,%s", name)
}

func f1(name string,f func(string)){
	f(name)
}

输出：
Hello,Hud
```

**go语言函数作为返回值**

```go
package main
import "fmt"
func add(x,y int) int {
	return x+y
}

func sub(x,y int )  {
	return x-y
}
func cal(s string) func(int,int)int  {
	switch s {
	case "+":
		return add
	case "-":
		return sub
	default:
		return nil
	}
}

func main() {
	ff :=cal("+")
	r :=ff(1,2)
	fmt.Printf("r: %v\n", r)

	fmt.Println("-------------")
	ff =cal("-")
	r =ff(5,4)
	fmt.Printf("r: %v", r)
}

输出：
r: 3
-------------
r: 1
```

### 14.7 `golang`匿名函数

go语言函数不能嵌套，但是在函数内部可以定义匿名函数，实现一下简单的功能调用。

所谓匿名函数就是没有名称的函数。语法格式如下：

```go
func (参数列表)(返回值)
```

**当然也可以既没有参数也没有返回值**

**匿名函数实例**

```go
package main
import "fmt"
func main() {
	max :=func(a int,b int)int {
		if a>b{
		return a
		}else{
	return b
		}
	}
	i := max(1,2)
	fmt.Printf("i: %v", i)
}

输出：
i: 2
```

**自己执行**

```go
 func main() {
	// 自己执行
	func (a int , b int){
		max := 0
		if a>b {
			max = a
		}else{
			max = b
		}
	fmt.Printf("max: %v", max)
	}(3,4)	
 }

输出：
max: 4
```

**匿名函数可以在函数内部进行一些运算**

```go
 func test1(){
	name := "hud"
	age := "24"

	f1 :=func () string  {
		return name + age
	}
	msg := f1()
	fmt.Printf("msg: %v", msg)
 }

输出：
msg: hud24
```

### 14.8 `golang`闭包

**闭包**可以理解成**定义在一个函数内部的函数**。在本质上，闭包是将该函数内部和函数外部连接起来的桥梁，或者说是函数和其引用环境的组合体。

闭包指的是一个函数和预期相关的引用环境组合而成的实体。简单的来说，**闭包=函数+引用环境**。首先看一个例子：

```go
package main
import "fmt"

func add() func(int) int {
	var x int
	return func(y int) int{
		x += y
		return x
	}
}
func main() {
	var f = add()
	fmt.Println(f(10))
	fmt.Println(f(20))
	fmt.Println(f(30))
	fmt.Println("--------")
	f1 := add()
	fmt.Println(f1(40))
	fmt.Println(f1(50))
}

输出：
10
30
60
--------
40
90
```

变量`f`是一个函数并且他引用了其外部作用域中的`x`变量，此时`f`就是一个闭包，在`f`的生命周期内，**变量`x`也一直有效。**

**闭包的进阶实例：**

```go
package main
import "fmt"
func mk (suffix string) func (string) string{
	return func(name string) string{
		if !strings.HasSuffix(name,suffix){
			return name + suffix
		}
		return name
	}
}
func main() {
	jpg := mk(".jpg")
	txt := mk(".txt")
	fmt.Println(jpg("test"))
	fmt.Println(txt("test"))

}
```

**闭包进阶实例：**

```go
package main
import "fmt"
func calc(base int)(func(int) int,func(int) int)  {
	add :=func(i int) int {
		base += i
		return base
	}
	sub :=func (i int) int{
		base -= i
		return base
	}
	return add , sub	
}
func main() {
	f1,f2 :=calc(10)
	fmt.Println(f1(1),f2(2))
	fmt.Println(f1(3),f2(4))
	fmt.Println(f1(5),f2(6))
}

输出:
11 9
12 8
13 7
```



### 14.9 `golang`递归

函数内部调用函数自身的函数成为递归函数。

使用递归函数最重要的三点：

1. 递归就是自己调用自己
2. 必须先定义函数的退出条件，没有退出条件，递归将变成死循环
3. go语言递归函数很可能会产生一大堆的`goroutine`，也可能会出现栈空间内存溢出问题

**go语言递归实例**

```go
package main
import "fmt"

func a(n int) int  {
	// 返回条件
	if n==1{
		return 1
	}else{
	// 自己调用自己
	 return n*a(n-1)
	}
}
func main() {
	x :=a(3)
	fmt.Printf("x: %v\n", x)
	y :=b(4)
	fmt.Printf("y: %v\n", y)
}

func b(x int) int {
	if x==1{
		return 1
	}else{
		return x+b(x-1)
	}
}

输出：
x: 6
y: 10
```

**使用递归进行斐波那契数列运算**

```go
package main
import "fmt"
func main() {
	f := fib(5)
	fmt.Printf("f: %v", f)
}

func fib(a int) int {
	if a == 1 || a ==2{
		return 1
	}else {
		return fib(a-1)+fib(a-2)
	}
}

输出：
f: 5
```

### 14.10 `golang`的defer语句

go语言中的`defer`语句会将其后面跟随的语句进行延迟处理，在`defer`归属的函数即将返回时，将延迟处理的语句按`defer`定义的逆序进行执行，也就是说，先被`defer`的语句最后被执行，最后被`defer`的语句，最先被执行

**defer特性**

------

1. 关键字`defer`用于注册延迟调用
2. 这些调用直到`return`前才被执行，因此可以用来做资源清理
3. 多个`defer`语句，按照先进后出的方式执行
4. `defer`语句中的变量，在`defer`声明时就决定了

**defer用途**

------

1. 关闭文件句柄
2. 锁资源释放
3. 数据库连接释放

**go语言`defer`语句实例**

**查看执行顺序**

```go
package main
import "fmt"
func main() {
	fmt.Println("start")
	defer fmt.Println("step1")
	defer fmt.Println("step2")
	defer fmt.Println("step3")
	fmt.Println("end")
}

输出：
start
end
step3
step2
step1
```

### 14.11 `golang init`函数

`golang`有一个特殊的函数`init`函数，先于`main`函数执行，实现包级别的一些初始化操作。

**`init`函数的主要特点**

- `init`函数先于`main()`函数自动执行，不能被其他函数调用；
- `init`函数没有输入参数、返回值
- 每个包可以有多个`init`函数
- **包的每个源文件也可以有多个init函数，这一点比较特殊**
- 同一个包的`init`执行顺序，`golang`没有明确定义，编程时要注意程序不要依赖这个执行顺序
- 不同包的`init`函数按照包导入的依赖关系决定执行顺序

**`golang`初始化顺序**

**初始化顺序：变量初始化-->`init()`-->`main()`**

```go
package main
import "fmt"

func init()  {
	fmt.Println("this is init function")
}
func main() {
	fmt.Println("main...")
}

输出：
this is init function
main...
```

可以看到，在main函数中，并没有调用init函数，但是还是执行了。其次，`init()`函数可以定义多个。

## 15. `golang`指针

Go语言中的函数传参都是值拷贝，当我们想要修改某个变量的时候，我们可以创建一个指向该变量地址的指针变量。传递数据使用指针，而无需拷贝数据。

类型指针不能进行偏移和运算。

Go语言中的指针操作非常简单，只需要记住两个符号：`&`（取地址符）和`*`（根据地址取值）

**指针地址和指针类型**

每个变量在运行时候都拥有一个地址，这个地址代表变量在内存中的位置。Go语言中使用`&`字符放在变量前面对变量进行**取地址**操作。Go语言中的值类型`(int、bool、float、string、array、struct)`都有对应的指针类型，如`*int、*int64、*string`等

**指针语法**

一个指针变量只想了一个值的内存地址。（也就是我们声明了一个指针之后，可以像变量赋值一样，把一个值的内存地址放入到指针当中。）

类似于变量和常量，在使用指针前你需要声明指针。指针声明的格式如下：

```go
var var_name *var_type
```

`var_type`:指针类型

`var_name`:指针变量名

`*`：为了指定变量是作为一个指针

**指针声明实例**

```go
package main
import "fmt"
func main() {
	var p *int  //声明指针变量
	fmt.Printf("p: %v\n", p)
	fmt.Printf("p: %T\n", p)

	var i int = 100
	k :=&i
	fmt.Printf("k: %v\n", k)
	fmt.Printf("k: %T\n", k)
    
    // 指针取值打印
	fmt.Printf("k: %v\n", *k)
    
    var st *string				// 声明字符串类型指针
	var s string = "Hud"
	st = &s						// 将变量赋值给指针
	fmt.Printf("st: %v\n", st)
	fmt.Printf("st: %T\n", st)
	fmt.Printf("st: %v\n", *st)
}

输出：
p: <nil>
p: *int
k: 0xc0000aa0a0
k: *int
K: 100
```

### 15.1 `golang`指向数组的指针

**定义语法**

```go
var ptr [MAX]*int;
```

**实例演示**

```go
package main
import "fmt"

const MAX int = 3
func main() {
	a :=[]int{1,3,5}
	var i int
	var ptr [MAX]*int;
	fmt.Println(ptr)		// 打印[<nil> <nil> <nil>]
	for i = 0; i < MAX; i++ {
		ptr[i] = &a[i] 	// 整数地址赋值给指针数组
	}
	for i = 0; i < MAX; i++ {
		fmt.Printf("a[%d] = %d \n", i,*ptr[i])		// *ptr[i]就是打印出相关指针的值了
	}
}

输出:
[<nil> <nil> <nil>]
a[0] = 1 
a[1] = 3 
a[2] = 5 
```

```go
package main
import "fmt"
func main() {
	//var a = [3]int{1,3,5}
	var p [3]*int
	fmt.Printf("p: %v\n", p)
	var a = [3]int{1,3,5}
	for i := 0; i < 3; i++ {
		p[i] = &a[i]
	}
	for i := 0; i < 3; i++ {
		fmt.Printf("a[%d]: %v\n", i, *p[i])
	}
}

输出：
p: [<nil> <nil> <nil>]
a[0]: 1
a[1]: 3
a[2]: 5
```

## 16. `golang`的类型定义和类型别名

------

在介绍结构体之前，先看看什么是类型定义和类型别名

### 16.1 Go语言类型定义

类型定义的语法

```go
type NewType Type
```

**实例**

```go
package main
import "fmt"
func main() {
	// 类型定义
	type MyInt int
	// 定义i为MyInt类型
	var i MyInt
	i = 98
	fmt.Printf("i: %v  type: %T", i,i)
}

输出：
i: 98  type: main.MyInt
```

### 16.2 Go语言类型别名

**类型别名的语法**

```go
type NewType = Type
```

**实例**

```go
	type Int = MyInt
	// b其实还是int类型
	var b Int = 9
	fmt.Printf("b: %v type:%T", b,b) 
	
输出：
b: 9 type:main.MyInt
```

**go语言类型定义和类型别名的区别**

1. 类型定义相当于定义了一个**全新的类型**，与之前的类型不同，但是类型别名并没有定义一个新的类型，而是使用了一个别名来替换之前的类型
2. 类型别名只会在代码中存在，在编译完成之后不会存在该别名
3. 因为类型别名和原来的类型是一致的，所以原来类型所拥有的方法，类型别名中也可以**调用**，但是如果是重新定义的一个类型，那么就不可以调用之前的任何方法

## 17. `Golang`结构体

go语言没有面向对象的概念了。但是可以使用结构体来进行实现，面向对象编程的一些特性，例如：继承、组合等特性。

### 17.1 Go语言结构体的定义

------

上一节我们介绍了类型定义，结构体的定义和类型定义类似，只不过多了一个`struct`关键字，语法结构如下

```go
type struct_variable_type struct{
	member definition...
	member definition...
	member definition...
	...
	member definition...
}
```

`type`：结构体定义关键字

`struct_variable_type`:结构体类型名称

`struct`：结构体定义关键字

`member definition`：成员定义

**实例**

```go
type Person struct{
	age int
	name string
	email string
}
```

以上我们定义一个Person结构体，有三个成员，来描述一个Person信息

形同类型的可以合并到一行：

```go
type Person struct{
	age int
	name,email string
}
```

**声明一个结构体变量**

声明一个结构体变量和声明一个普通变量相同，例如

```go
package main
import "fmt"
func main() {
	var qty Person
	fmt.Printf("qty: %v\n", qty)
	hud := Person{}
	fmt.Printf("hud: %v\n", hud)
}
type Person struct{
	age int
	name,email string
}

输出：
qty: {0  }
hud: {0  }
```

在结构体成员被赋值之前都是零值。

**访问结构体成员**

```go
package main
import "fmt"
func main() {
	
type Person struct{
	age int
	name,email string
}
	var qty Person
	qty.age = 24
	qty.name = "Qi Tianyu"
	qty.email = "qitianyu2007@126.com"

	fmt.Printf("qty: %v\n", qty)
}

输出：
qty: {24 Qi Tianyu qitianyu2007@126.com}
```

### 17.2 `golang`结构体的初始化

**未初始化的结构体成员都是零值**

● **使用键值对对结构体进行初始化**

```
package main
import "fmt"
func main() {
	
type Person struct{
	age int
	name,email string
}
	// 不要忘记","
	Monica :=Person{
		age: 20,
		name: "GuQchi",
		email: "qitianyu68@gamil.com",
	}
	fmt.Printf("Monica: %v\n", Monica)
}

输出:
Monica: {20 GuQchi qitianyu68@gamil.com}
```

●**使用值的列表初始化**

```
package main
import "fmt"
func main() {
	
type Person struct{
	age int
	name,email string
}
	Hud := Person{
		24,
		"qitianyu",
		"740912428@qq.com",
	}

	fmt.Printf("Hud: %v", Hud)
}

输出：
Hud: {24 qitianyu 740912428@qq.com}
```

**注意：（列表初始化）**

1. 必须初始化结构体的所有字段
2. 初始值的填充顺序必须与字段所在结构体中声明的顺序一致
3. 该方式不能和键值初始化方式混用

**部分成员初始化**

用不到的成员，可以不进行初始化

```go
package main
import "fmt"
func main() {
	
type Person struct{
	age int
	name,email string
}
	Monica :=Person{
		age: 20,
		name: "GuQchi",
	}
	fmt.Printf("Monica: %v\n", Monica)
}

输出：
Monica: {20 GuQchi }
```

### 17.3 `golang`结构体指针

结构体指针和普通变量指针相同，先来回顾一下普通变量指针。

```go
package main
import "fmt"
func main() {
	var name string
	name = "Hud"
	// 定义p_name指针类型
	var p_name *string
	// &name:取name的地址
	p_name = &name
	fmt.Printf("name: %v\n", name)
	// 输出指针地址
	fmt.Printf("p_name: %v\n", p_name)
	// 输出指针指向的内容值
	fmt.Printf("p_name: %v\n", *p_name)
}

输出：
name: Hud
p_name: 0xc00005c250
p_name: Hud
```

**定义结构体指针**

```go
func test2()  {
		type Person struct{
			id int 
			name string
			age int
		}
		// 先初始化一个结构体
		qty := Person{
			id : 77 ,
			name : "Hud",
			age : 24,
		}
		var p_Person *Person	//定义了一个结构体类型的指针
		p_Person = &qty
		fmt.Printf("qty: %v\n", qty)
		fmt.Printf("p_Person: %v\n", p_Person)
		fmt.Printf("p_Person: %v\n", *p_Person)
}

输出：
qty: {77 Hud 24}
p_Person: &{77 Hud 24}
p_Person: {77 Hud 24}
```

#### 使用`new`关键字创建结构体指针

我们还可以通过使用`new`关键字对结构体进行实例化，得到的是结构体的地址，例如：

```go
 func test3()  {
	type Person struct{
		id int 
		name string
		age int
	}
	var p_Person = new(Person)
	fmt.Printf("p_Person : %v\n", p_Person)
	fmt.Printf("*p_Person : %v\n", *p_Person)
	fmt.Printf("type(p_Person) : %T\n", *p_Person)
}

输出：
p_Person : &{0  0}
*p_Person : {0  0}
type(p_Person) : main.Person
```

### 17.4 `golang`结构体作为函数参数

go结构体可以像普通变量一样，作为函数的参数，传递给函数，这里纷飞两种情况：

1. 直接传递结构体，这是一个副本（拷贝作为值传递），在函数内部不会改变外面结构体内容
2. 传递结构体指针，这时在函数内部能够改变外部结构体内容

**直接传递结构体**

**实例**

```go
type Player struct{
	name string
	number int
	team string
} 
func  showplayer(James Player) {
	//var James Player
	James.name = "James"
	James.number = 23 
	James.team = "Lakers" 
	fmt.Printf("player: %v\n", James)		
}

 func main() {
	James :=Player{"James",6,"Heats"}
	Hud := Player{"Hud",77,"Nets"}
	fmt.Printf("Hud: %v \n", Hud)
	fmt.Println("----------")
	showplayer(James)
	fmt.Println("----------")
	fmt.Printf("player: %v\n", James)
}

输出：
Hud: {Hud 77 Nets} 
----------
player: {James 23 Lakers}
----------
player: {James 6 Heats}
```

可以看到`Hud: {Hud 77 Nets}` 是在函数外定义的变量，`player: {James 23 Lakers}`是在函数内部定义的变量，外部修改。

函数内部改变了结构体内容，函数外面并没有被改变。

```go
func showPlayer2(ply *Player){
	ply.name = "Durant"
	ply.number = 7
	ply.team = "Nets"
	fmt.Printf("ply: %v", ply)

}
func main() {
	Durant :=Player{
	name : "Durant",
	number : 35,
	team : "Thunder",
	}
	ply := &Durant
	fmt.Printf("ply: %v\n", ply)
	showPlayer2(ply)
}

输出：
ply: &{Durant 35 Thunder}
ply: &{Durant 7 Nets}
```

从运行结果来看，我们可以看到，调用函数之后，参数被改变了

### 17.5 `golang`嵌套结构体

go语言没有面向对象的编程思想，也没有继承关系，但是可以通过结构体嵌套来实现这种效果。

下面通过实例演示如何实现结构体嵌套，假如有一个人`Person`结构体，这个人还有一个宠物`Pet`结构体：

**`Pet`结构体**

```go
type Pet struct{
	name string
	age int
	kind string
}
```

**`Person`结构体**

```go
type Person struct{
	name string
	age int
	pet Pet
}
```

**进行结构体访问**

```go
package main
import "fmt"
type Pet struct{
	name string
	age int
	kind string
}
type Person struct{
	name string
	age int
	pet Pet
}
	func main() {
		gqc :=Person{
			age: 20,
			name: "Monica",
		}
	gqc.pet.name = "QB"
	gqc.pet.age = 1
	gqc.pet.kind = "cat"
		fmt.Printf("gqc: %v\n", gqc)
		fmt.Println("-----------")
	
		qty :=Pet{
			name : "hud",
			age : 24,
			kind : "person" ,
		}
	gqc = Person{
		age: 20,
		name: "Monica",
	}
		gqc.pet = qty 
			fmt.Printf("gqc: %v", gqc)
}

输出：
gqc: {Monica 20 {QB 1 cat}}
--------------------
gqc: {Monica 20 {hud 24 person}}
```

## 18. `goalng`方法

go语言没有面向对象的特性，也没有类对象的概念。但是，可以使用结构体来模拟这些特性，我们都知道面向对象里面有类方法等概念，我们也可以声明一些方法，属于某个结构体。

#### **go语言方法的语法**

------

Go中的方法，是一种特殊的函数，定义于`struct`之上（与`struct`关联、绑定）被称为`struct`的接受者（`receiver`）

通俗的讲，方法就是有接受者的函数。

**语法格式如下**

```go
type mytype struct{}

func (recv mytype) my_method(para) return_type{}
func (recv *mytype) my_method(para) return_type{}
```

`mytype`: 定义一个结构体

`recv`：接受该方法的结构体(receiver)

`my_method`：方法名称

`para`：参数列表

`return_type`：返回值类型

从语法可以看出：一个方法和一个函数非常类似，多了一个接受类型

```go
package main
import "fmt"

type Person struct{
	name string
}

func (per Person) eat()  {
	fmt.Println(per.name + " eat...")
}
func (per Person) sleep()  {
	fmt.Println(per.name + " sleep...")
}
func (per Person) fuck()  {
	fmt.Printf("%v fuck gqc",per.name)
}
// 带参数和返回值的方法
func (per Person) login(name string,pwd string) bool  {
	if name == "Hud" && pwd == "199866"{
		return true
	}else {
		return false
	}
}
func main() {
	var per Person
	per.name = "Hud"
	per.eat()
	per.sleep()
	per.fuck()
	cus := Person{
		name : "Hud",
	}
	b := cus.login("Hud","199866")
	fmt.Printf("b :%v", b)
}

输出：
Hud eat...
Hud sleep...
Hud fuck gqc
b :true
```

#### go语言方法的注意事项

1. 方法的receiver type一定要是`struct`类型，type定义的类型别名可退、`slice`、`map`、`channel`、`func`类型等都可以。
2. `struct`结合它的方法就等价于面向对象中的类。只不过`struct`可以和它的方法分开，并非一定要属于同一个文件，但必须同属于一个包
3. 方法有两种接收类型：{T type}和{T *type}，他们之间有区别
4. 方法就是函数，所以go中没有方法重载（`overload`）的说法，也就是说同一个类型中的所有方法名必须都唯一
5. 如果receiver是一个指针类型，则会自动解除引用
6. 方法和type是分开的，意味着实例的行为(behavior)和数据存储(field)是分开的，但是他们通过receiver建立起关联关系

#### `golang`方法接受者类型

结构体实例，有值类型和指针类型，那么方法的接收者是结构体，那么也有值类型和指针类型，区别就是接收者是否复制结构体副本。值类型复制，指针类型不复制。

#### 值类型结构体和指针类型结构体

**实例**

```go
package main
import "fmt"
type Person struct{
	name string
}
func main() {
	p1 := Person{name:"Hud"}
	fmt.Printf("p1 :%T\n", p1)
	p2 := &Person{name:"Hud"}
	fmt.Printf("p2 :%T\n", p2)

	p3 := Person{name:"Hud"}
	p4 := &Person{name:"Hud"}
	showPerson1(p3)
	fmt.Printf("p3: %v\n", p3.name)
	fmt.Println("----------------")
	showPerson2(p4)
	fmt.Printf("p4: %v\n", p4.name)

}	
func showPerson1(per Person)  {
		per.name = "Monica"
}
func showPerson2(per *Person)  {
		// per.name 自动解引用
		// (*per).name = "qty"
		per.name = "qty" 
}

输出：
p1 :main.Person
p2 :*main.Person
p3: Hud
----------------
p4: qty
```

可以看到传递结构体值的时候，外部结构体没有被修改。传递结构体指针时，结构体的值被修改了。



#### 工厂模式

封装结构体中的内容，只提供一个新建结构体函数

```go
//pro01/model/model.go
package model

import "fmt"

// 创建程序 在model包中定义Account结构体
//	1.Account结构体要求具有字段：账号（长度在6-10之间）、密码（必须是6位），余额（必须大于20）

// 定义一个局部的结构体
type account struct {
	accountNo string
	pwd       string
	balance   float64
}

// 工厂模式函数-构造函数
func NewAccount(accountNo string, pwd string, balance float64) *account {
	if len(accountNo) < 6 || len(accountNo) > 10 {
		fmt.Println("请输入6-10位账号")
		return nil
	} else if len(pwd) != 6 {
		fmt.Println("请输入6位密码")
		return nil
	} else if balance < 20 {
		fmt.Println("余额错误")
		return nil
	}
	return &account{
		accountNo: accountNo,
		pwd:       pwd,
		balance:   balance,
	}
}

func (account *account) Print() {
	fmt.Println(account.accountNo)
	fmt.Println(account.balance)
	fmt.Println(account.pwd)
}


```

在main**函数中使用和调用**

```go
package main

import (
	"pro1/model"
)

func main() {
	account := model.NewAccount("Hud9866", "199866", 9000.00)
	account.Print()
}
```



## 19. `golang`接口

接口像是一个公司里面的领导，他会定义一些通用规范，只设计规范而不实现规范

go语言的接口，是一种新的**类型定义**。他把所有的**具有共性的方法**定义在一起，任何其他类型只要实现了这些方法就是实现了这个接口。

语法格式和方法非常类似。

一个结构体只要实现了一个接口的所有方法，就是实现了这个接口（**go隐式实现接口**），可以降低我们代码的耦合性。便于检查错误，

### 接口的语法格式

```go
// 定义接口
type interface_name interface{
    method_name1 [return_type]
    method_name2 [return_type]
    method_name3 [return_type]
   	...
    method_namen [return_type]
}

// 定义结构体
type struct_name struct{
    // variables
}

// 实现接口方法
func (struct_name_variable struct_name) method_name1() [return_type]{
    // 方法实现
}
...
func (struct_name_variable struct_name) method_namen() [return_type]{
    // 方法实现
}
```

**接口实例**

下面我们定义一个`USB`接口，有`read`和`write`两个方法，再定义一个电脑`Computer`和一个手机`Mobile`来实现这个接口。

```go
type USB interface{
	read()
	write()
}
```

**Computer结构体**

```go
type Computer struct{
    name string
}
```

**Mobile结构体**

```go
type Mobile struct{
    brand string
}
```

**Computer实现`USB`接口方法**

```go
func (c Computer) read(){
	fmt.Printf("%v Computer read...\n",c.name)
}
func (c Computer) write(){
	fmt.Printf("%v Computer write...\n",c.name)
}
```

**Mobile实现`USB`接口方法**

```go
func (m Mobile) read(){
	fmt.Printf("%v Mobile read...\n",m.brand)
}
func (m Mobile) write(){
	fmt.Printf("%v Mobile write...\n",m.brand)
}
```

**整体进行实现**

```go
package main

import "fmt"

type USB interface {
	Start()
	Stop()
}

// 定义3个结构体
type phone struct {
	brand string
}
type pad struct {
	brand string
}
type computer struct {
}

// 分别定义两个结构体实现接口中的两个方法
func (p phone) Start() {
	fmt.Printf("%v手机开始工作\n", p.brand)
}

func (p phone) Stop() {
	fmt.Printf("%v手机停止工作\n", p.brand)
}

func (p pad) Start() {
	fmt.Printf("%v平板开始工作\n", p.brand)
}
func (p pad) Stop() {
	fmt.Printf("%v平板停止工作\n", p.brand)
}

// 只要是实现了USB接口方法的(就是指实现了USB接口的所有方法)
func (c computer) Working(u USB) {
	u.Start()
}
func (c computer) Stoping(u USB) {
	u.Stop()
}

func main() {
	phone := phone{"Apple"}
	pad := pad{"Huawei"}
	var c computer
	c.Working(phone)
	c.Working(pad)
	c.Stoping(phone)
	c.Stoping(pad)
}

输出：
Apple手机开始工作
Huawei平板开始工作
Apple手机停止工作
Huawei平板停止工作
```

### `golang`接口值类型接受者和指针类型接收者

这个话题，本质上和方法值类型接收者和指针类型接收者的思考方法是一样的，值接收者是一个拷贝，是一个副本，而指针接收者传递的是指针。

**实例演示**

**定义一个Pet接口**

```go
type Pet interface{
	eat()
}
```

**定义一个Cat结构体**

```go
type Cat struct{
	name string
}
```

**实现Pet接口（接收者是值类型）**

```go
func (cat Cat) eat()  {
	fmt.Printf("%v eat shit\n", cat.name)
	cat.name = "QB"
}
```

**测试**

```go
func main() {
	cat :=Cat{"QBiii"}
	fmt.Printf("cat: %p\n", &cat)
	cat.eat()
	fmt.Printf("cat: %v\n", cat)
}

输出：
cat: 0xc00005c250
QBiii eat shit
cat: {QBiii}
```

使用指针类型接收者进行对比看一下

```go
package main
import "fmt"
type Pet interface{
	eat()
}
type Cat struct{
	name string
}
func (cat *Cat) eat1()  {
	cat.name = "QB"
	fmt.Printf("%v eat bullshit\n", cat)
	}
func main() {
	cat :=&Cat{"丘比特"}
	fmt.Printf("cat: %p\n", cat)
	cat.eat1()
	fmt.Printf("cat: %v\n", cat.name)
}

输出：
cat: 0xc00005c250
&{QB} eat bullshit
cat: QB
```

对比之后可以发现，在第一个例子中，接收者类型是值类型，将参数传进对应方法之后，结构体的值没有发生改变，依然是`“QBiii”`，但是在第二个例子当中，接收者是指针类型接收者，`main()`函数定义的name为“丘比特”，但是传递到方法中后，结构体的值被改变成了“`QB`”

### 19.1 `golang`接口和类型的关系

1. 一个类型可以实现多个接口
2. **多个类型可以实现同一个接口（多态）**

#### 19.1.1 **一个类型实现多个接口**

​	一个类型实现多个接口，例如：有一个Player接口可以播放音乐，有一个Video接口可以播放视频，一个手机Mobile实现这两个接口，既可以播放音乐又可以播放视频。

**定义一个Player接口**

```go
type Player interface {
	playMusic()
}
```

**定义一个Video接口**

```go
type Video interface {
	playVideo()
}
```

**定义Mobile结构体**

```go
type Mobile struct {
	brand string
}
```

**实现两个接口**

```go
func (m Mobile) playMusic() {
	fmt.Println("lalalalala~~")
}
func (m Mobile) palyVideo() {
	fmt.Println("---------------")
	fmt.Println("|    Video    |")	
	fmt.Println("---------------")
}
```

**测试**

```go
func main() {
	m := Mobile{"apple"}
	m.playMusic()
	m.palyVideo()
}

输出：
lalalalala~~
---------------
|    Video    |
---------------
```

#### 19.1.2 多个类型实现同一个接口

比如一个宠物接口Pet，猫类型Cat和狗类型Dog都可以实现该接口，都可以把猫和狗当成宠物类型对待。这在其他语言中叫做多态

**定义一个Pet接口**

```go
type Pet interface {
	eat()
}
```

**定义Dog&Cat结构体**

```go
type Cat struct {
	name string
}
type Dog struct {
	name string
}
```

**定义方法**

```go
func (dog Dog) eat() {
	fmt.Printf("Dog(%v) is eating\n",dog.name)
}
func (cat Cat) eat() {
	fmt.Printf("Cat(%v) is eating\n",cat.name)
}
```

**测试**

```go
func main() {
	dog :=Dog{"gqc"}
	cat :=Cat{"QB"}
	dog.eat()
	cat.eat()
}

输出：
Dog(gqc) is eating
Cat(QB) is eating
```

**另外一种方式实现接口**

```go
func main() {
	// 展示多态
	var pet Pet
	pet = Dog{"gqc"}
	pet.eat()
	pet = Cat{"QB"}
	pet.eat()
}

输出：
Dog(gqc) is eating
Cat(QB) is eating
```

### 19.2 `golang`接口嵌套

接口可以通过嵌套，创建新的接口，例如：飞鱼、既可以飞又可以游泳，我们创建一个飞Fly接口，创建一个游泳接口Swim，飞鱼接口由这两个接口组成。

**飞`Flyer`接口**

```go
type Flyer interface {
	fly()
}
```

**游泳`Swimmer`接口**

```go
type Swimmer interface {
	swim()
}
```

**组合一个接口`FlyFish`**

```go
type Flyfish interface {
	Flyer
	Swimmer
}
```

**创建一个结构体`Fish`**

```go
type Fish struct {
}
```

**实现这个组合接口**

```go
func (fish Fish) fly()  {
	fmt.Println("fly....")
}
func (fish Fish) swim() {
	fmt.Println("swim....")
}
```

**测试**

```go
func main() {
	var ff Flyfish
	ff = Fish{}
	ff.fly()
	ff.swim()
}

输出：
fly....
swim....
```

### 19.3 `golang`通过接口实现`OCP`设计原则

`OCP`是面向对象得可复用设计的第一块基石，便是所谓的”开-闭“原则（Open-Closed Principle，缩写为`OCP`）虽然，go语言不是面向对象语言，但是也可以模拟实现这个原则。对**拓展**是开放的，对**修改**是关闭的。

**`OCP`设计原则实例**

下面通过一个人养宠物的例子，来解释`OCP`设计原则。

**定义一个宠物接口`Pet`**

```go
type Pet interface {
	eat()
	sleep()
}
```

该接口有吃和睡两个方法。

**定义一个Cat结构体**

```go
type Cat struct {
	name string
	age int
}
```

**Cat实现接口方法**

```go
func (cat Cat) eat() {
	fmt.Printf("cat:%v age:%v is eating...\n",cat.name,cat.age)
}
func (cat Cat) sleep() {
	fmt.Printf("cat:%v age:%v is sleeping...\n",cat.name,cat.age)
}
```

**定义一个Dog结构体**

```go
type Dog struct {
	name string
	age int
}
```

**Dog实现接口方法**

```go
func (dog Dog) eat() {
	fmt.Printf("dog:%v age:%v is eating...\n",dog.name,dog.age)
}
func (dog Dog) sleep() {
	fmt.Printf("dog:%v age:%v is sleeping...\n",dog.name,dog.age)
}
```

**定义一个`Person`结构体**

```go
type Person struct{
	name string
}
```

**为`Person`添加一个养宠物方法**

```go
func (per Person) care(pet Pet)  {
	pet.eat()
	pet.sleep()
}
```

**最后进行一下测试**

```go
func main() {
	dog := Dog{"Dove",2}
	cat := Cat{"QB",1}
	per := Person{"Monica"}

	per.care(dog)
	per.care(cat)
}

输出：
dog:Dove age:2 is eating...
dog:Dove age:2 is sleeping...
cat:QB age:1 is eating...
cat:QB age:1 is sleeping...
```

### 19.4 `golang`模拟`OOP`的属性和方法

`golang`没有面向对象概念，也没有封装的概念，但是可以通过结构体`struct`和函数绑定来实现`OOP`的属性和方法等特性，接收者receiver**方法**（函数与结构体进行绑定）

#### `golang`的继承

`golang`在本质上没有`OOP`概念，也没有继承的概念，但是可以通过**结构体嵌套**实现这个特性。

例如：

```go
 package main
import "fmt"

type Animal struct {
	name string
	age int 
}
func (a Animal) eat() {
	fmt.Printf("Animal %v is eating ...\n", a.name)
}
func (a Animal) sleep () {
	fmt.Printf("Animal %v is eating ...\n", a.name)
}
// 通过嵌套的方式定义结构体
type Dog struct {
	Animal
}
type Cat struct {
	Animal
}
func main() {
	dog :=Dog{Animal{"Dove",2}}
	cat :=Cat{Animal{"QB",1}}
	dog.eat()
	dog.sleep()
	cat.eat()
	cat.sleep()
}

输出:
Animal Dove is eating ...
Animal Dove is eating ...
Animal QB is eating ...
Animal QB is eating ...
```

如果说，新的结构体中不仅继承了原先结构体的一些特性，还有一些新的结构体特性可以:

**定义一个Animal结构体**

```go
type Animal struct {
	name string
	age int
}
```

**Animal实现方法**

```go
func (a Animal) eat(){
	fmt.Println("Is eating...")
}
```

**定义一个Cat结构体，继承Animal，并带新的特性**

```go
type Cat struct {
	Animal
	color string
}
```

**声明一个Cat结构体变量cat，并调用继承的结构体中的方法**

```go
func main() {
	cat :=Cat{Animal{"Qb",2},"white"}
	cat.eat()
}

输出：
Is eating...
```

### 19.5 `golang`构造函数

`golang`没有构造函数的概念，可以使用函数来模拟构造函数的功能。

**例如**

```go
package main
import "fmt"

type Person struct {
	name string
	age int
}
func NewPerson(name string,age int) (*Person,error)  {
	if name ==""{
		return nil,fmt. Errorf("name不能为空")
	}
	if age <= 0 {
		return nil,fmt. Errorf("age不能小于0")
	}
	return &Person{name:name,age:age},nil
}
func main() {
	person ,err :=NewPerson("hud",20)
	if err == nil{
		fmt.Printf("person :%v", *person)
	}
}

输出：
person :{hud 20}
```



### 19.6 多态

​	变量具有多种形态，在Go语言中，多态特征是通过接口实现的。可以按照统一的接口来调用不同的实现，这时接口变量呈现不同的形态

​	例如在上面USB的方法中，USB会根据传入的实参，来判断到底传入的是哪个结构体（Phone和Pad都实现了），USB体现出了多态的特征。

```go
	var usbArr [3]USB
	usbArr[0] = pad{"huawei"}
	usbArr[1] = pad{"oppo"}
	usbArr[2] = phone{"apple"}
	for i := 0; i < 3; i++ {
		fmt.Println(usbArr[i])
	}
```



- #### 多态数组

  还是用上面的USB、pad、phone的例子实现一个多态数组

### 接口使用的注意事项

1. **接口本身不能创建实例，但是可以指向一个实现了该接口的自定义类型的变量（实例）**

   ```go
   type People interface {
   	Say()
   }
   
   type Student struct {
   	name string
   	age  int
   }
   
   func (s Student) Say() {
   	fmt.Printf("I am %v,age%v", s.name, s.age)
   }
   func main() {
   	var p People = Student{"Hud", 24}
   	p.Say()
   }
   
   输出：
   I am Hud,age24
   ```

2. **接口中的方法都没有方法体，即都是没有实现的方法**

3. **在go中，一个自定义类型需要将某个接口的所有方法都实现，我们说这个自定义类型实现了这个接口。**

4. **一个自定义类型只有实现了某个接口，才能将该自定义类型的实例（变量）赋给接口类型（例如上面的代码）**

5. **只要是自定义数据类型就可以实现接口，不仅仅是结构体类型**

   ```go
   type myint int
   type Int interface {
   	Add()
   }
   
   func (m myint) Add() {
   	fmt.Printf("%v+3=%v", m, m+3)
   }
   
   func main() {
   	var i Int = myint(2)
   	i.Add()
   }
   
   输出：
   2+3=5
   ```

6. **一个自定义类型可以实现多个接口（只要这个结构体实现了这些接口的方法）**

7. **go的接口中不能有任何的变量**

8. **一个接口（接口A）可以继承多个别的接口（接口B、接口C），但是如果要实现A接口，就需要将B、C的方法也全部实现**

9. **Interface类型默认是一个指针（引用类型），如果没有对interface初始化就使用，那么会输出nil**

10. **空接口interface{}没有任何方法，所以所有的类型都实现了空接口。**



### **接口最佳实践**

​	**实现对Players结构体切片的排序：`sort.Sort(data Interface)`**  **这个在22.8章节的Sort中有用到。也可以看看**

```go
package main

import (
	"fmt"
	"sort"
)

// 声明一个Players结构体
type Players struct {
	name string
	num  int
}

// 声明一个Player结构体切片类型
type PlayerSlice []Players

// 实现Interface接口（三个方法）
// 1. Len()
func (p PlayerSlice) Len() int {
	return len(p)
}

// 2.Less() 表示按升序还是降序进行排序
func (p PlayerSlice) Less(i, j int) bool {
	return p[i].num < p[j].num
}

// 3.Swap() 会调用Swap()方法 进行交换并排序
func (p PlayerSlice) Swap(i, j int) {
	temp := p[i]
	p[i] = p[j]
	p[j] = temp
}

// 实现了三个方法也就是实现了接口
//  players :=PlayerSlice{{"james",23},{"Durant",35},{"Rose",1},{"Irving",2}}

func main() {
	players := PlayerSlice{{"james", 23}, {"Durant", 35}, {"Rose", 1}, {"Irving", 2}}
	fmt.Println(players)
	sort.Sort(players)
	fmt.Println(players)
}

输出：
[{james 23} {Durant 35} {Rose 1} {Irving 2}]
[{Rose 1} {Irving 2} {james 23} {Durant 35}]
```



## **20. `Golang`包**

包可以区分命名空间（一个文件夹中不能有两个同名文件），也可以更好的管理项目，在go中创建一个包，一般是创建一个文件夹，在该文件夹里面的go文件中，使用package关键字声明包名称，通常文件夹名称和包名称相同。并且同一个文件下面只有一个包。

### 创建包

------

1. 创建一个名为`bao`的文件夹

2. 创建一个`bao.go`文件

3. 在该文件中声明包

   ```go
   package bao
   import "fmt"
   	func Hello() {
   		fmt.Println("Hello from bao")
   }
   ```

### 导入包

------

要使用某个包下的变量或者方法，需要导入该包，导入包时候，要导入从`GOPATH`开始的包路径，例如在`main.go`中导入`bao`包

```go
package main
import (
	"PRO04/bao"
	"fmt"
)

func main() {
	bao.Hello()
	fmt.Println("hello from the main function")
}

输出：
Hello from bao
hello from the main function
```

### 包注意事项

- 一个文件夹下只能有一个packag
  - `import`后面其实是`GOPATH`开始的相对目录路径，包括最后一段，但由于一个目录下只能有一个`package`，所以`import`一个路径就等于是`import`了这个路径下的所有包
  - 注意，这里指的是“**直接包含**“的go文件。如果有子目录，那么子目录的父目录是完全两个包
- 比如你实现了一个计算器的`package`，名字叫做`calc`位于`calc`目录下面。但是又想给别人一个使用范例，于是在`calc`下可以创建个`example`子目录`(calc/example)`，这个子目录里有一个`example.go `(`calc/example/example.go`)。此时，`example.go`可以是`main`包，里面还可以有个main函数。
- 一个package文件不能在多个文件夹下
  - 如果多个文件夹下有重名的package，其实是彼此无关的package
  - 如果一个go文件需要同时使用不同目录下的同名`package`，需要在`import`这些目录时为每个目录制定一个package的别名。


### `golang`包管理工具go module

**go module简介**

------

go module是`golang` 1.11新加的特性，用来管理模块中包的依赖关系。

#### **go mod使用方法**

- 初始化模块

  ```go
  go mod init <项目模块名称>
  ```

- 依赖关系处理，根据go.mod文件

  ```go
  go mod tidy
  ```

- 将依赖包复制到项目下的vendor目录

  ```
  go mod vendor
  ```

  **如果包被屏蔽（墙），可以使用这个命令，随后使用go build -mod=vendor编译**

- 显示依赖关系

  ```go
  go list -m all
  ```

- 显示详细依赖关系

  ```go
  go list -m -json all
  ```

- 下载依赖

  ```go
  go mod download [path@version]
  ```

  **[path@version]是非必写的**

```shell
PS F:\GoCode\PRO04> go mod init PRO04 
go: creating new go.mod: module PRO04
go: to add module requirements and sums:
        go mod tidy
```

生成`go.mod`文件

```go
module PRO04

go 1.18
```



## 21. `golang`并发编程

### 21.1 `golang`协程

`golang`中的并发是**函数**相互独立运行的能力，**`Goroutines`**是并发运行的函数，`golang`提供了**`Goroutines`**作为并发处理操作的一种方式。

创建一个协程非常简单就是在一个任务函数签名添加一个go关键字。

```go
go task()
```

**实例1**

```go
package main
import (
	"fmt"
	"time"
)

func show(msg string)  {
	for i := 0; i < 5; i++ {
		fmt.Printf("msg: %v", msg)
		time.Sleep(time.Millisecond * 30)	//运行一次睡眠30ms
	}
}
func main() {
	go show("golang\n")	
	show("C Program\n")		//在main()中执行，如果它前面也添加go，程序没有输出
	fmt.Println("end...")
}

输出：
msg: C Program
msg: golang
msg: golang
msg: C Program
msg: C Program
msg: golang
msg: golang
msg: C Program
msg: C Program
msg: golang
end...
```

go关键字启动了一个协程来执行

### 21.2 `golang`通道`channel`

**为什么需要channel？**

使用全局变量加锁同步来解决`goroutine`的通讯，但不完美

1. 主线程在等待所有goroutine全部完成的时间很难确定
2. 如果主线程休眠时间长了，会加长等待时间，短了可能还有goroutine处于工作状态，也会随着主线退出而销毁
3. 通过全局变量加锁同步来实现通讯，也并不利用多个协程对全局变量的读写操作

`golang`提供了一种称为通道的机制，用于在`goroutine`之间共享数据，当你作为`goroutine`执行并发活动时，需要在`goroutine`之间共享资源或数据，通道充当`goroutine`之间的管道（通道）并提供一种机制来保证同步交换。

需要在声明通道时，指定数据类型。我们可以共享内置、命名、结构和引用类型的值和指针。数据在通道上传递，在任何给定时间只有一个`goroutine`可以访问数据项：因此按照设计不会发生数据竞争。

根据数据的交换行为，有两种类型的通道：**无缓冲通道**和**缓冲通道**。无缓冲通道用于执行`goroutine`之间的同步通信，而缓冲通道用于执行异步通信，无缓冲通道保证在发送和接受发生的瞬间执行两个`goroutine`之间的交换，缓冲通道没有这样的保证。

**通道由make函数创建，该函数指定`chan`关键字和通道的元素类型**

#### 创建无缓冲和缓冲通道的代码块

**语法**

```go
Unbuffered := make(chan int)  //整型无缓冲通道
buffered := make(chan int,10)	//整型有缓冲通道
```

使用内置函数`make`创建无缓冲通道和缓冲通道。make的第一个参数需要关键字`chan`，然后是通道允许交换的数据类型。

**这是将值发送到通道的代码块需要使用运算符：`<-`**

**语法**

```go
goroutine1 := make(chan string,5)  //字符串缓冲通道
goroutine1 <- "China"			   //通过通道发送字符串
```

一个包含5个值的缓冲区的字符串类型的`goroutine`通道，然后通过通道发送字符串"China"

**这是从通道接收值的代码块**

**语法**

```go
data := <-goroutine1  //从通道接收字符串
```

`<-`运算符附加到通道变量（`goroutine1`）的左侧，以接收来自通道的值。

**无缓冲通道**

在无缓冲通道中，在接收到任何值之前都没有能力保存他，在这种类型通道中，发送和接收`goroutine`在任何发送或接收操作完成之前的同一时刻都准备就绪，如果两个`goroutine`没有在同一时刻准备好，则通道会让执行其各自发送或接收操作的`goroutine`首先等待。同步是通道上发送和接收之间交互的基础，一个没有另一个就不可能发生。

**缓冲通道**

在缓冲通道中，有能力在接收到一个或者多个值之前保存他们。在这个类型的通道中，不会强制`goroutine`在同一时刻准备好执行发送和接收。当发送和接收阻塞时也有不同条件，只有当通道中没有要接收的值时，接收才会阻塞。仅当没有可用缓冲区来放置正在发送的值时，发送才会阻塞。

#### 通道发送和接收特性

1. 对于一个通道，发送操作之间是互斥的，接收操作之间也是互斥的。
2. 发送操作和接收操作中对元素值的处理都是不可分割的
3. 发送操作在完全完成之前会被阻塞，接收操作也是如此

**实例**

```go
package main
import (
	"fmt"
	"math/rand"
	"time"
)

// 创建int类型的无缓冲通道，只能传入int类型的值
var values = make(chan int)

func send()  {
	rand.Seed(time.Now().UnixNano())
	value := rand.Intn(10)
	fmt.Printf("send: %v\n", value)
	// time.Sleep(time.Second*5)
	values <- value
}

func main() {
	// 从通道接收值
	defer close(values)		// 通道用完了之后关闭
	go send()
	fmt.Println("wait...")
	value := <- values
	fmt.Printf("receive: %v\n", value)
	fmt.Println("end...")
}

输出：
wait...
send: 5
receive: 5
end...
```

**利用无缓冲 channel 用作信号传递实现 1 对 1 通知信号**

```go
package main

import (
	"fmt"
	"time"
)

type signal struct{}

func worker() {
	println("工人正在工作")
	time.Sleep(time.Second * 3)
}

func spawn(f func()) <-chan signal {
	c := make(chan signal)
	go func() {
		println("工人开始工作")
		f()
		c <- signal{}
	}()
	return c
}

func main() {
	println("开始一个工人")
	c := spawn(worker)
	<-c
	fmt.Println("工人工作结束")
}

/* 在这个例子中，spawn函数返回的channel，
被用于承载新Goroutine退出的“通知信号”
这个信号专门用作通知 main goroutine。
main goroutine 在调用 spawn 函数后一直
阻塞在对这个“通知信号”的接收动作上。
*/

输出：
开始一个工人
工人开始工作
工人正在工作
工人工作结束
```

**利用无缓冲 channel 用作信号传递实现 1 对 1 通知信号**

```go
package main

import (
	"fmt"
	"sync"
	"time"
)

func worker(i int) {
	fmt.Printf("worker %d: is working...\n", i)
	time.Sleep(1 * time.Second)
	fmt.Printf("worker %d: works done\n", i)
}

type signal struct{}

func spawnGroup(f func(i int), num int, groupSignal <-chan signal) <-chan signal {
	c := make(chan signal)
	var wg sync.WaitGroup

	for i := 0; i < num; i++ {
		wg.Add(1)
		go func(i int) {
			<-groupSignal
			fmt.Printf("worker %d: start to work...\n", i)
			f(i)
			wg.Done()
		}(i + 1)
	}

	go func() {
		wg.Wait()
		c <- signal{}
	}()
	return c
}

func main() {
	fmt.Println("start a group of workers...")
	groupSignal := make(chan signal)
	c := spawnGroup(worker, 5, groupSignal)
	time.Sleep(5 * time.Second)
	fmt.Println("the group of workers start to work...")
	close(groupSignal)  //向所有 worker goroutine 广播“开始工作”的信号
	<-c
	fmt.Println("the group of workers work done!")
}
// 关闭一个无缓冲 channel 会让所有阻塞在这个 channel 上的接收操作返回，从而实现了一种 1 对 n 的“广播”机制


输出：
start a group of workers...
the group of workers start to work...
worker 4: start to work...
worker 4: is working...
worker 3: start to work...
worker 3: is working...
worker 5: start to work...
worker 5: is working...
worker 2: start to work...
worker 2: is working...
worker 1: start to work...
worker 1: is working...
worker 1: works done
worker 2: works done
worker 4: works done
worker 3: works done
worker 5: works done
```



### 21.3 并发编程--`WaitGroup`实现同步

两个协程之间相互等待，等待另一个完成

**`state1` 字段**

接下来我们来看看 `WaitGroup` 的 `state1` 字段。· 是一个包含了 counter 总数、 waiter 等待数、`sema` 信号量的 `uint32` 数组。

每当有 goroutine 调用了 Wait() 方法阻塞等待时，就会对 waiter 数量 + 1，然后等待信号量的唤起通知。

当我们调用 Add() 方法时，就会对 state1 的 counter 数量 + 1。

当调用 Done() 方法时就会对 counter 数量 -1。

直到 counter == 0 时就可以通过信号量唤起对应 waiter 数量的 goroutine 了，也就是唤起刚刚阻塞等待的 goroutine 们。

关于信号量的解释，可以参考下 ***\*[golang 重要知识：mutex](https://link.zhihu.com/?target=https%3A//mp.weixin.qq.com/s/F5PnyH3SG0EZiOzmejr5mw)\**** 里的相关介绍：

**实例演示**

查看添加`waitGroup`和不添加`waitGroup`的区别

```go
package main
import "fmt"
func show(i int)  {
	fmt.Printf("%v\n",i)
}
func main() {
	for i := 0; i < 10; i++ {
		// 启动一个协程执行
		go show(i)
	}
	// 主协程
	fmt.Println("end...")
}

输出：
1
3
2
end...
```

可以看到在没有添加`waitGroup`时，主协程在运行结束后，整个程序就已经运行结束了，没有等待`show()`协程运行完毕。

**实例**

```go
package main
import "fmt"
import "sync"
var wg sync.WaitGroup
func show(i int)  {
	// defer wp.Add(-1)
	defer wg.Done()		// 当语句执行结束的时候才进行调用
	fmt.Printf("%v\n",i)
}
func main() {
	for i := 0; i < 10; i++ {
		// 启动一个协程执行
		wg.Add(1)
		go show(i)
	}

	wg.Wait()  // 等待子协程的结束
	// 主协程
	fmt.Println("end...")
}

输出：
9
4
0
1
2
3
6
5
7
8
end...
```

### 21.4 `golang`并发--runtime包

**runtime包里面定义了一些协程管理相关的API**

#### runtime.Gosched()

------

让出CPU时间片，重新等待安排任务

```go
package main
import(
	"fmt"
	"runtime"
)

func show(s string)  {
	for i := 0; i < 2; i++ {
		fmt.Println(s)
	}
}

func main() {
	go show("golang")	//协程函数
	// 主协程
	for i := 0; i < 2; i++ {
		// 	切一下，再次分配任务
		runtime.Gosched()  //有权刘执行任务了，让给其他子协程执行
		fmt.Println("java")
	}

	fmt.Println("program ended~!")
}

输出：
golang
golang
java
java
program ended~!
```

如果注释掉：

```go
package main
import(
	"fmt"
	"runtime"
)

func show(s string)  {
	for i := 0; i < 2; i++ {
		fmt.Println(s)
	}
}

func main() {
	go show("golang")	//协程函数
	// 主协程
	for i := 0; i < 2; i++ {
		// 	切一下，再次分配任务
		//runtime.Gosched()  //有权力执行任务了，让给其他子协程执行
		fmt.Println("java")
	}
	fmt.Println("program ended~!")
}

输出：
java
java
program ended~!
```

#### runtime.Goexit()

退出当前协程

```go
package main
import (
	"fmt"
	"runtime"
	"time"
)
func show(){
	for i := 0; i < 10; i++ {
		if i>=5 {
			runtime.Goexit()
		}
		fmt.Printf("i: %v\n", i)
	}
}

func main() {
	go show()
	time.Sleep(time.Second)	
}

输出：
i: 0
i: 1
i: 2
i: 3
i: 4
```

原本在这个休眠的1秒中内，子协程应该是将0~9全部输出的，但是在子协程中定义了这个`runtime.Goexit()`退出了子协程。所以程序最终输出为：0~4

#### runtime.GOMAXPROCS

设置最大CPU核心数

```go
package main
import (
	"fmt"
	"runtime"
	"time"
)
func a()  {
	for i := 0; i < 10; i++ {
		fmt.Println("A:",i) 
	}
}
func b()  {
	for i := 0; i < 10; i++ {
		fmt.Println("B:",i)
	}
}
func main() {
	fmt.Printf("runtime.NumCPU():%v\n", runtime.NumCPU())
	runtime.GOMAXPROCS(2)  //  设置最大CPU核心数
	go a()
	go b()
	time.Sleep(time.Second)
}

输出：
runtime.NumCPU():16
B: 0
B: 1
B: 2
B: 3
B: 4
B: 5
A: 0
A: 1
A: 2
A: 3
A: 4
A: 5
A: 6
A: 7
A: 8
A: 9
B: 6
B: 7
B: 8
B: 9
```

如果把CPU最大核心数改为1：

```go
func main() {
	fmt.Printf("runtime.NumCPU():%v\n", runtime.NumCPU())
	runtime.GOMAXPROCS(1)  //  设置最大CPU核心数
	go a()
	go b()
	time.Sleep(time.Millisecond * 100)
}

输出：
同上
```

也就是说为1的时候，就是串行执行。为2的时候可能是并行执行。（这边讲的不是很清楚，我也不太明白）

### 21.5 `Golang`并发--Mutex互斥锁实现同步

**互斥锁**:可以使临界区同时只有一个**线程**(协程)持有，这样别的线程(协程)想持有临界区的时候就会等待(失败)。

除了使用channel实现同步之外，还可以使用Mutex互斥锁的方法实现同步。一个加1操作和一个减1操作，都分别执行100次

```go
package main
import (
	"fmt"
	"sync"
	"time"
)
var m int = 10
var lock sync.Mutex
var wt sync.WaitGroup

func add()  {
	defer wt.Done()
	lock.Lock()
	m += 1
	fmt.Printf("m++: %+v\n", m)
	time.Sleep(time.Millisecond * 10)
	lock.Unlock()
}

func sub()  {
	defer wt.Done()
	lock.Lock()
	time.Sleep(time.Millisecond * 2)
	m -= 1
	fmt.Printf("m--: %+v\n", m)
	lock.Unlock()
}
func main() {
	for i := 0; i < 5; i++ {
		go add()
		wt.Add(1)
		go sub()
		wt.Add(1)
	}
	wt.Wait()
	fmt.Printf("%+v\n", m)
}

输出：
m++: 11
m--: 10
m--: 9
m++: 10
m--: 9
m++: 10
m--: 9
m++: 10
m--: 9
m++: 10
10
```

对线程进行加锁，可以避免内存中读取错误，实现同步。

### 21.6 `golang`并发--channel遍历

**方法1 for循环遍历**

```go
package main
import "fmt"
func main() {
	c := make(chan int)
	go func(){
		for i := 0; i < 10; i++ {
			c <- i
		}
		close(c)
	}()				//自己调用自己
	for {			// 定义一个死循环
		if data, ok := <-c; ok{
			fmt.Printf("data: %v\n", data)
		}else{
			break
		}
	}
}

输出：
data: 0
data: 1
data: 2
data: 3
data: 4
data: 5
data: 6
data: 7
data: 8
data: 9
```

**使用for range遍历channel**

```go
package main
import "fmt"
func main() {
	c := make(chan int)
	go func(){
		for i := 0; i < 10; i++ {
			c <- i
		}
		close(c)
	}()		//自己调用自己
	for v := range c {
		fmt.Printf("v: %+v\n", v)
	}
}

输出：
v: 0
v: 1
v: 2
v: 3
v: 4
v: 5
v: 6
v: 7
v: 8
v: 9
```

### 21.7 `goalng`并发--select switch

1. `select`是Go中的一个控制结构，类似于`switch`语句，用于处理异步IO操作。`select`会监听case语句中`channel`的读写操作，当case中的`channel`读写操作为非阻塞状态（即能读写）时，即会触发相应的动作。

   > ​	**`select`中的case语句必须是一个channel操作**
   >
   > ​	**`select`中的`default`子句总是可运行的**

2. 如果有多个`case`都可以运行，`select`会随机公平的选出一个执行，其他不会执行

3. 如果没有可运行的`case`语句，且有`default`语句。那么就会执行`default`的操作

4. 如果没有可运行的`case`语句，且没有`default`语句，`select`将阻塞，直到某个case通信可以运行

**实例**

```go
package main

import (
	"fmt"
	"time"
)

var chanInt = make(chan int)
var chanStr = make(chan string)

func main() {

	go func() {
		chanInt <- 98
		chanStr <- "hud"
		close(chanInt)
		close(chanStr)
	}()

	for {
		select {
		case r := <-chanInt:
			fmt.Printf("chanInt: %+v\n", r)
		case r := <-chanStr:
			fmt.Printf("chanStr: %+v\n", r)
		default:
			fmt.Printf("default..")
		}
		time.Sleep(time.Second)

	}

}

输出：
chanStr: 
chanStr: 
chanInt: 0
chanStr: 
chanInt: 0
chanStr: 
chanInt: 0
chanStr: 
chanStr: 
chanInt: 0
chanInt: 0
...
```

### 21.8 `goalng`并发--Timer

Timer顾名思义就是计时器的意思，可以实现一些定时器操作，在定时器内部也是通过channel来实现的

```go
package main

import (
	"fmt"
	"time"
)

func main() {
	timer1 := time.NewTimer(time.Second * 2)
	t1 := time.Now()
	fmt.Printf("t1: %v\n", t1)

	t2 := <-timer1.C // C的类型是一个通道（channel）
	fmt.Printf("t2: %v\n", t2)

	timer2 := time.NewTimer(time.Second * 2)
	<-timer2.C // 这就是不获取时间，直接阻塞
	fmt.Printf("2s后 :%v", time.Now())

	// 如果是只想单纯的等待的话，可以使用time.Sleep()来实现
	time.Sleep(time.Second * 2)
	fmt.Printf("再一次2s后: %v", time.Now())

	// time.After()的返回值是chan Time
	<-time.After(time.Second *2)
	fmt.Printf("再再一次2s后: %v", time.Now())
	
}

输出：
t1: 2022-07-09 18:31:35.5507983 +0800 CST m=+0.001724101
t2: 2022-07-09 18:31:37.5639031 +0800 CST m=+2.014828901
2s后 :2022-07-09 18:31:39.5790027 +0800 CST m=+4.029928501
再一次2s后: 2022-07-09 18:31:41.5825824 +0800 CST m=+6.033508201
再再一次2s后: 2022-07-09 18:31:43.5945889 +0800 CST m=+8.045514701
```

**time.Stop()**

```go
package main

import (
	"fmt"
	"time"
)
func main() {
	// 停止计时器
	time3 := time.NewTimer(time.Second * 3)
	go func() {
		<-time3.C
		fmt.Println("三秒计时： %v", time.Now())
	}()
	fmt.Println("三秒计时： %v", time.Now())
	stop := time3.Stop()
	if stop {
		fmt.Println("stop...")
	}

}

输出：
三秒计时： %v 2022-07-10 15:12:22.230836 +0800 CST m=+0.002005101
stop...
```

可以看到，stop函数停止了协程中的计时器，直接对func下的操作进行执行。

也就是组织timer事件发生，stop()函数执行后，timer计时器停止，相应事件不再执行。

**`time.Reset()`**

```go
package main

import (
	"fmt"
	"time"
)

func main() {
	// 重新设置计时器
	fmt.Printf("现在时间： %v\n", time.Now())
	time4 := time.NewTimer(time.Second * 4)
	time4.Reset(time.Second * 1)
	<-time4.C
	fmt.Printf("现在时间： %v\n", time.Now())
}

输出：
现在时间： 2022-07-10 15:36:03.7609956 +0800 CST m=+0.002148901
现在时间： 2022-07-10 15:36:04.776033 +0800 CST m=+1.017186301
```

timer被修改为了1s。

### 21.9 `golang`并发--Ticker

timer只执行一次，Ticker可以周期的执行

**实例**

```go
package main

import (
	"fmt"
	"time"
)

func main() {
	ticker := time.NewTicker(time.Second)
	counter := 1
	for _ = range ticker.C {
		fmt.Printf("ticker  time:%v\n", time.Now())
		counter++
		if counter >= 5 {
			break
		}
	}
	ticker.Stop()
}

输出：
ticker  time:2022-07-10 16:50:47.9508645 +0800 CST m=+1.010029201
ticker  time:2022-07-10 16:50:48.9524528 +0800 CST m=+2.011617501
ticker  time:2022-07-10 16:50:49.9577563 +0800 CST m=+3.016921001
ticker  time:2022-07-10 16:50:50.9513074 +0800 CST m=+4.010472101
```

**利用Ticker进行周期性的发送和接收**

```go
package main
import (
	"fmt"
	"time"
)

func main() {
	ticker := time.NewTicker(time.Second)
	chanInt := make(chan int)
	
    go func() {
		for _ = range ticker.C {
			select {
			case chanInt <- 1:
			case chanInt <- 2:
			case chanInt <- 3:
			}
		}
	}()

	var sum int = 0
	for v := range chanInt {
		fmt.Printf("收到: %v\n", v)
		sum += v
		if sum >= 10 {
			fmt.Printf("sum: %v\n", sum)
			break
		}
	}
}


输出：
收到: 2
收到: 3
收到: 1
收到: 3
收到: 3
sum: 12
```

### 21.10 `goalng`并发--原子变量的引入

**先看一个实例**

```go
package main

import (
	"fmt"
	"sync"
	"time"
)

var i = 10
var lock sync.Mutex

func add() {
	lock.Lock()
	i++
	fmt.Printf("i: %+v\n", i)
	lock.Unlock()
}

func sub() {
	lock.Lock()
	i--
	fmt.Printf("i: %+v\n", i)
	lock.Unlock()
}

func main() {
	for i := 0; i < 5; i++ {
		go add()
		go sub()
	}
	time.Sleep(time.Second * 2)
	fmt.Printf("i: %v\n", i)
}

输出：
i: 11
i: 10
i: 9
i: 10
i: 9
i: 10
i: 11
i: 10
i: 11
i: 10
i: 10
```

- 加锁代价比较耗时,需要上下文切换
- 针对基本数据类型,可以使用原子操作保证线程安全
- 原子操作在用户态就可以完成,因此性能比互斥锁要高

原子操作函数需要的是被操作值的指针，而不是这个值本身

**只要原子操作函数拿到了被操作值的指针**，就可以定位到存储该值的内存地址。只有这样，它们才能够通过底层的指令，准确地操作这个内存地址上的数据。

支持的类型
这些函数针对的数据类型并不多。但是，对这些类型中的每一个，

sync/atomic包都会有一套函数给予支持。这些数据类型有：`int32`、`int64`、`uint32`、`uint64`、`uintptr`，以及`unsafe`包中的`Pointer`。

不过，针对`unsafe.Pointer`类型，该包并未提供进行原子加法操作的函数。

**实例**

```go
package main

import (
	"fmt"
	"sync/atomic"
	"time"
)
var i int32 = 10

//cas: compare and swap
func add() {
	atomic.AddInt32(&i, 1)
	fmt.Printf("i: %v\n", i)
}
func sub() {
	atomic.AddInt32(&i, -1)
	fmt.Printf("i: %v\n", i)
}
func main() {
	for i := 0; i < 5; i++ {
		go sub()
		go add()
	}
	time.Sleep(time.Second)
	fmt.Printf("i: %v\n", i)
}

输出：
i: 12
i: 10
i: 11
i: 11
i: 10
i: 9
i: 10
i: 9
i: 10
i: 9
i: 10
```

#### 21.10.1 原子操作详解

`atomic`提供的原子操作能够确保任一时刻只有一个`goroutine`对变量进行操作，善用`atomic`能够避免程序中出现大量的锁操作。

atomic的常见操作：

- 增减操作
- 载入
- 比较并交换cas
- 交换
- 存储

下面就分别介绍这些操作

主要的作用就是在协程操作时候不需要再加

**增减操作**

------

`atomic`包提供了如下以Add为前缀的增减操作

```go
- func AddInt32(addr *int32,delta int32)(new int32)
- func AddInt64(addr *int64,delta int64)(new int64)
- func AddUint32(addr *uint32,delta uint32)(new uint32)
- func AddUint64(addr *uint64,delta uint64)(new uint64)
- func AddUintptr(addr *uintptr,delta uintptr)(new uintptr)
```

```go
package main

import (
	"fmt"
	"sync/atomic"
	"time"
)
//load and store
func las() {
	var i int32 = 77
	atomic.LoadInt32(&i) //read
	fmt.Printf("i: %v\n", i)

	atomic.SwapInt32(&i, 98)
	fmt.Printf("i: %v\n", i)
}

// cas compare and swap
func cas() {
	var i int32 = 100
	b := atomic.CompareAndSwapInt32(&i, 100, 200)
	fmt.Printf("i: %v\n", i)
	fmt.Printf("b: %v\n", b)
}

func main() {
	go las()
	go cas()

	time.Sleep(time.Second * 3)
}

输出：
i: 200
b: true
i: 77
i: 98
```

如果在`b := atomic.CompareAndSwapInt32(&i, 100, 200)`这个线程进行过程当中，有其他线程进来将变量的值修改了，这种情况下会操作失败，返回一个布尔类型的值：`false`

### *21.11 `Golang`并发--Context详解

**先看一个简单的例子，我们创建协程,构建携程在中的一个死循环**

```go
package main

import (
	"fmt"
	"time"
)

func main() {
	println("Contex...")
	go func() {
		for {
			fmt.Println("this is goroutine")
			time.Sleep(time.Second)
		}
	}()
	<-time.After(time.Second * 3)
	fmt.Println("end main")
}

输出：
Contex...
this is goroutine
this is goroutine
this is goroutine
end main
```

在这个代码中，主协程结束之后，子协程也结束了，而不是子协程自己结束的，子协程结束方法：

1. **借助`runtime`包中的`Goexit()`方法：**

``` go
package main

import (
	"fmt"
	"runtime"
	"time"
)

func main() {
	println("Contex...")
	go func() {
		for {
			fmt.Println("this is goroutine")
			time.Sleep(time.Second)
			runtime.Goexit()
		}
	}()
	<-time.After(time.Second * 5)

	fmt.Println("end main")

}

输出：
Contex...
this is goroutine
end main
```

2. **借助通道结束协程（外部信号）**

```go
package main

import (
	"fmt"
	"time"
)

func main() {
	println("Contex...")
	ch := make(chan bool)
	go func() {
		for {
			select {
			case <-ch:
				fmt.Println("我要结束了")
				return
			default:
				fmt.Println("我是协程")
			}
			fmt.Println("this is goroutine")
			time.Sleep(time.Second)
		}
	}()
	<-time.After(time.Second * 2)
	ch <- true
	<-time.After(time.Second * 5)

	fmt.Println("end main")

}

输出：
Contex...
我是协程
this is goroutine
我是协程
this is goroutine
我是协程
this is goroutine
我要结束了
end main
```

如果在协程中创建了子协程，问题就变得复杂起来了

**这就需要我们使用到go语言中的上下文：Context**

#### 21.11.1 WithCancel

```go
package main

import (
	"context"
	"fmt"
	"time"
)

func main() {
	println("Contex...")
	ctx, cf := context.WithCancel(context.Background())
	go TestCancel(ctx)
	<-time.After(time.Second * 5)
	cf()
	time.Sleep(time.Millisecond)
	fmt.Println("main结束")
}

func TestCancel(ctx context.Context) {
	for {
		select {
		case <-ctx.Done(): //在外界接收到cancel的时候，done会读到数据
			fmt.Println("主协程取消了，我是子协程，也同时结束了")
			return
		default:
			fmt.Println("我是子协程，我正在运行中...")
			time.Sleep(time.Second)
		}
	}
}

```

#### 21.11.2 WithDeadline

这个方法可以定义结合时间，指定存活多久

```go
package main

import (
	"context"
	"fmt"
	"time"
)

func main() {
	fmt.Println("main开始")
	ctx, _ := context.WithDeadline(context.Background(), time.Now().Add(time.Second*5))

	go testDeadline(ctx)

	time.Sleep(time.Second * 7)
	fmt.Println("main结束")
}

func testDeadline(ctx context.Context) {
	for {
		select {
		case <-ctx.Done():
			fmt.Println("我是子协程 我运行5秒就结束了")
			return
		default:
			fmt.Println("我是Deadline子协程，我正在执行中")
			time.Sleep(time.Second)
		}
	}
}

输出：
main开始
我是Deadline子协程，我正在执行中
我是Deadline子协程，我正在执行中
我是Deadline子协程，我正在执行中
我是Deadline子协程，我正在执行中
我是Deadline子协程，我正在执行中
我是子协程 我运行5秒就结束了
main结束
```

#### 21.11.3 WithTimeout

这个的使用方法和上面的`WithDeadline`差不多，**主要是时间格式不太一样**

```
package main

import (
	"context"
	"fmt"
	"time"
)

func main() {
	fmt.Println("main开始")
	ctx, _ := context.WithTimeout(context.Background(), time.Second*5)
	go testWithTimeout(ctx)
	time.Sleep(time.Second * 8)
	fmt.Println("main结束")
}

func testWithTimeout(ctx context.Context) {
	for {
		select {
		case <-ctx.Done():
			fmt.Println("我是timeout协程 我运行5秒就结束了")
			return
		default:
			fmt.Println("我是timeout协程正在执行中...")
			time.Sleep(time.Second)
		}
	}
}

输出：
main开始
我是timeout协程正在执行中...
我是timeout协程正在执行中...
我是timeout协程正在执行中...
我是timeout协程正在执行中...
我是timeout协程正在执行中...
我是timeout协程 我运行5秒就结束了
main结束
```

### 21.12 sync.Cond

### type Cond

- #### sync.Cond 的使用场景

  一句话总结：`sync.Cond` 条件变量用来协调想要访问共享资源的那些 goroutine，当共享资源的状态发生变化的时候，它可以用来通知被互斥锁阻塞的 goroutine。

  **`sync.Cond` 基于互斥锁/读写锁，它和互斥锁的区别是什么呢？**

  互斥锁 `sync.Mutex` 通常用来保护临界区和共享资源，条件变量 `sync.Cond` 用来协调想要访问共享资源的 `goroutine`。

  `sync.Cond` 经常用在多个 goroutine 等待，一个 goroutine 通知（事件发生）的场景。如果是一个通知，一个等待，使用互斥锁或 channel 就能搞定了。

  我们想象一个非常简单的场景：

  有一个协程在异步地接收数据，剩下的多个协程必须等待这个协程接收完数据，才能读取到正确的数据。在这种情况下，如果单纯使用 chan 或互斥锁，那么只能有一个协程可以等待，并读取到数据，没办法通知其他的协程也读取数据。

  这个时候，就需要有个全局的变量来标志第一个协程数据是否接受完毕，剩下的协程，反复检查该变量的值，直到满足要求。或者创建多个 channel，每个协程阻塞在一个 channel 上，由接收数据的协程在数据接收完毕后，逐个通知。总之，需要额外的复杂度来完成这件事。

  Go 语言在标准库 sync 中内置一个 `sync.Cond` 用来解决这类问题。

```go
type Cond struct {
    // 在观测或更改条件时L会冻结
    L Locker
    // 包含隐藏或非导出字段
}
```

Cond实现了一个条件变量，一个线程集合地，供线程等待或者宣布某事件的发生。

每个Cond实例都有一个相关的锁（一般是*Mutex或*RWMutex类型的值），它必须在改变条件时或者调用Wait方法时保持锁定。Cond可以创建为其他结构体的字段，Cond在开始使用后不能被拷贝。

#### func [NewCond](https://github.com/golang/go/blob/master/src/sync/cond.go?name=release#32)

```
func NewCond(l Locker) *Cond
```

使用锁l创建一个*Cond。

#### func (*Cond) [Broadcast](https://github.com/golang/go/blob/master/src/sync/cond.go?name=release#78)

```
func (c *Cond) Broadcast()
```

Broadcast唤醒所有等待c的线程。调用者在调用本方法时，建议（但并非必须）保持c.L的锁定。

#### func (*Cond) [Signal](https://github.com/golang/go/blob/master/src/sync/cond.go?name=release#70)

```
func (c *Cond) Signal()
```

Signal唤醒等待c的一个线程（如果存在）。调用者在调用本方法时，建议（但并非必须）保持c.L的锁定。

#### func (*Cond) [Wait](https://github.com/golang/go/blob/master/src/sync/cond.go?name=release#52)

```
func (c *Cond) Wait()
```

Wait自行解锁c.L并阻塞当前线程，在之后线程恢复执行时，Wait方法会在返回前锁定c.L。和其他系统不同，Wait除非被Broadcast或者Signal唤醒，不会主动返回。

因为线程中Wait方法是第一个恢复执行的，而此时c.L未加锁。调用者不应假设Wait恢复时条件已满足，相反，调用者应在循环中等待：

```go
c.L.Lock()
for !condition() {
    c.Wait()
}
... make use of condition ...
c.L.Unlock()
```

**使用实例**

- #### 生产者消费者模型

```go
package main

import (
	"fmt"
	"sync"
	"time"
)

type Store struct {
	DataCount int
	Max       int
	lock      sync.Mutex
	pCond     *sync.Cond
	cCond     *sync.Cond
}

type Producer struct{}

func (Producer) Produce(store *Store) {
	store.lock.Lock()
	defer store.lock.Unlock()
	if store.DataCount == store.Max {
		fmt.Println("生产者在等出货")
		store.pCond.Wait()
	}
	fmt.Println("生产+1")
	store.DataCount++
	store.cCond.Signal()
}

type Consumer struct{}

func (c Consumer) Consume(store *Store) {
	store.lock.Lock()
	defer store.lock.Unlock()
        if store.DataCount == 0 {
            fmt.Println("没货了，消费者在等")
            store.cCond.Wait()
        }
	fmt.Println("消费-1")
	store.DataCount--
	store.pCond.Signal()
}

func main() {
	s := &Store{
		Max: 10,
	}
	s.pCond = sync.NewCond(&s.lock)
	s.cCond = sync.NewCond(&s.lock)
	prodCount, consCount := 50, 50
	for i := 0; i < prodCount; i++ {
		go func() {
			for {
				time.Sleep(100 * time.Millisecond)
				Producer{}.Produce(s)
			}
		}()
	}
	for i := 0; i < consCount; i++ {
		go func() {
			for {
				time.Sleep(100 * time.Millisecond)
				Consumer{}.Consume(s)
			}
		}()
	}
	time.Sleep(1 * time.Second)
}

```



## 22. `golang`标准库

### 22.1 标准库OS模块

#### 22.1.1 文件目录相关

OS标准库实现了平台（操作系统）无关的编程接口：[Standard library - Go Packages](https://pkg.go.dev/std)

文件打开模式

```go
const (
    O_RDONLY int = syscall.O_RDONLY // 只读模式打开文件
    O_WRONLY int = syscall.O_WRONLY // 只写模式打开文件
    O_RDWR   int = syscall.O_RDWR   // 读写模式打开文件
    O_APPEND int = syscall.O_APPEND // 写操作时将数据附加到文件尾部
    O_CREATE int = syscall.O_CREAT  // 如果不存在将创建一个新文件
    O_EXCL   int = syscall.O_EXCL   // 和O_CREATE配合使用，文件必须不存在
    O_SYNC   int = syscall.O_SYNC   // 打开文件用于同步I/O
    O_TRUNC  int = syscall.O_TRUNC  // 如果可能，打开时清空文件
)
```

```go
package main
import (
	"fmt"
	"os"
	"time"
)

// 创建文件
func createFile() {
	f, err := os.Create("test.txt")
	if err != nil {
		fmt.Printf("err: %v\n", err)
	} else {
		fmt.Printf("f: %v\n", f)
	}
}

//创建目录
func creatDir() {
	//创建单个目录
	os.Mkdir("test0", os.ModePerm) // os.ModePerm为最高权限
	//创建多个级联目录
	err := os.MkdirAll("test1/a/b/c", os.ModePerm)
	if err != nil {
		fmt.Printf("err: %v\n", err)
	}
	fmt.Printf("err: %v\n", err)
}

//删除文件
func removeFile() {
	time.Sleep(time.Second * 3)
	os.Remove("test.txt")
}

//删除目录
func removeDir() {
	os.RemoveAll("test0")
	os.RemoveAll("test1")
}

//获得工作目录
func getWd() {
	dir, err := os.Getwd()
	fmt.Printf("dir: %v\n", dir)
	fmt.Printf("err: %v\n", err)
	// 更改目录
	os.Chdir("f:/")
	dir, err = os.Getwd()
	fmt.Printf("dir: %v\n", dir)
	fmt.Printf("err: %v\n", err)
}
// 获得临时目录
func tempDir() {
	s := os.TempDir()
	fmt.Printf("s: %v\n", s)
}
// 文件重命名
func reName() {
	os.Rename("test.txt", "test1.go")
}


func main() {
	// createFile()
	// creatDir()
	// removeFile()
	// removeDir()
	getWd()
    tempDir()
    reName()
}

输出：
dir: F:\GoCode\pro06
err: <nil>
dir: f:\
err: <nil>
s: C:\Users\Hud\AppData\Local\Temp
```

**文件的读写**

```go
package main

import (
	"fmt"
	"os"
	"time"
)
// 写文件
func writeFile() {
	os.WriteFile("test1.txt",
		[]byte(`hello from hud by golang
	Goodbye~ `), os.ModePerm)
}

// 读文件
func readFile() {
	time.Sleep(time.Second)
	f, err := os.ReadFile("test1.txt")
	//fmt.Printf("f: %s\n", f)
	fmt.Printf("f: %v\n", string(f[:]))
	fmt.Printf("err: %v\n", err)
}

func main() {
	writeFile()
	go readFile()
	time.Sleep(time.Second * 3)
}

输出：
f: hello from hud by golang
        Goodbye~
err: <nil>
```

#### 22.1.2 File文件读操作

和文件`File`结构体相关的文件**读操作**

```go
package main
import (
	"fmt"
	"os"
)

func openClosefile() {
	// 文件只能读
	f, _ := os.Open("test1.txt")
	fmt.Printf("%v\n", f.Name())
	// 根据第二个参数:设置读写或者没有该文件就进行创建、最高权限755
	f2, _ := os.OpenFile("test2.txt", os.O_RDWR|os.O_CREATE, 0755)
	fmt.Printf("f2: %v\n", f2.Name())

	err := f.Close()
	fmt.Printf("err: %v\n", err)
	err2 := f2.Close()
	fmt.Printf("err2: %v\n", err2)
}
func main() {
	openClosefile()
}

输出：
test1.txt
f2: test2.txt
err: <nil>
err2: <nil>
```

**创建文件**

```go
package main

import (
	"fmt"
	"os"
)
// 创建文件
func createFile() {
	//等价于 	os.OpenFile("name",os.O_RDWR|os.O_CREATE|os.O_TRUNC,0666)
	f, _ := os.Create("test3.txt")
	fmt.Printf("f.Name(): %v\n", f.Name())
	// 第一个参数 ，目录默认，Temp第二个参数 文件名前缀（看看下面创建出的临时文件）
	f2, _ := os.CreateTemp("", "temp")
	fmt.Printf("f2.Name(): %v\n", f2.Name())
}
func main() {
	createFile()
}

输出：
f.Name(): test3.txt
f2.Name(): C:\Users\Hud\AppData\Local\Temp\temp3224584296
```

**读文件**

```go
package main

import (
	"fmt"
	"os"
)
// 读文件
func readOps() {
	f, _ := os.Open("test1.txt")
	//创建缓冲区，把文件内容读进去
	buf := make([]byte, 10)
	n, _ := f.Read(buf)
	fmt.Printf("n: %v\n", n)
	fmt.Printf("string(buf): %v\n", string(buf))
}
func main() {
	// openClosefile()
	// createFile()
	readOps()
}

输出：
n: 10
string(buf): hello from
```

看到没有将文件内容读取完全，所以需要循环的来读。加一个for循环。

```go
// 循环读文件
func readOps() {
	f, _ := os.Open("test1.txt")

	for {
		//创建缓冲区，把文件内容读进去
		buf := make([]byte, 10)
		n, err := f.Read(buf)
		/* 	fmt.Printf("n: %v\n", n)
		fmt.Printf("string(buf): %v\n", string(buf)) */
		fmt.Println(string(buf))
		fmt.Printf("n: %v\n", n)
		if err == io.EOF {
			break
		}

	}
	f.Close()
}

输出：
hello from
n: 10
 hud by go
n: 10
lang
        Good
n: 10
bye~
n: 4

n: 0
```

#### 22.1.3 File文件写操作

介绍和`File`结构体相关的文件写操作。

```go
package main

import (
	"os"
)

func write() {
	// 不能使用open，不然文件就是只读的了
	// 打开读写权限，os.O_APPEND是添加方式写，第二次执行的时候会在后面添加
	f, _ := os.OpenFile("test.txt", os.O_RDWR|os.O_APPEND, 0755)
	f.Write([]byte(" Hello goalng!!"))
	f.Close()
}

//写字符串
func writeString() {
    // os.O_TRUNC表示覆盖原有文件内容
	f, _ := os.OpenFile("test.txt", os.O_RDWR|os.O_TRUNC, 0777)
	f.WriteString("hello java")
	f.Close()
}
// 指定位置开始写
func writeAt() {
	f, _ := os.OpenFile("test.txt", os.O_RDWR, 0777)
	f.WriteAt([]byte("this is from WriteAt"), 3)
	f.Close()
}
func main() {
	write()
}

输出：
helthis is from WriteAt(前面内容被覆盖掉了)
```

#### 22.1.4 进程相关操作

介绍`os`进程相关的操作

**获取进程Id**

```go
package main

import (
	"fmt"
	"os"
)

func getId() {
	// 获得当前正在运行的进程id
	fmt.Printf("os.Getpid(): %v\n", os.Getpid())
	//父id
	fmt.Printf("os.Getppid(): %v\n", os.Getppid())
}
func main() {
	getId()
}

输出：
os.Getpid(): 10740
os.Getppid(): 9316
```

**设置新的进程+开始一个新的进程**

```go
package main

import (
	"fmt"
	"os"
	"time"
)
func newProcess() {
	attr := &os.ProcAttr{
		// files指定新进程继承的活动文件对象
		// 前三个分别为：标准输入、标准输出、标准错误输出
		Files: []*os.File{os.Stdin, os.Stdout, os.Stderr},
		//新的环境变量
		Env: os.Environ(),
	}
	// 开始一个新的进程
	p, err := os.StartProcess("C:\\Windows\\System32\\notepad.exe",
		[]string{"C:\\Windows\\System32\\notepad.exe", "F:\\a.txt"}, attr)
	if err != nil {
		fmt.Printf("err: %v\n", err)
	}
	fmt.Println(p)
	fmt.Println("进程id:", p.Pid)

	// 通过进程id查找进程

	p2, _ := os.FindProcess(p.Pid)
	fmt.Println(p2)

	//等待10秒 执行函数
	time.AfterFunc(time.Second*10, func() {
		//向p进程发送退出信号
		p.Signal(os.Kill)
	})

	// 等待进程p的退出，返回进程状态
	ps, _ := p.Wait()
	fmt.Println(ps.String())
}
func main() {
	newProcess()
}

输出：
&{10452 888 0 {{0 0} 0 0 0 0}}
进程id: 10452
&{10452 920 0 {{0 0} 0 0 0 0}}
exit status 1
```

#### 22.1.5 环境相关方法

在`golang`里可以很方便轻松的设置系统的环境变量

```go
package main

import (
	"fmt"
	"os"
)

func main() {
	// 获得所有环境变量
	s := os.Environ()
	fmt.Printf("s: %v\n", s)

	// 获得某个特定环境变量
	s2 := os.Getenv("GOPATH")
	fmt.Printf("s2: %v\n", s2)

	//设置环境变量
	os.Setenv("env1", "env2") //前面是key 后面是value
	// func os.Setenv(key string, value string) error
	s2 = os.Getenv("aaa")
	fmt.Printf("s2: %v\n", s2)
	fmt.Println("--------")

	//查找  func os.LookupEnv(key string) (string, bool)
	s3, b := os.LookupEnv("env1")
	fmt.Printf("b: %v\n", b)
	fmt.Printf("s3: %v\n", s3)

	// 替换
	os.Setenv("NAME", "gopher")
	os.Setenv("BURROW", "/usr/gopher")

	fmt.Println(os.ExpandEnv("$NAME lives in ${burrow}."))

	//清空环境变量
	os.Clearenv()
}
```

#### os包的File方法

- #### func [Create](https://github.com/golang/go/blob/master/src/os/file.go?name=release#247)

```
func Create(name string) (file *File, err error)
```

Create采用模式0666（任何人都可读写，不可执行）创建一个名为name的文件，如果文件已存在会截断它（为空文件）。如果成功，返回的文件对象可用于I/O；对应的文件描述符具有O_RDWR模式。如果出错，错误底层类型是*PathError。

- #### func [Open](https://github.com/golang/go/blob/master/src/os/file.go?name=release#238)

```
func Open(name string) (file *File, err error)
```

Open打开一个文件用于读取。如果操作成功，返回的文件对象的方法可用于读取数据；对应的文件描述符具有O_RDONLY模式。如果出错，错误底层类型是*PathError。

- #### func [OpenFile](https://github.com/golang/go/blob/master/src/os/file_unix.go?name=release#76)

```
func OpenFile(name string, flag int, perm FileMode) (file *File, err error)
```

`OpenFile`是一个更一般性的文件打开函数，大多数调用者都应用Open或Create代替本函数。它会使用指定的选项（如O_RDONLY等）、指定的模式（如0666等）打开指定名称的文件。如果操作成功，返回的文件对象可用于I/O。如果出错，错误底层类型是*PathError。

- #### `func` (*File) [`WriteString`](https://github.com/golang/go/blob/master/src/os/file.go?name=release#195)

```
func (f *File) WriteString(s string) (ret int, err error)
```

WriteString类似Write，但接受一个字符串参数。

- #### func (*File) [WriteAt](https://github.com/golang/go/blob/master/src/os/file.go?name=release#158)

```
func (f *File) WriteAt(b []byte, off int64) (n int, err error)
```

WriteAt在指定的位置（相对于文件开始位置）写入len(b)字节数据。它返回写入的字节数和可能遇到的任何错误。如果返回值n!=len(b)，本方法会返回一个非nil的错误。

### 22.2  标准库io模块

Go语言中，为了方便开发者使用，将I/O操作封装在了如下几个包中：

- io为I/O原语(I/O primitives)提供基本的接口
- io/ioutil封装一些实用的I/O函数
- `fmt`实现格式化I/O，类似C语言中的`printf`和`scanf`
- `bufio`实现带缓冲I/O

**`io` -- 基本的IO接口**

在`io`包中最重要的两个接口：`Reader`和`Writer`接口。本章所提到的各种I/O包，都跟这两个接口有关，也就是说只要实现了这两个接口，他就有了I/O的功能

**Reader接口**

```go
type Reader interface{
	Read(p []byte)(n int,err error)		// 读到字节数组中，返回读取的字节数和错误
}
```

**Writer接口**

```go
type Writer interface{
	Read(p []byte)(n int,err error)		// 将字节数组写到对应的文件中去，返回写的字节数和错误
}
```

**哪些类型实现了Reader和Writer接口**

```go
os.File 同时实现了 io.Reader 和 io.Writer
strings.Reader实现了 io.Reader
bufio.Reader/Writer 分别实现了io.Reader和io.Writer
bytes.Buffer 同时实现了io.Reader 和 io.Writer
bytes.Reader 实现了 io.Reader
compress/gzip.Reader/Writer分别实现了io.Reader和io.Writer
crypto/cipher.StreamReader/StreamWriter 分别实现了io.Reader和io.Writer
crypto/tls.Conn 同时实现了io.Reader 和 io.Writer
encoding/csv.Reader/Writer 分别实现了io.Reader和io.Writer
```

```go
package main

import (
	"fmt"
	"strings"
)

func main() {
	r := strings.NewReader("Hello world!") // 返回一个reader
	buf := make([]byte, 15  )                // 创建一个字节类型的缓冲区
	r.Read(buf)                            // 将reader读到缓冲区里
	fmt.Printf("string(buf): %v\n", string(buf))
}

```

#### 22.2.1 `golang`标准库`ioutil`包

封装一些实用的I/O函数

| 名称        | 作用                                                       |
| ----------- | ---------------------------------------------------------- |
| `ReadAll`   | 读取数据，返回读取的字节slice                              |
| `ReadDir`   | 读取一个目录，返回目录入口数组`[]os.FileInfo`              |
| `ReadFile`  | 读一个文件，返回文件内容（字节slice）                      |
| `WriteFile` | 根据文件路径，写入字节slice                                |
| `TempDir`   | 在一个目录中创建指定前缀名的临时目录，返回新临时目录的路径 |
| `TempFIle`  | 在一个目录中创建指定前缀名的临时文件，返回`os.file`        |

实例展示

- 复制文件内容到另一个文件

- ```go
  package main
  import "io/ioutil"
  func main() {
    b, _ := ioutil.ReadFile("F:/GoCode/package-os/readme.md")
    ioutil.WriteFile("F:/GoCode/package-os/test.md", b, 0666)
  }
  ```

  

```go
package main

import (
	"fmt"
	"io/ioutil"
	"strings"
)

func main() {
	r := strings.NewReader("hello world") //返回一个reader
	b, err := ioutil.ReadAll(r)           // 返回一个字节数组和一个error
	if err != nil {
		fmt.Printf("err: %v\n", err)
	}
	fmt.Printf("string(b): %v\n", string(b))
    
    // 读取文件中内容
	f, _ := os.Open("abc.txt")
	b, _ := ioutil.ReadAll(f)
	fmt.Printf("string(b): %v\n", string(b))
}

输出：
string(b): hello world
string(b): hello from hud!
```

用for range循环读取当前目录的文件

```go
package main

import (
	"fmt"
	"io/ioutil"
)

func readDir() {
	fi, _ := ioutil.ReadDir(".")
	for _, v := range fi {
		fmt.Printf("v.Name(): %v\n", v.Name())
	}
}
func main() {
	readDir()
}

输出：
v.Name(): .vs
v.Name(): mypro
v.Name(): package-io
v.Name(): package-os
v.Name(): pro04
v.Name(): pro05
v.Name(): project01
v.Name(): project02
v.Name(): project03
```

**文件内容写入**

```go
func writeFile() {
	message := []byte("I am the chosen one!")
	err := ioutil.WriteFile("abc.txt", message, 0644)
	if err != nil {
		fmt.Printf("err: %v\n", err)
	}
}
```

**创建临时文件**

```go
// 创建临时文件
func createTempfile() {
	message := []byte("good good study!")
	f, err := ioutil.TempFile("", "example")
	if err != nil {
		log.Fatal(err)
	}
	fmt.Printf("f.Name(): %v\n", f.Name())
	_, err2 := f.Write(message)
	if err != nil {
		log.Fatal(err2)
	}
}

func main() {
	createTempfile()
}

输出：
f.Name(): C:\Users\Hud\AppData\Local\Temp\example2207452904
```



#### 22.2.2 拷貝文件實例

```go
// 将一个文件(图片/电影/MP3)拷贝到另外一个文件中...
// io包 func Copy(dst Writer,src Reader)(written int64,err error) written为拷贝字节数

package main

import (
	"bufio"
	"fmt"
	"io"
	"os"
)

func main() {

	wrriten, err := Copyfile("F:/1/aaa.jpg", "F:/GoCode/aaa.jpg")
	if err != nil {
		fmt.Printf("err: %v\n", err)
	}
	fmt.Printf("wrriten: %v\n", wrriten)
}

func Copyfile(dst string, src string) (wrriten int64, err error) {
	source, err := os.Open(src)
	if err != nil {
		fmt.Printf("err-open: %v\n", err)
	}
	defer source.Close()
	// 构建一个reader
	r := bufio.NewReader(source) // *bufio.Reader

	//打开目标文件构建writer,有可不存在，就要创建， 所以不能使用os.Open打开
	dest, err2 := os.OpenFile(dst, os.O_WRONLY|os.O_CREATE, 0666)
	if err2 != nil {
		fmt.Printf("err-write: %v\n", err2)
	}
	w := bufio.NewWriter(dest) // *bufio.Writer
	defer dest.Close()

	return io.Copy(w, r)

}

```



### 22.3 标准库bufio模块

**`bufio`**

bufio实现了有缓冲的I/O，他包装一个io.Reader或io.Writer接口对象，创建了另外一个也实现该接口，且同时还提供了缓冲和一些文本I/O的帮助函数的对象。

**常量**

```go
const (
	deeafultSize = 4096			// 默认缓冲区大小 4096字节
)
```

**进行读取**

```go
package main

import (
	"bufio"
	"fmt"
	"strings"
)

func main() {
	r := strings.NewReader("hello world from hud!")
	r2 := bufio.NewReader(r)    //创建一个新的reader，将r进行封装
	s, _ := r2.ReadString('\n') //以换行作为结尾
	fmt.Printf("s: %v\n", s)
}

输出：
s: hello world from hud!
```

或者对文件进行读取：

```go
package main

import (
	"bufio"
	"fmt"
	"os"
)

func main() {
	f, _ := os.Open("a.txt")
	defer f.Close()
	r := bufio.NewReader(f)
	s, _ := r.ReadString('\n')
	fmt.Printf("s: %v\n", s)
}

输出：
s: ABCDEFGHIJKLMNOPQRST
```

**Reset：丢弃缓冲中的数据，清除任何错误，将b重设为其下层从r读取数据**

```go
package main

import (
	"bufio"
	"fmt"
	"strings"
)

func main() {
	s := strings.NewReader("ABCDEFG")
	str := strings.NewReader("123456")
	r := bufio.NewReader(s)		// 读入缓冲区
	s2, _ := r.ReadString('\n')
	fmt.Printf("s2: %v\n", s2)
	r.Reset(str)
	s3, _ := r.ReadString('\n')
	fmt.Printf("s3: %v\n", s3)
}

输出：
s2: ABCDEFG
s3: 123456
```

#### 22.3.1 type Reader

**`func (*Read)ReadByte`**

```go
func (b *Reader) ReadByte() (c byte , err error)
```

ReadByte读取并返回一个字节，如果没有可用的数据，会返回错误

**`func (*Read)Unreadbyte`**

```go
func (b *Reader) UnreadByte() error
```

UnreadByte吐出最近一次读取操作读取的最后一个字节（只能吐出最后一个，多次调用会出问题）

```go
func test() {
	// 每次读取一个字节
	s := strings.NewReader("ABCDEFG")
	r := bufio.NewReader(s)

	b, _ := r.ReadByte()
	fmt.Printf("b: %c\n", b)

	b, _ = r.ReadByte()
	fmt.Printf("b: %c\n", b)

	r.UnreadByte() // 吐出一个字符 还是读前一个字节
	b, _ = r.ReadByte()
	fmt.Printf("b: %c\n", b)
}

输出：
b: A
b: B
b: B
```

**`func (*Read) ReadRune`**

```go
func (b *Reader) ReadRune() (r rune, size int,err error)
```

`ReadRune`读取一个`utf-8`编码的`unicode`码值，返回该码值、其编码长度和可能的错误。如果`utf-8`编码非法，读取位置只移动一个字节，返回`U+FFFD`。返回值size为1而err为nil。如果没有可用的数据，会返回错误

**`func (*Read) UnreadRune`**

```go
func (b *Reader) UnreadRune() error
```

`UnreadRune`吐出最近一次`ReadRune`调用读取的`unicode`码值，如果最近一次读取不是调用的`ReadRune`会返回错误。

```go
package main

import (
	"bufio"
	"fmt"
	"strings"
)
func testReadRune() {
	s := strings.NewReader("你好，世界！来自齐天宇")
	r := bufio.NewReader(s)

	r2, size, _ := r.ReadRune()
	fmt.Printf("r2: %c size:%v \n", r2, size)

	r.UnreadRune()
	r3, size2, _ := r.ReadRune()
	fmt.Printf("r3: %c size2: %v\n", r3, size2)
}

func main() {
		testReadRune()
}

输出：
r2: 你 size:3 
r3: 你 size2: 3
```

**`func (*Reader)ReadLine`**

```go
func (b *Reader) ReadLine() (line []byte,isPrefix bool,err error)
```

读一行的时候，遇到了"\n"代表是换行，如果该行内容过多无法容纳，将`isPrefix`置为true（也就是说后面的内容就被扔掉了，只读取了该行的一个前缀）

```go
func testReadLine() {
	f, _ := os.Open("a.txt")
	r := bufio.NewReader(f)
	w, isPrefix, _ := r.ReadLine()
	fmt.Printf("w: %s , isPrefix: %v\n", w, isPrefix)
	w, isPrefix, _ = r.ReadLine()
	fmt.Printf("w: %s , isPrefix: %v\n", w, isPrefix)
	w, isPrefix, _ = r.ReadLine()
	fmt.Printf("w: %s , isPrefix: %v\n", w, isPrefix)
}

输出：
w: ABCDEFGHIJKLMNOPQRST , isPrefix: false
w: 123123 , isPrefix: false
w: 齐天宇很帅 , isPrefix: false
```

**`func (*Reader)ReadSlice`**

```go
func (*b Reader) ReadSlice(delim byte) (line []byte,err error)
```

`ReadSlice()`一直读取直到遇到`deliem`字节，返回缓冲里的包含已读取的数据和`deliem`字节的切片。该返回值只在下一次读取操作之前合法。

```go
package main

import (
	"bufio"
	"fmt"
	"strings"
)

func main() {
	s := strings.NewReader("ABC,DEF,GHI,JKL")
	r := bufio.NewReader(s)

	w, _ := r.ReadSlice(',')
	fmt.Printf("w: %q\n", w)

	w, _ = r.ReadSlice(',')
	fmt.Printf("w: %q\n", w)

	w, _ = r.ReadSlice(',')
	fmt.Printf("w: %q\n", w)
}

输出：
w: "ABC,"
w: "DEF,"
w: "GHI,"
```

**`func (b *Reader) ReadString`**

```go
func (b *Reader) ReadString(delim byte) (line string,err error)
```

`ReadString`读取直到第一次遇到`delim`字节，返回一个包含已读取的数据和`delim`字节的字符串。

```go
func ReadString() {
	s := strings.NewReader("ABC DEF GHI JKL")
	r := bufio.NewReader(s)
	for i := 0; i < 4; i++ {
		s2, _ := r.ReadString(' ')
		fmt.Printf("s2: %q\n", s2)
	}
}


输出:
s2: "ABC "
s2: "DEF "
s2: "GHI "
s2: "JKL"
```

**`func (*Reader) WriteTo`**

```go
func (b *Reader) WriteTo(w io.Writer) (n int64,err error)
```

WriteTo方法实现了io.WriteTo接口

```go
func writeTo() {
	s := strings.NewReader("ABCDEFGHIJKLMN")
	r := bufio.NewReader(s)
	b := bytes.NewBuffer(make([]byte, 0))

	r.WriteTo(b)
	fmt.Printf("b: %q\n", b)
}
func main() {
	writeTo()
}

输出：
b: "ABCDEFGHIJKLMN"
```

**写入文件**

```go
func writeTo2() {
	f, _ := os.OpenFile("a.txt", os.O_RDWR, 0777)
	s := strings.NewReader("hhhhhhhhhh")
	r := bufio.NewReader(s)
	r.WriteTo(f)
}
```

- ### Reader结构体的方法

- #### func [NewReader](https://github.com/golang/go/blob/master/src/bufio/bufio.go?name=release#61)

```
func NewReader(rd io.Reader) *Reader
```

NewReader创建一个具有默认大小缓冲、从r读取的*Reader。

- #### func [NewReaderSize](https://github.com/golang/go/blob/master/src/bufio/bufio.go?name=release#46)

```
func NewReaderSize(rd io.Reader, size int) *Reader
```

NewReaderSize创建一个具有最少有size尺寸的缓冲、从r读取的*Reader。如果参数r已经是一个具有足够大缓冲的* Reader类型值，会返回r。

- #### func (*Reader) [Reset](https://github.com/golang/go/blob/master/src/bufio/bufio.go?name=release#67)

```
func (b *Reader) Reset(r io.Reader)
```

Reset丢弃缓冲中的数据，清除任何错误，将b重设为其下层从r读取数据。

- #### func (*Reader) [Buffered](https://github.com/golang/go/blob/master/src/bufio/bufio.go?name=release#261)

```
func (b *Reader) Buffered() int
```

Buffered返回缓冲中现有的可读取的字节数。

- #### func (*Reader) [Peek](https://github.com/golang/go/blob/master/src/bufio/bufio.go?name=release#123)

```
func (b *Reader) Peek(n int) ([]byte, error)
```

Peek返回输入流的下n个字节，而不会移动读取位置。返回的[]byte只在下一次调用读取操作前合法。如果Peek返回的切片长度比n小，它也会返会一个错误说明原因。如果n比缓冲尺寸还大，返回的错误将是ErrBufferFull。

- #### func (*Reader) [Read](https://github.com/golang/go/blob/master/src/bufio/bufio.go?name=release#153)

```
func (b *Reader) Read(p []byte) (n int, err error)
```

Read读取数据写入p。本方法返回写入p的字节数。本方法一次调用最多会调用下层Reader接口一次Read方法，因此返回值n可能小于len(p)。读取到达结尾时，返回值n将为0而err将为io.EOF。

- #### func (*Reader) [ReadByte](https://github.com/golang/go/blob/master/src/bufio/bufio.go?name=release#193)

```
func (b *Reader) ReadByte() (c byte, err error)
```

ReadByte读取并返回一个字节。如果没有可用的数据，会返回错误。

- #### func (*Reader) [UnreadByte](https://github.com/golang/go/blob/master/src/bufio/bufio.go?name=release#208)

```
func (b *Reader) UnreadByte() error
```

UnreadByte吐出最近一次读取操作读取的最后一个字节。（只能吐出最后一个，多次调用会出问题）

- #### func (*Reader) [ReadRune](https://github.com/golang/go/blob/master/src/bufio/bufio.go?name=release#228)

```go
func (b *Reader) ReadRune() (r rune, size int, err error)
```

ReadRune读取一个utf-8编码的unicode码值，返回该码值、其编码长度和可能的错误。如果utf-8编码非法，读取位置只移动1字节，返回U+FFFD，返回值size为1而err为nil。如果没有可用的数据，会返回错误。

- #### func (*Reader) [UnreadRune](https://github.com/golang/go/blob/master/src/bufio/bufio.go?name=release#250)

```go
func (b *Reader) UnreadRune() error
```

UnreadRune吐出最近一次ReadRune调用读取的unicode码值。如果最近一次读取不是调用的ReadRune，会返回错误。（从这点看，UnreadRune比UnreadByte严格很多）

- #### func (*Reader) [ReadLine](https://github.com/golang/go/blob/master/src/bufio/bufio.go?name=release#325)

```go
func (b *Reader) ReadLine() (line []byte, isPrefix bool, err error)
```

ReadLine是一个低水平的行数据读取原语。大多数调用者应使用ReadBytes('\n')或ReadString('\n')代替，或者使用Scanner。

ReadLine尝试返回一行数据，不包括行尾标志的字节。如果行太长超过了缓冲，返回值isPrefix会被设为true，并返回行的前面一部分。该行剩下的部分将在之后的调用中返回。返回值isPrefix会在返回该行最后一个片段时才设为false。返回切片是缓冲的子切片，只在下一次读取操作之前有效。ReadLine要么返回一个非nil的line，要么返回一个非nil的err，两个返回值至少一个非nil。

返回的文本不包含行尾的标志字节（"\r\n"或"\n"）。如果输入流结束时没有行尾标志字节，方法不会出错，也不会指出这一情况。在调用ReadLine之后调用UnreadByte会总是吐出最后一个读取的字节（很可能是该行的行尾标志字节），即使该字节不是ReadLine返回值的一部分。

- #### func (*Reader) [ReadSlice](https://github.com/golang/go/blob/master/src/bufio/bufio.go?name=release#273)

```go
func (b *Reader) ReadSlice(delim byte) (line []byte, err error)
```

ReadSlice读取直到第一次遇到delim字节，返回缓冲里的包含已读取的数据和delim字节的切片。该返回值只在下一次读取操作之前合法。如果ReadSlice放在在读取到delim之前遇到了错误，它会返回在错误之前读取的数据在缓冲中的切片以及该错误（一般是io.EOF）。如果在读取到delim之前缓冲就被写满了，ReadSlice失败并返回ErrBufferFull。因为ReadSlice的返回值会被下一次I/O操作重写，调用者应尽量使用ReadBytes或ReadString替代本法功法。当且仅当ReadBytes方法返回的切片不以delim结尾时，会返回一个非nil的错误。

- #### func (*Reader) [ReadBytes](https://github.com/golang/go/blob/master/src/bufio/bufio.go?name=release#367)

```go
func (b *Reader) ReadBytes(delim byte) (line []byte, err error)
```

ReadBytes读取直到第一次遇到delim字节，返回一个包含已读取的数据和delim字节的切片。如果ReadBytes方法在读取到delim之前遇到了错误，它会返回在错误之前读取的数据以及该错误（一般是io.EOF）。当且仅当ReadBytes方法返回的切片不以delim结尾时，会返回一个非nil的错误。

- #### func (*Reader) [ReadString](https://github.com/golang/go/blob/master/src/bufio/bufio.go?name=release#415)

```go
func (b *Reader) ReadString(delim byte) (line string, err error)
```

ReadString读取直到第一次遇到delim字节，返回一个包含已读取的数据和delim字节的字符串。如果ReadString方法在读取到delim之前遇到了错误，它会返回在错误之前读取的数据以及该错误（一般是io.EOF）。当且仅当ReadString方法返回的切片不以delim结尾时，会返回一个非nil的错误。

- #### func (*Reader) [WriteTo](https://github.com/golang/go/blob/master/src/bufio/bufio.go?name=release#422)

```go
func (b *Reader) WriteTo(w io.Writer) (n int64, err error)
```

WriteTo方法实现了io.WriterTo接口。



#### 22.3.2 type Writer

```
type Writer struct {
	err error
	buf []byte
	n int
	wr io.writer
}
```

```go
package main

import (
	"bufio"
	"os"
)

func testwriter() {
	f, _ := os.OpenFile("a.txt", os.O_RDWR|os.O_APPEND, 0777)
	w := bufio.NewWriter(f)
	defer f.Close()
	w.WriteString("Hud is your god!")
	w.Flush()
}
func main() {
	testwriter()
}

```

**`func NewWriter`**

```go
func NewWriter (w io.Writer) *Writer
```

创建一个具有默认大小缓冲、写入w的*Writer。NewWriter()等于NewWriterSize(wr,4096)

**`func NewWriterSize`**

```go
func NewWriterSize(w io.Writer,size int) *Writer
```

NewWriterSize创建一个具有最少有size尺寸的缓冲、写入w的Writer。

**`func (*Writer)Reset`**

```
func (*Writer) Reset(w io.Writer)
```

Reset丢弃缓冲区中的数据，清除任何错误，将b重设，将其输出写入w

```go
func testReset() {
	b := bytes.NewBuffer(make([]byte, 0))
	w := bufio.NewWriter(b)
	w.WriteString("Hud is your god!")
	c := bytes.NewBuffer(make([]byte, 0))
	w.Reset(c)
	w.WriteString("Qty is your god!")
	w.Flush() 		//如果不flush，内容就被
	fmt.Println(b)
	fmt.Println(c)
}

输出：

Qty is your god!
```

只能看到第二句，这是因为第一句已经被Reset掉了

**`func (*Writer) Flush`**

flush方法将缓冲中的数据写入下层的io.Writer接口

#### 22.3.3 type Scanner

Scanner类型提供了方便的读取数据接口。

**`func NewScanner()`**

```go
func NewScanner(r io.Reader) *Scanner
```

NewScanner创建并返回一个从r读取数据的Scanner，默认的分隔函数是ScanLines

**`func (*Scanner) Scan`**

```go
func (s *Scanner) Scan() bool
```

Scan()方法获取当前位置的token（该token可以通过Bytes或Text方法获得），并让Scanner的扫描位置移动到下一个token，当扫描因为抵达输入流结尾或者遇到错误而停止时，本方法会返回false，在Scan方法返回false后，Err方法将返回扫描时遇到的任何错误，除非是`io.EOF`，此时Err会返回nil。

```go
package main
import (
	"bufio"
	"fmt"
	"strings"
)

func testscan() {
	s := strings.NewReader("ABC DEF GHI JKL")
	s2 := bufio.NewScanner(s) // 根据这个reader创建scanner
	s2.Split(bufio.ScanWords) // 根据words进行拆分 以空格作为分隔
	for s2.Scan() {
		fmt.Println(s2.Text())
	}
}

func main() {
	testscan()
}

输出：
ABC
DEF
GHI
JKL
```



### 22.4 标准库log模块

#### log简介

------

`golang`内置了`log`包，实现简单的日志服务，通过调用log包的函数，可以实现简单的日志打印功能。

#### log使用

------

`log`包中有3个系列的日志打印函数，分别为：`print`、`panic`和`fatal`

| 函数系列 | 作用                                                    |
| -------- | ------------------------------------------------------- |
| print    | 单纯打印日志                                            |
| panic    | 打印日志，抛出panic异常(defer函数会执行)                |
| fatal    | 打印日志，强制结束程序`(os.Exit(1))`，defer函数不会执行 |

**实例**

```go
package main

import "log"

func main() {
	log.Print("log")
	log.Printf("my log is %d", 98)
	name := "Hud"
	age := 24
	log.Println(name, age)
}

输出：
2022/07/20 14:08:10 log
2022/07/20 14:08:10 my log is 98
2022/07/20 14:08:10 Hud 24
```

**panic使用实例**

```go
package main

import (
	"fmt"
	"log"
)

func testpanic() {
	defer fmt.Println("这是defer函数")
	log.Panic("这里就不往下执行了")
	fmt.Println(">>>end<<<")
}

func main() {
	testpanic()
}
输出：
2022/07/20 14:31:12 这里就不往下执行了
这是defer函数
panic: 这里就不往下执行了

goroutine 1 [running]:
log.Panic({0xc0000cdf20?, 0x0?, 0x1e2f2c40598?})
        Q:/Golang-SDK/src/log/log.go:385 +0x65
main.testpanic()
        f:/GoCode/package-io/test-log.go:18 +0x94
main.main()
        f:/GoCode/package-io/test-log.go:23 +0x17
exit status 2
```

看到panic后面的语句并没有被执行，但是defer语句被执行了。

**再来看看Fatal**

```go
package main

import (
	"fmt"
	"log"
)
func testfatal() {
	defer fmt.Println("这是defer函数")
	log.Fatal("这里就不往下执行了")
	fmt.Println(">>>end<<<")
}

func main() {
    testfatal()		//通过os.Exit(1) 方式退出
}

输出：
2022/07/20 15:01:25 这里就不往下执行了
exit status 1
```

#### log配置

**标准log配置**

默认情况下log只会打印出时间，但是实际情况下我们可能还需要获取文件名、行号等信息。log包提供给我们定制的接口：

​	log包提供两个标准log配置的相关方法：

```go
func Flags() int 			//返回标准log输出配置
func SetFlags(flga int)		//设置标准log输出配置
```

**flag参数**

```go
const (
	Ldate         = 1 << iota     // 日期: 2009/01/23
	Ltime                         // 时间: 01:23:23
	Lmicroseconds                 // 微妙级别的时间: 01:23:23.123123.（用于增强Ltime位）
	Llongfile                     // 文件全路径名+行号: /a/b/c/d.go:23
    Lshortfile                    // 文件名+行号: d.go:23. (会覆盖掉Llongfile)
	LUTC                          // 使用UTC时间
	Lmsgprefix   				  // 将“前缀”从行的开头移动到消息的前面
	LstdFlags     = Ldate | Ltime // 标准Logger的初始值
```

**标准日志配置实例**

```go
func setlog() {
	i := log.Flags()
	fmt.Printf("i: %v\n", i)
	log.SetFlags(log.Ldate | log.Ltime | log.Llongfile)
	log.Print("Log")
}

func main() {
	// testfatal()
	setlog()
}

输出：
i: 3
2022/07/20 15:37:00 f:/GoCode/package-io/test-log.go:31: Log
```

**日志前缀配置**

`log`包提供两个日志前缀配置的相关函数：

```go
func Prefix() string 				//返回日志的前缀配置
func SetPrefix(prefix string)		// 设置日志前缀
```

**日志前缀设置实例**

```go
func LogInit() {
	i := log.Flags()
	fmt.Printf("i: %v\n", i)
	log.SetPrefix("LogPrefix")
	log.SetFlags(log.Ldate | log.Ltime | log.Llongfile)

}
func main() {
	LogInit()
	log.Print("Logi: 3")
}

输出：
LogPrefix2022/07/20 15:50:46 f:/GoCode/package-io/test-log.go:39: Log
```

**日志输出位置配置**

前面介绍的都是将日志输出到控制台上去，`Golang`的`log`包还支持将日志输出到文件中，`log`包提供了`func SetOutput(w io.Writer)`函数，将日志输出到文件中。

```go
func LogInit() {
	log.SetFlags(log.Ldate | log.Ltime | log.Llongfile)
	//a.log：只读、追加、没有就创建
	f, err := os.OpenFile("a.log", os.O_WRONLY|os.O_APPEND|os.O_CREATE, 0664)
	if err != nil {
		log.Fatal("日志文件错误")
	}
	log.SetOutput(f)
}

func main() {
	// testfatal()
	// setlog()
	LogInit()
	log.Print("Log")
}

输出：
2022/07/20 16:21:05 f:/GoCode/package-io/test-log.go:43: Log
```

**自定义Logger**

`log`包为我们提供了内置函数，让我们能自定义logger，从效果上看，就是将上面的标准日志配置、日志前缀配置和日志输出位置配置整合到了一个函数中，是的日志配置显得不那么繁琐

`log`包中提供了`func New(out io.Writer , prefix string , flag int) *Logger`函数来实现自定义logger

**示例**

```go
func Initfunc() {
	f, err := os.OpenFile("aaa.log", os.O_CREATE|os.O_APPEND|os.O_WRONLY, 0644)
	if err != nil {
		log.Panic("Failed to Open log file")
	}
	logger = log.New(f, "LogPrefix:", log.Ldate|log.Ltime|log.Llongfile)

}
func main() {
	// testfatal()
	// setlog()
	// LogInit()
	Initfunc()
	logger.Print("log<<<")
}

输出：
（创建aaa.log文件）
2022/07/20 16:21:05 f:/GoCode/package-io/test-log.go:43: Log
```

### 22.5 标准库`builtin`模块

`builtin`包提供了一些类型声明、变量和常量声明、还有一些便利函数。这个包不需要导入。这些变量和函数就可以直接使用。

#### 常用函数

------

##### **append**

```go
func append(slice []Type, elems ...Type) []Type

slice = append(slice , elem1 , elem2) // 直接在slice后面添加单个元素，添加元素类型可以slice不同
slice = append(slice, anotherslice...)	//  直接将另外一个slice添加到slice后面，但其本质还是将anotherSlice中的元素一个一个添加到slice中，和第一种方法也是类似
```

**实例**

```go
package main

import "fmt"

func main() {
	s1 := []int{1, 2, 3}
	i := append(s1, 4)
	fmt.Printf("i: %v\n", i)

	s2 := []int{5, 6, 7}
	i2 := append(s1, s2...)
	fmt.Printf("i2: %v\n", i2)
}

输出：
i: [1 2 3 4]
i2: [1 2 3 5 6 7]
```

##### **Len**

------

 返回：数组、切片、字符串、通道的长度

实例

```go
package main

import "fmt"
func testlen() {
	s1 := "hello from Hud"
	i := len(s1)
	fmt.Printf("i: %v\n", i)

	s2 := []int{1, 2, 3}
	i2 := len(s2)
	fmt.Printf("i2: %v\n", i2)
}

func main() {
	testlen()
}

输出：
i: 14
i2: 3
```

##### **`print` 、`println`**

打印输出到控制台

**实例**

```go
hud 24
--------------
hud   24package main

import "fmt"
func testPrint() {
	name := "hud"
	age := 24
	print(name, " ", age, "\n")
	fmt.Println("--------------")
	println(name, " ", age)
}
func main() {
	testPrint()
}

输出：
hud 24
--------------
hud   24
```

##### **panic**

抛出一个panic异常

**实例**

```go
func testPanic() {
	defer fmt.Println("panic异常之后执行")
	panic("panic错误")
	fmt.Println("end")
}
func main() {
	testPanic()
}

输出：
panic异常之后执行
panic: panic错误

goroutine 1 [running]:
main.testPanic()
        f:/GoCode/package-io/test-builtin.go:34 +0x73
main.main()
        f:/GoCode/package-io/test-builtin.go:41 +0x17
exit status 2
```

##### **new和make**

`new`和`make`的区别：

1. `make`智能用来分配及初始化的类型为`slice`、`map`、`chan`的数据；`new`可以分配任意类型的数据
2. `new`分配返回的是指针，即类型`*T`，`make`返回引用，即`T`
3. `new`分配的空间被清零，`make`分配后，会进行初始化

**实例**

```go
func testNew() {
	b := new(bool)
	fmt.Printf("b: %v type: %T\n", b, b)
	i := new(int)
	fmt.Printf("i: %v type: %T\n", i, i)
	s := new(string)
	fmt.Printf("s: %v type: %T\n", s, s)
}

func main() {
	testNew()
}

输出：
b: 0xc000016098 type: *bool
i: 0xc0000160b8 type: *int
s: 0xc000060250 type: *string
```

看出：new()函数返回的是一个指针类型的变量。

**make**

内建函数`make(T,args)`与`new(T)`的用途不一样，他只能用来创建`slice`、`map`、`channel`，并且返回一个初始化的（而不是置零），类型为T的值（而不是*T）。之所以有所不同，是因为这三个类型背后引用了使用前必须初始化的数据结构。例如，slice是一个三元描述符，包含一个指向数据 （在数组中）的指针，长度以及容量。在这些项被初始化之前slice都是nil的。对于`slice`、`map`和`channel`，`make`初始化这些内部数据结构，并准备好可用的值。

```go
make([]int,10,100)
```

分配一个有100个int的数组，然后创建一个长度为10，容量为100的slice结构，该slice引用包含前10个元素的数组，对应的，`new([]int)`返回一个指向新分配的，被置零的slice结构体的指针，即指向值为nil的slice的指针。

```go
func testmake() {
	var p *[]int = new([]int)
	fmt.Printf("p: %v\n", p)
	v := make([]int, 10) // 已经分配10int
	fmt.Printf("v: %v\n", v)
}
```

### 22.6 标准库bytes模块

------

bytes提供了对**字节切片**进行读写操作的一系列函数，字节切片处理的函数比较多分为基本处理函数，比较函数，后缀检查函数，索引函数，分隔函数，大小写处理函数和子切片处理函数。

#### **常用函数**

##### contains

可以用这个函数检查是否包含，返回`true`或者`false`

```go
func testTranType() {
	//Contains函数
	b := []byte("hud your papa")	//字符串强制转化为byte切片
	b1 :=[]byte("hud")
	b2 :=[]byte("Hud")

	b3 :=bytes.Contains(b,b1)
	fmt.Printf("b3: %v\n", b3)
	b4 :=bytes.Contains(b,b2)
	fmt.Printf("b4: %v\n", b4)
}

输出：
b3: true
b4: false
```

##### count

用于计数的函数

```go
func testCount() {
	s := []byte("Hud said:'Helloooooooooo'")
	s1 := []byte("")
	s2 := []byte("e")
	s3 := []byte("o")

	fmt.Printf("count(h): %v\n", bytes.Count(s, s1))
	fmt.Printf("count(e): %v\n", bytes.Count(s, s2))
	fmt.Printf("count(o): %v\n", bytes.Count(s, s3))
}

输出：
count(H): 2
count(e): 1
count(o): 10
```

##### repeat

重复输出

```go
func testRepeat() {
	s := []byte("hud")
	fmt.Println(string(bytes.Repeat(s, 1)))
	fmt.Println(string(bytes.Repeat(s, 3)))
}

输出：
hud
hudhudhud
```

##### Replace

对字节切片中的内容进行替换

```go
func testReplace() {
	s := []byte("hud said:hello hud's world from hud")
	old := []byte("hud")
	new := []byte("gqc")
	fmt.Println(string(bytes.Replace(s, old, new, 1)))  //替换一次
	fmt.Println(string(bytes.Replace(s, old, new, 2)))  //替换两次
	fmt.Println(string(bytes.Replace(s, old, new, -1))) //不限次数 有几个换几个
}
func main() {
	testReplace()
}

输出：
gqc said:hello hud's world from hud
gqc said:hello gqc's world from hud
gqc said:hello gqc's world from gqc
```

##### Runes

返回Runes字符,一个汉字字符占用三个字节长度

```go
func testRunes() {
	s := []byte("齐天宇说：你好世界")
	r := bytes.Runes(s)
	fmt.Printf("s: %v len(s):%v\n", string(s), len(s))
	fmt.Printf("r: %v len(r):%v\n", string(r), len(r))
}

输出：
s: 齐天宇说：你好世界 len(s):27
r: 齐天宇说：你好世界 len(r):9
```

##### Join

字节切片的连接

```go
func testJoin() {
	s := [][]byte{[]byte("你好"), []byte("世界")}
	s1 := []byte(",")
	fmt.Printf("bytes.Join(s, s1): %v\n", string(bytes.Join(s, s1)))
	s2 := []byte("!")
	fmt.Printf("bytes.Join(s, s2): %v\n", string(bytes.Join(s, s2)))
}

输出：
bytes.Join(s, s1): 你好,世界
bytes.Join(s, s2): 你好!世界
```

#### Reader类型

Reader实现了`io.Reader,io.ReadAt,io.WriteTo,io.Seeker,io.ByteScanner,io.RuneScanner`接口，Reader是只读的，可以seek

```go
func testReader() {
	data := "123456789"
	// 通过byte创建Reader
	r := bytes.NewReader([]byte(data))
	// 返回未读取部分的长度
	fmt.Println("r len :", r.Len())
	// 返回底层数据总长度
	fmt.Println("r size : ", r.Size())
	fmt.Println("--------------")

	buf := make([]byte, 2)
	for {
		// 读取数据
		n, err := r.Read(buf)
		if err != nil {
			break
		}
		fmt.Println(string(buf[:n]))
	}
	fmt.Println("--------------")

	// 设置偏移量，因为上面的操作已经修改了读取位置等信息
	r.Seek(0, 0)
	for {
		// 一个字节一个字节的读
		b, err := r.ReadByte()
		if err != nil {
			break
		}
		fmt.Println(string(b))
	}
	fmt.Println("--------------")

	r.Seek(0, 0)
	off := int64(0)
	for {
		// 指定偏移量读取
		n, err := r.ReadAt(buf, off)
		if err != nil {
			break
		}
		off += int64(n)
		fmt.Println(off, string(buf[:n]))
	}
}

输出：
r len : 9
r size :  9
--------------
12
34
56
78
9
--------------
1
2
3
4
5
6
7
8
9
--------------
2 12
4 34
6 56
8 78
```

#### Buffer类型

 缓冲区是具有读取和写入方法的可变大小的字节缓冲区。Buffer的零值是准备使用的空缓冲区。

声明一个Buffer的四种方法：

```go
var b bytes.Buffer	//直接定义一个Buffer变量，不用初始化可以直接使用。
b := new(bytes.Buffer)	//使用new返回Buffer变量
b := bytes.NewBuffer(s []byte)	//从一个[]byte切片，构造一个Buffer
b := bytes.NewBufferString(s string)	// 从一个string变量构造一个Buffer
```

 **实例**

```go
func testBuffer() {
	var b bytes.Buffer
	fmt.Printf("b: %v\n", b)
	var s = bytes.NewBufferString("Hello")
	fmt.Printf("s: %v\n", s)
	var s1 = bytes.NewBuffer([]byte("Hello~"))
	fmt.Printf("s1: %v\n", s1)
}

输出:
b: {[] 0 0}
s: Hello
s1: Hello~
```

**往Buffer中写入数据**

```go
b.Write(d []byte)		// 将切片d写入buffer的尾部
b.WriteString(s string)	// 将字符串s写入Buffer的尾部
b.WriteByte(c byte)		// 将字符c写入buffer的尾部
b.WriteRune(r rune)		// 将一个rune类型的数据放到缓冲器的尾部
b.WriteTo(w io.Writer)	// 将Buffer中的内容输出到实现了io.Writer接口的可写入对象中
```

 **实例**

```go
func testBuffer1() {
	var b bytes.Buffer
	n, _ := b.WriteString("Hello")
	fmt.Printf("n: %v\n", n)
	fmt.Printf("b: %v\n", string(b.Bytes()))
}

输出：
n: 5
b: Hello 
```

###  22.7 标准库errors模块

errors包实现了操作错误的函数，`golang`使用`error`类型来返回函数执行过程中遇到的错误，如果返回的error值为nil，则表示未遇到错误，否则error会返回一个字符串，说明遇到了什么错误。

#### err结构

```go
type error interface(){
	Error() string
}
```

你可以用任何类型去实现它（只要添加一个`Error()`方法即可），也就是说，error可以是任何类型，这也意味着函数返回的error值实际可以包含任何信息，不一定是字符串。

`error`不一定表示一个错误，它可以表示任何信息，比如`io`包中就用`error`类型的`io.EOF`表示数据读取结束，而不是遇到了什么错误。

errors包实现了一个最简单的error类型，只包含一个字符串，它可以记录大多数情况下遇到的错误信息，errors包的用法也很简单，只有一个`new`函数，用于生成一个最简的error对象：

```go
func New(text string) error
```

```go
package main

import (
	"errors"
	"fmt"
)

func check(s string) error {
	if s == "" {
		return errors.New("字符串不能为空")
	} else {
		return nil
	}
}

func main() {
	check("hello")
	// fmt.Printf("err2: %v\n", err2.Error())
	err := check("")
	fmt.Printf("err: %v\n", err.Error())
}

输出：
err: 字符串不能为空
```

#### 自定义错误

```go
package main
import (
	"errors"
	"fmt"
	"time"
)

type MyError struct {
	When time.Time
	What string
}

func check(s string) error {
	if s == "" {
		return errors.New("字符串不能为空")
	} else {
		return nil
	}
}

// myError is an error implementation that includes a time and a message

func (e MyError) Error() string {
	return fmt.Sprintf("%v %v\n", e.When, e.What)
}

func oops() error {
	return MyError{
		time.Date(1998, 06, 06, 20, 30, 0, 0, time.UTC),
		"the file system has gone away",
	}
}

func main() {
	if err := oops(); err != nil {
		fmt.Println(err)
	}
}

输出：
1998-06-06 20:30:00 +0000 UTC the file system has gone away
 
```

### 22.8 标准库sort模块

#### sort包的内容以及使用

sort包提供了排序切片和用户自定义数据集以及相关功能的函数

sort包主要针对`[]int`、`[]float64`、`[]string`以及其他**自定义切片**的排序

#### 结构体

```go
type IntSlice struct
type Float64Slice
type StringSlice
```

**实例**

1. **`func Ints(a []int)`	//对int类型的切片进行排序**

```go
package main

import (
	"fmt"
	"sort"
)

func main() {
	s := []int{2, 4, 1, 3} //定义一个int类型的无序切片
	sort.Ints(s)           //调用方法对切片s进行排序
	fmt.Printf("s: %v\n", s)
}

输出：
s: [1 2 3 4]
```

2. **`func IntsAreSorted(a []int) bool`  // 判断int类型切片是否排序**

```
package main

import (
	"fmt"
	"sort"
)
func testIAS(s []int) bool {
	b := sort.IntsAreSorted(s)
	return b
}
func main() {
	s := []int{2, 4, 1, 3} //定义一个int类型的无序切片
	fmt.Printf("testIAS(s): %v\n", testIAS(s))
}

输出：
testIAS(s): false
```

3. **`func SearchInts(a []int ,x int) int`	//通过二分查找的方式查找一个元素，返回一个索引**

这里需要注意一点就是：`SearchInts` 在`ints`切片中搜索x并返回索引 如Search函数所述. 返回可以插入x值的索引位置，如果x不存在，返回数组a的长度 **切片必须以升序排列**

```go
func testSearchInts(a []int, x int) int {
	i := sort.SearchInts(a, x)
	return i
}
func main() {

	s := []int{2, 4, 1, 3} //定义一个int类型的无序切片
	// testSort(s)
	// fmt.Printf("testIAS(s): %v\n", testIAS(s))
	a := testSearchInts(s, 1)
	b := testSearchInts(s, 9)
	fmt.Printf("a: %v\n", a)
	fmt.Printf("b: %v\n", b)
}

输出：
a: 0
b: 4
```

4. **接口 type interface**

```
type Interface interface{
	Len() int 	//Len()方法返回集合中的元素个数
	Less(i,j int) bool	//  i>j ,该方法返回索引i的元素是否比索引j的元素小
	Swap(i,j int)		//交换i,j 的值
}
```

**实例**

```go
type NewInt []uint //定义NewInt为一个无符号整型的切片

func (n NewInt) Len() int {
	return len(n)
}

func (n NewInt) Less(i, j int) bool {
	fmt.Println(i, j, n[i] < n[j], n)
	return n[i] < n[j]
}

func (n NewInt) Swap(i, j int) {
	n[i], n[j] = n[j], n[i]
}

func main() {
	n := NewInt{9, 8, 7, 6, 5}
	sort.Sort(NewInt(n))
	fmt.Printf("n: %v\n", n)
}

输出：
1 0 true [9 8 7 6 5]
2 1 true [8 9 7 6 5]
1 0 true [8 7 9 6 5]
3 2 true [7 8 9 6 5]
2 1 true [7 8 6 9 5]
1 0 true [7 6 8 9 5]
4 3 true [6 7 8 9 5]
3 2 true [6 7 8 5 9]
2 1 true [6 7 5 8 9]
1 0 true [6 5 7 8 9]
n: [5 6 7 8 9]
```

**结构体**

------

三种结构体的方法都是一样的，只是分别针对int切片，float切片、string切片这三种不同的类型。

然后这三种结果都有五个公开方法：

```
func (p xxxSlice) Len() int //返回切片长度
func (p xxxSlice) Less(i,j int) bool	
func (p xxxSlice) Swap(i, j int)
func (p xxxSlice) Search(x xxx) int
// 这个和后面那个功能一样
func (p xxxSlice) Sort()
```

#### 综合实例

`[]float64:`

```go
f := []float64{1.1, 4.4, 5.5, 3.3, 2.2}
sort.Float64s(f)
fmt.Printf("f: %v\n", f)

输出：
f: [1.1 2.2 3.3 4.4 5.5]
```

`[]int:`

```go
f := []int{3, 5, 1, 2, 4}
sort.Ints(f)
fmt.Printf("f: %v\n", f)

输出：
f: [1 2 3 4 5]
```

`string：`

```go
// 字符串排序，先比较高位，相同的再比较低位
func Tstring() {
	ls := sort.StringSlice{
		"100",
		"42",
		"41",
		"3",
		"2",
	}
	fmt.Println(ls)	//[100 42 41 3 2]
	sort.Strings(ls)
	fmt.Println(ls)	//[100 2 3 41 42]
}

// 字符串排序，先比较高位，相同的再比较低位
func SString() {
	ls := sort.StringSlice{
		"d",
		"ac",
		"c",
		"ab",
		"e",
	}
	fmt.Println(ls)		// [d ac c ab e]
	sort.Strings(ls)
	fmt.Println(ls)		// [ab ac c d e]	
}
```

**复杂结构：`[][]int:`**

```go
type Testslice [][]int

func (l Testslice) Len() int {
	return len(l)
}
func (l Testslice) Swap(i, j int) {
	l[i], l[j] = l[j], l[i]
}
func (l Testslice) Less(i, j int) bool {
	return l[i][1] < l[j][1]	//以第"1"索引位置进行排序
}
func main() {
	ls := Testslice{
		{1, 4},
		{9, 3},
		{7, 5},
		{5, 6},
	}
	fmt.Println(ls)		// [[1 4] [9 3] [7 5] [5 6]]
	sort.Sort(ls)
	fmt.Println(ls)		// [[9 3] [1 4] [7 5] [5 6]]
}

```

**复杂结构：`[][]map[string]int   [{"k",0},{"k1",1},{"k2",2}]:     `**

```go
type Testmap []map[string]float64

func (l Testmap) Len() int {
	return len(l)
}
func (l Testmap) Swap(i, j int) {
	l[i], l[j] = l[j], l[i]
}
func (l Testmap) Less(i, j int) bool {
	return l[i]["a"] < l[j]["a"] // 按照"a"对应的值排序 3、4、5
}
func main() {
	ls := Testmap{
		{"a": 4, "b": 12},
		{"a": 3, "b": 11},
		{"a": 5, "b": 10},
	}
	fmt.Println(ls)			// [map[a:4 b:12] map[a:3 b:11] map[a:5 b:10]]
	sort.Sort(ls)
	fmt.Println(ls)			// [map[a:3 b:11] map[a:4 b:12] map[a:5 b:10]]
}
```

**复杂结构体：  `[]struct:`**

```go
type people struct {
	name string
	age  int
}

type testPeople []people

func (l testPeople) Len() int {
	return len(l)
}
func (l testPeople) Swap(i, j int) {
	l[i], l[j] = l[j], l[i]
}
func (l testPeople) Less(i, j int) bool {
	return l[i].age < l[j].age // 按照"a"对应的值排序
}
func main() {
		ls := testPeople{
		{name: "qb", age: 1},
		{name: "hud", age: 24},
		{name: "monica", age: 22},
	}
	fmt.Println(ls)			// [{qb 1} {hud 24} {monica 22}]
	sort.Sort(ls)
	fmt.Println(ls)			// [{qb 1} {monica 22} {hud 24}]
}
```

这里可以看出，我们可以对切片排序的规则进行自定义

### 22.9 标准库time

time包提供测量和显示时间的功能

#### 基本使用

打印显示现在的时间，基本实例如下

其中`now`为`time.Time`类型，`Month`为`time.Month`

```go
package main
import (
	"fmt"
	"time"
)

func testTime() {
	now := time.Now()
	fmt.Printf("Current time: %v\n", now)

	year := now.Year()
	month := now.Month()
	day := now.Day()
	hour := now.Hour()
	minute := now.Minute()
	second := now.Second()
	fmt.Printf("%d-%02d-%02d %02d:%02d:%02d\n", year, month, day, hour, minute, second)
	fmt.Printf("%T-%T-%T-%T-%T-%T", year, month, day, hour, minute, second)
}

func main() {
	testTime()
}

输出：
Current time: 2022-07-24 17:06:37.12851 +0800 CST m=+0.002117601
2022-07-24 17:06:37
int-time.Month-int-int-int-int
```

#### 时间戳

在编程中对于时间戳的应用也尤为广泛，例如在Web开发中做cookies有效期，接口加密，`Redis`中的key有效期等等，大部分都是使用到了时间戳。

时间戳是自1970年1月1日(08:00:00GMT)至当前时间的总毫秒数。它也被称为Unix时间戳(UnixTimestamp)。golang中获取时间戳的方式如下:

```go
func testtimestamp() {
	now := time.Now()
	fmt.Printf("TimeStamp type:%T , TimeStamp:%v", now.Unix(), now.Unix())
}
func main() {
	testtimestamp()
}

输出：
TimeStamp type:int64 , TimeStamp:1658654717
```

#### 时间戳格式转换为普通的时间格式

在`golang`中可以`time.Unix`来直接将时间戳转化为当前时间格式，实现瞬间替换

```go
func stampTranNoraml() {
	timestamp := time.Now().Unix()
	timeObj := time.Unix(timestamp, 0) //将时间戳转换为时间格式
	fmt.Println(timeObj)
	year := timeObj.Year()
	month := timeObj.Month()
	day := timeObj.Day()
	hour := timeObj.Hour()
	minute := timeObj.Minute()
	second := timeObj.Second()
	fmt.Printf("%d-%02d-%02d %02d:%02d:%02d\n", year, month, day, hour, minute, second)

}
func main() {
	stampTranNoraml()
}

输出：
2022-07-24 17:32:37 +0800 CST
2022-07-24 17:32:37
```

####  操作时间

**ADD**

```go
func Add(h, m, s time.Duration) {
	now := time.Now()
	fmt.Printf("now: %v\n", now)
	fmt.Println(now.Add(time.Hour*h + time.Minute*m + time.Second*s))
}
func main() {
	Add(1, 1, 1)
}

输出：
now: 2022-07-25 14:36:37.0714176 +0800 CST m=+0.002000701
2022-07-25 15:37:38.0714176 +0800 CST m=+3661.002000701
```

**SUB**

```go
func timeSub() {
	now := time.Now()
	targettime := now.Add(time.Hour)
	fmt.Println(targettime.Sub(now))
}

输出：
1h0m0s
```

**EQUAL**

```go
func (t time) Equal (u time) bool
```

判断两个时间是否相同，会考虑时区的影响，不同时区的时间也可以正确比较

**Before**

```go
func (t time) Before (u time) bool
```

如果t代表的时间在u之前，那么返回`true`，否则返回`false`

**After**

```go
func (t time) After (u time) bool
```

如果t代表的时间在u之后，那么返回`true`，否则返回`false`

### 22.10 标准库encoding/json

`JSON`(JavaScript Object Notation)是一种**轻量级的数据交换格式**，易于人的阅读和编写，同时也易于机器解析和生成，可以有效的提升网络传输效率，通常程序在网络上传输时，会先将数据序列化为json字符串

这个包可以实现`json`的编码和解码·，就是将json字符串转换为struct或者将struct转换为json

#### 核心的两个函数

------

```go
func Marshal (v interface{}) ([]byte,error)
```

将struct编码成json，可以接受任意类型

```go
func Unmarshal(data []byte,v interface{}) error
```

将json转码成struct结构体

#### 两个核心结构体

```go
type Decoder struct{
	//contains filtered or unexported fields
}
```

从输入流读取并解析json

```go
type Encoder struct{
	//contains filtered or unexported fields
}
```

从json写到输出流

- ### func [Marshal](https://github.com/golang/go/blob/master/src/encoding/json/encode.go?name=release#131)

```go
func Marshal(v interface{}) ([]byte, error)
```

Marshal函数返回v的json编码。

Marshal函数会递归的处理值。如果一个值实现了Marshaler接口切非nil指针，会调用其MarshalJSON方法来生成json编码。nil指针异常并不是严格必需的，但会模拟与UnmarshalJSON的行为类似的必需的异常。

否则，Marshal函数使用下面的基于类型的默认编码格式：

布尔类型编码为json布尔类型。

浮点数、整数和Number类型的值编码为json数字类型。

字符串编码为json字符串。角括号"<"和">"会转义为"\u003c"和"\u003e"以避免某些浏览器吧json输出错误理解为HTML。基于同样的原因，"&"转义为"\u0026"。

数组和切片类型的值编码为json数组，但[]byte编码为base64编码字符串，nil切片编码为null。

结构体的值编码为json对象。每一个导出字段变成该对象的一个成员，除非：

```
- 字段的标签是"-"
- 字段是空值，而其标签指定了omitempty选项
```

空值是false、0、""、nil指针、nil接口、长度为0的数组、切片、映射。对象默认键字符串是结构体的字段名，但可以在结构体字段的标签里指定。结构体标签值里的"json"键为键名，后跟可选的逗号和选项，举例如下：

```
// 字段被本包忽略
Field int `json:"-"`
// 字段在json里的键为"myName"
Field int `json:"myName"`
// 字段在json里的键为"myName"且如果字段为空值将在对象中省略掉
Field int `json:"myName,omitempty"`
// 字段在json里的键为"Field"（默认值），但如果字段为空值会跳过；注意前导的逗号
Field int `json:",omitempty"`
```

"string"选项标记一个字段在编码json时应编码为字符串。它只适用于字符串、浮点数、整数类型的字段。这个额外水平的编码选项有时候会用于和javascript程序交互：

```go
Int64String int64 `json:",string"`
```

如果键名是只含有unicode字符、数字、美元符号、百分号、连字符、下划线和斜杠的非空字符串，将使用它代替字段名。

匿名的结构体字段一般序列化为他们内部的导出字段就好像位于外层结构体中一样。如果一个匿名结构体字段的标签给其提供了键名，则会使用键名代替字段名，而不视为匿名。

Go结构体字段的可视性规则用于供json决定那个字段应该序列化或反序列化时是经过修正了的。如果同一层次有多个（匿名）字段且该层次是最小嵌套的（嵌套层次则使用默认go规则），会应用如下额外规则：

1）json标签为"-"的匿名字段强行忽略，不作考虑；

2）json标签提供了键名的匿名字段，视为非匿名字段；

3）其余字段中如果只有一个匿名字段，则使用该字段；

4）其余字段中如果有多个匿名字段，但压平后不会出现冲突，所有匿名字段压平；

5）其余字段中如果有多个匿名字段，但压平后出现冲突，全部忽略，不产生错误。

对匿名结构体字段的管理是从go1.1开始的，在之前的版本，匿名字段会直接忽略掉。

映射类型的值编码为json对象。映射的键必须是字符串，对象的键直接使用映射的键。

指针类型的值编码为其指向的值（的json编码）。nil指针编码为null。

接口类型的值编码为接口内保持的具体类型的值（的json编码）。nil接口编码为null。

通道、复数、函数类型的值不能编码进json。尝试编码它们会导致Marshal函数返回UnsupportedTypeError。

Json不能表示循环的数据结构，将一个循环的结构提供给Marshal函数会导致无休止的循环。

**结构体转换为json**

```go
package main
import (
	"encoding/json"
	"fmt"
)

type Person struct {
	Name  string `json:"NAME"`
	Age   int    `json:"AGE"`
	Email string `json:"EMAIL"`
}

func main() {
	p := Person{
		Name:  "hud",
		Age:   24,
		Email: "qitianyu2007@126.com",
	}
	b, _ := json.Marshal(p)
	fmt.Printf("p: %v\n", p)
	fmt.Printf("b: %v\n", string(b))
}

输出：
p: {hud 24 qitianyu2007@126.com}
b: {"NAME":"hud","AGE":24,"EMAIL":"qitianyu2007@126.com"}
```

**json转换为结构体**

```go
func jsonTostruct(p []byte) {
	var m Person
	json.Unmarshal(p, &m)	// m是一个指针类型，取地址
	fmt.Printf("m: %v\n", m)
}

func main() {
	p := []byte(`{"Name":"hud","Age":24,"Email":"qitianyu2007@126.com"}`)
	jsonTostruct(p)
}

输出：
m: {hud 24 qitianyu2007@126.com}
```

**对map进行序列化和反序列化**

```go
package main

import (
	"encoding/json"
	"fmt"
)

func testmap() {
	players := make(map[string]int)
	players["james"] = 23
	players["Durant"] = 35
	players["rose"] = 1

	// 将player这个map进行序列化
	m, err := json.Marshal(players)
	if err != nil {
		print(err)
	}
	fmt.Printf("%v,%T", string(m), m)
}

func unmar(b []byte) {
	players := make(map[string]int)
	json.Unmarshal(b, &players)
	fmt.Printf("%v", players)
}
func main() {
	testmap()											//	{"Durant":35,"james":23,"rose":1}			
	b := []byte(`{"Durant":35,"james":23,"rose":1}`)
	unmar(b)						// map[Durant:35 james:23 rose:1]
}
```



### 22.11  标准库encoding/xml

`xml`包实现`xml`解析

#### 核心的两个函数

```go
func Marshal (v interface{}) ([]byte,error)
```

将`struct`编码成`xml`，可以接收任意类型

```go
func Unmarshal(data []byte,v interface{}) error
```

将`xml`转码成`struct`结构体

#### 两个核心结构体

```go
type Decoder struct{
	...
}
```

从输入流读取并解析xml

```go
type Encoder struct{
	//contains filtered or unexported fields
}
```

从`xml`写到输出流

**实例：结构体转换为`xml`**

```go
package main
import (
	"encoding/xml"
	"fmt"
)

type Person struct {
	XMLName xml.Name `xml:"person"` //根元素名称：person
	Name    string   `xml:"name"`
	Age     int      `xm;:"age"`
	Email   string   `xml:"e-mail"`
}

func Marshal(p Person) {
	//有缩进格式
	/* func xml.MarshalIndent(v any, prefix string, indent string) ([]byte, error)
	MarshalIndent works like Marshal, but each XML element begins on a new indented line that starts with prefix and is followed by one or more copies of indent according to the nesting depth.
	xml.MarshalIndent on pkg.go.dev */
	b, _ := xml.MarshalIndent(p, " ", "  ")	// 后面两个表示前缀和格式 两个空格为对齐
	fmt.Printf("b: %v\n", string(b))
}

func main() {
	p := Person{
		Name:  "Monica",
		Age:   22,
		Email: "buzhidao@gmail.com",
	}
	Marshal(p)
}

输出：
b:  <person>
   <name>Monica</name>
   <Age>22</Age>
   <e-mail>buzhidao@gmail.com</e-mail>
 </person>
```

**也可以读写文件**

```go
package main

import (
	"encoding/xml"
	"fmt"
)

type Person struct {
	XMLName xml.Name `xml:"person"` //根元素名称：person
	Name    string   `xml:"name"`
	Age     int      `xm;:"age"`
	Email   string   `xml:"e-mail"`
}
func unmarshal(b []byte) {
	var m Person
	xml.Unmarshal(b, &m)
	fmt.Printf("m: %v\n", m)
}

func main() {
	b := []byte(` <person>
   <name>Monica</name>
   <Age>22</Age>
   <e-mail>buzhidao@gmail.com</e-mail>
 </person> `)
	unmarshal(b)
}

输出：
m: {{ person} Monica 22 buzhidao@gmail.com}
```

**如果是读文件内容**

```go
b, _ := ioutil.ReadFile("a.xml")
unmarshal(b)

输出：
m: {{ person} Monica 22 buzhidao@gmail.com}
```

### 22.12 PROTOBUF

Protobuf是一种性能优异、跨语言、跨平台的序列化格式。它是基于二进制的描述性格式，非纯文本，因此他的编码内容不可直接读取。protobuf有专门的语法，需要专用的代码生成器得到golang代码。

- #### 什么是Protocol Buffers?

  - 是一种轻便高效的序列化结构化数据的协议
  - 通常用在存储数据和需要远程数据通信的程序上
  - 跨语言，更小更快也更简单

- #### 为什么要使用Protocol Buffers？

  - 加速站点之间的传输速度
  - 解决数据之间传输不规范问题

- #### Protocol Buffers常用概念

  - Message 定义：描述了一个请求或响应的消息格式
  -  字段标识：消息的定义中，每个字段都有一个惟一的数值标签
  - 常用的数据类型：`double`，`float`，`int32/64`，`bool`，`string`，`bytes`
  - Service 服务定义：在Service中可以定义一个`RPC`服务接口

- #### Protocol Buffers Message中字段修饰符

  - singular：表示成员有0个或者1个，一般省略不写
  - repeated：表示该字段可以包含0~N个元素（理解为Go中的数组或者切片）

  ```protobuf
  syntax = "proto3";
  
  package go.micro.service.product;
  
  service Product{
      rpc AddProduct(ProductInfo) returns(ResponseProduct){}
  }
  
  message ProductInfo {
      int64 id = 1 ;    // 1:字段标识符
      string product_name = 2;  //尽量1~15
  }
  
  message ResponseProduct {
      int64 product_id = 1;
  }
  ```

- #### 安装教程

  [知乎链接](https://zhuanlan.zhihu.com/p/361997082)

- #### `protoc --go_out=. *.proto` 生成文件

  ```bash
  (base) PS F:\Learning-JobAccess-Camp\pkg\apis> protoc --go_out=. --plugin= types.proto
  
  ```
  
- #### JSON、YAML、PROTOBUF性能测试：

  ```go
  package main
  
  import (
  	"Learning-JobAccess-Camp/pkg/apis"
  	"encoding/json"
  	"fmt"
  	"github.com/golang/protobuf/proto"
  	"gopkg.in/yaml.v3"
  	"io/ioutil"
  	"log"
  	"time"
  )
  
  /*
  性能对比： 10w条数据
  
  ==================序列化JSON==================
  序列化耗时： 34.2005ms
  写文件： 91.2864ms
  ==================序列化YAML==================
  序列化耗时： 1.0374918s
  写文件： 91.5277ms
  ==================序列化ProtoBuf==================
  序列化耗时： 6.1438ms
  写文件： 1.0555ms
  
  ==================反序列化JSON==================
  反序列化JSON时间: 97.3399ms
  ==================反序列化Yaml==================
  反序列化Yaml时间: 791.4535ms
  ==================反序列化ProtoBuf==================
  反序列化ProtoBuf时间: 10.108ms
  */
  func main() {
  	// 10万条数据
  	// json yaml protobuf 分别保存，记录序列化耗时
  	count := 100000
  	persons := make([]*apis.PersonalInformation, 0, count)
  
  	for i := 0; i < count; i++ {
  			persons = append(persons, &apis.PersonalInformation{
  				Name:   "Hud",
  				Sex:    "男",
  				Tall:   1.81,
  				Weight: 81,
  				Age:    24,
  			})
  		}
  		{
  			fmt.Println("==================序列化JSON==================")
  			startTime := time.Now()
  			data, err := json.Marshal(persons)
  			if err != nil {
  				log.Fatal(err)
  			}
  			finishJsonMarshalTime := time.Now()
  			err = ioutil.WriteFile("F:/Learning-JobAccess-Camp/chapter08/04.think/data/data.json", data, 0777)
  			if err != nil {
  				log.Fatal(err)
  			}
  			finishWriteFileTime := time.Now()
  			fmt.Println("序列化耗时：", finishJsonMarshalTime.Sub(startTime))
  			fmt.Println("写文件：", finishWriteFileTime.Sub(finishJsonMarshalTime))
  		}
  		{
  			fmt.Println("==================序列化YAML==================")
  			startTime := time.Now()
  			data, err := yaml.Marshal(persons)
  			if err != nil {
  				log.Fatal(err)
  			}
  			finishYamlMarshalTime := time.Now()
  			err = ioutil.WriteFile("F:/Learning-JobAccess-Camp/chapter08/04.think/data/data.yaml", data, 0777)
  			if err != nil {
  				log.Fatal(err)
  			}
  			finishWriteFileTime := time.Now()
  			fmt.Println("序列化耗时：", finishYamlMarshalTime.Sub(startTime))
  			fmt.Println("写文件：", finishWriteFileTime.Sub(finishYamlMarshalTime))
  		}
  		{
  			fmt.Println("==================序列化ProtoBuf==================")
  			pLister := &apis.PersonalInformationList{
  				Items: persons,
  			}
  			startTime := time.Now()
  			data, err := proto.Marshal(pLister)
  			if err != nil {
  				log.Fatal(err)
  			}
  			finishYamlMarshalTime := time.Now()
  			err = ioutil.WriteFile("F:/Learning-JobAccess-Camp/chapter08/04.think/data/data.protobuf", data, 0777)
  			if err != nil {
  				log.Fatal(err)
  			}
  			finishWriteFileTime := time.Now()
  			fmt.Println("序列化耗时：", finishYamlMarshalTime.Sub(startTime))
  			fmt.Println("写文件：", finishWriteFileTime.Sub(finishYamlMarshalTime))
  		}
  
  	//    反序列化JSON时间: 95.6069ms
  	{
  		fmt.Println("==================反序列化JSON==================")
  		startTime := time.Now()
  		data, err := ioutil.ReadFile("F:/Learning-JobAccess-Camp/chapter08/04.think/data/data.json")
  		if err != nil {
  			log.Fatal(err)
  		}
  		err = json.Unmarshal(data, &persons)
  		if err != nil {
  			log.Fatal(err)
  		}
  		finishTime := time.Now()
  		fmt.Println("反序列化JSON时间:", finishTime.Sub(startTime))
  		//	}
  
  		//反序列化Yaml时间: 803.5403ms
  		{
  			fmt.Println("==================反序列化Yaml==================")
  			startTime := time.Now()
  			data, err := ioutil.ReadFile("F:/Learning-JobAccess-Camp/chapter08/04.think/data/data.yaml")
  			if err != nil {
  				log.Fatal(err)
  			}
  			err = yaml.Unmarshal(data, &persons)
  			if err != nil {
  				log.Fatal(err)
  			}
  			finishTime := time.Now()
  			fmt.Println("反序列化Yaml时间:", finishTime.Sub(startTime))
  		}
  		//反序列化ProtoBuf时间: 20.8213ms
  		{
  			pLister := &apis.PersonalInformationList{}
  			fmt.Println("==================反序列化ProtoBuf==================")
  			startTime := time.Now()
  			data, err := ioutil.ReadFile("F:/Learning-JobAccess-Camp/chapter08/04.think/data/data.protobuf")
  			if err != nil {
  				log.Fatal(err)
  			}
  			err = proto.Unmarshal(data, pLister)
  			if err != nil {
  				log.Fatal(err)
  			}
  			finishTime := time.Now()
  			fmt.Println("反序列化ProtoBuf时间:", finishTime.Sub(startTime))
  		}
  
  	}
  }
  
  ```

  
  
- #### 生成`gorm`注释

  **安装`proto-go-inject-tag`**

  ```
  go install github.com/favadi/protoc-go-inject-tag@latest
  ```

  **在`apis`文件夹下执行命令**

  ```
  protoc-go-inject-tag input="*.pb.go"
  ```

  

### 22.13 标准库math

这个包包含一些有用的数学计算函数，例如：三角函数、随机数、绝对值、平方根等

#### 常用函数

------

**绝对值**

```go
func Abs(n float64) float64 {
	return math.Abs(n)
}

func main() {
	fmt.Printf("Abs(-3.14): %v\n", Abs(-3.14))
}

输出：
Abs(-3.14): 3.14
```

返回m的n次方

```go
func pow(m, n float64) float64 {
	return (math.Pow(m, n))
}

func main() {
	fmt.Printf("pow(2, 2): %v\n", pow(2, 2))
}
```

**计算10的n次方**

```go
func main() {
	fmt.Printf("math.Pow10(3): %v\n", math.Pow10(3))
}

输出：
math.Pow10(3): 1000
```

**开平方**

```go
func main() {
	fmt.Printf("math.Sqrt(64): %v\n", math.Sqrt(64))
}

输出：
math.Sqrt(64): 8
```

**开立方**

```go
func main() {
	fmt.Printf("math.Cbrt(27): %v\n", math.Cbrt(27))
}

输出：
math.Cbrt(27): 3
```

**向上/下取整**

```go
func main() {
	fmt.Printf("math.Ceil(3.14159): %v\n", math.Ceil(3.14159))		//向上取整
	fmt.Printf("math.Floor(3.14159): %v\n", math.Floor(3.14159))	//向下取整
}

输出：
math.Ceil(3.14159): 4
math.Floor(3.14159): 3
```

**取余数**

```go
func main() {
	fmt.Printf("math.Mod(10, 3): 1 %v\n", math.Mod(10, 3))
}

输出：
math.Mod(10, 3): 1
```

**分别取整数和小数部分：**

```go
func main() {
	int2, frac := math.Modf(3.14159265358979)
	fmt.Printf("int2: %v\n", int2)
	fmt.Printf("frac: %v\n", frac)
}

输出：
int2: 3
frac: 0.14159265358979
```

**生成随机数： rand**

为了使每次生成的随机数不一样，我们需要给一个每次都不一样的Seed

```go
package main

import (
	"fmt"
	"math/rand"
	"time"
)
func main() {

	rand.Seed(time.Now().UnixNano())
	num := rand.Intn(10)		//10代表随机数的最大值
	fmt.Println(num)
}

输出：
4
```

**方法二：生成指定区间的随机数**

```go
package main

import (
	"fmt"
	"math/rand"
	"time"
)

func RandInt(min, max int) int {

	if min >= max || min == 0 || max == 0 {
		return max
	}
	return rand.Intn(max-min) + min
}

//调用
func main() {
	rand.Seed(time.Now().UnixNano())

	num := RandInt(190, 200)
	fmt.Println(num)
}
```

实例：生成5个随机数存储在一个数组中，并反转打印出来

```go
package main

import (
	"fmt"
	"math/rand"
	"time"
)

func main() {
	var a [5]int
	rand.Seed(time.Now().UnixNano())		// 设置随机种子
	for i := 0; i < 5; i++ {
		a[i] = rand.Intn(15)
	}
	fmt.Printf("a: %v\n", a)
	for i := 0; i < len(a)/2; i++ {
		a[i], a[len(a)-i-1] = a[len(a)-i-1], a[i]
	}
	fmt.Printf("a: %v\n", a)

}

输出：
a: [3 1 13 14 12]
a: [12 14 13 1 3]
```



## 23. go操作mysql数据库

### 安装配置mysql驱动

**安装驱动**

```shell
go get -u github.com/go-sql-driver/mysql
```

**初始化模块**

```go
go mod init
go mod tidy
```

**导入包**

```go
import(
	"database/sql"
	_ "github.com/go-sql-driver/mysql"
)
```



### 数据库连接

#### **获得连接**

```go
package main

import (
	"database/sql"
	"fmt"
	"time"

	_ "github.com/go-sql-driver/mysql"
)

func main() {
	db, err := sql.Open("mysql", "root:199866@/go_db")
	if err != nil {
		panic(err)
	}
	fmt.Println(db)

	// 最大连接时长
	db.SetConnMaxLifetime(time.Minute*3)
	// 最大连接数
	db.SetMaxOpenConns(10)
	// 空闲连接数
	db.SetMaxIdleConns(10)
}
```

#### 初始化连接

Open函数可能只是验证其参数格式是否正确，实际上并不创建与数据库的连接。如果要检查数据源的名称是否真实有效，应该调用Ping方法。

返回的DB对象可以安全的被多个`goroutine`并发调用，并且维护其自己的空闲连接池。因此Open函数应金杯调用一次，很少需要关闭这个DB对象。

```go
package main

import (
	"database/sql"
	"fmt"

	_ "github.com/go-sql-driver/mysql"
)

// 定义一个全局对象db
var db *sql.DB //sql.DB 类型指针变量

func initDB() (err error) {
	dsn := "root:199866@tcp(127.0.0.1:3306)/go_db?charset=utf8mb4&parseTime=True" // mysql需要字符集,解析时间
	// 不会校验账号密码是否正确
	// 注意这里 不要使用" := " 我们是给全局变量赋值，然后在main函数中使用全局变量db
	db, err = sql.Open("mysql", dsn)
	if err != nil {
		return err
	}
	db.Ping() //ping一下 如果出错则返回
	if err != nil {
		return err
	}
	return nil
}

func main() {
	err := initDB()
	if err != nil {
		fmt.Println("初始化失败！")
	} else {
		fmt.Println("初始化成功")
	}
}

输出：
初始化成功
```



### Go操作MySQL数据库

插入、更新和删除都使用`Exec`方法

```go
func(db *DB) Exec(query string,args ...interface{}) (Result,error)  	// 传入sql语句
```

#### 插入数据

```go
package main

import (
	"database/sql"
	"fmt"

	_ "github.com/go-sql-driver/mysql"
)

// 定义一个全局对象db
var db *sql.DB //sql.DB 类型指针变量
//插入数据
func insertData() {
	sqlStr := "INSERT INTO USER_TBL(NAME,PWD) VALUES(?,?)"
	r, err := db.Exec(sqlStr, "hud", "199866")
	if err != nil {
		fmt.Println("出现错误 %v\n", err)
		return
	}
	i, err2 := r.LastInsertId()
	if err2 != nil {
		fmt.Println("get LastInsertId failed ,err:%v", err2)
		return
	}
	fmt.Printf("get LastInsertId succeed,id is %v\n", i)
}

func main() {
	insertData()
}


输出：
get LastInsertId succeed,id is 5
```

#### **查询一行数据**

```go
package main

import (
	"database/sql"
	"fmt"

	_ "github.com/go-sql-driver/mysql"
)

// 定义一个全局对象db
var db *sql.DB //sql.DB 类型指针变量

func initDB() (err error) {
	dsn := "root:199866@tcp(127.0.0.1:3306)/go_db?charset=utf8mb4&parseTime=True" // mysql需要字符集,解析时间
	// 不会校验账号密码是否正确
	// 注意这里 不要使用" := " 我们是给全局变量赋值，然后在main函数中使用全局变量db
	db, err = sql.Open("mysql", dsn)
	if err != nil {
		return err
	}
	db.Ping() //ping一下 如果出错则返回
	if err != nil {
		return err
	}
	return nil
}
// 定义一个User结构体，用于接收返回的数据库数据
type User struct {
	id   int
	name string
	pwd  string
}

// 查询数据
func queryOnerow() {
	s := "SELECT * FROM USER_TBL WHERE ID = ?"
	var u User
	err := db.QueryRow(s, 1).Scan(&u.id, &u.name, &u.pwd)
	if err != nil {
		fmt.Printf("err: %v\n", err)
	} else {
		fmt.Printf("u: %v\n", u)
	}
}

func main() {
	initDB()
	queryOnerow()
}

输出：
u: {1 hud 199866}
```

#### **查询多行数据**

```go
func queryManyrow() {
	s := "SELECT * FROM USER_TBL"
	r, err := db.Query(s)
	var u User
	defer r.Close()
	if err != nil {
		fmt.Printf("err: %v", err)
	} else {
		for r.Next() {
			r.Scan(&u.id, &u.name, &u.pwd)
			fmt.Printf("u: %v\n", u)
		}
	}
}

输出：
u: {1 hud 199866}
u: {2 QTY 123456}
```

#### 更新数据

```go
/ 更新数据
func updateData() {
	s := "UPDATE USER_TBL SET NAME=? ,PWD = ? WHERE ID = ?"
	r, err := db.Exec(s, "James", "0623", "2")
	if err != nil {
		fmt.Printf("err: %v\n", err)
		return
	}
	i, err2 := r.RowsAffected()
	if err2 != nil {
		fmt.Println("更新行失败", err2)
		return
	}
	fmt.Println("更新行成功,更新的是", i)
}

輸出：
更新行成功,更新的是 1
```

#### 刪除数据

```go
// 删除数据
func delData() {
	s := "DELETE FROM USER_TBL WHERE ID = ?"
	r, err := db.Exec(s, 2)
	if err != nil {
		fmt.Printf("err: %v\n", err)
		return
	}
	i, err2 := r.RowsAffected()
	if err2 != nil {
		fmt.Printf("err2: %v\n", err2)
		return
	}
	fmt.Printf("删除的是第%v行\n", i)
}

输出：
删除的是第2行
```

#### GORM

- **什么是ORM**

  `ORM`是对象与关系型数据库之间的映射关系，`ORM`建立了编程语言中对象（例如`struct`）与数据库的元数据（例如table）之间的映射关系	

  - 简单易用：对象即表，自动映射

  - 易于理解：操作过程只有对象，无需关注底层SQL

  - 定义精确：对象类型与数据库精确匹配

    ```go
    import(
    	_"gorm.io/driver/mysql"
    	_"gorm.io/gorm"
    )
    ```

- #### 使用方法

  [链接](https://github.com/favadi/protoc-go-inject-tag)

- #### 使用示例

  ```protobuf
  // file: test.proto
  syntax = "proto3";
  
  package pb;
  option go_package = "/pb";
  
  message IP {
    // @gotags: valid:"ip"    使用这个tag~~~~
    string Address = 1;
  
    // Or:
    string MAC = 2; // @gotags: validate:"omitempty"
  }
  ```

  

## 24. 类型断言

类型断言，由于接口是一般类型，不知道具体类型，如果要转成具体类型，就需要使用类型断言。举个例子

```go
type point struct {
	x int
	y int
}

func main() {
	A := point{3, 4}
	var B interface{}
	B = A
	C := point{1, 2}
	C = B
	fmt.Printf("C: %v\n", C)
}
// 这样写会报错cannot use B (variable of type interface{}) as point value in assignment: need type assertion
```

**使用类型断言**

```go
type point struct {
	x int
	y int
}

func main() {
	A := point{3, 4}
	var B interface{}
	B = A
	C := point{1, 2}
	C = B.(point)
	fmt.Printf("C: %v\n", C)
}
```

在进行类型断言时 ，如果类型不匹配，就会报panic，因此进行类型断言时，要确保原来的空接口指向的就是断言的类型。

如果想在类型断言错误时候，不报panic 继续执行

```go
func main() {
	var a interface{}
	var b float32 = 1.1
	a = b

	c, ok := a.(float64)
	if ok {
		fmt.Println("success")
		fmt.Printf("c: %v\n", c)
	} else {
		fmt.Println("Failed")
	}
	fmt.Println("繼續執行")
}

輸出：
Failed
繼續執行
```

### 24.1 类型断言最佳实践

在章节19中定义了USB接口，其中phone结构体还定义了一个call的方法，当接收者是phone的时候，还需要调用call方法

```go
package main

import "fmt"

type USB interface {
	Start()
	Stop()
}

// 定义3个结构体
type phone struct {
	brand string
}
type pad struct {
	brand string
}
type computer struct{}

// 分别定义两个结构体实现接口中的两个方法
func (p phone) Start() {
	fmt.Printf("%v手机开始工作\n", p.brand)
}

func (p phone) Stop() {
	fmt.Printf("%v手机停止工作\n", p.brand)
}
func (p phone) Call() {
	fmt.Printf("%v手机正在打电话\n", p.brand)
}

func (p pad) Start() {
	fmt.Printf("%v平板开始工作\n", p.brand)
}
func (p pad) Stop() {
	fmt.Printf("%v平板停止工作\n", p.brand)
}

//类型断言（体会好处）
func (c computer) Working(u USB) {
	u.Start()
	u.Stop()
	if p, ok := u.(phone); ok {
		p.Call()
	}
}

func main() {
	var usbArr [3]USB
	usbArr[0] = pad{"huawei"}
	usbArr[1] = pad{"oppo"}
	usbArr[2] = phone{"apple"}
	var c computer
	for _, v := range usbArr {
		c.Working(v)
	}

}

输出：
huawei平板开始工作
huawei平板停止工作
oppo平板开始工作
oppo平板停止工作
apple手机开始工作
apple手机停止工作
apple手机正在打电话
```

这里看到，经过类型断言可以将接口类型重新转换成结构体类型从而实现特有的方法

**实践2**

写一个函数，循环判断传入参数的类型

```go
func TypeJudge(items ...interface{}) {   //...表示传入任意个数个参数 ，interface{}表示任意类型
	for i, x := range items {
		switch x.(type) {
		case bool:
			fmt.Println("bool")
		case float64:
			fmt.Println("float64")
		case int,int64:
			fmt.Println("int,int64")
		case nil:
			fmt.Println("nil")
		case string:
			fmt.Println("string")
		default:
			fmt.Println("unknown")
	}
	}
}
```



## 25. 单元测试

​		在工作中，我们会遇到，就是去确认一个函数，或者一个模块的结果是否正确。

### **传统测试缺点分析**

- 不方便，我们需要在main函数中去调用，这样就需要去调用main函数，如果现在项目正在运行，就可能要去停止项目
- 不利于管理，因为我们在测试多个函数或者多个模块时，都需要写在main函数中，不利于管理和清晰思路
- 引出testing测试框架，可以很好的解决这个问题



go语言中自带有一个轻量级的测试框架testing和自带go test命令来实现**单元测试**和**性能测试**。

可以解决以下问题：

1. 确保每个函数是可以运行的，并且运行结果是正确的
2. 确保写出的代码的性能是好的
3. 单元测试能够及及时的发现程序设计或者实现的逻辑错误，使问题及早暴露，便于问题的暴露解决。而性能测试的重点

在于发现程序设计上的一些问题，让程序能在高并发的情况下还能保持稳定



```go
//  Test/ttjson.go
package main

import (
	"encoding/json"
	"fmt"
)

type Person struct {
	Name  string `json:"NAME"`
	Age   int    `json:"AGE"`
	Email string `json:"EMAIL"`
}

func jsonTostruct(p []byte) {
	var m Person
	json.Unmarshal(p, &m) // m是一个指针类型，取地址
	fmt.Printf("m: %v\n", m)
}

func structTojson() []byte {
	p := Person{
		Name:  "hud",
		Age:   24,
		Email: "qitianyu2007@126.com",
	}

	b, _ := json.Marshal(p)
	//fmt.Printf("b: %v\n", string(b))
	return b
}

func openhaha() error {
	file, err := os.OpenFile("f:/Gocode/aaa.txt", os.O_RDONLY, 0666)
	print(file.Name())
	if err != nil {
		return err
	}
	return nil
}
```

**测试文件**

```go
// Test/json_test.go
package main

import (
	"testing"
) // 引入testing框架

func TestStrtoJson(t *testing.T) {
	x := structTojson()
	jsonTostruct(x)
	t.Logf("执行正确")
}

func TestHello(t *testing.T) {
	//fmt.Println("hello函数被调用")
	//t.Fatalf("好像没错！")
	t.Logf("这就是tmd日志")
}

func TestOpen(t *testing.T) {
	err := openhaha()
	if err != nil {
		t.Fatalf("%v", err)
	}
}
```

**调试测试**

```shell
F:\GoCode\Test>go test -v
=== RUN   TestStrtoJson
m: {hud 24 qitianyu2007@126.com}
    json_test.go:10: 执行正确
--- PASS: TestStrtoJson (0.00s)
=== RUN   TestHello
    json_test.go:16: 这就是tmd日志
--- PASS: TestHello (0.00s)
=== RUN   TestOpen
--- FAIL: TestOpen (0.00s)
panic: runtime error: invalid memory address or nil pointer dereference [recovered]
        panic: runtime error: invalid memory address or nil pointer dereference
[signal 0xc0000005 code=0x0 addr=0x0 pc=0xf82a5a]

goroutine 8 [running]:
testing.tRunner.func1.2({0xf97b20, 0x10adff0})
        Q:/Golang-SDK/src/testing/testing.go:1389 +0x24e
testing.tRunner.func1()
        Q:/Golang-SDK/src/testing/testing.go:1392 +0x39f
panic({0xf97b20, 0x10adff0})
        Q:/Golang-SDK/src/runtime/panic.go:838 +0x207
os.(*File).Name(...)
        Q:/Golang-SDK/src/os/file.go:57
test_pro.openhaha()
        F:/GoCode/Test/ttjson.go:35 +0x3a
test_pro.TestOpen(0xc0001384e0)
        F:/GoCode/Test/json_test.go:20 +0x1e
testing.tRunner(0xc0001384e0, 0xfc3248)
        Q:/Golang-SDK/src/testing/testing.go:1439 +0x102
created by testing.(*T).Run
        Q:/Golang-SDK/src/testing/testing.go:1486 +0x35f
exit status 2
FAIL    test_pro        0.837s
```

**shell中**

```shell
// go test默认是测试文件夹内所有的_test.go文件
// 如果要测试特定的某几个文件
>go test -v xxx1_test.go xxx2_test.go 
// 测试特定的文件中的特定的函数的话
>go test -v -test.run TestXxxx
F:\GoCode\Test>go test -v -test.run TestOpen
=== RUN   TestOpen
--- FAIL: TestOpen (0.00s)
panic: runtime error: invalid memory address or nil pointer dereference [recovered]
        panic: runtime error: invalid memory address or nil pointer dereference
[signal 0xc0000005 code=0x0 addr=0x0 pc=0x7c2a5a]

goroutine 19 [running]:
testing.tRunner.func1.2({0x7d7b20, 0x8edff0})
        Q:/Golang-SDK/src/testing/testing.go:1389 +0x24e
testing.tRunner.func1()
        Q:/Golang-SDK/src/testing/testing.go:1392 +0x39f
panic({0x7d7b20, 0x8edff0})
        Q:/Golang-SDK/src/runtime/panic.go:838 +0x207
os.(*File).Name(...)
        Q:/Golang-SDK/src/os/file.go:57
test_pro.openhaha()
        F:/GoCode/Test/ttjson.go:35 +0x3a
test_pro.TestOpen(0xc0000851e0)
        F:/GoCode/Test/json_test.go:20 +0x1e
testing.tRunner(0xc0000851e0, 0x803248)
        Q:/Golang-SDK/src/testing/testing.go:1439 +0x102
created by testing.(*T).Run
        Q:/Golang-SDK/src/testing/testing.go:1486 +0x35f
exit status 2
FAIL    test_pro        0.203s

// 如果你用Goland那当我没说
```



### **单元测试总结**

- 测试用例文件必须以`_test.go`结尾，例如`Hud_test.go`
- 测试用例函数必须以Test开头，一般来说就是Test+被测试的函数名，例如`TestStrToJson`
- `TestStrToJson(t *testing.T)`的形参类型必须是**`*testing.T`**
- 一个测试用例当中可以有多个测试用例函数
- 运行测试用例指令(直接`cd`到`xxx_test.go`所在目录即可)
  - go test [如果运行正确无日志，**如果有错误 ，会输出日志**]
  - go test -v [无论运行正确或是错误，都输出日志]
- 当出现错误时候，可以使用`t.Fatalf()`来格式化输出错误信息，并退出程序
- `t.Logf()`方法可以用来输出日志
- 测试用例函数没有放在main**函数**中，也执行了。这就是测试用例的方便之处
- PASS表示测试用例运行成功，FAIL表示测试用例运行失败



### 单元测试综合案例

**要求**

- 编写一个Players结构体，字段Name、Number、Team

- 给Players结构体绑定一个方法Store，可以将一个Players对象序列化后保存到文件中

- 给Players绑定方法Restore，可以将一个序列化的Players，从文件中读取，反序列化为Players对象

- 测试用例文件`players_test.go`,编写测试用例函数`TestStore`和`TestRestore`进行测试0

  

  **这里发现了一个坑！！！**

  **如果你的结构体名是首字母大写的话，那么结构体内的字段名的首字母也需要大写，不然就找不着了，好像就是找不到这个参数了。。。**

**函数实现**

```go
// Test/store.go
package test

import (
	"encoding/json"
	"fmt"
	"io/ioutil"
)

// 编写一个Players结构体，字段Name、Number、Team
type Players struct {
	Name   string
	Number int
	Team   string
}

//给Players结构体绑定一个方法Store，可以将一个Players对象序列化后保存到文件中
func (p Players) Store() (error, Players) {
	// 先进行序列化
	b, err := json.Marshal(p)
	if err != nil {
		fmt.Println("序列化错误")
		return err, Players{}
	}
	path := "f:/Gocode/Test/store.log"
	err2 := ioutil.WriteFile(path, b, 0666)
	if err2 != nil {
		fmt.Println("写入文件出错")
		return err2, Players{}
	}
	fmt.Printf("b: %v\n", string(b))
	return nil, p

}

func (p *Players) Restore() (error, Players) {
	path := "f:/Gocode/Test/store.log"
	b, err := ioutil.ReadFile(path)
	if err != nil {
		fmt.Println("读取文件出错")
		return err, Players{}
	}
	err2 := json.Unmarshal(b, &p)
	if err2 != nil {
		fmt.Println("反序列化错误")
		return err2, Players{}
	}
	fmt.Printf("b: %v\n", p)
	return nil, *p
}

```

**测试文件**

```go
// Test/store_test.go
package test

import "testing"

func TestStoreandRestore(t *testing.T) {
	p := Players{"James", 23, "Lakers"}
	err, p2 := p.Store()
	if err != nil {
		t.Fatalf("%v", err)
	}
	err2, p3 := p.Restore()
	if err2 != nil {
		t.Fatalf("%v", err2)
	}
	if p2 != p3 {
		t.Fatalf("测试错误")
	}
}

测试结果：
Running tool: Q:\Golang-SDK\bin\go.exe test -timeout 30s -run ^TestStoreandRestore$ test_pro

=== RUN   TestStoreandRestore
b: {"Name":"James","Number":23,"Team":"Lakers"}
b: &{James 23 Lakers}
--- PASS: TestStoreandRestore (0.00s)
PASS
ok      test_pro        0.161s
```



## 26. goroutine补充学习

### 基本概念

#### 进程和线程的说明

- 进程就是程序在操作系统中的一次执行过程，是系统进行资源分配和调度的基本单位
- 线程是进程的一个执行实例，是程序执行的最小单元，他是比进程更小的能独立运行的基本单位
- 一个进程可以创建销毁多个线程，通一个进程中的多个线程可以并发执行
- 一个程序至少有一个进程，一个进程至少有一个线程

#### 并发和并行

- 多线程程序在单核上运行，就是并发
- 多线程程序在多核上运行，就是并行



**并发的特点：**

- 多个任务作用在同一个CPU
- 从微观的角度来看，在一个时间点上，其实只有一个任务在执行

**并行的特点：**

- 多个任务作用在多个cpu
- 从微观角度来看，在一个时间点上就是多个任务在同时执行



**Go协程和Go主线程**

1. Go主线程：一个Go线程上，可以起多个协程，你可以这样理解，协程是轻量级的线程【编译器做了优化】。

2. Go协程的特点：

   ● 有独立的栈空间

   ● 共享程序堆空间

   ● 调度由用户控制

   ● 协程是轻量级别的线程



**入门案例**

1. 在主线程中，开启一个goroutine，该协程每隔一秒钟输出一个hello Hud

2. 在主线程中也每隔一秒钟输出一次hello golang，输出10次后，退出程序

3. 要求主线程和goroutine同时执行

   ```go
   package main
   import (
   	"fmt"
   	"strconv"
   	"time"
   )
   
   func output() {
   	for i := 0; i < 5; i++ {
   		fmt.Println("Hello,world" + strconv.Itoa(i))
   		time.Sleep(time.Second)
   	}
   }
   
   func main() {
   	go output()
   	for i := 0; i < 5; i++ {
   		fmt.Println("Hello !!! Hud " + strconv.Itoa(i))
   		time.Sleep(time.Second)
   	}
   }
   
   输出结果：
   Hello,world0
   Hello !!! Hud 0
   Hello !!! Hud 1
   Hello,world1
   Hello,world2
   Hello !!! Hud 2
   Hello !!! Hud 3
   Hello,world3
   Hello,world4
   Hello !!! Hud 4
   ```

   只要主线程结束，程序就结束了，不会管你协程有没有结束。

**小结**

1. 主线程是一个物理线程，直接作用在`cpu`上，是重量级的，非常耗费`cpu`资源
2. 协程从主线程开启的，是轻量级的线程，是逻辑态，对资源消耗相对小
3. `golang`的协程机制是重要的特点，可以轻松的开启上万个协程。



### MPG

- **M：**操作系统的主线程（是物理线程）
- **P：**协程执行需要的上下文
- **G：**协程
- **MPG运行状态1：**
  - 当前程序有三个M，如果都在一个CPU运行，就是并发，如果在不同的CPU运行，就是并行
  - M1,M2,M3正在执行一个G,M1协程队列有三个，M2协程队列有三个，M3协程队列有两个
  - Go协程是轻量级的线程，是逻辑态的，Go可以轻易的起上万个协程
- **MPG运行状态2：**
  - M0主线程正在执行G0协程，另外有三个协程正在等待
  - 如果G0阻塞，比如读取文件或数据库等等
  - 这个时候就会创建M1主线程(也有可能是从已有的线程池中取出M1)，并且将等待的三个协程挂到M1下进行执行，M0主线程下的G0仍然执行者文件i/o操作。
  - 这样的MPG调度模式可以既让G0执行，同时也不会让队列的其他协程一直阻塞，仍然可以并发/并行执行
  - 等到G0不阻塞了，M0会被放到空闲的主线程继续执行(从已有的线程池中取)，同时G0又会被唤醒



### **互斥锁（sync.Mutex）**

用一个需求引入，现在要计算1-200的各个数的阶乘，并且把各个数的阶乘放入到map中，最后显示出来，要求使用`goroutine`完成。

假设我直接起200个协程，同时开始写这个map

会报一个比较经典的错误：`fatal error: concurrent map writesmap[69]=0`

**如果我们想看看是否存在资源竞争的问题，其实也很简单，只需要在编译该程序时，增加一个参数-race即可**

```go
PS F:\GoCode\testGoroutine> .\gochan.exe 
==================
WARNING: DATA RACE
Write at 0x00c0000c4450 by goroutine 8:
```

使用互斥锁sync(synchronized)包下的`Mutex`(互斥)

```go
package main

import (
	"fmt"
	"sync"
	"time"
)

//用一个需求引入，现在要计算1-200的各个数的阶乘，并且把各个数的阶乘放入到map中，最后显示出来，要求使用goroutine完成。
// 1、编写一个函数，计算各个数的阶乘，并放入到一个map中
// 2、我们启动的协程是多个，统计的结果将放入到map中
// 3、map应该做成一个全局变量
var (
	Mymap = make(map[int]int, 10)
	//声明一个全局的互斥锁
	lock sync.Mutex
)

func test(n int) {
	res := 0
	for i := 1; i < n; i++ {
		res = i + 1
	}
	lock.Lock()
	Mymap[n] = res
	lock.Unlock()
}

func main() {
	// 开启多个协程完成这个任务
	for i := 1; i <= 200; i++ {

		go test(i)

	}
	time.Sleep(time.Second * 10)
	lock.Lock()
	for i, v := range Mymap {
		fmt.Printf("map[%v]=%v\n", i, v)
	}
	lock.Unlock()
}
```

主线程并不知道协程是否执行完毕，所以如果不在for range循环前后加锁，还是有可能会出现底层资源竞争的情况。。。



### 管道(Channel)

- #### 为什么需要channel

  1. 主线程在等待所有`goroutine`全部完成的时间很难确定。
  2. 如果时间长了，会增加等待时间，如果等待的时间短了，未完成的`goroutine`会随着main函数的结束而被销毁
  3. 通过全局变量枷锁同步来实现通讯，也并不利用多个协程 对全局变量读写操作

- #### channel的介绍

  1. channel的本质就是一个数据结构-队列
  2. 数据是先进先出的
  3. 线程安全，多`goroutine`访问时，不需要加锁，就是说channel本身就是线程安全的
  4. channel有类型时，一个string的channel只能存放string类型的数据

- #### channel的声明

  ```go
  // var [管道名称] = make (chan [chanType],[容量])
  // 声明带缓冲int类型管道
  var intChan = make(chan int, 10)
  
  //声明不带缓冲的string类型管道
  schan := make(chan string)
  ```
  
  **注意：**
  
  - **给管道写入数据时，不能超过他的容量，否则会报错**
  
  - **管道读写数据，头出尾入**
  
    ```go
    package main
    import "fmt"
    func main() {
    	var intChan = make(chan int, 10)
    	intChan <- 3
    	var a int
    	a = <-intChan
    	fmt.Printf("a: %v\n", a)
    }
    ```
  
  - **channel中只能存放指定的数据类型**
  
  - **在没有使用协程的情况下，如果channel数据取完了，再取就会报dead lock**

**看一个案例代码**

```go
package main
import "fmt"

type cat struct {
	name string
	age  int
}

func main() {

	bigchan := make(chan interface{}, 20)
	qb := cat{"qb", 2}
	// bigchan <- 23
	bigchan <- qb
	//类型断言
	cat11 := <-bigchan
	newcat := cat11.(cat)
	fmt.Printf("name:%v", newcat.name)
}

输出：
name:qb
```

简单的讲一下这个代码，声明的管道类型是空接口类型（因为所有的类型都实现了空接口，所以这个channel中可以传入任意类型的值），向管道内添加一个cat结构体变量，再从中取出一个值，你可以在编译器中看到这个变量的类型是空接口类型。我们用一个变量`cat11`来接收管道内输出的值，会发现无法使用这个变量的字段，因为传出来的是空结构体类型是没有字段名的。所以我们在这里使用了类型断言，用于接收这个值。



- #### channel的关闭

  使用内置函数close可以关闭channel，当channel关闭之后，就不能再向channel写数据了，但是仍然可以从该channel读取数据。

  ```go
  package main
  
  import "fmt"
  
  func test() (int, int) {
  
  	intchan := make(chan int, 20)
  	intchan <- 1
  	intchan <- 2
  	close(intchan)
  	a := <-intchan
  	b := <-intchan
  	return a, b
  }
  
  func main() {
  	i, i2 := test()
  	fmt.Printf("i: %v\n", i)
  	fmt.Printf("i2: %v\n", i2)
  }
  
  ```

  

- #### channel的遍历

- channel支持for-range遍历，但是要注意两个细节

  1. 在遍历时，如果channel没有关闭，则会出现deadlock错误

  2. 在遍历时，如果channel已经关闭则正常遍历数据遍历完后退出。

     **一定记得关闭通道**

     举个例子：

     ```go
     package main
     import "fmt"
     
     func main() {
     	intchan := make(chan int, 20)
     	intchan <- 1
     	intchan <- 2
     	for v := range intchan {
     		fmt.Println(v)
     	}
     }
     
     运行：
     PS F:\GoCode\testGoroutine> go run "f:\GoCode\testGoroutine\test-chan.go"
     1
     2
     fatal error: all goroutines are asleep - deadlock!
     ```

     发生deadlock错误，为了解决这个问题，在遍历之前关闭管道：

     ```go
     package main
     
     import "fmt"
     
     func main() {
     	intchan := make(chan int, 2)
     	intchan <- 1
     	intchan <- 2
     	close(intchan)
     	for v := range intchan {
     		fmt.Println(v)
     	}
     }
     
     输出：
     1
     2
     ```

  

  - #### 应用实例

    - 开启一个`writeData`协程，向管道`intChan`中写入50个整数
    - 开启一个readData协程，从管道intChan中读取writeData写入的数据
    - 注意：writeData和readData操作的是同一个管道
    - 主线程需要等待writeData和readData协程都完成工作才能退出

    ```go
    package main
    
    import (
    	"fmt"
    	"time"
    )
    func writeData(intchan chan int) {
    	for i := 0; i < 50; i++ {
    		intchan <- i
    		fmt.Printf("写入：%v\n", i)
    		time.Sleep(time.Microsecond)
    	}
    	close(intchan)
    }
    func readData(intchan chan int, exitchan chan bool) {
    	for {
    		value, ok := <-intchan
    		if !ok {
    			break
    		}
    		fmt.Printf("读到数据：%v\n", value)
    		time.Sleep(time.Microsecond)
    	}
    	// 读取完数据后，也就是任务完成
    	exitchan <- true
    	close(exitchan)
    }
    
    func main() {
    	intchan := make(chan int, 50)
    	exitchan := make(chan bool, 1)
    
    	go writeData(intchan)
    	go readData(intchan, exitchan)
    	time.Sleep(time.Second * 10)
    }
    
    
    这里体现的利用休眠的方法来让goroutine交替执行
    ```

  考虑另外一种可能，如果我们不进行休眠，然后管道的大小小于了数据量的大小，考虑到数据操作的速度很快，有没有可能**读或写操作一下子就把管道占满导致死锁了呢**？来看看代码：	

  ```go
  package main
  
  import (
  	"fmt"
  	"time"
  )
  
  func writeData(intchan chan int) {
  	for i := 0; i < 20; i++ {
  		intchan <- i
  		fmt.Printf("写入：%v\n", i)
  		// time.Sleep(time.Microsecond)
  	}
  	close(intchan)
  }
  func readData(intchan chan int, exitchan chan bool) {
  	for {
  		value, ok := <-intchan
  		if !ok {
  			break
  		}
  		fmt.Printf("读到数据：%v\n", value)
  		// time.Sleep(time.Microsecond)
  	}
  	// 读取完数据后，也就是任务完成
  	exitchan <- true
  	close(exitchan)
  }
  
  func main() {
  	intchan := make(chan int, 4)
  	exitchan := make(chan bool, 1)
  
  	go writeData(intchan)
  	go readData(intchan, exitchan)
  	time.Sleep(time.Second * 10)
  }
  
  输出：
  读到数据：0
  写入：0
  写入：1
  写入：2
  写入：3
  写入：4
  写入：5
  读到数据：1
  读到数据：2
  读到数据：3
  读到数据：4
  读到数据：5
  读到数据：6
  写入：6
  写入：7
  写入：8
  写入：9
  写入：10
  写入：11
  读到数据：7
  读到数据：8
  读到数据：9
  读到数据：10
  读到数据：11
  读到数据：12
  写入：12
  写入：13
  写入：14
  写入：15
  写入：16
  写入：17
  读到数据：13
  读到数据：14
  读到数据：15
  读到数据：16
  读到数据：17
  读到数据：18
  写入：18
  写入：19
  读到数据：19
  ```

  可以看到，虽然可能写入的速度很快，占满了管道。这样可以理解为：只要这个管道他是在“流动”的，就不会发生阻塞，也就是说有读有写。



- ### 应用实例

  统计1~200000中的数字中，哪些是素数？

  思路分析：

  1. 传统的方法就是写一个循环，循环的判断每一个数字是不是素数
  2. 使用并发或者并行的方式，将统计素数的任务分配给多个(4个吧)goroutine去完成，这时候就会用到goroutine

  代码分析：

  - 主协程首先启动一个协程**putNum**，用于向管道**intChan**中不停的写入1~200000的数字
  - 主线程再起四个协程**primeNum**，从**intChan**中取出数字，并计算是否为素数
  - 如果计算出是素数，将这个数字写入一个**resultChan**中去
  - 一个**primeNum**没有数据可取的时候，就往exitChan中传一个值，管道里面有4个才退出

- ### **代码实现**

```go
package main

import (
	"fmt"
	"time"
)

func main() {
	intChan := make(chan int, 10000)  // 放入数字
	primeChan := make(chan int, 8000) // 放入结果
	// 标识可以进行退出的管道
	exitChan := make(chan bool, 4)
	// 开启协程，放入数字
	go putNum(intChan)

	// 开启四个协程，判断取到的数字是否是素数,如果是，就放到primeChan中
	for i := 0; i < 4; i++ {
		go primeNum(intChan, primeChan, exitChan)
	}

	// 主线程进行处理, 只要能从这个exitXChan中取出四个东西出来就关闭,不然就阻塞在这

	go func() {
		for i := 0; i < 4; i++ {
			<-exitChan
		}
		// 当我们取出了四个结果的时候，就可以放心关闭primeChan
		close(primeChan)
	}()

	//遍历primeChan 把结果取出来
	for {
		res, ok := <-primeChan
		if !ok {
			break
		}
		fmt.Printf("res: %v\n", res)
	}
	fmt.Println("主线程退出")
}

// 开启一个协程，写入1~200000   channel是引用类型
func putNum(intChan chan int) {
	for i := 0; i <= 200; i++ {
		intChan <- i // 向里面扔数据，扔完就关闭
	}
	close(intChan)
}
func primeNum(intChan chan int, primeChan chan int, exitChan chan bool) { // 从哪取出，送到哪儿去，确退出标识

	var flag bool // 标识素数?
	for {
		time.Sleep(time.Millisecond)
		num, ok := <-intChan
		if !ok {
			break
		}
		flag = true //默认是素数
		for i := 2; i < num; i++ {
			if num%i == 0 {
				flag = false // 不是素数，退出循环
				break
			}
		}
		if flag {
			primeChan <- num
		}
	}
	fmt.Println("协程因为取不到数据而退出了")
	// 这里取不到数据了，可以向exitChan发消息了
	exitChan <- true

}

输出：
res: 0
res: 1
res: 2
res: 3
res: 5
res: 7
res: 11
res: 13
res: 17
res: 19
res: 23
res: 29
res: 31
res: 37
res: 41
res: 43
res: 47
res: 53
res: 59
res: 61
res: 67
res: 71
res: 73
res: 79
res: 83
res: 89
res: 97
res: 101
res: 103
res: 107
res: 109
res: 113
res: 127
res: 131
res: 137
res: 139
res: 149
res: 151
res: 157
res: 163
res: 167
res: 173
res: 179
res: 181
res: 191
res: 193
res: 197
res: 199
协程因为取不到数据而退出了
协程因为取不到数据而退出了
协程因为取不到数据而退出了
协程因为取不到数据而退出了
主线程退出
```



- ### Channel使用细节和注意事项

  - **channel可以声明为只读，或者只写性质**

    ```go
    // 声明只读的管道
    var chan1 <-chan int
    fmt.Println(chan1)
    num := <-chan1
    
    // 声明为只写的管道
    var chan2 chan<- int
    chan2 = make(chan int, 6)
    chan2 <- 2
    ```

  - **使用select可以解决从管道取数据的阻塞问题**

    ```go
    package main
    
    import (
    	"fmt"
    )
    
    func main() {
    
    	// 定义一个管道 10个数据int
    	intchan := make(chan int, 10)
    	for i := 0; i < 10; i++ {
    		intchan <- i
    	}
    	// 定义一个管道 5个数据string
    	stringChan := make(chan string, 5)
    	for i := 0; i < 5; i++ {
    		stringChan <- "this is num :" + fmt.Sprintf("%d", i)
    	}
    
    	// 传统的方法在遍历管道时，如果不关闭会导致死锁deadlock
    	// 在实际开发中，有可能不好确定什么时候关闭管道
    	// 可以使用select方法
    	for {
    		select {
    		case v := <-intchan: // 如果管道最终一直没有关闭，也不会一直阻塞而导致死锁
    			fmt.Printf("从intChan读取了数字%v\n", v)
    		// 会自动的到下一个case去进行匹配
    		case v := <-stringChan:
    			fmt.Printf("%v\n", v)
    		default:
    			fmt.Println("都取不到数据了")
    			return
    		}
    	}
    }
    
    输出：
    this is num :0
    this is num :1
    this is num :2
    从intChan读取了数字0
    this is num :3
    this is num :4
    从intChan读取了数字1
    从intChan读取了数字2
    从intChan读取了数字3
    从intChan读取了数字4
    从intChan读取了数字5
    从intChan读取了数字6
    从intChan读取了数字7
    从intChan读取了数字8
    从intChan读取了数字9
    都取不到数据了
    ```

    

  - **`goroutine`中使用recover，解决协程中出现panic，导致程序崩溃问题**

    > Recover 是一个Go语言的内建函数，可以让进入宕机流程中的 goroutine 恢复过来，recover 仅在延迟函数 defer 中有效，在正常的执行过程中，调用 recover 会返回 nil 并且没有其他任何效果，如果当前的 goroutine 陷入panic，调用 recover 可以捕获到 panic 的输入值，并且恢复正常的执行。
    >
    > 通常来说，不应该对进入 panic 宕机的程序做任何处理，但有时，需要我们可以从宕机中恢复，至少我们可以在程序崩溃前，做一些操作，举个例子，当 web 服务器遇到不可预料的严重问题时，在崩溃前应该将所有的连接关闭，如果不做任何处理，会使得客户端一直处于等待状态，如果 web 服务器还在开发阶段，服务器甚至可以将异常信息反馈到客户端，帮助调试。
    >
    > #### 提示
    >
    > 在其他语言里，宕机往往以异常的形式存在，底层抛出异常，上层逻辑通过 try/catch 机制捕获异常，没有被捕获的严重异常会导致宕机，捕获的异常可以被忽略，让代码继续运行。
    >
    > Go语言没有异常系统，其使用 panic 触发宕机类似于其他语言的抛出异常，recover 的宕机恢复机制就对应其他语言中的 try/catch 机制。

    例如有两个goroutine，我们希望在其中一个goroutine发送panic的时候，不要影响到我其他协程和主线程的正常执行

    ```go
    package main
    
    import (
    	"fmt"
    	"time"
    )
    
    func sayHello() {
    	for i := 0; i <= 5; i++ {
    		fmt.Println("hello,Hud!")
    	}
    }
    
    func test() {
    	// 这里使用defer + recover
    	defer func() {
    		if err := recover(); err != nil {
    			fmt.Println("test()发生错误", err)
    		}
    	}()
    	panic("fuck in test")
    }
    
    func main() {
    	go sayHello()
    	go test()
    	for i := 0; i < 5; i++ {
    		time.Sleep(time.Second)
    		fmt.Println("fuck")
    	}
    }
    
    输出：
    test()发生错误 fuck in test
    hello,Hud!
    hello,Hud!
    hello,Hud!
    hello,Hud!
    hello,Hud!
    hello,Hud!
    fuck
    fuck
    fuck
    fuck
    fuck
    ```

    在这里可以看到：在使用了recover之后，即使在协程中出现了panic情况，但是不影响其他协程协程和主线程的正常执行，而且错误会被输出出来、、

    

## 27. 反射

### 基本介绍

1. 反射可以在运行时动态获取变量的各种信息，比如变量的类型、类别
2. 如果是结构体变量，还可以获取到结构体本身的信息，包括结构体的字段和方法
3. 通过反射，可以修改变量的值，可以调用关联的方法
4. 使用反射，需要import( "reflect")

- ## package reflect

```
import "reflect"
```

reflect包实现了运行时反射，允许程序操作任意类型的对象。典型用法是用静态类型interface{}保存一个值，通过调用TypeOf获取其动态类型信息，该函数返回一个Type类型值。调用ValueOf函数返回一个Value类型值，该值代表运行时的数据。Zero接受一个Type类型参数并返回一个代表该类型零值的Value类型值



在实际开发中，有时候会专门定义函数用作反射

```go
// 专门用于做反射
func test(b interface{})
	// 如何将interface{}转成reflect.Value
	rVal := refelect.ValueOf(b)
	
	// 如何将reflect.Value -> interface{}
	iVal:=rVal.Interface{}

	//如何将interface{}转成原来的变量类型 使用类型断言
	v :=iVal.(原来的类型)
```



### 反射的入门

**快速入门说明**

- 编写一个案例，演示对(基本数据类型、interface{}、`reflect.Value`)进行反射的基本操作

```go
package main

import (
	"fmt"
	"reflect"
)

// 编写一个案例，演示对(基本数据类型、interface{}、`reflect.Value`)进行反射的基本操作
func reflectTest(i interface{}) {
	// 通过反射获取传入变量的type、kind和值
	// 现获取到reflect.type
	rfltyp := reflect.TypeOf(i)
	fmt.Printf("Type: %v\n", rfltyp)

	// 获取reflect.value类型 (取得的类型是不是int类型了reflect.Value)
	rflVal := reflect.ValueOf(i)
	fmt.Printf("Value: %v\n", rflVal)
	fmt.Printf("Type: %T\n", rflVal)
	// 如果我要拿到它的值，并且要返回一个真实的int类型
	realint := reflect.ValueOf(i).Int() + 2
	fmt.Printf("realint: %v\n", realint)
	fmt.Printf("realint_Type: %T\n", realint)

	// 下面我们将rVal转成interface{}
	inter := rflVal.Interface()
	// 将inter通过类型断言转换为需要的类型
	num2 := inter.(int)
	fmt.Printf("num2: %v\n", num2)
	fmt.Printf("num2: %T\n", num2)
}

func main() {
	// 先定义一个int类型
	var num int = 100
	reflectTest(num)
}

输出：
Type: int
Value: 100
Value: reflect.Value
realint: 102
realint_Type: int64
num2: 100
num2: int
```

- 对结构体类型进行反射

  ```go
  type players struct {
  	name string
  	num  int
  }
  
  // 编写一个案例，演示对结构体类型、interface{}、reflect.Value
  func reflectStruct(i interface{}) {
  	// 获取reflect.type
  	rfltype := reflect.TypeOf(i)
  	fmt.Printf("rfltype: %v\n", rfltype)
  	fmt.Printf("rfltype'Type: %T\n", rfltype)
  
  	// 获取reflect.Value
  	rflvalue := reflect.ValueOf(i)
  	fmt.Printf("rflvalue: %v\n", rflvalue)
  	fmt.Printf("rflvalue Type: %T\n", rflvalue)
  
  	// 将rflvalue转成interface{}类型
  	iV := rflvalue.Interface()
  	fmt.Printf("iV: %v type:%T\n", iV, iV)
  
  }
  
  func main() {
  	james := players{"james", 23}
  	reflectStruct(james)
  }
  
  输出:
  rfltype: main.players
  rfltype'Type: *reflect.rtype
  rflvalue: {james 23}
  rflvalue Type: reflect.Value
  iV: {james 23} type:main.players
  ```
  
  使用switch加入类型断言，可以让语句变得更加灵活：`switch x.(type)` 



### 反射的注意事项和细节

1. reflect.Value.Kind,获取变量的类别，返回的是一个常量【手册】

   ```go
   func reflectStruct(i interface{}) {
   	rfltype := reflect.TypeOf(i)
   
   	rflvalue := reflect.ValueOf(i)
   
   	// 获取到对应变量的kind
   	// rtltype.Kind() ==>获取
   	// rflvalue.Kind() ==>也可以获取
   	
   	fmt.Println("获取kind----------")
   	kind1 := rfltype.Kind()
   	kind2 := rflvalue.Kind()
   	fmt.Printf("rfltype'Kind: %v\n", kind1)
   	fmt.Printf("rflvalue'Kind: %v\n", kind2)
   
   }
   
   输出：
   获取kind----------
   rfltype'Kind: struct
   rflvalue'Kind: struct
   ```

2. Type是类型，Kind是类别，Type和Kind可能是相同的，也可能是不同的，比如

   ```go
   var num int = 10  // num的type和kind都是int
   // 再比如
   type players struct {
   	name string
   	num  int
   }
   // type是mian.Players 但是kind是struct
   ```

3. 通过反射可以让变量在interface{}和`Reflect.Value`之间相互转换

4. 使用反射的方式来获取变量的值(并返回对应的类型，要求数据类型匹配)，比如x的类型是Int，那么就要用`reflect.Value.Int()`，否则会报panic

5. 通过反射来修改变量，注意当使用`SetXxx`方法来设置需要通过对应的指针类型来完成，这样才能传入变量的值，同时需要使用到`reflect.Value.Elem()`方法

   #### func (Value) [SetInt](https://github.com/golang/go/blob/master/src/reflect/value.go?name=release#1576)

   ```
   func (v Value) SetInt(x int64)
   ```

   **设置v的持有值。如果v的Kind不是`Int、Int8、Int16、Int32、Int64`之一或者v.CanSet()返回假，会panic。**

   #### func (Value) [Elem](https://github.com/golang/go/blob/master/src/reflect/value.go?name=release#831)

   ```
   func (v Value) Elem() Value
   ```

   **Elem返回v持有的接口保管的值的Value封装，或者v持有的指针指向的值的Value封装。如果v的Kind不是Interface或Ptr会panic；如果v持有的值为nil，会返回Value零值。**

   ------

   用这两个方法，对反射的值进行修改。首先第一点，我们构建的反射的形式参数一般是一个空接口类型,需要改变原本变量的值，那么值传递肯定是不够的，我们需要进行指针传递，查看一下传递进来的类别：

   ```go
   func reflectElem(i interface{}) {
   	rflValue := reflect.ValueOf(i)
   	fmt.Printf("kind: %v\n", rflValue.Kind())
   }
   func main() {
   	var num int = 10
   	reflectElem(&num)
   }
   输出：
   kind: ptr
   ```

   是一个指针，但是从上面的方法中我们可以看到：**`func (v Value) SetInt(x int64)`**作用的对象是value类型，所以还需要使用到Elem这个方法

   ```go
   package main
   
   import (
   	"fmt"
   	"reflect"
   )
   
   // 通过反射，修改num int 的值
   // 修改结构体字段的值
   
   func reflectElem(i interface{}) {
   	rflValue := reflect.ValueOf(i)
   	rflValue.Elem().SetInt(20)
   }
   func main() {
   	var num int = 10
   	reflectElem(&num)
   	fmt.Printf("num: %v\n", num)
   }
   
   输出：
   num: 20
   ```



### 反射练习

- **给你一个变量`var v float64 = 1.2` ，请使用反射来得到它的`reflect.value`，然后获取对应的Type，Kind和值，并将`reflect.Value`转换成interface{}，再将interface{}转换为`float64`**

  ```go
  package main
  
  import (
  	"fmt"
  	"reflect"
  )
  
  func reflectValue(i interface{}) {
  	rflValue := reflect.ValueOf(i)
  	fmt.Printf("rflValue: %v\n", rflValue)
  	rflType := reflect.TypeOf(i)
  	fmt.Printf("rflType: %v\n", rflType)
  	fmt.Printf("kind:%v\n", rflValue.Kind())
  
  	a2 := rflValue.Interface()
  	fmt.Printf("a2: %v\n", a2)
  	fmt.Printf("a2: %T\n", a2)
  	f := a2.(float64)
  	fmt.Printf("f: %v\n", f)
  	fmt.Printf("f: %T\n", f)
  
  }
  
  func main() {
  	var a float64 = 1.2
  	reflectValue(a)
  }
  
  输出：
  rflValue: 1.2
  rflType: float64
  kind:float64
  a2: 1.2
  a2: float64
  f: 1.2
  f: float64
  ```



### 反射实践

这里有要看两个方法

#### func (Value) [Method](https://github.com/golang/go/blob/master/src/reflect/value.go?name=release#1272)

```go
func (v Value) Method(i int) Value
```

返回v持有值类型的第i个方法的已绑定（到v的持有值的）状态的函数形式的Value封装。返回值调用Call方法时不应包含接收者；返回值持有的函数总是使用v的持有者作为接收者（即第一个参数）。如果i出界，或者v的持有值是接口类型的零值（nil），会panic。

#### func (Value) [Call](https://github.com/golang/go/blob/master/src/reflect/value.go?name=release#408)

```go
func (v Value) Call(in []Value) []Value
```

Call方法使用输入的参数in调用v持有的函数。例如，如果len(in) == 3，v.Call(in)代表调用v(in[0], in[1], in[2])（其中Value值表示其持有值）。如果v的Kind不是Func会panic。它返回函数所有输出结果的Value封装的切片。和go代码一样，每一个输入实参的持有值都必须可以直接赋值给函数对应输入参数的类型。如果v持有值是可变参数函数，Call方法会自行创建一个代表可变参数的切片，将对应可变参数的值都拷贝到里面。



再讲一次这个，关于传入指针类型时候，例如传入参数是一个指针类型，在进行方法调用(对于`reflect.ValueOf()`获取到的值，是指针类型的，而在反射中我们一般调用的都是值类型)，需要用Elem()进行值的获取。

```go
// 使用反射来遍历结构体字段，调用结构体的方法，并获取结构体标签的值
package main

import (
	"fmt"
	"reflect"
)

type Player struct {
	Name string `json:"Name"`
	Num  int
	Team string
}

func (p Player) Play() {
	fmt.Printf("%v is shooting\n", p.Name)
	fmt.Printf("Number %v with a slam dunk\n", p.Num)
	fmt.Println("-----------PlayOver-----------")
}

func (p Player) Transfer(team string) {
	fmt.Printf("%v wants to transfer to %v\n", p.Name, team)
}

func (p *Player) Set(name string, num int, team string) {
	p.Name = name
	p.Num = num
	p.Team = team
}

func TestStruct(i interface{}) {
	rtype := reflect.TypeOf(i)
	rvalue := reflect.ValueOf(i)

	// 获取该结构体有几个字段
	num := rvalue.Elem().NumField()
	fmt.Printf("The struct has %d fields\n", num)
	for i := 0; i < num; i++ {
		fmt.Printf("Field %d : 值为 %v \n", i, rvalue.Elem().Field(i))
		// 获取到struct标签，注意需要通过reflect.Type来获取tag标签的值
		tagval := rtype.Elem().Field(i).Tag.Get("json")

		if tagval != "" {
			fmt.Printf("Field %d 的tag为:%v\n", i, tagval)
		}
	}

	// 获取该结构体有多少方法
	numofmethod := rvalue.NumMethod()
	fmt.Printf("The struct has %v Methods\n", numofmethod)

	// 这里选取第几个方法时候，排序顺序并不是按照方法在代码中出现呢的先后顺序
	// 而是根据方法名的首字母ASCII码进行排序
	fmt.Println("-------StartToUseMethod-------")
	rvalue.Method(0).Call(nil)
	var params []reflect.Value
	// 调用结构体的第二个方法
	// 首先声明一个reflect.Value类型的切片
	params = append(params, reflect.ValueOf("Heat"))
	rvalue.Method(2).Call(params)

	var param []reflect.Value
	param = append(param, reflect.ValueOf("Durant"))
	param = append(param, reflect.ValueOf(7))
	param = append(param, reflect.ValueOf("Nets"))

	rvalue.Method(1).Call(param)

}

func main() {
	var james Player = Player{
		Name: "james",
		Num:  23,
		Team: "Lakers",
	}
	TestStruct(&james)
	fmt.Printf("james: %v\n", james)
}


输出：
The struct has 3 fields
Field 0 : 值为 james 
Field 0 的tag为:Name
Field 1 : 值为 23
Field 2 : 值为 Lakers
The struct has 3 Methods
-------StartToUseMethod-------
james is shooting
Number 23 with a slam dunk
-----------PlayOver-----------
james wants to transfer 
james: {Durant 7 Nets}
```

这个关于结构体的反射的实践案例可以好好看一看，主要就是对于接收一个指针类型的结构体，使用Elem()方法对其进行接收



## 28. 网络编程

### 基本介绍

`Golang`的主要设计目标之一就是面向大规模后端服务程序，网络通信这块是服务端程序必不可少也是直观重要的一个部分。

**网络编程有两种：**

- **TCP socket编程：**网络编程的主流，之所以叫`TCP socket`编程，是因为底层是基于`TCP/IP`协议的。
- **B/S结构的http编程：**我们使用浏览器去访问网页时，使用的就是`http`协议，而`http`底层依旧是用`tcp socket`实现的



**协议(`TCP/IP`)**

传输控制协议/英特网互联协议，又叫网络通讯协议，这个协议是Internet最基本的协议、Internet国际互联网络的基础。简单的说就是由网络层的IP协议和传输层的TCP协议组成的。



**`IP`地址**

每个Internet上的主机和路由器都有一个**`IP`**地址，他包括网络号和主机号。`ip`地址有`ipv4`(32位)和`ipv6`(128位)，可以通过`ipconfig`来查看



**端口(port)**

我们这里所指的端口不是物理意义上的端口，而是特指TCP/IP协议中的端口，是逻辑意义上的端口，它其实是每一个使用网卡的程序的编号。每个数据包都发到主机的特定端口，所以不同的程序就能取到自己所需要的数据。



- 只要是做服务程序 都必须监听一个端口
- 该端口就是其他程序和该服务通讯的通道
- 一个电脑有65535个端口
- 一旦一个端口被某个程序监听了，那么其他的程序就不能再该端口上监听
  - 1~1024是固定端口(程序员不要用)
  - 22：`SSH` 远程登录协议 
  - 23：`talent`使用
  - 21：`ftp`使用
  - 25：`smtp`使用
  - 80：`iis`使用
  - 7：`echo`服务

- 在计算机(尤其是做服务器)中尽可能少的开端口
- 一个端口只能被一个程序监听
- 如果使用`netstat -an`可以查看本机有哪些端口在被监听
- 可以使用`netstat -anb`来查看监听端口的`pid`，再结合任务管理器关闭不安全的端口





### 快速入门

- #### 服务端的处理流程

  - 监听端口 8888
  - 创建客户端的tcp连接，建立客户端和服务器端的链接
  - 创建goroutine，处理该连接的请求

- #### 客户端的处理流程

  - 建立与服务器端的链接
  - 发送请求数据【终端】，接收服务器端返回的结果数据
  - 关闭连接

```
127.0.0.1是回送地址，指本地机，一般用来测试使用。回送地址（127.x.x.x）是本机回送地址（Loopback Address）,即主机IP堆栈内部的IP地址，主要用于网络软件测试以及本地机进程间通信，无论什么程序，一旦使用回送地址发送数据，协议软件立即返回之，不进行任何网络传输。
```

- ### type [Listener](https://github.com/golang/go/blob/master/src/net/net.go?name=release#266)

```
type Listener interface {
    // Addr返回该接口的网络地址
    Addr() Addr
    // Accept等待并返回下一个连接到该接口的连接
    Accept() (c Conn, err error)
    // Close关闭该接口，并使任何阻塞的Accept操作都会不再阻塞并返回错误。
    Close() error
}
```

Listener是一个用于面向流的网络协议的公用的网络监听器接口。多个线程可能会同时调用一个Listener的方法。

Example

- #### func [Listen](https://github.com/golang/go/blob/master/src/net/dial.go?name=release#261)

```
func Listen(net, laddr string) (Listener, error)
```

返回在一个本地网络地址laddr上监听的Listener。网络类型参数net必须是面向流的网络：

`"tcp"、"tcp4"、"tcp6"、"unix"或"unixpacket"`。参见Dial函数获取`laddr`的语法。



### Http基本操作

| **方法**    | **描述**                                                     |
| ----------- | ------------------------------------------------------------ |
| **GET**     | 请求指定的页面信息，并返回实体主体                           |
| **HEAD**    | 类似于**GET**请求，只不过返回的响应中没有具体的内容，用于获取表头 |
| **POST**    | 向指定资源提交数据进行处理请求(例如提交表单或者上传文件)，数据被包含在请求中，POST请求可能会导致新的资源的建立或者已有资源的修改 |
| **PUT**     | 从客户端向服务器传送的数据取代指定的文档的内容               |
| **DELETE**  | 请求服务器删除指定的页面                                     |
| **CONNECT** | HTTP/1.1协议中预留给能够将连接改为管道方式的代理服务器       |
| **OPTIONS** | 允许客户端查看服务器的性能                                   |
| **TRACE**   | 回显服务器收到的请求，主要用于测试或者诊断                   |
| **PATCH**   | 是对PUT方法的补充，用来对已知的资源进行局部更新              |



- #### **`http GET`**

  **请求指定页面信息，并返回实体主体**

  ```go
  package main
  
  import (
  	"fmt"
  	"io/ioutil"
  	"log"
  	"net/http"
  )
  
  func main() {
  	resp, err := http.Get("http://www.baidu.com")
  	if err != nil {
  		log.Fatal(err)
  	}
  	defer resp.Body.Close()
  	data, err := ioutil.ReadAll(resp.Body)
  	fmt.Println(string(data))
  }
  
  ```

- #### **`http Post`**

  **向目标服务器传输数据**

  ```go
  package main
  
  import (
  	"fmt"
  	"io/ioutil"
  	"log"
  	"net/http"
  	"strings"
  )
  
  func main() {
  	r := strings.NewReader("foooo")
  	resp, err := http.Post("https://www.baidu.com", "*/*", r)
  	if err != nil {
  		log.Fatal(err)
  	}
  	defer resp.Body.Close()
  	data, err := ioutil.ReadAll(resp.Body)
  	fmt.Println(string(data))
  }
  
  ```


### Golang HTTP服务

- `ServerMux：golang`原生支持的请求分发器，可以通过路径+处理方法来对不同的URL提供服务

  ```go
  package main
  
  import (
  	"net/http"
  )
  
  func main() {
  	mux := http.NewServeMux()
  	mux.Handle("/hello", http.HandlerFunc(func(writer http.ResponseWriter, request *http.Request) {
  		writer.Write([]byte("hello"))
  	}))
  	mux.Handle("/rank", http.HandlerFunc(func(writer http.ResponseWriter, request *http.Request) {
  		writer.Write([]byte("rank"))
  	}))
  	mux.Handle("/history/Hud", http.HandlerFunc(func(writer http.ResponseWriter, request *http.Request) {
  		//todo call rank function
  		writer.Write([]byte("Hud's History"))
  	}))
  	http.ListenAndServe(":8080", mux)
  }
  ```
  

### http Request

#### - Body

Body: 只能读一次，意味着你读了别人就不能读了，别人读了你就不能读了

```go
func readBodyOnce(w http.ResponseWriter, r *http.Request) {
	body, err := io.ReadAll(r.Body)
	if err != nil {
		fmt.Fprintf(w, "read body failed: %v", err)
		// 记住要返回，不然就还会执行后面的代码
		return
	}
	// 类型转换，将 []byte 转换为 string
	fmt.Fprintf(w, "read the data: %s \n", string(body))

	// 尝试再次读取，啥也读不到，但是也不会报错
	body, err = io.ReadAll(r.Body)
	if err != nil {
		// 不会进来这里
		fmt.Fprintf(w, "read the data one more time got error: %v", err)
		return
	}
	fmt.Fprintf(w, "read the data one more time: [%s] and read data length %d \n", string(body), len(body))
}
```

利用PostMan对8080端口进行Post：

```
POST --> this is post body

返回：
read the data: this is post body 
read the data one more time: [] and read data length 0 
```



#### - GetBody

原则上是可以读多次的，但是在原生的**`http.Request`**t里面，这个是nil

所以有一些Web框架会在收到请求之后，第一件事情就是给**`GetBody`**赋值

```go
func getBodyIsNil(w http.ResponseWriter, r *http.Request) {
	if r.GetBody == nil {
		fmt.Fprint(w, "GetBody is nil\n")
	} else {
		fmt.Fprintf(w, "GetBody not nil")
	}
}
```

利用PostMan对8080端口进行Post：

```
POST --> localhost:8080 this is post body

返回：
GetBody is nil
```



#### - Query

除了Body，我们还可能传递参数的地方就是Query

也就是`http://xxx.com/yourpath?**id=123**` ，所有的值都被解释为字符串，所以需要自己解析为数字等

```go
func queryParams(w http.ResponseWriter, r *http.Request) {
	values := r.URL.Query()
	fmt.Fprintf(w, "query is %v\n", values)
}

func main(){
    http.HandleFunc("/url/query", queryParams)
}
```

```
POST --> localhost:8080/url/query?name=hud

返回：
query is map[name:[hud]]

```



#### - URL

**包含路径方面的所有信息和一些很有用的操作**

- URL里面Host不一定有值
- r.Host里面一般都有值，是Host这个header的值
- RawPath也是不一定有
- Path肯定有

```go
func wholeURL(w http.ResponseWriter, r *http.Request) {
	data, _ := json.Marshal(r.URL)
	fmt.Fprintf(w, string(data))
}
```

```json
POST  --> localhost:8080/wholeURL

返回:
{
    "Scheme": "",
    "Opaque": "",
    "User": null,
    "Host": "",
    "Path": "/wholeURL",
    "RawPath": "",
    "OmitHost": false,
    "ForceQuery": false,
    "RawQuery": "",
    "Fragment": "",
    "RawFragment": ""
}

```

#### - Header

**header大体上是两类：一类是http预定义的，一类是自己定义的**

- Go会自动将header名字转为标准名字——其实就是就是大小写调整
- 一般会用X开头来表明是自己定义的，比如说X-mycompany-your=header

```go
func header(w http.ResponseWriter, r *http.Request) {
	fmt.Fprintf(w, "header is %v", header)
}
```

```
POST --> localhost:8080/header
Headers:
	Key : X-Hud-key
	Value : 

返回:
header is map[Accept:[*/*] Accept-Encoding:[gzip, deflate, br] Cache-Control:[no-cache] Connection:[keep-alive] Content-Length:[0] Postman-Token:[f408e885-b803-449b-a253-5db834f99476] User-Agent:[PostmanRuntime/7.30.0]]

```



#### - Form

- `Form`和`ParseForm`
- **要先调用`ParseForm`**
- 建议加上**Content-Type**`:application/x-www-form-urlencoded`

```go
func form(w http.ResponseWriter, r *http.Request) {
	fmt.Fprintf(w, "before parse form %v\n", r.Form)
	err := r.ParseForm()
	if err != nil {
		fmt.Fprintf(w, "parse form error %v\n", r.Form)
	}
	fmt.Fprintf(w, "after parse form %v\n", r.Form)
}
```

```
POST --> localhost:8080/form?name=hud

返回：
before parse form map[]
after parse form map[name:[hud]]
```

- #### HTTP库使用总结

  - Body和GetBody：重点在于Body是一次性的，而GetBody默认情况下是没有，一般中间件会考虑帮你注入这个方法
  - URL：注意URL中的字段的含义可能并不如你期望的那样
  - Form：记得调用前线用ParseForm，别忘了在请求里面加上http头



### RESTFul API

#### 定义

应用于REST设计风格的**Web API**称为**RESTful API**，他从以下三个方面资源进行定义：

- 直观简短的资源地址：**URI**，比如http://example.com/resources.

- 传输的资源，Web服务接受与返回的互联网媒体类型，比如：**JSON、XML、YAML**

- 对资源的操作：Web服务在资源上所支持的一系列**请求方法（比如：POST、GET、PUT或DELETE）**

  - #### **简单来说，就是http method决定了操作，http path决定了操作对象**



### Context

#### Beego Context 设计

```go
type Context struct {
	Input          *BeegoInput
	Output         *BeegoOutput
	Request        *http.Request
	ResponseWriter *Response
	_xsrfToken     string
}
```

- Input: 对**输入**的封装

- Output：对**输出**的封装

- Response: 对**响应**的封装

```go
type BeegoInput struct {
	Context       *Context
	CruSession    session.Store
	pnames        []string
	pvalues       []string
	data          map[interface{}]interface{} // store some values in this context when calling context in filter or controller.
	dataLock      sync.RWMutex
	RequestBody   []byte
	RunMethod     string
	RunController reflect.Type
}
```

- **反向引用了 Context**
- 直接耦合了 Session
- 维持了不同部分的输入

```go
type BeegoOutput struct {
	Context    *Context
	Status     int
	EnableGzip bool
}
```

```go
type Response struct {
	http.ResponseWriter
	Started bool
	Status  int
	Elapsed time.Duration
}
```

- 反向引用了 Context
- 维持住了 Status，即 HTTP响应码



#### Gin Context设计

```go
type Context struct {
	writermem responseWriter
	Request   *http.Request
	Writer    ResponseWriter

	Params   Params
	handlers HandlersChain
	index    int8
	fullPath string

	engine       *Engine
	params       *Params
	skippedNodes *[]skippedNode

	// This mutex protects Keys map.
	mu sync.RWMutex

	// Keys is a key/value pair exclusively for the context of each request.
	Keys map[string]any

	// Errors is a list of errors attached to all the handlers/middlewares who used this context.
	Errors errorMsgs

	// Accepted defines a list of manually accepted formats for content negotiation.
	Accepted []string

	// queryCache caches the query result from c.Request.URL.Query().
	queryCache url.Values

	// formCache caches c.Request.PostForm, which contains the parsed form data from POST, PATCH,
	// or PUT body parameters.
	formCache url.Values

	// SameSite allows a server to define a cookie attribute making it impossible for
	// the browser to send this cookie along with cross-site requests.
	sameSite http.SameSite
}
```

- Gin 的 Context 也是放了一些和输入输出有关的字段。
- 这些字段不必细究都是用来干什么的。
- 另外一个是它内部还有缓存，避免了重复读取和解析的开销。



#### Echo Context设计

```go
Context interface {
		// Request returns `*http.Request`.
		Request() *http.Request

		// SetRequest sets `*http.Request`.
		SetRequest(r *http.Request)

		// SetResponse sets `*Response`.
		SetResponse(r *Response)

		// Response returns `*Response`.
		Response() *Response

		// IsTLS returns true if HTTP connection is TLS otherwise false.
		IsTLS() bool

		// IsWebSocket returns true if HTTP connection is WebSocket otherwise false.
		IsWebSocket() bool

		// Scheme returns the HTTP protocol scheme, `http` or `https`.
		Scheme() string

		// RealIP returns the client's network address based on `X-Forwarded-For`
		// or `X-Real-IP` request header.
		// The behavior can be configured using `Echo#IPExtractor`.
		RealIP() string

		// Path returns the registered path for the handler.
		Path() string

		// SetPath sets the registered path for the handler.
		SetPath(p string)

		// Param returns path parameter by name.
		Param(name string) string

		// ParamNames returns path parameter names.
		ParamNames() []string

		// SetParamNames sets path parameter names.
		SetParamNames(names ...string)

		// ParamValues returns path parameter values.
		ParamValues() []string

		// SetParamValues sets path parameter values.
		SetParamValues(values ...string)

		// QueryParam returns the query param for the provided name.
		QueryParam(name string) string

		// QueryParams returns the query parameters as `url.Values`.
		QueryParams() url.Values

		// QueryString returns the URL query string.
		QueryString() string

		// FormValue returns the form field value for the provided name.
		FormValue(name string) string

		// FormParams returns the form parameters as `url.Values`.
		FormParams() (url.Values, error)

		// FormFile returns the multipart form file for the provided name.
		FormFile(name string) (*multipart.FileHeader, error)

		// MultipartForm returns the multipart form.
		MultipartForm() (*multipart.Form, error)

		// Cookie returns the named cookie provided in the request.
		Cookie(name string) (*http.Cookie, error)

		// SetCookie adds a `Set-Cookie` header in HTTP response.
		SetCookie(cookie *http.Cookie)

		// Cookies returns the HTTP cookies sent with the request.
		Cookies() []*http.Cookie

		// Get retrieves data from the context.
		Get(key string) interface{}

		// Set saves data in the context.
		Set(key string, val interface{})

		// Bind binds the request body into provided type `i`. The default binder
		// does it based on Content-Type header.
		Bind(i interface{}) error

		// Validate validates provided `i`. It is usually called after `Context#Bind()`.
		// Validator must be registered using `Echo#Validator`.
		Validate(i interface{}) error

		// Render renders a template with data and sends a text/html response with status
		// code. Renderer must be registered using `Echo.Renderer`.
		Render(code int, name string, data interface{}) error

		// HTML sends an HTTP response with status code.
		HTML(code int, html string) error

		// HTMLBlob sends an HTTP blob response with status code.
		HTMLBlob(code int, b []byte) error

		// String sends a string response with status code.
		String(code int, s string) error

		// JSON sends a JSON response with status code.
		JSON(code int, i interface{}) error

		// JSONPretty sends a pretty-print JSON with status code.
		JSONPretty(code int, i interface{}, indent string) error

		// JSONBlob sends a JSON blob response with status code.
		JSONBlob(code int, b []byte) error

		// JSONP sends a JSONP response with status code. It uses `callback` to construct
		// the JSONP payload.
		JSONP(code int, callback string, i interface{}) error

		// JSONPBlob sends a JSONP blob response with status code. It uses `callback`
		// to construct the JSONP payload.
		JSONPBlob(code int, callback string, b []byte) error

		// XML sends an XML response with status code.
		XML(code int, i interface{}) error

		// XMLPretty sends a pretty-print XML with status code.
		XMLPretty(code int, i interface{}, indent string) error

		// XMLBlob sends an XML blob response with status code.
		XMLBlob(code int, b []byte) error

		// Blob sends a blob response with status code and content type.
		Blob(code int, contentType string, b []byte) error

		// Stream sends a streaming response with status code and content type.
		Stream(code int, contentType string, r io.Reader) error

		// File sends a response with the content of the file.
		File(file string) error

		// Attachment sends a response as attachment, prompting client to save the
		// file.
		Attachment(file string, name string) error

		// Inline sends a response as inline, opening the file in the browser.
		Inline(file string, name string) error

		// NoContent sends a response with no body and a status code.
		NoContent(code int) error

		// Redirect redirects the request to a provided URL with status code.
		Redirect(code int, url string) error

		// Error invokes the registered global HTTP error handler. Generally used by middleware.
		// A side-effect of calling global error handler is that now Response has been committed (sent to the client) and
		// middlewares up in chain can not change Response status code or Response body anymore.
		//
		// Avoid using this method in handlers as no middleware will be able to effectively handle errors after that.
		Error(err error)

		// Handler returns the matched handler by router.
		Handler() HandlerFunc

		// SetHandler sets the matched handler by router.
		SetHandler(h HandlerFunc)

		// Logger returns the `Logger` instance.
		Logger() Logger

		// SetLogger Set the logger
		SetLogger(l Logger)

		// Echo returns the `Echo` instance.
		Echo() *Echo

		// Reset resets the context after request completes. It must be called along
		// with `Echo#AcquireContext()` and `Echo#ReleaseContext()`.
		// See `Echo#ServeHTTP()`
		Reset(r *http.Request, w http.ResponseWriter)
	}Context interface {
		// Request returns `*http.Request`.
		Request() *http.Request

		// SetRequest sets `*http.Request`.
		SetRequest(r *http.Request)

		// SetResponse sets `*Response`.
		SetResponse(r *Response)

		// Response returns `*Response`.
		Response() *Response

		// IsTLS returns true if HTTP connection is TLS otherwise false.
		IsTLS() bool

		// IsWebSocket returns true if HTTP connection is WebSocket otherwise false.
		IsWebSocket() bool

		// Scheme returns the HTTP protocol scheme, `http` or `https`.
		Scheme() string

		// RealIP returns the client's network address based on `X-Forwarded-For`
		// or `X-Real-IP` request header.
		// The behavior can be configured using `Echo#IPExtractor`.
		RealIP() string

		// Path returns the registered path for the handler.
		Path() string

		// SetPath sets the registered path for the handler.
		SetPath(p string)

		// Param returns path parameter by name.
		Param(name string) string

		// ParamNames returns path parameter names.
		ParamNames() []string

		// SetParamNames sets path parameter names.
		SetParamNames(names ...string)

		// ParamValues returns path parameter values.
		ParamValues() []string

		// SetParamValues sets path parameter values.
		SetParamValues(values ...string)

		// QueryParam returns the query param for the provided name.
		QueryParam(name string) string

		// QueryParams returns the query parameters as `url.Values`.
		QueryParams() url.Values

		// QueryString returns the URL query string.
		QueryString() string

		// FormValue returns the form field value for the provided name.
		FormValue(name string) string

		// FormParams returns the form parameters as `url.Values`.
		FormParams() (url.Values, error)

		// FormFile returns the multipart form file for the provided name.
		FormFile(name string) (*multipart.FileHeader, error)

		// MultipartForm returns the multipart form.
		MultipartForm() (*multipart.Form, error)

		// Cookie returns the named cookie provided in the request.
		Cookie(name string) (*http.Cookie, error)

		// SetCookie adds a `Set-Cookie` header in HTTP response.
		SetCookie(cookie *http.Cookie)

		// Cookies returns the HTTP cookies sent with the request.
		Cookies() []*http.Cookie

		// Get retrieves data from the context.
		Get(key string) interface{}

		// Set saves data in the context.
		Set(key string, val interface{})

		// Bind binds the request body into provided type `i`. The default binder
		// does it based on Content-Type header.
		Bind(i interface{}) error

		// Validate validates provided `i`. It is usually called after `Context#Bind()`.
		// Validator must be registered using `Echo#Validator`.
		Validate(i interface{}) error

		// Render renders a template with data and sends a text/html response with status
		// code. Renderer must be registered using `Echo.Renderer`.
		Render(code int, name string, data interface{}) error

		// HTML sends an HTTP response with status code.
		HTML(code int, html string) error

		// HTMLBlob sends an HTTP blob response with status code.
		HTMLBlob(code int, b []byte) error

		// String sends a string response with status code.
		String(code int, s string) error

		// JSON sends a JSON response with status code.
		JSON(code int, i interface{}) error

		// JSONPretty sends a pretty-print JSON with status code.
		JSONPretty(code int, i interface{}, indent string) error

		// JSONBlob sends a JSON blob response with status code.
		JSONBlob(code int, b []byte) error

		// JSONP sends a JSONP response with status code. It uses `callback` to construct
		// the JSONP payload.
		JSONP(code int, callback string, i interface{}) error

		// JSONPBlob sends a JSONP blob response with status code. It uses `callback`
		// to construct the JSONP payload.
		JSONPBlob(code int, callback string, b []byte) error

		// XML sends an XML response with status code.
		XML(code int, i interface{}) error

		// XMLPretty sends a pretty-print XML with status code.
		XMLPretty(code int, i interface{}, indent string) error

		// XMLBlob sends an XML blob response with status code.
		XMLBlob(code int, b []byte) error

		// Blob sends a blob response with status code and content type.
		Blob(code int, contentType string, b []byte) error

		// Stream sends a streaming response with status code and content type.
		Stream(code int, contentType string, r io.Reader) error

		// File sends a response with the content of the file.
		File(file string) error

		// Attachment sends a response as attachment, prompting client to save the
		// file.
		Attachment(file string, name string) error

		// Inline sends a response as inline, opening the file in the browser.
		Inline(file string, name string) error

		// NoContent sends a response with no body and a status code.
		NoContent(code int) error

		// Redirect redirects the request to a provided URL with status code.
		Redirect(code int, url string) error

		// Error invokes the registered global HTTP error handler. Generally used by middleware.
		// A side-effect of calling global error handler is that now Response has been committed (sent to the client) and
		// middlewares up in chain can not change Response status code or Response body anymore.
		//
		// Avoid using this method in handlers as no middleware will be able to effectively handle errors after that.
		Error(err error)

		// Handler returns the matched handler by router.
		Handler() HandlerFunc

		// SetHandler sets the matched handler by router.
		SetHandler(h HandlerFunc)

		// Logger returns the `Logger` instance.
		Logger() Logger

		// SetLogger Set the logger
		SetLogger(l Logger)

		// Echo returns the `Echo` instance.
		Echo() *Echo

		// Reset resets the context after request completes. It must be called along
		// with `Echo#AcquireContext()` and `Echo#ReleaseContext()`.
		// See `Echo#ServeHTTP()`
		Reset(r *http.Request, w http.ResponseWriter)
	}
```

```go
context struct {
		request  *http.Request
		response *Response
		path     string
		pnames   []string
		pvalues  []string
		query    url.Values
		handler  HandlerFunc
		store    Map
		echo     *Echo
		logger   Logger
		lock     sync.RWMutex
	}
```



- Echo 的 Context 被设计为接口，和 `Beego`、Gin 都有点不太一样。但是实际上，它只有一个实现 context。
- context 和 Beego、Gin 的都差不多，也就是各种字段维护了来自各个部分的输入或者输出。
- 特殊之处在于 context 本身维护了一个logger，还维护了一个 lock。将 logger 做到context 维度和将 context 用锁保护起来，都是很罕见的做法。



#### Context处理输入/输出

- #### **处理输入要解决的问题：**

  - 反序列化输入：将 Body 字节流转换成一个具体的类型
  - 处理表单输入：可以看做是一个和 JSON 或者 XML 差不多的一种特殊序列化方式
  - 处理查询参数：指从 URL 中的查询参数中读取值，并且转化为对应的类型
  - 处理路径参数：读取路径参数的值，并且转化为具体的类型 
  - 重复读取 **`body：http.Request`** 的 Body 默认是只能读取一次，不能重复读取的
  - 读取 Header：从 Header 里面读取出来特定的值，并且转化为对应的类型
  - 模糊读取：按照一定的顺序，尝试从 Body、Header、路径参数或者 Cookie 里面读取值，并且转化为特定类型



- **处理输出要解决的问题：**
  - 序列化输出：按照某种特定的格式输出数据，例如 JSON 或者 XML
  - 渲染页面：要考虑模板定位、命名和渲染的问题
  - 处理状态码：允许用户返回特定状态码的响应，例如 HTTP 404
  - 错误页面：特定 HTTP Status 或者 error 的时候，能够重定向到一个错误页面，例如404 被重定向到首页
  - 设置 Cookie ：设置 Cookie 的值
  - 设置 Header：往 Header 里面放一些东西



#### Body输入

JSON 作为最为常见的输入格式，可以率先支持。其余的类似于 XML 或者 `protobuf` 都可以按照类似的思路支持。

```go
type Context struct {
	Req  *http.Request
	Resp http.ResponseWriter
}

func (c *Context) BindJson(val any) error {
	if val == nil{
		return errors.New("web: Input can't be nil")
	}
    if c.Req.Body == nil {
		return errors.New("web: Body can't be nil")
	}
	decoder := json.NewDecoder(c.Req.Body)
	return decoder.Decode(val)
}
```

**问题：**

在 JSON 的反序列化过程中，其实有两个参数：

- **`UseNumber`**：如果为 true，并且我们没有显示声明数字类型，会使用 json 的 Number 类型来作为数字类型

- **`DisallowUnknownFields`**：禁止未知的字段，如果出现未知字段，那么会返回 error

针对这个问题的解决方案

- #### 方案1

**把这两个参数放在方法的参数当中：**

```go
func (c *Context) BindJson1(val any, useNumber bool, disallowUnknown bool) error {
	if val == nil {
		return errors.New("web: Input can't be nil")
	}
	if c.Req.Body == nil {
		return errors.New("web: Body can't be nil")
	}
	decoder := json.NewDecoder(c.Req.Body)
	// useNumber => 数字就会用Number来表示
	// 否则默认是float64
	if useNumber{
		decoder.UseNumber()
	}
	// 如果要是有一个未知的字段，就会报错
	// 比如说你User只有Name和Email两个字段
	// JSON里面额外多了一个Age字段，那么就会报错
	if disallowUnknown{
		decoder.DisallowUnknownFields()
	}
	return decoder.Decode(val)
}
```

- #### 方案2

**声明变量**

```go
var(
	JSONUseNumber = true
	JSONDisAllowUnknown = true
)

func (c *Context) BindJson2(val any) error {
	if val == nil {
		return errors.New("web: Input can't be nil")
	}
	if c.Req.Body == nil {
		return errors.New("web: Body can't be nil")
	}
	decoder := json.NewDecoder(c.Req.Body)
	// useNumber => 数字就会用Number来表示
	// 否则默认是float64
	if JSONUseNumber {
		decoder.UseNumber()
	}
	// 如果要是有一个未知的字段，就会报错
	// 比如说你User只有Name和Email两个字段
	// JSON里面额外多了一个Age字段，那么就会报错
	if JSONDisAllowUnknown {
		decoder.DisallowUnknownFields()
	}
	return decoder.Decode(val)
}
```

严谨地说，如果用户有这种需求，那么他可能需要的是：

- 整个应用级别上控制 `useNumber` 或者`disableUnknownFields`

- 单一 `HTTPServer` 实例上控制 `useNumber` 或者`disableUnknownFields`

- 特定路径下，例如在 /user/** 都为 true 或者都为false

- 特定路由下，例如在 /user/details 下都为 true 或者false

不同情况下框架支持的方式也不一样：

- 整个应用级别：维持两个全局变量

- `HTTPServer` 级别：在 `HTTPServer` 里面定义两个字段

- 引入类似 `BindJSONOpt` 的方法，用户灵活控制



#### 表单输入

表单在 Go 的 **`http.Request`** 里面有两个

- **`Form`**： 一个是 URL 里面的查询参数和 PATCH、POST、PUT的表单数据

- **`PostForm`**: PATCH、POST 或者 PUT body 参数

但是不管使用哪个，都要先使用 **`ParseForm`** 解析表单数据。、



表单在 Go 的 http.Request 里面有两个

- `Form`：基本上可以认为，所有的表单数据都能拿到

- `PostForm`：在编码是 `x-www-form-urlencoded` 的时候才能拿到

实际中我是不建议大家使用表单的，我一般只在 Body 里面用 JSON 通信，或者用 `protobuf` 通信。

```go
s.Post("/form", func(ctx *Context) {
		ctx.Req.ParseForm()
		ctx.Resp.Write([]byte("hello form"))
	})
```



#### 查询参数

所谓的查询参数，就是指在 URL 问号之后的部分。

例如 URL：http://localhost:8081/form?name=xiaoming&age=18

那么查询参数有两个：`name=xiaoming` 和 `age=18`

前面我们注意到，如果要是调用了 `ParseForm`，那么这部分也可以在 Form 里面找到。

问题：这个 `ParseQuery` 每次都会解析一遍查询串，在我们这里就是 name=xiaoming&age=18 字符串。

```go
func (c *Context) QueryValue1(key string) (string, error) {
	params := c.Req.URL.Query()
	if params == nil {
		return "", errors.New("web: 没有任何查询参数")
	}
	vals, ok := params[key]
	if !ok {
		return "", errors.New("web: 找不到这个key")
	}
	return vals[0], nil
}
```

**类似 Gin 框架那样，引入查询参数缓存。**

这个缓存是不存在所谓的失效不一致问题的，因为对于 Web 框架来说，请求收到之后，就是确切无疑，不会再变的。

```go
type Context struct {
	Req        *http.Request
	Resp       http.ResponseWriter
	PathParams map[string]string

	QueryValues url.Values
}

func (c *Context) QueryValue(key string) (string, error) {
	if c.QueryValues == nil {
		c.QueryValues = c.Req.URL.Query()
	}
	// 用户区别不出来是没有值，还是恰好是空的字符串
	return c.QueryValues.Get(key), nil
}

```

除了前面提到的类似 FormValueAsInt64 这种在 Context 上加方法的方案，还可以考虑 **`StringValue`** 的方案。这种方案参考了 `sql.Row` 。

构建一个结构体**`StringValue`**

```go
type StringValue struct {
	val string
	err error
}
```



#### 处理输出--JSON响应

这种设计非常简单，就是帮助用户将 `val` 转化一下。其它格式的输出也是类似的写法。

也可以考虑提供一个更加方便的 **`RespJSONOK`** 方法，这个就是看个人喜好了。

这里有一个问题，如果 val 已经是 string 或者 []byte了，那么用户该怎么办？val 是 string 或者 []byte 肯定不需要调用 **`RespJSON`**了，自己直接操作 Resp。

```go
type Context struct {
	Req        *http.Request
	Resp       http.ResponseWriter
	PathParams map[string]string

	queryValues url.Values
}

func (c *Context) RespJsonOk(val any) error {
	return c.RespJson(http.StatusOK,val)
}

func (c *Context) RespJson(status int, val any) error {
	data, err := json.Marshal(val)
	if err != nil {
		return err
	}
	c.Resp.WriteHeader(status)
	c.Resp.Header().Set("Content-Type", "application/json")
	c.Resp.Header().Set("Content-Length", strconv.Itoa(len(data)))
	n, err := c.Resp.Write(data)
	if n != len(data) { // 说明没写完
		return errors.New("web: 未写入全部数据")
	}
	return err
}
```



#### 处理输出--设置 Cookie

其实类似这种方法不是很有必要在我们 Context 里面再自己定义一遍的。因为用户完全可以自己调用这个`http.SetCookie` 的方法。

只不过对于新人来说，有这么一个方法可能更好一点。因为他们可能找不到 `http.SetCookie` 这个方法。

```go
func (c *Context) SetCookie(Cookie *http.Cookie)  {
	http.SetCookie(c.Resp,Cookie)
}
```



#### 处理输出 --错误页面

我们通常有一个需求，**是如果一个响应返回了404，那么应该重定向到一个默认页面，比如说重定位到首页。**

那么该怎么处理？

​		这里有一个很棘手的点：不是所有的 404 都是要重定向的。比如说你是异步加载数据的 RESTful 请求，例如在打开页面之后异步加载用户详情，即便 404 了也

不应该重定向。

如果使用`func (c *Context) ErrorPage(){}`这种方式，用户每次都需要进行检测是不是500,然后进行调用

**解决方案：AOP里解决**

## **29. Redis**

**`Redis`是`NoSQL`数据库，不是传统的关系型数据库。**

**`Redis`(Remote Dictionary Sever 远程字典服务器)，`Redis`的性能非常高，单机能够达到`15w qps`，通常适合做缓存，也可以持久化**

**`Redis`是完全开源免费的，高性能的(key/Value)分布式内存数据库，基于内存运行并支持持久化的`NoSQL`数据库，是最热门的`NoSQL`数据库之一，也成为数据结构服务器。**

### **Redis的基本使用**

**`Redis`安装好以后，默认有16个数据库，初始默认使用0号库，编号是0...15**

- #### **`Redis`的五大数据类型**

  **String(字符串)、Hash(哈希)、List(列表)、Set(集合)和`zset`(`sorted set` 有序集合)**

1. **添加key-val [set]**

   ```
   127.0.0.1:6379> set key1 hello
   OK
   127.0.0.1:6379> get key1
   "hello"
   ```

2. **查看当前数据库的key-val数量 [dbsize]**

   ```
   127.0.0.1:6379> dbsize
   (integer) 2
   ```

3. **清空当前数据库的key-val[flushdb]**

   ```
   127.0.0.1:6379> flushdb
   OK
   ```

4. **清空所有数据库的key-val[flushall]**

   ```
   127.0.0.1:6379> flushall
   OK
   (0.68s)
   ```

5. **切换redis数据库[select index]**

   ```
   127.0.0.1:6379> SELECT index
   (error) ERR invalid DB index
   ```

6. **获取key对应的值[get key]**

   ```
   127.0.0.1:6379[1]> get key1
   "Hud"
   ```

   

- ### **String**

  **string是`redis`最基本的类型，一个key对应一个value。**

  **string类型是二进制安全的，除普通字符串外，也可以存放图片等数据。**

  **`redis`中字符串value最大是512M**

  **举例：存放一个地址信息**

  - #### **增删改查 (`set | get | del`)**
  
  ```
  address 北京 天安门
  key: address
  value: 北京天安门
  ```

  **在`Redis`中，set指令：对应的key存在就相当于修改，如果不存在就相当于添加**
  
  ```
  127.0.0.1:6379> set address beijing
  OK
  127.0.0.1:6379> get address
  "beijing"
  127.0.0.1:6379> set address nanjing
  OK
  127.0.0.1:6379> get address
  "nanjing"
  127.0.0.1:6379> dbsize
  (integer) 2
  127.0.0.1:6379> del address
  (integer) 1
  127.0.0.1:6379> get address
  (nil)
  ```
  
  - #### **设置key value的生存时间 `setex(set with expire)`键秒值**
  
  ```
  127.0.0.1:6379> setex name1 10 Hud
  OK
  127.0.0.1:6379> get name1
  "Hud"
  127.0.0.1:6379> get name1
  "Hud"
  127.0.0.1:6379> get name1
  "Hud"
  127.0.0.1:6379> get name1
  (nil)
  ```
  
  **10秒钟后，已经消失了**
  
  - #### **`mset` 同时设置一个或多个key-value对**
  
    ```
    127.0.0.1:6379> mset man Hud girl Monica Cat Qb
    OK
    127.0.0.1:6379> dbsize
    (integer) 4
    127.0.0.1:6379> get man
    "Hud"
    127.0.0.1:6379> get girl
    "Monica"
    127.0.0.1:6379> get Cat
    "Qb"
    ```
  
  - #### **`mget` 同时获取一个或多个key-value对**
  
    ```
    127.0.0.1:6379> mget man girl
    1) "Hud"
    2) "Monica"
    ```





- ### **Hash(类似go里面的Map)**

  **`Redis hash`是一个键值对集合**

  **Redis hash是一个string类型的field和value的映射表 ，hash特别适合用于存储对象**

  **举例 ：存放一个user信息**

  **name : “hud” | age : 24 | job : "gopher"**          

  - #### **hset**  

    ```
    127.0.0.1:6379> hset user1 name "Hud"
    (integer) 1
    127.0.0.1:6379> hset user1 age 24
    (integer) 1
    127.0.0.1:6379> hset user1 job "gopher"
    (integer) 1
    ```

  - #### **hget**

    ```
    127.0.0.1:6379> hget user1 name
    "Hud"
    127.0.0.1:6379> hget user1 age
    "24"
    127.0.0.1:6379> hget user1 job
    "gopher"
    ```

  - #### **hgetall**

    ```
    127.0.0.1:6379> hgetall user1
    1) "name"		# 域
    2) "Hud"		# 值
    3) "age"
    4) "24"
    5) "job"
    6) "gopher"
    ```

  - #### **Hash使用细节和注意事项(hmset|hmget|hlen)**

    **在给user设置name和age时，前面我们是一步步设置的，使用`hmset`和`hmget`可以一次性来设置多个field的值和返回多个field的值和返回多个field的值,hlen可以统计一个hash有几个元素，hexists key field：查看hash表key中，给定域field是否存在**

    ```
    127.0.0.1:6379> hmset user2 name Monica age 22 job doctor
    OK
    127.0.0.1:6379> hmget user2
    (error) ERR wrong number of arguments for 'hmget' command
    127.0.0.1:6379> hmget user2 name age job
    1) "Monica"
    2) "22"
    3) "doctor"
    127.0.0.1:6379> hlen user2
    (integer) 3
    
    
    127.0.0.1:6379> hexists user1 job
    (integer) 1
    127.0.0.1:6379> hexists user1 money
    (integer) 0
    ```

    

- ### **List(列表)**

  **列表是简单的字符串列表，按照插入的顺序排序。你可以添加一个元素到列表的头部(左边)或者尾部(右边)**

  **List的本质是一个链表，List元素是有序的，元素的值可以重复。**

  **例如存放多个地址信息：**
  **`city : beijing shanghai nanjing` (`key:city` 三个元素)**

  

  - #### **lpush**

    ```
    127.0.0.1:6379> lpush city nanjing beijing shanghai
    (integer) 3
    ```

  - #### **lrange**

    ```
    127.0.0.1:6379> lrange city 0 -1
    1) "shanghai"
    2) "beijing"
    3) "nanjing"
    127.0.0.1:6379> lrange city 0 2
    1) "shanghai"
    2) "beijing"
    3) "nanjing"
    127.0.0.1:6379> lrange city 0 1
    1) "shanghai"
    2) "beijing"
    127.0.0.1:6379> lrange city 0 0
    1) "shanghai"
    ```

    **把List想象成一根管道，lpush就是从左边开始向里面扔，lrange从右边取。**

    #### **-- LRANGE key start stop**

    **返回列表key中指定区间内的元素，区间以偏移量start和stop指定。下标(index)参数strat和stop都以0为底，也就是说以0表示列表的第一个元素，以1表示列表的第二个元素，以此类推。**

    **你也可以使用负数下标，以-1表示列表的最后一个元素，-2表示列表的倒数第二个元素以此类推。**

    ```
    127.0.0.1:6379> rpush city tokyo
    (integer) 4
    127.0.0.1:6379> lrange city 0 -1
    1) "shanghai"
    2) "beijing"
    3) "nanjing"
    4) "tokyo"
    127.0.0.1:6379> lpush city chicago
    (integer) 5
    127.0.0.1:6379> lrange city 0 -1
    1) "chicago"
    2) "shanghai"
    3) "beijing"
    4) "nanjing"
    5) "tokyo"
    ```

    **这样看就比较好理解了，lpush/rpush就等于在左边或者右边新加一个上去，range就是从左右开始读**

  - #### **lpop/rpop**

    **从左或者右弹出一个元素，可以理解为堆栈的弹栈？**

    ```
    127.0.0.1:6379> lpop city
    "chicago"
    127.0.0.1:6379> rpop city
    "tokyo"
    
    现在看看列表里面的元素
    127.0.0.1:6379> lrange city 0 -1
    1) "shanghai"
    2) "beijing"
    3) "nanjing"
    ```

  - #### **del**

    **不想要这个列表了，直接删除**

    ```
    127.0.0.1:6379> del city
    (integer) 1
    127.0.0.1:6379> lrange city 0 -1
    (empty list or set)
    ```

    #### **List的使用细节和注意事项**

    1. **index，按照索引下标获得元素(从左到右，编号从0开始)**

    2. **LLEN key**

       **返回列表的长度，如果key不存在，则key被解释为一个空列表返回0**

       ```
       127.0.0.1:6379> lpush city nanjing beijing shanghai
       (integer) 3
       127.0.0.1:6379> llen city
       (integer) 3
       127.0.0.1:6379> llen cit
       (integer) 0
       ```

    3. **List数据可以从左边或者右边插入添加**

    4. **如果值全移除，那么对应的键也就消失了**



- ### **Set(集合)**

  **Redis的Set是string类型的无序集合**

  **底层是HashTable数据结构，Set也是存放很多字符串元素，字符串元素是无序的，而且元素的值不能重复**

  - #### **sadd/smembers 分别用来添加和查看集合元素**

    ```
    127.0.0.1:6379> sadd emails qitinayu2007@126.com qitianyu68@gamil.com
    (integer) 2
    127.0.0.1:6379> smembers emails
    1) "qitinayu2007@126.com"
    2) "qitianyu68@gamil.com"
    ```

  - #### **集合的CRUD操作**

    - **sadd 添加元素**

    - **smembers[取出所有值]**

    - **sismember[判断是否是成员]**

      ```
      127.0.0.1:6379> sismember emails qitianyu68@gmail.com
      (integer) 0
      127.0.0.1:6379> sismember emails qitianyu68@gamil.com		// 他妈的 这里打错了
      (integer) 1
      ```

    - **srem[删除指定值]**

      ```
      127.0.0.1:6379> srem emails qitianyu68@gamil.com
      (integer) 1
      ```

      

### **go连接Redis**

- #### **Installation**

**Install:**

```
go get -u github.com/go-redis/redis
```

**Import:**

```
import "github.com/go-redis/redis"
```

**[参考官方文档](https://pkg.go.dev/github.com/go-redis/redis#section-readme)**

- #### **Set/Get接口**

  **通过Golang添加和获取key-value**

  ```go
  package main
  
  import (
  	"fmt"
  	_ "github.com/garyburd/redigo/redis"  //两个都可以
  	"github.com/go-redis/redis"
  )
  
  func main() {
  	client := redis.NewClient(&redis.Options{
  		Addr:     "localhost:6379",
  		Password: "", // no password set
  		DB:       0,  // use default DB
  	})
  
  	// 测试连接是否成功
  	s, err := client.Ping().Result()
  	fmt.Printf("s: %v\n", s)
  	if err != nil {
  		fmt.Printf("err: %v\n", err)
  	}
  	defer client.Close()
  
  	// 基本的set和get操作
  	sc, err1 := client.Set("Name", "Hud", 0).Result()
  	if err1 != nil {
  		fmt.Printf("err1: %v\n", err1)
  	}
  	fmt.Printf("sc: %v\n", sc)
  
  	res, err := client.Get("Name").Result()
  	if err != nil {
  		fmt.Printf("err: %v\n", err)
  	}
  	fmt.Printf("%v\n", res)
  }
  
  输出：
  s: PONG
  sc: OK
  Hud
  ```

- #### **使用Hash的hset/hget接口**

  ```go
  func TestHash() {
  	// hmset
  	client.HSet("user", "name", "hud")
  	client.HSet("user", "age", "24")
  	client.HSet("user", "job", "Gopher")
  	redis.NewStringCmd(client.Do("hmset", "user", "address", "jianye", "email", "qitianyu2007@126.com"))
  	// hmget
  	i, err := client.HMGet("user", "name", "age", "job", "address", "email").Result()
  	if err != nil {
  		fmt.Printf("err: %v\n", err)
  	}
  	fmt.Printf("user: %v\n", i)
  }
  ```

  

- ### **`redis`链接池**

  **通过`Golang`对Redis操作，还可以通过Redis链接池，流程如下：**

  - **实现初始化一定数量的链接，放入到链接池**
  - **当Go需要操作Redis时，直接从Redis链接池中取出链接即可**
  - **这样可以节省临时获取Redis链接的时间，从而提高效率**

  **核心代码：**

  ```go 
  var pool *redis.Pool
  pool=&redis.Pool{
  	MaxIdle:8,  //最大空闲链接数
  	MaxActive:0  // 表示和数据库最大链接数，0表示没有限制
  	IdleTimeout:100, //最大空闲时间，例如100s内都没有用过这个链接，放回空闲
  	Dial:func()(redis.Conn,err){  //初始化链接的代码
  		return redis.Dial("tcp","localhost:6379") 
  	},
  }
  c:=pool.Get()	// 从链接池中取出一个链接
  pool.Close	// 关闭链接池，一旦链接池被关闭了，就不能再从链接池中取链接了
  ```
  
  **链接池使用案例**
  
  ```go
  package main
  
  import (
  	"fmt"
  
  	"github.com/garyburd/redigo/redis"
  )
  
  // 定义一个全局的pool
  var pool *redis.Pool
  
  // 当启动程序时候，就初始化这个链接池
  func init() {
  	pool = &redis.Pool{
  		MaxIdle:     8,   //最大空闲链接数
  		MaxActive:   0,   // 表示和数据库最大链接数，0表示没有限制
  		IdleTimeout: 100, //最大空闲时间，例如100s内都没有用过这个链接，放回空闲
  		Dial: func() (redis.Conn, error) { //初始化链接的代码
  			return redis.Dial("tcp", "localhost:6379")
  		},
  	}
  
  }
  func main() {
  	// 先从pool取出一个链接
  	c := pool.Get()
  	defer c.Close()
  
  	_, err := c.Do("set", "cat", "qb")
  	if err != nil {
  		fmt.Printf("err: %v\n", err)
  	}
  	reply, err2 := redis.String(c.Do("get", "cat"))
  	if err2 != nil {
  		fmt.Printf("err2: %v\n", err2)
  	}
  	fmt.Printf("reply: %v\n", reply)
  }
  ```
  
  
  
  

## **30. go语言与数据结构**

### **稀疏矩阵**

```go
package main

import "fmt"

type ValNode struct {
	row int
	col int
	val int
}

func main() {
	var chessMap [11][11]int //1表示黑棋 2表示白棋
	chessMap[1][2] = 1       //黑
	chessMap[2][3] = 2       //白

	// 输出看看原始的数组
	for _, v := range chessMap {

		for _, v2 := range v {
			fmt.Printf("%d\t", v2)
		}
		fmt.Println("")
	}

	// 3 转成稀疏数组
	// (1) 遍历CheesMap 如果发现有一个元素的值不等于0，那我们就创建一个node结构体
	// (2) 将其放入到对应的切片中即可
	var sparseArray []ValNode
	for i, v := range chessMap {
		for j, v2 := range v {
			if v2 != 0 {
				// 创建一个Valnode值结点
				valnode := ValNode{
					row: i,
					col: j,
					val: v2,
				}
				sparseArray = append(sparseArray, valnode)
			}
		}
	}
	//  输出稀疏数组
	fmt.Println("当前稀疏数组是：")
	for i, valnode := range sparseArray {
		fmt.Printf("%d: %d %d %d\n", i, valnode.row, valnode.col, valnode.val)
	}

	// 恢复稀疏数组为原始数组
	// 先创建一个原始数组
	var chessMap2 [11][11]int
	for i := 0; i < 11; i++ {
		for j := 0; j < 11; j++ {
			chessMap2[i][j] = 0
		}
	}
	// 遍历稀疏数组,将值赋
	for _, valnode := range sparseArray {
		chessMap2[valnode.row][valnode.col] = valnode.val
	}

	for _, v := range chessMap2 {
		for _, v2 := range v {
			fmt.Printf("%d\t", v2)
		}
		fmt.Println("")
	}
}

输出：
0       0       0       0       0       0       0       0       0       0       0
0       0       1       0       0       0       0       0       0       0       0
0       0       0       2       0       0       0       0       0       0       0
0       0       0       0       0       0       0       0       0       0       0
0       0       0       0       0       0       0       0       0       0       0
0       0       0       0       0       0       0       0       0       0       0
0       0       0       0       0       0       0       0       0       0       0
0       0       0       0       0       0       0       0       0       0       0
0       0       0       0       0       0       0       0       0       0       0
0       0       0       0       0       0       0       0       0       0       0
0       0       0       0       0       0       0       0       0       0       0
当前稀疏数组是：
0: 1 2 1
1: 2 3 2
0       0       0       0       0       0       0       0       0       0       0
0       0       1       0       0       0       0       0       0       0       0
0       0       0       2       0       0       0       0       0       0       0
0       0       0       0       0       0       0       0       0       0       0
0       0       0       0       0       0       0       0       0       0       0
0       0       0       0       0       0       0       0       0       0       0
0       0       0       0       0       0       0       0       0       0       0
0       0       0       0       0       0       0       0       0       0       0
0       0       0       0       0       0       0       0       0       0       0
0       0       0       0       0       0       0       0       0       0       0
0       0       0       0       0       0       0       0       0       0       0
```





## 31. Gin

- ### IRoutes接口

核心接口 **`IRoutes`**：提供的是注册路由的抽象。它的实现类 Engine 类似于 **`ControllerRegister`**。

Use 方法提供了用户接入自定义逻辑的能力，这个一般情况下也被看做是插件机制。

还额外提供了静态文件的接口。

Gin 没有 Controller 的抽象。所以在这方面我和 Gin的倾向比较一致，即 MVC 应该是用户组织 Web 项目的模式，而不是我们中间件设计者要考虑的。

```go
type IRoutes interface {
	Use(...HandlerFunc) IRoutes

	Handle(string, string, ...HandlerFunc) IRoutes
	Any(string, ...HandlerFunc) IRoutes
	GET(string, ...HandlerFunc) IRoutes
	POST(string, ...HandlerFunc) IRoutes
	DELETE(string, ...HandlerFunc) IRoutes
	PATCH(string, ...HandlerFunc) IRoutes
	PUT(string, ...HandlerFunc) IRoutes
	OPTIONS(string, ...HandlerFunc) IRoutes
	HEAD(string, ...HandlerFunc) IRoutes

	StaticFile(string, string) IRoutes
	StaticFileFS(string, string, http.FileSystem) IRoutes
	Static(string, string) IRoutes
	StaticFS(string, http.FileSystem) IRoutes
}
```

- ### Engine实现

  Engine 可以看做是 Beego 中 HttpServer 和ControllerRegister 的合体。

  - 实现了路由树功能，提供了注册和匹配路由的功能

  - 它本身可以作为一个 Handler 传递到 http 包，用于启动服务器

  Engine 的路由树功能本质上是依赖于 methodTree 的。

  

- ### methodTrees和methodTree

  methodTree才是真实的路由树

  Gin定义了methodTrees，**他实际上代表的是森林**，即每一个HTTP方法都对应到一棵树

  ```go
  type methodTree struct {
  	method string
  	root   *node
  }
  
  type methodTrees []methodTree
  
  func (trees methodTrees) get(method string) *node {
  	for _, tree := range trees {
  		if tree.method == method {
  			return tree.root
  		}
  	}
  	return nil
  }
  
  ```

- ### Context抽象

  Context也是代表了执行的上下文，提供了丰富的API：

  - **处理请求的API：**代表的是以Get和Bind为前缀的方法
  - **处理响应的API：**例如返回JSON或者XML响应的方法
  - **渲染页面：**如HTML方法

- ### 你好,GIN!

  **示例**

  ```go
  package main
  
  import (
  	"github.com/gin-gonic/gin"
  	"log"
  )
  
  func main() {
  	r := gin.Default()
  	r.GET("/", func(c *gin.Context) {
  		c.Writer.Write([]byte("你好,Gin!"))
  	})
  	err := r.Run(":8080")
  	if err != nil {
  		log.Println("運行錯誤", err)
  	}
  }
  ```

### Gin与HTTP基本操作-GET

可以非常简便的使用`JSON`格式数据

```go
package main

import (
	"Learning-JobAccess-Camp/pkg/apis"
	"github.com/gin-gonic/gin"
)

func main() {
	r := gin.Default()
	r.GET("/", func(c *gin.Context) {
		c.Writer.Write([]byte("This is index page from Gin!Welcome"))
	})// 如果用JSON 就可以返回JSON格式，并自带content-type: application/json
	r.GET("/history", func(c *gin.Context) {
		c.JSON(200, []apis.PersonalInformation{
			{
				Name:   "Qty",
				Sex:    "男",
				Tall:   1.81,
				Weight: 81.0,
				Age:    24,
			},
			{
				Name:   "Monica",
				Sex:    "女",
				Tall:   1.65,
				Weight: 47.0,
				Age:    22,
			},
		})
	})
	err := r.Run(":8081")
	if err != nil {
		// todo handle err
	}
}
```



### Gin与HTTP基本操作-POST

```go
package main

import (
	"Learning-JobAccess-Camp/pkg/apis"
	"github.com/gin-gonic/gin"
)

func main() {
	r := gin.Default()
	// 一般来说使用POST来进行创建
	r.POST("/register", func(c *gin.Context) {
		pi := &apis.PersonalInformation{}
		err := c.BindJSON(pi)
		if err != nil {
			//H is a shortcut for map[string]interface{}
			c.JSON(400, gin.H{
				"message": "无法读取个人注册信息",
			})
			return
		}
		//todo register to rank
		c.JSON(200, nil)
	})
	err := r.Run(":8081")
	if err != nil {
		//todo handle err
	}
}

```

- #### 使用POSTMAN进行GET操作：

  - ##### `.Query`

    ```go
    r.GET("/getWithQuery", func(c *gin.Context) {
    		name := c.Query("name")
    		c.JSON(200, gin.H{
    			"payload": base64.StdEncoding.EncodeToString([]byte(name)),
    		})
    	})
    ```

    ```
    GET --> http://localhost:8081/getWithQuery?name=Hud
    
    {
        "payload": "SHVk"
    }
    ```

  - #### `.Param`

    ```go
    r.GET("/getWithParam/:name", func(c *gin.Context) {
    		name := c.Param("name")
    		c.JSON(200, gin.H{
    			"payload": base64.StdEncoding.EncodeToString([]byte(name)),
    		})
    	})
    ```

    ```
    GET --> http://localhost:8081/getWithParam/Hud
    
    {
        "payload": "SHVk"
    }
    ```

**对于同一个URL，例如我精确定义了`localhost:8081/getWithParam/Hud`這个地址，但是我在对`/getWithParam/:name`时使用`Hud`这个参数，那么还是根据精确度的优先级优先访问前者。**



### 调试GIN

[**源代码**](https://github.com/gin-contrib/pprof)

**包`pprof`通过其HTTP服务器运行时分析数据以`pprof`可视化工具预期的格式提供服务。**

```go
package main

import (
	"github.com/gin-contrib/pprof"
	"github.com/gin-gonic/gin"
)

func main() {
  router := gin.Default()
  pprof.Register(router)
  router.Run(":8080")
}
```

打开浏览器，访问http://localhost:8080/debug/pprof

可以展示当前服务器的一些状态

go用来看当前服务器服务状态：

**`go tool pprof --help`**

```bash

C:\Users\Hud>go tool pprof --help
usage:

Produce output in the specified format.

   pprof <format> [options] [binary] <source> ...

Omit the format to get an interactive shell whose commands can be used
to generate various views of a profile

   pprof [options] [binary] <source> ...

Omit the format and provide the "-http" flag to get an interactive web
interface at the specified host:port that can be used to navigate through
various views of a profile.

   pprof -http [host]:[port] [options] [binary] <source> ...

Details:
  Output formats (select at most one):
    -callgrind       Outputs a graph in callgrind format
    -comments        Output all profile comments
    -disasm          Output assembly listings annotated with samples
    -dot             Outputs a graph in DOT format
    -eog             Visualize graph through eog
    -evince          Visualize graph through evince
    -gif             Outputs a graph image in GIF format
    -gv              Visualize graph through gv
    -kcachegrind     Visualize report in KCachegrind
    -list            Output annotated source for functions matching regexp
    -pdf             Outputs a graph in PDF format
    -peek            Output callers/callees of functions matching regexp
    -png             Outputs a graph image in PNG format
    -proto           Outputs the profile in compressed protobuf format
    -ps              Outputs a graph in PS format
    -raw             Outputs a text representation of the raw profile
    -svg             Outputs a graph in SVG format
    -tags            Outputs all tags in the profile
    -text            Outputs top entries in text form
    -top             Outputs top entries in text form
    -topproto        Outputs top entries in compressed protobuf format
    -traces          Outputs all profile samples in text form
    -tree            Outputs a text rendering of call graph
    -web             Visualize graph through web browser
    -weblist         Display annotated source in a web browser

  Options:
    -call_tree       Create a context-sensitive call tree
    -compact_labels  Show minimal headers
    -divide_by       Ratio to divide all samples before visualization
    -drop_negative   Ignore negative differences
    -edgefraction    Hide edges below <f>*total
    -focus           Restricts to samples going through a node matching regexp
    -hide            Skips nodes matching regexp
    -ignore          Skips paths going through any nodes matching regexp
    -intel_syntax    Show assembly in Intel syntax
    -mean            Average sample value over first value (count)
    -nodecount       Max number of nodes to show
    -nodefraction    Hide nodes below <f>*total
    -noinlines       Ignore inlines.
    -normalize       Scales profile based on the base profile.
    -output          Output filename for file-based outputs
    -prune_from      Drops any functions below the matched frame.
    -relative_percentages Show percentages relative to focused subgraph
    -sample_index    Sample value to report (0-based index or name)
    -show            Only show nodes matching regexp
    -show_from       Drops functions above the highest matched frame.
    -source_path     Search path for source files
    -tagfocus        Restricts to samples with tags in range or matched by regexp
    -taghide         Skip tags matching this regexp
    -tagignore       Discard samples with tags in range or matched by regexp
    -tagleaf         Adds pseudo stack frames for labels key/value pairs at the callstack leaf.
    -tagroot         Adds pseudo stack frames for labels key/value pairs at the callstack root.
    -tagshow         Only consider tags matching this regexp
    -trim            Honor nodefraction/edgefraction/nodecount defaults
    -trim_path       Path to trim from source paths before search
    -unit            Measurement units to display

  Option groups (only set one per group):
    granularity
      -functions       Aggregate at the function level.
      -filefunctions   Aggregate at the function level.
      -files           Aggregate at the file level.
      -lines           Aggregate at the source code line level.
      -addresses       Aggregate at the address level.
    sort
      -cum             Sort entries based on cumulative weight
      -flat            Sort entries based on own weight

  Source options:
    -seconds              Duration for time-based profile collection
    -timeout              Timeout in seconds for profile collection
    -buildid              Override build id for main binary
    -add_comment          Free-form annotation to add to the profile
                          Displayed on some reports or with pprof -comments
    -diff_base source     Source of base profile for comparison
    -base source          Source of base profile for profile subtraction
    profile.pb.gz         Profile in compressed protobuf format
    legacy_profile        Profile in legacy pprof format
    http://host/profile   URL for profile handler to retrieve
    -symbolize=           Controls source of symbol information
      none                  Do not attempt symbolization
      local                 Examine only local binaries
      fastlocal             Only get function names from local binaries
      remote                Do not examine local binaries
      force                 Force re-symbolization
    Binary                  Local path or build id of binary for symbolization
    -tls_cert             TLS client certificate file for fetching profile and symbols
    -tls_key              TLS private key file for fetching profile and symbols
    -tls_ca               TLS CA certs file for fetching profile and symbols

  Misc options:
   -http              Provide web interface at host:port.
                      Host is optional and 'localhost' by default.
                      Port is optional and a randomly available port by default.
   -no_browser        Skip opening a browser for the interactive web UI.
   -tools             Search path for object tools

  Legacy convenience options:
   -inuse_space           Same as -sample_index=inuse_space
   -inuse_objects         Same as -sample_index=inuse_objects
   -alloc_space           Same as -sample_index=alloc_space
   -alloc_objects         Same as -sample_index=alloc_objects
   -total_delay           Same as -sample_index=delay
   -contentions           Same as -sample_index=contentions
   -mean_delay            Same as -mean -sample_index=delay

  Environment Variables:
   PPROF_TMPDIR       Location for saved profiles (default $HOME/pprof)
   PPROF_TOOLS        Search path for object-level tools
   PPROF_BINARY_PATH  Search path for local binary files
                      default: $HOME/pprof/binaries
                      searches $name, $path, $buildid/$name, $path/$buildid
   * On Windows, %USERPROFILE% is used instead of $HOME
  
```



## 32. Web框架概览

### `Beego` —— Controller抽象

**Beego** 是基于 MVC (Model-View-Controller）的，所以它定义了一个核心接口 ControllerInterface。ControllerInterface 定义了一个控制器必须要解决什么问题。同时 ContollerInterface 的默认实现 Controller 提供了实现自定义控制器的各种辅助方法，所以在 Beego 里面，一般都是组合 Controller 来实现自己的 Controller.

```go
package beego

import "github.com/beego/beego/v2/server/web"

type UserController struct {
	web.Controller
}

func (c *UserController) GetUser() {
	c.Ctx.WriteString("This is hello from Hud!!")
}
```

```go
package beego

import (
	"github.com/beego/beego/v2/server/web"
	"testing"
)

func TestUserController(t *testing.T) {
	web.BConfig.CopyRequestBody = true
	c := &UserController{}
	web.Router("/user", c, "get:GetUser")
	// 监听 8081 端口
	web.Run(":8081")
}

```

虽然用户被要求组合Controller，但是路由注册和服务器启动是通过另外一套机制来完成的。

- ### HttpServer和ControllerRegister

  ControllerInterface 可以看做核心接口，因为它直接体现了 **Beego** 的设计初衷：MVC 模式。同时它也是用户核心接入点。

  但是如果从功能特性上来说，**HttpServer** 和**ControllerRegister** 才是核心。

  -  **HttpServer**：代表一个”服务器” ，大多数时候它就是一个进程。

  -  **ControllerRegister**：真正干活的人。**注册路由，路由匹配和执行业务代码**都是透过它来完成的。

大多数情况下，HttpServer就是一个天然的隔离机制

```go
// HttpServer defines beego application with a new PatternServeMux.
type HttpServer struct {
	Handlers           *ControllerRegister
	Server             *http.Server
	Cfg                *Config
	LifeCycleCallbacks []LifeCycleCallback
}

// ControllerRegister containers registered router rules, controller handlers and filters.
type ControllerRegister struct {
	routers      map[string]*Tree
	enablePolicy bool
	enableFilter bool
	policies     map[string]*Tree
	filters      [FinishRouter + 1][]*FilterRouter
	pool         sync.Pool

	// the filter created by FilterChain
	chainRoot *FilterRouter

	// keep registered chain and build it when serve http
	filterChains []filterChainConfig

	cfg *Config
}
```

- ### Context抽象

  用户操作请求和响应是通过 Ctx 来达成的。它代表的是整个请求执行过程的上下文。

  进一步，**Beego** 将 Context 细分了几个部分：

  - **Input**：定义了很多和处理请求有关的方法

  - **Output**：定义了很多和响应有关的方法

  - **Response**：对 `http.ResponseWriter` 的二次封装

  ```go
  type Context struct {
  	Input          *BeegoInput
  	Output         *BeegoOutput
  	Request        *http.Request
  	ResponseWriter *Response
  	_xsrfToken     string
  }
  ```

**`ControllerRegister`** 最为基础，它解决了路由注册和路由匹配这个基础问题。

**`Context`** 和 **`Controller`** 为用户提供了丰富 API，用于辅助构建系统。

**`HttpServer`** 作为服务器抽象，用于管理应用生命周期和资源隔离单位。



### Iris ——Application

https://github.com/kataras/iris

Application 是 Iris 的核心抽象，它代表的是”应用” 。实际上这个语义更加接近 Beego 的 HttpServer 和 Gin的 Engine。

它提供了：

- 生命周期控制功能，如 Shutdown 等方法

-  注册路由的 API

个人认为 Application 这个名字不是很合适，比如说有些应用会监听多个端口。不同的端口提供不同的功能，也就是常说的多 Server 应用。相比之下，HttpServer 或者 Engine会更合适一点。

```go
package iris

import (
	"github.com/kataras/iris/v12"
	"testing"
)

func TestHelloWorld(t *testing.T) {
	app := iris.New()

	app.Get("/", func(ctx iris.Context) {
		_, _ = ctx.HTML("Hello <strong>%s</strong>!", "World")
	})

	_ = app.Listen(":8083")
}

```

- ### 路由相关

  Iris 的设计非常复杂。在 Beego 和 Gin 里面能够明显看到路由树的痕迹，但是在 Iris 里面就很难看出来。

  和处理路由相关的三个抽象：

  - **Route**：直接代表了已经注册的路由。在 Beego 和 Gin里面，对应的是路由树的节点

  - **APIBuilder**：创建 Route 的 Builder 模式，Party 也是它创建的

  - **repository**：存储了所有的 Routes，有点接近 Gin 的methodTrees 的概念

 

### Echo —— Echo

Echo 是它内部的一个结构体，类似于 Beego 的 HttpServer和 Gin 的 Engine：

-  暴露了注册路由的方法，但是它并不是路由树的载体

-  生命周期管理：如 Shutdown 和 Start 等方法

在 Echo 里面有两个相似的字段：

- **router**：这其实就是代表路由树

- **routers**：这代表的是根据 Host 来进行分组组织，可以看做是近似于 namespace 之类的概念，既是一种组织方式，也是一种隔离机制



### Web核心



在框架对比的时候，我们注意到对于一个Web框架来说，至少要提供三个抽象：

- 代表服务器的抽象，这里我们称之为Server
- 代表上下文的抽象，这里我们称之为Context
- **路由树**



- ### Server

  从前面框架对比来看，对于一个web框架来说，我们首先要有一个整体代表服务器的抽象，也就是Server

  Server 从特性上来说，至少要提供三部分功能：

  - **生命周期控制**：即启动、关闭。如果在后期，我们还要考虑增加生命周期回调特性

  - **路由注册接口**：提供路由注册功能

  - **作为 http 包到 Web 框架的桥梁**

  **http 包暴露了一个接口，Handler。它是我们引入自定义 Web 框架相关的连接点。**

  

  - #### *Server 定义版本一：只组合 http.Handler*

    **优点：**

    - 用户在使用的时候只需要调用 http.ListenAndServe 就可以和 HTTPS 协议完全无缝衔接

    - 极简设计

    **缺点：**

    - 难以控制生命周期，并且在控制生命周期的时候增加回调支持

    - 缺乏控制力：如果将来希望支持优雅退出的功能，将难以支持
  
    
  
  - #### *Server 定义版本二：组合 http.Handler 并且增加 Start 方法*
  
    **优点**：
  
    - Server 既可以当成普通的 http.Handler 来使用，又可以作为一个独立的实体，拥有自己的管理生命周期的能力
  
    - 完全的控制，可以为所欲为
  
    **缺点：**
  
    - 如果用户不希望使用 ListenAndServeTLS，那么 Server 需要提供 HTTPS 的支持 
  
    
    **注意：Start 方法可以不需要 addr 参数，那么在创建实现类的时候传入地址就可以。**
    
    版本一和版本二都直接耦合了 Go 自带的 http 包，如果我们希望切换为 fasthttp 或者类似的 http 包，则会非常困难。
    
    ```go
    type Server interface {
    	http.Handler
    	Start(addr string) error
    }
    
    func TestServer(t *testing.T) {
    	var h Server // NewServer
    
    	// 方法一：用户完全委托给http包
    	err := http.ListenAndServe(":8080", h)
    	if err != nil {
    		// todo handle error
    	}
    	http.ListenAndServeTLS(":443", "", "", h)
    
    	// 方法二：用户自己手动管理
    	h.Start("8081")
    }
    
    ```
- ### Server——HTTPServer实现

  该实现直接使用 http.ListenAndServe 来启动，后续可以根据需要替换为：

  - 内部创建 http.Server 来启动

  - 使用 http.Server 来启动，换取更大的灵活性，如将端口监听和服务器启动分离等

  **ServerHTTP** 则是我们整个 Web 框架的核心入口。我们将在整个方法内部完成：

  - **Context 构建**

  - **路由匹配**

  - **执行业务逻辑**

  ```go
  // 确保HTTPServer肯定实现了Server接口
  var _ Server = &HTTPServer{}
  
  type HTTPServer struct{}
  
  // ServeHTTP HTTPServer 处理请求的入口
  func (s *HTTPServer) ServeHTTP(writer http.ResponseWriter,request){
      // 框架代码就在这里
    	// Context 构建
      // 路由匹配
      // 执行业务逻辑
  }
  
  func (s *HTTPServer) Start(addr string) error{
     return http.ListenAndServe(addr,s)
  }
  ```
  
  
  - ### **思考点**
  
    - AddRoute 方法只接收一个 HandleFunc。因为我希望它只注册业务逻辑。即便真有多个的场景，用户可以自己组合成一个。
  
    - 如果允许注册多个，那么在实现的时候就要考虑，其中一个失败了，是否还允许继续执行下去；反过来，如果其中一个 HandleFunc 要中断
  
      执行，怎么中断。
  
    - 这里我采用了新的名字 AddRoute，我认为这更加贴近这个方法本意。
  
    - Handle：看上去像是处理什么东西，而实质上我们这里只是注册路由，所以用 AddRoute 会更加合适
  



#### 路由树

- #### **我们分成以下步骤来实现一颗路由树：**

  - 全静态匹配

  - 支持通配符匹配
  - 支持参数路由


------



- ### **Beego的实现**

  Beego的核心结构体是三个：

  - **ControllerRegister**：类似于容器，放着所有的路由树
    - 路由树是按照 HTTP method 来组织的，例如 GET 方法会对应有一棵路由树
  - **Tree**：它代表的就是路由树，在 Beego 里面，一棵路由树被看做是由子树组成的
  - **leafInfo**：代表叶子节点

  ```go
  type ControllerRegister struct {
  	routers      map[string]*Tree
  	enablePolicy bool
  	enableFilter bool
  }
  
  type Tree struct {
  	// prefix set for static router
  	prefix string
  	// search fix route first
  	fixrouters []*Tree
  	// if set, failure to match fixrouters search then search wildcard
  	wildcard *Tree
  	// if set, failure to match wildcard search
  	leaves []*leafInfo
  }
  
  type leafInfo struct {
  	// names of wildcards that lead to this leaf. eg, ["id" "name"] for the wildcard ":id" and ":name"
  	wildcards []string
  
  	// if the leaf is regexp 正则表达式
    
  	regexps *regexp.Regexp
  
  	runObject interface{}
  }
  ```

  Beego的数定义，并没有采用Children式的定义，**而是采用递归式的定义，即一棵树是由根节点+叶子节点构成的**



- ### Gin的实现

  Gin的关键结构体更加直观：

  - **methodTrees**：也就是路由树也是按照 HTTP方法组织的，例如 GET 会有一棵路由树

  - **methodTree**：定义了单棵树。树在 Gin 里面采用的是 children 的定义方式，即树由节点构成（注意对比 Beego）

  - **node**：代表树上的一个节点，里面维持住了children，即子节点。同时有 nodeType 和wildChild 来标记一些特殊节点

    ```go
    tyep methodTree struct{
    	method string
    	root *node
    }
    
    type methodTrees []methodTree 
    
    type node struct{
    	path 		string 
    	indices 	string
        wildChild 	bool
        nType		nodeType
        priority 	uint32
        children 	[]*node
        handlers	HandlersChain
        fullPath	string
    }
    ```

  **Gin是利用路由的公共前缀来构造路由树（前缀树）**

  

- ### Echo的实现

  Echo 的实现稍微有点复杂，并且概念之间不是很清晰：

  - 在 Echo 结构体里面维护了 routers，但是 routers 并不是按照 HTTP 方法组织的，而是按照所谓的 Host 来组织的，Host 可以看做一个命名空间

  - Router：代表路由注册中心，里面维护了路由树

  - Route：代表具体的路由

  - node：则是中规中矩的树节点设计，它内部依旧采用类型的数据

#### 

- ### 路由树——设计总结

  **归根结底就是设计一颗多叉树。**

  - 同时我们**按照 HTTP 方法来**组织路由树，每个HTTP 方法一棵树

  - 节点维持住自己的**子节点**

  - 这两种形态的路由树组织，性能差异不大（最长公共前缀）

  

- ### 路由树 —— 全静态匹配

  我们利用全静态匹配来构建路由树，后面再考虑重构路由树以支持通配符匹配、参数路由等复杂匹配。

  所谓的静态匹配，就是**路径的每一段都必须严格相等**。

  

  - #### 全静态匹配——接口设计

    **关键类型：**

    - **router**：维持住了所有的路由树，它是整个路由注册和查找的总入口。router 里面维护了一个 map，是按照 HTTP 方法来组织路由树的

    - **node**：代表的是节点。它里面有一个 children 的map 结构，使用 map 结构是为了快速查找到子节点

      ```go
      type router struct {
      	// Beego Gin HTTP Method 对应一棵树
      	// GET有一棵树，POST也有一棵树
      
      	// http method => 路由树根节点
      	trees map[string]*node
      }
      
      func newRouter() *router {
      	return &router{
      		trees: map[string]*node{},
      	}
      }
      
      type node struct {
      	path string
      	// path 到子节点的映射
      	children map[string]*node
      	// 缺一个代表用户注册的业务逻辑
      	handler HandleFunc
      }
      ```

  

- ### 路由树——TDD起步

  在有了类型定义之后，我们就可以考虑按照TDD的思路，用测试来驱动我们的实现

  简化版本的TDD：

  - 定义 API
  - 定义测试
  - 添加测试用例
  - 实现，并且确保实现能够通过测试用例
  - 重复 3-4 直到考虑了所有的场景
  - 重复步骤 1-5

  

- ### 路由树——通配符匹配

  所谓通配符匹配，**是指用 * 号来表达匹配任何路径**。要考虑几个问题：

  - 如果路径是 /a/b/c 能不能命中 /a/* 路由？

  - 如果注册了两个路由 /user/123/home 和 /user/*/* 。那么输入路径`/user/123/detail` 能不能命中 `/user/*/*`?

  **这两个都是理论上可以，但是不应该命中**。

  - 从实现的角度来说，其实并不难。

  - 从用户的角度来说，他们不应该设计这种路由。给用户自由，但是也要限制不良实践。

  - 后者要求的是一种可回溯的路由匹配，即发现 /user/123/home 匹配不上之后要回溯回去 /user/* 进一步查找，典型的投入大产出低的特性。

  

  ```go
  // node 代表树的节点
  // 路由树的匹配顺序是：
  // 1. 静态完全匹配 
  // 2. 通配符匹配
  // 这是不回溯匹配
  type node struct(){
  	path string
      // children 子节点
      // 子节点的path=>node
      children map[string]*node
      // handler 命中路由之后执行的逻辑
      handler HandleFunc
      
      // 通配符*表达的节点，任意匹配
      starChild *node
  }
  ```
  
  
  
- ### 路由树——参数路径

  所谓参数路径，就是指在路径中带上参数，同时这些参数对应的值可以被业务取出来使用。

  例如：**`/user/:id`** ，如果输入路径 /user/123，那么会命中这个路由，并且 id = 123。

  那么要考虑：

  **允不允许同样的参数路径和通配符匹配一起注册？**例如同时注册 /user/* 和 /user/:id

  可以，但是没必要，用户也不应该设计这种路由

  新增`paramChild`字段

  ```go
  type node struct {
  	path string
  	// children 子节点
  	// 子节点的 path => node
  	children map[string]*node
  	// handler 命中路由之后执行的逻辑
  	handler HandleFunc
  
  	// 加一个路径参数
  	paramChild *node
  	// 通配符 * 表达的节点，任意匹配
  	starChild *node
  }
  ```

  ```go
  func (n *node) equal(y *node) (string, bool) {
  	if y == nil {
  		return "目标节点为 nil", false
  	}
  	if n.path != y.path {
  		return fmt.Sprintf("%s 节点 path 不相等 x %s, y %s", n.path, n.path, y.path), false
  	}
  	
  	if n.paramChild !=nil{
  		msg, ok := n.paramChild.equal(y.paramChild)
  		if !ok{
  			return msg , ok
  		}
  	}
  	
  ```

  ```go
  func (n *node) childOf(path string) (*node, bool) {
  	if n.children == nil {
  		if n.paramChild != nil {
  			return n.paramChild, true
  		}
  		return n.starChild, n.starChild != nil
  	}
  	res, ok := n.children[path]
  	if !ok {
  		if n.paramChild != nil {
  			return n.paramChild, true
  		}
  		return n.starChild, n.starChild != nil
  	}
  	return res, ok
  }
  ```



#### AOP方案

**AOP (Aspect Oriented Programming)，面向切面编程。核心在于将横向关注点从业务中剥离出来。**

横向关注点：**就是那些跟业务没啥关系，但是每个业务又必须要处理的。常见的有几类：**

- 可观测性：logging、metric 和 tracing

- 安全相关：登录、鉴权与权限控制

- 错误处理：例如错误页面支持

- 可用性保证：熔断限流和降级等

基本上 Web 框架都会设计自己的 AOP 方案



#### 不同Web框架的AOP方案



**Beego** 早期的时候设计完善的回调机制，大体上有三类：

- **Middleware：它的缺陷是基本脱离了 Beego 的控制。**

  Beego 的 HTTPServer 本身就是一个 Handler，用户自己再

  开发一个 http.Handler，然后将两者结合在一起，这样用户

  的 http.Handler 就没法利用 Beego 内部的数据了。

- **Filter：Beego 允许用户注册不同时机运行的 Filter。**

  这些Filter 都是单向的，而不是环绕式的。

- **FilterChain：FilterChain 可以看做是可以利用 Beego 内部数据的 Middleware。**

  它将 Filter 组织成链，每一个 Filter都要考虑调用下一个 Filter，否则就会中断执行。但同时，这些 Filter 也失去了指定时机运行的能力。



**Gin 设计**

- Gin 的设计稍微不一样。在 Beego 里面，FilterChain 是通过 next 来从一个 Filter 执行到另外一个 Filter。相当于每个 Filter 自由决定要不要调用下一个 Filter。

- Gin 用的是半集中式设计，由 Context 来调度。但也是实现者在 HandlerFunc 里面主动调用下一个。完全的集中式，是由一个中央管理器之类的统一调度各种

- Filter 或者 Handler，在中间件设计里面不常用。

  ```go
  func (c *Context) Next() {
  	c.index++
  	for c.index < int8(len(c.handlers)) {
  		c.handlers[c.index](c)
  		c.index++
  	}
  }
  ```

  ```go
  // HandlerFunc defines the handler used by gin middleware as return value.
  type HandlerFunc func(*Context)
  
  // HandlersChain defines a HandlerFunc slice.
  type HandlersChain []HandlerFunc
  ```



#### Middleware

这里我们也叫 Middleware 好了，它的定义也是接收一个 `HandleFunc` 作为输入，返回一个 `HandleFunc`。

Middleware 的提供者要决定何时调用 next。它既是一个责任链模式，也是一个洋葱模式，后面你们可以看到我在中间件设计里会大量使用这个模式。

```go
func TestHTTPServer_ServeHTTP(t *testing.T) {
	server := NewHTTPServer()
	server.mdl = []Middleware{
		func(next HandleFunc) HandleFunc {
			return func(ctx *Context) {
				fmt.Println("第一个 before")
				next(ctx)
				fmt.Println("第一个 after")
			}
		},
		func(next HandleFunc) HandleFunc {
			return func(ctx *Context) {
				fmt.Println("第二个 before")
				next(ctx)
				fmt.Println("第二个 after")
			}
		},
		func(next HandleFunc) HandleFunc {
			return func(ctx *Context) {
				fmt.Println("第三个 中断")
			}
		},
		func(next HandleFunc) HandleFunc {
			return func(ctx *Context) {
				fmt.Println("第四个(You can't see it)")

			}
		},
	}
	server.ServeHTTP(nil, &http.Request{})
}
```

正常执行，最终会到用户业务逻辑里面。某个 HandleFunc 没有调用 next，那么执行流程就被打断了。

- ### Tracing

  ​		**Tracing**：踪迹，它记录从收到请求到返回响应的整个过程。在分布式环境下，一般代表着请求从Web 收到，沿着后续微服务链条传递，得到响应再返回到前端的过程。

  需要注意的是，trace 不仅仅包含服务调用信息，实际上整条链路上的信息都可能包含在内，包括：

  - RPC 调用

  - HTTP 调用

  - 数据库查询

  - 发送消息

  - 业务步骤

  这些步骤，也可以进一步被细分，分成更加细的span。

  Tracing相关的几个概念：

  - **tracer**：表示用来记录 trace（踪迹）的实例，一般来说，tracer 会有一个对应的接口。

  - **span**：代表 trace 中的一段。因此 trace 本身也可以看做是一个 span。span 本身是一个层级概念，因此有父子关系。一个 trace 的 span可以看做是多叉树。

  

  - #### **OpenTelemetry** 

    OpenTelemetry是 OpenTracing 和 OpenCensus合并而来。

    OpenTelemetry 同时支持了 logging、tracing 和metrics

    OpenTelemetry 提供了各种语言的 SDK

    OpenTelemetry 适配了各种开源框架，如Zipkin、Jeager、Prometheus新时代的可观测性平台。

    

  - #### OpenTelemetry GO SDK 入门

    **TracerProvider**：用于构造 tracer 实例。Provider在平时开发中也很常见，有时可以看作是轻量级的工厂模式。

    **tracer**：追踪者，也就是用于构造 trace 的东西。构造 tracer 需要一个 instrumentationName，一般来说就是你构造 tracer 的地方的包名（主要保证唯一就好）。

    **span**：调用 tracer 上的 Start 方法。如果传入的context 里面已经有一个 span 了，那么新创建的span 就是老的 span 的儿子。span 要记住调用End。

    






## 33. 分布式

#### 分布式概念

所有的服务部署在同一台机器上，称为**单点部署**，单点部署的优缺点：

- **优点**

  - 部署简单
  - 容易维护

- **缺点**

  - 单点故障
  - 吞吐量受限

  为了满足企业对服务的质量要求，通常会将应用模块进行划分，并将每个模块的各个组件部署在多台服务器上，以满足当单台服务器或多台服务器出故障或维护时，不中断全部服务或大多数服务不受影响。这种服务部署的方式即为分布式部署。



#### 分布式的优缺点

- **优点**
  - 稳定可靠
  - 容量大
- **缺点**
  - 系统复杂
  - 维护成本高



#### 应用与分布式

根据应用有无状态，将应用分为：无状态应用、有状态应用

- **无状态应用**

  应用的每个实体提供完全一致的功能， 每次服务的内容为一次性服务或者任何一个实体均可以在任何时间互相替换。

  - 网页前段服务
  - 后端计算服务
  - 代理服务
  - 等等（只要是计算的、不存数据的、只提供资源的都可以是无状态的应用）

- **有状态应用**

  应用的每个实例因数据内容的差异而提供不同类型、功能的服务，或者在服务中扮演了特定的角色。在服务时，他不可替代或者需要特定的操作后才可替代

  - 数据库服务
  - 存储服务
  - 文件服务器
  - 等等



#### ETCD

**认识`etcd`**

- ## 1.1 `etcd` 概念

从哪里说起呢？官网第一个页面，有那么一句话：

```text
"A distributed, reliable key-value store for the most critical data of a distributed system"
```

即 `etcd` 是一个**分布式**、**可靠 key-value** 存储的**分布式系统**。当然，它不仅仅用于存储，还提供共享配置及服务发现。

- ## 1.2 `etcd` vs `Zookeeper`

  提供配置共享和服务发现的系统比较多，其中最为大家熟知的是 Zookeeper，而 etcd 可以算得上是后起之秀了。在项目实现、一致性协议易理解性、运维、安全等多个维度上，etcd 相比 zookeeper 都占据优势。

  本文选取 Zookeeper 作为典型代表与 etcd 进行比较，而不考虑 Consul 项目作为比较对象，原因为 Consul 的可靠性和稳定性还需要时间来验证（项目发起方自身服务并未使用Consul，自己都不用)。

  - 一致性协议： etcd 使用 Raft 协议，Zookeeper 使用 ZAB（类PAXOS协议），前者容易理解，方便工程实现；
  - 运维方面：etcd 方便运维，Zookeeper 难以运维；
  - 数据存储：etcd 多版本并发控制（MVCC）数据模型 ， 支持查询先前版本的键值对
  - 项目活跃度：etcd 社区与开发活跃，Zookeeper 感觉已经快死了；
  - API：etcd 提供 HTTP+JSON, gRPC 接口，跨平台跨语言，Zookeeper 需要使用其客户端；
  - 访问安全方面：`etcd` 支持 `HTTPS` 访问，`Zookeeper` 在这方面缺失；

​		...

- ## 1.3 `etcd` 应用场景

  etcd 比较多的应用场景是用于服务发现，服务发现 (Service Discovery) 要解决的是分布式系统中最常见的问题之一，**即在同一个分布式集群中的进程或服务如何才能找到对方并建立连接。**和 `Zookeeper` 类似，`etcd` 有很多使用场景，包括：

  - 配置管理
  - 服务注册发现
  - 选主
  - 应用调度
  - 分布式队列
  - 分布式锁

- ## 1.4 `etcd` 工作原理

  ### 1.4.1 如何保证一致性

  `etcd` 使用 **raft 协议**来维护集群内各个节点状态的一致性。简单说，`etcd` 集群是一个分布式系统，由多个节点相互通信构成整体对外服务，每个节点都存储了完整的数据，并且通过 Raft 协议保证每个节点维护的数据是一致的。

  每个 etcd 节点都维护了一个状态机，并且，任意时刻至多存在一个有效的主节点。主节点处理所有来自客户端写操作，通过 Raft 协议保证写操作对状态机的改动会可靠的同步到其他节点。

  ### 1.4.2 数据模型

  etcd 的设计目标是用来存放非频繁更新的数据，提供可靠的 Watch插件，它暴露了键值对的历史版本，以支持低成本的快照、监控历史事件。这些设计目标要求它使用一个持久化的、多版本的、支持并发的数据数据模型。

  当 etcd 键值对的新版本保存后，先前的版本依然存在。从效果上来说，键值对是不可变的，etcd 不会对其进行 in-place 的更新操作，而总是生成一个新的数据结构。为了防止历史版本无限增加，etcd 的存储支持压缩（Compact）以及删除老旧版本。

  - #### **逻辑视图**

  从逻辑角度看，etcd 的存储是一个扁平的二进制键空间，键空间有一个针对键（字节字符串）的词典序索引，因此范围查询的成本较低。

  键空间维护了多个修订版本（Revisions），每一个原子变动操作（一个事务可由多个子操作组成）都会产生一个新的修订版本。在集群的整个生命周期中，修订版都是单调递增的。修订版同样支持索引，因此基于修订版的范围扫描也是高效的。压缩操作需要指定一个修订版本号，小于它的修订版会被移除。

  一个键的一次生命周期（从创建到删除）叫做 “代 (Generation)”，每个键可以有多个代。创建一个键时会增加键的版本（version），如果在当前修订版中键不存在则版本设置为1。删除一个键会创建一个墓碑（Tombstone），将版本设置为0，结束当前代。每次对键的值进行修改都会增加其版本号 — 在同一代中版本号是单调递增的。

  当压缩时，任何在压缩修订版之前结束的代，都会被移除。值在修订版之前的修改记录（仅仅保留最后一个）都会被移除。

  - #### **物理视图**

    etcd 将数据存放在一个持久化的 B+ 树中，处于效率的考虑，每个修订版仅仅存储相对前一个修订版的数据状态变化（Delta）。单个修订版中可能包含了 B+ 树中的多个键。

    键值对的键，是三元组（major，sub，type）：

    - major：存储键值的修订版
    - sub：用于区分相同修订版中的不同键
    - type：用于特殊值的可选后缀，例如 t 表示值包含墓碑

    键值对的值，包含从上一个修订版的 Delta。B+ 树 —— 键的词法字节序排列，基于修订版的范围扫描速度快，可以方便的从一个修改版到另外一个的值变更情况查找。

    etcd 同时在内存中维护了一个 B 树索引，用于加速针对键的范围扫描。索引的键是物理存储的键面向用户的映射，索引的值则是指向 B+ 树修该点的指针。

    



#### GRPC

​	**Web编程的烦恼：**

- 要精确的设计URL，不然引起URL冲突，导致请求失败
- 要时刻考虑发送的内容、返回的内容，并做内容校验，否则无法保证成功
- 需要使用特定的网络客户端来发送请求，也要启动特定的服务端接收请求
- 如果想要连续获取服务端的变更，就需要不停地轮循检查变更

有没有一种方法，写功能的时候调用服务端的方法、接口像本地调用一样？

有没有一种方法，服务端可以主动把变更推送到客户端？同样客户端也可以连续一串操作让服务端确认？

- ##  简单介绍

在这一节的内容中，我将简单的跟你介绍一下`gRPC`这个东西。
`RPC`的全称是`Remote Procedure Call`，远程过程调用。**这是一种协议，是用来屏蔽分布式计算中的各种调用细节**，**使得你可以像是本地调用一样直接调用一个远程的函数。**
而`gRPC`又是什么呢？用官方的话来说：

> A high-performance, open-source universal RPC framework

**`gRPC`是一个高性能的、开源的通用的RPC框架。**

在`gRPC`中，我们称调用方为`client`，被调用方为`server`。
跟其他的`RPC`框架一样，`gRPC`也是基于”服务定义“的思想。简单的来讲，就是我们通过某种方式来描述一个服务，这种描述方式是语言无关的。在这个”服务定义“的过程中，我们描述了我们提供的服务服务名是什么，有哪些方法可以被调用，这些方法有什么样的入参，有什么样的回参。

也就是说，在定义好了这些服务、这些方法之后，`gRPC`会屏蔽底层的细节，`client`只需要直接调用定义好的方法，就能拿到预期的返回结果。对于`server`端来说，还需要实现我们定义的方法。同样的，`gRPC`也会帮我们屏蔽底层的细节，我们只需要实现所定义的方法的具体逻辑即可。

你可以发现，在上面的描述过程中，所谓的”服务定义“，就跟定义接口的语义是很接近的。我更愿意理解为这是一种”约定“，**双方约定好接口**，然后`server`**实现这个接口**，`client`**调用这个接口的代理对象**。至于其他的细节，交给`gRPC`。

此外，`gRPC`还是语言无关的。你可以用C++作为服务端，使用Golang、Java等作为客户端。为了实现这一点，我们在”定义服务“和在编码和解码的过程中，应该是做到**语言无关的**。

下面放一张官网上面的图：

![img](https://img2020.cnblogs.com/blog/1998080/202009/1998080-20200924161632078-309009747.jpg)

因此，`gRPC`使用了`Protocol Buffers`。

在这里我不会展开来讲`Protocol Buffers`这个东西，你可以把他当成一个代码生成工具以及序列化工具。这个工具可以把我们定义的方法，转换成特定语言的代码。比如你定义了一种类型的参数，他会帮你转换成`Golang`中的`struct 结构体`，你定义的方法，他会帮你转换成`func 函数`。此外，在发送请求和接受响应的时候，这个工具还会完成对应的编码和解码工作，将你即将发送的数据编码成`gRPC`能够传输的形式，又或者将即将接收到的数据解码为编程语言能够理解的数据格式。

对`gRPC`的简单介绍就到这里，下面的内容我们直接开始实践。

简单来说，GRPC是一个现代化的高性能的RPC框架，他可以灵活的运行在各种环境中

- ##  环境配置

在这一节中，可能很多内容会不那么的适用。

但是限于篇幅，我没有列举所有的安装方式。如果在安装的过程中你遇到了问题，可以在网上搜索解决，也可以在文章末尾找到我的联系方式，我们一起研究。

- ### 2.1 gRPC

```bash
go get google.golang.org/grpc
```

这一步安装的是`gRPC`的核心库，但是这一步是需要（特别的上网方式）的。所以如果在安装过程中出错了，你可以科学一波，也可以找一找其他的安装方法。

- ### 2.2 protocol buffers

在Mac OS中，直接用brew安装。

```armasm
brew info protobuf
```

- ### 2.3 protoc-gen-go

上一步安装的是protocol编译器。而上文中我们提到了可以生成各种不同语言的代码。因此，除了这个编译器，我们还需要配合各个语言的代码生成工具。

对于`Golang`来说，称为`protoc-gen-go`。

不过在这儿有个小小的坑，`github.com/golang/protobuf/protoc-gen-go`和`google.golang.org/protobuf/cmd/protoc-gen-go`是不同的。

区别在于前者是旧版本，后者是google接管后的新版本，他们之间的API是不同的，也就是说用于生成的命令，以及生成的文件都是不一样的。

因为目前的`gRPC-go`源码中的example用的是后者的生成方式，为了与时俱进，本文也采取最新的方式。

你需要安装两个库：

```go
go install google.golang.org/protobuf/cmd/protoc-gen-go
go install google.golang.org/grpc/cmd/protoc-gen-go-grpc
```

因为这些文件在安装`grpc`的时候，已经下载下来了，因此使用`install`命令就可以了，而不需要使用`get`命令。



- ### 3. proto文件创建

在开始开发之前，先说说我们的目标。

在这个`grpc-practice`项目中，我希望实现一个功能，客户端可以发送消息给服务端，服务端收到消息后，返回响应给客户端。

正如前面所说的，在开发`server`与`client`之前，我们需要先定义服务。

因此，在这一节的内容中，我将向你介绍proto文件的编写。

- #### 3.1 项目结构

在这之前，先让我们看看整个项目的初始结构。
![img](https://img2020.cnblogs.com/blog/1998080/202009/1998080-20200924161834930-1252892090.jpg)

`server`和`client`我们先不管，在这一节内容中我们先编写`*.proto'文件。

在proto文件夹中创建`message.proto`文件。

在文件的第一行，我们写上：

```ini
syntax = "proto3";
```

这是在说明我们使用的是`proto3`语法。

然后我们应该写上：

```java
option go_package = ".;message";
option go_package = "./";
```

这部分的内容是关于最后生成的go文件是处在哪个目录哪个包中，`.`代表在当前目录生成，`message`代表了生成的`go文件`的包名是`message`。

然后我们需要定义一个服务，在这个服务中需要有一个方法，这个方法可以接受客户端的参数，再返回服务端的响应。

那么我们可以这么写：

```scss
service MessageSender {
  rpc Send(MessageRequest) returns (MessageResponse) {}
}
```

其实很容易可以看出，我们定义了一个service，称为`MessageSender`，这个服务中有一个rpc方法，名为`Send`。这个方法会发送一个`MessageRequest`，然后返回一个`MessageResponse`。

让我们在看看具体的`MessageRequest`和`MessageResponse`：

```cmake
message MessageResponse {
  string responseSomething = 1;
}

message MessageRequest {
  string saySomething = 1;
}
```

`message`关键字，其实你可以理解为`Golang`中的结构体。这里比较特别的是变量后面的“赋值”。注意，这里并不是赋值，而是在定义这个变量在这个message中的位置。更具体的内容我应该会在源码分析部分讲到。

在编写完上面的内容后，在`/grpc-practice/src/helloworld/proto`目录下执行如下命令：

```lua
protoc --go_out=. message.proto
protoc --go-grpc_out=. message.proto
```

这两条命令会生成如下的两个文件：

![img](https://img2020.cnblogs.com/blog/1998080/202009/1998080-20200924161855325-187405311.jpg)

在这两个文件中，包含了我们定义方法的go语言实现，也包含了我们定义的请求与相应的go语言实现。

简单来讲，就是`protoc-gen-go`已经把你定义的语言无关的`message.proto`转换为了go语言的代码，以便`server`和`client`直接使用。

**注意，到了这一部分你可能会有一些疑惑。**

在网上的一些教程中，有这样的生成方式：

```lua
protoc --go_out=plugins=grpc:. helloworld.proto
```

这种生成方式，使用的就是`github`版本的`protoc-gen-go`，而目前这个项目已经由Google接管了。

并且，如果使用这种生成方式的话，并不会生成上图中的`xxx_grpc.pb.go`与`xxx.pb.go`两个文件，只会生成`xxx.pb.go`这种文件。

此外，你也可能遇到这种错误：

```delphi
protoc-gen-go-grpc: program not found or is not executable
Please specify a program using absolute path or make sure the program is available in your PATH system variable
--go-grpc_out: protoc-gen-go-grpc: Plugin failed with status code 1.
```

这是因为你没有安装`protoc-gen-go-grpc`这个插件，这个问题在本文中应该不会出现。

你还可能会遇到这种问题：

```verilog
--go_out: protoc-gen-go: plugins are not supported; use 'protoc --go-grpc_out=...' to generate gRPC
```

这是因为你安装的是更新版本的`protoc-gen-go`，但是你却用了旧版本的生成命令。

但是这两种方法都是可以完成目标的，只不过`api`不太一样。本文是基于Google版本的`protoc`-gen-go进行示范。

至于其他更详细的资料，你可以在这里看到：https://github.com/protocolbuffers/protobuf-go/releases/tag/v1.20.0#v1.20-generated-code



- ### GRPC的注意事项

  - **序列号一旦完成，不可更改**
  - **每个消息都是独立的个体**
  - **不完全支持`golang`所有的映射关系(例如：map嵌套)**



## 34.容器

`Dockerfile`是用来定义如何编译容器镜像的定义文件，他拥有自己独立的语法，最终编译出来的容器镜像是一个不可修改的一个整体。

**Docker常用的一些语法**

- **ADD：**添加文件到容器镜像中，注：当是压缩包时，会自动解压
- **COPY：**复制文件到容器镜像中
- **RUN：**编译镜像时运行程序
- **CMD：** 启动镜像时运行程序



### 编译容器镜像-高阶

- #### 多步骤编译镜像

  ​		当我们需要一个镜像的时候，通常会需要编译环境，配置等，最终编译出我们需要的应用。而应用运行时并不需要编译环境。多步骤编译镜像会大大缩小最终产出的容器镜像的规模。

  ​		 
