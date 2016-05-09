title: Set和Map
speaker: 刘经济
transition: cards
files: /css/common.css

[slide]

# ESMAScript 6 之 Set和Map
## 演讲者：刘经济




[slide]
#Set  {:&.flexbox.vleft}

ES6提供了新的数据结构Set。它类似于数组，但是成员的值都是唯一的，没有重复的值

Set本身是一个构造函数，用来生成Set数据结构

Set函数可以接受一个数组（或类似数组的对象）作为参数，用来初始化

向Set加入值的时候，不会发生类型转换

```javascript
var s = new Set();
[1, 2 ,3, 4, 5, 5, 3].map(x => s.add(x));
for(let i of s) {console.log(i)};
// 1 2 3 4 5

var set = new Set([1, 2, 3, 4, 4])
[...set]
// [1, 2, 3, 4]
```




[slide]  
#Set实例的属性和方法 {:&.flexbox.vleft}

属性：

	Set.prototype.constructor：构造函数，默认就是Set函数。

	Set.prototype.size：返回Set实例的成员总数



[slide]  
#Set实例的属性和方法 {:&.flexbox.vleft}

操作方法方法:

	add(value)：添加某个值，返回Set结构本身。

	delete(value)：删除某个值，返回一个布尔值，表示删除是否成功。

	has(value)：返回一个布尔值，表示该值是否为Set的成员。

	clear()：清除所有成员，没有返回值





[slide]  
#Set实例的属性和方法 {:&.flexbox.vleft}
遍历方法:

	keys()：返回一个键名的遍历器

	values()：返回一个键值的遍历器

	entries()：返回一个键值对的遍历器

	forEach()：使用回调函数遍历每个成员


注意：由于Set结构没有键名，只有键值（或者说键名和键值是同一个值），所以key方法和value方法的行为完全一致



[slide]  
#WeakSet {:&.flexbox.vleft}

WeakSet的成员只能是对象，而不能是其他类型的值	
WeakSet中的对象都是弱引用
WeakSet不能遍历





[slide]
#Map  {:&.flexbox.vleft}
key可以为任何数据类型的键值对集合

```javascript
let o = {p: 'hello world'}
let m = new Map();
m.set(o, 'content');
m.get(o); // content
```


[slide]
#Map  {:&.flexbox.vleft}

Map也可以接受一个数组作为参数。该数组的成员是一个个表示键值对的数组

```javascript
var map = new Map([["name", "张三"], ["title", "Author"]]);

map.size // 2
map.has("name") // true
map.get("name") // "张三"
map.has("title") // true
map.get("title") // "Author"
```

[slide]
#Map  {:&.flexbox.vleft}
注意：

1、只有对同一个对象的引用，Map结构才将其视为同一个键

2、如果对同一个键多次赋值，后面的值将覆盖前面的值

3、如果读取一个未知的键，则返回undefined

4、Map的键实际上是跟内存地址绑定的，只要内存地址不一样，就视为两个键

5、如果Map的键是一个简单类型的值（数字、字符串、布尔值），则只要两个值严格相等，Map将其视为一个键，包括0和-0

6、Map将NaN视为同一个键





[slide]
#Map  {:&.flexbox.vleft}
属性：

	size：属性返回Map结构的成员总数


[slide]
#Map  {:&.flexbox.vleft}

操作方法方法:

	set(key, value): set方法设置key所对应的键值，然后返回整个Map结构。如果key已经有值，则键值会被更新，否则就新生成该键

	get(key): get方法读取key对应的键值，如果找不到key，返回undefined

	has(key): has方法返回一个布尔值，表示某个键是否在Map数据结构中

	delete(key): delete方法删除某个键，返回true。如果删除失败，返回false

	clear(): clear方法清除所有成员，没有返回值




[slide]
#Map  {:&.flexbox.vleft}
遍历方法:

	keys()：返回键名的遍历器

	values()：返回键值的遍历器

	entries()：返回所有成员的遍历器

	forEach()：遍历Map的所有成员




