
# 现代Fortran编程的工程规范 

---
使用模块（module）来组织代码，避免使用全局变量和共用体（common block）。
使用隐式无（implicit none）来声明变量类型和属性，避免使用隐式类型转换。
使用意义明确的变量名和注释来提高代码可读性。
使用子程序（subroutine）和函数（function）来封装功能，避免使用goto语句。
使用接口（interface）来定义子程序和函数的参数类型和数量，避免使用隐式接口。
使用分配（allocatable）数组来动态分配内存，避免使用指针（pointer）数组或静态数组。
使用派生类型（derived type）来定义复杂的数据结构，避免使用结构体（structure）或记录体（record）。
使用泛型过程（generic procedure）来实现多态性，避免使用重载操作符或重载函数。
使用类（class）和扩展类型（extended type）来实现继承和动态绑定，避免使用抽象接口或抽象派生类型。
---

## 概述

根据网上的一些文章 ，现代Fortran编程的工程规范可以包括以下几个方面

- 使用模块化和封装的思想，将程序分为不同的模块和子程序，避免使用全局变量和共用体。
- 使用隐式无类型声明和显式接口，避免使用隐式类型转换和隐含接口。 
- 使用动态内存分配和指针，避免使用固定大小的数组和公共区域。 
- 使用自定义数据类型和派生类型，避免使用简单类型和结构体。 
- 使用面向对象的特性，如继承、多态、泛型、抽象类等，提高代码的复用性和可扩展性。 
- 使用函数式编程的特性，如纯函数、递归、高阶函数等，提高代码的简洁性和可读性。 
- 遵循一些编码风格和规范，如命名规则、缩进对齐、注释说明等，提高代码的可维护性。 

## 示例代码 

以下是一些现代Fortran编程的示例代码： 

### 使用模块化和封装的思想 

```fortran
! 定义一个数学模块 
module math_module contains 
! 定义一个求平方根的子程序 
subroutine sqrt(x,y) 
implicit none 
real, intent(in) :: x ! 输入参数 
real, intent(out) :: y ! 输出参数 
y = x**0.5 ! 计算平方根 
end subroutine sqrt 
end module math_module 
! 调用数学模块 
program test 
use math_module ! 使用模块 
implicit none 
real :: a,b a = 4.0 
call sqrt(a,b) ! 调用子程序 
print *, 'The square root of ', a, ' is ', b 
end program test 
``` 

### 使用隐式无类型声明和显式接口 

```fortran
! 定义一个函数模块 
module func_module contains 
! 定义一个求阶乘的函数，并使用显式接口声明输入输出类型 
function factorial(n) result(f) 
implicit none ! 隐式无类型声明 
integer, intent(in) :: n ! 输入参数类型为整数 
integer :: f ! 输出结果类型为整数 
if (n == 0) then ! 递归边界条件 
f = 1 
else 
f = n * factorial(n-1) 
! 递归调用函数本身 
end if 
end function factorial 
end module func_module 

! 调用函数模块 
program test 
use func_module ! 使用模块 
implicit none 
integer :: n,m n = 5 
m = factorial(n) ! 调用函数 
print *, 'The factorial of ', n, ' is ', m 
end program test 
```

### 使用动态内存分配和指针

```fortran
! 定义一个动态数组并使用指针操作 
program test 
implicit none 
integer, pointer :: p(:,:) ! 声明一个二维整数指针数组 
integer :: i,j,n,m n = 3 ; m = 4 ! 给定数组大小 
allocate(p(n,m)) ! 动态分配内存空间 
do i=1,n ! 给数组赋值 
do j=1,m 
p(i,j) = i*j 
end do 
end do 
do i=1,n ! 打印数组元素 
do j=1,m 
print *, 'p(',i,',',j,')=', p(i,j) 
end do 
end do 
deallocate(p) ! 释放内存空间
```

### 使用自定义数据类型和派生类型

