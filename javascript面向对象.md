# 目标
* 面向对象
* 类和对象的关系
* 使用class创建自定义类
* 继承
# 面向对象编程介绍
## 面向过程编程
POP(process-oriented programming)

分析出解决问题需要的**步骤**，用函数将步骤实现，使用时再依次调用函数。
## 面向对象编程
OOP(object-oriented programming)

把事务分解为一个个的**对象**，由对象之间分工合作
### 特性
* 封装性
* 继承性
* 多态性
## OOP 与 POP 对比
面向过程
* 优点：性能比面向对象高，适合跟硬件联系很紧密的编程，例如单片机。
* 缺点：没有面向对象易维护、易复用、易扩展。
面向对象
* 优点：易维护、易复用、易扩展，由于面向对象有封装、继承、多态的特性，可设计出低耦合的系统。
* 缺点：性能比面向过程低。
# 类和对象
思维特点：

类：抽取对象共用的属性和行为封装成一个类，泛指某一大类。

对象：对类进行实例化，泛指某一个。
## 对象
在javascript中，对象是一组无序的属性和方法的集合，所有的事物都是对象，例如：字符串、数值、数组和函数等。

对象组成：

* 属性：事物的特征，常用名词
* 方法：事物的行为，常用动词
## 类
**ES6新增**了类的概念，即用关键字class声明，之后可用该类实例化对象。
### 创建
```javascript
/* 创建类 */
class Person {
  constructor(name) {
	/* this指代的是对象，不是类 */
	this.name = name;
  }
  say(word) {
	console.log(word)
  }
}
/* 创建对象 */
const lily = new Person('lily')
```
* 所有函数不用写function
* 函数间没有”，“
### constructor构造函数
* 是类的默认方法
* 用于传递参数返回实例对象
* 通过new命令生成对象实例时，自动调用该方法，如果没有显示定义，类的内部会自动创建一个constructor()
## 继承
```javascript
class Father {
  // this指代父类Father
  contructor(x, y) {
	this.x = x
	this.y = y
  }
  money() {
	console.log('money')
  }
  sum() {
	console.log(this.x + this.y)
  }
}
class Son extends Father {
  // this指代子类Son
  contructor(x, y) {
	this.x = x
	this.y = y
  }
}
const son = new Son()
// ok
son.money()
// uncaught referenceerror: must call super constructor
son.sum(1,2)
```
解释：
* Son中的this指代Son,Father中的this指代父类Father，son.sum(1,2)执行后Son子类确实可以获取到值，但该值并未传递给Father，因此报错
### super关键字
* 用于**访问**以及**调用**父类上的函数
* 可调用父类的构造函数，也可调用父类的普通函数
```javascript
class Father {
  // this指代父类Father
  contructor(x, y) {
	this.x = x
	this.y = y
  }
  money() {
	console.log('money')
  }
  sum() {
	console.log(this.x + this.y)
  }
}
class Son extends Father {
  // this指代子类Son
  contructor(x, y) {
	// this.x = x
	// this.y = y

	// 调用父类中的构造函数
	super(x,y);
  }
}
const son = new Son()
// ok
son.money()
// ok 3
son.sum(1,2)
```
### 使用父类的普通函数

```javascript
class Father {
  say() {
	console.log('father')
  }
}
class Son extends Father {
  say() {
	console.log('son')
  }
}
const son = new Son()
// son
say()
```

```javascript
class Father {
  say() {
	console.log('father')
  }
}
class Son extends Father {
  say() {
	// super.say()即调用父类的方法
	console.log(super.say())
  }
}
const son = new Son()
// father
say()
```
备注：

* 继承中的属性或方法查找原则：**就近原则**即子类没有才去父类查找
* 子类扩展自己的方法时，super必须在子类this之前调用
```javascript
class Father {
  constructor() {
	this.x = x
	this.y = y
  }
  sum() {
	console.log(this.x + this.y)
  }
}
class Son extends Father {
  constructor() {
	// super()在this之前调用
	super(x,y)
	this.x = x
	this.y = y
  }
  subtract() {
	console.log(this.x - this.y)
  }
}
const son = new Son()
// father
say()
```
注意点：
* 在ES6中没有变量提升，所以必须先定义类，然后才能实例化对象

```javascript
const son = new Son()
// 报错
say()

class Son {
  constructor() {
	// super()在this之前调用
	super(x,y)
	this.x = x
	this.y = y
  }
  subtract() {
	console.log(this.x - this.y)
  }
}
```
* 类里面的共有的属性和方法要加this使用
## 类里面的this指向问题
* constructor 里面的this指代的是创建的**实例对象**
* 普通方法 里面的this指代的是**调用对象**

```javascript
let that

class Son {
  constructor() {
	// constructor 里面的this指代的是 创建的实例对象
	that = this
	this.x = x
	this.y = y
	this.btn = document.querySelector('button')
	this.btn.click = this.sing;
  }
  sing() {
  // 这个方法里面的this指向btn按钮，因为这个按钮调用了这个函数
  console.log(this)
  // 如果在这个函数中想访问constructor里的this，可在全局声明一个变量，并将constructor里的this赋值给该全局变量，即代码里的that
  }
  dance() {
  // 这个方法里面的this指向son对象，因为son对象调用了这个函数
  console.log(this)
  }
}
const son = new Son()
son.dance()
```





























