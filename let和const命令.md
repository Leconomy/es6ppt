title: let和const
speaker: 刘经济
transition: cards
files: /css/common.css

[slide]

# ESMAScript 6 之 let和const
## 演讲者：刘经济



[slide]
#let命令 {:&.flexbox.vleft}

1、只在当前块作用域有效

2、不存在变量的提升

3、存在暂时性死区

4、不可重复声明变量

5、形成块级作用域

注：暂时性死区:temporal dead zone，简称TDZ,一旦用let声明后，变量就绑定"binding"在此区域，不再受外部环境影响

[slide]
#const命令 {:&.flexbox.vleft}

1、声明常量，不可修改

2、声明必须立即赋值，不可留到以后赋值

3、只在声明的块级作用域内有效

4、不可重复声明

5、变量不会提升

6、存在暂时性死区

7、对于复合型数据，变量名不指向数据，而是指向数据的地址

const只是保证变量名指向的地址不变，并不保证该地址的数据不变
