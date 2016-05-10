title: Generator
speaker: liujingji
url: https://github.com/ksky521/nodePPT
transition: cards
files: /js/demo.js,/css/demo.css

[slide]

# ESMAScript 6 之 Generator
## 演讲者：刘经济



[slide]

# 基本概念 {:&.flexbox.vleft}
* Generator函数是ES6提供的一种异步编程解决方案,可以把它理解成，Generator函数是一个状态机，封装了多个内部状态

* 执行Generator函数会返回一个遍历器对象,返回的遍历器对象，可以依次遍历Generator函数内部的每一个状态




[slide]
# 基本特点 {:&.flexbox.vleft}
+ function关键字与函数名之间有一个星号
+ 函数体内部使用yield语句，定义不同的内部状态




[slide]
# HelloWorld样例 {:&.flexbox.vleft}
```javascript
function* helowWorldGenerator() {
	yield 'hello';
	yield 'world';
	return 'ending';
}
let hw = helowWorldGenerator();
```

[slide]
# 执行 {:&.flexbox.vleft}
- Generator函数的调用方法与普通函数一样，也是在函数名后面加上一对圆括号。
- 调用Generator函数后，该函数并不执行，返回的也不是函数运行结果，而是一个指向内部状态的指针对象
- 必须调用遍历器对象的next方法，使得指针移向下一个状态

```javascript
hw.next()
// { value: 'hello', done: false }
hw.next()
// { value: 'world', done: false }
hw.next()
// { value: 'ending', done: true }
hw.next()
// { value: undefined, done: true }
```




[slide]
# yield语句 {:&.flexbox.vleft}
调用遍历器对象next方法,指针便移向下一个状态即遇到yield语句停止。

yield语句是暂停执行的标记

遍历器对象的next方法的运行逻辑：
1. 遇到yield语句，就暂停执行后面的操作，并将紧跟在yield后面的那个表达式的值，作为返回的对象的value属性值
2. 下一次调用next方法时，再继续往下执行，直到遇到下一个yield语句
3. 如果没有再遇到新的yield语句，就一直运行到函数结束，直到return语句为止，并将return语句后面的表达式的值，作为返回的对象的value属性值
4. 如果该函数没有return语句，则返回的对象的value属性值为undefined





[slide]
#next方法的参数 {:&.flexbox.vleft}
yield句本身没有返回值，或者说总是返回undefined。

next方法可以带一个参数，该参数就会被当作上一个yield语句的返回值