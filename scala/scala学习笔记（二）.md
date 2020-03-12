[TOC]

# 1.面向对象和函数式编程

**面向对象**

解决问题时，将问题拆解称一个一个小问题（形成了对象）；分别解决对象关系，继承，实现，重写，多态。

**函数式编程**

关心的是问题的解决方案（封装功能），重点在于函数（功能）函数的入参，出参。

> Java中的方法和Scala中的函数都可以进行功能的封装，但是方法必须和类型绑定，但是函数不需要。

# 2.函数

## **Java方法声明**

```java
public static void test(String s){}
```

## **函数声明**

```scala
def test(s : String): Unit ={
	//函数体
	println(s)
}
```

## 调用函数

```scala
test("zhangsan")
```

> Scala语法非常灵活，在任意的语法中可以声明其他语法规则。

* 函数没有重载的概念，在同一个作用域中，函数不能重名；
* Scala中没有throws关键字，所以函数中如果有异常发送，也不需要在函数声明时抛出异常。

* Scala可以采用自动推断功能来简化函数的声明
  * 如果函数声明时，明确无返回值Unit，那么即使函数体中有return也不起作用；
  * 如果将函数体的最后一行代码进行返回，那么return关键字可以省略；
  * 如果可以根据函数的最后一行代码推断类型，那么函数返回值类型可以省略；
  * 如果函数只有一行代码，大括号可以省略；
  * 如果函数声明中没有参数列表，小括号可以省略。

# 3.常见函数类型

## 可变参数

```scala
def test(name :String*):Unit={
	println(name)
}
//调用函数时，可以传多个参数，也可以不传参数。
test("zhangsan","lisi","wangwu")
test()
```

## 默认参数

```Scala
def test(name :String,age :Int=20):Unit={
	println(s"${name}-${age}")
}
//在不传的情况下，会使用默认值。
//调用函数时，参数匹配规则为从前到后。
test("lisi")
test("zhangsan",30)
```

## 带名参数

```scala
def test(name2:String="lisi",name1:String):Unit={
	println(s"${name1}-${name2}")
}
test(name1="zhangsan")
```

## 递归函数

```scala
/**
     * 递归函数 
     * 5的阶乘
     */
    def fun2(num :Int) :Int= {  //必须写返回值类型
      if(num ==1)
        num
      else 
        num * fun2(num-1)
    }
    print(fun2(5))
```

## 匿名函数

```Scala
/**
 * 匿名函数
 * 1.有参数匿名函数
 * 2.无参数匿名函数
 * 3.有返回值的匿名函数
 * 注意：
 * 可以将匿名函数返回给定义的一个变量
 * 匿名函数不能显式声明函数的返回类型

 */
//有参数匿名函数
val value1 = (a : Int) => {
  println(a)
}
value1(1)
//无参数匿名函数
val value2 = ()=>{
  println("123")
}
value2()
//有返回值的匿名函数
val value3 = (a:Int,b:Int) =>{
  a+b
}
println(value3(4,4))
```

## 嵌套函数

```Scala
/**
     * 嵌套函数：
     * 		在函数体内有定义了一个函数
     */
    def fun7(num:Int)={
      def fun8(a:Int,b:Int):Int={
        if(a == 1){
          b
        }else{
          fun8(a-1,a*b)
        }
      }
      fun8(num,1)
    }
```

## 偏应用函数

偏应用函数是一种表达式，不需要提供函数需要的所有参数，只需要提供部分，或不提供所需参数。在多个函数调用时，有共同的参数被使用，则可提取出来默认写死，只需要为函数提供部分的参数。

```scala
/**
 * 偏应用函数
 */
def log(date :Date, s :String)= {
  println("date is "+ date +",log is "+ s)
}

val date = new Date()
log(date ,"log1")
log(date ,"log2")
log(date ,"log3")

//想要调用log，以上变化的是第二个参数，可以用偏应用函数处理
val logWithDate = log(date,_:String)    //下划线相当于占位符的作用，手动传入即可
logWithDate("log11")
logWithDate("log22")
logWithDate("log33")
```

## 高阶函数

函数的参数是函数，或者函数的返回类型是函数，或者函数的参数和函数的返回类型是函数的函数。

```scala
//函数的参数是函数
    def hightFun(f : (Int,Int) =>Int, a:Int ) : Int = {
      f(a,100)
    }
    def f(v1 :Int,v2: Int):Int  = {
      v1+v2
    }
    
    println(hightFun(f, 1))
    
    //函数的返回是函数
    //1，2,3,4相加
    def hightFun2(a : Int,b:Int) : (Int,Int)=>Int = {
      def f2 (v1: Int,v2:Int) :Int = {
        v1+v2+a+b
      }
      f2
    }
    println(hightFun2(1,2)(3,4))
    
    //函数的参数是函数，函数的返回是函数
    def hightFun3(f : (Int ,Int) => Int) : (Int,Int) => Int = {
      f
    } 
    println(hightFun3(f)(100,200))
    println(hightFun3((a,b) =>{a+b})(200,200))
    //以上这句话还可以写成这样
    //如果函数的参数在方法体中只使用了一次 那么可以写成_表示
    println(hightFun3(_+_)(200,200))
```

## 柯里化函数

```scala
/**
       * 柯里化函数
       * 		可以理解为高阶函数的简化
       * 		klhFun函数就是对嵌套函数这种情况的高阶函数的简化版
       */

      def klhFun(a:Int)(b:Int) = a*b
      具体：
      def klhAllFun(a:Int):(Int)=>Int = {
        val fun = (b:Int)=>a*b
        fun
      }
```

