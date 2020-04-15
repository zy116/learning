### JS基础

#### 1. 简介

``` 
JavaScript由三部分组成 ECMAScript，DOM，BOM
ECMAScript：语言的语法及对象
DOM：文档对象模型，处理网页内容的方法和接口
BOM：浏览器对象模型，与浏览器交互的方法和接口
```

#### 2. 语法

```
1. 不是用var声明的变量函数，都是全局的
2. 闭包，在其他区域可以使用某个函数里的变量，函数等
3. 冒泡：由于一个DOM对象被触发时，所产生的事件会从文档根节点流向目标(捕获阶段)途径各节点进行捕获各节	  	 点，到达目标对象时事件被触发，触发之后会流回根节点，对路径上的各节点触发事件。
例：document.getElementById("ul").onclick.addEventListener("click",function(e){
	if(e.target&&e.target.nodeName.toUpperCase=="LI")
		alert(e.target.innerText)
},false) 其中false是不进行冒泡，点击某个li时，只对整个ul中的这个li执行事件。
4. typeof null / typeof object 返回object
```

####  3. 数组

1. JavaScript中的数组里面的元素类型可以不一致。构建新数组 直接var x =[1,2,3],注意是[]
2. 数组可以在末尾直接添加元素，即数组长度是动态的，使用如`push("qq")`添加，**push返回的是新数组长度**
   shift是删除首个，unshift是添加首个，清空数组直接`x.length=0`即可
3. `var arr = new Array("qq","www")`  但是不要使用这个形式，直接用`["qq","www"]`更好，并且直接打印arr得到的是整个数组
4. arr.sort()里要写比值函数，`arr.sort(function(a,b){return a-b;})`这样就是排成递增
5. **数组的方法**
   1. splice
   2. 
6. 迭代：这三个方法都是执行括号里的函数
   (1) arr.forEach()对每个元素执行括号内的函数，不会对数组本身造成改变，所以用text连接输出
   	forEach()使用：`forEach(function(element,index,array){})`
   	                第一个参数是x 第二个是索引 第三个是数组
   (2) arr.map()对每个元素执行函数，来创建一个新数组进行迭代，原数组不会改变，输出新数组
   (3) arr.filter()对所有元素进行筛选，将其迭代，所以函数通常是筛选函数

#### 4. 函数

``` 
JavaScript里函数的命名是function getsum()，没有返回值类型，可以var x =getsum()
方法可以不写形参，所以实参可以随便传几个，且形参可以是一个语句及函数，argument可以统计形参，类似于数组，argument[0]第一个形参，所以没有重载，只能模拟
匿名函数，var x =getsum(){函数体}
自调用函数，;(function(){函数体})() 前面加;号
function也有数据类型，var fn=fun(){} ，console.log(typeof fn)是function，所以fn就指向了这个函数，可以打印出来，打印结果是整个函数
函数也可以作为参数传递，并在调用函数里使用，test(fun){fun()} test(fn);
函数还可以作为返回值类型，如在方法里return出去一个方法，这个方法返回的也就是一个方法
函数带括号引用的是函数的返回值，不带括号返回的是函数的整个代码
apply()函数和call()函数：都是由函数调用，它接收两个参数，第一个参数就是需要绑定的this变量，可以用于指定对象，第二个参数是Array，表示函数本身的参数，即调用函数的参数。
回调函数：函数作为参数
```

``` 
console.log(a,b,c)打印a,b,c
在方法里面出现var a=b=c=9;那么a是局部变量，b,c是全局变量
```

#### 5. 预解析

``` 
JavaScript里有预解析功能，就是在一个作用域里，先对变量和函数进行声明，执行代码按照从上到下依次跟在下面，比如赋值操作跟调用函数操作，注意：每个作用域都得进行预解析，在函数内部也要
如果变量与函数名相同，函数名优先，就是比如console(a) a预解析了，有函数跟变量，打印的是函数
注：=== 是类型和值完全一样
```

#### 6. 对象

