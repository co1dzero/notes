preventDefault() 阻止默认`



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


    <!-- 导入vue的库文件，在window全局就有了Vue这个构造函数 -->
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

> 在绑定 布尔值 即 `true`和`false`时，例如 `allowClear="false"` 定义在字符串内，所以借用`v-bind`将其绑定为一个变量，即 `:allowClear="false"` 来实现正常使用

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

------

#### 事件修饰符(1) .stop 阻止冒泡

在vue中使用.stop来阻止默认冒泡事件

```html
<div id="app">
        <div id="inner" @click="innerClick()">
            <input type="button" value="按钮"  @click="btnClick()" name="" id="">
        </div>
    </div>
<script src="./js/vue.js"></script>
    <script>
 
        let vm = new Vue({
            el:"#app",
            data:{},
            methods:{
                innerClick(){// 内部div点击事件
                    console.log("内部div点击事件");
                },
                btnClick(){// 按钮点击事件
                    console.log("按钮点击事件");
                }
            }
        })
 
    </script>
```

![img](https://img-blog.csdnimg.cn/f60512f769e040358f7f568687d4f56c.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBA5pyA54ix5Zad5oCh5a6d,size_6,color_FFFFFF,t_70,g_se,x_16)

加上.stop

```html
                                 <!-- (1) .stop  阻止冒泡 -->
<input type="button" value="按钮"  @click.stop="btnClick()" name="" id="">
```

![img](https://img-blog.csdnimg.cn/b4a3d6bd7cdc443c9428e88cf90aa87b.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBA5pyA54ix5Zad5oCh5a6d,size_6,color_FFFFFF,t_70,g_se,x_16)

------



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

`v-for`渲染列表`table`：

```
			<table class="rules-table">
              <tr>
                <th>里程区间（公里）</th>
                <th>自提（+ x 天）</th>
                <th>配送（+x 天）</th>
              </tr>
              <tr v-for="item in ranges" :key="item.id">
                <td>{{ item.mileageRange }}</td>
                <td>{{ item.ownTime }}</td>
                <td>{{ item.distributionTime }}</td>
              </tr>
            </table>
            
            -------------------------------------------------------
            data() {
    return {
      ranges: [
        {
          id: 1,
          mileageRange: '0<里程≤100',
          ownTime: '0~1',
          distributionTime: '1~2',
        },
        {
          id: 2,
          mileageRange: '100<里程≤200',
          ownTime: '1~2',
          distributionTime: '1~2',
        },
        {
          id: 3,
          mileageRange: '200<里程≤300',
          ownTime: '1~2',
          distributionTime: '1~2',
        },
        {
          id: 4,
          mileageRange: '300<里程',
          ownTime: '1~2',
          distributionTime: '1~2',
        },
      ],
    }
  },
```



### 4.8.1 v-for 中的索引

`v-for`指令还支持一个<font color='red'>**可选的第二个参数**</font>，即<font color='red'>**当前项的索引**</font>。语法格式为 `(item, index) in items`，

> `index`从0开始

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

注意：`v-for`指令中的 <font color='red'>**item 项**</font>和<font color='red'>**index 索引**</font>都是形参，可以	进行重命名，例如：(user,i) in userlist



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

<font color='red'>**全局过滤器写在`main.js`内**</font>

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

```js
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
        	console.log(res)
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



## *vue 中axios

```vue
Get请求
<template>
  <div class="back1">
    <h1>left组件</h1>
    <button @click="getInfo">发送GET请求</button>
  </div>
</template>

<script>
import axios from 'axios'
export default {
  methods: {
    async getInfo() {
      const { data: res } = await axios.get(
        'http://www.liulongbin.top:3006/api/get'
      )
      console.log(res)
      console.log(res.data)
    },
  },
}
</script>

<style lang="less" scoped>
.back1 {
  background-color: aqua;
  min-height: 200px;
  flex: 1;
}
</style>

```

```vue
<template>
  <div class="back">
    <h1>right组件</h1>
    <button @click="postInfo">POST请求</button>
  </div>
</template>

<script>
import axios from 'axios'
export default {
  methods: {
    async postInfo() {
      const { data: res } = await axios.post(
        'http://www.liulongbin.top:3006/api/post',
        { name: 'zs', age: 20 }
      )
      console.log(res)
      console.log(res.data)
    },
  },
}
</script>

<style lang="less" scoped>
.back {
  background-color: deeppink;
  min-height: 200px;
  flex: 1;
}
</style>

```

### 简易

#### 把axios挂载到vue原型上

> `vue.prototype.axios` 中的`axios`是自定义的，可以改为例如`$http`,则在使用的时候就要修改成对应的`this.$http.get`或`this.&http.host`

![](C:\Users\shizeyu\Desktop\notes\Ajax-vue\Snipaste_2022-10-24_15-03-29.png)

![](C:\Users\shizeyu\Desktop\notes\Ajax-vue\Snipaste_2022-10-24_15-17-19.png)

#### 并配置请求根目录

> 把 axios 挂载到 Vue.prototype 上，供每个 .vue 组件的实例直接使用，

![](C:\Users\shizeyu\Desktop\notes\Ajax-vue\Snipaste_2022-10-24_15-24-58.png)

![](C:\Users\shizeyu\Desktop\notes\Ajax-vue\Snipaste_2022-10-24_15-26-37.png)

<font color='red'>**`注意`**</font>：但是，把`axios`挂载到`Vue`原型上，有一个缺点，不利于`api`接口的复用`



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

### 7.2 父组件向子组件共享数据

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

### 7.3 子组件向父组件共享数据

子组件向父组件共享数据使用<font color='red'>**自定义事件**</font>

> 通过触发`add`然后执行`$emit`，通过`$emit`触发自定义事件`numchange`将`count`传递过去，再触发事件绑定的事件处理函数`getNewCount`将传递过来的子组件的值

![img](https://pic4.zhimg.com/80/v2-8e957d00b4c7338a641dbf12ede729a7_1440w.webp)

可以通过vue插件的事件栏

![](C:\Users\shizeyu\Desktop\notes\Ajax-vue\Snipaste_2022-10-09_13-56-31.png)

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
            //NewCount 是自定义事件名
            this.$emit("NewCount",this.count)
        }
    }



}
</script>

<style>

</style>
```

## 7.4兄弟组件之间的数据共享

非父子即兄弟

在`vue2.x`中，兄弟组件之间数据共享的方案是`EventBus`

1、创建<font color='red'>**`evenBus.js`**</font>模块，并向外共享一个<font color='red'>**`Vue`的实例对象`d`**</font>

2、在数据<font color='red'>**发送方**</font>，调用<font color='red'>**`bus.$emit`**</font>('事件名称',要发送的数据) 方法<font color='red'>**触发自定义事件**</font>

3、在数据<font color='red'>**接收方**</font>，调用<font color='red'>**`bus.$on`**</font>('事件名称',事件处理函数)方法<font color='red'>**注册一个自定义事件**</font>

