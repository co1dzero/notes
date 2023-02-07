# Node.js

### 思考：为什么 JavaScript 可以在浏览器中被执行？

答：依靠 JavaScript 解析引擎

- Chrome：V8
- Firefox：OdinMonkey（奥丁猴）
- Safari：JSCore
- IE：Chakra（IE 已经淘汰，微软最新的 Edge 浏览器使用 V8）

> Chrome 浏览器的 V8 解析引擎是目前世界上性能最好的 JS 解析引擎！

------

### 思考：为什么 JavaScript 可以操作 DOM 和 BOM？

答：每个浏览器都内置了 DOM、BOM 相关的 API 接口函数，因此，浏览器中的 JavaScript 才能调用它们。

## 1. Node.js 是什么

Node.js 的官网地址：https://nodejs.org/zh-cn/

`Node.js` 是一个基于 `Chrome V8` 引擎的 `JavaScript` 运行环境。

> 我们写了一段js放到浏览器中执行就是**前端开发**，如果js放到node执行就是**后端开发**了

>传统的 JavaScript 只能运行在浏览器端，脱离浏览器不能运行，也就不能操作本地的文件或者创建文件，也不能进行网络编程，Node.js 的出现打破了这一局面。
>Node.js 编写的代码还是 JS，所以开发者需要利用 Chrome V8 来运行 JS。Node.js 借助了 C/C++ 中的 libuv 库来实现文件读取和事件循环。我们不必深挖其中的原理，只需要知道如何使用就行，Node.js 已经为我们打包好了相关接口。

- 浏览器是 JavaScript 的前端运行环境
- Node.js 是 JavaScript 的后端运行环境
- Node.js 中无法调用 DOM 和 BOM 等浏览器内置的API

![](C:\Users\shizeyu\Desktop\notes\Ajax-vue\Snipaste_2023-01-13_16-22-18.png)

## 2. Node.js可以做什么？

Node.js 作为一个独立于浏览器的 JS 运行环境，仅仅提供了基础的功能和 API。然而，基于 Node.js 提供的这些基础，很多强大的工具和框架如雨后春笋，层出不穷，所以学会了 Node.js，可以让前端程序员具备全栈开发能力：

- 基于 Express/Koa 框架，可以快速构建 Web 应用
- 基于 Electron 框架，可以构建跨平台的桌面应用
- 基于 restify 框架，可以快速构建 API 接口项目
- 读写和操作数据库、创建实用的命令行工具辅助前端开发……

## 3. Node.js怎么学

浏览器中的 JavaScript 学习路径：

JavaScript 基础语法 + 浏览器内置 API（DOM + BOM）+ 第三方库（jQuery、art-template 等）

**Node.js 的学习路径：**

**JavaScript 基础语法** + <font color='red'>Node.js 内置 API 模块</font>（fs、path、http 等）+ <font color='red'>第三方 API 模块</font>（express、mysql 等）

## 4. Node.js环境的安装

Node.js 官网：https://nodejs.org/zh-cn/

点击绿色按钮进行下载，下载后打开安装包，默认下一步安装（对于这类基础环境推荐安装路径默认 C 盘）。

