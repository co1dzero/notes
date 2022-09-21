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

# 二. vue的基本使用

## 1.基本步骤

new Vue（）

① 导入vue.js的script脚本文件

```html
<script src="./vue.js"></script>
```

②在页面中声明一个将要被vue所控制的DOM区域

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





# 三. Vue的调试工具

## 3.1 安装 vue-devtools

![](C:\Users\shizeyu\Desktop\notes\Ajax-vue\Snipaste_2022-09-21_16-51-34.png)

## 3.2 配置

![](C:\Users\shizeyu\Desktop\notes\Ajax-vue\Snipaste_2022-09-21_16-52-18.png)

## 3.3 使用 vue-devtools 调试Vue

![](C:\Users\shizeyu\Desktop\notes\Ajax-vue\Snipaste_2022-09-21_16-58-14.png)

**`Root指向el指的区域，叫做根节点。右侧data被Vue接管，改变其值，页面效果也会改变`**





# 四. Vue的指令和过滤器

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









# 五. 品牌列表案例

































