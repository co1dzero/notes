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

```js
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

```js
path.extname(path)
```

参数解读：

- path：字符串【必选参数】，表示一个路径的字符串
- 返回值：字符串，返回得到的扩展名字符串

代码示例：

```js
const path = require('path');

const fpath = '/a/b/c/index.html';

const fext = path.extname(fpath);
console.log(fext);
```

运行结果：

[![image-20221203114304427](https://github.com/JERRY-Z-J-R/I-love-you-3-thousand/raw/master/%E6%88%91%E7%88%B1%E4%BD%A0%EF%BC%8C%E4%B8%8D%E6%AD%A2%E4%B8%89%E5%8D%83%E9%81%8D/Node/02-fs%E6%96%87%E4%BB%B6%E7%B3%BB%E7%BB%9F%E6%A8%A1%E5%9D%97/mark-img/image-20221203114304427.png)](https://github.com/JERRY-Z-J-R/I-love-you-3-thousand/blob/master/我爱你，不止三千遍/Node/02-fs文件系统模块/mark-img/image-20221203114304427.png)



------

# http模块

## 一、什么是http模块

在网络节点中，负责消费资源的计算机，叫作“客服端”，<font color='red'>负责对外提供网络资源的计算机</font>，叫作“服务器”。

<font color='red'>http 模块</font>是 Node.js 官方提供的，用来<font color='red'>创建 Web 服务器</font>的模块。通过 http 模块提供的 <font color='blue'>`http.createServer()`</font> 方法，就能方便的把一台普通的电脑，变成一台 Web 服务器，从而对外提供 Web 资源服务。

如果要希望使用 http 模块创建 Web 服务器，则需要先导入它：

```js
// http 模块是 Node.js 自带的，无需下载，即可引入！
const http = require('http');
```



## 二、进一步了解http模块的作用

服务器和普通电脑的<font color='red'>**区别**</font>在于，服务器上安装了<font color='red'> web 服务器软件</font>，例如：IIS、<font color='red'>Apache</font>、Nginx 等。通过安装这些服务器软件，就能把一台普通的电脑变成一台 web 服务器。

在 Node.js 中，我们<font color='red'>不需要</font>使用 IIS、Apache、Nginx 等这些<font color='red'>第三方 web 服务器软件</font>。因为我们可以<font color='red'>基于 Node.js 提供的 http 模块</font>，通过几行简单的代码，就能轻松的手写一个服务器软件，从而对外提供 web 服务。



## 三、服务器相关的概念

### 3.1 IP地址

<font color='red'>IP 地址</font>就是互联网上<font color='red'>每台计算机的唯一地址</font>，因此 IP 地址具有唯一性，只有在知道对方的 IP 地址的前提下，才能与对应的电脑之间进行数据通信。

IP 地址的格式：通常使用<font color='red'> “点分十进制” 表示成（a.b.c.d）的形式</font>，其中，a,b,c,d 都是 0~255 之间的十进制整数。例如：用点分十进制表示的 IP 地址（192.168.54.2）

注意：

> 1. 互联网中每台 Web 服务器，都有自己的 IP 地址，例如：大家可以再 Windows 终端中运行 <font color='red'>ping www.baidu.com </font> 命令，即可查看到百度服务器的 IP 地址。
>
>    ![](C:\Users\shizeyu\Desktop\notes\Ajax-vue\Snipaste_2023-02-07_16-05-30.png)
>
> 2. 在开发期间，自己的电脑既是一台服务器，也是一个客服端，其中：<font color='red'>127.0.0.1 </font>这个 IP 地址为本机地址，也就是本机作为服务器时的地址。仅限于本机。

### 3.2 域名和域名服务器

尽管 IP 地址能够唯一标记网络上的计算机，但 IP 地址是一长串数字，不直观，而且<font color='red'>不便于记忆</font>，于是人们又发明了另外一套字符型的地址方案，即所谓的<font color='red'>域名（Domain Name）地址</font>。

<font color='red'>IP 地址</font>和<font color='red'>域名</font>是<font color='red'>一一对应</font>的关系，这份对应关系存在一种叫作 <font color='red'>“域名服务器”</font>（DNS，Domain name server）的电脑中，使用者只需通过好记的域名访问对应的服务器即可，对应的转换工作由域名服务器实现。因此，<font color='red'>域名服务器就是提供 IP 地址和域名之间的转换服务的服务器</font>。

> 特殊的：`127.0.0.1` 对应的域名是 `localhost`，它们都代表：本机。

### 3.3 端口号

如果把计算机比喻成一栋大楼，那么计算机中的端口号就好像是每户的门牌号一样。

同样的道理，在一台电脑中，可以运行成白上千个 web 服务，每个 web 服务都对应一个唯一的端口号。客户端发送过来的网络请求，通过端口号，可以被准确地交给<font color='red'>对应的 web 服务进行处理</font>。

注意：

- 端口号在 ip 或 域名 后写，用 `:` 进行分割，例如：`127.0.0.1:8080`、`localhost:8080`
- 每个端口号不能同时被多个 web 服务占用
- 其中 URL 中的<font color='red'> 80 端口可以被省略</font>，8081不可省略，即：`x.x.x.x:80` 等同于 `x.x.x.x`



## <u>四、创建最基本的web服务器</u>

### 4.1 创建web服务器的基本步骤

1. 导入 http 模块
2. 创建 web 服务器实例
3. 为服务器实例绑定<font color='red'>` request `事件</font>，<font color='blue'>监听客户端的请求</font>
4. 启动服务器



步骤1 - 导入 http 模块

```js
const http = require('http');
```

步骤2 - 创建 web 服务器实例

```js
// 调用 http.createServer() 方法，即可快速创建一个 web 服务器实例
const server = http.createServer();
```

步骤3 - 为服务器实例绑定 request 事件

```js
// 为服务器实例绑定 request 事件，即可 监听 客户端发送过来的网络请求

