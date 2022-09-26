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



















# 三. Vue-cli



# 四. vue 组件











# 啊啊啊

<font color='red'>****</font>





























