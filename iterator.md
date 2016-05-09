title: iterator
speaker: liujingji
transition: cards
files: /js/demo.js,/css/demo.css

[slide]

# ESMAScript 6 之 Iterator
## 演讲者：let和const

[slide]

# 概念 {:&.flexbox.vleft}
遍历器（Iterator）一种接口，为各种不同的数据结构提供统一的访问机制。

任何数据结构只要部署Iterator接口，就可以完成遍历操作（即依次处理该数据结构的所有成员）

[slide]

# 作用 {:&.flexbox.vleft}

1、为各种数据结果，提供一个统一的、简便的访问接口

2、使得数据结构的成员能够按某种次序排列

3、使ES6创造了一种新的遍历命令for...of循环，Iterator接口主要提供for...of消费
[slide]
# 遍历过程 {:&.flexbox.vleft}

1、创建一个指针对象，指向当前数据结构的起始位置，即遍历器本质上就是一个指针对象

2、第一次调用指针对象的next方法，可以将指针指向数据结构的第一个成员

3、第二次调用指针对象的next方法，指针就指向数据结构的第二个成员

4、不断调用指针对象的next方法，直到它指向数据结构的结束位置

每一次调用next方法，都会返回数据结构的当前成员的信息。

具体来说，就是返回一个包含value和done两个属性的对象。

其中，value属性是当前成员的值，done属性是一个布尔值，表示遍历是否结束

[slide]
# 数据结构的默认Iterator接口 {:&.flexbox.vleft}

ES6规定，默认的Iterator接口部署在数据结构的Symbol.iterator属性.

或者说，一个数据结构只要具有Symbol.iterator属性，就可以认为是“可遍历的”（iterable

调用Symbol.iterator方法，就会得到当前数据结构默认的遍历器生成函数

Symbol.iterator本身是一个表达式，返回Symbol对象的iterator属性，这是一个预定义好的、类型为Symbol的特殊值，所以要放在方括号

在ES6中，有三类数据结构原生具备Iterator接口：数组、某些类似数组的对象、Set和Map结构。

其他数据结构（主要是对象）的Iterator接口，都需要自己在Symbol.iterator属性上面部署，这样才会被for...of循环遍历

[slide]
#调用Iterator接口的场合 {:&.flexbox.vleft}
1、解构赋值
对数组喝Set结构进行结构赋值时，会默认调用Symbol.iterator方法

2、扩展运算符

3、yield*
yield*后面跟的是一个可遍历的结构，它会调用该结构的遍历器接口

4、其他的场合
由于数组的遍历会调用遍历器接口，所以任何接受数组作为参数的场合，其实都调用了遍历器接口

for...of

Array.from()

Map(), Set(), WeakMap(), WeakSet()（比如new Map([['a',1],['b',2]])）

Promise.all()

Promise.race()




