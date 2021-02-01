# java学习

# 1.head first Java

## 1.变量

除非在变量后边加 f ，否则所有的带小数点的都会被当作double

大数（int）不能存入小数（short）中，但小数可以存入大数中，（数据类型）

## 2.对象

set 和 get 的封装：用private修饰实例变量，用public修饰set和get，这样其他程序就不能随意设置任意长度的对象的实例变量，比如身高不能为负数，封装可以使你即便以后想给这个值设置界限，也不用更改其他程序

```java
private height;
void setHeight(int height){
	if(height>0){
		this.height = height
	}else{System.out.println("something wrong")}
}
```

==**== == 和 equals()区别：在object类中，两者判定的都是地址（是否指向同一个对象），在其他类中，可能equals被改写，改为值的判定。子类定义equals方法时，首先调用超类的equals，如果超类中的域都相等，则比较子类中的实例域





## ch01 基础

java中interger和boolean两种类型不相容，不能用

```java
int x = 1;
while(x){}
```

**强类型语言**：代表不允许变量保存类型的数据，不允许隐式变量类型转换，必须要进行强制类型转化才能换成别的类型，比如interger和boolean中的1，这是很关键的类型安全性功能

创建对象时，他会被存放在称为堆的内存区域，不管对象如何创建都会存在于此区域，该堆可以垃圾回收，java会根据对象大小来分配内存空间