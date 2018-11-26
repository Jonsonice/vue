v-if
v-if是条件渲染指令，它根据表达式的真假来删除和插入元素，它的基本语法如下：v-if="expression",expression是一个返回bool值的表达式，表达式可以是一个bool属性，也可以是一个返回bool的运算式.
注意：yes, no, age, name这4个变量都来源于Vue实例选项对象的data属性。

这段代码使用了4个表达式：

数据的yes属性为true，所以"Yes!"会被输出；
数据的no属性为false，所以"No!"不会被输出；
运算式age >= 25返回true，所以"Age: 28"会被输出；
运算式name.indexOf('jack') >= 0返回false，所以"Name: keepfool"不会被输出。
注意：v-if指令是根据条件表达式的值来执行元素的插入或者删除行为。

这一点可以从渲染的HTML源代码看出来，面上只渲染了3个<h1>元素，v-if值为false的<h1>元素没有渲染到HTML。

为了再次验证这一点，可以在Chrome控制台更改age属性，使得表达式age >= 25的值为false，可以看到<h1>Age: 28</h1>元素被删除了。

age是定义在选项对象的data属性中的，为什么Vue实例可以直接访问它呢？
这是因为每个Vue实例都会代理其选项对象里的data属性。

v-show指令
v-show也是条件渲染指令，和v-if指令不同的是，使用v-show指令的元素始终会被渲染到HTML，它只是简单地为元素设置CSS的style属性。
在Chrome控制台更改age属性，使得表达式age >= 25的值为false，可以看到<h1>Age: 24</h1>元素被设置了style="display:none"样式。

v-else指令
可以用v-else指令为v-if或v-show添加一个“else块”。v-else元素必须立即跟在v-if或v-show元素的后面——否则它不能被识别。
v-else元素是否渲染在HTML中，取决于前面使用的是v-if还是v-show指令。
这段代码中v-if为true，后面的v-else不会渲染到HTML；v-show为tue，但是后面的v-else仍然渲染到HTML了。

v-for指令
v-for指令基于一个数组渲染一个列表，它和JavaScript的遍历语法相似：
v-for="item in items"
items是一个数组，item是当前被遍历的数组元素。
我们在选项对象的data属性中定义了一个people数组，然后在#app元素内使用v-for遍历people数组，输出每个person对象的姓名、年龄和性别。

v-bind指令
v-bind指令可以在其名称后面带一个参数，中间放一个冒号隔开，这个参数通常是HTML元素的特性（attribute），例如：v-bind:class
v-bind:argument="expression"
下面这段代码构建了一个简单的分页条，v-bind指令作用于元素的class特性上。
这个指令包含一个表达式，表达式的含义是：高亮当前页。
注意v-for="n in pageCount"这行代码，pageCount是一个整数，遍历时n从0开始，然后遍历到pageCount –1结束。

v-on指令
v-on指令用于给监听DOM事件，它的用语法和v-bind是类似的，例如监听<a>元素的点击事件：
<a v-on:click="doSomething">
有两种形式调用方法：绑定一个方法（让事件指向方法的引用），或者使用内联语句。
Greet按钮将它的单击事件直接绑定到greet()方法，而Hi按钮则是调用say()方法。

v-bind和v-on的缩写
Vue.js为最常用的两个指令v-bind和v-on提供了缩写方式。v-bind指令可以缩写为一个冒号，v-on指令可以缩写为@符号。

<!--完整语法-->
<a href="javascripit:void(0)" v-bind:class="activeNumber === n + 1 ? 'active' : ''">{{ n + 1 }}</a>
<!--缩写语法-->
<a href="javascripit:void(0)" :class="activeNumber=== n + 1 ? 'active' : ''">{{ n + 1 }}</a>
<!--完整语法-->
<button v-on:click="greet">Greet</button>
<!--缩写语法-->
<button @click="greet">Greet</button>