```
1. 声明 var student={
		name:'lia'，
		"grade":{
		math:76
		}
		fun:function(){}
	}主要注意不是等号，且方法名也是冒号表示  
2. 调用对象的另一个方式，把对象当成一个数组，console(student['name'])，方法名用''表示
3. 创建对象的方式 function Hero(name,age){
		this.name=name;
		this.age=age;
}注意：相当于带参构造
4. for(var i in person)的用法，i代表的是person里的各个属性，如i=name;还可以在forin中继续加循环，如grade也是一个对象，有第二层循环，math的获取方式：person[i][j]，这个只能用于类数组，每个格式都是一样的

```

#### 7. 字符串

```
所有的字符串方法都是返回一个新字符串，不会改变原字符串。
split(",") 将字符串分割成一个数组 字符串中，为分割处1,2,3分割为 [1][2][3]
字符串与数字相加，数字转换成字符串。字符串与数字比较，字符串转换成数字。两个字符串数字比较，比较的是字符串第一个的ascii码大小,如"2">"12"
slice(2,4) 从2到4剪切，可以接受负索引
subString(2,4)从2到4剪切，不能接受负索引
substr(2,4) 从2开始剪长度为4的
```

#### 8. 数值

```
Number() 用于其他类型的转成数值类型  parseInt()同理
constructor返回变量或对象的属性，如person.constuctor()就是object

```

#### 9. 冒泡与捕获

给父子元素创建事件的时候，点击子元素，父元素也会产生事件。

事件的发生存在着两个阶段，捕获阶段与冒泡阶段，顺序：从父元素捕获到触发元素，再从触发元素冒泡到最父级

在添加监听事件时可以通过最后一个参数设置true或false来设置此元素的时间发生在什么阶段，默认是false，事件冒泡。

~~~
关系：b1>b2>b3 b3是内层元素
document.getElementById("b1").addEventListener("click", function () {
    alert("b1")
},true) //b1事件发生在事件捕获阶段，触发子元素事件之前先触发此元素
document.getElementById("b2").addEventListener("click", function () {
    alert("b2")
},false)//b2事件发生在冒泡阶段，触发完子元素之后触发
document.getElementById("b3").addEventListener("click", function () {
    alert("b3")
})

如点击b3，弹出顺序：b1，b3，b2
~~~

捕获阶段：比如点击子元素，从父元素一级一级向下，捕获到这个子元素的过程。

冒泡阶段：子元素事件发生后，再从点击元素一层层往上触发

#### 10. 跨域

```
javascript中实现跨域的方式总结
第一种方式：jsonp请求；jsonp的原理是利用<script>标签的跨域特性，可以不受限制地从其他域中加载资源，类似的标签还有<img>.	
第二种方式：document.domain；这种方式用在主域名相同子域名不同的跨域访问中
第三种方式：window.name；window的name属性有个特征：在一个窗口(window)的生命周期内,窗口载入的所有的页面都是共享一个window.name的，每个页面对window.name都有读写的权限，window.name是持久存在一个窗口载入过的所有页面中的，并不会因新页面的载入而进行重置。
第四种方式：window.postMessage；window.postMessages是html5中实现跨域访问的一种新方式，可以使用它来向其它的window对象发送消息，无论这个window对象是属于同源或不同源。
第五种方式：CORS；CORS背后的基本思想，就是使用自定义的HTTP头部让浏览器与服务器进行沟通，从而决定请求或响应是应该成功还是应该失败。
第六种方式：Web Sockets；web sockets原理：在JS创建了web socket之后，会有一个HTTP请求发送到浏览器以发起连接。取得服务器响应后，建立的连接会使用HTTP升级从HTTP协议交换为web sockt协议。
```



#### 11. 原型



### JSON

~~~
是一种数据交换格式，JavaScript object notation  
用于把对象变成字符串，字符串变回对象。
JSON.stringify(object,array,format) 第一个对象名，第二个想要输出的对象属性，第三个缩进格式。
toJSON方法：在对象中添加toJSON:function(){},调用stringify方法时，返回这个方法里的内容。
JSON.parse()将字符串转变成对象
~~~

### AJAX