// 使用服务器实例的 .on() 方法绑定事件，为服务器绑定一个 request 事件
// 服务器实例.on('事件名',function(req, res))
server.on('request', (req, res) => {
    // 只要客户端来请求服务器，就会触发 request 事件，从而调用这个事件处理回调函数
    console.log('Someone visit our web server.')
});
```

步骤4 - 启动服务器

```js
// 调用服务器实例的 .listen() 方法，即可启动当前的 web 服务器实例

// 调用 server.listen(端口号, 回调函数) 方法，即可启动 web 服务器
server.listen(80, () => {
    console.log('http server running at http://127.0.0.1');
});
```



### 4.2 创建web服务器案例

```js
const http = require('http');

const server = http.createServer();

server.on('request', (req, res) => {
    console.log('Someone visit our web server.')
});

server.listen(8080, () => {
    console.log('http server running at http://127.0.0.1:8080');
});
```

运行结果：

![](C:\Users\shizeyu\Desktop\notes\Ajax-vue\Snipaste_2023-02-07_16-51-58.png)

可见，一个最基本的 web 服务器就成功运行了！我们点击这个 URL 用浏览器（客服端）进行访问：

![](C:\Users\shizeyu\Desktop\notes\Ajax-vue\Snipaste_2023-02-07_16-51-58.png)

web 服务器成功接收到了客服端（浏览器）的请求，并在控制台打印 `Someone visit our web server.`，而浏览器窗口之所以一直处于加载中，那时因为目前 web 服务器并没有响应任何数据给客服端（浏览器），所以浏览器一直在等待响应。



### 4.3 req 请求对象

req（request【请求】）

只要服务器接收到了客户端的请求，就会调用通过<font color='red'> `server.on()` </font>为服务器绑定的<font color='red'> `request` 事件处理函数</font>。

如果想要在事件处理函数中，<font color='red'>访问与客户端相关的<u>**数据**</u>或<u>**属性**</u></font>，可以使用如下方式：

```js
server.on('request', (req) => {
    // req 是请求对象，它包含了与客户端相关的数据和属性，例如：
    // req.url 是客户端请求的 URL 地址
    // req.method 是客户端的 method 请求类型
    const str = `Your request url is ${req.url}, and request method is ${req.method}`;
    console.log(str);
});
```

现在来看实际演示：

```js
const http = require('http');

const server = http.createServer();

server.on('request', (req) => {
    // req 是请求对象，它包含了与客户端相关的数据和属性，例如：
    // req.url 是客户端请求的 URL 地址
    // req.method 是客户端的 method 请求类型
    const str = `Your request url is ${req.url}, and request method is ${req.method}`;
    console.log(str);
});

