`preventDefault() 阻止默认`



------

# Vue

# 一. 简介

## 1.1 什么是vue

用于构建用**户见界面**的**框架**

1 构建用户界面

- 用Vue往html页面中填充数据

2 框架

- 框架是一套现成的解决方案，程序员只能遵守框架的规则，去编写的自己的
- 要学习vue，就是在学习vue的框架的用法
- vue的指令、组件（是对ui结构的复用cv工程师）、路由Vuex、Vue组件库

## 1.2 vue的两个特性

1 数据驱动视图

- 数据的变化会**驱动视图**自动更新
- 单向的：页面依赖的数据变化→vue监听数据的变化→（自动渲染）→页面结构

2 双向数据绑定

> 在页面中，form表单负责**采集数据**，Ajax负责**提交数据**

- js数据的变化，会被自动渲染到页面上
- 页面上表单的数据发生变化时会被vue自动获取到，并更新到js数据中

## 1.3 MVVM

MVVM是Model-View-ViewModel的简写，实现数据驱动试图和双向数据绑定的 **核心原理（底层原理）**

![img](https://upload-images.jianshu.io/upload_images/26460997-bf9bb9152df90ab8.png?imageMogr2/auto-orient/strip|imageView2/2/w/1200/format/webp)

> 双向影响
>
> 注意：数据驱动视图和双向数据绑定的底层原理是MVVM（Mode 数据源、View 视图、ViewModel就是Vue示例,核心）

> 作者：尤雨溪



------

# 二. vue的基本使用

## 1.基本步骤

new Vue（）

① 导入vue.js的script脚本文件

```html
<script src="./vue.js"></script>
```

②在页面中声明一个将要被vue所控制的DOM区域

`若el指定了多个标签，只会控制第一个`

```
 el: '#app'
```

③创建vm实例对象（vue实例对象）

```html
<body>
    <!-- 被控制的div {{ }} 占位符，插值表达式，与Ajax中的模板引擎相似-->
    <div id="app">{{ username }}</div>


    <!-- 导入vue的库文件，在window全局九有了Vue这个构造函数 -->
    <script src="./vue.js"></script>
    <script>
        // 构建Vue的实例对象
        const vm = new Vue({
            //el 属性是固定的手法，表示当前 vm 实例要控制页面上的哪个区域，接受值是一个选择器
            el: '#app',
            // data 对象就是要渲染到页面上的数据
            data: {
                username: 'zhangsan'
            }
        })
    </script>

</body>
```

![](C:\Users\shizeyu\Desktop\notes\Ajax-vue\Snipaste_2022-09-21_16-49-46.png)





------

# 三. Vue的调试工具

## 3.1 安装 vue-devtools

![](C:\Users\shizeyu\Desktop\notes\Ajax-vue\Snipaste_2022-09-21_16-51-34.png)

## 3.2 配置

![](C:\Users\shizeyu\Desktop\notes\Ajax-vue\Snipaste_2022-09-21_16-52-18.png)

## 3.3 使用 vue-devtools 调试Vue

![](C:\Users\shizeyu\Desktop\notes\Ajax-vue\Snipaste_2022-09-21_16-58-14.png)

**`Root指向el指的区域，叫做根节点。右侧data被Vue接管，改变其值，页面效果也会改变`**





# 四. Vue的指令

## 4.1 指令的概念

指令是Vue提供的**模板语法**，用于辅助开发者渲染页面的基本结构

### vue的指令根据不同的用途分为六大类：

1. **内容渲染**指令
2. **属性绑定**指令
3. **事件绑定**指令
4. **双向绑定**指令
5. **条件渲染**指令
6. **列表渲染**指令

## 4.2 内容渲染指令

内容渲染指令是用来辅助开发者<font color='red'>**渲染DOM元素中的文本内容**</font>。

### 4.2.1常用的内容渲染指令：

>1.v-text
>2.{{ }}
>3.v-html

### 4.2.2 v-text（几乎不用）

`v-text`的缺点：<font color='red'>**会覆盖元素内部原有的内容**</font>

```html
<!-- 把username 对应的值，渲染到p种，（跟属性用法相似） --> 
<p v-text="username"></p>

<!-- 把gender对应的值，渲染到第二个p标签中 -->
<!-- 注意：默认文本会被gender值覆盖掉 -->
<p v-text="gender">性别:</p>
```

用法示例：

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
</head>
<body>
    
    <!-- Vue控制的 -->
    <div id="app">
        <p v-text="username"></p>
        <p v-text="gender">性别:</p>
    </div>


    <!-- 导入vue的库文件，在window全局九有了Vue这个构造函数 -->
    <script src="./vue.js"></script>
    <script>
        // 构建Vue的实例对象
        const vm = new Vue({
            //el 属性是固定的手法，表示当前 vm 实例要控制页面上的哪个区域，接受值是一个选择器
            el: '#app',
            // data 对象就是要渲染到页面上的数据
            data: {
                username: 'zhangsan',
                gender: '女'
            }
        })
    </script>
</body>
</html>
```



### 4.2.3  {{}} [插值](https://so.csdn.net/so/search?q=插值&spm=1001.2101.3001.7020)表达式（用的最多）

vue提供的`{{}}`语法，是用来解决`v-text`会覆盖默认文本内容的问题，这种{{}}语法的专业名称是<font color='red'>**插值[表达式](https://so.csdn.net/so/search?q=表达式&spm=1001.2101.3001.7020)**</font>。

`{{}}`在实际开发中用的最多，只是内容的占位符，不会覆盖原有的内容。

使用`{{}}`可以将对应的值渲染到元素的内容节点中。

用法示例：

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
</head>
<body>
    <div id="app">
        <p>姓名：{{ username }}</p>
        <p>性别：{{ gender }}</p>
    </div>

    <script src="https://cdn.jsdelivr.net/npm/vue@2/dist/vue.js"></script>
    <script>
        const vm = new Vue({
            el: '#app',
            data: {
                username: "lisi",
                gender: "男"
            }
        })
    </script>
</body>
</html>
```



### 4.2.4 v-html

`v-text`和`{{}}`只能渲染纯文本内容，如果要把包含`html`标签的字符串渲染为页面的`html`元素，需要使用`v-html`。

**包含`html`标签的字符串渲染为页面的`html`元素**

用法示例：

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
</head>
<body>
    <div id="app">
        <div v-html="content"></div>
    </div>
    <script src="https://cdn.jsdelivr.net/npm/vue@2/dist/vue.js"></script>
    <script>
        const vm = new Vue({
            el: "#app",
            data: {
                content: "<h1>你好</h1>"
            }
        })
    </script>
</body>
</html>


```



## 4.3 属性绑定指令（v-bind）（：）

**`插值表达式 {{}} 只能用在内容节点中，不能用在属性节点中`**

### 4.3.1 v-bind

如果需要为元素的属性动态绑定**属性值**，则需要 v-bind 属性绑定指令。

```html
<!-- <标签名 v-bind:属性名='动态数据名'> -->
<input type="text" v-bind:placeholder="tips">

<script src="./vue.js"></script>
    <script>
        // 构建Vue的实例对象
        const vm = new Vue({
            //el 属性是固定的手法，表示当前 vm 实例要控制页面上的哪个区域，接受值是一个选择器
            el: '#app',
            // data 对象就是要渲染到页面上的数据
            data: {
                tips: '请输入用户名',

            }
        })
</script>
```

在Vue中 v-bind绑定可以简写成:

```html
<!-- 在Vue中 v-bind绑定可以简写成: -->
<input type="text" :placeholder="tips">
```



## 4.4 支持JavaScript表达式

```html
{{ number + 1 }}

{{ ok ? 'YES' : 'NO' }}

//对字符串进行取反，split拆分成数组，reverse()反转数组，join('')数组转字符串
{{ message.split('').reverse().join('') }}

//id是数据名，’‘字符串 ， + 拼接
<div v_bind:id=" 'list' + id " ></div>
```



## 4.5 事件绑定指令（v-on）（@）

### 4.5.1 v-on（重要）

Vue提供了 v-on 事件绑定指令，来辅助为DOM元素绑定事件监听

```html
<body>
    <!-- 被控制的div -->
    <div id="app">

        <div>count的值：{{count}}</div>

        <!-- 语法格式为 v-on:事件名称="事件处理函数的名称" -->
        <button v-on:click="add">+1</button>
        <!-- 绑定事件可以通过（）来传递参数 -->
        <!-- 绑定事件可以省略 v-on: 为 @ -->
        <button @click="sub(1)">-1</button>

    </div>

    <!-- 导入vue的库文件，在window全局九有了Vue这个构造函数 -->
    <script src="./vue.js"></script>
    <script>
        // 构建Vue的实例对象
        const vm = new Vue({
            //el 属性是固定的手法，表示当前 vm 实例要控制页面上的哪个区域，接受值是一个选择器
            el: '#app',
            // data 对象就是要渲染到页面上的数据
            data: {
                count: 0
            },

            // methods 方法内，就是定义事件的处理函数
            methods: {
                add: function () {
                    vm.count += 1
                },
                // 简写可以省略一部分
                sub(n) {
                    //this指向vm实例
                    this.count -= n
                }
            }
        })
    </script>
</body>
```

![](C:\Users\shizeyu\Desktop\notes\Ajax-vue\Snipaste_2022-09-22_15-58-36.png)

> **注意：原生DOM对象有 `onclick`、`oninput`、`onkeyup`等原生事件，替换为vue的事件绑定形式后,**
>
> **分别为： `v-on:click` 、`v-on:input`、`v-on:keyup`**
>
> **即： `@click` 、`@input` 、`@keyup` **



### 4.5.2 事件对象 $event

当事件函数未传参数时，会有一个默认事件对象



![](C:\Users\shizeyu\Desktop\notes\Ajax-vue\Snipaste_2022-09-22_16-18-18.png)

![](C:\Users\shizeyu\Desktop\notes\Ajax-vue\Snipaste_2022-09-22_16-19-13.png)

但当有实参时会传回实参，Vue内置了变量，交 `$event`  ，他就是原生DOM的事件对象`e`

```html
<!-- 事件对象必须写为$event，形参不必 -->
<button @click="add($event,1)">+N</button>
```

```html
	<div id="app">
        <div>count的值：{{count}}</div>
        <!-- 让按钮偶数是黄色，奇数无颜色 -->
        <!-- Vue内置了变量，交 $event  ，他就是原生DOM的事件对象e -->
        <!-- 事件对象必须写为$event，形参不必 -->
        <button @click="add($event,1)">+N</button>
    </div>



    <!-- 导入vue的库文件，在window全局九有了Vue这个构造函数 -->
    <script src="./vue.js"></script>
    <script>
        // 构建Vue的实例对象
        const vm = new Vue({
            //el 属性是固定的手法，表示当前 vm 实例要控制页面上的哪个区域，接受值是一个选择器
            el: '#app',
            // data 对象就是要渲染到页面上的数据
            data: {
                count: 0
            },

            // methods 方法内，就是定义事件的处理函数
            methods: {
                add(e, n) {
                    vm.count += n
                    console.log(e);

                    // 判断是否为偶数
                    if (this.count % 2 === 0) {
                        //偶数 原生DOM语法
                        e.target.style.background = 'yellow'
                    } else {
                        //奇数
                        e.target.style.background = ''
                    }
                }
            }
        })
    </script>
```

### 4.5.3 事件修饰符

在事件处理函数中调用`event.preventDefault()`或`event.stopPropagation()`是非常常见的需求，

Vue提供了时间修饰符，来更方便的<font color='red'>**对事件的触发进行控制**</font>

常见的**事件修饰符**：

|              事件修饰符               | 说明                                                      |
| :-----------------------------------: | :-------------------------------------------------------- |
| <font color='red'>**.prevent**</font> | **阻止默认行为（例如：阻止a链接的跳转、阻止表单的提交）** |
|  <font color='red'>**.stop**</font>   | **阻止事件冒泡**                                          |
|             **.capture**              | 以捕获模式触发当前的事件处理函数                          |
|                 .once                 | 绑定的事件只能触发一次                                    |
|                 .self                 | 只有在event.target是当前元素自身时触发事件处理函数        |

示例:

```html
        <a href="http://www.baidu.com" @click.prevent="show">跳转</a>
```



### 4.5.4 按键修饰符

在监听**键盘事件**时。我们需要**判断详细的按键**，为键盘相关的事件添加**按键修饰符**，

```html
        <!-- 只有在key是 'enter' 的时候调用 vm.submit()  -->
        <input @keyup.enter="submit">

        <!-- 只有在key是 'Esc' 的时候调用 vm.clearInput() -->
        <input @keyup.esc="clearInput">

		<input @keyup.esc="clearInput" @keyup.enter="submit">
```

```
                submit(e) {
                    e.target.value = ''
                },
                clearInput(e) {
                    e.target.value = ''
                }
```



## 4.6 双向绑定指令（v-model）

让程序员在不操作DOM的情况下，<font color='red'>**快速获取表单数据**</font>。

`v-mode`l是双向绑定，表单数据和所绑定的后台数据互相影响。

`v-bind`单向的，后台数据影响表单，但表单数据不会影响数据源

v-model` 本质是监听标签的 `value 属性

```html
	<div id="app">
        <div>count的值：{{username}}</div>
        <input type="text" v-model="username">
		<!-- 底层逻辑里，v-model封装了监听value -->
        <input type="text" :value="username">


    </div>

	<!-- 导入vue的库文件，在window全局九有了Vue这个构造函数 -->
    <script src="./vue.js"></script>
    <script>
        // 构建Vue的实例对象
        const vm = new Vue({
            //el 属性是固定的手法，表示当前 vm 实例要控制页面上的哪个区域，接受值是一个选择器
            el: '#app',
            // data 对象就是要渲染到页面上的数据
            data: {
                tips: '请输入用户名',
                username: 'zhangsan',
                gender: '女',
                info: '<p  style="color: #fff000; font-weight: bold;" >你好世界</p>',
                count: 0
            }
        })
    </script>
```



### 4.6.1 v-model 的使用场景

1. `input` 输入框 `v-mode`会自动判读type类型然后
   - `type = "redio"`
   - `type = "checkbox"`
   - `type = "xxx..."`
2. `extarea`
3. `select`

`select`的控制问题,city跟value互相影响而不是

```html
<select v-model="city">
	<option value="">请选择城市</option>
	<option value="1">北京</option>
	<option value="2">天津</option>
	<option value="3">廊坊</option>
</select>
```



### 4.6.2 v-model 指令的修饰符

| 修饰符  | 作用                                | 示例                            |
| :-----: | ----------------------------------- | ------------------------------- |
| .number | 自动将用户的输入值转为数值类型      | `<input v-model.number="age"/>` |
|  .trim  | 自动过滤用户输入的首尾空白字符      | `<input v-model.trim="msg"/>`   |
|  .lazy  | 在 “change” 时，而非 “input” 时更新 | `<input v-model.lazy="msg"/>`   |

```html
		<div id="app">

        <!-- 默认虽然一开始显示是数据源格式，但input提交会提交字符串，从而改变n1和n2为字符串，添加.number后提交则为数值格式 -->
        <input type="text" v-model.number="n1">+ <input type="text" v-model.number="n2">= <span>{{n1+n2}}</span>
        
        <!-- 每次失去焦点后，会去除值的前后空格，然后再提交到数据源 -->
        <input type="text" v-model.trim="username">
        <button @click="showClick">hhh</button>
    </div>

    <!-- 导入vue的库文件，在window全局九有了Vue这个构造函数 -->
    <script src="./vue.js"></script>
    <script>
        // 构建Vue的实例对象
        const vm = new Vue({
            //el 属性是固定的手法，表示当前 vm 实例要控制页面上的哪个区域，接受值是一个选择器
            el: '#app',
            // data 对象就是要渲染到页面上的数据
            data: {
                username: 'zhangsan',
                n1: 1,
                n2: 2,
            },

            // methods 方法内，就是定义事件的处理函数
            methods: {
                add(e, n) {
                    vm.count += n
                    console.log(e);

                    // 判断是否为偶数
                    if (this.count % 2 === 0) {
                        //偶数 原生DOM语法
                        e.target.style.background = 'yellow'
                    } else {
                        //奇数
                        e.target.style.background = ''
                    }

                },
                showClick() {
                    console.log(`用户名是：${this.username}`);
                }
            }
        })
    </script>
```

![](C:\Users\shizeyu\Desktop\notes\Ajax-vue\Snipaste_2022-09-23_11-16-18.png)



## 4.7 条件渲染指令

条件渲染指令辅助开发者，<font color='red'>**按需控制DOM的显示和隐藏**</font>，有两个分别是：

- v-if  （更常用）
  - 隐藏会删除代码
- v-show
  - 隐藏会添加样式display none

```html
 	<div id="app">
        <!-- 这是被 v-if控制的模块 隐藏会删除代码-->
        <p v-if="flag">这是被 v-if控制的模块</p>
        <!-- 这是被v-show 控制的磨块 隐藏会添加样式display none-->
        <p v-show="flag">这是被v-show 控制的磨块</p>
    </div>
```

![](C:\Users\shizeyu\Desktop\notes\Ajax-vue\Snipaste_2022-09-23_15-12-56.png)

![](C:\Users\shizeyu\Desktop\notes\Ajax-vue\Snipaste_2022-09-23_15-13-21.png)

> 在.vue文件中，整个页面是先编译完再渲染，所以不会出现由上至下先v-if 初始值是false时先生成又删除的情况。



### 4.7.1 v-else

`v-if`可以单独使用，也可以配合`v-else`指令一起使用

`v-else`必须和`v-if`一起使用

```
<div v-if='Math.random() >0.5'>
	随机数大于0.5	
</div>
<div v-else>
	随机数小于或等于0.5	
</div>
```



### 4.7.2 v-else-if

`v-else-if`充当`v-if`的else-if块，可以连续使用

`v-else-if`必须和`v-if`一起使用

```html
        <div v-if="type==='A'">优秀</div>
        <div v-else-if="type==='B'">良好</div>
        <div v-else-if="type==='C'">一般</div>
        <div v-else>差</div>
```



## 4.8 列表渲染指令

`Vue`提供了`v-for`，<font color='red'>**基于一个数组来循环渲染一个列表结构**</font>

`v-for`需要使用 item in items 形式的特殊语法

- items 是<font color='red'>**待循环的数组**</font>
- item 是<font color='red'>**被循环的每一项**</font>

```html
data：{
	list: [  //列表数据
		{ id: 1, name: 'zs' },
		{ id: 2, name: 'ls' }
	]
}
// ---------------------------------------
<ul>
	<li v-for="item in list">姓名是:{{ item.name }}</li>
</ul>
```



### 4.8.1 v-for 中的索引

`v-for`指令还支持一个<font color='red'>**可选的第二个参数**</font>，即<font color='red'>**当前项的索引**</font>。语法格式为 `(item, index) in items`，

```html
data：{
	list: [  //列表数据
		{ id: 1, name: 'zs' },
		{ id: 2, name: 'ls' }
	]
}
// ---------------------------------------
<ul>
	<li v-for="(item, index) in list">索引是：{{ index }}，姓名是:{{ item.name }}</li>
</ul>
```

注意：`v-for`指令中的 <font color='red'>**item 项**</font>和<font color='red'>**index 索引**</font>都是形参，可以进行重命名，例如：(user,i) in userlist



### 4.8.2 v-for 中的key值

注意事项：

1. **官方建议，只要用到了 `v-for`指令，那么一定要绑定一个`:key`值**

2. 而且，**通常把`id`作为`key`的值 **

3. 官方对`key`的值的类型有要求，必须为**字符串或数字类型**

4. 同时`key`的值**必须具有唯一性**，是不能重复的，所以通常都是选择`id`作为`key`
5. 使用 `index` 的值当作key的值没有任何意义，(`index`与数据没有对应关系，非常容易变动)

```html
<ul>
    <!-- 官方建议，只要用到了 v-for指令，那么一定要绑定一个:key值 -->
    <!-- 而且，尽量把id作为key的值，官方对key的值的类型有要求，必须为字符串或数字类型 -->
    <!-- 同时`key`的值是不能重复的，所以通常都是选择`id`作为`key` -->
	<li v-for="(item, index) in list" :key='item.id'>索引是：{{ index }}，姓名是:{{ item.name }}</li>
</ul>
```







# 五. Vue的过滤器（Vue 2）

**vue 3已经删掉了过滤器功能**

过滤器（`Filters`）是`vue`提供的功能，常用于<font color='red'>**文本的格式化**</font>。过滤器可以用在两个地方：**插值表达式**{{}}和 **`v-bind`属性绑定**。

过滤器应该被添加在`JavaScript`表达式的<font color='red'>**尾部**</font>，由<font color='red'>**”管道符“**</font>进行调用

过滤器本质就是**函数**`function`

**过滤器函数必须被定义在 `filters` 节点之下，与`el`同级。<font color='red'>过滤器一定要有一个返回值</font>**

```html
<!-- 在{{}}中通过‘管道符’调用 capitalize 过滤器 ，对 message的值进行格式化 -->				
<p>{{ message | capitalize }}</p>

<!-- 在 v-bind 中通过‘管道符’调用 formatId 过滤器，对 rawId 的值进行格式化 -->
<div v-bind:id="rawId | formatId"></div>
```

管道符前的数据作为参数传入过滤器函数中被格式化操作，返回值最后输出

![](C:\Users\shizeyu\Desktop\notes\Ajax-vue\Snipaste_2022-09-23_17-10-15.png)

```html
	<script src="./vue.js"></script>
    <script>
        // 构建Vue的实例对象
        const vm = new Vue({
            //el 属性是固定的手法，表示当前 vm 实例要控制页面上的哪个区域，接受值是一个选择器
            el: '#app',
            // data 对象就是要渲染到页面上的数据
            data: {
                message: 'hello world',
            },
            // 过滤器函数必须被定义在 filters 节点之下
            filters: {
                capitalize(a) {
                    //过滤器一定要有一个返回值
                    return a
                }
            }
        })
    </script>
```



## 5.1 私有过滤器和全局过滤器

在`filters` 节点之下定义的过滤器，成为**”私有过滤器“**，因为它只能在他所在的vue所控制的区域内

**全局过滤器** 独立于每个 vm 之外 ,**基本都是定义全局过滤器**

```coffeescript
// 全局过滤器 独立于每个 vm 之外
// Vue.filiter() 方法接受两个参数：
//  第 1 个参数，是全局过滤器的‘ 名字 ’
//  第 2 个参数，是全局过滤器的‘ 处理函数 ’
Vue.filter('capitalize', (str) => {
	return str.charAt(0).toUpperCase + str.slice(1)
})
```

> 如果全局过滤器和私有过滤器名字一致，此时按照''就近原则''，调用的是 私有过滤器



## 5.2 连续调用多个过滤器

可以 串联

```html
<!-- 把 message 的值，交给 filterA 进行处理 -->
<!-- 把 filierA 的值，交给 filterB 进行处理 -->
<!-- 把 filterB 的值，作为最终值渲染到页面上 -->
{{ message | filterA | filterB }}
```



## 5.3 过滤器传参

过滤器本质是JavaScript函数，因此可以接受参数，

```html
<!-- arg1 和 arg2 是传递给 filterA 的参数 -->
<p>{{ message | filter(arg1,arg2) }}</p>

// 过滤器处理函数的形参列表中：
//  第一个参数：永远都是”管道符“前面待处理得值
//  第二给参数开始，才是调用过滤器传递归来的 arg1 和 arg2 参数
Vue.filter('filterA', (message, arg1, arg2) => {
	//过滤器代码

})
```





# Vue 基础入门

# 一.监听器

## 1.1 什么是 watch 侦听器

用于[监听](https://so.csdn.net/so/search?q=监听&spm=1001.2101.3001.7020)数据变化，从而针对特定的数据做出特定的操作



## 1.2 侦听器的格式

### 优缺点

1. 方法格式的侦听器
   - 缺点1：无法再刚既然你页面的时候，自动触发
   - 缺点2：如果监听一个对象，对象内的属性发生变化，不会触发监听器
2. 对象格式的侦听器
   - 优点1：可以通过 **immediate**选项，让侦听器自动触发
   - 优点2：可以通过**deep**选项，让侦听器深度监听对象中每个属性的变化

## 1.3 方法格式的侦听器（简单）

```
watch: {
	username(newVal, oldVal) {
    //监听 username 值的变化，侦听谁的值就以谁的名字命名函数名
    //newVal是“变化后的新值”，oldVal是“变化前的久值”
    console.log(newVal, oldVal);
    }
}
```

```html
    <script src="./vue.js"></script>
    <script>
        // 构建Vue的实例对象
        const vm = new Vue({
            //el 属性是固定的手法，表示当前 vm 实例要控制页面上的哪个区域，接受值是一个选择器
            el: '#app',
            // data 对象就是要渲染到页面上的数据
            data: {
                username: 'zhangsan',
            },

            watch: {
                username(newVal, oldVal) {
                    //监听 username 值的变化，监听谁的值就以谁的名字明明函数名
                    //newVal是“变化后的新值”，oldVal是“变化前的久值”
                    console.log(newVal, oldVal);
                }
            }
    </script>
```



## 1.4 对象格式的侦听器（含复杂的）

### `immediate` 的作用：控制侦听器是否自动触发一次

```html
watch: {
	// 定义对象格式的侦听器
	username: {
		// hander是固定写法，表示当 username 的值发生变化时，自动调用 hander 处理函数
		handler(newVal, oldeVal) {
			console.log(newVal, oldeVal);
		},
		// immediate 选项的默认值是 false
		// immediate 的作用：控制侦听器是否自动触发一次
		immediate: true
	}
},
```

```html
<script src="./vue.js"></script>
    <script>
        // 构建Vue的实例对象
        const vm = new Vue({
            //el 属性是固定的手法，表示当前 vm 实例要控制页面上的哪个区域，接受值是一个选择器
            el: '#app',
            // data 对象就是要渲染到页面上的数据
            data: {
                username: 'zhangsan',
            },
            // watch: {
            //     // 对象格式的
            //     // username(newVal, oldVal) {
            //     //     //监听 username 值的变化，监听谁的值就以谁的名字明明函数名
            //     //     //newVal是“变化后的新值”，oldVal是“变化前的久值”
            //     //     console.log(newVal, oldVal);

            //     }
            // },

            watch: {
                // 定义对象格式的侦听器
                username: {
                    // hander是固定写法，表示当 username 的值发生变化时，自动调用 hander 处理函数
                    handler(newVal, oldeVal) {
                        console.log(newVal, oldeVal);
                    },
                    // immediate 选项的默认值是 false
                    // immediate 的作用：控制侦听器是否自动触发一次
                    immediate: true
                }
            },
    </script>
```



## 1.5 深度侦听

### `deep`

如果<font color='red'>**watch侦听的是一个对象**</font>

在<font color='red'>**方法格式的侦听器**</font>，如果监听一个对象，对象内的属性发生变化，<font color='red'>**不会触发监听器**</font>

通过对象侦听器的<font color='red'>**deep选项**</font>来让侦听器深度监听对象中每个属性的变化

```
deep: true
```

```html
<body>
    <div id="app">
        <input type="text" v-model="info.username">
    </div>



    <!-- 导入vue的库文件，在window全局九有了Vue这个构造函数 -->
    <script src="./vue.js"></script>
    <script>
        // 构建Vue的实例对象
        const vm = new Vue({
            //el 属性是固定的手法，表示当前 vm 实例要控制页面上的哪个区域，接受值是一个选择器
            el: '#app',
            // data 对象就是要渲染到页面上的数据
            data: {
                info: {
                    username: 'zs'
                }
            },

            watch: {
                // 定义对象格式的侦听器
                info: {
                    handler(newVal, oldeVal) {
                        console.log(newVal, oldeVal);
                    },
                    // immediate 选项的默认值是 false
                    // immediate 的作用：控制侦听器是否自动触发一次
                    immediate: true,
                    // 开启深度侦听，只要对象中的任何一个属性变化了，都会触发“对象的侦听器”
                    deep: true
                }
            },
        })
    </script>
</body>
```



## 1.6 监听对象单个属性的变化

如果<font color='red'>**只想监听对象中单个属性的变化**</font>，则可以按照如下的方式定义watch侦听器：

> **侦听这种对象内属性需要加单引号或双引号**

```
            watch: {
                // 定义对象格式的侦听器
                // 侦听这种对象内属性需要加单引号或双引号
                'info.username': {
                    handler(newVal, oldeVal) {
                        console.log(newVal, oldeVal);
                    },
                }
            },
```

```html
<body>
    <div id="app">
        <input type="text" v-model="info.username">
    </div>



    <!-- 导入vue的库文件，在window全局九有了Vue这个构造函数 -->
    <script src="./vue.js"></script>
    <script>
        // 构建Vue的实例对象
        const vm = new Vue({
            //el 属性是固定的手法，表示当前 vm 实例要控制页面上的哪个区域，接受值是一个选择器
            el: '#app',
            // data 对象就是要渲染到页面上的数据
            data: {
                info: {
                    username: 'zs'
                }
            },

            watch: {
                // 定义对象格式的侦听器
                // 侦听这种对象内属性需要加单引号或双引号
                'info.username': {
                    handler(newVal, oldeVal) {
                        console.log(newVal, oldeVal);
                    },
                }
            },
        })
    </script>
</body>
```





# 二.计算属性

计算属性指的是，通过一系列计算，最终得到一个属性值

这个动态计算出来的属性值可以被模板结构或 methods 方法使用，

<font color='red'>**所有的计算属性都要定义到`computed`下**</font>

<font color='red'>**计算属性在定义时，要定义成‘方法格式’，所以有返回值return**</font>

<font color='red'>**但使用是当属性来使用**</font>

好处：实现了代码的复用

```html
<body>
    <div id="app">
        {{ rgb }}
    </div>



    <!-- 导入vue的库文件，在window全局九有了Vue这个构造函数 -->
    <script src="./vue.js"></script>
    <script>
        // 构建Vue的实例对象
        const vm = new Vue({
            //el 属性是固定的手法，表示当前 vm 实例要控制页面上的哪个区域，接受值是一个选择器
            el: '#app',
            // data 对象就是要渲染到页面上的数据
            data: {
                r: 0,
                g: 0,
                b: 0
            },

            // 所有的计算属性都要定义到`computed`下
            // 计算属性在定义时，要定义成‘方法格式’ 所以有返回值return
            // 但使用是当属性来使用
            computed: {
                // rgb作为一个计算属性，被定义成了方法格式
                // 在这个方法中最终返回一个字符串
                rgb() {
                    return `rgb(${this.r},${this.g},${this.b})`
                }
            },

            methods: {
                show() {
                    // 调用属性
                    onsole.log(this.rgb);
                }
            }
        })
    </script>
</body>
```





# 三.axios

> axios *[æk'si:əʊs]*是一个专注于网络请求的库！

相比于XHR 它更简单易用

相比于JQ它更轻量化，专注于网络数据请求

> axios是通过Promise实现对ajax技术的一种封装,就像jquery对ajax的封装一样,简单来说就是ajax技术实现了局部数据的刷新,axios实现了对ajax的封装,axios有的ajax都有,ajax有的axios不一定有,总结一句话就是axios是ajax,ajax不止axios

## 安装

使用 npm:

```
$ npm install axios
```

使用 bower:

```
$ bower install axios
```

使用 cdn:

```
<script src="https://unpkg.com/axios/dist/axios.min.js"></script>
```



## 基础语法：

```html
<script src="https://unpkg.com/axios/dist/axios.min.js"></script>
    <script>

        // 调用axios方法返回值是promise对象
        axios({
            // 请求方式
            method: 'GET',
            // 请求地址
            url: 'http://www.liulongbin.top:3006/api/getbooks'
        }).then((result) => {
            // .then 用来指定请求成功后的回调函数
            // 形参中的result是请求成功之后的结果,
            // 真实的数据在 result的data内，即 result.data
            console.log(result);
        })
    </script>
```

[^promise]: 补充知识部分

<font color='red'>**axios在请求到数据之后，在真正的数据之外，套了一层壳，进行了包装**</font>

如图所示，网页显示和apipost的结果不同



![](C:\Users\shizeyu\Desktop\notes\Ajax-vue\Snipaste_2022-09-27_09-41-05.png)

![](C:\Users\shizeyu\Desktop\notes\Ajax-vue\Snipaste_2022-09-27_09-41-14.png)



实际<font color='red'>**真实的数据**</font>在`axios`数据的`data`项里

![](C:\Users\shizeyu\Desktop\notes\Ajax-vue\Snipaste_2022-09-27_09-43-04.png)



## get请求

```
axios({
	method: 'GET',
	url: 'http://www.liulongbin.top:3006/api/get',
	params: {
		name: 'zs',
		age: 20
    }
}).then(function(res){
	console.log(res.data)
})
```

## post请求

```
axios({
	method: 'POST',
	url: 'http://www.liulongbin.top:3006/api/post',
	data: {
		bookname: '程序员自我修养',
		price: 666
    }
}).then(function(res){
	console.log(res.data)
})
```

<font color='red'>**两者传参不同 get请求用params，post请求用data**</font>



## 解决.then回调地狱的问题

> 相比于Promise，async/await能更好的处理then链
> await关键字只能在async function中使用，在任何非async function的函数中使用await关键字都会抛出错误。await关键字在执行下一行代码之前 等待右侧表达式（可能是一个Promise）返回。
>
> async/await的优势在于处理then的调用链，能够更清晰准确的写出代码，并且也能解决[回调](https://so.csdn.net/so/search?q=回调&spm=1001.2101.3001.7020)地狱的问题。当然也存在一些缺点，因为await将异步代码改造成了同步代码，如果多个异步代码**没有依赖性**却使用了await会导致性能上的降低。

**如果调用某个方法的返回值是promise实例，则前面可以添加await**

**await 只能用在被async "修饰"的方法中**

```html
<scripy>
    document.querySelector('#id名字').addEventListener('click', async function(){
    	const result = await axios({
    		method: 'POST',
			url: 'http://www.liulongbin.top:3006/api/post',
			data: {
				bookname: '程序员自我修养',
			price: 666
    		}
    	})
    
    	console.log(result.data)
    })
</scripy>
```

## 实际使用

1. 调用 axios 之后，使用 async/await 进行简化，以简化.then操作
2. 使用赋值解构，从axios封装的大对象中，把 data属性解构出来
3. 把解构出来的 data 属性，使用 冒号 ：进行重命名，一般都命名为 { data:res }
4. res.data即真实数据

```html
<body>

    <div>
        <button id="btn">GET</button>
    </div>


    <script src="https://unpkg.com/axios/dist/axios.min.js"></script>
    <script>
        document.querySelector('#btn').addEventListener('click', async function () {
            // 1. 调用 axios 之后，使用 async/await 进行简化
            // 2. 使用赋值解构，从axios封装的大对象中，把 data属性解构出来
            // 3. 把解构出来的 data 属性，使用 冒号 ：进行重命名，一般都命名为 { data:res }
            // 4. res.data即真实数据
            // 解构赋值的时候，只用：进行重命名
            // 调用axios方法返回值是promise对象
            const { data: res } = await axios({
                // 请求方式
                method: 'GET',
                // 请求地址
                url: 'http://www.liulongbin.top:3006/api/getbooks'
            })
            // .then((result) => {
            // .then 用来指定请求成功后的回调函数
            // 形参中的result是请求成功之后的结果
            // console.log(result);
            // })
            console.log(res.data);
        })
    </script>
</body>
```

![](C:\Users\shizeyu\Desktop\notes\Ajax-vue\Snipaste_2022-09-27_11-16-39.png)



### 10.1 axios发起GET请求

```
引入axios本地文件
<script src="../axios.min.js"></script>
```

```
axios.get('url',{params:{ /*参数*/ }}).then(callback)
```

```
		// 请求的URL地址
        const url = 'http://www.liulongbin.top:3006/api/get'
        // 请求的参数对象
        const paramsOBj = { name: 'zs', age: 20 }
        // 调用axios.get() 发起GET请求
        document.querySelector('#btn').addEventListener('click', async function () {
        	const {data:res}= await axios.get(url, { params: paramsOBj })
        	console.log(res.data)
        })
```

### 10.2 axios发起POST请求

```
axios.post('url',{ /*参数*/ }).then(callback)
```

```
		// 请求的URL地址
        const url = 'http://www.liulongbin.top:3006/api/post'
        // 要提交到服务器的数据
        const dataObj = { location:'北京', address:'顺义' }
        // 调用axios.post() 发起POST请求
        document.querySelector('#btn').addEventListener('click', async function () {
        	const {data:res}= await axios.post(url, dataObj)
        	console.log(res.data)
        })
```

### 

# 四. Vue-cli （脚手架）

Vue CLI 是一个基于 Vue.js 进行快速开发的完整系统

> Vue CLI 致力于将 Vue 生态中的工具基础标准化。它确保了各种构建工具能够基于智能的默认配置即可平稳衔接，这样你可以专注在撰写应用上，而不必花好几天去纠结配置的问题。与此同时，它也为每个工具提供了调整配置的灵活性，无需 eject

## 一.安装

Node 版本要求

Vue CLI 4.x 需要 [Node.js](https://nodejs.org/) v8.9 或更高版本 (推荐 v10 以上)。你可以使用 [n](https://github.com/tj/n)，[nvm](https://github.com/creationix/nvm) 或 [nvm-windows](https://github.com/coreybutler/nvm-windows) 在同一台电脑中管理多个 Node 版本。

可以使用下列任一命令安装这个新的包：

```
npm install -g @vue/cli
# OR
yarn global add @vue/cli
```

安装之后，你就可以在命令行中访问 `vue` 命令。你可以通过简单运行 `vue`，看看是否展示出了一份所有可用命令的帮助信息，来验证它是否安装成功。

你还可以用这个命令来检查其版本是否正确：

```
vue --version
or
vue -V
```

### 升级[#](https://cli.vuejs.org/zh/guide/installation.html#升级)

如需升级全局的 Vue CLI 包，请运行：

```
npm update -g @vue/cli

# 或者
yarn global upgrade --latest @vue/cli
```

#### 项目依赖[#](https://cli.vuejs.org/zh/guide/installation.html#项目依赖)

上面列出来的命令是用于升级全局的 Vue CLI。如需升级项目中的 Vue CLI 相关模块（以 `@vue/cli-plugin-` 或 `vue-cli-plugin-` 开头），请在项目目录下运行 `vue upgrade`：

```
用法： upgrade [options] [plugin-name]

（试用）升级 Vue CLI 服务及插件

选项：
  -t, --to <version>    升级 <plugin-name> 到指定的版本
  -f, --from <version>  跳过本地版本检测，默认插件是从此处指定的版本升级上来
  -r, --registry <url>  使用指定的 registry 地址安装依赖
  --all                 升级所有的插件
  --next                检查插件新版本时，包括 alpha/beta/rc 版本在内
  -h, --help            输出帮助内容
```



## 二.创建一个项目

在<font color='red'>**要创建的目录里运行**</font>vue create

运行以下命令来创建一个新项目：

```
vue create 项目的名称
```

接下来弹出一个信息框：

```
?  Your connection to the default npm registry seems to be slow.   
   Use https://registry.npm.taobao.org for faster installation? Yes
```

由于我是在国内操作的，访问比较慢，所以弹出一个信息询问我们是否加速，我们选择 `yes`。

![](C:\Users\shizeyu\Desktop\notes\Ajax-vue\Snipaste_2022-09-28_09-16-07.png)

vue2 vue3 自定义

![](C:\Users\shizeyu\Desktop\notes\Ajax-vue\Snipaste_2022-09-28_09-20-01.png)

![](C:\Users\shizeyu\Desktop\notes\Ajax-vue\Snipaste_2022-09-28_09-20-53.png)

![](C:\Users\shizeyu\Desktop\notes\Ajax-vue\Snipaste_2022-09-28_09-23-23.png)

![](C:\Users\shizeyu\Desktop\notes\Ajax-vue\Snipaste_2022-09-28_09-25-18.png)

![](C:\Users\shizeyu\Desktop\notes\Ajax-vue\Snipaste_2022-09-28_09-25-42.png)

如果看到这行文字就说明你项目初始化成功。

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200911204005946.png#pic_center)

```
cd xxx 		//到根目录

npm run serve //与webpack自定义的 run dev相同时运行的意思
```

### 窗口冻结和恢复

![](C:\Users\shizeyu\Desktop\notes\Ajax-vue\Snipaste_2022-09-28_09-26-55.png)



## 三.跑起来项目

运行以下命令，进入监听（类似于webpack-dev-serve插件）然后打开域名，如图所示

```
cd xxx 		//到根目录

npm run serve //与webpack自定义的 run dev相同时运行的意思
```

<font color='red'>**npm窗口不能关啊，否则监听就断了**</font>

![](C:\Users\shizeyu\Desktop\notes\Ajax-vue\Snipaste_2022-09-28_09-36-37.png)

![](C:\Users\shizeyu\Desktop\notes\Ajax-vue\Snipaste_2022-09-28_09-36-51.png)



同样的在`package.json`配置文件中，有同样的`scripts`，只不过相较于`webpack`的`dev/build`，`Vue`这里默认是`serve/build`

![](C:\Users\shizeyu\Desktop\notes\Ajax-vue\Snipaste_2022-09-28_09-42-03.png)

也可以用vscode自带的终端，快捷键ctrl+`

![](C:\Users\shizeyu\Desktop\notes\Ajax-vue\Snipaste_2022-09-28_09-51-19.png)



## 四.项目的目录结构

1. src--源代码
2. .gitgnore--git忽略文件
3. babel.xxx--babel配置文件（js语法兼容 加载器

![](C:\Users\shizeyu\Desktop\notes\Ajax-vue\Snipaste_2022-09-28_10-00-47.png)

![](C:\Users\shizeyu\Desktop\notes\Ajax-vue\Snipaste_2022-09-28_10-06-08.png)

vue脚手架将包含new vue的编译生成的控制放到了自动的js文件中

![](C:\Users\shizeyu\Desktop\notes\Ajax-vue\Snipaste_2022-09-28_10-08-00.png)

![在这里插入图片描述](https://img-blog.csdnimg.cn/20181124105445337.jpg?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzM4NjUyODcx,size_16,color_FFFFFF,t_70)

>bulid
>里面是一些操作文件，使用npm run * 时执行的就是这里的文件。
>config
>配置文件，执行文件需要的配置信息。例如运行的端口，IP等等信息
>src
>资源文件，所有的组件以及所用的图片都是在这个文件夹下放着。
>看一下这个文件夹都放了哪些东西。
>assets
>资源文件夹，放图片之类的资源，
>components
>组件文件夹，写的所有组件都放在这个文件夹下，
>router
>路由文件夹，这个决定了页面的跳转规则，
>App.vue
>应用组件，所有自己写的组件，都是在这个组件之上运行了。
>main.js
>webpack入口文件。

node_modules

>node_modules是安装node后用来存放用包管理工具下载安装的包的文件夹。比如webpack、gulp、grunt这些工具。在node.js中模块与文件是一一对应的，也就是说一个node.js文件就是一个模块。
>
>modules(模块)：在node.js中模块与文件是一一对应的，也就是说一个node.js文件就是一个模块，文件内容可能是我们封装好的一些JavaScript方法、jsON数据、编译过的C/C++拓展等，在关于node.js的误会提到过node.js的架构。
>
>其中http、fs、net等都是node.js提供的核心模块，使用C/C++实现，外部用JavaScript封装。

### vue项目中src目录的构成（重要*）

```
assets 文件夹：资源文件夹，放图片、css样式表之类的资源，
components 组件文件夹，写的、封装的、可复用的所有组件都放在这个文件夹下，
main.js 是项目的入口文件，整个项目的执行需要先执行main.js
App.vue 是项目的根组件，控制UI界面，应用组件，所有自己写的组件，都是在这个组件之上运行了。
```

![](C:\Users\shizeyu\Desktop\notes\Ajax-vue\Snipaste_2022-09-28_10-19-59.png)

在vue项目中，src目录下的main.js就是wepack的entry节点语法

![](C:\Users\shizeyu\Desktop\notes\Ajax-vue\Snipaste_2022-09-28_10-27-34.png)





## 六. vue项目运行的过程

在工程化的项目中，vue要做的事是通过<font color='red'>**main.js**</font>把<font color='red'>**App.vue**</font>的UI结构渲染到<font color='red'>**index.html**</font>的指定区域中。

其中：

1. <font color='red'>**App.vue**</font> 用来编写待渲染的<font color='red'>**模板结构**</font>
2. <font color='red'>**index.html**</font>中需要预留一个 <font color='red'>**el区域**</font>
3. <font color='red'>**main.js**</font> 把 App.vue 渲染到了 index.html 所预留的区域中

### main结构如下所示

```js
// 导入 vue这个包，得到 Vue 构造函数
import Vue from 'vue'
// 导入 App.vue根组件，将来要把 App.vue 中的模板UI结构，渲染到 HTML 页面中
import App from './App.vue'

// 去掉生产模式下的一些提示，防止浏览器控制台打印警告信息
Vue.config.productionTip = false

// 创建 Vue 的实例对象
new Vue({
  el: '#app',
  // 把 render 函数指定的组件，渲染到 HTML 页面中
  render: h => h(App),
})
```

> **`render`的作用，把导入的`App.vue`渲染到`index.html`的`<div id="app"></div>`中，即用`App.vue`顶替到`<div id="app"></div>`中**

**Vue实例的 .$mount('#app') 方法，作用与el属性完全一样**

```js
// 导入 vue这个包，得到 Vue 构造函数
import Vue from 'vue'
// 导入 App.vue根组件，将来要把 App.vue 中的模板UI结构，渲染到 HTML 页面中
import App from './App.vue'

// 去掉生产模式下的一些提示，防止浏览器控制台打印警告信息
Vue.config.productionTip = false

// 创建 Vue 的实例对象
new Vue({
  // el: '#app',
  // 把 render 函数指定的组件，渲染到 HTML 页面中
  render: h => h(App),
}).$mount('#app')

// Vue实例的 .$mount('#app') 方法，作用与el属性完全一样
```



















# 五. vue 组件

## 1.什么是组件化开发

<font color='red'>**组件化开发**</font>指的是：根据<font color='red'>**封装**</font>的思想，<font color='red'>**把页面上可重用的UI结构封装为组件**</font>，从而方便开发和维护

## 2.Vue项目中的组件化开发

`vue` 是一个<font color='red'>**支持组件化开发**</font>的前端框架。

`vue` 中规定：<font color='red'>**组件的后缀名**</font>是<font color='red'>**.vue**</font>。`APP.vue` 文件本质上是一个 vue 的<font color='red'>**组件**</font>

### 根组件：render指向的.vue文件就是根组件（App.vue)

## 3. vue 组件的三个组成部分

每个.vue组件都由3部分构成，分别是：

- <font color='red'>**template**</font> -> 组件的<font color='red'>**模板结构**</font> UI结构、DOM标签
- <font color='red'>**script**</font> -> 组件的 <font color='red'>**JavaScript行为**</font>
- <font color='red'>**style**</font> -> 组件的<font color='red'>**样式**</font>

> 通俗来说，整个vue就是控制内，**data相较于以前要写成函数形式，其他的包括methods使用与之前一致**

```vue
<template>
  <div class="test-box">自定义数值{{ username }}</div>
</template>

<script>
// 默认导出。这是个固定写法
export default {
  // data数据源
  // 注意： .vue组件中的data不能像之前一样，不能指向对象
  // 注意：组件中的data必须是一个函数
  // data: {
  //   username: "zs",
  // },
  // 组件中的data写成一个函数，数据以函数返回值形式定义，这样每复用一次组件，就会返回一分新的data，类似于给每个组件实例创建一个私有的数据空间，让各个组件实例维护各自的数据
  // 若写成以前的单纯的对象形式，就使得所有组件实例共用了一份data，就会造成一个变了全都变的情况
  data() {
    // 这个 return 出去的 { }中，可以定义数据
    return {
      username: "zs",
    };
  },
};
</script>

<style>
.test-box {
  background-color: red;
}
</style>

```

>  data
>
>  注意： .vue组件中的data不能像之前一样，不能指向对象,组件中的data必须是一个**函数**
>
>  组件中的data写成一个函数，数据以函数返回值形式定义，这样每复用一次组件，就会返回一分新的data，类似于给每个组件实例创建一个私有的数据空间，让各个组件实例维护各自的数据
>
>  若写成以前的单纯的对象形式，就使得所有组件实例共用了一份data，就会造成一个变了全都变的情况

## 4.组件中的methods（v-on）（@）

```vue
<template>
  <div>
    <div class="test-box">自定义数值{{ username }}</div>
    <button @click="changeName">修改用户名</button>
  </div>
</template>

<script>
// 默认导出。这是个固定写法
export default {
  // data数据源
  // 注意： .vue组件中的data不能像之前一样，不能指向对象
  // 注意：组件中的data必须是一个函数
  // data: {
  //   username: "zs",
  // },
  // 组件中的data写成一个函数，数据以函数返回值形式定义，这样每复用一次组件，就会返回一分新的data，类似于给每个组件实例创建一个私有的数据空间，让各个组件实例维护各自的数据
  // 若写成以前的单纯的对象形式，就使得所有组件实例共用了一份data，就会造成一个变了全都变的情况
  data() {
    // 这个 return 出去的 { }中，可以定义数据
    return {
      username: "admin",
    };
  },
  methods: {
    changeName() {
      // 在组件中，this就表示当前组件的实例对象
      console.log(this);
      this.username = "hhh";
    },
  },
  // 当前组建中的监听器
  watch: {},
  // 当前组件中的计算属性
  computed: {},
  // 当前组件中的过滤器
  filters: {},
};
</script>

<style>
.test-box {
  background-color: red;
}
</style>

```

在组件中，this就表示当前组件的实例对象

![](C:\Users\shizeyu\Desktop\notes\Ajax-vue\Snipaste_2022-09-29_14-54-51.png)

## 5. .vue 只能有一个根节点

![](C:\Users\shizeyu\Desktop\notes\Ajax-vue\Snipaste_2022-09-29_14-59-35.png)

![](C:\Users\shizeyu\Desktop\notes\Ajax-vue\Snipaste_2022-09-29_14-56-51.png)

报错，只能有一个根节点

## 6.启用less语法

![](C:\Users\shizeyu\Desktop\notes\Ajax-vue\Snipaste_2022-09-29_15-01-58.png)



## 7.组件之间的父子关系

组件在被封装好之后，<font color='red'>**彼此之间是相互独立的**</font>，不存在关系

在<font color='red'>**使用组件**</font>，<font color='red'>**根据彼此的嵌套关系**</font>，形成了<font color='blue'>**父子关系、兄弟关系**</font>



## 8.（私有子组件） 使用组件的三个步骤

### 8.1 步骤一 使用 import 语法导入需要的组件

```vue
import Left from '@/components/Left.vue'
```

![](C:\Users\shizeyu\Desktop\notes\Ajax-vue\Snipaste_2022-09-29_15-58-39.png)

### 8.2 使用 components 节点注册组件

```vue
export default{
	components:{
		Left
	}
}
// 若注册多个组件，就Left,right
```

![](C:\Users\shizeyu\Desktop\notes\Ajax-vue\Snipaste_2022-09-29_15-59-41.png)

### 8.3 以标签习惯是使用刚才注册的组件

```
	<div>
      <!-- 这里渲染名为 left 的组件 -->
      <Left></Left>
    </div>
```

![](C:\Users\shizeyu\Desktop\notes\Ajax-vue\Snipaste_2022-09-29_16-00-18.png)

全部代码：

```vue
<template>
  <div>
    <div class="test-box">自定义数值{{ username }}</div>
    <button @click="changeName">修改用户名</button>

    <div>
      <!-- 这里渲染名为 left 的组件 -->
      <Left></Left>
    </div>
  </div>
</template>

<script>
// 导入需要使用的.vue文件
import Left from "@/components/Left.vue";
// 默认导出。这是个固定写法
export default {
  // data数据源
  // 注意： .vue组件中的data不能像之前一样，不能指向对象
  // 注意：组件中的data必须是一个函数
  // data: {
  //   username: "zs",
  // },
  // 组件中的data写成一个函数，数据以函数返回值形式定义，这样每复用一次组件，就会返回一分新的data，类似于给每个组件实例创建一个私有的数据空间，让各个组件实例维护各自的数据
  // 若写成以前的单纯的对象形式，就使得所有组件实例共用了一份data，就会造成一个变了全都变的情况
  data() {
    // 这个 return 出去的 { }中，可以定义数据
    return {
      username: "admin",
    };
  },
  methods: {
    changeName() {
      // 在组件中，this就表示当前组件的实例对象
      console.log(this);
      this.username = "hhh";
    },
  },

  components: {
    // 全称代码是 'Left': left   键值对，可简写
    Left,
  },
};
</script>

<style lang='less'>
.test-box {
  background-color: red;
  color: "blue";
}
</style>

```

![](C:\Users\shizeyu\Desktop\notes\Ajax-vue\Snipaste_2022-09-29_15-57-21.png)



## 9. 使用 components 节点注册的组件是私有子组件

8.2中使用 components 节点注册组件是私有子组件

只有导入了vue，并且注册了才能是使用这个组件，若其他组件想使用也要进行同样的导入注册操作



所以可以选择进行<font color='red'>**注册全局组件**</font>



## 10. 注册全局组件

在vue项目的<font color='red'>**main.js**</font>入口文件中，通过<font color='red'>**Vue.componebt()**</font>方法，可以注册全局组件，实例：

```js
// 导入需要全局注册的组件
import Count from '@/components/Count.vue'

// 参数1 字符串格式，表示组件的"注册名称",即调用的时候使用的名称
// 参数2 需要被全局注册的那个组件
Vue.component('MyCount',Count)
```



## 11.组件的props

props 是组件的<font color='red'>**自定义属性**</font>，在<font color='red'>**封装通用组件**</font>的时候，合理的使用 props 可以极大的<font color='red'>**提高组件的复用性**</font>

语法格式：

```vue
// 在被调用的组件中设置props  （简化版）
export default{
	// 组件的自定义属性
	props:['自定义属性A','自定义属性B'，'其他自定义属性...'],
	
	// 组件的私有数据
	data(){
		return{}
	}
}

or  （完整对象格式）

export default:
	props: {
		//自定义属性A : { */ 配置选项 */ }
		//自定义属性B : { */ 配置选项 */ }
		//自定义属性C : { */ 配置选项 */ }
	}
}
```

```
// 在调用者组件内使用
<组件名 自定义属性A='xxx'>
or
// v-bind本质是js，props的值默认是字符串，而v-bind可以是数值或
<组件名 :自定义属性A='xxx'>
```

### 11.1结合v-bind ，如上

Vue规定：组件中封装的自定义属性是<font color='red'>**只读**</font>，<font color='red'>**不能直接修改**</font>props的值。否则会报错

要修改 props 的值，可以把<font color='red'>**props 的值转存到data中**</font>

![](C:\Users\shizeyu\Desktop\notes\Ajax-vue\Snipaste_2022-09-30_10-06-56.png)

### 11.2实例：

`main.js` 定义`count.vue`为全局组件，标签`MyCount`

![](C:\Users\shizeyu\Desktop\notes\Ajax-vue\Snipaste_2022-09-30_10-13-53.png)

`Left`组件调用了`count.vue`组件

![](C:\Users\shizeyu\Desktop\notes\Ajax-vue\Snipaste_2022-09-30_10-13-59.png)

`Left.vue`是根组件的私有组件，渲染

![](C:\Users\shizeyu\Desktop\notes\Ajax-vue\Snipaste_2022-09-30_10-14-17.png)

使用自定义props

![](C:\Users\shizeyu\Desktop\notes\Ajax-vue\Snipaste_2022-09-30_10-14-53.png)

![](C:\Users\shizeyu\Desktop\notes\Ajax-vue\Snipaste_2022-09-30_10-19-08.png)



### 11.3 props 的 default 默认值

在自定义属性时，可以通过default来定义属性的默认值，

**props的完整对象格式**：

```
export default:
	props: {
		//自定义属性A : { */ 配置选项 */ }
		//自定义属性B : { */ 配置选项 */ }
		//自定义属性C : { */ 配置选项 */ }
	}
}
```

props 的 default 默认值:

```coffeescript
export default:
	props: {
		init: {
			// 用default 属性定义属性的默认值 若没有传递init值 默认值才会生效
			default: 0
		}
	}
}
```



### 11.4 props 的 type 默认值

> 用 `type` 属性定义属性的默认值

> 如果传递过来的值不符合此类型，则会在终端报错

```
export default:
	props: {
		init: {
			// 用default 属性定义属性的默认值 若没有传递init值 默认值才会生效
			default: 0,
			// 用 `type` 属性定义属性的默认值
			// 如果传递过来的值不符合此类型，则会在终端报错
			type: Number,
		}
	}
}
```

<font color='red'>**报错解决**</font>

> 大部分可以通过传递只时候加v-bind：来解决详见11.1



### 11.5 props 的 required 必填项

必填项校验，若设置为 `true` 则若调用组件时不输入传递值则报错

```
export default:
	props: {
		init: {
			// 用default 属性定义属性的默认值 若没有传递init值 默认值才会生效
			default: 0,
			// 用 `type` 属性定义属性的默认值
			// 如果传递过来的值不符合此类型，则会在终端报错
			type: Number,
			// 必填项校验
			required: true,
		}
	}
}
```



## 12 组件之间样式冲突（scoped）

默认情况下，<font color='red'>**写在.vue组件中的样式会全局生效**</font>，因此会容易造成<font color='red'>**多个组件之间的样式冲突问题**</font>

> 导致组件之间样式冲突的根本原因：
>
> 1. 单页面应用程序，所有组件的DOM结构，都是唯一的 index.html 页面进行呈现的
> 2. 每个组件中的样式，都会影响整个 index.html 页面中的 DOM元素

本质：利用css属性选择器来解决这个问题

### 12.1.什么是scoped

在Vue文件中的style标签上有一个特殊的属性，scoped。当一个style标签拥有scoped属性时候，它的css样式只能用于当前的Vue组件，可以使组件的样式不相互污染。如果一个项目的所有style标签都加上了scoped属性，相当于实现了样式的模块化。

### 12.2.scoped的实现原理

Vue中的scoped属性的效果主要是通过PostCss实现的。以下是转译前的代码:

```
<style scoped>

    .example{

        color:red;

    }

</style>

<template>

    <div>scoped测试案例</div>

</template>
```

转译后:

```
.example[data-v-5558831a] {

  color: red;

}

<template>

    <div class="example" data-v-5558831a>scoped测试案例</div>

</template>
```

既:PostCSS给一个组件中的所有dom添加了一个独一无二的动态属性，给css选择器额外添加一个对应的属性选择器，来选择组件中的dom,这种做法使得样式只作用于含有该属性的dom元素(组件内部的dom)。

> 总结：scoped的渲染规则：

1. 给HTML的dom节点添加一个不重复的data属性(例如: data-v-5558831a)来唯一标识这个dom 元素
2. 在每句css选择器的末尾(编译后生成的css语句)加一个当前组件的data属性选择器(例如：[data-v-5558831a])来私有化样式

![](C:\Users\shizeyu\Desktop\notes\Ajax-vue\Snipaste_2022-09-30_15-01-10.png)



![](C:\Users\shizeyu\Desktop\notes\Ajax-vue\Snipaste_2022-09-30_15-10-59.png)

![](C:\Users\shizeyu\Desktop\notes\Ajax-vue\Snipaste_2022-09-30_15-15-37.png)



<font color='red'>**scoped能使得样式只能渲染自己组件内的内容，保证样式不会污染出去**</font>

<font color='red'>**但其父级若无 scoped 则会把 父级的样式染进 子级覆盖子级的样式**</font>



### 12.3 /deep/ 穿透

scoped看起来很好用，当时在Vue项目中，当我们引入第三方组件库时(如使用vue-awesome-swiper实现移动端轮播)，需要在局部组件中修改第三方组件库的样式，而又不想去除scoped属性造成组件之间的样式覆盖。这时我们可以通过特殊的方式穿透scoped。

> sass和less的样式穿透 使用/deep/

<font color='red'>**通过在父级样式中添加`/deep/`可以控制子级组件的样式对其进行样式，这样就可以避免操作已经封装好的子级组件**</font>

![](C:\Users\shizeyu\Desktop\notes\Ajax-vue\Snipaste_2022-09-30_15-31-15.png)

> 查看代码可以发现其自动生成了[data -v-xxx] + 标签 来指向子级的标签

![](C:\Users\shizeyu\Desktop\notes\Ajax-vue\Snipaste_2022-09-30_15-31-00.png)









# 六.组件的生命周期

## 6.1 生命周期 & 生命周期函数

<font color='red'>**生命周期**</font> （ Life Cycle ）是指一个组件从 <font color='red'>**创建**</font> -> <font color='red'>**运行**</font> -> <font color='red'>**销毁**</font> 的整个阶段， <font color='red'>**强调的是一个时间段 **</font>。
<font color='red'>**生命周期函数**</font> ：是由 vue 框架提供的 <font color='red'>**内置函数**</font> ，会伴随着组件的生命周期， <font color='red'>**自动按次序执行**</font> 。
注意： <font color='blue'>**生命周期强调的是时间段，生命周期函数强调的是时间点**</font>。

## 6.2 组件生命周期函数的分类

![img](https://img-blog.csdnimg.cn/1b79ad28000f4f47b0c5c07d59ec0323.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBA5qyi5oSJ772e,size_20,color_FFFFFF,t_70,g_se,x_16)

## 6.3 生命周期图示

> 编译流程
>
> `.vue`文件`html`无法识别，所以通过脚手架中`package.json`配置文件中的`vue-template-compiler`编译器从`main.js`开始编译，对根节点进行编译，然后编译在根节点中调用的其他组件，最后都会被编译成`html`下方的那两个js文件内。
>
> 组件可以当成是构造函数，调用组建的过程可以看作是`new`一个构造函数的实例

参考 vue 官方文档给出的“生命周期图示”：
https://cn.vuejs.org/v2/guide/instance.html# 生命周期图示

![img](https://img-blog.csdnimg.cn/3c069e13b29246a984e406a179c634ae.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBA5qyi5oSJ772e,size_20,color_FFFFFF,t_70,g_se,x_16)

##  6.4 生命周期函数

### 创建阶段

new Vue() 即以<>标签形式创建实例

#### 1.beforeCreate（不重要没用）

**创建阶段的第1个生命周期函数,组件的props，methods，data尚未被创建，处于不可用**

#### 2.created（最早可以发起Ajax请求）

创建阶段的第2个生命周期函数，组件的props，methods，data已创建好，可以使用，但<font color='red'>**组件的模板结即`<template>`构尚未生成 ，不能操作DOM，！！！但最早可以发起Ajax请求**</font>

<font color='red'>**经常通过created函数调用methods中的方法，请求服务器的数据，并且把请求到的数据转存到data中，供template模板渲染时去使用**</font>

![](C:\Users\shizeyu\Desktop\notes\Ajax-vue\Snipaste_2022-10-08_09-37-56.png)

#### 3.beforeMount（没啥用）

创建阶段的第3个生命周期函数,内存编译好的HTML结构准备渲染到浏览器中，此时浏览器中还没有当前组件的DOM结构，**无法操作DOM**

#### 4.mounted（最早可以操作DOM）

创建阶段的第4个生命周期函数，**已经渲染内存的HTML结构**到浏览器中，包含了当前组件的DOM结构，

<font color='red'>**！！！最早可以操作DOM**</font>

### 运行阶段（根据数据变化进入运行阶段）

#### 1.beforeUpdate

运行阶段的第1个生命周期函数，**将要**根据数据变化后、最新的数据，重新渲染组件的模板结构，<font color='red'>**此时数据变化后还未放到模板结构上**</font>

#### 2.updated（当数据变化后，为了能够操作到最新的DOM结构）

运行阶段的第2个生命周期函数，完成了最新数据重新渲染到组件的DOM结构

<font color='red'>**!!!当数据变化后，为了能够操作到最新的DOM结构,应将代码写在update中**</font>

### 销毁阶段（用的很少)

```
<button @click="flag = !flag">取反控制自定义·组件·Test显示还是移除</button>
<Test v-if="flag"></Test>

//
data(){
	return{
		flag: true;
	}
}
```



#### 1.beforeDestroy

销毁阶段的第1个生命周期函数，**组件还处于正常工作状态**

#### 2.destroyed

销毁阶段的第2个生命周期函数

```vue
<template>
  <div class="test-container">
      <h3 id="myh3">Test.vue组件  ----{{books.length }}本图书</h3>
      <p id="pppp">message的值是：{{message}}</p>
      <button @click="message+='迪丽热巴'">修改message的值</button>
  </div>
</template>
 
<script>
export default {
    props:['info'],
    data(){
        return{
            message:'hello vue.js!',
            /* 定义books数组，存储的是所有图书列表数据，默认为空数组 */
            books:[]
        }
    },
    methods:{
        show(){
            console.log('调用了Test组件的show方法！');
        },
        /* 使用Ajax请求图书列表的数据 */
        initBookList(){
            const xhr=new XMLHttpRequest()
            xhr.addEventListener('load',()=>{
               const result=JSON.parse(xhr.responseText)
               console.log(result);
               this.books=result.data
            })
            xhr.open('GET','http://www.liulongbin.top:3006/api/getbooks')
            xhr.send()
        }
    },
    /* 创建阶段的第1个生命周期函数,
    组件的props，methods，data
    尚未被创建，处于不可用 */
    beforeCreate() {
        /* console.log(this.info);
        console.log(this.message);
        this.show() */
    },
   
   /* 创建阶段的第2个生命周期函数
    组件的props，methods，data已创建好
    可以使用，但组件的模板结构尚未生成
    ，不能操作DOM，
    ！！！但最早可以发起Ajax请求
     */
    created() {
       /*created生命周期函数  
       经常通过created函数调用methods中的方法，
       请求服务器的数据，并且把请求到的数据转存到data中
       供template模板渲染时去使用 */
    /* console.log(this.info);
        console.log(this.message);
        this.show() */
        this.initBookList()
        
    },
    
    /* 创建阶段的第3个生命周期函数,
    内存编译好的HTML结构准备渲染到浏览器中
    此时浏览器中还没有当前组件的DOM结构
    无法操作DOM */
    beforeMount(){
        /* console.log('beforeMount');
        const dom=document.querySelector('#myh3')
        console.log(dom); */
    },
 
    /* 创建阶段的第4个生命周期函数
    已经渲染内存的HTML结构到浏览器中
    包含了当前组件的DOM结构，
    ！！！最早可以操作DOM */
    mounted() {
    //   console.log(this.$el);  
     const dom=document.querySelector('#myh3')
        console.log(dom);
    },
 
    /* 运行阶段的第1个生命周期函数
    将要根据数据变化后、最新的数据，重新渲染组件的
    模板结构，此时数据变化后还未放到模板结构上 */
    beforeUpdate(){
      /*   console.log('beforeUpdate');
        console.log(this.message);
        const dom=document.querySelector('#pppp')
        console.log(dom.innerHTML); */
    },
    
    /* 运行阶段的第2个生命周期函数,
    完成了最新数据重新渲染到组件的DOM结构
    !!!当数据变化后，为了能够操作到最新的DOM结构,
    应将代码写在update中 */
    updated() {
          console.log('beforeUpdate');
        console.log(this.message);
        const dom=document.querySelector('#pppp')
        console.log(dom.innerHTML);
    },
 
 
    /* 销毁阶段的第1个生命周期函数
    组件还处于正常工作状态 */
    beforeDestroy(){
        console.log('beforeDestroy');
        console.log(this.message);
    },
 
    /* 销毁阶段的第2个生命周期函数 */
    destroyed() {
        
    },
 
}
</script>
 
<style lang="less" scoped>
test-container{
    background-color: pink;
    height: 200px;
}
 
</style>
```































# 七.组件之间的数据共享

在项目开发中，组件之间的最常见的关系分为如下两种：

1、父子关系

2、兄弟关系

## 7.1 父子组件的数据共享

父子组件之间的数据共享又分为：

父-->子共享数据

子-->父共享数据

## 7.2 父组件向子组件共享数据

父组件向子组件共享数据需要使用<font color='red'>**自定义属性 props**</font> 

```vue
//子组件
<template>
       <div>
             <h5>Son组件</h5>
             <p>父组件专传递过来的msg值是:{{ msg }}</p>
             <p>父组件专传递过来的user值是:{{ user }}</p>
       </div>
</template>

<script>
export default {

     props:["msg","user"]

}
</script>
```



```vue
//父组件

//调用子组件
//通过属性绑定将父组件对应的属性值传给子组件，":"一定要加，不然只传递message过去，而不是hello vue.js
<Son :msg="message" :user="userinfo"></Son>

data(){
     return{
             message:"hello vue.js",
             userinfo:{ name:'zs', age:20 }
     }

}
```

> 不要修改`props`的值

## 7.3 子组件向父组件共享数据

子组件向父组件共享数据使用<font color='red'>**自定义事件**</font>

![img](https://pic4.zhimg.com/80/v2-8e957d00b4c7338a641dbf12ede729a7_1440w.webp)

```vue
<template>
    <div>
        父组件:{{count}}

        //绑定getNewCount函数
        <Zi @NewCount="getNewCount"></Zi>

    </div>
</template>

<script>
import Zi from '@/components/Zi.vue'


export default {
    components:{
    Zi,
    
},

    data(){
        return {
            count:0
        }
    },
    methods:{

        //定义getNewCount函数,参数val是子组件的值
        getNewCount(val){
            this.count=val;
        }
    }

}
</script>

<style>

</style>
```



```vue
<template>
    <div>
        子组件:{{count}}
        <button @click="add">+1</button>
    </div>
</template>

<script>
export default {

    data(){
        return {
            count:0
        }
    },
    methods:{
        add(){

            this.count+=1;
            //修改数据时，通过$emit()触发自定义事件
            this.$emit("NewCount",this.count)
        }
    }



}
</script>

<style>

</style>
```

## 兄弟组件之间的数据共享

在vue2.x中，兄弟组件之间数据共享的方案是EventBus

1、创建evenBus.js模块，并向外共享一个Vue的实例对象

2、在数据发送方，调用bus.$emit('事件名称',要发送的数据) 方法触发自定义事件

3、在数据接收方，调用bus.$on('事件名称',事件处理函数)方法注册一个自定义事件

![img](https://pic2.zhimg.com/80/v2-7a52831742b4cee23350270a2f905295_1440w.webp)

```vue
//兄弟组件（数据发送端）
<template>
  <div>
        <h1>Right组件{{ msg }}</h1>
        <button @click="sendMsg"></button>
  </div>
</template>

<script>

    import bus from "@/eventBus.js"
export default {

    data(){
        return {
            msg:"hello vue.js"
        }
    },
    methods:{
        sendMsg(){
            bus.$emit("share",this.msg)
        }
    }

}
</script>

<style lang="less" scoped>
    div{
        width: 300px;
        height: 400px;
        background-color: aqua;
    }
</style>
```



```js
//eventBus.js

import Vue from 'vue'
//向外共享Vue的实例对象
export default new Vue()
```



```vue
// 兄弟组件(数据接收方)
<template>
   <div>
            <h1>Lift组件{{msgFromLeft}}</h1>

   </div>
</template>

<script>

import bus from '@/eventBus.js'

export default {
        data(){
            return {
                msgFromLeft:""
            }
        },
        created(){  
            bus.$on("share",val=>{
                this.msgFromLeft=val;
            })
        }
}
</script>

<style lang="less" scoped>
div{
    width: 300px;
    height: 400px;
    background-color: antiquewhite;
}
</style>
```

## ref引用

什么是ref引用

ref用来辅助开发者在不依赖jQuery的情况下，获取DOM元素或组件的引用。

每个vue的组件实例上，都包含一个$refs对象，里面存储着对应的DOM元素或组件的引用。默认情况下，组件的$refs指定一个空对象

```vue
<template>
  <div>

    <!-- 起ref名字 -->
    <h1 ref="h1">App根目录</h1>
    <h2 ref="h2">aa</h2>
    <button @click="show">打印this</button>
  </div>
</template>

<script>
export default {

  methods:{
    show(){

      //通过this.$refs.名字获取标签
      console.log(this.$refs.h1)
    }
  }
    

}
</script>
```

使用ref引用组件实例

如果想要使用ref引用页面上的组件实例，则可以按照如下的方式进行操作

```vue
<template>
  <div>
    counter组件
  </div>
</template>

<script>
export default {

    methods:{
        add(){
            console.log("+1")
        }

    }

}
</script>
```



```vue
<template>
  <div>

    <!-- 使用ref属性，为对应的组件添加对应的名称 -->
      <My-Count ref="counterRef"></My-Count>
      <button @click="show">+1</button>

  </div>
</template>

<script>
import MyCount from "@/components/counter.vue" 

export default {

  components:{
    "My-Count":MyCount,
  },



  methods:{
    show(){

      //通过this.$refs.引用名称，可以引用组件的实例
      console.log(this.$refs.counterRef)

      //引用到组件的实例之后，就可以调用组件上的methods方法
      this.$refs.counterRef.add()

    }
  }
    

}
</script>
```

## this.$nextTick(cb)

组件的$nextTick(cb)方法，会把cb回调推迟到下一个DOM更新周期之后执行。通俗的理解是：等组件的DOM更新完成之后，再执行cb回调函数，从而能保证cb回调函数可以操作到最新的DOM

```vue
<template>
  <div>
    <input type="text" v-if="inputVisible" @blur="showButton" ref="iptRef">
    <button @click="showInput" v-else >输入内容</button>
  </div>
</template>

<script>
export default {

  data(){
    return {
      inputVisible:false
    }
  },

    methods:{

      //点击按钮，展示输入框
        showInput(){

          //1、切换布尔值，把文本展示出来
          this.inputVisible=true

          //让文本框获取焦点
          //直接使用this.$refs.iptRef.focus()会报错，因为DOM没有渲染完成，不能拿到dom的focus(),使用$nextTick()等待DOM渲染完成
          this.$nextTick(()=>{
            this.$refs.iptRef.focus()
          })


        },

      
        showButton(){
          this.inputVisible=false
        }

    }

}
</script>
```

## 动态组件

### 什么是动态组件

动态组件指的是动态切换组件的显示与隐藏

### 如何实现动态组件的渲染

vue提供了一个内置的<component>组件，专门用来实现动态组件的渲染

```vue
<template>
  <div>
    <div>
      <h1>App组件</h1>
      <button @click="showLeft">切换为Left组件</button>
      <button @click="showRight">切换为Right组件</button>
    </div>
    <div class="www">
      <component :is="comName"></component>  
    </div>
  </div>
</template>

<script>
import Left from "@/components/Left.vue"
import Right from "@/components/Right.vue"
export default {

  data(){
      return {
        comName:"Left"
      }
  },

  components:{
    Left,
    Right,
  },

  methods:{
    showLeft(){
      this.comName="Left"
    },
    showRight(){
      this.comName="Right"
    }

  }
}
</script>
```

### 使用keep-alive保持状态

当组件被切换到其他组件在切换回来的时候是，组件会重新创建新的组件，原来的组件被销毁，原来的数据跟着销毁，为了保持原来的数据和组件不被销毁可以使用**keep-alive将组件缓存**

```text
<keep-alive>
      <component :is="comName"></component>  
</keep-alive>
```

### keep-alive对应的生命周期函数

当组件被缓存时，会自动触发组件的deactivated生命周期

当组件被激活时，会自动触发组件的activated生命周期

这些生命周期写在组件中

### keep-alive的include属性

指定那些组件可以缓存，即那个组件可以由keep-alive

include属性用来指定：只有名称匹配的组件会被缓存。多个组件名之间使用英文的逗号分隔

exclude属性表示不被缓存的组件，include和exclude不能同时使用

```text
<keep-alive include="myLefr,MyRight">
      <component :is="comName"></component>  
</keep-alive>
```

如果在“声明组件”的时候，没有为组件指定name名称，则组件队的名称默认就是“注册时候的名称”

当提供了name属性之后，组件的名称就是name属性的值

组件的“注册名称”的主要应用场景是，以标签的形式，把注册号的组件，渲染和使用到页面结构中

组件声明时候的name名称的主要应用场景：结合keep-alive标签实现缓存功能，以及调试工具中看到组件的name名称





























# 八.ref引用























# 补充知识



## promise

介绍
promise是ES6的重要特性之一

传统的异步编程的解决方案是使用回调函数，但是这样就会导致嵌套过深，产生回调地狱，那么promise异步编程的另一种解决方案，而且会更加的强大。

三种状态

- pending（待定）初始状态，既没有被兑现，也没有被拒绝
- fulfilled（已兑现）意味着操作成功完成
- rejected（已拒绝）意味着操作失败。

特点

- 待定状态的 Promise 对象要么会通过一个值被兑现（fulfilled），要么会通过一个原因（错误）*被拒绝（rejected）*当这些情况之一发生时，我们用 promise 的 then 方法排列起来的相关处理程序就会被调用
- Promise.prototype.then 和 Promise.prototype.catch 方法返回的是 promise， 所以它们可以被链式调用

## promise的三个实例方法

### then（）方法

- then是实例状态发生改变时的回调函数，第一个参数是resolved状态的回调函数，第二个参数是rejected状态的回调函数
- then方法返回的是一个新的Promise实例，也就是promise能链式书写的原因

```javascript
promise.then(result => {···})
```

### catch方法

当出现异常 则需要catch方法进行捕获

```javascript
promise.then(result => {···}).catch(error => {···})
```

### finally()方法

方法用于指定不管 Promise 对象最后状态如何，都会执行的操作

```
promise.then(result => {···}).catch(error => {···}).finally(() => {···});
```

promise的静态方法
resolve方法
方法返回一个以给定值解析后的Promise 对象
定值有以下几种情况：

- 如果这个值是一个 promise ，那么将返回这个 promise
- 参数不是具有then()方法的对象，或根本就不是对象，Promise.resolve()会返回一个新的 Promise 对象，状态为resolved
- 没有参数时，直接返回一个resolved状态的 Promise 对象

### reject()方法

Promise.reject(reason)方法也会返回一个新的 Promise 实例,该实例的状态为rejected

```
const p = Promise.reject('出错了')

等同于
const p = new Promise((resolve, reject) => reject('出错了'))
p.then(null, function (s) {console.log(s)})
//出错了Promise.reject()方法的参数，会原封不动地变成后续方法的参数
```

### any()方法

接收一个Promise可迭代对象，只要其中的一个 promise 成功，就返回那个已经成功的 promise 。如果可迭代对象中没有一个 promise 成功（即所有的 promises 都失败/拒绝），就返回一个失败的 promise 和AggregateError类型的实例，它是 Error 的一个子类，用于把单一的错误集合在一起。本质上，这个方法和Promise.all()是相反的。

```
const pErr = new Promise((resolve, reject) => {
  reject("总是失败");
});

const pSlow = new Promise((resolve, reject) => {
  setTimeout(resolve, 500, "最终完成");
});

const pFast = new Promise((resolve, reject) => {
  setTimeout(resolve, 100, "很快完成");
});

Promise.any([pErr, pSlow, pFast]).then((value) => {
  console.log(value);
  // pFast fulfils first
})
```

#### All()方法

1. 方法接收一个promise的iterable类型（注：Array，Map，Set都属于ES6的iterable类型）的输入，并且只返回一个[`Promise`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Promise)实例

```
const p = Promise.all([p1, p2, p3]);
```

> 实例p的状态由p1,p2,p3决定，分两种情况：
>
> 1. 只有p1、p2、p3的状态都变成fulfilled，p的状态才会变成fulfilled，此时p1、p2、p3的返回值组成一个数组，传递给p的回调函数
> 2. 只要p1、p2、p3之中有一个被rejected，p的状态就变成rejected，此时第一个被reject的实例的返回值，会传递给p的回调函数

#### allSettled方法

> Promise.all 会在任何一个请求失败的时候进入失败状态
>
> 由于单一 Promise 进入 rejected 状态便会立即让 Promise.all() 的结果进入 rejected 状态，以至于通过 Promise.all() 进入 rejected 状态时，其中的源 Promise 仍然可能处于 pending 状态，以至于无法获得所有 Promise 完成的时机。

> Promise.allSettled() 静态方法会等待所有源 Promise 进入 fulfilled 或者 rejected 状态，从而确保不会造成时序上的冲突。

#### race方法

该方法同样是将多个 Promise 实例，包装成一个新的 Promise 实例

```
const p = Promise.race([p1, p2, p3]);
```

> 1. 只要p1、p2、p3之中有一个实例率先改变状态，p的状态就跟着改变
> 2. 率先改变的 Promise 实例的返回值则传递给p的回调函数

### [语法糖](https://so.csdn.net/so/search?q=语法糖&spm=1001.2101.3001.7020)Async/Await

在ES8中新增了`Promise`的语法糖`async await`来更优雅的处理异步。

`async` 可以单独存在, 用该关键字声明的函数返回的是一个 Promise 对象。

```
async funtion add(){
    return 1
}
add()
add() instanceof Promise // true
```

`await` 不可以单独存在，必须要配合 `async` 一起存在使用

```
function sub() {
    await 1
}
// 这个方法定义就不满足语法的，会如下报错
// Uncaught SyntaxError: await is only valid in async function
```

`async` `await` 让异步处理更优雅

```
let fs = require('fs')

var  gen = async function() {

    const f1= await readFile('files/a.txt');//封装一个promise对象
    console.log(f1)
    const f2=  await readFile('files/b.txt');
    console.log(f2)
    const f3=  await readFile('files/c.txt');
    console.log(f3)
  
  };


  var readFile=function(path){
     return  new Promise((resolve,reject)=>{
        fs.readFile(path,'utf-8',function(err,data){
            if(!err){
          
             resolve(data)
            }else{
              reject(err)
            }
            
         });
      })
   
}


  
var obj = gen();
```



### 

## CSS 属性选择器详解

**CSS 2 引入了属性选择器。**

**属性选择器可以根据元素的属性及属性值来选择元素。**

------

### 简单属性选择

如果希望选择有某个属性的元素，而不论属性值是什么，可以使用简单属性选择器。

------

例子 1

如果您希望把包含标题（title）的所有元素变为红色，可以写作：

```
*[title] {color:red;}
```

例子 2

与上面类似，可以只对有 href 属性的锚（a 元素）应用样式：

```
a[href] {color:red;}
```

例子 3

还可以根据多个属性进行选择，只需将属性选择器链接在一起即可。

例如，为了将同时有 href 和 title 属性的 HTML 超链接的文本设置为红色，可以这样写：

```
a[href][title] {color:red;}
```

例子 4

可以采用一些创造性的方法使用这个特性。

例如，可以对所有带有 alt 属性的图像应用样式，从而突出显示这些有效的图像：

```
img[alt] {border: 5px solid red;}
```

例子 5：为 XML 文档使用属性选择器

属性选择器在 XML 文档中相当有用，因为 XML 语言主张要针对元素和属性的用途指定元素名和属性名。

假设我们为描述太阳系行星设计了一个 XML 文档。如果我们想选择有 moons 属性的所有 planet 元素，使之显示为红色，以便能更关注有 moons 的行星，就可以这样写：

```
planet[moons] {color:red;}
```

这会让以下标记片段中的第二个和第三个元素的文本显示为红色，但第一个元素的文本不是红色：

```
<planet>Venus</planet>
<planet moons="1">Earth</planet>
<planet moons="2">Mars</planet>
```

------

### 根据具体属性值选择

除了选择拥有某些属性的元素，还可以进一步缩小选择范围，只选择有特定属性值的元素。

例子 1

例如，假设希望将指向 Web 服务器上某个指定文档的超链接变成红色，可以这样写：

```
a[href="http://www.w3school.com.cn/about_us.asp"] {color: red;}
```

例子 2

与简单属性选择器类似，可以把多个属性-值选择器链接在一起来选择一个文档。

```
a[href="http://www.w3school.com.cn/"][title="W3School"] {color: red;}
```

这会把以下标记中的第一个超链接的文本变为红色，但是第二个或第三个链接不受影响：

```
<a href="http://www.w3school.com.cn/" title="W3School">W3School</a>
<a href="http://www.w3school.com.cn/css/" title="CSS">CSS</a>
<a href="http://www.w3school.com.cn/html/" title="HTML">HTML</a>
```

例子 3

同样地，XML 语言也可以利用这种方法来设置样式。

下面我们再回到行星那个例子中。假设只希望选择 moons 属性值为 1 的那些 planet 元素：

```
planet[moons="1"] {color: red;}
```

上面的代码会把以下标记中的第二个元素变成红色，但第一个和第三个元素不受影响：

```
<planet>Venus</planet>
<planet moons="1">Earth</planet>
<planet moons="2">Mars</planet>
```



#### 属性与属性值必须完全匹配

请注意，这种格式要求必须与属性值完全匹配。

如果属性值包含用空格分隔的值列表，匹配就可能出问题。

请考虑一下的标记片段：

```
<p class="important warning">This paragraph is a very important warning.</p>
```

如果写成 p[class="important"]，那么这个规则不能匹配示例标记。

要根据具体属性值来选择该元素，必须这样写：

```
p[class="important warning"] {color: red;}
```

------

### 根据部分属性值选择

如果需要根据属性值中的词列表的某个词进行选择，则需要使用波浪号（~）。

假设您想选择 class 属性中包含 important 的元素，可以用下面这个选择器做到这一点：

```
p[class~="important"] {color: red;}
```

如果忽略了波浪号，则说明需要完成完全值匹配。

#### 部分值属性选择器与点号类名记法的区别

该选择器等价于我们在类选择器中讨论过的点号类名记法。

也就是说，p.important 和 p[class="important"] 应用到 HTML 文档时是等价的。

那么，为什么还要有 "~=" 属性选择器呢？因为它能用于任何属性，而不只是 class。

例如，可以有一个包含大量图像的文档，其中只有一部分是图片。对此，可以使用一个基于 title 文档的部分属性选择器，只选择这些图片：

```
img[title~="Figure"] {border: 1px solid gray;}
```

这个规则会选择 title 文本包含 "Figure" 的所有图像。没有 title 属性或者 title 属性中不包含 "Figure" 的图像都不会匹配。

#### 子串匹配属性选择器

下面为您介绍一个更高级的选择器模块，它是 CSS2 完成之后发布的，其中包含了更多的部分值属性选择器。按照规范的说法，应该称之为“子串匹配属性选择器”。

很多现代浏览器都支持这些选择器，包括 IE7。

下表是对这些选择器的简单总结：

| 类型         | 描述                                       |
| :----------- | :----------------------------------------- |
| [abc^="def"] | 选择 abc 属性值以 "def" 开头的所有元素     |
| [abc$="def"] | 选择 abc 属性值以 "def" 结尾的所有元素     |
| [abc*="def"] | 选择 abc 属性值中包含子串 "def" 的所有元素 |

可以想到，这些选择有很多用途。

举例来说，如果希望对指向 W3School 的所有链接应用样式，不必为所有这些链接指定 class，再根据这个类编写样式，而只需编写以下规则：

```
a[href*="w3school.com.cn"] {color: red;}
```

**提示：**任何属性都可以使用这些选择器。

------

### 特定属性选择类型

最后为您介绍特定属性选择器。请看下面的例子：

```
*[lang|="en"] {color: red;}
```

上面这个规则会选择 lang 属性等于 en 或以 en- 开头的所有元素。因此，以下示例标记中的前三个元素将被选中，而不会选择后两个元素：

```
<p lang="en">Hello!</p>
<p lang="en-us">Greetings!</p>
<p lang="en-au">G'day!</p>
<p lang="fr">Bonjour!</p>
<p lang="cy-en">Jrooana!</p>
```

一般来说，[att|="val"] 可以用于任何属性及其值。

假设一个 HTML 文档中有一系列图片，其中每个图片的文件名都形如 *figure-1.jpg* 和 *figure-2.jpg*。就可以使用以下选择器匹配所有这些图像：

```
img[src|="figure"] {border: 1px solid gray;}
```

当然，这种属性选择器最常见的用途还是匹配语言值。











# 啊啊啊

<font color='red'>****</font>



## less知识 

## Virtual Dom

# 简单了解SPA、SEO及CSR和SSR渲染方式