![img](https://pic2.zhimg.com/80/v2-7a52831742b4cee23350270a2f905295_1440w.webp)

![](C:\Users\shizeyu\Desktop\notes\Ajax-vue\Snipaste_2022-10-09_14-12-40.png)

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

# 八. ref引用

## 8.1什么是ref引用

`ref`用来辅助开发者在<font color='red'>**不依赖`jQuery`的情况下**</font>，获取`DOM`元素或组件的引用。

每个`vue`的组件实例上，都包含一个<font color='red'>**`$refs`对象**</font>，里面存储着对应的DOM元素或组件的引用。默认情况下，<font color='red'>**组件的`$refs`指定一个空对象**</font>

> $开头的都是Vue内置的

## 8.2 ref获取dom引用

1. 在`DOM`标签内设置`ref `名字 

   > 尽量名字以`Ref`结尾方便查看

2. `this.$refs.名字`     获取标签 eg：`this.$refs.h1Ref`

```vue
<template>
  <div>

    <!-- 起ref名字 名字任意 -->
    <h1 ref="h1">App根目录</h1>
    <h2 ref="h2">aa</h2>
    <button @click="show">打印this</button>
  </div>
</template>

<script>
export default {

  methods:{
    show(){

      //通过this.$refs.名字获取标签 this是这个vue实例
      console.log(this.$refs.h1);
      this.$refs.h1.style.color='red'
    }
  }
    

}
</script>
```

## 8.3 使用ref引用组件实例

如果想要使用`ref`<font color='red'>**引用页面上的组件实例**</font>，则可以按照如下的方式进行操作

> 尽量名字以`Ref`结尾方便查看

1. 先对要引用的组件添加`ref`      eg：`<My-Count ref="counterRef"></My-Count>`
2. 通过`this.$refs.名字.方法()`来运行子组建的方法  eg： `this.$refs.counterRef.add()` 
3. 也广泛用于**便捷**获取组件的值或对值操作（比子父传递和兄弟传递更方便）   eg：`this.$refs.counterRef.count = 0`

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

## 8.4 this.$nextTick(cb)

官方挂载方法，组件的<font color='red'>**`$nextTick(cb)`**</font>方法，会把cb回调<font color='red'>**推迟到下一个`DOM`更新周期之后执行**</font>。通俗的理解是：等组件的`DOM`更新完成之后，再执行`cb`回调函数，从而能保证`cb`回调函数可以操作到最新的`DOM`

```
this.$nextTick(()=>{
            this.$refs.iptRef.focus()
          })
```

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



# 九. 动态组件 components

## 9.1 什么是动态组件

动态组件指的是<font color='red'>**动态切换组件的显示与隐藏**</font>

## 9.2 如何实现动态组件的渲染

vue提供了一个内置的**`<components>`**组件，专门用来实现动态组件的渲染

> `componment`作为一个占位符来使用
>
> `is` 属性的值，表示要渲染的组件的名字



```vue
<template>
  <div>
    <div>
      <h1>App组件</h1>
      <button @click="showLeft">切换为Left组件</button>
      <button @click="showRight">切换为Right组件</button>
    </div>
    <div class="www">
      <components :is="comName"></components>  
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

## 9.3 使用keep-alive保持状态

当组件被切换到其他组件在切换回来的时候是，**组件会重新创建新的组件，原来的组件被销毁**，原来的数据跟着销毁，为了保持原来的数据和组件不被销毁可以使用**keep-alive将组件缓存**

> `keep-alive` 可以把内部的组件进行缓存，而不是销毁组件

```text
<keep-alive>
      <components :is="comName"></component>  
</keep-alive>
```

 被缓存：

![](C:\Users\shizeyu\Desktop\notes\Ajax-vue\Snipaste_2022-10-19_14-56-38.png)

## 9.4 keep-alive对应的生命周期函数

当组件<font color='red'>**被缓存**</font>时，会自动触发组件的<font color='red'>**`deactivated`**</font>生命周期

当组件<font color='red'>**被激活**</font>时，会自动触发组件的<font color='red'>**`activated`**</font>生命周期

<font color='red'>**这些生命周期写在组件中**</font>

![](C:\Users\shizeyu\Desktop\notes\Ajax-vue\Snipaste_2022-10-19_16-02-08.png)

> 当组件第一次被创建的时候，既会执行 `created` 生命周期，也会执行 `activated` 生命周期
>
> 当时，当组件被激活时，只会触发 `activated` 生命周期，不再触发 `created`。因为组件没有被重新创建

![](C:\Users\shizeyu\Desktop\notes\Ajax-vue\Snipaste_2022-10-19_16-00-12.png)



## 9.5 keep-alive的include属性

指定哪些组件可以缓存，即那个组件可以由`keep-alive`

`include`属性用来指定：只有<font color='red'>**名称匹配的组件**</font>会被缓存。多个组件名之间使用<font color='red'>**英文的逗号分隔**</font>

`exclude`属性表示不被缓存的组件，<font color='red'>**`include`和`exclude`不能同时使用**</font>

```text
<keep-alive include="myLefr,MyRight">
      <component :is="comName"></component>  
</keep-alive>
```

## 扩展-组件name属性的影响

> 如果在“声明组件”的时候，没有为组件指定name名称，则组件队的名称默认就是“注册时候的名称”即

![](C:\Users\shizeyu\Desktop\notes\Ajax-vue\Snipaste_2022-10-19_16-28-50.png)

> 当提供了name属性之后，组件的名称就是name属性的值

![](C:\Users\shizeyu\Desktop\notes\Ajax-vue\Snipaste_2022-10-19_16-29-28.png)

> 组件的“注册名称”的主要应用场景是，以标签的形式，把注册号的组件，渲染和使用到页面结构中
>
> 组件声明时候的name名称的主要应用场景：结合keep-alive标签实现缓存功能，以及调试工具中看到组件的name名称

<font color='red'>**设置了`name`的组件用`keep-alive`的`include`和`exclude`要使用`name`的名称而不是注册名称**</font>





# 十. 插槽（#）

## 10.1 什么是插槽

<font color='red'>**插槽（Slot）**</font>是 vue 为<font color='red'>**组件的封装者**</font>提供的能力。允许开发者在封装组件时，把<font color='red'>**不确定的、希望由用户指定的部分**</font>定义为插槽。可以把插槽认为是组件封装期间，为用户预留的内容的占位符。

> 在使用封装好的组件时可以diy组件，方便复用

![](C:\Users\shizeyu\Desktop\notes\Ajax-vue\14538900e74d087cabf71e76eaef81b5-4.png)

##  10.2 体验插槽的基础用法

在封装组件时，可以通过 **`<slot>`** 元素定义插槽，从而为用户预留内容占位符。示例代码如下：

```vue
<!-- left组件调用者	 -->
<template>
  <div id="app">
    <left>
      <p>插槽测试</p>
    </left>
  </div>
</template>

<script>
import left from "./components/left.vue";
export default {
  name: "App",
  components: {
    left,
  },
};
</script>
```

```vue
<!-- left组件 -->
<tem<!-- 声明一个插槽区域 -->plate>
  <div>
    <div>count:{{ count }}</div>
    <button @click="count += 1">+1</button>
    <!-- 声明一个插槽区域 -->
    <slot></slot>
  </div>
</template>
```

###  （1）没有预留插槽的内容会被丢弃

如果在封装组件时<font color='red'>**没有预留任何 `<slot>` 插槽**</font>，则用户提供的任何<font color='red'>**自定义内容都会被丢弃**</font>。示例代码如下：

![](C:\Users\shizeyu\Desktop\notes\Ajax-vue\Snipaste_2022-10-20_10-48-41.png)

![](C:\Users\shizeyu\Desktop\notes\Ajax-vue\Snipaste_2022-10-20_10-48-48.png)

### （2）后备内容（默认内容）

封装组件时，可以为预留的 `<slot>` 插槽提供<font color='red'>**后备内容（默认内容）**</font>。如果组件的使用者没有为插槽提供任何内容，则后备内容会生效。示例代码如下：

![](C:\Users\shizeyu\Desktop\notes\Ajax-vue\Snipaste_2022-10-20_10-51-08.png)

![](C:\Users\shizeyu\Desktop\notes\Ajax-vue\Snipaste_2022-10-20_10-50-47.png)

![](C:\Users\shizeyu\Desktop\notes\Ajax-vue\Snipaste_2022-10-20_10-50-54.png)

## 10.3 具名插槽

如果在封装组件时<font color='red'>**需要预留多个插槽节点**</font>，则需要为每个 `<slot>` 插槽指定<font color='red'>**具体的 `name` 名称**</font>。这种<font color='red'>**带有具体名称的插槽叫做“具名插槽”**</font>。示例代码如下：

> 温馨提醒：官方规定，每个插槽都有一个`name` 名称，如果没有指定 `name` 名称的插槽，会有隐含的名称叫做 **“`default`”**。

![](C:\Users\shizeyu\Desktop\notes\Ajax-vue\Snipaste_2022-10-20_10-22-27.png)

### （1） 为具名插槽提供内容

在向具名插槽提供内容的时候，我们需要指明插槽，使用 **`v-slot`** 。

但需要在一个<font color='red'> **`<template>`** </font>元素上使用 **`v-slot`** 指令，并以 **`v-slot`** 的参数的形式提供其名称。示例代码如下：

1. 如果要把内容填充到指定名称的插槽中，需要使用`v-slot:`这个指令

2. `v-slot:`后面要跟上插槽的名字`name`

3. `v-slot:`指令不能直接用在元素上身上，必须用在`template`标签上，或者<font color='red'>**自定义组件**</font>

4. `template`这个标签，它是一个虚拟的标签，只起到包裹作用，但是它是不会被渲染为任何实质性的`html`元素
5. `v-slot:`指令的简写形式是`#`

>`<template>`组件并不渲染也不显示，只是在这起到包裹作用

![](C:\Users\shizeyu\Desktop\notes\Ajax-vue\Snipaste_2022-10-20_10-35-09.png)



### （2） 具名插槽的简写形式（#）

跟 `v-on` 和 `v-bind` 一样，`v-slot` 也有缩写，即把参数之前的所有内容 (`v-slot:`) 替换为字符 `#`。例如 `v-slot:header`

可以被重写为` #header`：

![](C:\Users\shizeyu\Desktop\notes\Ajax-vue\Snipaste_2022-10-20_10-44-13.png)



## 10.4 作用域插槽

在封装组件的过程中，<font color='red'>**可以为预留的 `<slot>` 插槽绑定 `props` 数据，这种带有 `props `数据的 `<slot>` 叫做“作用域插槽”**</font>。可以使用 `v-slot:` 的形式，接收作用域插槽对外提供的数据。

> **实质是子传父，传递过来之后是对象的形式，接收形参通常为`scope`**

示例代码如下：

```vue
<!-- left子组件 -->
<template>
  <div>
    <div>count:{{ count }}</div>
    <button @click="count += 1">+1</button>
    <!-- 声明一个插槽区域 -->
    <slot name="default" :msg="list">
      <p>默认内容</p>
    </slot>
  </div>
</template>

<script>
export default {
  name: "myleft",
  data() {
    return {
      list: {
        a: 1,
        b: 2,
      },
    };
  },
};
</script>
```

```vue
<!-- 父组件名 -->
<template>
  <div id="app">
    <!-- 组件名 -->
    <left>
      <template #default="scope">
        <p>插槽测试</p>
        <p>{{ scope }}</p>
      </template>
    </left>
  </div>
</template>

<script>
import left from "./components/left.vue";

export default {
  name: "App",
  components: {
    left,
  },
};
</script>
```

![](C:\Users\shizeyu\Desktop\notes\Ajax-vue\Snipaste_2022-10-20_11-12-34.png)

![在这里插入图片描述](https://img.php.cn/upload/article/000/000/024/8b03904cbb5f21328af0fc53950d8c47-11.png)

![在这里插入图片描述](https://img.php.cn/upload/article/000/000/024/8b03904cbb5f21328af0fc53950d8c47-12.png)

###  解构插槽 Prop

作用域插槽对外提供的数据对象，可以使用<font color='red'>**解构赋值**</font>简化数据的接收过程。示例代码如下：



![在这里插入图片描述](https://img.php.cn/upload/article/000/000/024/0043aea935e524a0277643fb040033bd-13.png)





# 十一. 自定义指令

## 1 什么是自定义指令

vue 官方提供了 v-text、v-for等常用指令，除此之外vue还允许开发者自定义指令

## 2 自定义指令的分类

vue 中的自定义指令分为两类，分别是：

- <font color='red'>**私有自定义指令**</font>
- <font color='red'>**全局自定义指令**</font>

## 3 私有自定义指令

在每个 `vue` 组件中，可以在 <font color='red'>**`directives`**</font> 节点下声明<font color='red'>**私有自定义指令**</font>。示例如下：

### * bind函数

**`bind`指令当指令第一次被绑定到元素上的时候，会立即触发`bind`指令**

调用的时候需要加上 `v-` 前缀

形参中的 el 是绑定了此指令的，原生的 DOM 对象

```
directives: {
	color: {
		//为绑定到的 HTML 元素设置红色的文字
		bind(el) {
			// 形参中的 el 是绑定了此指令的，原生的 DOM 对象
			el.style.color = 'red'
		}
	}
}
```

```vue
<template>
  <div>
    <div v-color>count:{{ count }}</div>
  </div>
</template>

<script>
export default {
  name: "myleft",
  directives: {
    color: {
      //为绑定到的 HTML 元素设置红色的文字
      bind(el) {
        // 形参中的 el 是绑定了此指令的，原生的 DOM 对象
        el.style.color = "red";
      },
    },
  },
};
</script>
```

### 若绑定自定义值-使用binding

传入变量，若向直接给值要加单引号

查看`binding`的值发现是一个对象，接收的值都在`value`内所以使用`binding.value`来获取绑定的值

```vue
<template>
  <div>
    <!-- 传入变量color，若向直接给值要加单引号 -->
    <div v-color="color">count:{{ count }}</div>
    <div v-color="'red'">1234567</div>
  </div>
</template>

<script>
export default {
  name: "myleft",
  data() {
    return {
      color: "blue",
    };
  },
  directives: {
    color: {
      //为绑定到的 HTML 元素设置红色的文字
      //建议使用 binding 为形参名来接收被绑定的值
      bind(el, binding) {
        // 形参中的 el 是绑定了此指令的，原生的 DOM 对象
        el.style.color = binding.value;

        console.log(binding);
      },
    },
  },
};
</script>

<style>
</style>
```

![](C:\Users\shizeyu\Desktop\notes\Ajax-vue\Snipaste_2022-10-20_15-58-29.png)

### * update函数

<font color='red'>**`bind`函数只调用一次**</font>，当指令第一次绑到元素时调用，<font color='red'>**当 `DOM` 更新时 `bind` 函数不会被触发**</font>。<font color='red'>**`update`**</font> 函数会在<font color='red'>**每次 `DOM` 更新时**</font>被调用，示例如下：

> `update`只有当`DOM`值变化才会触发，当一开始的时候不触发，所以`bind`和`update`结合使用

```
directives: {
    color: {
      //为绑定到的 HTML 元素设置红色的文字
      //   bind当指令第一次绑到元素时调用
      bind(el, binding) {
        // 形参中的 el 是绑定了此指令的，原生的 DOM 对象
        el.style.color = binding.value;

        console.log(binding);
      },
      //   updata 函数会在每次 DOM 更新时被调用
      update(el, binding) {
        el.style.color = binding.value;
      },
    },
  },
```

```vue
<template>
  <div>
    <!-- 按键换色 -->
    <button @click="color = 'pink'">换色</button>
    <div v-color="color">count:{{ count }}</div>
    <div v-color="'red'">1234567</div>
  </div>
</template>

<script>
export default {
  name: "myleft",
  data() {
    return {
      color: "blue",
    };
  },
  directives: {
    color: {
      //为绑定到的 HTML 元素设置红色的文字
      //   bind当指令第一次绑到元素时调用
      bind(el, binding) {
        // 形参中的 el 是绑定了此指令的，原生的 DOM 对象
        el.style.color = binding.value;

        console.log(binding);
      },
      //   updata 函数会在每次 DOM 更新时被调用
      update(el, binding) {
        el.style.color = binding.value;
      },
    },
  },
};
</script>

<style>
</style>
```

### 函数简化

如果`bind`和`update`函数中的<font color='red'>**逻辑完全相同**</font>，则<font color='red'>**对象格式**</font>的自定义指令可以简写成<font color='red'>**函数形式**</font>：

```
directives: {
    color(el, binding) {
      el.style.color = binding.value;
    },
  },
```

```
//旧
directives: {
    color: {
      //为绑定到的 HTML 元素设置红色的文字
      //   bind当指令第一次绑到元素时调用
      bind(el, binding) {
        // 形参中的 el 是绑定了此指令的，原生的 DOM 对象
        el.style.color = binding.value;

        console.log(binding);
      },
      //   updata 函数会在每次 DOM 更新时被调用
      update(el, binding) {
        el.style.color = binding.value;
      },
    },
  },
```

完整代码：

```vue
<template>
  <div>
    <!-- 按键换色 -->
    <button @click="color = 'pink'">换色</button>
    <div v-color="color">count:{{ count }}</div>
    <div v-color="'red'">1234567</div>

    <!-- <button @click="count += 1">+1</button> -->
    <!-- 声明一个插槽区域 -->
    <!-- <slot name="default" :msg="list">
      <p>默认内容</p>
    </slot> -->
  </div>
</template>

<script>
export default {
  name: "myleft",
  data() {
    return {
      color: "blue",
      count: 0,
      list: {
        a: 1,
        b: 2,
      },
    };
  },
  directives: {
    color(el, binding) {
      el.style.color = binding.value;
    },
  },
};
</script>

<style>
</style>
```





## 4 全局自定义指令 

全局共享的自定义指令需要通过 “vue.directive()” 进行声明，

<font color='red'>**书写在`main.js`文件内**</font>

示例代码：

```
Vue.directive('过滤器的名字', function () {    })
```

```js
// 全局自定义指令
Vue.directive('color', (el, binding) => {
  el.style.color = binding.value
})
```



# 十二. ESLint

### 什么是[eslint](https://so.csdn.net/so/search?q=eslint&spm=1001.2101.3001.7020)

[ESLint](http://eslint.cn/) 是一个代码检查工具，用来检查你的代码是否符合指定的规范（例如： = 的前后必须有一个空格）。

![](C:\Users\shizeyu\Desktop\notes\Ajax-vue\Snipaste_2022-10-24_09-56-29.png)

```
// prettier 配置
"eslint.alwaysShowStatus": true,
"prettier.trailingComma": "none",
"prettier.semi": false,
// 每行文字合数超出此限制会被迫换行
"prettier.printWidth": 300,
// 使用单引号替换双引号
"prettier.singleQuote": true,
"prettier.arrowParens": "avoid",
// 设置.vue 文件中，HTML代码的格式化插件
"vetur.format.defaultFormatter.html": "js-beautify-html",
"vetur.ignoreProjectWarning": true,
"vetur.format.defaultFormatterOptions": {
"prettier": {
"trailingComma":"none",
"semi":false,
"singleQuote":true,
"arrowParens":"avoid",
"printWidth":300
},
"js-beautify-html": {
"wrap_attributes": "force-expand-multiline"
}
}
```

```
//  EsLint 配置
"editor.codeActionsOnSave": {
"source.fixAll": true
},
```

![](C:\Users\shizeyu\Desktop\notes\Ajax-vue\Snipaste_2022-10-24_14-00-03.png)

![](C:\Users\shizeyu\Desktop\notes\Ajax-vue\Snipaste_2022-10-24_14-23-05.png)

![](C:\Users\shizeyu\Desktop\notes\Ajax-vue\Snipaste_2022-10-24_14-23-32.png)

![](C:\Users\shizeyu\Desktop\notes\Ajax-vue\Snipaste_2022-10-24_14-24-12.png)









# vue路由

# 一. 前端路由的概念和原理

## 1. 什么是路由

路由（英文：router）就是<font color='red'>**对应关系**</font>。

## 2. SPA 与前端路由

SPA 指的是一个 web 网站只有唯一的一个 HTML 页面，所有组件的展示与切换都在这唯一的一个页面内完成。
此时，不同组件之间的切换需要通过前端路由来实现。

结论：在 SPA 项目中，不同功能之间的切换，要依赖于前端路由来完成！

## 3. 什么是前端路由

通俗易懂的概念：<font color='red'>**Hash 地址**</font>与<font color='red'>**组件之间**</font>的<font color='red'>**对应关系。**</font>

> Hash地址 就是 锚链接 #

>`注意1`：在 hash 地址中，`/` 后面的参数项，叫做“路径参数”。																			在路由的“参数对象”中，需要使用 `this.$route.params` 来访问路径参数

> `注意2`：在 hash 地址中，`？` 后面的参数项，叫做“查询参数”。																			在路由的“参数对象”中，需要使用 `this.$route.query` 来访问查询参数

> `注意3`：在 `this.$route` 中，`path` 只是路径部分，`fullPath` 是完整的地址

> eg：`/movie/2?name=zs&age=20` 是`fullPath`																										`/movie/2` 是`path`的值

## 4. 前端路由的工作方式

① 用户点击了页面上的<font color='red'>**路由链接**</font>
② 导致了<font color='red'>**URL 地址栏**</font> 中的<font color='red'>**Hash 值**</font>发生了变化
③ <font color='red'>**`前端路由`监听了到 Hash 地址的变化**</font>
④ 前端路由把当前 <font color='red'>**Hash 地址对应的组件**</font>渲染都浏览器中

![在这里插入图片描述](https://img-blog.csdnimg.cn/67918c1647ed42d0a2990763c08b6b0b.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBAMDU0MzE=,size_20,color_FFFFFF,t_70,g_se,x_16)

> 结论：前端路由，指的是 Hash 地址与组件之间的对应关系！

## 5. 实现前端路由(原生路由切换原理)

步骤1：通过`component`标签，结合 变量`comName` 动态渲染不同的组件。示例代码如下：

![在这里插入图片描述](https://img-blog.csdnimg.cn/c74f2d6985044d4eb80bfbe907822497.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBAMDU0MzE=,size_20,color_FFFFFF,t_70,g_se,x_16)

步骤2：在 `App.vue` 组件中，为 链接添加对应的 `hash` 值：

![在这里插入图片描述](https://img-blog.csdnimg.cn/a5e19fd150e346ea93432d582cd85e31.png)

步骤3：在 `created` 生命周期函数中，监听浏览器地址栏中 `hash `地址的变化，动态切换要展示的组件的名称：

> 这里不用`click`事件是因为如果手动更改`hash`值的话不会触发`click`
>
> 自己封装事件是非常麻烦的，所以常用vue-router

![在这里插入图片描述](https://img-blog.csdnimg.cn/2dcff9df7db749d89969f0f961d50753.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBAMDU0MzE=,size_17,color_FFFFFF,t_70,g_se,x_16)

完整代码：

```vue
<template>
  <div class="app-container">
    <h1>App 根组件</h1>

    <a href="#/home">首页</a>
    <a href="#/movie">电影</a>
    <a href="#/about">关于</a>
    <hr />
    <component :is="comName"></component>
  </div>
</template>

<script>
// 导入组件
import Home from '@/components/Home.vue'
import Movie from '@/components/Movie.vue'
import About from '@/components/About.vue'

export default {
  name: 'App',
  data() {
    return {
      // 在动态组件的位置，要展示的组件的名字，值必须是字符串
      comName: 'Home'
    }
  },
  created() {
    // 只要当前的 App 组件一被创建，就立即监听 window 对象的 onhashchange 事件
    window.onhashchange = () => {
      console.log('监听到了 hash 地址的变化', location.hash)
      switch (location.hash) {
        case '#/home':
          this.comName = 'Home'
          break
        case '#/movie':
          this.comName = 'Movie'
          break
        case '#/about':
          this.comName = 'About'
          break
      }
    }
  },
  // 注册组件
  components: {
    Home,
    Movie,
    About
  }
}
</script>

<style lang="less" scoped>
.app-container {
  background-color: #efefef;
  overflow: hidden;
  margin: 10px;
  padding: 15px;
  > a {
    margin-right: 10px;
  }
}
</style>


```

> 这里使用a标签进行定位，会用到a标签的锚链接的功能，所以在访问的路径的前面需要加个“#”

![在这里插入图片描述](https://img-blog.csdnimg.cn/59d461ae94f34c10bb4e9612ad37c6d7.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBAMDU0MzE=,size_20,color_FFFFFF,t_70,g_se,x_16)

> `App.vue`组件的生命周期函数`created()`方法中，通过`window.onhashchange`事件，即监听导航栏的地址是否发生变化，将相应的组件通过动态绑定的方式，更新到component组件中。

![在这里插入图片描述](https://img-blog.csdnimg.cn/5038fc75bcd44739abf06bf5313e328a.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBAMDU0MzE=,size_20,color_FFFFFF,t_70,g_se,x_16)

> `location`是包含记录网址hash值的事件，打印`location`：

![](C:\Users\shizeyu\Desktop\notes\Ajax-vue\Snipaste_2022-10-26_10-57-53.png)

------

### location.hash详解

1.存在形式及意义

一般情况下为URL后 "#" 及其后面一部分组成，如`http://www.test.com/#/something`，

其中`http://www.test.com`为真实的路径，而#/something则为网页中的位置，称之为锚点

在访问锚点时会自动跳刀锚点所在的网页位置，通常有两种方式作为锚点

`<a name="something"></a>`

`<element id="something"></element>`

以上两种均可通过http://www.test.com/#/something使页面滚动到该元素的位置

**2.hash的读写**

location.hash可读可写的

```commonlisp
//当前URL为http://www.test.com/#/something
location.hash;		        //输出 #/something
 
location.hash = '#/test1';	//http://www.test.com/#/test1,并且会新增一条历史记录
```

> 在对hash写时有个需要注意的地方，如下所示

```commonlisp
//当前URL为http://www.test.com/
location.hash = "#/test"	//http://www.test.com/#/test
locationl.hash = "/#/test"	//http://www.test.com/#/#/test
```

当写入第一个字符不为为 "#" 时会自动生成一个 "#" 在字符串之前，再把字符串追加到生成的#后面

这样会造成有两个#,此时location.hash输出 "#/#/test"

**3.onhashchange事件**

在hash值发生变化时会触发该事件

```js
window.onhashchange = function(e){
	console.log(e);
}
```

总结：

location.hash与HTML5 history类似，都能够在改变页面的URL而不会引起浏览器的重载

但是location.hash支持比较早的浏览器，而history是在HTML5的新API，可能某些较早的浏览器不支持

因此在vue-router中对此做了两种模式，即history模式与hash模式可以适应不同的浏览器

具体解释之后更新vue-router的原理分析

------





# 二. vue-router 的基本使用

## 2.1 什么是 `vue-router`

<font color='red'>`vue-router`</font>是`vue.js`官方给出的<font color='red'>路由解决方案</font>。它只能结合`vue`项目进项使用，能够轻松的管理 `SPA` 项目中的组件的切换。

vue-router的官方文档地址：

[vue-router]: http://router.vuejs.org/zh/

## 2.2 `vue-router `安装和配置的步骤

> 若在创建项目的时候选择了vue-router插件，则这些步骤可以省略

① 安装 vue-router 包

<font color='red'>**② 创建路由模块**</font>(js文件)

③ 导入并挂载路由模块

④ 生命<font color='red'>**路由链接**</font>和<font color='red'>**占位符**</font>

### 2.2.1 在项目中安装 `vue-router`

> vue2的vue-router 安装需要指定版本，否则会默认下载最新版本，最新版本只支持vue3

在`vue2`项目中，安装`vue-router`的命令如下：

```
npm i vue-router@3.5.2 -S
```



### 2.2.2 创建路由模块

> 若在创建项目的时候选择了vue-router插件，则这些步骤可以省略

在<font color='red'>**`src`**</font>源代码目录下，新建<font color='red'>**`router/index.js`**</font>路由模块，并初始化如下的代码：

```js
// 1. 导入 Vue 和 VueRouter 的包
import Vue from "vue";
import VueRouter from "vue-router";

// 2. 调用 Vue.use() 函数，把 VueRouter 安装为 Vue 的插件
// Vue.use() 函数的作用就是安装插件的
Vue.use(VueRouter)

// 3. 创建路由的实例对象
const router =new VueRouter()

// 4. 向外共享路由的实例对象，让其他组件可以使用
export default router
```

![](C:\Users\shizeyu\Desktop\notes\Ajax-vue\Snipaste_2022-10-26_16-36-55.png)

我们配置完路由还需要对路由进行注册，注册完就可以使用了

注册就是在main.js文件下输入两行代码即可

> `new vue`是项目的实例，将`router`实例对象加到项目的实例里
>
> `router:router`   等同于 `router`

>第一处的路径也可以直接写成 `@/router` ，因为 在进行模块漫画导入的时候，如果给定的文件夹，则默认导入这个文件下的，名字叫做 `index.js` 的文件

![](C:\Users\shizeyu\Desktop\notes\Ajax-vue\Snipaste_2022-10-26_17-01-27.png)



## 2.3 在路由模块中声明路由的对应关系

路由模块：router/index.js

> router-view是渲染位置，但除去在根组件app.vue中的特殊情况，可以直接使用，在组件中嵌套的话使用各种嵌套渲染使用router-view时候结合`3.2 嵌套路由`通过子路由来实现

### 路由链接`<router-view>`（渲染位置）

```vue
<template>
  <div class="app-container">
    <h1>App2 组件</h1>
    
    <a href="#/home">首页</a>
    <a href="#/movie">电影</a>
    <a href="#/about">关于</a>
 
    <hr />
    
    <!-- 只要在项目中安装和配置了 vue-router 就可以使用 vue-router 组件了 -->
    <!-- 它的作用为: 占位符 -->
    <router-view></router-view>
    
  </div>
</template>
```

![](C:\Users\shizeyu\Desktop\notes\Ajax-vue\Snipaste_2022-10-27_15-18-13.png)

在路由模块中导入需要切换的组件,并且声明它的路由规则 ( 对应关系 ) 

> hash值和组件的对应关系
>
> path中的路径必须省略掉 # 号否则报错

![](C:\Users\shizeyu\Desktop\notes\Ajax-vue\Snipaste_2022-10-27_15-38-47.png)

```js
// src/router /index.js 就是当前项目的路由模块
// 导入 Vue 和 VueRouter 的包
import Vue from 'vue'
import VueRouter from "vue-router"
 
// 导入需要的组件
import Home from "../components/Home.vue"
import Movie from "../components/Movie.vue"
import About from "../components/About.vue"
 
// 调用 Vue.use() 函数 把 VueRouter 安装为 Vue 的插件
Vue.use(VueRouter)
 
// 创建路由的实例对象
const router = new VueRouter({
  // routers 是一个数组 作用为 定义 "hash地址" 与 "组件" 之间的对应关系
  // 必须省略掉 # 号
  routes: [
    // 理由规则
    {path: '/home', component: Home},
    {path: '/movie', component: Movie},
    {path: '/about', component: About}
  ],
})
 
// 向外共享路由的实例对象
export default router
```

### 占位符`<router-link>`（hash跳转）

<font color='red'>**在安装了 `vue-router` 后,可以使用 `<router-link>` 标签替代 `<a>` 标签**</font>

<font color='red'>**使用 `<router-link>` 标签时,链接推荐省略 "#" 号**</font>

![](C:\Users\shizeyu\Desktop\notes\Ajax-vue\Snipaste_2022-10-27_15-51-58.png)

```vue
<template>
  <div class="app-container">
    <h1>App 根组件</h1>

    <!-- 当安装了 vue-router 后 就可以使用 router-link 来替代普通的 a 链接了 -->
    <!-- <a href="#/left">左</a> -->
    <router-link to="/left">左</router-link>
    <a href="#/right">右</a>
    <hr />

    <!-- 只要在项目中安装并配置了 vue-router ，就可以使用 router-view 这个组件了 -->
    <!-- 它的作用很单纯：占位符 -->
    <router-view></router-view>
  </div>
</template>

<script>
export default {
  name: 'App',
}
</script>

<style lang="less" scoped>
.app-container {
  background-color: #efefef;
  overflow: hidden;
  margin: 10px;
  padding: 15px;
  > a {
    margin-right: 10px;
  }
}
</style>
```

>`<router-link>`改变`hash`值跳转，然后自动去`index.js`的`routes`中去查找渲染的组件，然后component指定的组件会渲染到路由链接`<router-view>`的位置上
>
>在调用的组件内无需再引入，因为再`index.js`中已经调用

------





# 三. vue-router 的常见用法

## 3.1 路由重定向

<font color='red'>路由重定向</font>指的是：用户在访问<font color='red'>地址 A </font>的时候，<font color='red'>强制用户跳转</font>到地址 C ，从而展示特定的组件页面。通过路由规则的<font color='red'> `redirect` </font>属性，指定一个新的路由地址，可以很方便地设置路由的重定向：

> 常用于解决 `/`  地址问题

![](C:\Users\shizeyu\Desktop\notes\Ajax-vue\Snipaste_2022-10-27_16-09-39.png)

## 3.2 嵌套路由

通过路由实现<font color='red'>组件的嵌套展示</font>，叫做嵌套路由。

通过 children 属性声明子路由规则:

```
/user/johnny/profile                     /user/johnny/posts
+------------------+                  +-----------------+
| User             |                  | User            |
| +--------------+ |                  | +-------------+ |
| | Profile      | |  +------------>  | | Posts       | |
| |              | |                  | |             | |
| +--------------+ |                  | +-------------+ |
+------------------+                  +-----------------+
    父级路由链接                   内还有子级路由链接显示子级模板
```

### 3.2.1 声明子级路由链接和占位符

> 子级组件内

![](C:\Users\shizeyu\Desktop\notes\Ajax-vue\Snipaste_2022-10-27_16-36-02.png)

```vue
<template>
  <div class="app-container">
    <h1>about组件</h1>

    <!-- 子级路由链接 -->
    <router-link to="/about/tab1">tab1</router-link>
    <router-link to="/about/tab2">tab2</router-link>
    <hr />

    <!-- 子级路由占位符 -->
    <router-view></router-view>
  </div>
</template>

<script>
export default {}
</script>

<style lang="less" scoped>
.app-container {
  background-color: aqua;
  overflow: hidden;
  margin: 10px;
  padding: 15px;
  > a {
    margin-right: 10px;
  }
}
</style>

```

### 3.2.2 通过 children 声明嵌套路由的规则

在 `src/router/inder.js`路由模块中，导入需要的组件，并使用 <font color='red'>`children`属性</font>声明嵌子路由规则

>子级路由规则中，path尽量不要‘/’

![](C:\Users\shizeyu\Desktop\notes\Ajax-vue\Snipaste_2022-10-27_16-47-34.png)

```js
// 1. 导入 Vue 和 VueRouter 的包
import Vue from "vue";
import VueRouter from "vue-router";

// 导入需要的组件
import left from "@/components/left.vue"
import right from "@/components/right.vue"
import about from "@/components/about.vue"

import tab1 from "@/components/tab/tab1.vue"
import tab2 from "@/components/tab/tab2.vue"


// 2. 调用 Vue.use() 函数，把 VueRouter 安装为 Vue 的插件
Vue.use(VueRouter)

// 3. 创建路由的实例对象
const router =new VueRouter({
  // routes 是一个数组，作用：定义 “ hash 地址 ” 与 “组件” 之间的对应关系
  routes:[
    // 重定向路由规则
    {
      path:'/',redirect:'/right'
    },
    {
      path:'/left',component: left
    },
    {
      path:'/right',component: right
    },
    {      // about 页面的路由规则（父级路由规则）
      path:'/about',
      component: about,
      // redirect:'/about/tab1',
      children:[   // 1. 通过 children 属性，嵌套生命子级路由规则
        // 子级路由规则中，path尽量不要‘/’
        {path:'/',redirect:'/about/tab1'},
        { path:'tab1', component:tab1 }, // 2. 访问 /about/tab1 时，展示 tab1 组件
        { path:'tab2', component:tab2 },

      ]
    },

  ]
})

// 4. 向外共享路由的实例对象
export default router

```

![](C:\Users\shizeyu\Desktop\notes\Ajax-vue\Snipaste_2022-10-27_16-52-57.png)



### 3.2.3 默认子路由

默认子路由：如果`children`数组中，某个路由规则的`path`值为空字符串，则这条路由规则，叫做“默认子路由”

> 与‘/’相似

![](C:\Users\shizeyu\Desktop\notes\Ajax-vue\Snipaste_2022-10-27_17-02-04.png)



## 3.3 动态路由匹配

动态路由指的是：把 `hash`地址中<font color='red'>可变得部分</font>定义为<font color='red'>参数项</font>，从而<font color='red'>提高路由规则的复用性</font>

在`vue-router`中使用<font color='red'>英文的冒号（:）</font>来定义路由的参数项。示例代码如下：

```js
// 路由中的动态参数以 : 进行声明，冒号后面的是动态参数的名称
{ path:'/movie/:id',component:Movie }

// 将以下三个路由规则合并为一个，提高了路由的复用性
{ path:'/movie/1',component:Movie }
{ path:'/movie/2',component:Movie }
{ path:'/movie/3',component:Movie }
```

（太麻烦了通常是用props）在``movie`组件内可以通过`{{ this.$route.params.mid }}`获得`mid`的值，`this.`可以省略

> `注意1`：在 hash 地址中，`/` 后面的参数项，叫做“路径参数”。																			在路由的“参数对象”中，需要使用 `this.$route.params` 来访问路径参数
>
> `注意2`：在 hash 地址中，`？` 后面的参数项，叫做“查询参数”。																			在路由的“参数对象”中，需要使用 `this.$route.query` 来访问查询参数
>
> `注意3`：在 `this.$route` 中，`path` 只是路径部分，`fullPath` 是完整的地址
>
> eg：`/movie/2?name=zs&age=20` 是`fullPath`																										`/movie/2` 是`path`的值

![在这里插入图片描述](https://img-blog.csdnimg.cn/78e8e7d6d7b8487eaf58bb21457f42ab.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBAQmxpenphcmTliY3nq68=,size_12,color_FFFFFF,t_70,g_se,x_16#pic_center)



## 3.4 为路由打开props传参

```js
// 在movie组件中添加props
//使用：来声明参数，参数名自取，在movie组件中，mid为props匹配的参数名
//在组件中定义props数组
  // 接收 props 数据
  props: ['mid'],
      
//在router中
  //可以为路由规则开启props传参，从而方便的拿到动态参数的值
   { path: '/movie/:mid', component: Movie, props: true },
```





## 3.5 声明式导航 & 编程式导航

在浏览器中，<font color='red'>点击链接</font>实现导航的方式，叫做<font color='red'>声明式导航</font>。例如：

- 普通网页中点击<font color='red'>`<a>`链接</font>、`vue`项目中点击<font color='red'>`<router-link>`</font>都属于声明式导航

在浏览器中，<font color='red'>调用 API 方式</font>实现导航的方式，叫做<font color='red'>编程式导航</font>。例如：

- 普通网页中点击<font color='red'>`location.href`</font>跳转到新页面的方式，属于编程式导航，但这是原生的方法 vue有自己的的API



### 3.5.1 vue-router 中编程式导航 API

vue-router 提供了许多编程式导航的 API，其中最常用的导航 API 分别是：

① this.$router.<font color='red'>push</font>('hash 地址')

- 跳转到指定的 hash 地址，并<font color='red'>增加</font>一条历史记录

② this.$router.<font color='red'>replace</font>('hash 地址')

- 跳转到指定的 hash 地址，并<font color='red'>替换掉当前的</font>历史记录

③ this.$router.<font color='red'>go</font>(数值 n )

- 实现导航历史的前进、后退

>  this.$route 是路由的“ 参数对象 ”
>
> this.$router 是路由的“ 导航对象 ”，他提供了很多导航功能

#### $router.push

增加一条历史记录

![](C:\Users\shizeyu\Desktop\notes\Ajax-vue\Snipaste_2022-10-31_16-18-09.png)

#### $router.replace

替换当前历史记录

![](C:\Users\shizeyu\Desktop\notes\Ajax-vue\Snipaste_2022-10-31_16-21-55.png)

#### $router.go

实现导航历史的前进、后退

> 如果后退的层数超过上限，则会原地不动 eg:$router.go(-100)

```vue
<template>
  <div class="back">
    <h1>right组件</h1>
    <button @click="postInfo">POST请求</button>
    <button @click="gotoGY">通过push跳转到关于</button>
    <button @click="gotoGY2">通过replace跳转到关于</button>
    <button @click="goback">通过go后退</button>
    <button @click="gofront">通过go前进</button>
  </div>
</template>

<script>
import axios from 'axios'
export default {
  methods: {
    async postInfo() {
      const { data: res } = await axios.post('/api/post', {
        name: 'zs',
        age: 20,
      })
      console.log(res)
      console.log(res.data)
    },
    gotoGY() {
      // 通过编程式导航API跳转到指定页面
      this.$router.push('/about')
    },
    gotoGY2() {
      // 通过编程式导航API跳转到指定页面
      this.$router.replace('/about')
    },
    goback() {
      //如果后退的层数超过上限，则会原地不动
      this.$router.go(-1)
    },
    gofront() {
      this.$router.go(1)
    },
  },
}
</script>

<style lang="less" scoped>
.back {
  background-color: deeppink;
  min-height: 200px;
  flex: 1;
}
</style>

```

#### $router.go 的简化方法

在实际开发中，一般只会前进或者后退一层页面，因此 vue-router 提供了如下两个简便方法：

① this.$router.<font color='red'>back</font>()

- 在历史记录中，<font color='red'>后退</font>到上一个页面

② this.$router.<font color='red'>forward</font>()

- 在历史记录中，<font color='red'>前进</font>到下一个页面

> 在行内使用编程式导航跳转的时候，`this`必须省略，否则报错，可以理解为this指向按钮报错

![](C:\Users\shizeyu\Desktop\notes\Ajax-vue\Snipaste_2022-10-31_16-36-16.png)

## 3.6 导航守卫

<font color='red'>导航守卫</font>可以<font color='red'>控制路由的访问权限</font>。示意图如下：

![](C:\Users\shizeyu\Desktop\notes\Ajax-vue\Screenshot_20221101_103802_tv.danmaku.bili.jpg)

### 3.6.1 全局前置守卫

每次发生路由的<font color='red'>导航跳转</font>时，都会触发<font color='red'>全局前置守卫</font>。因此，在全局前置守卫中，程序员可以对每个路由进行<font color='red'>访问权限</font>的控制：

```js
// 创建路由实例对象
const router = new VueRouter({ ... })
                              
// 调用路由实例对象的 beforeEach 方法，即可声明 "全局前置守卫"
// 每次发生路由导航跳转的时候，都会自动触发 fn 这个 "回调函数"
router.beforeEach(fn)                              
```

### 3.6.2 守卫方法的三个形参

<font color='red'>全局前置守卫</font>的回调函数中接受 3 个形参，格式为：

```js
// 创建路由实例对象
const router = new VueRouter({ ... })
                              
// 全局前置守卫
router.beforeEach((to, from, next) => {
    // to 是将要访问的路由的信息对象
    // from 是将要离开的路由的信息对象
    // next 是一个函数，调用 next() 表示放行，允许这次路由导航
    next() //没有 next() 所有跳转均会失效
})          
```

### 3.6.3  next 函数的 3 种调用方式

参考示意图，3种调用方式最终的导致的结果：

![](C:\Users\shizeyu\Desktop\notes\Ajax-vue\Screenshot_20221101_142405.jpg)

当前用户<font color='red'>拥有</font>后台主页的访问权限，直接放行：`next()`

当前用户<font color='red'>没有</font>后台主页的访问权限，<font color='red'>强制其跳转到当前页面</font>：`next('/login')`

当前用户<font color='red'>没有</font>后台主页的访问权限，<font color='red'>不允许跳转到后台页面</font>：`next(false)`

### 3.6.4 控制后台主页的访问权限

```js
// 创建路由实例对象
const router = new VueRouter({ ... })
                              
// 全局前置守卫
router.beforeEach((to, from, next) => {
	if(to.path === '/main') {
        const token = localStorage.getItem('token')
        if (token) {
            next()  // 访问的是后台主页，且有 token 的值，即有权限
        } else {
            next('login')  // 访问的是后台页面，但是没有 token 的值，即没有权限，跳转到登陆页面
        }
    } else {
        next()  // 访问的不是后台主页，直接放行
    }
})
```

可以手动加一个`token`

![](C:\Users\shizeyu\Desktop\notes\Ajax-vue\Snipaste_2022-11-01_15-00-08.png)









# 四. 后台管理案例











































# 补充知识



## * scss的基本使用

### SCSS-基本语法

内容：嵌套语法； &父[选择器](https://so.csdn.net/so/search?q=选择器&spm=1001.2101.3001.7020)；变量；mixins；模块

#### 1. 嵌套语法

和less一样，scss同样支持嵌套型的语法

![在这里插入图片描述](https://img-blog.csdnimg.cn/e241261e619e477880a9c487a99b0d7a.png#pic_center)

转化成css后

![在这里插入图片描述](https://img-blog.csdnimg.cn/3a0ee6d8d0344217908f80450e8c1248.png#pic_center)

#### 2. 变量

定义变量：sass使用$符号来标识变量
![在这里插入图片描述](https://img-blog.csdnimg.cn/42ffeedd035b4e40a6758d2aad33b55a.png#pic_center)
使用变量：
![在这里插入图片描述](https://img-blog.csdnimg.cn/576130a679b34ef2b8868b5c5f3b4452.png#pic_center)

#### 3. 父选择器 &

> & 用在嵌套的scss代码里，来引用父元素

```scss
.dashboard {
	&-container {
		margin: 30px;
	}
	&-text {
		font-size: 30px;
		line-height: 46px;
	}
}

==

.dashboard-container {
	margin: 30px; 
}
.dashboard-text {
	font-size: 30px;
	line-height: 46px; 
}
```

在嵌套 CSS 规则时，有时也需要直接使用嵌套外层的父选择器，例如，当给某个元素设定 hover 样式时，或者当 body 元素有某个 classname 时，可以用 & 代表嵌套规则外层的父选择器。
![在这里插入图片描述](https://img-blog.csdnimg.cn/6a04ca2fa20f43ba9555e1a3ad0283d9.png#pic_center)

```scss
.el-checkbox__inner {
  &:hover {
    border-color: #42b983;
  }
}

==

.el-checkbox__inner:hover {
    border-color: #42b983;
}
```



#### 4. 混合 mixins

mixins混入，是代码复用的方式
定义格式：@mixin 名称 { 代码 }
使用格式：include 名称
定义样式：

![在这里插入图片描述](https://img-blog.csdnimg.cn/3f444e92212d408c945c76dba3647b23.png#pic_center)

使用mixins
![在这里插入图片描述](https://img-blog.csdnimg.cn/55a8b793cb894c8081a69ad4c742efdd.png#pic_center)

#### 5. 模块

一个.scss文件就是一个模块，多个.scss文件之间可以相互引用。
例如：在base.scss定义变量，然后在test.scss中引入这个文件，就可以使用其中定义的变量了
![在这里插入图片描述](https://img-blog.csdnimg.cn/a5a8b62cd1124c059e793f2286a78a4c.png#pic_center)

格式：@import ‘./xxxx.scss’;
示例：新建base.scss，并定义变量

![在这里插入图片描述](https://img-blog.csdnimg.cn/dd284b99d313449da61ca7473e86711e.png#pic_center)

在test.scss中引入base.scss
![在这里插入图片描述](https://img-blog.csdnimg.cn/346467f571ef4737b3f884e55d20d622.png#pic_center)







https://blog.csdn.net/weixin_67745264/article/details/125141904

------



## * JavaScript

### [splice](https://so.csdn.net/so/search?q=splice&spm=1001.2101.3001.7020)()函数详解

> splice() 方法向/从[数组](https://so.csdn.net/so/search?q=数组&spm=1001.2101.3001.7020)中添加/删除项目，然后返回被删除的项目。
> 注释：该方法会改变原始数组。
>
> 参数：
>
> 1. index —— 必需。整数，规定添加/删除项目的位置，使用负数可从数组结尾处规定位置。
> 2. howmany —— 必需。要删除的项目数量。如果设置为 0，则不会删除项目。
> 3. item1, …, itemX —— 可选。向数组添加的新项目。
>
> 返回值
>
> 1. Array —— 包含被删除项目的新数组，如果有的话。

[https://blog.csdn.net/weixin_45726044/article/details/120151153](https://blog.csdn.net/weixin_45726044/article/details/120151153)

------

## *css

### display：flex和display: inline-flex区别

flex： 将对象作为弹性伸缩盒显示
inline-flex：将对象作为内联块级弹性伸缩盒显示

flex

```css
<style>
.main{
      background-color: #0f0;
      display: flex;/*父div设置该属性*/
    }               
    .main>div{
      width: 50px;
      height: 50px;
      border: 1px solid black;
    }
</style>
```

此时没有为父元素main设置宽度，默认为100%；

![img](https://upload-images.jianshu.io/upload_images/6522941-adacf1c29b59e976.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1000/format/webp)

inline-flex

```html
//样式
<style>
.main{
      background-color: #0f0;
      display: inline-flex;/*父div设置该属性*/
    }
    .main>div{
      width: 50px;
      height: 50px;
      border: 1px solid black;
    }
    .main div:nth-child(2){
            height:60px;
    }
</style>
//DOM
<div class="main">
    <div></div>
    <div></div>
    <div></div>
    <div></div>
  </div>
```

此处虽然木有给父元素设置宽度，但是父元素默认会根据子元素的宽高去自适应。

![img](https://upload-images.jianshu.io/upload_images/6522941-a6d119c9af3ffe3b.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/726/format/webp)



------



## * main.js中

`main.js`的`Vue.config.productionTip = false`只是关闭了开发模式和发布模式的文本提醒没有啥用

## * promise

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

## * promise的三个实例方法

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

## * CSS 属性选择器详解

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









## * 在vue中使用rules对表单字段进行验证

> vue 中[表单](https://so.csdn.net/so/search?q=表单&spm=1001.2101.3001.7020)字段验证的写法和方式有多种，本博客介绍三种较为常用的验证方式。

### 1.写在data里的验证

```vue
<!-- 表单 -->
<el-form ref="rulesForm" :rules="formRules" :model="rulesForm" label-width="200px">
    <el-form-item label="用户名称:" prop="userName">
       <el-input v-model="rulesForm.userName" style="width:300px" maxlength="50"/>
    </el-form-item>
</el-form>
```

- `<el-form>`：代表这是一个表单
- `<el-form>` -> `ref`：表单被引用时的名称，标识
- `<el-form>` -> `rules`：表单验证规则
- `<el-form>` -> `model`：表单数据对象
- `<el-form>` -> `label-width`：表单域标签的宽度，作为 Form 直接子元素的 form-item 会继承该值
- `<el-form>` -> `<el-form-item>`：表单中的每一项子元素
- `<el-form-item>` -> `label`：标签文本
- `<el-form-item>` -> `prop`：表单域 model 字段，在使用 validate、resetFields 方法的情况下，该属性是必填的
- `<el-input>`：输入框
- `<el-input>` -> `v-model`：绑定的表单数据对象属性
- `<el-input>` -> `style`：行内样式
- `<el-input>` -> `maxlength`：最大字符长度限制

#### **data 数据**

```office
data() {
    return {
        // 省略别的数据定义
        ...
        
        // 表单验证
        formRules: {
            userName: [
                {required: true,message: "请输入用户名称",trigger: "blur"}
            ]
        }
    }
}
```

- `formRules`：与上文  '表单内容' 中 `<el-form>` 表单的 `:rules` 属性值相同
- `userName`：与上文 '表单内容' 中 `<el-form-item>` 表单子元素的 `prop` 属性值相同
- **`验证内容是：必填，失去焦点时验证，如果为空，提示信息为 '请输入用户名称'`**

![](C:\Users\shizeyu\Desktop\notes\Ajax-vue\image-20221025143212122.png)

------

###  **2. 写在行内**

**表单内容**:

```vue
<!-- 表单 -->
<el-form ref="rulesForm" :rules="formRules" :model="rulesForm" label-width="200px">
    <el-form-item label="银行名称:" prop="accountName" :rules="[{required:true,message:'请输入银行名称',trigger:'blur'}]">
        <el-input v-model="rulesForm.accountName" style="width:300px" maxlength="50"/>
    </el-form-item>
</el-form>
```

- `<el-form-item>` -> `rules`：和第一种方式表现的效果一致，只是写法不一样，这里不再赘述

**data 数据没有内容**

------

### **3. 引入外部定义的规则**

**表单内容**:

```vue
<!-- 表单 -->
<el-form ref="rulesForm" :rules="formRules" :model="rulesForm" label-width="200px">
    <el-form-item label="银行卡号:" prop="accountNumber">
       <el-input v-model="rulesForm.accountNumber" style="width:300px" maxlength="19"/>
    </el-form-item>
</el-form>
```

- 表单内容与第一种方式写法一致，这里不再赘述

**script 内容**

```vue
<script>
// 引入了外部的验证规则
import { validateAccountNumber } from "@/utils/validate";
 
// 判断银行卡账户是否正确
const validatorAccountNumber = (rule, value, callback) => {
  if (!value) {
    return callback(new Error("请输入账户信息"));
  } else {
    if (validateAccountNumber(value)) {
      callback();
    } else {
      return callback(new Error('账号格式不正确'))
    }
  }
};
 
export default {
    data() {
        return {
            // 省略别的数据定义
            ...
        
            // 表单验证
            formRules: {
                accountNumber: [
                    {required: true,validator: validatorAccountNumber,trigger: "blur"}
                ]
            }
        }
    }
}
</script>
```

- `import`：先引入了外部的验证规则 
- `const`：定义一个规则常量，常量名可变， '= (rule, value, callback) => {}' 为固定格式，`value` 入参为验证的字段值
- `formRules` -> `accountNumber`：表单验证中使用 validator 指定自定义校验规则常量名称

**validate.js**

```js
/* 银行账户 */
export function validateAccountNumber(str) {
  const reg = /^([1-9]{1})(\d{14}|\d{18})$/
  return reg.test(str)
}
```

- 验证规则

------

#### **以上都是在失去焦点时的验证，下面来分析一下如何在表单提交时验证

 **1. 表单的提交按钮**

```vue
<!-- 表单 -->
<el-form ref="rulesForm" :rules="formRules" :model="rulesForm" label-width="200px">
    <el-form-item>
        <el-button type="primary" @click="onSubmit('rulesForm')">保存</el-button>
        <el-button @click="cancel">取消</el-button>
    </el-form-item>
</el-form>
```

- `<el-button>`：按钮
- `<el-button>`-> `type`：按钮类型
- `<el-button>` -> `@click`：按钮点击时触发的事件，这里注意方法的入参为 'rulesForm'，这里要与 `<el-form>` 表单的 rel 属性值一致

 **2. methods 方法**

```js
methods: {
    // 保存
    onSubmit(formName) {
        this.$refs[formName].validate(valid => {
            if (valid) {
                console.log("success submit!!");
            }else{
                console.log("error submit!!");
            }
        });
    },
    // 取消
    cancel() {
        
    }
}
```

- `this.$refs[formName].validate：中的 formName` 就是传入的 'rulesForm'，与 `<el-form>` 表单的 `rel` 属性值一致，这样就指定好需要验证的表单了
- 然后要结合`validate.js`来判断必须要有`validate.js`

------

**完整示例代码如下**：

**1. rules.vue**：

```vue
<template>
  <div class="app-container">
    <el-tabs v-model="activeName">
      <el-tab-pane label="表单" name="rulesPane" @tab-click="handleClick">
        <!-- 表单 -->
        <el-form ref="rulesForm" :rules="formRules" :model="rulesForm" label-width="200px">
          <el-form-item label="用户名称:" prop="userName">
            <el-input v-model="rulesForm.userName" style="width:300px" maxlength="50"/>
          </el-form-item>
          <el-form-item label="银行名称:" prop="accountName" :rules="[{required:true,message:'请输入银行名称',trigger:'blur'}]">
            <el-input v-model="rulesForm.accountName" style="width:300px" maxlength="50"/>
          </el-form-item>
          <el-form-item label="银行卡号:" prop="accountNumber">
            <el-input v-model="rulesForm.accountNumber" style="width:300px" maxlength="50"/>
          </el-form-item>
          <el-form-item>
            <el-button type="primary" @click="onSubmit('rulesForm')">保存</el-button>
            <el-button @click="cancel">取消</el-button>
          </el-form-item>
        </el-form>
      </el-tab-pane>
    </el-tabs>
  </div>
</template>
 
<script>
import { validateAccountNumber } from "@/utils/validate";
 
// 判断银行卡账户是否正确
const validatorAccountNumber = (rule, value, callback) => {
  if (!value) {
    return callback(new Error("请输入账户信息"));
  } else {
    if (validateAccountNumber(value)) {
      callback();
    } else {
      return callback(new Error('账号格式不正确'))
    }
  }
};
 
export default {
  name: "rules",
  data() {
    return {
      activeName: "rulesPane",
      defaultProps: {
        children: "children",
        label: "label"
      },
      rulesForm: {
      },
      //   表单验证
      formRules: {
        userName: [
          {
            required: true,
            message: "请输入用户名称",
            trigger: "blur"
          }
        ],
        accountNumber: [
          {
            required: true,
            validator: validatorAccountNumber,
            trigger: "blur"
          }
        ],
      }
    };
  },
  created() {},
  mounted() {},
  methods: {
    handleClick(tab) {
      
    },
    // 取消
    cancel() {
      
    },
    // 保存
    onSubmit(formName) {
      this.$refs[formName].validate(valid => {
        if (valid) {
          console.log("success submit!!");
        } else {
          console.log("error submit!!");
          return false;
        }
      });
    }
  }
};
</script>
 
<style lang="scss">
</style>
```

**2. validate.js**

```js
/* 银行账户 */
export function validateAccountNumber(str) {
  const reg = /^([1-9]{1})(\d{14}|\d{18})$/
  return reg.test(str)
}
```

**效果图**	

![rules](https://img-blog.csdnimg.cn/20190108111721773.gif)

------



### 校验规则

| 参数       | 说明                                                         | 类型                                    | 默认值   |
| :--------- | :----------------------------------------------------------- | :-------------------------------------- | :------- |
| enum       | 枚举类型                                                     | string                                  | -        |
| len        | 字段长度                                                     | number                                  | -        |
| max        | 最大长度                                                     | number                                  | -        |
| message    | 校验文案                                                     | string                                  | -        |
| min        | 最小长度                                                     | number                                  | -        |
| pattern    | 正则表达式校验                                               | RegExp                                  | -        |
| required   | 是否必选                                                     | boolean                                 | `false`  |
| transform  | 校验前转换字段值                                             | function(value) => transformedValue:any | -        |
| type       | 内建校验类型，[可选项](https://github.com/yiminghe/async-validator#type) | string                                  | 'string' |
| validator  | 自定义校验（注意，[callback 必须被调用](https://github.com/ant-design/ant-design/issues/5155)） | function(rule, value, callback)         | -        |
| whitespace | 必选时，空格是否会被视为错误                                 | boolean                                 | `false`  |

#### trigger:‘blur’ OR trigger:‘change’ OR 不设置:

> 对el-input输入框的验证，trigger的值选blur，即失去焦点时进行验证。
>
> 下拉框（el-select）、日期选择器（el-date-picker）、复选框（el-checkbox）、单选框（el-radio）验证时，trigger的值选择change，即当值发生变化时就进行验证。

------







## *【JS】正则表达式总结(用于校验)

**1.数字/货币金额（支持负数、千分位分隔符）**

```
/(^[-]?[1-9]\d{0,2}($|(,\d{3})*($|(\.\d{1,2}$))))|((^[0](\.\d{1,2})?)|(^[-][0]\.\d{1,2}))$/
```

**2.数字/货币金额 (只支持正数、不支持校验千分位分隔符)**

```
/(^[1-9]([0-9]+)?(\.[0-9]{1,2})?$)|(^(0){1}$)|(^[0-9]\.[0-9]([0-9])?$)/
```

**3.银行卡号（16或19位）**

```
/^([1-9]{1})(\d{15}|\d{18})$/
```

**4.中文姓名**

```
/^([\u4e00-\u9fa5·]{2,10})$/
```

**5.手机号(严谨), 根据工信部2019年最新公布的手机号段**

```
/^1((3[\d])|(4[5,6,7,9])|(5[0-3,5-9])|(6[5-7])|(7[0-8])|(8[\d])|(9[1,8,9]))\d{8}$/
```

**6.手机号(宽松), 只要是13,14,15,16,17,18,19开头即可**

```
/^1[3-9]\d{9}$/
```

**7.email地址**

```
/^\w+([-+.]\w+)*@\w+([-.]\w+)*\.\w+([-.]\w+)*$/
```

**8.国内座机电话,如: 0341-86091234**

```
/\d{3}-\d{8}|\d{4}-\d{7}/
```

**9.二代身份证号(18位数字),最后一位是校验位,可能为数字或字符X**

```
/^\d{6}(18|19|20)\d{2}(0\d|11|12)([0-2]\d|30|31)\d{3}(\d|X|x)$/
```



------





## * RegExp(正则表达式)

### 一、RegExp([正则表达式](https://so.csdn.net/so/search?q=正则表达式&spm=1001.2101.3001.7020))

正则表达式（RegExp）是Regular Expression缩写，是用于查找符合某些规则的字符串的工具。
正则表达式是一个描述字符模式的对象，当检索某个文本时，可以使用一种模式来描述要检索的内容，RegExp 就是这种模式。

#### 正则的创建

构造函数
字面量

```js
    // 构造函数式
    // var reg=new RegExp(pattern,attribute);
    var reg1 = new RegExp('a','i');
​
    // 字面量式
    // var reg=/pattern/attribute;
    var reg2 = /a/i; 

```

上面两种创建方式所表达的内容是一致的，都是匹配字符串中的’a’，并且是忽略大小写的。
pattern：匹配模式。
attribute：匹配特征。

#### 正则对象的属性和方法

上面我们仅仅只是得到一个正则对象，还不能做任何事情，例如对字符串的校验等。

```coffeescript
正则对象的属性
global:全局的，对应修饰符g
ignoreCase:忽略大小写，对应修饰符i
multiline:多行，对应修饰符m
lastIndex:下一次匹配的字符位置
正则对象的属性
test():测试方法，用于测试一个字符串是否符合正则表达式对象所指定的模式规则，返回true或false
exec()：搜索方法，用于在字符串中查找符合正则表达式对象所指定的模式的子字符串，返回找到的结果，若找不到则返回null
```

#### 匹配模式pattern

在正则中匹配模式`pattern`是整个正则表达式的灵魂，同样它也是正则表达式中最复杂的部分。 在匹配模式中我们需要学习三个部分：

```coffeescript
元字符：具有特殊含义的字符
量词：指定字符出现的次数
特殊符号：具有特定含义的符号
元字符
\s:匹配任何的空白字符
\S:任何非空白字符
\d:匹配一个数字字符，等价于[0-9]
\D:除了数字之外的任何字符，等价于[^0-9]
\w:匹配一个数字、下划线或字母字符，等价于[A-Za-z0-9_]
\W:任何非单字字符，等价于[^a-zA-z0-9_]
.:匹配除了换行符之外的任意字符
量词
{n}:匹配前一项n次
{n,}:匹配前一项至少n次
{n,m}:匹配前一项至少n次最多m次
*:匹配前一项至少0次最多无数次，{0,}
+:匹配前一项至少1次最多无数次，{1,}
?:匹配前一项最多1次，{0,1}
特殊符号
/.../:代表一个模式的开始和结束
^:匹配字符串的开始，即表示行的开始
$:匹配字符串的结束，即表示行的结束
[ ]:表示可匹配的列表
( ):用于分组
|:表示或者
[^ ]:在[  ]中的尖括号表示非

```

#### string对象的正则方法

match
search
replace
split

------

## * 关于overflow:hidden的作用（溢出隐藏、清除浮动、解决外边距塌陷、省略号等等）

https://blog.csdn.net/qq_41638795/article/details/83304388



------

## * Vue 中 import from @符号指的是什么

> 简单说安装了插件默认是 src 
>
> eg：@/utils/auth = src/utils/auth

**1、假设vue文件中引入如下代码**

```java
import { auth } from "@/utils/auth";
```

**2、@符号表示的含义**

- @符号表示一个特定路径名称，这个设置引入的是src/utils路径下的auth.js文件

**3、lz的vue框架中，@符号可以在build/vue.config.js文件中设置，如下图：lz的@符号表示src路径**

- 具体在哪个文件下的vue配置文件可根据实际情况参考

![在这里插入图片描述](https://img-blog.csdnimg.cn/20210611233751367.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2xpMTMyNTE2OTAyMQ==,size_16,color_FFFFFF,t_70#pic_center)

------

## * 关于hash和history的区别和使用

https://blog.csdn.net/weixin_46589442/article/details/125796515



------

## * export default向外共享路由的实例对象，让其他组件可以使用

------

## * Vue中 Vue.prototype 详解及使用

https://blog.csdn.net/ZYS10000/article/details/107233453/

我们可能会在很多组件里用到数据/实用工具，但是不想污染全局[作用域](https://so.csdn.net/so/search?q=作用域&spm=1001.2101.3001.7020)。这种情况下，可以通过在原型上定义它们使其在每个 Vue 的实例中可用。

#### 1. 基本示例

在main.js中添加一个变量到 Vue.prototype

```javascript
Vue.prototype.$appName = 'My App'
```

这样 $appName 就在所有的 Vue 实例中可用了，甚至在实例被创建之前就可以

```javascript
new Vue({
  beforeCreate: function () {
    console.log(this.$appName)
  }
})
```

控制台会打印出 My App，就这么简单！

#### 2. 为实例prototype设置作用域

为什么 appName 要以 $ 开头？这很重要吗？

这里没有什么魔法。$ 是在 Vue 所有实例中都可用的 property 的一个简单约定。这样做会避免和已被定义的数据、方法、计算属性产生冲突。
如果我们设置：

```
Vue.prototype.appName = 'My App'
```

那么如下的代码输出什么：

```js
new Vue({
  data: {
    // 啊哦，`appName` 也是一个我们定义的实例 property 名！
    appName: 'The name of some other app'
  },
  beforeCreate: function () {
    console.log(this.appName)
  },
  created: function () {
    console.log(this.appName)
  }
})

```

日志中会先出现 “My App”，然后出现 “The name of some other app”，因为 this.appName 在实例被创建之后被 data 覆写了。我们通过 $ 为实例 property 设置作用域来避免这种事情发生。你还可以根据你的喜好使用自己的约定，诸如 $_appName 或 ΩappName，来避免和插件或未来的插件相冲突。

#### 3. 注册和使用全局变量

每个组件都是一个vue实例，Vue.prototype加一个变量，只是给每个组件加了一个属性，这个属性的值并不具有全局性。
比如以下例子：

```js
// main.js
import Vue from 'vue'
import App from './App'
import router from './router'
import store from './store'

Vue.config.productionTip = false
Vue.prototype.$appName = 'main'

new Vue({
    el: '#app',
    store,
    router,
    components: { App },
    template: '<App/>',
})

// 给所有组件注册了一个属性 $appName，赋予初始值 'main' ，所有组件都可以用 this.$appName 访问此变量;
// 如果组件中没有赋值，初始值都是'main'

```

```vue
// home.vue
<template>
  <div>
    <div @click="changeName">change name</div>
    <div @click="gotoTest2">goto test2</div>
  </div>
</template>

<script>
export default {
  methods:{
    changeName(){
      this.$appName = "test1"
    },
    gotoTest2(){
      this.$router.push('/about')
    } 
  }
}
</script>

```

```vue
// about.vue
<template>
  <div>
    <div>{{this.$appName}} in test2</div>
  </div>
</template>
```

点击 home 中的 change name 再跳转about，about里面还是显示 main in test2

**如果要实现全局变量的功能，需要把属性变为引用类型**

```js
Vue.prototype.$appName = { name: 'main' }
```

**后面使用 this.$appName.name 改变和引用相应的值**
这进入 about 后显示 test1 in test2

#### 4. 原型方法的上下文

在 JavaScript 中一个原型的方法会获得该实例的上下文,也就是说可以使用 this 访问：数据、计算属性、方法或其它任何定义在实例上的东西。
让我们将其用在一个名为 $reverseText 的方法上：

```js
 // main.js
Vue.prototype.$reverseText = function (propertyName) {
  this[propertyName] = this[propertyName]
    .split('')
    .reverse()
    .join('')
}
```

```vue
// 相应组件
<script>
export default {
  data() {
    return{
      message: 'Hello'
    }
  },
  created() {
    console.log(this.message) // => "Hello"
    this.$reverseText('message')
    console.log(this.message) // => "olleH"
  }
}
</script>

```

#### 5. 应用示例

**5.1 引入 axios**

```javascript
npm install vue-axios --save

npm install qs.js --save　　//它的作用是能把json格式的直接转成data所需的格式
```

```js
// mian.js
import Vue from 'vue'
import axios from 'axios'
import qs from 'qs'

Vue.prototype.$axios = axios    //全局注册，使用方法为:this.$axios
Vue.prototype.qs = qs           //全局注册，使用方法为:this.qs

```

```vue
// 相应组件
<script>
  export default{
    data(){
      return{
        userId:666,　　　　　　　　　
        token:'',
      }
    },
    created(){
      this.$axios({
        method:'post',
        url:'api',
        data:this.qs.stringify({    //这里是发送给后台的数据
          userId:this.userId,
          token:this.token,
        })
      }).then((response) =>{          //这里使用了ES6的语法
        console.log(response)       //请求成功返回的数据
      }).catch((error) =>{
        console.log(error)       //请求失败返回的数据
      })
    }
  }
</script>

```



------

## *vue之moment使用

### 前言

在日常开发中，我们常常会遇到以下几种场景：

- 需要对日期进行非标准格式展示，如 ：2021年5月11日星期二下午6点42分
- 需要对日期进行处理，如：要取前24小时的时间 等

在这时候用js原生的`new Date()`处理就有些麻烦了，因此我们找到了`moment`这个类库

### 一、moment是什么？

`moment` 是一个 `JavaScript` 日期处理类库。
注：以下所有时间相对于现在时间：2021/05/11/18:42 星期二

### 1.日期格式化：

- `moment().format('MMMM Do YYYY, h:mm:ss a');` // 五月 11日 2021, 6:42:31 下午
- `moment().format('dddd');` // 星期二
- `moment().format("MMM Do YY");` // 5月 11日 21
- `moment().format('YYYY [escaped] YYYY');` // 2021 escaped 2021
- `moment().format();` //2021-05-11T18:06:42+08:00

### 2.相对时间：

- `moment("20111031", "YYYYMMDD").fromNow();` // 2011/10/31号相对于现在是： 10 年前
- `moment("20120620", "YYYYMMDD").fromNow();` // 2012/06/20号相对于现在是： 9 年前
- `moment().startOf('day').fromNow();` //当前日期开始即：2021/05/11/00:00:00相对于现在是： 19 小时前
- `moment().endOf('day').fromNow();` //当前日期结束即：2021/05/11/24:00:00相对于现在是： 5 小时内
- `moment().startOf('hour').fromNow();` //当前日期小时开始即：2021/05/11/18:00:00相对于现在是： 42分钟前

### 3.日历时间：

- `moment().subtract(10, 'days').calendar();` // 当前时间往前推10天的日历时间： 2021/05/01
- `moment().subtract(6, 'days').calendar();` // 当前时间往前推6天： 上星期三18:42
- `moment().subtract(3, 'days').calendar();` // 当前时间往前推3天： 上星期六18:42
- `moment().subtract(1, 'days').calendar();` // 当前时间往前推1天： 昨天18:42
- `moment().calendar();` // 今天18:42
- `moment().add(1, 'days').calendar();` // 当前时间往后推1天： 明天18:42
- `moment().add(3, 'days').calendar();` // 当前时间往后推3天： 下星期五18:42
- `moment().add(10, 'days').calendar();` // 当前时间往后推10天： 2021/05/21

### 4.多语言支持：

- `moment.locale();` // zh-cn
- `moment().format('LT');` // 18:42
- `moment().format('LTS');` // 18:42:31
- `moment().format('L');` // 2021/05/11
- `moment().format('l');` // 2021/5/11
- `moment().format('LL');` // 2021年5月11日
- `moment().format('ll');` // 2021年5月11日
- `moment().format('LLL');` // 2021年5月11日下午6点42分
- `moment().format('lll');` // 2021年5月11日 18:42
- `moment().format('LLLL');` // 2021年5月11日星期二下午6点42分
- `moment().format('llll');` // 2021年5月11日星期二 18:42

### 二、使用步骤（例：默认查询时间24小时之前~当前时间）

### 1.引入库

```bash
$ npm install moment --save
1
```

### 2.在main.js中全局引入（也可单独在使用的文件中引入，具体看需求）

```js
import moment from "moment"
Vue.prototype.$moment = moment;
```

### 3.在需要使用日期的地方使用

HTML中：

```html
 <el-date-picker
    	v-model="timeRange"
        type="datetimerange"
        range-separator="至"
        start-placeholder="开始日期"
        end-placeholder="结束日期">
 </el-date-picker>

```

JS中：

```js
 data() {
      return {
         timeRange:[],
      }
   },
  mounted(){
        let start = this.$moment()
            .subtract('1', 'd')
            .format('YYYY-MM-DD HH:mm:ss') //当前时间往前推1天（24小时）：2021-05-10 18:42:53
        let end = this.$moment().format('YYYY-MM-DD HH:mm:ss') //当前时间：2021-05-11 18:42:53
        this.timeRange=[start,end]
   },  

```

### 三、日期格式

| 格式 | 含义  |  举例  |               备注                |
| :--: | :---: | :----: | :-------------------------------: |
| yyyy |  年   |  2021  |              同YYYY               |
|  M   |  月   |   1    |               不补0               |
|  MM  |  月   |   01   |                                   |
|  d   |  日   |   2    |               不补0               |
|  dd  |  日   |   02   |                                   |
| dddd | 星期  | 星期二 |                                   |
|  H   | 小时  |   3    |          24小时制；不补0          |
|  HH  | 小时  |   18   |             24小时制              |
|  h   | 小时  |   3    | 12小时制，须和 A 或 a 使用；不补0 |
|  hh  | 小时  |   03   |    12小时制，须和 A 或 a 使用     |
|  m   | 分钟  |   4    |               不补0               |
|  mm  | 分钟  |   04   |                                   |
|  s   |  秒   |   5    |               不补0               |
|  ss  |  秒   |   05   |                                   |
|  A   | AM/PM |   AM   |       仅 format 可用，大写        |
|  a   | am/pm |   am   |       仅 format 可用，小写        |

#### 具体方法以及参数可详见[moment官方文档](http://momentjs.cn/docs/)

mount()

要获取当前的日期和时间，只需调用不带参数的 `moment()` 即可。

------

## * ant-design-vue使用之路

https://blog.csdn.net/qq_39692513/article/details/111468260

### 引入[ant-design](https://so.csdn.net/so/search?q=ant-design&spm=1001.2101.3001.7020)-vue

#### 1.全局引入

```
1. 命令行使用npm安装
npm install ant-design-vue --save
2. main.ts文件中导入
import Antd from 'ant-design-vue';
import 'ant-design-vue/dist/antd.css';

```

#### 2. 局部引入

为了减小打包大小，提高加载速度，更推荐这种做法

##### 局部引入组件

```
1. 命令行安装ant-design-vue包
npm install ant-design-vue --save

2 创建antPlugin.js文件，按需引入组件都可在这个文件中写，以button组件为例
import Vue from 'vue'
import {Button} from 'ant-design-vue' // 官方文档中组件去掉a，首字母大写如a-form-model， 按需引入组件就是 FormModel
Vue.use(Button)

3 main.ts 导入此文件
import ‘@/util/antPlugin’

4 babel.config.js 添加import插件，自动引入组件对应样式
module.exports = {
  // ...
  plugins: [
    [
      'import',
      { libraryName: 'ant-design-vue', libraryDirectory: 'es', style: 'css' }
    ]
  ]
}

5 坑
引入样式时，需要npm安装less-loader去解析，less-loader版本过高超过6.0后，会报错。
需手动设置javascriptEnabled。故我们在vue.config.js文件中设置(*楼主当时设置了好多遍也没起效，最后发现是less-loader没安装完全，多安装几次就好了*)
modules.exports = {
  css: {
    loaderOptions: {
      less: {
        javascriptEnabled: true
      }
    }
  }
}

```

##### 局部引入图标

按需采用吧，而且要注意ant-design-vue组件中，自带的图标，也要引用进来，不然组件图标会消失。

```
1 在项目中创建文件icons.ts ，引入并导出你需要的图标
export { default as CloseCircleFill } from '@ant-design/icons/lib/fill/CloseCircleFill'
export { default as QuestionCircleTwoTone } from '@ant-design/icons/lib/twotone/QuestionCircleTwoTone'
export { default as ForkOutline } from '@ant-design/icons/lib/outline/ForkOutline'
2 在vue.config.js中配置将从npm包中导入映射从你创建的文件中导入
module.exports = {
 configureWebpack: {
    resolve: {
      alias: {
        '@ant-design/icons/lib/dist$': path.resolve(__dirname, './src/util/icons.ts')
      }
    },
    plugins: [
      new MomentLocalesPlugin({
        localesToKeep: ['zh-CN']
      })
    ]
  },
}
3 坑
记得找到组件自身所引入图标，也导入进来

```

### 使用

#### 1message的使用

可在js中方便的调用message弹窗

```
1 创建message.js
import { message } from 'ant-design-vue'
2 定义sucess、error等方法，并导出，即可方便使用了
function success (msg: string) {
  message.success(msg)
}
export default { success, error, warn, info }

```

#### 2 日期范围组件本地化

讲一下日期选择器本地化，这里讲一下多处
多处本地化，推荐使用config-provider
一个地方组件化，推荐使用组件中locale参数

```
tempate中使用a-config-provider
<a-config-provider :locale="locale">
					<a-range-picker :ranges="range" v-model="dateData" :disabledDate="getDisabledTime" :allowClear="false" format="YYYY-MM-DD HH:mm:ss" />
				</a-config-provider>
				
js中
import moment from 'moment'
import zhCN from 'ant-design-vue/es/locale/zh_CN'
import 'moment/locale/zh-cn'
moment.locale('zh-cn')
 		class类中
 			public locale = zhCN //定义语言
 			
	public range = { //设置快捷选项
		今天: [moment().startOf('day'), moment()],
		昨天: [
			moment()
				.startOf('day')
				.subtract(1, 'days'),
			moment()
				.endOf('day')
				.subtract(1, 'days')
		],
		最近三天: [
			moment()
				.startOf('day')
				.subtract(2, 'days'),
			moment()
		],
		最近一周: [
			moment()
				.startOf('day')
				.subtract(1, 'weeks'),
			moment()
		]
	}
	
	public getDisabledTime(current: any) { //定义选择范围
		return current < moment().subtract(7, 'day') || current > moment()
	}

```

#### 3组件化的小技巧

主要是依靠[] 操作符和，传递父方法。以list和form为例

##### list

```
1 子组件中
 template中
 
  <a-list item-layout="horizontal" :data-source="data">
    <div v-if="headerButtons.length !== 0" slot="header" class="button-postion">
     <a-button type="primary" class="button-margin"  v-for="(button) in headerButtons" :key="button.name" @click="emitParent(button.funcName,button.type)">
        {{button.name}}
      </a-button>
    </div>   //  【顶部按钮，传递想展示按钮以及方法】
    <a-list-item slot="renderItem" slot-scope="item">
      <a-list-item-meta
        :description="item[name]"
      >
        <a href="javascript:void(0);" class="title-width" v-if="mainListFunc" slot="title"  @click="emitRouter(item)">{{ item[id] }}</a>
        <span type="link" v-else slot="title" >{{ item[id] }}</span>
      </a-list-item-meta>  //【 list列表，将展示字段传递，使用item[字段]来调用】
       <div class="content-width">{{item[remark]}}</div>
      <a slot="actions">
        <a-button size="small" type="link"  v-for="(button) in buttons" :key="button.name" @click="emitParent(button.funcName,button.type,item)">
        {{button.name}}
      </a-button> //【传递按钮时，同时传递方法】
      </a>
    </a-list-item>
  </a-list>

js中，接收参数并调用父方法

 public emitParent (funcName: string, type: number, data: object = {}) {
     this.$emit(funcName, type, data)
   }


2 父组件中
template中引入子组件，并传递参数

<list :headerButtons="headerButtons" :id="id" :name="name" :remark="remark" :data="data" :buttons="buttons" :mainListFunc="mainListFunc" @addOrEditData="startForm"  @startSureShow="startSureShow" @mainIdFunc="gotoRouter"></list>

js中 定义传递按钮参数及其他参数
public buttons =[{ name: '编辑', funcName: 'addOrEditData', type: 2 },
    { name: '删除', funcName: 'startSureShow', type: 3 }]/

```

##### form

```
1 子组件
template中
  <a-form-model
    ref="ruleForm"
    :model="formData"
    :rules="rules"
    :label-col="labelCol"
    :wrapper-col="wrapperCol"
  >
    <a-form-model-item class="item-margin-bottom" v-for="item in formLabel" :key="item.propName" :label="item.label" :prop="item.propName"> // 【使用form循环来遍历输入列表，传入formLabel】
      <a-radio-group v-if="item.type === 1" v-model="formData[item.propName]" :disabled="item.disabled">  // 【使用formData[item.propName]】来双向绑定
        <a-radio v-for="radio in item.values" :key="radio.value" :value="radio.value">{{radio.label}}</a-radio>
      </a-radio-group>
       <a-input v-else-if="item.type === 2" v-model="formData[item.propName]" type="textarea" :disabled="item.disabled" />
      <a-input v-else v-model="formData[item.propName]" :disabled="item.disabled" />
    </a-form-model-item>
    </a-form-model>

2父组件中
template中引入并传递参数
<dialog-form :title="title" :visible="visible" :confirmLoading="confirmLoading" :formData="formData" :formLabel="formLabel" :rules="rules" @saveFunc="saveScenceData" @cancelFunc="closeDialog"></dialog-form>

js中定义参数

  public formLabel = [{ label: '场景id', propName: 'businessid', disabled: false }, // 标签显示
    { label: '场景名称', propName: 'businessname', disabled: false },
    { label: '场景描述', propName: 'remark', disabled: false },
  ]
   public formData= { // 表单数据
    businessid: '',
    businessname: '',
    remark： ‘’
  }


```

### 优化

#### [webpack](https://so.csdn.net/so/search?q=webpack&spm=1001.2101.3001.7020)分析插件

```
vue.config.js中
module.exports = {
  chainWebpack: (config) => {
     config
       .plugin('webpack-bundle-analyzer')
       .use(require('webpack-bundle-analyzer').BundleAnalyzerPlugin)
   },
}
运行后，打开地址，可看到各个文件的打包大小，进而选择性的优化

```

#### 优化强依赖插件moment

```
去除其他语言包，只保留中文和英文（英文内置，不可去除）
module.exports ={
    plugins: [
      new MomentLocalesPlugin({
        localesToKeep: ['zh-CN']
      })
    ]
  },
}

```







------



# 啊啊啊

<font color='red'>****</font>



## less知识 

## Virtual Dom

# 简单了解SPA、SEO及CSR和SSR渲染方式
