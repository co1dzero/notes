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



## 4.3 属性绑定指令（v-bind）

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
> **即： `@click` 、`@input` 、`@keyup` `**



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
|              .capture**               | 以捕获模式触发当前的事件处理函数                          |
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

v-model` 本质是监听标签的 `value 属性`

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
    //监听 username 值的变化，侦听谁的值就以谁的名字明明函数名
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

vue脚手架将new vue控制放到了自动的js文件中

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
export default{
	// 组件的自定义属性
	props:['自定义属性A','自定义属性B'，'其他自定义属性...'],
	
	// 组件的私有数据
	data(){
		return{}
	}
}
```

















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







# 啊啊啊

<font color='red'>****</font>



## less知识 template