server.listen(8080, () => {
    console.log('http server running at http://127.0.0.1');
});
```

运行代码，我们在浏览器地址栏中输入 127.0.0.1：

![](C:\Users\shizeyu\Desktop\notes\Ajax-vue\Snipaste_2023-02-07_17-01-12.png)

可见，此时客户端请求的 URL 是根路径（/），请求方式是 GET（浏览器地址栏请求都是 GET 方式）。

我们在浏览器地址栏中输入 127.0.0.1/index.html：

![](C:\Users\shizeyu\Desktop\notes\Ajax-vue\Snipaste_2023-02-15_11-16-10.png)

可见，此时客户端请求的 URL 是（/index.html），请求方式是 `GET`。

下面，我们利用 Apifox、Postman 等这些 API 请求工具来测试 POST 请求方式：

> Apifox、Postman 这些都是目前最火热的 API 请求工具，其中 Postman 是全世界最出名的 API 请求工具，Apifox 是近几年国产的一款功能丰富的 API 请求工具，这里推荐直接使用 Apifox，因为支持中文，功能丰富和强大，界面友好，且免费！

![](C:\Users\shizeyu\Desktop\notes\Ajax-vue\Snipaste_2023-02-16_16-36-07.png)

可见，此时客户端请求的 URL 是（/about.html），请求方式是 POST。

### 4.4 res 响应对象

在服务器的 request 事件处理函数中，如果想<font color='gree'>响应与服务器相关</font>的<font color='red'>数据</font>或<font color='red'>属性</font>，可以使用如下的方式：

```js
server.on('request', (req, res) => {
    // res 是响应对象，它包含了与服务器相关的数据和属性，例如：
    // 要发送（响应）到客服端的字符串
    const str = `Your request url is ${req.url}, and request method is ${req.method}`;
    // res.end() 方法的作用：
    // 向客户端发送指定的内容，并结束这次请求的处理过程
    // 调用 res.end() 方法，向客户端响应内容
    res.end(str);
});
```

现在来看实际演示：

```js
const http = require('http');

const server = http.createServer();

server.on('request', (req, res) => {
    const str = `Your request url is ${req.url}, and request method is ${req.method}`;
    res.end(str);
});

server.listen(80, () => {
    console.log('http server running at http://127.0.0.1');
});
```

运行代码，我们在浏览器地址栏中输入 127.0.0.1：

[![image-20221203193037820](https://github.com/JERRY-Z-J-R/I-love-you-3-thousand/raw/master/%E6%88%91%E7%88%B1%E4%BD%A0%EF%BC%8C%E4%B8%8D%E6%AD%A2%E4%B8%89%E5%8D%83%E9%81%8D/Node/03-http%E6%A8%A1%E5%9D%97/mark-img/image-20221203193037820.png)](https://github.com/JERRY-Z-J-R/I-love-you-3-thousand/blob/master/我爱你，不止三千遍/Node/03-http模块/mark-img/image-20221203193037820.png)

利用 Apifox 进行 POST 测试：

[![image-20221203193303334](https://github.com/JERRY-Z-J-R/I-love-you-3-thousand/raw/master/%E6%88%91%E7%88%B1%E4%BD%A0%EF%BC%8C%E4%B8%8D%E6%AD%A2%E4%B8%89%E5%8D%83%E9%81%8D/Node/03-http%E6%A8%A1%E5%9D%97/mark-img/image-20221203193303334.png)](https://github.com/JERRY-Z-J-R/I-love-you-3-thousand/blob/master/我爱你，不止三千遍/Node/03-http模块/mark-img/image-20221203193303334.png)

### 4.5 解决中文乱码问题

当调用 res.end() 方法，向客户端发送<font color='gree'>中文内容</font>的时候，会出现乱码问题，此时，需要<font color='gree'>手动设置内容的编码格式</font>：

乱码情况：

```js
server.on('request', (req, res) => {
    // 发送（响应）包含中文的内容
    const str = `您请求的 url 地址是 ${req.url}, 请求的 method 类型是 ${req.method}`;
    res.end(str);
});
```

[![image-20221203202107408](https://github.com/JERRY-Z-J-R/I-love-you-3-thousand/raw/master/%E6%88%91%E7%88%B1%E4%BD%A0%EF%BC%8C%E4%B8%8D%E6%AD%A2%E4%B8%89%E5%8D%83%E9%81%8D/Node/03-http%E6%A8%A1%E5%9D%97/mark-img/image-20221203202107408.png)](https://github.com/JERRY-Z-J-R/I-love-you-3-thousand/blob/master/我爱你，不止三千遍/Node/03-http模块/mark-img/image-20221203202107408.png)

解决方案：

```js
server.on('request', (req, res) => {
    // 发送（响应）包含中文的内容
    const str = `您请求的 url 地址是 ${req.url}, 请求的 method 类型是 ${req.method}`;
    // 为了防止中文显示乱码的问题，需要利用 .setHeader() 方法设置响应头 Content-Type 的值为 text/html; charset=utf-8
    res.setHeader('Content-Type', 'text/html; charset=utf-8');
    res.end(str);
});
```

[![image-20221203202220335](https://github.com/JERRY-Z-J-R/I-love-you-3-thousand/raw/master/%E6%88%91%E7%88%B1%E4%BD%A0%EF%BC%8C%E4%B8%8D%E6%AD%A2%E4%B8%89%E5%8D%83%E9%81%8D/Node/03-http%E6%A8%A1%E5%9D%97/mark-img/image-20221203202220335.png)](https://github.com/JERRY-Z-J-R/I-love-you-3-thousand/blob/master/我爱你，不止三千遍/Node/03-http模块/mark-img/image-20221203202220335.png)

### 4.6 根据不同的url响应不同的内容

核心实现步骤：

1. 获取请求的 url 地址
2. 设置默认的响应内容为 404 Not found
3. 判读用户请求的是否为 / 或 /index.html 首页
4. 判断用户请求的是否为 /about.html 关于页面
5. 设置 Content-Type 响应头，防止中文乱码
6. 使用 res.end() 把内容响应给客户端

实现代码：

```js
const http = require('http');