~~~ 
ajax：异步JavaScript和xml
创建xhr对象，var xhr = new XMLHttpRequest();
xhr方法:responseText 接收服务器非xml的响应。 responseXML 
onreadystatechange方法:
用法
xmlhttp.onreadystatechange=function()
{
    if (xmlhttp.readyState==4 && xmlhttp.status==200)
    {
        document.getElementById("myDiv").innerHTML=xmlhttp.responseText;
    }
}
~~~

### jQuery

~~~
一个JavaScript代码库，具有很多简化的接口，更方便，实质就是一个js文件，引用一下即可。
我下载在了develop里
~~~

### ES5



### ES6

ECMAScript第六个版本，2015年发布 ie11及以下的不支持

#### 1. let和const

1. var声明的变量是全局变量，被声明之后，全局都可以使用，并且统一变化  

​      **注意**：在函数内var声明的变量，函数使用结束后就被销毁

​				块级作用域不是函数作用域，`if(){块级} `    `function(){函数}`

2. **暂时性死区**：只要在块级作用域声明了let变量，它所声明的变量就绑定在了这个作用域，只能先声明后使用

   ~~~
   var tmp = 123;
   
   if (true) {
     tmp = 'abc'; // ReferenceError
     let tmp;
   } //此时虽然有全局变量tmp，但是在块级作用域里，有let声明，所以要遵循let规则
   ~~~

3. 不允许重复声明

   在同一作用域内，不能let重复声明一个变量

   ~~~
   function func(arg) {
     let arg;
   }
   func() // 报错
   
   function func(arg) {
     {
       let arg;
     }
   }
   func() // 不报错
   ~~~

4. 变量提升

   es5只存在函数作用域和全局作用域，会存在内层重复声明的变量覆盖外层的

   ~~~
   var tmp = new Date();
   
   function f() {
     console.log(tmp);
     if (false) {
     //此处声明的tmp会被提升到外部，所以打印出来是undefined
       var tmp = 'hello world';
     }  
   }
   
   f(); // undefined
   ~~~

5. 块级作用域

   外层无法读取到内层的变量，内层可以重复定义外层的变量，所以用自调用函数进行封装私有变量可以不必要

   ~~~
   function f() {
           let x =0;
           {
               let x =9;
               console.log(x); 
           }
           console.log(x);
       }
       f(); // 9   0
   ~~~

   es6中块级作用域必须要有大括号，let声明只能出现在当前作用域的顶层

   ~~~
   if (true) let x = 1; //报错 
   ~~~

6. const

   const声明一个只读的常量，并且声明时必须初始化值，也不提升变量，暂时性死区，块级作用域生效

   **本质**：const保证的不是变量不能变化，指的是变量指向的那个地址保存的数据不会变化，对于基本数据类型，变量指向的是内存地址，数值就存储在这个地址，对于引用类型，变量指向的是一个地址指针

   ~~~
   const foo = {};
   
   // 为 foo 添加一个属性，可以成功
   foo.prop = 123;
   foo.prop // 123
   
   // 将 foo 指向另一个对象，就会报错，即，const的变量的指向是不能变化的，但是变量内部的值可以变化
   foo = {}; // TypeError: "foo" is read-only
   ~~~

   **注意**：`object.freeze`:将一个对象进行冻结，对象不能进行更改，`const foo = Object.freeze({});`

   此时foo不能进行添加属性等

   顶层对象

   在浏览器中顶层对象指window对象，在es5中，顶层对象与全局变量是等价的，在es6，let全局变量不是顶层变量

   ~~~
   var a = 1;
   // 如果在 Node 的 REPL 环境，可以写成 global.a
   // 或者采用通用方法，写成 this.a
   window.a // 1
   
   let b = 1;
   window.b // undefined
   ~~~

#### 2. 变量的解构赋值（后续进行补充）

1. es6允许以下赋值方式

   ~~~
   let [a, b, c] = [1, 2, 3];
   ~~~

#### 3. 字符串的扩展（后续补充）

#### 4. 字符串的新增方法（后续补充）

