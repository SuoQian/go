# go
[go语言的主要特点](#go语言的主要特点)  
[go的常用关键字用途](#go的常用关键字用途)  
[go的代码编写常识](#go的代码编写常识)  
[go的可见性规则](#go的可见性规则)  
[go的基本数据类型](#go的基本数据类型)  
[go变量的声明格式](#go变量的声明格式)  
[go变量的类型转换](#go变量的类型转换)  
[go常量的声明定义](#go常量的声明定义)  
[go控制语句](#go控制语句)  






### go语言的主要特点

1. 以非常直观和极低的方案实现高并发

2. 高效的垃圾回收机制

3. 快速编译(同时解决C语言中头文件太多问题,  
   简言之就是之前被导入的有用的包在代码迭代  
   之后若变得无用,裁之,以提高代码的编译速度)

4. 为多核计算机提供性能提升的方案(在程序运行过程当中  
   允许指定去调用多少个cpu的核数, 以此来提升程序的整体性能)

5. UTF-8编码支持(每一个go的源码都是UTF-8格式, 因此可以  
   支持任何字符包括中文)

### go的常用关键字用途

1. go程序是通过package来组织的, 只有package名称为  
   main的包可以包含main函数, 一个可执行程序有且仅  
   有一个main包  
   
2. 通过import关键字来导入其他非main包  

3. 通过const关键字来进行常量的定义  

4. 通过在函数体外部使用var关键字来进行全局变量的声明与赋值  

5. 通过type关键字来进行结构(struct)或接口(interface)的声明  

6. 通过func关键字来进行函数的声明

### go的代码编写常识

1. `package main` 必须作为任一go程序可执行代码的第一行


2. 
   ```
   import "fmt"
   import "os"
   import "io"
   import "time"
   ```  
   一般情况下将以上代码简写为下面的形式  
   ```
   import (
      "fmt"
      "os"
      "io"
      "time"
   )
   ```  

	不止是导包可以简写为上面的形式,以下也是可以的:  
 
    ```
   //常量的定义  
   const (
	PI = 3.14
	const1 = "1"
	const2 = 2
	const3 = 3 
   )
   ```  
    ```
   //全局变量的声明与赋值
   var (
	name1 = "suo"
	name2 = "1"
	name3 = 2
	name4 = 3
   )
   ```  
    ```
   //一般类型的声明
   type (
	newtype int
	type1 float
	type2 string
	type3 byte
   )
   ```
   
3. 当使用第三方包时, 包名可能会非常接近易混淆甚至有可能同名  
   此时就可以给包起别名进行区别和调用, 如:  
   `import (io "fmt")` 给fmt包起别名为io  
   `io.Println("Hello World")` 用io这个别名对包进行调用
   
### go的可见性规则  

1. go语言中使用大小写来决定,常量, 变量, 类型, 结构, 接口, 函数,  
是否可被外部包所调用, 根据约定函数名首字母为小写即为: private  
   为大写即为: public

### go的基本数据类型

1. 布尔型: bool   
    长度: 1字节  
    取值范围: true, false  
    注意事项: 不可以用0,1数字代表true或false  

2. 整型: int/uint  
    根据运动平台可能为32位或64位  

3. 8位整型: int8/uint8  
    长度: 1字节  
    取值范围: -128 ~ 127/0 ~ 255  
    
4. 字节型: byte(uint8别名)  

5. 16位整型: int16/uint16  
    长度: 2字节  
    取值范围: -32768\~32767/0\~65535  
    
6. 32位整型: int32(rune)/uint32  
    长度: 4字节  
    取值范围: -2^32/2\~2^32/2-1/0\~2^32-1  
    
7. 64位整型: int64/uint64  
    长度: 8字节  
    取值范围: -2^64/2\~2^64/2-1/0\~2^64-1  
    
8. 浮点型: float32/float64   
    长度: 4/8字节  
    小数位: 精确到7/15小数位  
    
9. 复数: complex64/complex128  
    长度: 8/16字节  

10. 足够保存指针的32位或64位整数型: uintptr  

11. 其他值类型: array, struct, string  

12. 引用类型: slice, map, chan  

13. 接口类型: interface  

14. 函数类型: func  

15. 类型零值: 零值并不等于空值, 而是当变量被声明为某种类型后的默认值  
通常情况下值类型的默认值为0, bool为false, string为空字符串"",  
array数组如果没有指定容量, 默认值为\[], 如果指定了容量, 默认值  
与所指定的元素的类型的默认值一致,比如:\[1]int为\[0], \[1]bool为\[false]  
    
16. 溢出检查: 使用`fmt.Println(math.MaxInt/MinInt8/16/32/64)`检查  
使用的类型是否满足业务需要, 避免溢出.  

17. 在声明变量时可以给类型起别名, 这和给包起别名很类似, 甚至支持中文格式  
的别名, 只是不常这样用.  

### go变量的声明格式  

1. 变量的声明: var name type    
变量的赋值: name = value  

2. 声明和赋值一次完成: var name type = value(注: type可以省略, 编译器会根据value自动推断)    

3. 变量的声明和赋值最简版: name := value  

4. 多个变量的声明与赋值: 多个全局变量声明可以使用var()的形式进行简写, 可以写在一行, 但var不能省略,  
所有变量都可以使用类型推断, 多个局部变量不可以使用var()简写, 但可以如下方式简写  
```
//多个局部变量声明  
var a, b, c, d int  
//多个局部变量赋值  
a, b, c, d = 1, 2, 3, 4  
//多个局部变量声明和赋值  
var e, f, g, h int = 5, 6, 7, 8  
//省略变量类型, 由系统判断  
var i, j, k, l = 9, 10, 11, 12  
//多个局部变量声明和赋值的最简写法  
m, n, o, p := 13, 14, 15, 16  
```  
name可以使用 _ , 可用于忽略函数的某个返回值,  

### go变量的类型转换  

1. go不存在隐式转换, 所有类型转换必须显示声明, 转换只能发生在两种相互兼容的类型之间,  
```
//在相互兼容的两种类型之间进行转换  
var a float32 = 1.1  
b := int(a)  
//下面的转换无法通过编译  
var c bool = true  
d := int(c)
```  
2. 从严格意义上讲, type newint int, 这里的newint并不能说是int的别名, 而只是底层数据结构相同  
在这里称为自定义类型, 在进行类型转换时仍旧需要显式转换, 但是byte和rune确实是uint8和int32的别名  
可以相互进行转换.

### go常量的声明定义  

1. 常量的值在编译时就已经确定  
2. 常量的定义格式与变量基本相同  
3. 等号右边必须是常量或常量表达式, 不可以是程序运行时才能得到的值.   
4. 常量表达式中的函数必须是内置函数  
5. 常量的名称一般为全大写, 但是根据go语言的特点, 首字母为大写既可被外部包调用, 为了不让外部包调用  
可以在常量名前加 \_(下划线) 或 c(小写c 即const的首字母)  

6. 常量的初始化与枚举:  
     在定义常量组时, 如果不提供初始值, 则表示将使用上一行的表达式.  
     使用相同的表达式不代表具有相同的值  
     iota是常量计数器, 从0开始, 组中每定义一个常量自动递增1  
     通过初始化规则与iota可以达到枚举的效果  
     每遇到一个const关键字, iota会重置为0  
     
### go控制语句  

1. if判断语句的左大括号必须和if放在同一行, 否则会报编译错误  
2. for循环语句的左大括号同样必须和for放在同一行, 否则会报编译错误  








