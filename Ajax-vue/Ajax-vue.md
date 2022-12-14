Ctrl + shift + ] = 小黑点

Ctrl + \消除上一行格式

Ctrl + [消除上一行格式

<font color='red'>****</font>

# AJax

## 一.form表单的基本使用

表单：负责**数据采集**用于采集用户输入的信息，通过form提交操作，把采集到的数据提交到服务器

表单三部分：

- 表单标签
- 表单域
- 表单按钮

```html
	<form action="">  //表单标签
        <input type="text" name="password">   //表单域
        <button type="submit">提交</button>   //表单按钮
    </form>
```

### 1.1 form标签的属性

<font color='red'>**8.3的 FormData是其替代**</font>

#### 1.action

```
<form action="">
```

action 属性用来规定提交时，**向何处发送表单数据**

通常后接一个后端提供的URL地址，当未指定属性值时，action默认是当前页面的URL地址

> 注意：当提交表单后，会自动跳转到action的属性指定的URL地址，**内容会以字符串的形式显示在URL上**

#### 2.target

```html
<form action="" target="_self">
```

用来规定**在何处打开action URL**

| 值     | 描述                     |
| ------ | ------------------------ |
| _blank | 在新窗口打开             |
| _self  | 默认。在相同的框架中打开 |
|        |                          |
|        |                          |
|        |                          |

#### 3.method

```
<form action="/asdadsa" target="_self" method="post">
```

method属性规定**以何种方式**把表单数据提交到action URL。

| GET  | 默认。通过URL地址的像是，把数据提交到action URL 显示在URL中，不常用 |
| ---- | ------------------------------------------------------------ |
| POST | 不显示在URL中，隐藏，使用频繁                                |

#### 4.enctype

```html
<form action="/asdadsa" target="_self" method="post" enctype="">
```

enctype属性规定在**发送表达数据之前如何对数据进行编码**。

| 值                                | 表述                                                         |
| --------------------------------- | ------------------------------------------------------------ |
| application/x-www-form-urlencoded | 在发送前编码所有字符（默认）                                 |
| multipart/form-data               | 不对字符编码，在使用包含**文件上传**控件的表单时，必须使用该值 |
| text/plain                        | 空格转换为”+“(很少用)                                        |

> 注意：上传文件时一定要用multipart/form-data，其他时候默认就好

### 1.2 form的同步提交

form的同步提交：通过submit,触发表单提交从而使页面跳转到action URL的行为交表单提交

> 缺点：会跳转而且返回后数据丢失，改用ajax来提交，表单只收集

## 二.通过Ajax提交表单数据

### 2.1 监听表单提交事件

jquery方法：

```javascript
		$(function () {
            //第一种
            $('#formname').submit(function (e) {
                alert('监听到了')
            })
            //第二种
            $('formname').on('submit', function (e) {
                alert('监听到了')
            })
        })
```

### 2.2阻止默认表单默认行为

当监听到表单的提交事件后，可以调用event.preventDefault()，来阻止表单提交和页面的跳转

```js
$(function () {
    $('formname').on('submit', function (e) {
          alert('监听到了')
          e.preventDefault()
    })
})
```

### 2.3 快速获取表单数据

#### serialize()

**jquery语法**原生获取表单可以看8.3,可以一次性获取表单中所有的数据

```javascript
$('formname').serialize()
```

```html
	<form action="" id='form1'>  //表单标签
        <input type="text" name="username">   //表单域
        <input type="text" name="password">
        <button type="submit">提交</button>   //表单按钮
    </form>
    
   	let data = $('#form1').serialize()  //结果（键值对形式）：username=值&password=值 
```

> <font color='red'>注意：使用serialize时候，必须为每个表单元素添加name属性！</font>

## 三.模板引擎

可以根据程序员指定的<font color='red'>模板结构</font>和<font color='red'>数据</font>，自动生成一个完整的HTML页面

## 四.art-template模板引擎

### 4.1基本使用

```html
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <!-- 1.导入模板引擎，在window全局就有了template这个构造函数 template('模板的Id',需要渲染的数据对象) -->
    <script src="./template-web.js"></script>
</head>

<body>

    <div id="container"></div>

    <!-- 3.定义模板 -->
    <!-- 3.1模板的html结构，必须定义在script中，默认type是text/javaScript -->
    <script type="text/html" id="tpl-user">
        <h1>{{name}}    -------   {{age}}</h1>
    </script>

    <script>
        // 2.定义需要渲染的数据
        const data = {
            name: '张三',
            age: 18
        }

        //4. 调用template函数 模板的Id不用加#因为是template函数
        const htmlstr = template('tpl-user', data)
        console.log(htmlstr);

        //5. 渲染html结构
        document.querySelector('#container').innerHTML = htmlstr

    </script>
</body>
```

### 4.2art-template标准语法

提供了{{  }}可以进行<font color='red'>标量输出</font>，或<font color='red'>循环数组</font>

#### 原文输出

```
{{@ value}}  //原文输出
//比如'<h1>hhhh</h1>' 加@才能输出h1格式的hhhh
```

#### 条件输出

```
{{if value}} 按需输出的内容 {{/if}}
```

```html
//条件输出
		const data = {
            flag: 1
        }
        //
		<div>
            {{if flag===1}}
            {{flag}}
            {{if flag===0}}
            {{/if}}      //最终输出flag的值1
        </div>
```

循环输出

```
{{each arr}}
	{{$index}} {{$value}}
{{/each}}
```

```html
		<ul>
            {{each hobby}}
            <li>{{$index}} {{$value}}</li>
            {{/each}}
        </ul>
        const data = {
            hobby: ['吃饭', '睡觉', '写代码']
        }
        //输出 
        0 吃饭
		1 睡觉
		2 写代码
```

#### 过滤器

本质：就是function处理函数

```js
//调用过滤器
{{value | filterName}}  // ‘|’ （管道操作符）代表调用某个函数 左边值 右边处理函数 返回新值
//定义过滤器
template.defaults.imports.filterName = function(value){
	xxx
	return xxx
}  //return返回处理的结果 filterName是自定义函数名
```

## 五.模板引擎的实现原理

### 5.1正则与字符串操作

#### exec()

用于检索字符串中的正则表达式的匹配

如果字符串中有匹配的值，则返回该匹配值，否则返回null。

```
RegExpObject.exec(string)
```

```javascript
var str = 'hello'
var pattern = /o/
//输出结果["o", indew: 4, input: "hello", groups: undefined]
console.log(pattern.exec(str))
```

#### 分组

正则表达式中( )包起来的内容表示一个分组，可以通过分组来<font color='red'>提取自己想要的内容</font>

```javascript
var str = '<div>我是{{name}}</div>'
var pattern = /{{([a-zA-Z]+)}}/

var patternResult = pattern.exec(str)
console.log(patternResult)
//得到name想关的分组信息 即下面的"name"分组将其从中提取了出来
//["{{name}}","name",index:7,input:"<div>我是{{name}}</div>",groups:undfined]
```

#### 字符串的replace函数

用一些字符<font color='red'>替换</font>一些字符

```javascript
var result = '123456'.replace('123','abc') //得到的的值为字符串：'abc456'
```

可以搭配while来替换

replace替换为真值

## 六.XMLHttpRequest

### 6.1 XMLHttpRequest介绍

简称(xhr)是浏览器提供的javascript<font color='red'>对象</font>，通过他，可以请求服务器上的数据资源，jQuery中的AJax函数就是基于xh让封装出的

<font color='red'>**XMLHttpRequest是底层原生**</font>

### 6.2 发起get请求

```html
	<script>

        //1. 创建XHR对象
        const xhr = new XMLHttpRequest()
        //2. 调用open函数 请求方式和URL地址
        xhr.open('GET', 'http://www.liulongbin.top:3006/api/getbooks')
        //3. 调用send函数，发起Ajax请求
        xhr.send()
        //4. 监听onreadystatechange事件
        xhr.onreadystatechange = function () {
            //4.1 监听xhr对象的请求状态 readystate ；与服务器响应的状态 status
            if (xhr.readyState === 4 && xhr.status === 200) {
                //4.2 打印服务器响应回来的数据
                console.log(xhr.responseText);
            }
        }
    </script>
```

### 6.3 xhr的readyState属性

XMLHttpRequest对象的readystate属性，当作当前Ajax<font color='red'>请求所处的状态</font>，每个Ajax必定处于其中一个状态

| 值   | 状态             | 描述                                           |
| ---- | ---------------- | ---------------------------------------------- |
| 0    | UNSENT           | XMLHttpRequest对象已被创建，但未调用open方法   |
| 1    | OPENED           | open()方法已经被调用                           |
| 2    | HEADERS_RECEIVED | send()方法已经被调用，响应头也已经被接收       |
| 3    | LOADING          | 数据接收中，此时response属性中已经包含部分数据 |
| 4    | DONE             | Ajax请求完成，数据传输已经彻底完成或者失败     |

### 6.4 带参数的Get请求

在调用xhr.open()期间 为URL地址指定参数

```
xhr.open('GET', 'http://www.liulongbin.top:3006/api/getbooks?id=1')  //?id=1
```

这种参数叫做<font color='red'>**查询字符串，是键值对的形式**</font>

#### 查询字符串

定义：即URL参数是指在URL末尾家伙是那个用于服务器发送信息的字符串（变量）

<font color='red'>**? 后接 参数=值 使用 &进行分割**</font>

#### get请求带参数的本质：

不管是$.ajax()、$.get()还是xhr方式，都是以查询字符串的形式住家在URL地址之后

### 6.5 URL编码

URL地址不允许出现字母标点数字之外的，如在中文，会进行编码<font color='red'>**（转义）**</font>，使用英文字符表示

浏览器提供了URL编码解码的api

- encodeURI()
- decodeURI()

> 浏览器会自动对URL地址编码

### 6.6 发起post请求

```javascript
		//1. 创建XHR对象
        const xhr = new XMLHttpRequest()
        //2. 调用post函数 请求方式和URL地址
        xhr.open('POST', 'http://www.liulongbin.top:3006/api/addbook')
        //3. 设置 Content-Type 属性 (固定写法)
        xhr.setRequestHeader('Content-Type', 'application/x-www-form-urlencoded')
        //4. 调用send()，同时将数据以查询字符串的形式，提交给服务器
        xhr.send('bookname=水浒传一&author=施耐庵&publisher=天津图书出版社')
            //5. 监听onreadystatechange事件
        xhr.onreadystatechange = function () {
            //5.1 监听xhr对象的请求状态 readystate ；与服务器响应的状态 status
            if (xhr.readyState === 4 && xhr.status === 200) {
                //4.2 打印服务器响应回来的数据 xhr.responseText可能是JSON字符串
                console.log(xhr.responseText);
            }
        }
```

### 6.7自定义Ajax封装（原生xhr编写Ajax请求）

```html
	html文件
	<script>
        // get请求
        itheima({
            method: 'get',
            url: 'http://www.liulongbin.top:3006/api/getbooks',
            data: {
                id: 1
            },
            success: function (res) {
                console.log(res);
            }
        })
        //post请求
        itheima({
            method: 'post',
            url: 'http://www.liulongbin.top:3006/api/addbook',
            data: {
                bookname: '博人传',
                author: 'nnn',
                publisher: '北京出版社'
            },
            success: function (res) {
                console.log(res);
            }
        })
    </script>
```

```javascript
js文件
//数据处理 将输入的对象处理为字符串输出
function resolveData(data) {
    const arr = []
    for (let k in data) {
        let str = k + '=' + data[k]
        arr.push(str)
    }

    return arr.join('&')
}
// console.log(resolveData({ name: 'zs', age: 18 }));

//主函数
function itheima(options) {
    const xhr = new XMLHttpRequest()

    //把外界（用户）传递过来的参数对象，转换为字符串 data数据
    const qs = resolveData(options.data)

    //判断请求是GET还是POST，method是用户传进来的toUpperCase转成统一大写
    if (options.method.toUpperCase() === 'GET') {
        //发起GET请求
        xhr.open(options.method, options.url + '?' + qs)
        xhr.send()
    } else if (options.method.toUpperCase() === 'POST') {
        //发起POST请求
        xhr.open(options.method, options.url)
        xhr.setRequestHeader('Content-Type', 'application/x-www-form-urlencoded')
        xhr.send(qs)
    }

    //监听onreadystatechange事件
    xhr.onreadystatechange = function () {
        if (xhr.readyState === 4 && xhr.status === 200) {
            //打印服务器响应回来的数据 xhr.responseText是JSON格式
            const result = JSON.parse(xhr.responseText);
            //成功之后的回调函数 参数是result对象
            options.success(result)

        }
    }
}
```

## 七.数据交换格式

服务器与客户端之间进行数据传输和交换的格式

有<font color='red'>**XML**</font>和<font color='red'>**JSON**</font>。

### 7.1 XML

可扩展的标记语言 与html相似，都是标记语言，但两者没有任何关系

- html是网页内容的载体
- <font color='red'>**XML是数据的载体**</font>

```
<note>
	<to>ls</to>  //给谁
	<from>zs</from>  //谁给的
	<heading>通知</heading>  //标题
	<body>晚上开会</body>  //内容
</note>
```

### 7.2 JSON

JSON就是JavaScript对象和数组的字符串表示法，它使用文本表示一个Js对象或数组的信息

所以，<font color='red'>**JSON的本质是字符串**</font>，主流的数据交换格式

#### JSON结构

包括<font color='red'>**对象**</font>和<font color='red'>**数组**</font>两种结构，通过互相<font color='red'>**嵌套**</font>

##### 对象结构：

​	{ key: value, key: value, ... }    //键值对

​	**key**：双引号 " " 包裹的 **字符串**

​	**value**：

> <font color='red'>**注意**</font>：JSON都是双引号，不使用单引号
>
> 属性名必须使用双引号，字符串类型也必须使用双引号
>
> <font color='red'>**JSON中不能写注释因为他不是js代码**</font>
>
> 不能使用undefined或函数作为JSON的值

##### 数组结构：

​	["java",30,true ...]

```javascript
//这是一个对象
const bbj = {a: 'hello', b: 'world' }

//这是一个JSON字符串，本质是一个字符串
const json = '{"a": "hello" , "b": "world"}'
```

#### JSON和JS对象的互换

JSON字符串转换成JS对象     叫做 JSON<font color='red'>**反序列化**</font>

```
JSON.parse()
```

JS对象转换成JSON字符串     叫做 JSON<font color='red'>**序列化**</font>

```
JSON.stringify()
```

```
const obj = JSON.parse('{"a": "hello", "b": "world"}')
```

><font color='red'>**应用**</font>：AJax get获得的数据如果是JSON就可以换成js对象格式

## 八.XMLHttpRequest Level2

### 8.1 旧版弊端：

只支持文本传输，无法传输文件和读取文件。传送接受时，没有进度信息，只能提示是否完成。

### 8.2 设置HTTP请求时间-新功能

有时ajax请求很耗时

```
xhr.timeout = 3000    //单位为ms 最长时间过来这个时间，就自动停止HTTP请求
```

```
//超出时间后的事件
xhr.ontimeout = function(event){
	alert('请求超时！')
}
```

> 可以定义完xhr之后就设置

### 8.3 FormData对象管理表单数据-新功能h5新增

原生代码

```javascript
        //1. 创建FormData 实例
        let fd = new FormData()
        //调用append函数，想fd中追加
        fd.append('unname', '123455')
        fd.append('upwd', '212121')

        const xhr = new XMLHttpRequest()
        xhr.open('POST', 'http://www.liulongbin.top:3006/api/formdata')
        xhr.send(fd)
        xhr.onreadystatechange = function () {
            if (xhr.readyState === 4 && xhr.status === 200) {
                console.log(JSON.parse(xhr.responseText));
            }
        }
```

**也可以动态获取网页表单的值进行Ajax请求**

```html
	<form action="" id="form1">
        <input type="text" name="unname" autocomplete="off">
        <input type="password" name="upwd">
        <button type="submit">提交</button>
    </form>

    <script>
        //1. 通过 DOM 操作 获取form表单元素
        const form = document.querySelector('#form1')

        form.addEventListener('submit', function (e) {
            //阻止表单的默认提交行为
            e.preventDefault()

            //创建FormData，快速获取form表单中的信息
            const fd = new FormData(form)

            const xhr = new XMLHttpRequest()
            xhr.open('POST', 'http://www.liulongbin.top:3006/api/formdata')
            xhr.send(fd)
            xhr.onreadystatechange = function () {
                if (xhr.readyState === 4 && xhr.status === 200) {
                    console.log(JSON.parse(xhr.responseText));
                }
            }
        })
    </script>
```

### 8.4 上传文件

1 定义ui结构

```
	<!-- 1.1 文件选择框 -->
    <input type="file" id="file1">
    <!-- 1.2 上传文件的按钮 -->
    <button id="btnUpload">上传文件</button>
    <!-- 1.3 img 标签 用来显示上传成功后的图片 -->
    <img src="" alt="" id="img" width="800">
```



```html
<body>
    <!-- 1.定义ui结构 -->
    <!-- 1.1 文件选择框 -->
    <input type="file" id="file1">
    <!-- 1.2 上传文件的按钮 -->
    <button id="btnUpload">上传文件</button>
    <!-- 1.3 img 标签 用来显示上传成功后的图片 -->
    <img src="" alt="" id="img" width="800">

    <script>
        // 2.验证是否选择了文件
        // 2.1 获取上传文件的按钮
        const btnUpload = document.querySelector('#btnUpload')
        // 2.2 为按钮添加click事件
        btnUpload.addEventListener('click', function () {
            // 2.3 获取到选择的文件列表
            const files = document.querySelector('#file1').files
            if (files.length <= 0) {
            	//若为空提醒
                return alert('请选择上传的文件')
            }
            // 3.向FormData中追加文件
            const fd = new FormData()
            //avatar头项的意思
            fd.append('avatar', files[0])
            //通过xhr上传文件
            const xhr = new XMLHttpRequest()
            xhr.open('POST', 'http://www.liulongbin.top:3006/api/upload/avatar')
            xhr.send(fd)
            xhr.onreadystatechange = function () {
                if (xhr.readyState === 4 && xhr.status === 200) {
                    const data = JSON.parse(xhr.responseText)
                    console.log(data);
                    if (data.status === 200) {
                        //data有status属性
                        document.querySelector('#img').src = 'http://www.liulongbin.top:3006' + data.url
                    } else {
                        console.log('图片上传失败' + data.message);
                    }
                }
            }

        })



    </script>
</body>
```

### 8.5 显示文件上传进度

可以通过监听xhr.upload.onprogress事件，来获取文件的上传速度

```javascript
			//创建XHR对象
            const xhr = new XMLHttpRequest()
			//监听事件上传的速度
            xhr.upload.onprogress = function (e) {
            	//e.lengthComputable是一个布尔值，表示当前上传的资源是否具有可计算的长度
                if (e.lengthComputable) {
                    //计算出上传的速度
                    //e.loaded已传输的字节，e.total需要传输的总字节 ceil上取整
                    const procentComplete = Math.ceil((e.loaded / e.total) * 100)
                    console.log(procentComplete);
                }
            }
```

## 九.jQuery高级

### 9.1 jQuery实现文件上传

```html
	<!-- 1 ui设置 -->
    <input type="file" id="file1">
    <button id="btnUpload">上传</button>


    <script>
        $(function () {
            //  2 验证是否选择了文件 -->
            $('#btnUpload').on('click', function () {
                // 将JQ对象转换成dom对象才能使用.files方法
                const files = $('#file1')[0].files
                if (files.length <= 0) {
                    return alert('请选择文件后再上传')
                }

                const fd = new FormData()
                fd.append('avatar', files[0])

                // 发起JQ的Ajax请求
                $.ajax({
                    method: 'post',
                    url: 'http://www.liulongbin.top:3006/api/upload/avatar',
                    data: fd,
                    //不修改Content-type属性，使用FormData默认的Content-type值
                    processData: false,
                    // 不对FormData中的数据进行URL编码，而是将FormData数据鸳鸯发送到服务器
                    contentType: false,
                    success: function (res) {
                        console.log(res);
                    }
                })
            })
        })
    </script>
```

### 9.2 jQuery实现loading效果

#### ajaxStart（callback）

Ajax请求开始，执行ajaxStart函数，可以在callback中显示loading效果

```js
			// 监听到AJax开始执行，只能附加到文档document上
            $(document).ajaxStart(function () {
                $('#loading').show()
            })
```

#### ajaxStop（callback）

Ajax请求结束时，执行ajaxStopt函数，可以在callback中显示loading效果

```js
            $(document).ajaxStop(function () {
                $('#loading').hide()
            })
```

## 十.axios--非原生

Axios是专注于<font color='red'>**网络数据请求**</font>的库

相比于XHR 它更简单易用

相比于JQ它更轻量化，专注于网络数据请求

> axios是通过Promise实现对ajax技术的一种封装,就像jquery对ajax的封装一样,简单来说就是ajax技术实现了局部数据的刷新,axios实现了对ajax的封装,axios有的ajax都有,ajax有的axios不一定有,总结一句话就是axios是ajax,ajax不止axios

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
        axios.get(url, { params: paramsOBj }).then(function (res) {
            //res.data 是服务器返回的数据
            const result = res.data
            console.log(res.data);
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
        axios.post(url, dataObj).then(function (res) {
            //res.data 是服务器返回的数据
            const result = res.data
            console.log(res.data);
        })
```

### 10.3 直接使用axios发起请求

类似于jq中$.ajax()的函数

```
axios({
	method: '请求类型',
	url: '请求的URL地址',
	data: {  /*POST参数*/  },
	params: {  /*GET参数*/  }
}).then(callback)
```

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

## 十一.同源和跨域

### 11.1 同源

如果两个页面有相同的**协议、域名、端口**，则两个页面具有相同的源

例如：<font color='red'>**http(协议)**</font>://<font color='green'>**www . test . com(域名)**</font>:<font color='blue'>**80(端口默认是80)**</font>/index.html

### 11.2 同源策略

同源策略（Same origin policy）是一种约定，它是**浏览器**最核心也最基本的**安全功能**，如果缺少了同源策略，则浏览器的正常功能可能都会受到影响。可以说Web是构建在同源策略基础之上的，浏览器只是针对同源策略的一种实现。

同源策略是浏览器的行为，是为了保护本地数据不被JavaScript代码获取回来的数据污染，因此拦截的是客户端发出的请求回来的数据接收，即请求发送了，服务器响应了，但是无法被浏览器接收。

### 11.3 跨域

协议、域名、端口任何一个不一致就是跨域

> 浏览器允许发起跨域请求，但是跨域请求回来的数据，会被浏览器同源策略拦截，无法被页面获取到

### 11.4 实现跨域请求 （JSONP、CORS）

JSONP：只支持GET请求

CORS：w3c标准，根本解决方案，支持GET和POST

## 十二.JSONP

原理：HTML 的<script> 元素是一个例外。利用 <script> 元素的这个开放策略，网页可以得到从其他来源动态产生的 JSON 资料，而这种使用模式就是所谓的 JSONP。用 JSONP 抓到的资料并不是 JSON，而是任意的JavaScript，用 JavaScript 直译器执行而不是用 JSON 解析器解析。

**script的src属性可以请求非同源的js脚本，并通过函数调用的形式**

```html
	<script>
        function success(data) {
            console.log('JSONP响应回来的数据');
            console.log(data);

        }
    </script>
	//?后接成功函数&带一些参数传递过去
    <script src="http://www.liulongbin.top:3006/api/jsonp?callback=success&name=ls&age=30"></script>
```

### jQuery中的JSONP

Jq除了可以发起真正的ajax请求还可以发起JSONP数据请求

```js
$.ajax({
    url:'http://www.liulongbin.top:3006/api/jsonp?name=ls&age=30',
    //如果使用$.ajax()发起JSONP请求，必须指定datatype为jsonp
    dataType: 'jsonp',
    success: function(res){
        console.log(res)
    }
})
```

**默认情况下，使用JQ发起JSONP请求，会自动携带一个callback=jQueryxxx的参数，jQueryxxx是一个随机生成的一个回调函数的名称**

#### 自定义参数和回调函数名称

用jQuery发起JSONP请求想要自定义<font color='red'>**参数**</font>和<font color='red'>**回调函数名称**</font>

```js
$.ajax({
    url:'http://www.liulongbin.top:3006/api/jsonp?name=ls&age=30',
    //如果使用$.ajax()发起JSONP请求，必须指定datatype为jsonp
    dataType: 'jsonp',
    
    //发送到服务器的参数名称，默认是callback，通常不会修改
    jsonp: 'callback',
    //自定义的回调函数名称，默认是随机生成的一个回调函数jQueryxxx
    jsonpCallback: 'abc',
    
    success: function(res){
        console.log(res)
    }
})
```

> jQuery实现JSONP的原理也是依靠script的src，他会动态添加，等请求成功再删除

# HTTP

## 13.1 通信

通信的 **主体、内容、方式**

## 13.2 互联网的通信协议

<font color='blue'>网页内容</font>又叫做<font color='red'>超文本</font>,因此<font color='blue'>网页内容的传输协议</font>又叫做<font color='red'>超文本传输协议</font>，简称<font color='red'>**HTTP协议**</font>

## 13.3 HTTP请求消息

由于 `HTTP 协议`属于**客户端浏览器和服务器**之间的**通信协议**。因此，客户端发起的请求叫做 `HTTP 请求`，客户端发送到服务器的消息，叫做 **HTTP 请求消息（HTTP 请求报文）**

HTTP 请求消息由`请求行`（request line）、`请求头部`（ header ） 、`空行` 和 `请求体` 4 个部分组成。

![在这里插入图片描述](https://img-blog.csdnimg.cn/96720e1c506345b19cea925f74c57c11.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBAQ29uY2lzaW9uLg==,size_20,color_FFFFFF,t_70,g_se,x_16)

### 请求行

`请求行`由**请求方式**、**URL** 和 **HTTP 协议版本** 3 个部分组成，他们之间使用空格隔开。

![在这里插入图片描述](https://img-blog.csdnimg.cn/b2b74c58533f44868a8fe9335a983d11.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBAQ29uY2lzaW9uLg==,size_20,color_FFFFFF,t_70,g_se,x_16)

### 请求头部

请求头部用来描述客户端的基本信息，从而把客户端相关的信息告知服务器。比如：

- User-Agent用来说明当前是什么类型的浏览器；
- Content-Type用来描述发送到服务器的数据格式；
- Accept 用来描述客户端能够接收什么类型的返回内容；
- Accept-Language用来描述客户端期望接收哪种人类语言的文本内容。

![在这里插入图片描述](https://img-blog.csdnimg.cn/c4c692b687da48e9a074e305bfefb8dd.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBAQ29uY2lzaW9uLg==,size_20,color_FFFFFF,t_70,g_se,x_16)

请求头部由多行 `键/值对` 组成，每行的键和值之间用英文的冒号分隔。

![在这里插入图片描述](https://img-blog.csdnimg.cn/634f81820f0940bc8bc2e0c2faf1bd0d.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBAQ29uY2lzaW9uLg==,size_20,color_FFFFFF,t_70,g_se,x_16)

![在这里插入图片描述](https://img-blog.csdnimg.cn/fb9b2b95582342308a01662507ec9396.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBAQ29uY2lzaW9uLg==,size_20,color_FFFFFF,t_70,g_se,x_16)

`注意`：详细说明可参考MDN官方文档[链接](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Headers)

### 空行

最后一个请求头字段的后面是一个**空行**，通知服务器请求头部至此结束。**请求消息中的空行，用来分隔请求头部与请求体。**

![在这里插入图片描述](https://img-blog.csdnimg.cn/cdd54b63ed294317886e8b4cc79964ce.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBAQ29uY2lzaW9uLg==,size_20,color_FFFFFF,t_70,g_se,x_16)

### 请求体

请求体中存放的，是要通过 `POST 方式` 提交到服务器的数据。

`注意`**只有 POST 请求才有请求体，GET 请求没有请求体！**

![在这里插入图片描述](https://img-blog.csdnimg.cn/777ee81783474649a085e7872be77f86.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBAQ29uY2lzaW9uLg==,size_20,color_FFFFFF,t_70,g_se,x_16)

![在这里插入图片描述](https://img-blog.csdnimg.cn/edc91e9f2eba4a2f9cbe00271bd1e5e3.png)

## 13.4 HTTP响应消息

1. **响应消息**就是**服务器**响应给**客户端**的消息内容，也叫作`响应报文`。
2. `HTTP响应消息`由**状态行、响应头部、空行 和 响应体** 4 个部分组成，如下图所示：

![在这里插入图片描述](https://img-blog.csdnimg.cn/45a642fcda52461b823a2c3f467c7d0b.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBAQ29uY2lzaW9uLg==,size_20,color_FFFFFF,t_70,g_se,x_16)

### 状态行

状态行由 `HTTP 协议版本`、`状态码`和`状态码的描述文本` 3 个部分组成，他们之间使用空格隔开;

![在这里插入图片描述](https://img-blog.csdnimg.cn/a96916e8a092475a87e1b4d0f0ab3aba.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBAQ29uY2lzaW9uLg==,size_20,color_FFFFFF,t_70,g_se,x_16)

### 响应头部

响应头部用来描述**服务器的基本信息**。响应头部由多行`键/值对` 组成，每行的键和值之间用英文的冒号分隔。

![在这里插入图片描述](https://img-blog.csdnimg.cn/188ebdf5354a47a98c07a044c6c3f200.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBAQ29uY2lzaW9uLg==,size_20,color_FFFFFF,t_70,g_se,x_16)

`注意`：详细说明可参考MDN官方文档[链接](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Headers)

### 空行

在最后一个响应头部字段结束之后，会紧跟一个空行，用来通知客户端响应头部至此结束。**响应消息中的空行，用来分隔响应头部与响应体**。

![在这里插入图片描述](https://img-blog.csdnimg.cn/563f82428aa04d7a9cbf3f02683ded0d.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBAQ29uY2lzaW9uLg==,size_20,color_FFFFFF,t_70,g_se,x_16)

### 响应体

响应体中存放的，是**服务器响应给客户端的资源内容**。

![在这里插入图片描述](https://img-blog.csdnimg.cn/bec27734575c4fd5a8c3dba545dcc262.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBAQ29uY2lzaW9uLg==,size_20,color_FFFFFF,t_70,g_se,x_16)

## 13.5 HTTP请求方法

HTTP 请求方法，属于 HTTP 协议中的一部分，其作用是：**表明要对服务器上的资源执行的操作**。最常用的请求方法是 GET 和 POST。

![在这里插入图片描述](https://img-blog.csdnimg.cn/cf9158db81844171be6f891418846826.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBAQ29uY2lzaW9uLg==,size_20,color_FFFFFF,t_70,g_se,x_16)

## 13.6 HTTP响应状态代码

`HTTP 响应状态码`（HTTP Status Code），也属于 HTTP 协议的一部分，用来标识**响应的状态**。**响应状态码会随着响应消息一起被发送至客户端浏览器**，浏览器根据服务器返回的响应[状态码](https://so.csdn.net/so/search?q=状态码&spm=1001.2101.3001.7020)，就能知道这次 HTTP 请求的结果是成功还是失败了。

### 组成及分类

`HTTP 状态码`由`三个十进制数字`组成，**第一个十进制数字定义了状态码的类型**，后两个数字用来对状态码进行细分。**HTTP 状态码共分为 5 种类型：**

![在这里插入图片描述](https://img-blog.csdnimg.cn/c46d335e9f224b4db8f78c0995a87f11.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBAQ29uY2lzaW9uLg==,size_20,color_FFFFFF,t_70,g_se,x_16)

`注意`：详细内容可查看MDN官方文档[链接](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Status)

### 2**的响应状态码

`2**`范围的状态码，表示**服务器已成功接收到请求并进行处理**。

![在这里插入图片描述](https://img-blog.csdnimg.cn/fca40f462116451db79800676dbc0ec8.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBAQ29uY2lzaW9uLg==,size_20,color_FFFFFF,t_70,g_se,x_16)

### 3**的响应状态码

`3** 范围的状态码`，表示**服务器要求客户端重定向，需要客户端进一步的操作以完成资源的请求**。

![在这里插入图片描述](https://img-blog.csdnimg.cn/fe003dc8cf804036939ea17ea98b0c57.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBAQ29uY2lzaW9uLg==,size_20,color_FFFFFF,t_70,g_se,x_16)

### 4**的响应状态码

`4**`范围的状态码，表示**客户端的请求有非法内容，从而导致这次请求失败**。

![在这里插入图片描述](https://img-blog.csdnimg.cn/7917b8fdb45e41e4a7406a6b259dbf0e.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBAQ29uY2lzaW9uLg==,size_20,color_FFFFFF,t_70,g_se,x_16)

### 5**的响应状态码

`5**` 范围的状态码，表示**服务器未能正常处理客户端的请求而出现意外错误**。

![在这里插入图片描述](https://img-blog.csdnimg.cn/9c96ede5bd8c48bcb70040539456b8bd.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBAQ29uY2lzaW9uLg==,size_20,color_FFFFFF,t_70,g_se,x_16)

# Git

### 版本控制软件

版本控制软件（版本控制规划系统）用来记录文件变化

#### 分类：

本地版本控制系统、集中化版本控制系统、**分布式版本控制系统（Git）**

## 1 什么是Git

Git（读音为/gɪt/）是一个开源的分布式版本控制系统，可以有效、高速地处理从很小到非常大的项目版本管理。

## 2.1 SVN的差异比较

传统的版本控制系统SVN基于差异的版本控制，他存储的是一组基本文件和每个文件随时间逐步累积的差异

## 2.2 Git的快照记录

是在原有文件版本基础上重新生成一份新的文件，类似于备份，如果文件没有修改，git不再重新存储该文件，而是保留一个链接指向之前存储的文件。

占用此版空间大，但切换较快

Git操作绝大多数操作在本地完成，都**只需访问本地文件和资源**

## 3 Git的三个区域

**工作区、暂存区、Git仓库**

## 4 Git中的三种状态

**已修改、已暂存、已提交**

## 5 Git基本的工作流程

1. 在工作区修改文件
2. 将你想要下次提交的更改进行暂存
3. 提交更新，找到暂存区的文件，将1快照永久性存储在Git仓库中

## 6 Git使用

```
# 用户名和邮箱
git config --global user.name "xxx"
git config --global user.email "zxxx"
```

配置文件C:\Users\shizeyu/.gitconfig

```
# 查看配置信息
$ git config --list --global

$ git config user.name
```

```
# 帮助手册
$ git help config
# 简明版
$ git config -h
```

### 1 获取Git仓库的两种方式

1. 在现有目录中初始化仓库:

   在项目根目录中，通过鼠标右键打开Git Bash

   执行<font color='red'>**git init**</font>命令，创建一个隐藏的.git目录，**这个目录就是当前项目的Git仓库**

2. 从其他服务器克隆一个

### 2 工作区的4种状态

![img](https://pic1.zhimg.com/80/v2-77c35c21defc40aab86e73a14e9e5c64_1440w.jpg)

`git操作终极结果`：让工作区的文件都处于 “ 未修改 ” 的状态 

### 3 检查文件的当前状态

<font color='red'>**git status**</font>命令查看文件处于什么状态

![img](https://pic1.zhimg.com/80/v2-fb84af3a37c273764bd4f29349f15c60_1440w.jpg)

### 4 精简的方式显示文件状态

 <font color='red'>**git status -s**</font>

![img](https://pic3.zhimg.com/80/v2-902d295c450da81f60f357116b5d1f02_1440w.jpg)

### 5 跟踪新文件 文件进入暂存区

<font color='red'>**git add**</font> 跟踪完可以继续使用git status查看情况 新添加到暂存区中的文件前面有绿色的A标记

![img](https://pic1.zhimg.com/80/v2-65fdb2cf12308b11c8935c8941624490_1440w.jpg)

![img](https://pic4.zhimg.com/80/v2-c6f0371222f0ea5fdc80a2e541edaebf_1440w.jpg)

### 6 提交更新 文件从暂存区进库

```
git commit -m "需要显示的消息"
```

![img](https://pic2.zhimg.com/80/v2-ad186a9002be52cad5852bfce8f4d5a5_1440w.jpg)

![img](https://pic2.zhimg.com/80/v2-dc44ef07e2a604946ee42093962f7ab9_1440w.jpg)

### 7 对已经提交的文件修改

![img](https://pic1.zhimg.com/80/v2-1a4115deb45c00a96d29abc9ea49ca6c_1440w.jpg)

`注意`：红色的<font color='red'>**M**</font> 表示已近修改但是没有放到暂存区

### 8 暂存已修改的文件 修改文件放入暂存区

![img](https://pic1.zhimg.com/80/v2-65fdb2cf12308b11c8935c8941624490_1440w.jpg)

![img](https://pic4.zhimg.com/80/v2-e522f4fd03bde9c41615cf1681dfc6bf_1440w.jpg)

### 9 提交已暂存的文件

![img](https://pic1.zhimg.com/80/v2-3a3d7549487d5f416160d143274d8bf4_1440w.jpg)

### 10 撤销对文件的修改

```
git checkout -- index.html
```

![img](https://pic2.zhimg.com/80/v2-5b140b1174cbc8937fb761c4f0b4532d_1440w.jpg)

`本质：用Git仓库中保存额文件，覆盖了工作区中指定的文件。`

### 11 向暂存区一次性添加多个文件

```
git add .
```

![img](https://pic3.zhimg.com/80/v2-a2cce7ff6dda6c9dacbb75a95cf5d79e_1440w.jpg)

> 高频使用

### 12 取消暂存的文件

```
git reset HEAD index.html
```

![img](https://pic3.zhimg.com/80/v2-2525f70da424cdc904001c394a3c3446_1440w.jpg)

### 13 跳过暂存区

```
git commit -a -m "描述信息"
```

![img](https://pic2.zhimg.com/80/v2-986319aa1e4bb2e998530d48e15886ad_1440w.jpg)

**`注意:前提是要跟踪的文件`**

### 14 移除文件

```
git rm -f index.js
git rm --cached index.css
```

![img](https://pic3.zhimg.com/80/v2-6bcde3fa68d7d661522e77fde4df90fa_1440w.jpg)

**`注意:移除后文件会显示绿色的D,表示提交后移除，需要git commit -a -m提交操作才能移除，保留工作区的文件即本地文件还会保留，呈现？？未跟踪状态`**

### 15 忽略文件

![img](https://pic3.zhimg.com/80/v2-d7c42bdec5c0b5a2a6ca4f0b6d1bcf42_1440w.jpg)

![img](https://pic1.zhimg.com/80/v2-c21fa6a9187c808fbdad1b91c6b9cf1c_1440w.jpg)

```c
# 忽略所有的.a文件
*.a

# ！取反，上面忽略了所有.a文件，但跟踪！后的文件
！lib.a

# 只忽略当前目录下的TODO文件，不忽略其他的
/TODO

# 忽略任何目录下名为build的文件夹
build/

# 忽略 doc下的.txt文件，但不忽略 子目录下的.txt文件,比如doc/sorver/sada.txt
doc/*.txt

# 忽略 doc 目录及其子目录下所有的.pdf文件
doc/**/*.pdf
```

### 16 查看提交历史

```
# 按时间先后顺序列出提交历史，最近的排最上面
git log

# 只展示最新的两条提交历史，数字可以按需进行填写3给就是-3
git log -2

# 在一行上展示最近两条提交历史
git log -2 --pretty=oneline

# 在一行上展示最近两条提交历史的信息，并自定义输出的格式
# %h 提交的简写哈希值编码  %an作者的名字   %ar作者修订日期，按多久以前的方式显示   %s提交说明
git log -2 --pretty=format:"%h | %an | %ar | %s"
```

### 17 回退到指定的版本

```
# 在一行上展示最近两条提交历史
git log -2 --pretty=oneline

# 使用 git reset --hard命令，根据指定的提交ID回退到指定版本
git reset --hard <CommitID>

# 在旧版本中使用 git reflog --pretty=oneline 命令，查看命令操作的历史
git reflog --pretty=oneline

# 再次根据指定的提交ID，跳转到最新的版本
git reset --hard <CommitID>
```



# Github

开源项目托管平台

## 访问方法

1. HTTPS：零配置，每次访问仓库都要输入Github的账号和密码
2. SSH：需要进行额外的配置   （git@开头）

![img](https://img-blog.csdnimg.cn/7b65b10acda3492187be4a664378e824.png)

**第二次更新只需要git push就行了**







# Vue

## 1.什么是vue

用于构建用**户见界面**的**框架**

1 构建用户界面

- 用Vue往html页面中填充数据

2 框架

- 框架是一套现成的解决方案，程序员只能遵守框架的规则，去编写的自己的
- 要学习vue，就是在学习vue的框架的用法
- vue的指令、组件（是对ui结构的复用cv工程师）、路由Vuex、Vue组件库

## 2.vue的两个特性

1 数据驱动视图

- 数据的变化会驱动视图自动更新
- 单向的：页面依赖的数据变化→vue监听数据的变化→（自动渲染）→页面结构

2 双向数据绑定

> 在页面中，form表单负责采集数据，Ajax负责提交数据

- js数据的变化，会被自动渲染到页面上
- 页面上表单的数据发生变化时会被vue自动获取到，并更新到js数据中

> 双向影响
>
> 数据驱动视图和双向数据绑定的底层原理是MVVM（Mode 数据源、View 视图、ViewModel就是Vue示例）

# vue的基本使用

## 1.基本步骤

new Vue（）

① 导入vue.js的script脚本文件

```
<script src="./vue.js"></script>
```

②在页面中声明一个将要被vue所控制的DOM区域

③创建vm实例对象（vue实例对象）

```
	<!-- Vue控制的div -->
    <div id="app">{{ username }}</div> //输出uername的值 zhangsan

    <!-- 导入Vue库文件，在window全局就有了Vue这个构造函数 -->
    <script src="./vue.js"></script>
    <!-- 创建Vue实例对象 -->
    <script>
    // 创建Vue实例对象，属性固定写法el，表示当前vm实例要控制页面上的哪个区域，接受的值是一个选择器，data对象就是要渲染到页面上的值
        constvm = new Vue({	
            el: '#app',
            data: {
                username: 'zhangsan'
            }
        })

    </script>
```

























































