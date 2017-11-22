# JS里的数据

- JS的历史
- 数据类型

## JS的历史

|  年份   | 大事记                                      |
| :---: | ---------------------------------------- |
| 1990年 | 李爵士（Tim Berners-Lee）发明了万维网（World Wide Web） |
| 1992年 | 美国国家超级电脑应用中心（NCSA）开始开发一个独立的浏览器，叫做Mosaic。这是人类历史上第一个浏览器。 |
| 1994年 | Netscape公司在Mosaic基础上开发面向普通用户的新一代的浏览器Netscape Navigator，年底Navigator发布了1.0版，市场份额一举超过90%。 |
| 1995年 | Netscape公司雇佣程序员Brendan Eich开发这种网页脚本语言，后者只用了10天，就设计完成了这种语言的第一版，命名Mocha。9月，改名为LiveScript。12月4日，Netscape公司与Sun公司联合发布了JavaScript语言。 |
| 1996年 | 3月，Navigator 2.0浏览器正式内置了JavaScript脚本语言。8月，微软模仿JavaScript开发了一种相近的语言，取名为JScript。11月，Netscape公司决定将JavaScript提交给国际标准化组织ECMA（European Computer Manufacturers Association），希望JavaScript能够成为国际标准，以此抵抗微软。 |
| 1997年 | 7月，ECMA组织发布262号标准文件（ECMA-262）的第一版，规定了浏览器脚本语言的标准，并将这种语言称为ECMAScript。ECMA-262标准后来也被另一个国际标准化组织ISO（International Organization forStandardization）批准，标准号是ISO-16262。 |
| 1998年 | 6月，ECMAScript 2.0版发布。                    |
| 1999年 | 12月，ECMAScript 3.0版发布，成为JavaScript的通行标准，得到了广泛支持。 |
| 2007年 | 10月，ECMAScript 4.0版草案发布，对3.0版做了大幅升级，预计次年8月发布正式版本。草案发布后，由于4.0版的目标过于激进，各方对于是否通过这个标准，发生了严重分歧。 |
| 2008年 | 7月，由于4.0版本分歧过大，ECMA开会决定，中止ECMAScript 4.0的开发（即废除了这个版本）。 |
| 2009年 | 12月，ECMAScript 5.0版正式发布。                 |
| 2011年 | 6月，ECMAscript 5.1版发布，并且成为ISO国际标准（ISO/IEC 16262:2011）。 年底，所有主要浏览器都支持ECMAScript 5.1版的全部功能。 |
| 2015年 | 6月，ECMAScript 6正式发布，并且更名为“ECMAScript 2015”。这是因为TC39委员会计划，以后每年发布一个ECMAScirpt的版本。 |
| 2016年 | 6月，ECMAScript 2016（ECMAScript 7）发布。      |
| 2017年 | 6月，ECMAScript 2017（ECMAScript 8）发布。      |

[ES.Next](https://en.wikipedia.org/wiki/ECMAScript)
ES.Next is a dynamic name that refers to whatever the next version is at time of writing. ES.Next features are more correctly called proposals, because, by definition, the specification has not been finalized yet.



## 数据类型

JS中有7种数据类型(不区分大小写)： 

简单类型：数值(number)、 字符串(string)、布尔(boolean)、 symbol、 null、 undefiend；

复杂类型：对象(object)。  

### 数值(number)

```
十进制：1 1.1 .1 1.23e2  

二进制：0b11  

八进制：011  注意0开头  

十六进制：0x11
```

### 字符串(string)

```
'你好'， "你好"，  ''  "， " ' ' "
```

```
转义 
表示的string就是'时, var a="'"    
表示的string是'"时, var a='\'"'

\转义符 \n回车 \t制表符 \不占长度

多行字符串
var s1 = '12345\
6789'   s1.length = 9
var s2 = '123' + '456' [推荐]
var s3 = `123
456` s3.length = 7(包含回车）   ES6新特性
```

### 布尔(boolean)

```
布尔 boolean  人名，数学家，
逻辑学
true 真 
false 假
&&与运算 ||--或运算 
```

除了下面六个值被转为**false**，其他值转换时都视为**true**。

```
- undefined
- null
- false
- 0
- NaN
- ""或''（空字符串）
```

### symbol

search key: symbol 方应杭

### null类型 和 undefined类型

两者都表示什么也没有（JS的bug）  

1. 变量没有值 -- undefined。（语法）
2. 有一个对象object,现在不想给值 -- null;有一个非对象,不想给值 -- undefined。（惯例）

### 对象(object )

对象就是简单类型的组合,哈希表{key:value,}

```
person['key'] --> 单引号不能省略
key: 
  'a  b' '9a' [成立]  
   9a [不成立] 
```

```
  var person = {
      name: 'Frank', 
      'child': {
          name: 'Jack'
      }, // 最后这个逗号可有可无
  }
```

- object 的 key 一律是字符串，不存在其他类型的 key
- object[''] 是合法的
- object['key'] 可以写作 object.key
- 注意 object.key 与 `object[key]` 不同
- delete object['key']
- 'key' in objec

### typeof 操作符

| xxx 的类型    | string   | number   | boolean   | symbol   | undefined   | null         | object   | function   |
| ---------- | -------- | -------- | --------- | -------- | ----------- | ------------ | -------- | ---------- |
| typeof xxx | 'string' | 'number' | 'boolean' | 'symbol' | 'undefined' | **'object'** | 'object' | 'function' |

注意: function 并不是一个类型。



> 资料参考:
>
> [JavaScript 标准参考教程-阮一峰](http://javascript.ruanyifeng.com/)
>
> [JS里的数据-写代码啦](https://xiedaimala.com/courses/ec3a5e28-02da-47d6-9226-927db23e82a2/tasks/0a86dfb0-a8c5-49c6-a066-7704d19ee0d2)   
>
> 扩展阅读：
>
> [ES 5 新增特性汇总-方应杭](https://zhuanlan.zhihu.com/p/24336831)