#### 5. 正则的扩展（后续补充）

#### 6. 数值的扩展（后续补充）

#### 7. 函数的扩展（后续补充）

#### 8. 数组的扩展（后续补充）

1. 扩展运算符`...`：该运算符可以将一个数组转成一个参数序列

   ~~~
   function f(v, w, x, y, z) { }
   const args = [0, 1];
   f(-1, ...args, 2, ...[3]);  //等于f(-1,0,1,2,3)
   
   // ES5的 写法
   var arr1 = [0, 1, 2];
   var arr2 = [3, 4, 5];
   Array.prototype.push.apply(arr1, arr2);//push不能添加一个数组
   
   // ES6 的写法
   let arr1 = [0, 1, 2];
   let arr2 = [3, 4, 5];
   arr1.push(...arr2);
   ~~~

   

#### 9. 对象的扩展

1. 属性简洁写法，直接在大括号里写入变量或函数

   如下：属性名就是变量名, 属性值就是变量值。

   ~~~
   function f(x, y) {
     return {x, y};   //等同于return {x:x,y:y}
   }
   f(1, 2) // Object {x: 1, y: 2}
   
   const o = {
     method() {   // 等同于method:function
       return "Hello!";
     }
   };
   ~~~

2. 属性的遍历

   es6遍历对象有5种方法

   1. for in

#### 10.对象的新增方法（后续补充）

#### 11.Symbol

**symbol是第七种数据类型**。es5中的对象属性名都是字符串，如foos，如果给对象添加属性，容易重复命名错误，symbol就可以保证每个名字独一无二。

1. symbo的用法

   **参数是对于symbo变量的描述，无实际含义**

   ~~~
   let s = Symbol();或者let s1 = Symbol('foo');
   s  //Symbol()  s1   //Symbol(foo)
   s==s1  //false
   let s2 = Symbol('foo')
   s1==s2 // false 即使是同一参数，依旧不相等
   ~~~

   symbol变量不能与其他类型变量进行运算，拼接等，但是可以转成字符串`s.toString()`，也可以转成bool

   ~~~
   let s = Symbol();
   console.log(Boolean(s))  // true
   console.log(!s)   //false
   ~~~

2. Symbol.prototype.description

   由于对于symbol的描述的读取不是很方便，需要显式转换成字符串，即`s.toString()`，所以提供了`description`方法

   ~~~
   const sym = Symbol('foo');
   sym.description // "foo"
   ~~~

3. 作为属性名的symbol（属性名的唯一，以防添加覆盖）

   说明：不能使用点运算符，因为点后面跟的默认是字符串属性名，就不是symbol类型了

   ~~~
   let sym = Symbol();
   let a = {
   [sym]:"hello"
   }
   console.log(a[sym])
   ~~~

4. （后续补充）

#### 11. set和map数据结构

##### 1. set

1. 用法：set是一个构造函数，可以传入数组，字符串，去重，`set的去重机制是===`

   注：[…x]可以返回一个数组，x可以是set

   ~~~
   const s = new Set([1,2,3,2,34,5,2,3,5]);
   console.log(s)// Set(5) {1, 2, 3, 34, 5}
   console.log([...arr])//[1, 23, 4, 2, 52, 25]
   ~~~

2. set的方法

   - `Set.prototype.constructor`：构造函数，默认就是`Set`函数。
   - `Set.prototype.size`：返回`Set`实例的成员总数。

   Set 实例的方法分为两大类：操作方法（用于操作数据）和遍历方法（用于遍历成员）。

   操作方法：

   - `Set.prototype.add(value)`：添加某个值，返回 Set 结构本身。
   - `Set.prototype.delete(value)`：删除某个值，返回一个布尔值，表示删除是否成功。
   - `Set.prototype.has(value)`：返回一个布尔值，表示该值是否为`Set`的成员。
   - `Set.prototype.clear()`：清除所有成员，没有返回值。

   遍历方法：

   以下中，key和values都是一个值，所以返回都是一样的，entries返回键值对也是两个一样的值

   - `Set.prototype.keys()`：返回键名的遍历器
   - `Set.prototype.values()`：返回键值的遍历器
   - `Set.prototype.entries()`：返回键值对的遍历器
   - `Set.prototype.forEach()`：使用回调函数遍历每个成员

