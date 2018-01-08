# go
[go语言的主要特点](#go语言的主要特点)  
[go的常用关键字用途](#go的常用关键字用途)  
[go的代码编写常识](#go的代码编写常识)  
[go的可见性规则](#go的可见性规则)  
[go的基本数据类型](#go的基本数据类型)


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
   32位整型: int32(rune)/uint32  
    长度: 4字节  
    取值范围: -2^32/2\~2^32/2-1/0\~2^32-1  
   64位整型: int64/uint64  
    长度: 8字节  
    取值范围: -2^64/2\~2^64/2-1/0\~2^64-1  
   浮点型: float32/float64   
    长度: 4/8字节  
    小数位: 精确到7/15小数位  
   复数: complex64/complex128  
    长度: 8/16字节  
   足够保存指针的32位或64位整数型: uintptr  
   其他值类型: array, struct, string  
   引用类型: slice, map, chan  
   接口类型: interface  
   函数类型: func  
   
    





