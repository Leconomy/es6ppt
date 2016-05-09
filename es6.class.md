title: class
speaker: liujingji
url: https://github.com/ksky521/nodePPT
transition: cards
files: /js/demo.js,/css/demo.css

[slide]

# ESMAScript 6 之 Class
## 演讲者：刘经济

[slide]

# 基本语法 {:&.flexbox.vleft}
```javascript
class ClassName {
	
	constructor(arg1, arg2) {    // 构造函数
		this.arg1 = arg1;
		this.arg2 = arg2;
	}

	funName() {                  // 直接写方法名即可，不需要加function关键字
		// 方法体
	}

	funName1() {                 // 方法之间不需要加逗号分隔
		// 方法体
	}
}
类的所有方法仍然都定义在类的prototype属性上
```
类的方法都定义在prototype对象上面，所有类的新方法可以添加在prototype对象上面
Object.assign方法可以很方便的向类中添加多个方法

```javascript
Class ClassName {
	constructor() {

	}
}
Object.assign(ClassName.prototype, {
	fun1Name() {

	},
	fun2Name() {

	}
})
```
类的内部所以定义的方法，都是不可枚举的
类的属性名，可以采用表达式，但是需要吧变量放在[]中
[slide]
#constructor方法 {:&.flexbox.vleft}

constructor方法是类的默认方法，当用new创建实例时，会自动调用该方法

一个类必须有constructor方法，如果没有显示定义，会默认添加一个空的constructor方法

```javascript
constructor() {}
```
constructor方法默认返回实例对象，也可以指定返回另外的一个对象
```javascript
class Person {
	constructor() {
		return Object.create(null);
	}
}
new Person() instanceof Person
// false
```
[slide]
#实例对象 {:&.flexbox.vleft}
实例化对象仍然通过使用new命令，但是忘记加new会报语法错误

实例对象的属性除非显示定义在其自身上，否则都是定义在prototype上

类的所有实例共享一个prototype对象即实例对象的____proto____指向类

```javascript
let p1 = new Person('zhangsan', 30);
let p2 = new Person('lisi', 20);

p1.__proto__.say = function() {return 'I am a good man';}

p1.say(); // 'I am a good man'
p2.say(); // 'I am a good man'

let p3 = new Person('wangwu', 25);
p3.say() // 'I am a good man'
```
因此可以使用实例对象的__proto__改写原型，从而改写Class的原始定义，强烈建议不使用它


[slide]
#Class表达式 {:&.flexbox.vleft}
```javascript
const MyClass = class Me {     // Me如果在内部没用到可以省略
	getClassName() {
		return Me.name;
	}
}
```
类的名字为MyClass而不说Me，Me只在Class内部代码可用，指代当前类

采用表达式，可以写出立即执行的Class
```javascript
let Person = new class {
	constructor(name) {
		this.name = name;
	}

	sayName() {
		console.log(this.name)
	}

}('zhangsan');
person.sayName();   // 'zhangsan'
```

[slide]
#不存在变量提升 {:&.flexbox.vleft}
```javascript
{
	let Person = class {};
	class Teacher extends Person
}
```
如果存在Class的提升，上面代码就会报错。因为let命令说不会提成的
[slide]
#Extends的继承目标 {:&.flexbox.vleft}
extends关键字后面可以跟多种类型的值
```javascript
class A extends A{}
```
只要说一个有prototype属性的函数，就能被B继承
由于函数都有prototype属性，因此A可以说任意函数
[slide]
#Object.getPrototypeOf() {:&.flexbox.vleft}
Object.getPrototypeOf方法可以用来葱子类上获取父类
```javascript
Object.getPrototypeOf(B) === A
// true
```
[slide]
#super关键字 {:&.flexbox.vleft}
在子类中，super关键字代表父类
```javascript
class B extends A {
	get m() {
		return this._p * super._p;  // 通过super关键字，调用父类的实例
	}
	set m() {
		throw new Error('read only')
	}
}
```
对象总是继承其他对象的，所以可以在任意一个对象中，使用super关键字
```javascript
var obj = {
	toString() {
		return 'MyObject:' + super.toString();
	}
}
obj.toString() // MyObject:[object Object]
```
[slide]
#Class的取值函数和存值函数 {:&.flexbox.vleft}
在Class内部可以使用get和set关键字，对某个属性设置存值函数和取值函数，拦截该属性的存取行为
存值函数和取值函数是设置在属性的descriptor对象上的

[slide]
#Class的静态方法 {:&.flexbox.vleft}
在方法前加上static关键字，就表示此方法上静态方法，只能通过类来调用
父类的静态方法，可以被子类继承
静态方法也是可以从super对象上调用
ES6规定类的内部没有静态属性，但是ES7有一个提案即在属性名前加static