const server = http.createServer();

server.on('request', (req, res) => {
    // 获取请求的 url 地址
    const url = req.url;
    // 设置默认的内容为 404 Not found
    let content = '<h1>404 Not found!</h1>';
    if (url === '/' || url === '/index.html') {
        // 客户端请求的是首页
        content = '<h1>首页</h1>';
    } else if (url === '/about.html') {
        // 客户端请求的是关于页面
        content = '<h1>关于页面</h1>';
    }
    // 设置 Content-Type 响应头，防止中文乱码
    res.setHeader('Content-Type', 'text/html; charset=utf-8');
    // 使用 res.end() 把内容响应给客户端
    res.end(content);
});

server.listen(80, () => {
    console.log('http server running at http://127.0.0.1');
});
```

测试：

[![image-20221203220857638](https://github.com/JERRY-Z-J-R/I-love-you-3-thousand/raw/master/%E6%88%91%E7%88%B1%E4%BD%A0%EF%BC%8C%E4%B8%8D%E6%AD%A2%E4%B8%89%E5%8D%83%E9%81%8D/Node/03-http%E6%A8%A1%E5%9D%97/mark-img/image-20221203220857638.png)](https://github.com/JERRY-Z-J-R/I-love-you-3-thousand/blob/master/我爱你，不止三千遍/Node/03-http模块/mark-img/image-20221203220857638.png)

## 五、web服务器案例

![](C:\Users\shizeyu\Desktop\notes\Ajax-vue\Snipaste_2023-02-17_10-37-38.png)

在 node/web 路径下有三个网页文件，我们的目标就是实现一个 Node.js Web 静态服务器来运行这个网页。

**核心思路**

把文件的<font color='gree'>实际存放路径</font>，<font color='red'>作为</font>每个资源的<font color='gree'>请求 url 地址</font>。

下图展示了这种思路的一个基本原理及流程。

![](C:\Users\shizeyu\Desktop\notes\Ajax-vue\Snipaste_2023-02-17_10-35-31.png)

**实现代码**

```js
// 导入 http 模块
const http = require('http');
// 导入 fs 模块
const fs = require('fs');
// 导入 path 模块
const path = require('path');

// 创建 web 服务器
const server = http.createServer();