[slide]
#WeakMap {:&.flexbox.vleft}

WeakMap只接受对象作为键名（null除外），不接受其他类型的值作为键名，而且键名所指向的对象，不计入垃圾回收机制






[slide]
#WeakMap与Map {:&.flexbox.vleft}

WeakMap与Map在API上的区别主要是两个: 

1、没有遍历操作，也没有size属性；

2、无法清空，即不支持clear方法，只有get()、set()、has()、delete()方法




[slide]
#WeakMap {:&.flexbox.vleft}
主要用途:

1、WeakMap应用的典型场合就是DOM节点作为键名

2、部署私有属性





[slide]

#与其他数据解构的互相转换一 {:&.flexbox.vleft}

Map转为数组

	Map转为数组最方便的方法，就是使用扩展运算符(...)

```javascript
let myMap = new Map().set(true, 7).set({foo: 3}, ['abc']);
[...myMap]
// [ [ true, 7 ], [ { foo: 3 }, [ 'abc' ] ] ]
```





[slide]

#与其他数据解构的互相转换二 {:&.flexbox.vleft}

数组转为Map

	将数组转入Map构造函数，就可以转为Map

```javascript
new Map([[true, 7], [{foo: 3}, ['abc']]])
// Map {true => 7, Object {foo: 3} => ['abc']}
```



[slide]

#与其他数据解构的互相转换三 {:&.flexbox.vleft}
Map转为对象

	如果所有Map的键都是字符串，它可以转为对象

```javascript
function strMapToObj(strMap) {
  let obj = Object.create(null);
  for (let [k,v] of strMap) {
    obj[k] = v;
  }
  return obj;
}

let myMap = new Map().set('yes', true).set('no', false);
strMapToObj(myMap)
// { yes: true, no: false }
```	




[slide]

#与其他数据解构的互相转换四 {:&.flexbox.vleft}

对象转为Map

```javascript
function objToStrMap(obj) {
  let strMap = new Map();
  for (let k of Object.keys(obj)) {
    strMap.set(k, obj[k]);
  }
  return strMap;
}

objToStrMap({yes: true, no: false})
// [ [ 'yes', true ], [ 'no', false ] ]
```






[slide]

#与其他数据解构的互相转换五 {:&.flexbox.vleft}

Map转为JSON

	Map的键名都是字符串，这时可以选择转为对象JSON

```javascript
function strMapToJson(strMap) {
  return JSON.stringify(strMapToObj(strMap));
}

let myMap = new Map().set('yes', true).set('no', false);
strMapToJson(myMap)
// '{"yes":true,"no":false}'
```

Map的键名有非字符串，这时可以选择转为数组JSON

```javascript
function mapToArrayJson(map) {
  return JSON.stringify([...map]);
}

let myMap = new Map().set(true, 7).set({foo: 3}, ['abc']);
mapToArrayJson(myMap)
// '[[true,7],[{"foo":3},["abc"]]]'
```





[slide]

#与其他数据解构的互相转换六 {:&.flexbox.vleft}

JSON转为Map

	JSON转为Map，正常情况下，所有键名都是字符串

```javascript
function jsonToStrMap(jsonStr) {
  return objToStrMap(JSON.parse(jsonStr));
}

jsonToStrMap('{"yes":true,"no":false}')
// Map {'yes' => true, 'no' => false}
```

	有一种特殊情况，整个JSON就是一个数组，且每个数组成员本身，又是一个有两个成员的数组。这时，它可以一一对应地转为Map。这往往是数组转为JSON的逆操作

```javascript
function jsonToMap(jsonStr) {
  return new Map(JSON.parse(jsonStr));
}

jsonToMap('[[true,7],[{"foo":3},["abc"]]]')
// Map {true => 7, Object {foo: 3} => ['abc']}
```