3. （后续补充）

##### 2. map

键值对的数据结构，object也是键值对，但是object的键名只能是字符串

- 2. 1map的使用

  不仅仅是数组，任何具有 Iterator 接口、且每个成员都是一个双元素的数组的数据结构，都可以当作`Map`构造函数的参数，如set也可以

  - 数组作为参数

    ~~~
    const map = new Map([
      ['name', '张三'],
      ['title', 'Author']
    ]);
    
    等价于
    const items = [
      ['name', '张三'],
      ['title', 'Author']
    ];
    
    const map = new Map();
    
    items.forEach(
      ([key, value]) => map.set(key, value)
    );
    ~~~

  - set作为参数

    ~~~
    const sets = new Set([
         ['foo',1],
         ['bar',2]
     ])
    
     const map = new Map(sets);
     console.log(map)  //Map(2) {"foo" => 1, "bar" => 2}
    ~~~

  **注意**：存储的键是一个地址，就算值一样，只要不是同一个引用，就是不同的键。

  ~~~
  const map = new Map();
  
  //计算键的值是一样的
  const k1 = ['a'];
  const k2 = ['a'];
  
  map
  .set(k1, 111)
  .set(k2, 222);
  
  map.get(k1) // 111
  map.get(k2) // 222
  ~~~

- 2. 2 map的操作和方法

  **（1）size 属性**

  `size`属性返回 Map 结构的成员总数。

  ```javascript
  const map = new Map();
  map.set('foo', true);
  map.set('bar', false);
  
  map.size // 2
  ```

  **（2）Map.prototype.set(key, value)**

  `set`方法设置键名`key`对应的键值为`value`，然后返回整个 Map 结构。如果`key`已经有值，则键值会被更新，否则就新生成该键。

  ```javascript
  const m = new Map();
  
  m.set('edition', 6)        // 键是字符串
  m.set(262, 'standard')     // 键是数值
  m.set(undefined, 'nah')    // 键是 undefined
  ```

  `set`方法返回的是当前的`Map`对象，因此可以采用链式写法。

  ```javascript
  let map = new Map()
    .set(1, 'a')
    .set(2, 'b')
    .set(3, 'c');
  ```

  **（3）Map.prototype.get(key)**

  `get`方法读取`key`对应的键值，如果找不到`key`，返回`undefined`。

  ```javascript
  const m = new Map();
  
  const hello = function() {console.log('hello');};
  m.set(hello, 'Hello ES6!') // 键是函数
  
  m.get(hello)  // Hello ES6!
  ```

  **（4）Map.prototype.has(key)**

  `has`方法返回一个布尔值，表示某个键是否在当前 Map 对象之中。

  ```javascript
  const m = new Map();
  
  m.set('edition', 6);
  m.set(262, 'standard');
  m.set(undefined, 'nah');
  
  m.has('edition')     // true
  m.has('years')       // false
  m.has(262)           // true
  m.has(undefined)     // true
  ```

  **（5）Map.prototype.delete(key)**

  `delete`方法删除某个**键**，返回`true`。如果删除失败，返回`false`。

  ```javascript
  const m = new Map();
  m.set(undefined, 'nah');
  m.has(undefined)     // true
  
  m.delete(undefined)
  m.has(undefined)       // false
  ```

  **（6）Map.prototype.clear()**

  `clear`方法清除所有成员，没有返回值。

  ```javascript
  let map = new Map();
  map.set('foo', true);
  map.set('bar', false);
  
  map.size // 2
  map.clear()
  map.size // 0
  ```

  map的遍历方法

  - `Map.prototype.keys()`：返回键名的遍历器。
  - `Map.prototype.values()`：返回键值的遍历器。
  - `Map.prototype.entries()`：返回所有成员的遍历器。
  - `Map.prototype.forEach()`：遍历 Map 的所有成员。