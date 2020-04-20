### 1. 实例

当一个 Vue 实例被创建时，它将 `data` 对象中的所有的属性加入到 Vue 的**响应式系统**中。当这些属性的值发生改变时，视图将会产生“响应”，即匹配更新为新的值。
	// 我们的数据对象
	var data = { a: 1 }
	
	// 该对象被加入到一个 Vue 实例中
	var vm = new Vue({
	  data: data
	})
	
	// 获得这个实例上的属性
	// 返回源数据中对应的字段
	vm.a == data.a // => true
	
	// 设置属性也会影响到原始数据
	vm.a = 2
	data.a // => 2
	
	// ……反之亦然
	data.a = 3
	vm.a // => 3
当数据改变时视图会进行重新渲染，但是只能是实例被创建的时候已有的属性才是响应式的，新增的属性不具备实时更新

~~~
vm.b = 'hi' //不触发视图更新
~~~

### 2. 生命周期![Vue 实例生命周期](https://cn.vuejs.org/images/lifecycle.png)

每个 Vue 实例在被创建时都要经过一系列的初始化过程。同时在这个过程中也会运行一些叫做**生命周期钩子**的函数，这给了用户在不同阶段添加自己的代码的机会。生命周期钩子的 `this` 上下文指向调用它的 Vue 实例。

~~~
new Vue({
        el: "#fa",
        data: {
            a: 1
        },
        created: function () {
            // `this` 指向 vm 实例
            console.log('a is: ' + this.a) //a is :1
        }
    })
~~~

不要在选项属性或回调上使用箭头函数比如 `created: () => console.log(this.a)` 或 `vm.$watch('a', newValue => this.myMethod())`，因为箭头函数没有this。

 vue每个组件都是独立的，每个组件都有一个属于它的生命周期，从一个组件**创建、数据初始化、挂载、更新、销毁**，这就是一个组件所谓的生命周期。

- create：意思就是创建这个实例。beforeCreate：此时vue对象还未初始化，created：此时vue对象初始化完成，但是没有绑定到数据上去,但是vue对象已经初始化好。

~~~
var vm = new Vue({
        el: '#app',
        data: {
            message: 'Vue的生命周期'
        },
        beforeCreate: function() {
            console.group('------beforeCreate创建前状态------');
            console.log("%c%s", "color:red" , "el     : " + this.$el); //undefined
            console.log("%c%s", "color:red","data   : " + this.$data); //undefined
            console.log("%c%s", "color:red","message: " + this.message)
        },
        created: function() {
            console.group('------created创建完毕状态------');
            console.log("%c%s", "color:red","el     : " + this.$el); //undefined
            console.log("%c%s", "color:red","data   : " + this.$data); //已被初始化
            console.log("%c%s", "color:red","message: " + this.message); //已被初始化
        },
        beforeMount: function() {
            console.group('------beforeMount挂载前状态------');
            console.log("%c%s", "color:red","el     : " + (this.$el)); //已被初始化
            console.log(this.$el);
            console.log("%c%s", "color:red","data   : " + this.$data); //已被初始化
            console.log("%c%s", "color:red","message: " + this.message); //已被初始化
        },
        mounted: function() {
            console.group('------mounted 挂载结束状态------');
            console.log("%c%s", "color:red","el     : " + this.$el); //已被初始化
            console.log(this.$el);
            console.log("%c%s", "color:red","data   : " + this.$data); //已被初始化
            console.log("%c%s", "color:red","message: " + this.message); //已被初始化
        },
        beforeUpdate: function () {
            console.group('beforeUpdate 更新前状态===============》');
            console.log("%c%s", "color:red","el     : " + this.$el);
            console.log(this.$el);
            console.log("%c%s", "color:red","data   : " + this.$data);
            console.log("%c%s", "color:red","message: " + this.message);
        },
        updated: function () {
            console.group('updated 更新完成状态===============》');
            console.log("%c%s", "color:red","el     : " + this.$el);
            console.log(this.$el);
            console.log("%c%s", "color:red","data   : " + this.$data);
            console.log("%c%s", "color:red","message: " + this.message);
        },
        beforeDestroy: function () {
            console.group('beforeDestroy 销毁前状态===============》');
            console.log("%c%s", "color:red","el     : " + this.$el);
            console.log(this.$el);
            console.log("%c%s", "color:red","data   : " + this.$data);
            console.log("%c%s", "color:red","message: " + this.message);
        },
        destroyed: function () {
            console.group('destroyed 销毁完成状态===============》');
            console.log("%c%s", "color:red","el     : " + this.$el);
            console.log(this.$el);
            console.log("%c%s", "color:red","data   : " + this.$data);
            console.log("%c%s", "color:red","message: " + this.message)
        }
    })
~~~