// 监听 web 服务器的 request 事件
server.on('request', (req, res) => {
    // 获取到客户端请求的 url 地址
    const url = req.url;
    // 把请求的 url 地址映射为具体的文件存放路径
    const fpath = path.join(__dirname, url);

    // 根据映射过来的文件路径读取文件的内容
    fs.readFile(fpath, 'utf8', (err, dataStr) => {
        // 读取失败，向客户端响应固定的错误信息
        if (err) {
            return res.end('404 Not Found.');
        }
        // 读取成功，将读取到的内容响应给客服端
        res.end(dataStr);
    });
});

// 启动服务器
server.listen(80, () => {
    console.log('server running at http://127.0.0.1');
});
```

测试：

[![image-20221203231850626](https://github.com/JERRY-Z-J-R/I-love-you-3-thousand/raw/master/%E6%88%91%E7%88%B1%E4%BD%A0%EF%BC%8C%E4%B8%8D%E6%AD%A2%E4%B8%89%E5%8D%83%E9%81%8D/Node/03-http%E6%A8%A1%E5%9D%97/mark-img/image-20221203231850626.png)](https://github.com/JERRY-Z-J-R/I-love-you-3-thousand/blob/master/我爱你，不止三千遍/Node/03-http模块/mark-img/image-20221203231850626.png)

**思考：**我们刚才只处理了对 html 文件的访问，没有处理对 css 及 js 文件的访问，那 css 及 js 是如何响应过去的呢？

为了弄清楚这个问题，我们修改一下代码，打印一些信息：

```js
// 获取到客户端请求的 url 地址
const url = req.url;
console.log('--------------------------------------------');
console.log(url);
// 把请求的 url 地址映射为具体的文件存放路径
const fpath = path.join(__dirname, url);
console.log(fpath);
```

再次运行，访问 127.0.0.1/web/index.html，查看控制台：

[![image-20221204001416768](https://github.com/JERRY-Z-J-R/I-love-you-3-thousand/raw/master/%E6%88%91%E7%88%B1%E4%BD%A0%EF%BC%8C%E4%B8%8D%E6%AD%A2%E4%B8%89%E5%8D%83%E9%81%8D/Node/03-http%E6%A8%A1%E5%9D%97/mark-img/image-20221204001416768.png)](https://github.com/JERRY-Z-J-R/I-love-you-3-thousand/blob/master/我爱你，不止三千遍/Node/03-http模块/mark-img/image-20221204001416768.png)

![](C:\Users\shizeyu\Desktop\notes\Ajax-vue\Snipaste_2023-02-17_14-51-15.png)

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>web服务器案例</title>
    <link rel="stylesheet" href="./index.css">
</head>
<body>
    <div class="wow" id="wow">Wow!</div>
    <script src="./index.js"></script>
</body>
</html>
```

解释：当访问 http://127.0.0.1/web/index.html 时，浏览器收到了服务器的响应，获得了 index.html 页面，浏览器在解析 index.html 页面时发现了该页面需要另外的 "./index.css" 以及 "./index.js"，所以浏览器会继续请求服务器来获取 css 及 js 文件，而请求的路径则是在原有路径 http://127.0.0.1/web 的基础上加上 "./index.css" 以及 "./index.js"，所以最终浏览器就以 http://127.0.0.1/web/index.css 及 http://127.0.0.1/web/index.js 的形式又请求了两次服务器（还有一次是请求浏览器窗口图标，暂时不用管）。

> ` favicon.ico `请求浏览器窗口图标

------

通常，考虑到用户访问的方便性以及系统安全性，我们以 127.0.0.1 及 127.0.0.1/index.html 代替 127.0.0.1/code/index.html，所以我们对代码进行资源请求路径的<font color='gree'>优化</font>：