[![image-20221130205640710](https://github.com/JERRY-Z-J-R/I-love-you-3-thousand/raw/master/%E6%88%91%E7%88%B1%E4%BD%A0%EF%BC%8C%E4%B8%8D%E6%AD%A2%E4%B8%89%E5%8D%83%E9%81%8D/Node/01-%E5%88%9D%E5%A7%8BNode/mark-img/image-20221130205640710.png)](https://github.com/JERRY-Z-J-R/I-love-you-3-thousand/blob/master/我爱你，不止三千遍/Node/01-初始Node/mark-img/image-20221130205640710.png)

> 区分 LTS 版本和 Current 版本的不同
>
> - LTS 为长期稳定版，对于追求稳定性的企业级项目来说，推荐安装 LTS 版本的 Node.js
> - Current 为新特性尝鲜版，对于热衷于尝试新特性的用户来说，推荐安装 Current 版本的 Node.js。但是，Current 版本中可能存在隐藏的 Bug 或安全性漏洞，因此不推荐在企业级项目中使用 Current 版本的 Node.js

查看已安装的 Node.js 的版本号：终端中输入 `node -v`，如果命令能够成功识别就证明 Node.js 已经安装成功。

如果无法识别 `node` 命令，那么请在环境变量 **Path** 中添加 Node.js 安装包的根路径后再次尝试。

利用 Node.js 执行 JavaScript 脚本：

```
// hello.js
console.log('Hello Node.js');
```

在 hello.js 文件所在路径下打开终端执行命令：`node hello.js`，控制台成功输出 **Hello Node.js** 即为成功。

> 如果`.js`文件不在终端所处的当前路径下，那么执行命令中需要带上文件路径：`node ..\code\hello.js`。

> 终端使用技巧：
>
> - 使用 `↑` 键，可以快速定位到上一次执行的命令
> - 使用 `tab` 键，能够快速补全路径
> - 使用 `esc` 键，能够快速清空当前已输入的命令（Linux、MacOS 中为：`ctrl + u`）
> - 输入 `cls` 命令，可以清空终端（Linux、MacOS 中为：`clear`）

Node.js 详细内容请查阅文档：

[Docs | Node.js (nodejs.org)](https://nodejs.org/zh-cn/docs/)

[Node.js 中文文档 | Node.js 中文网 (nodeapp.cn)](https://www.nodeapp.cn/)

# fs文件系统模块

## 一、什么是fs文件系统模块

fs 模块是 Node.js 官方提供的，用来操作文件的模块。它提供了一系列的方法和属性，用来满足用户对文件的操作需求。

例如：

- `fs.readFile()`方法，用来<font color='red'>读取</font>指定文件中的内容
- `fs.writeFile()`方法，用来向指定的文件中<font color='red'>写入</font>内容

如果要在 JavaScript 代码中，使用 fs 模块来操作文件，则需要使用如下的方式先<font color='red'>导入</font>它：

```js
const fs = require('fs');
```

## 二、读取指定文件中的内容

### 2.1 fs.readFile()的语法格式

使用`fs.readFile()`方法，可以读取指定文件中的内容，语法格式如下：

```js
fs.readFile(path[, options], callback)
```

参数解读：

- 参数1：<font color='red'>必选</font>参数，字符串，表示文件的路径
- 参数2：可选参数，表示以什么样的<font color='red'>编码格式</font>来读取文件，默认值是 null（如果未指定字符编码，则返回原始的 buffer）
- 参数3：<font color='red'>必选</font>参数，文件读取完成后，通过回调函数拿到读取的结果

### 2.2 fs.readFile()的示例代码

以 `UTF-8` 的编码格式为例，读取指定文件的内容，并打印 err 和 dataStr 的值：

```js
const fs = require('fs');

fs.readFile('文件路径', 'utf8', function(err, dataStr) {
    console.log(err);
    console.log('---------------');
    console.log(dataStr);
})
```

正式测试：

在`./files/`目录下有一个`test.txt`文件，内容为：`Wow~`。

代码：

```js
// 导入 fs 模块来操作文件
const fs = require('fs');

// 调用 fs.readFile() 方法读取文件
// 参数1：待读取文件的存放路径
// 参数2：读取文件时采用的编码格式，一般默认指定 utf8
// 参数3：回调函数，拿到读取失败err 和成功的结果 dataStr
fs.readFile('./files/test.txt', 'utf8', (err, dataStr) => {
    // 如果读取成功，则 err 的值为 null
    // 如果读取失败，则 err 的值为错误对象，dataStr 的值为 undefined

    // 失败时，打印失败的结果：
    console.log(err);
    console.log('---------------');
    // 成功时，打印成功的结果：
    console.log(dataStr);
})
```

运行结果：

[![image-20221201191734477](https://github.com/JERRY-Z-J-R/I-love-you-3-thousand/raw/master/%E6%88%91%E7%88%B1%E4%BD%A0%EF%BC%8C%E4%B8%8D%E6%AD%A2%E4%B8%89%E5%8D%83%E9%81%8D/Node/02-fs%E6%96%87%E4%BB%B6%E7%B3%BB%E7%BB%9F%E6%A8%A1%E5%9D%97/mark-img/image-20221201191734477.png)](https://github.com/JERRY-Z-J-R/I-love-you-3-thousand/blob/master/我爱你，不止三千遍/Node/02-fs文件系统模块/mark-img/image-20221201191734477.png)

如果，我们将路径故意修改错误：`./files/err.txt`，再次运行：

[![image-20221201192034834](https://github.com/JERRY-Z-J-R/I-love-you-3-thousand/raw/master/%E6%88%91%E7%88%B1%E4%BD%A0%EF%BC%8C%E4%B8%8D%E6%AD%A2%E4%B8%89%E5%8D%83%E9%81%8D/Node/02-fs%E6%96%87%E4%BB%B6%E7%B3%BB%E7%BB%9F%E6%A8%A1%E5%9D%97/mark-img/image-20221201192034834.png)](https://github.com/JERRY-Z-J-R/I-love-you-3-thousand/blob/master/我爱你，不止三千遍/Node/02-fs文件系统模块/mark-img/image-20221201192034834.png)

err 不再是`null`，而是错误信息：no such file or directory（没有这样的文件或目录）。

### 2.3 判断文件是否读取成功

方法：通过判断 err 对象是否为`null`，从而判断文件是否读取成功。

```js
const fs = require('fs');

fs.readFile('./files/test.txt', 'utf8', (err, result) => {
    if (err) {
        return console.log('文件读取失败！' + err.message);
    }
    console.log('文件读取成功，内容是：' + result);
})
```

成功时：

[![image-20221201202128017](https://github.com/JERRY-Z-J-R/I-love-you-3-thousand/raw/master/%E6%88%91%E7%88%B1%E4%BD%A0%EF%BC%8C%E4%B8%8D%E6%AD%A2%E4%B8%89%E5%8D%83%E9%81%8D/Node/02-fs%E6%96%87%E4%BB%B6%E7%B3%BB%E7%BB%9F%E6%A8%A1%E5%9D%97/mark-img/image-20221201202128017.png)](https://github.com/JERRY-Z-J-R/I-love-you-3-thousand/blob/master/我爱你，不止三千遍/Node/02-fs文件系统模块/mark-img/image-20221201202128017.png)

失败时（err.txt 文件不存在）：

[![image-20221201202202132](https://github.com/JERRY-Z-J-R/I-love-you-3-thousand/raw/master/%E6%88%91%E7%88%B1%E4%BD%A0%EF%BC%8C%E4%B8%8D%E6%AD%A2%E4%B8%89%E5%8D%83%E9%81%8D/Node/02-fs%E6%96%87%E4%BB%B6%E7%B3%BB%E7%BB%9F%E6%A8%A1%E5%9D%97/mark-img/image-20221201202202132.png)](https://github.com/JERRY-Z-J-R/I-love-you-3-thousand/blob/master/我爱你，不止三千遍/Node/02-fs文件系统模块/mark-img/image-20221201202202132.png)

## 三、向指定的文件中写入内容

### 3.1 fs.writeFile()的语法格式

使用`fs.writeFile()`方法，可以向指定的文件中写入内容，语法格式如下：

```js
fs.writeFile(file, data[, options], callback)
```

参数解读：

- 参数1：<font color='red'>必选</font>参数，需要指定一个<font color='red'>文件路径的字符串</font>，表示文件的存放路径
- 参数2：<font color='red'>必选</font>参数，表示要写入的内容
- 参数3：可选参数，表示以什么编码格式写入文件内容，默认值是 utf8
- 参数4：<font color='red'>必选</font>参数，文件写入完成后的回调函数

> <font color='red'>**注意**</font>：
>
> - `fs.writeFile()`方法写入时可以创建文件，但不能凭空创建路径！
> - `fs.writeFile()`方法多次对同一文件进行写入，后写入的会覆盖先写入的！

### 3.2 fs.writeFile()的实例代码

向指定的文件路径中，写入文件内容：

```js
const fs = require('fs');

fs.writeFile('文件路径', 'XXXXXXXXXX', function(err) {
    console.log(err);
})
```

向指定的文件路径中，写入 “Hello Node.js” 文件内容：

```js
const fs = require('fs');

fs.writeFile('./files/hello.txt', 'Hello Node.js!', err => {
    // 如果文件写入成功，则 err 的值为 null
    // 如果文件写入失败，则 err 的值为一个 错误对象
    console.log(err);
})
```

运行结果：

[![image-20221201203749988](https://github.com/JERRY-Z-J-R/I-love-you-3-thousand/raw/master/%E6%88%91%E7%88%B1%E4%BD%A0%EF%BC%8C%E4%B8%8D%E6%AD%A2%E4%B8%89%E5%8D%83%E9%81%8D/Node/02-fs%E6%96%87%E4%BB%B6%E7%B3%BB%E7%BB%9F%E6%A8%A1%E5%9D%97/mark-img/image-20221201203749988.png)](https://github.com/JERRY-Z-J-R/I-love-you-3-thousand/blob/master/我爱你，不止三千遍/Node/02-fs文件系统模块/mark-img/image-20221201203749988.png)

[![image-20221201203757306](https://github.com/JERRY-Z-J-R/I-love-you-3-thousand/raw/master/%E6%88%91%E7%88%B1%E4%BD%A0%EF%BC%8C%E4%B8%8D%E6%AD%A2%E4%B8%89%E5%8D%83%E9%81%8D/Node/02-fs%E6%96%87%E4%BB%B6%E7%B3%BB%E7%BB%9F%E6%A8%A1%E5%9D%97/mark-img/image-20221201203757306.png)](https://github.com/JERRY-Z-J-R/I-love-you-3-thousand/blob/master/我爱你，不止三千遍/Node/02-fs文件系统模块/mark-img/image-20221201203757306.png)

### 3.3 判断文件是否写入成功

方法：通过判断 err 对象是否为`null`，从而判断文件是否写入成功。

```js
const fs = require('fs');

fs.writeFile('./files/hello.txt', 'Hello Node.js!', err => {
    if (err) {
        return console.log('文件写入失败！' + err.message);
    }
    console.log('文件写入成功！');
})
```

成功时：

[![image-20221201204809179](https://github.com/JERRY-Z-J-R/I-love-you-3-thousand/raw/master/%E6%88%91%E7%88%B1%E4%BD%A0%EF%BC%8C%E4%B8%8D%E6%AD%A2%E4%B8%89%E5%8D%83%E9%81%8D/Node/02-fs%E6%96%87%E4%BB%B6%E7%B3%BB%E7%BB%9F%E6%A8%A1%E5%9D%97/mark-img/image-20221201204809179.png)](https://github.com/JERRY-Z-J-R/I-love-you-3-thousand/blob/master/我爱你，不止三千遍/Node/02-fs文件系统模块/mark-img/image-20221201204809179.png)

失败时（路径不存在，电脑上没有 w 盘符）：

[![image-20221201204916749](https://github.com/JERRY-Z-J-R/I-love-you-3-thousand/raw/master/%E6%88%91%E7%88%B1%E4%BD%A0%EF%BC%8C%E4%B8%8D%E6%AD%A2%E4%B8%89%E5%8D%83%E9%81%8D/Node/02-fs%E6%96%87%E4%BB%B6%E7%B3%BB%E7%BB%9F%E6%A8%A1%E5%9D%97/mark-img/image-20221201204916749.png)](https://github.com/JERRY-Z-J-R/I-love-you-3-thousand/blob/master/我爱你，不止三千遍/Node/02-fs文件系统模块/mark-img/image-20221201204916749.png)

## 四、练习：考试成绩整理

要求：使用 fs 文件系统模块，将素材目录下**成绩.txt**文件中的考试数据，整理到**成绩-ok.txt**文件中。

整理前：

```
小红=99 小白=100 小黄=70 小黑=66 小绿=88
```

整理后：

```
小红：99
小白：100
小黄：70
小黑：66
小绿：88
```

实现步骤：

- 导入需要的 fs 文件系统模块
- 使用 fs.readFile() 方法，读取素材目录下的 成绩.txt 文件
- 判断文件是否读取失败
- 文件读取成功后，处理成绩数据
- 将处理完成的成绩数据，调用 fs.writeFile() 方法，写入到新文件 成绩-ok.txt 中
- 判断文件是否写入成功

实现代码：

```js
const fs = require('fs');

// 调用 fs.readFile() 方法，读取成绩数据
fs.readFile('./files/成绩.txt', 'utf8', (err, dataStr) => {
    if (err) {
        return console.log('文件读取失败：' + err.message);
    }

    // 将成绩数据按照空格进行分割
    const arrOld = dataStr.split(' ');

    // 循环分割后的数组，对每一项数据进行字符串的替换操作
    const arrNew = [];
    arrOld.forEach(item => {
        arrNew.push(item.replace('=', '：'));
    })

    // 把新数组中的每一项进行合并，得到一个新的字符串
    const newStr = arrNew.join('\r\n');

    // 调用 fs.writeFile() 方法，把处理完的成绩数据，写入到新文件中
    fs.writeFile('./files/成绩-ok.txt', newStr, err => {
        if (err) {
            return console.log('文件写入失败：' + err.message);
        }
        console.log('文件写入成功！')
    })
})
```

## 五、路径动态拼接问题

在使用 fs 模块操作文件时，如果提供的操作路径是以`./`或`../`开头的相对路径时，<font color='red'>很容易出现路径动态拼接错误的问题</font>。

原因：代码在运行的时候，会以执行 node 命令时所处的目录，动态拼接出被操作文件的完整路径。

[![image-20221202191526595](https://github.com/JERRY-Z-J-R/I-love-you-3-thousand/raw/master/%E6%88%91%E7%88%B1%E4%BD%A0%EF%BC%8C%E4%B8%8D%E6%AD%A2%E4%B8%89%E5%8D%83%E9%81%8D/Node/02-fs%E6%96%87%E4%BB%B6%E7%B3%BB%E7%BB%9F%E6%A8%A1%E5%9D%97/mark-img/image-20221202191526595.png)](https://github.com/JERRY-Z-J-R/I-love-you-3-thousand/blob/master/我爱你，不止三千遍/Node/02-fs文件系统模块/mark-img/image-20221202191526595.png)

<font color='red'>解决方案：</font>在使用 fs 模块操作文件时，

1. <font color='red'>直接提供完整的路径（绝对路径）</font>，从而防止路径动态拼接的问题，但是这样的解决方案存在非常大的缺陷，因为一但文件代码的路径发生变动，或者项目在文件结构不同的机器中进行了迁移，那么这个绝对路径就会立马失效，所以这不是一个好的解决办法。

   > 注：**转义字符 “ \\ ”**
   >
   > **作用：**用于表示一个反斜杠，防止它被解释为一个转义序列符。
   >
   > ```c
   > int main()
   > {
   > 	printf("\\");
   > 	// 将会打印出\（反斜杠）
   > 	return 0;
   > }
   > ```

2. <font color='red'>Node.js 提供的解决方案：</font>`__dirname`。

`__dirname`：总是指向被执行 js 文件的绝对路径（即：当前文件所处绝对路径）。

```js
const fs = require('fs');

fs.readFile(__dirname + '/files/test.txt', 'utf8', (err, dataStr) => {
    if (err) {
        return console.log('文件读取失败：' + err.message);
    }
    console.log(dataStr);
})
```



## 六、path路径模块

### 6.1 什么是path路径模块

path 模块是 Node.js 官方提供的、用来处理路径的模块。它提供了一系列的方法和属性，用来满足用户对路径的处理需求。

例如：

- `path.join()`方法，用来将多个路径片段拼接成一个完成的路径字符串
- `path.basename()`方法，用来从路径字符串中，将文件名解析出来
- `path.extname()`方法，用来从路径字符串中，将文件扩展名解析出来

如果要在 JavaScirpt 代码中，使用 path 模块来处理路径，则需要使用如下的方式先导入它：

```js
const path = require('path');
```

### 6.2 路径拼接

`path.join()`的语法格式：

使用`path.join()`方法，可以把多个路径片段拼接为完整的路径字符串，语法格式如下：

```js
path.join([...paths])
```

参数解读：

- ...paths：字符串，路径片段序列
- 返回值：字符串，合成路径

代码示例：

```js
const path = require('path');

const pathStr = path.join('/a', '/bc/d', '../', './e', 'f');
console.log(pathStr);

const pathStr2 = path.join(__dirname, './files/test.txt')
console.log(pathStr2);
```

运行结果：

[![image-20221203110526320](https://github.com/JERRY-Z-J-R/I-love-you-3-thousand/raw/master/%E6%88%91%E7%88%B1%E4%BD%A0%EF%BC%8C%E4%B8%8D%E6%AD%A2%E4%B8%89%E5%8D%83%E9%81%8D/Node/02-fs%E6%96%87%E4%BB%B6%E7%B3%BB%E7%BB%9F%E6%A8%A1%E5%9D%97/mark-img/image-20221203110526320.png)](https://github.com/JERRY-Z-J-R/I-love-you-3-thousand/blob/master/我爱你，不止三千遍/Node/02-fs文件系统模块/mark-img/image-20221203110526320.png)

> <font color='red'>**注意**</font>：今后凡是涉及到路径拼接的操作，都要使用`path.join()`方法进行处理，不要直接使用字符串拼接！

### 6.3 获取路径中的文件名

`path.basename()`的语法格式：

使用`path.basename()`方法，可以获取路径中的最后一部分，经常通过这个方法获取路径中的文件名，语法格式如下：

```js
path.basename(path[, ext])
```

参数解读：

- path：字符串【必选参数】，表示一个路径的字符串
- ext：字符串【可选参数】，表示文件扩展名
- 返回值：字符串`<string>`，表示路径中的最后一部分（通常是用来返回文件名）

代码示例：

```
const path = require('path');

const fpath = '/a/b/c/index.html';

let fullName = path.basename(fpath);
console.log(fullName);

let nameWithoutExt = path.basename(fpath, '.html');
console.log(nameWithoutExt);
```

运行结果：

[![image-20221203113330008](https://github.com/JERRY-Z-J-R/I-love-you-3-thousand/raw/master/%E6%88%91%E7%88%B1%E4%BD%A0%EF%BC%8C%E4%B8%8D%E6%AD%A2%E4%B8%89%E5%8D%83%E9%81%8D/Node/02-fs%E6%96%87%E4%BB%B6%E7%B3%BB%E7%BB%9F%E6%A8%A1%E5%9D%97/mark-img/image-20221203113330008.png)](https://github.com/JERRY-Z-J-R/I-love-you-3-thousand/blob/master/我爱你，不止三千遍/Node/02-fs文件系统模块/mark-img/image-20221203113330008.png)

### 6.4 获取路径中的文件扩展名

`path.extname()`的语法格式：

使用`path.extname()`方法，可以获取路径中的文件扩展名部分，语法格式如下：

```
path.extname(path)
```

参数解读：

- path：字符串【必选参数】，表示一个路径的字符串
- 返回值：字符串，返回得到的扩展名字符串

代码示例：

```
const path = require('path');

const fpath = '/a/b/c/index.html';

const fext = path.extname(fpath);
console.log(fext);
```

运行结果：

[![image-20221203114304427](https://github.com/JERRY-Z-J-R/I-love-you-3-thousand/raw/master/%E6%88%91%E7%88%B1%E4%BD%A0%EF%BC%8C%E4%B8%8D%E6%AD%A2%E4%B8%89%E5%8D%83%E9%81%8D/Node/02-fs%E6%96%87%E4%BB%B6%E7%B3%BB%E7%BB%9F%E6%A8%A1%E5%9D%97/mark-img/image-20221203114304427.png)](https://github.com/JERRY-Z-J-R/I-love-you-3-thousand/blob/master/我爱你，不止三千遍/Node/02-fs文件系统模块/mark-img/image-20221203114304427.png)













