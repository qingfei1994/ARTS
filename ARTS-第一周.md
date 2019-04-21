## ARTS-第一周
### Algorithm
[Maximun Subarray](https://github.com/qingfei1994/algorithm/blob/master/Dynamic%20Programming.md)
### Review

https://alvinalexander.com/scala/best-practice-eliminate-null-values-from-code-scala-idioms

作者建议在scala程序中消灭null。

*怎样消灭？*

通过Option(Some/None)对象取代可能为null的对象，例如方法不要返回null，返回Option对象；如果一个变量没有初始值，赋值为Option，而不是null
或者用Try(Success/Fail)来取代可能为null的对象，与Option类似，Sucess和Fail也是Try的子类。

*为什么要消灭null*
 
我尝试从作者所列出的好处寻找原因.

1.可以消灭NullPointerException

2.代码将会更加安全

3.不需要用if来判断某个对象是否为null

*NullObject 设计模式*

Effective Scala书中建议不要过度使用Option，而是用一种NullObject的模式。Null Object就是一个继承自基类并且赋予空的行为的类，如下面所示。

```
trait Animal {
	def makeSound()
}
class Dog extends Animal {
	def makeSound() {println("woof")}
}
class NullObject extends Animal {
	def makeSound(){}
}
```
 
### Tips

1.在Vim中输入^A等字符需要用ctrl+V+A

2.Scala Option的正确使用方式

https://alvinalexander.com/scala/best-practice-option-some-none-pattern-scala-idioms


在scala中，Option是Some和None的父类，意味着当一个函数返回Option对象的时候，可能是Some的对象，也可能是None，所以我们一般会通过模式匹配/getOrElse/foreach来处理Option

例如：

假设a是Option对象，

```scala
val b = a match {
case Some(a) => a
case None => throw new Exception()
}
```

又或者从方法返回Option对象

```scala
def toInt(s:String) :Option[Int] = {
try {
Some(Integer.parseInt(s))
} catch {
case e:Exception => None
}
}
```