```fortran
! 定义一个自定义数据类型表示复数，并重载加法运算符(+)
type complex_number 
real :: real_part 
real :: imag_part 
contains 
operator(+) => complex_addition    
end type complex_number 

function complex_addition(x,y) result(z)
type(complex_number), intent(in) :: x,y
type(complex_number) :: z
z%real_part = x%real_part + y%real_part
z%imag_part = x%imag_part + y%imag_part    
end function complex_addition 

program test 
implicit none 
type(complex_number) :: a,b,c
a = complex_number(1.0,2.0)
b = complex_number(3.0,-4.0)
c = a + b ! 使用重载的加法运算符
print *, 'The sum of ', a, ' and ', b, ' is ', c    
end program test 
```

### 使用面向对象的特性

```fortran
! 定义一个抽象类表示几何形状，并定义一个纯虚函数求面积 abstract 
type shape 
contains 
pure function area(self) result(a)
class(shape), intent(in) :: self ! 使用类参数表示多态
real :: a 
end function area 
end type shape 

! 定义一个派生类表示圆形，并实现求面积的函数
type, extends(shape) :: circle 
real :: radius 
contains 
function area(self) result(a)
class(circle), intent(in) :: self ! 使用类参数表示多态
real :: a 
a = 3.14 * self%radius**2 ! 计算圆形面积
end function area 
end type circle 

! 定义一个派生类表示矩形，并实现求面积的函数
type, extends(shape) :: rectangle 
real :: length,width 
contains 
function area(self) result(a)
class(rectangle), intent(in) :: self ! 使用类参数表示多态
real :: a 
a = self%length * self%width ! 计算矩形面积
end function area 
end type rectangle 
! 调用抽象类和派生类
```

### 使用函数式编程的特性 

```fortran
! 定义一个高阶函数，接受一个函数作为参数，并返回一个函数作为结果 
function compose(f,g) result(h) 
implicit none 
interface function f(x) 
real :: x 
real :: f 
end function 

f function g(x) 
real :: x 
real :: g 
end function g 
end interface interface 

function h(x) 
real :: x 
real :: h 
end function h 
end interface 

h = lambda(x) f(g(x)) 
! 使用lambda表达式定义一个复合函数 
end function compose 

! 定义两个简单的函数，分别求平方和开方 
function square(x) 
implicit none 
real :: x,square 
square = x**2 ! 计算平方 
end function square 

function root(x) 
implicit none 
real :: x,root 
root = x**0.5 ! 计算开方 
end function root 
 
! 调用高阶函数和简单函数
program test 
implicit none 
real :: x,y 
interface 
function f(x)
real :: x 
real :: f 
end function f 
end interface 
x = 4.0 ! 给定一个数值
f = compose(square,root) ! 使用高阶函数组合两个简单函数
y = f(x) ! 调用复合函数
print *, 'The result of applying ', f, ' to ', x, ' is ', y ! 打印结果
end program test 
```

### 遵循一些编码风格和规范

! 使用缩进对齐，使用空格分隔符号，使用下划线连接单词，使用有意义的变量名，使用注释说明代码功能
! 定义一个模块，实现一个求解二次方程的子程序

```fortran
module equation_module 
contains 
! 定义一个求解二次方程的子程序，并检查输入参数是否合法
subroutine solve_quadratic_equation(a,b,c,x1,x2)
    implicit none 
    real, intent(in) :: a,b,c ! 输入参数为二次方程的系数
    real, intent(out) :: x1,x2 ! 输出参数为二次方程的根
    real :: delta ! 定义一个局部变量表示判别式
    
    if (a == 0.0) then ! 检查a是否为零，如果是则停止程序并报错
        stop 'Error: a cannot be zero.'
    end if 
    
    delta = b**2 - 4*a*c ! 计算判别式
    
    if (delta < 0.0) then ! 检查判别式是否小于零，如果是则停止程序并报错
        stop 'Error: no real roots.'
    end if 
    
    x1 = (-b + sqrt(delta)) / (2*a) !
    x2 = (-b - sqrt(delta)) / (2*a) ! 计算第二个根
    
end subroutine solve_quadratic_equation 
end module equation_module 

! 调用模块中的子程序
program test 
use equation_module ! 使用模块
implicit none 
real :: a,b,c,x1,x2 
a = 1.0 ; b = -5.0 ; c = 6.0 ! 给定二次方程的系数
call solve_quadratic_equation(a,b,c,x1,x2) ! 调用子程序求解二次方程
print *, 'The roots of the equation are ', x1, ' and ', x2 ! 打印结果
end program test 

```