- mount：意思是挂载上去。

  beforeMount之前，有一个过程：

  首先会判断对象是否有**el选项**。**如果有的话就继续向下编译，如果没有**el选项**，则停止编译，也就意味着停止了生命周期，直到在该vue实例上调用vm.$mount(el) -- el指的如#app。**

  然后，我们往下看，**template**参数选项的有无对生命周期的影响。
  （1）如果vue实例对象中有template参数选项，则将其作为模板编译成render函数。
  （2）如果没有template选项，则将外部HTML作为模板编译。
  （3）可以看到template中的模板优先级要高于outer HTML的优先级。

  所以**el的判断**要在template之前~是因为vue需要通过el找到对应的outer template，如果没有template才好讲外部HTML作为模板编译。同时在vue对象中还有一个**render函数**，它是以createElement作为参数，然后做渲染操作，而且我们可以直接嵌入JSX，所以综合排名优先级：

  **render函数选项 > template选项 > outer HTML**

  打印出来结果为`this is createElement`,注释掉render之后，打印结果`Vue的生命周期这是在template中的`

  ![img](file:///C:\Users\12864\AppData\Roaming\Tencent\Users\1296424171\QQ\WinTemp\RichOle\6_H8F9WNIPK4_@AX1FMOM8P.png)

  beforeMount函数之前，就经历了上述过程，此时el还未绑定元素，打印el结果是

  ![img](file:///C:\Users\12864\AppData\Roaming\Tencent\Users\1296424171\QQ\WinTemp\RichOle\JH4MUGPHH%P]%0KXRV}]`5W.png)

  mounted之后，已经绑定页面元素

  ![img](file:///C:\Users\12864\AppData\Roaming\Tencent\Users\1296424171\QQ\WinTemp\RichOle\K8B}YL~G3SR@%ROD4OBVASK.png)

- update:更新数据。

  **beforeupdate：**数据更新时调用，发生在虚拟 DOM 重新渲染和打补丁之前。 你可以在这个钩子中进一步地更改状态，这不会触发附加的重渲染过程。

  **updated：**当这个钩子被调用时，组件 DOM 已经更新，所以你现在可以执行依赖于 DOM 的操作。然而在大多数情况下，你应该避免在此期间更改状态，因为这可能会导致更新无限循环。

- destroy：销毁实例

  **beforeDestroy**：实例销毁之前调用。在这一步，实例仍然完全可用。

  **destroyed**：Vue 实例销毁后调用。调用后，Vue 实例指示的所有东西都会解绑定，所有的事件监听器会被移除，所有的子实例也会被销毁。 该钩子在服务器端渲染期间不被调用。

### 3.模板语法

Vue.js 使用了基于 HTML 的模板语法，允许开发者声明式地将 DOM 绑定至底层 Vue 实例的数据。所有 Vue.js 的模板都是合法的 HTML，所以能被遵循规范的浏览器和 HTML 解析器解析。在底层的实现上，Vue 将模板编译成虚拟 DOM 渲染函数。

#### 插值

- 文本

  数据绑定最常见的形式就是使用“Mustache”语法 (双大括号) 的文本插值：

  ~~~
  <span>Message: {{ msg }}</span>
  ~~~

  {{}}会将此处数据替换为实例对象msg的值，无论何时，绑定的对象的msg的值变化，此处值都会更新

  通过使用` v-once `指令，你也能执行一次性地插值，当数据改变时，插值处的内容不会更新。

  ~~~
  <span v-once>这个将不会改变: {{ msg }}</span>
  ~~~

- 原始HTML

  双大括号会将数据解释为普通文本，而非 HTML 代码。为了输出真正的 HTML，需要使用 `v-html` ：

  ~~~
  <p>Using mustaches: {{ rawHtml }}</p>
  <p>Using v-html directive: <span v-html="rawHtml"></span></p> 
  ~~~

  **注：**站点上动态渲染的任意 HTML 可能会非常危险，因为它很容易导致 XSS 攻击

- 属性

  Mustache 语法不能作用在 HTML attribute 上，遇到这种情况应该使用 `v-bind` ,此时绑定的值与设置的值一致

  ~~~
  <div v-bind:id="dynamicId"></div>
  ~~~

- JavaScript表达式

  实现JavaScript的表达式，但是只能包含单个表达式，不能包含语句

  ~~~
  {{ number + 1 }}
  ~~~

#### 指令

指令 (Directives) 是带有 `v-` 前缀的特殊 attribute。指令 attribute 的值预期是**单个 JavaScript 表达式** ，`v-for` 是例外情况。如`v-bind`等都是指令

### 4. 计算属性和监听器

#### 计算属性

我们可以将同一函数定义为一个方法而不是一个计算属性。两种方式的最终结果确实是完全相同的。然而，不同的是**计算属性是基于它们的响应式依赖进行缓存的**。只在相关响应式依赖发生改变时它们才会重新求值。这就意味着只要 `message` 还没有发生改变，多次访问 `reversedMessage` 计算属性会立即返回之前的计算结果，而不必再次执行函数。

计算属性有getter和setter，默认只有getter，读取数值，可以增加一个setter，可以改变依赖的值

~~~
computed: {
  fullName: {
    // getter
    get: function () {
      return this.firstName + ' ' + this.lastName
    },
    // setter
    set: function (newValue) {
      var names = newValue.split(' ')
      this.firstName = names[0]
      this.lastName = names[names.length - 1]
    }
  }
}
~~~

#### 侦听器

`watch`属性，监听某个数据，数据改变，运行内部的函数

### 5. class和style

#### 绑定HTML Class