```js
// 导入 http 模块
const http = require('http');
// 导入 fs 模块
const fs = require('fs');
// 导入 path 模块
const path = require('path');

// 创建 web 服务器
const server = http.createServer();

// 监听 web 服务器的 request 事件
server.on('request', (req, res) => {
    // 获取到客户端请求的 url 地址
    const url = req.url;
    // 把请求的 url 地址映射为具体的文件存放路径
    
    // 优化资源的请求路径
    let fpath = '';
    if (url === '/') {
        // 当路径为空为首页，自动拼接首页路径
        fpath = path.join(__dirname, './code/index.html');
    } else {
        // 当客户端请求路径，自动拼接/code路径
        fpath = path.join(__dirname, '/code', url);
    }

    // 根据映射过来的文件路径读取文件的内容
    fs.readFile(fpath, 'utf8', (err, dataStr) => {
        // 读取失败，向客户端响应固定的错误信息
        if (err) {
            return res.end('404 Not Found.');
        }
        // 读取成功，将读取到的内容响应给客服端
        res.end(dataStr);
    });
});

// 启动服务器
server.listen(80, () => {
    console.log('server running at http://127.0.0.1');
});
```

[![image-20221204002358226](https://github.com/JERRY-Z-J-R/I-love-you-3-thousand/raw/master/%E6%88%91%E7%88%B1%E4%BD%A0%EF%BC%8C%E4%B8%8D%E6%AD%A2%E4%B8%89%E5%8D%83%E9%81%8D/Node/03-http%E6%A8%A1%E5%9D%97/mark-img/image-20221204002358226.png)](https://github.com/JERRY-Z-J-R/I-love-you-3-thousand/blob/master/我爱你，不止三千遍/Node/03-http模块/mark-img/image-20221204002358226.png)



------

# 【模块化】

> 原创内容，转载请注明出处！

# 一、模块化的基本概念

## 1.1 什么是模块化

<font color='red'>模块化</font>是指解决一个<font color='gree'>复杂问题</font>时，自顶向下逐层<font color='gree'>把系统划分成若干模块的过程</font>。对于整个系统来说，<font color='gree'>模块是可组合、分解和更换的单元</font>。

## 1.2 编程领域中的模块化

编程领域中的模块化，就是<font color='red'>遵守固定的规则</font>，把一个<font color='red'>大文件</font>拆成<font color='gree'>独立并互相依赖</font>的<font color='red'>多个小模块</font>。

把代码进行模块化拆分的好处：

- 提高了代码的<font color='gree'>复用性</font>
- 提高了代码的<font color='gree'>可维护性</font>
- 可以实现<font color='gree'>按需加载</font>

## 1.3 模块化规范

<font color='gree'>模块化规范</font>就是对代码进行模块化的拆分与组合时，需要遵守的那些规则。

例如：

- 使用什么样的语法格式来<font color='gree'>引用模块</font>
- 在模块中使用什么样的语法格式<font color='gree'>向外暴露成员</font>

<font color='gree'>模块化规范的好处</font>：大家都遵守同样的模块化规范写代码，降低了沟通的成本，极大方便了各个模块之间的相互调用，利己利人。

# 二、Node.js中的模块化

> Node.js 默认采用 CommonJS 模块化，当然新版的 Node.js 也提供了 ES6 的模块化！

## 2.1 Node.js中模块的分类

Node.js 中根据模块来源不同，将模块分为了 3 大类，分别是：

- <font color='red'>内置模块</font>（内置模块是由 Node.js 官方提供的，例如 fs、path、http 等）
- <font color='red'>自定义模块</font>（用户创建的每个独立的 .js 文件，都可以看作是一个自定义模块）
- <font color='red'>第三方模块</font>（<font color='gree'>由第三方开发出来的模块</font>，并非官方提供的内置模块，也不是用户创建的自定义模块，<font color='gree'>使用前需要下载</font>）

## 2.2 <font color='gree'>加载</font>模块

使用强大的<font color='red'> `require()` </font>方法，可以加载需要的<font color='gree'>内置模块、用户自定义模块、第三方模块</font>进行使用。

例如：

```js
// 加载内置的 fs 模块
const fs = require('fs');

// 加载用户自定义模块（需要带上路径，.js后缀可带可不带）
// const custom = require('./custom');
const custom = require('./custom.js');

// 加载第三方模块（关于第三方模块的下载和使用，会在后面进行专门的讲解）
const moment = require('moment');
```

<font color='red'>注意</font>：使用 `require()` 方法加载模块的一瞬间，会立即执行被加载模块中的代码！

## 2.3 Node.js中的模块作用域

**什么是<font color='red'>模块作用域</font>？**

和<font color='red'>函数作用域</font>类似，在自定义模块中定义的<font color='gree'>变量、方法</font>等成员，<font color='gree'>只能在所在的模块内被访问</font>，这种<font color='gree'>模块级别的访问限制</font>，叫作<font color='red'>模块作用域</font>。

> **模块作用域的好处：防止了全局变量污染的问题！**

## 2.4 向外共享模块作用域中的成员

### **【module 对象】**

在每个自定义模块中都有一个 module 对象，它里面<font color='gree'>存储了和当前模块有关的信息</font>，打印如下：

![](C:\Users\shizeyu\Desktop\notes\Ajax-vue\Snipaste_2023-02-20_16-52-04.png)

其中 module 对象中的 exports 默认是一个空对象`{}`。

>exports 对象用于向外共享信息

### **【module.exports 对象】**

外界用 `require()` 方法导入自定义模块时，得到的就是` module.exports `所指向的对象，默认为 `{}`。

![](C:\Users\shizeyu\Desktop\notes\Ajax-vue\Snipaste_2023-02-20_16-59-33.png)

在自定义模块中，我们可以使用 `module.exports` 对象，将模块内的成员共享出去，供外界使用。

![](C:\Users\shizeyu\Desktop\notes\Ajax-vue\Snipaste_2023-02-21_16-11-09.png)

共享成员时的<font color='red'>注意点</font>：

使用 `require()` 方法导入模块时，导入的结果，<font color='gree'>永远以 module.exports 指向的对象为准！</font>

![](C:\Users\shizeyu\Desktop\notes\Ajax-vue\Snipaste_2023-02-21_16-20-12.png)

### **【exports 对象】**

由于 module.exports 单词写起来比较复杂，为了简化向外共享成员的代码，Node 提供了<font color='gree'> exports 对象</font>。

<font color='gree'>默认情况下，exports 和 module.exports 指向同一个对象</font>。最终共享的结果，还是<font color='red'>以 module.exports 指向的对象为准</font>。

![](C:\Users\shizeyu\Desktop\notes\Ajax-vue\Snipaste_2023-02-21_16-28-14.png)

![](C:\Users\shizeyu\Desktop\notes\Ajax-vue\Snipaste_2023-02-21_16-33-22.png)

这个发现exports指向的对象并非体现在了module.exports上为什么呢？详细注意事项

![](C:\Users\shizeyu\Desktop\notes\Ajax-vue\Snipaste_2023-02-21_16-29-12.png)



### **【exports 和 module.exports 的使用注意】**

时刻谨记，`require()` 导入模块时，得到的永远是<font color='red'> module.exports </font>指向的对象：

![](C:\Users\shizeyu\Desktop\notes\Ajax-vue\Snipaste_2023-02-21_16-59-12.png)

情况一：

![](C:\Users\shizeyu\Desktop\notes\Ajax-vue\Snipaste_2023-02-21_16-47-45.png)

![](C:\Users\shizeyu\Desktop\notes\Ajax-vue\Snipaste_2023-02-21_16-50-44.png)

情况二：

![](C:\Users\shizeyu\Desktop\notes\Ajax-vue\Snipaste_2023-02-21_16-52-32.png)

![](C:\Users\shizeyu\Desktop\notes\Ajax-vue\Snipaste_2023-02-21_16-53-56.png)

情况三：

![](C:\Users\shizeyu\Desktop\notes\Ajax-vue\Snipaste_2023-02-21_16-56-04.png)

![](C:\Users\shizeyu\Desktop\notes\Ajax-vue\Snipaste_2023-02-21_16-56-27.png)

情况四：

![](C:\Users\shizeyu\Desktop\notes\Ajax-vue\Snipaste_2023-02-21_16-59-45.png)

![](C:\Users\shizeyu\Desktop\notes\Ajax-vue\Snipaste_2023-02-21_17-00-43.png)

> <font color='red'>注意</font>：为了防止混乱，建议不要在同一个模块中同时使用 exports 和 module.exports！

## 2.5 Node.js中的模块化规范

Node.js 遵循了 CommonJS 模块化规范，CommonJS 规定了模块的特性和各模块之间如何相互依赖。

CommonJS 规定：

1. 每个模块内部，module 变量代表当前模块
2. module 变量是一个对象，它的 exports 属性（即 module.exports）是对外的接口
3. 加载某个模块，其实是加载该模块的 module.exports 属性，require() 方法用于加载模块









