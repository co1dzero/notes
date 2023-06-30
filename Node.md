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

```js
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

Node.js 遵循了 CommonJS 模块化规范，CommonJS 规定了<font color='gree'>模块的特性</font>和<font color='gree'>各模块之间如何相互依赖</font>。

CommonJS 规定：

1. 每个模块内部，<font color='gree'>module 变量</font>代表当前模块
2. module 变量是一个对象，它的 exports 属性（即 <font color='red'>module.exports</font>）是<font color='gree'>对外的接口</font>
3. 加载某个模块，其实是加载该模块的 module.exports 属性，<font color='gree'>require() 方法用于加载模块</font>

------

# 【npm与包】

# 一、包

## 1.1 什么是包？

Node.js 中的<font color='gree'>第三方模块</font>又叫作<font color='gree'>包</font>。

> 就像<font color='pink'>电脑</font>和<font color='pink'>计算机</font>指的是相同的东西，<font color='pink'>第三方模块</font>和<font color='pink'>包</font>指的是同一个概念，只不过叫法不同。

## 1.2 包的来源

不同于 Node.js 中的内置模块与自定义模块，<font color='gree'>包是由第三方个人或团队开发出来的</font>，免费供所有人使用。

<font color='red'>注意</font>：Node.js 中的包都是免费开源的，不需要付费便可免费下载使用。

## 1.3 为什么需要包？

由于 Node.js 的内置模块仅仅提供了一些底层基础性的 API，导致在基于内置模块进行项目的开发时，效率很低。

<font color='gree'>包是基于内置模块封装出来的</font>，提供了更高级、更方便的 API，<font color='gree'>极大的提高了开发效率</font>。

<font color='red'>包</font>和<font color='gree'>内置模块</font>之间的关系，类似于<font color='red'> jQuery </font>和<font color='gree'> 浏览器内置 API </font>之间的关系。

## 1.4 从哪里下载包？

国外有一家 IT 公司，叫作<font color='red'>【Npm, Inc.】</font>这家公司旗下有一个非常著名的网站：https://www.npmjs.com/，它是<font color='gree'>全球最大的包共享平台</font>，任何人可以从这个网站上搜索到任何你想要的包，只要你有足够的耐心！

到目前为止，全球约<font color='orange'> 1100 多万</font>的开发人员，通过这个包共享平台，开发并共享了超过<font color='orange'> 120 多万</font> 个包供我们使用。

<font color='red'>npm, Inc. 公司</font>提供了一个地址为 https://registry.npmjs.org/ 的服务器，来对外共享所有的包，我们可以从这个服务器上下载自己所需要的包。

<font color='red'>注意</font>：

- 从 https://www.npmjs.com/ 网站上搜索自己所需要的包
- 从 https://registry.npmjs.org/ 服务器上下载自己所需要的包

## 1.5 如何下载包？

<font color='red'>npm, Inc. 公司</font>提供了一个包管理工具，我们可以使用这个包管理工具，从 https://registry.npmjs.org/ 服务器把需要的包下载到本地使用。

这个包管理工具的名字叫作<font color='gree'> Node Package Manager</font>（简称<font color='red'> npm 包管理工具</font>），这个包管理工具随着 Node.js 的安装包一起被安装到了用户的电脑上。

大家可以在终端中执行<font color='red'> npm -v </font>命令，来查看自己电脑上所安装的 npm 包管理工具的版本号。

# 二、npm初体验

## 案例：格式化时间

### 一.格式化时间的传统做法

①创建格式化时间的自定义模块

②定义格式化时间的方法

③创建补零函数

④从自定义模块中导出格式化时间的函数

<font color='gree'>⑤导入格式化时间的自定义模块</font>

<font color='gree'>⑥调入格式化时间的函数</font>

![](C:\Users\shizeyu\Desktop\notes\Ajax-vue\Snipaste_2023-02-28_16-34-45.png)



### 二.格式化时间的高级做法

1. <font color='gree'>使用 npm 包管理工具，在项目中安装格式化时间的包 moment</font>
2. 使用 require() 导入格式化时间的包
3. 参考 moment 官方 API 文档对时间进行格式化

**【在项目中安装包的命令】**

如果想在项目中安装指定名称的包，需要运行如下的命令：

```js
npm install 包的完整名称
```

上述的装包命令，可以简写成如下格式：

```
npm i 包的完整名称
```

![](C:\Users\shizeyu\Desktop\notes\Ajax-vue\Snipaste_2023-02-28_16-44-43.png)



**【利用 moment 对时间进行格式化】**

首先我们打开 https://www.npmjs.com/，并在搜索框中搜索 moment。

![](C:\Users\shizeyu\Desktop\notes\Ajax-vue\Snipaste_2023-02-28_16-45-56.png)

在结果列表中，找到 moment 点击进入。

![](C:\Users\shizeyu\Desktop\notes\Ajax-vue\Snipaste_2023-02-28_16-46-33.png)

moment 主页的相关说明（其它包也大同小异）：

![](C:\Users\shizeyu\Desktop\notes\Ajax-vue\Snipaste_2023-02-28_16-54-04.png)

点击文档，即可查看使用说明：

![](C:\Users\shizeyu\Desktop\notes\Ajax-vue\Snipaste_2023-02-28_16-56-59.png)

> 目前绝大多数的开源项目都是英文文档，所以良好的英文听说读写能力是一个出色程序员的标配！

根据文档的指示，我们开始编写代码：

```js
// 导入 moment 包
const moment = require('moment');

// 调用 moment() 方法，得到当前的时间
// 针对当前的时间，调用 format() 方法，按照指定的格式进行时间的格式化
const dt = moment().format('YYYY-MM-DD HH:mm:ss');

console.log(dt);
```

![](C:\Users\shizeyu\Desktop\notes\Ajax-vue\Snipaste_2023-02-28_16-58-41.png)



**【初次装包后多了哪些文件】**

初次装包完成后，在项目文件夹下多一个叫作<font color='red'> node_modules </font>的文件夹和<font color='red'> package.json </font>及<font color='red'> package-lock.json </font>文件。

其中：

- <font color='red'>node_modules </font>文件夹用来<font color='gree'>存放所有已安装到项目中的包</font>。require() 导入第三方包时，就是从这个目录中查找并加载包
- package.json 文件用来记录项目的基本信息以及 node_modules 目录下的每一个包的大版本号
- <font color='red'>package-lock.json </font>文件用来<font color='gree'>记录 node_modules 目录下的每一个包的详细下载信息</font>，例如包的名字、具体版本号、下载地址等

> 注意：程序员不要手动修改 node_modules 及 package.json package-lock.json 文件中的任何内容，npm 包管理工具会自动维护它们！

[![image-20221208195853018](https://github.com/JERRY-Z-J-R/I-love-you-3-thousand/raw/master/%E6%88%91%E7%88%B1%E4%BD%A0%EF%BC%8C%E4%B8%8D%E6%AD%A2%E4%B8%89%E5%8D%83%E9%81%8D/Node/05-npm%E4%B8%8E%E5%8C%85/mark-img/image-20221208195853018.png)](https://github.com/JERRY-Z-J-R/I-love-you-3-thousand/blob/master/我爱你，不止三千遍/Node/05-npm与包/mark-img/image-20221208195853018.png)



**【安装指定版本的包】**

默认情况下，使用 npm install 命令安装包的时候，<font color='gree'>会自动安装最新版本的包</font>。如果需要安装指定版本的包，可以在包名之后，通过<font color='red'> @ 符号</font>指定具体的版本，例如：`npm i moment@2.29.4`。



**【包的语义化版本规范】**

包的版本号是以 “点分十进制” 形式进行定义的，总共有三位数字，例如：<font color='red'>2.24.0</font>

其中，每一位数字所代表的含义如下：

- 第一位数字：<font color='red'>大版本号</font>
- 第二位数字：<font color='gree'>功能版本号</font>
- 第三位数字：Bug 修复版本号

> <font color='red'>版本号提升的规则</font>：只要前面的版本号增长了，则后面的版本号<font color='red'>归零</font>。

# 三、包管理配置文件

npm 规定，在<font color='red'>项目根目录</font>中，<font color='red'>**必须**</font>提供一个叫作<font color='red'> package.json </font>的包管理配置文件，用来记录与项目有关的一些配置信息。例如：

- 项目的名称、版本号、描述等
- 项目中都用到了哪些包
- 哪些包只在<font color='red'>开发期间</font>会用到
- 哪些包在<font color='red'>开发</font>和<font color='red'>部署</font>时都需要用到



## 3.1 多人协作的问题

[![image-20221208201810025](https://github.com/JERRY-Z-J-R/I-love-you-3-thousand/raw/master/%E6%88%91%E7%88%B1%E4%BD%A0%EF%BC%8C%E4%B8%8D%E6%AD%A2%E4%B8%89%E5%8D%83%E9%81%8D/Node/05-npm%E4%B8%8E%E5%8C%85/mark-img/image-20221208201810025.png)](https://github.com/JERRY-Z-J-R/I-love-you-3-thousand/blob/master/我爱你，不止三千遍/Node/05-npm与包/mark-img/image-20221208201810025.png)

从我们之前创建的时间格式化项目文件夹就可以发现，真正的业务代码（test.js）只有 1 KB 的大小，而 node_modules 文件夹却有 4 MB 大小！这还只是一个非常小型的项目，对于中大型项目来说，<font color='gree'>一般业务代码只占整个项目大小的 1%！另外的 99% 大部分都是 node_modules 中的依赖包的大小！</font>此时就会带来一个严重的问题：假如项目 1G 大小，而实际业务代码只有 10 MB，此时如果我们要将项目上传到云端或者发送给其他人，那么就需要发送 1G 的数据，这是非常耗费资源且耗时的！在实际团队合作的开发中，往往有一个统一的云端代码仓库实时同步各个程序员本地的代码，如果都不做任何处理直接上传和发送项目原始数据的话，根本不现实！

- 问题：<font color='gree'>第三方包体积过大</font>，不方便共享项目源代码
- 解决思路：<font color='gree'>共享时剔除掉 node_modules 文件夹</font>



## 3.2 如何记录项目中安装了哪些包

在<font color='gree'>项目根目录</font>中，创建一个叫作<font color='red'> package.json </font>的配置文件，即可用来记录项目中安装了哪些包，从而方便剔除 node_modules 目录之后，在团队成员之间共享项目的源代码。

> <font color='red'>注意</font>：今后如果使用 GitHub、Gitee 等来共享项目，那么一定要把 node_modules 文件夹添加到 Git 忽略文件 .gitignore 中。

## 3.3 快速创建package.json

npm 包管理工具提供了一个<font color='red'>快捷命令</font>，可以在<font color='gree'>执行命令时所处的目录中</font>，快速创建 package.json 这个包管理配置文件：

```
npm init
```

我们也可以加上 `-yes` 或 `-y` 参数，表示创建项目时跳过确认。

```
npm init -yes 
或
npm init -y
```

> 注意：执行这个命令时项目应是空的！

> Node.js 在我们写了代码，用 npm 安装依赖包时，除了会创建 node_modules 文件夹及 package-lock.json 文件之外，还会同时创建 package.json 文件（前提是项目之前没有执行过 npm init -y ）。

注意：

- 上述命令<font color='gree'>只能在英文的目录下成功执行</font>！所以，项目文件夹的名称一定要使用英文命名，<font color='gree'>不要使用中文，也不能出现空格</font>！
- 往后，当我们用 npm install XXX 或 npm i XXX 命令安装依赖包时，npm 包管理工具会自动把<font color='gree'>包的名称</font>和<font color='gree'>版本号</font>，记录到 package.json 中！

![](C:\Users\shizeyu\Desktop\notes\Ajax-vue\Snipaste_2023-03-01_10-35-28.png)

可以发现，自动生成的 package.json 文件中自动记录了我们的项目名称（可以修改，默认使用文件夹名称），项目版本号，项目许可类型（默认 ISC）等信息。

> 注意：当我们下载了包之后，package.json 中只是记录了该包的名称及大版本号！当 node_modules 文件夹不存在或是破损后，我们需要通过 package.json 文件的记录重新还原依赖包时，npm 会下载该大版本下的最新版的包，所以就不能 100% 确保我们的包是同一个版本的！虽然大版本内的更新一般都是 bug 更新，通常不会涉及 API 的更新，但是还是非常容易出现莫名其妙的版本问题，所以除了 package.json 之外还需要 package-lock.json 来辅助，该文件就是为了锁定依赖包的具体版本号的，它里面记录的包的名称以及具体的版本，并且还记录了包的下载地址以及它所依赖的包的信息！有了 package-lock.json 文件，当我们用 npm 恢复 node_modules 文件夹时就会依据 package-lock.json 中的记录来下载恢复，大大避免了依赖包版本导致的各种莫名其妙的问题！

## 3.4 ` dependencies `节点

package.json 文件中，有一个<font color='red'> dependencies </font>节点，专门用来记录你使用<font color='gree'> npm install 命令安装了哪些包</font>。

dependencies：依赖关系

实际演示：

- 未安装任何包前的 package.json 文件

```js
{
  "name": "nodestudy",
  "version": "1.0.0",
  "description": "",
  "main": "index.js",
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1"
  },
  "keywords": [],
  "author": "",
  "license": "ISC"
}
```

- 执行 `npm i moment` 命令后的 package.json 文件

同时，项目还多了 node_modules 文件夹（里面存放了 moment 的相关代码和资源）和 package-lock.json 文件。

![](C:\Users\shizeyu\Desktop\notes\Ajax-vue\Snipaste_2023-03-08_15-39-50.png)

> 版本号前带 `^` 表示这是一个大版本，下次下载时，只需要保证版本高于 `2.24.0` 低于 `3.0.0` 即可！

- 执行 `npm i jquery art-template` 命令后的 package.json 文件

> 注：npm i 可以一次安装多个包，包与包之间用空格隔开。

[![image-20221208222947028](https://github.com/JERRY-Z-J-R/I-love-you-3-thousand/raw/master/%E6%88%91%E7%88%B1%E4%BD%A0%EF%BC%8C%E4%B8%8D%E6%AD%A2%E4%B8%89%E5%8D%83%E9%81%8D/Node/05-npm%E4%B8%8E%E5%8C%85/mark-img/image-20221208222947028.png)](https://github.com/JERRY-Z-J-R/I-love-you-3-thousand/blob/master/我爱你，不止三千遍/Node/05-npm与包/mark-img/image-20221208222947028.png)

## 3.5 一次性安装所有的依赖包

当我们拿到一个<font color='red'>剔除了 node_modules </font>的项目后，需要先把所有的包下载到项目中，才能将项目运行起来。否则会报类似于下面的错误：

```js
Error: Cannot find module 'moment'
```

可以运行 <font color='red'> `npm install` </font> 命令（或<font color='red'> `npm i` </font>）一次性安装所有的依赖包（复原 node_modules 文件夹）：

```markdown
# 执行 npm install 命令时，npm 包管理工具会先读取 package.json 及 package-lock.json 中的 dependencies 节点（package-lock.json 优先级更高）
# 读取到记录的所有依赖包名称和版本号之后，npm 包管理工具会把这些依赖包一次性下载到项目中
npm install
```

[![image-20221208224421695](https://github.com/JERRY-Z-J-R/I-love-you-3-thousand/raw/master/%E6%88%91%E7%88%B1%E4%BD%A0%EF%BC%8C%E4%B8%8D%E6%AD%A2%E4%B8%89%E5%8D%83%E9%81%8D/Node/05-npm%E4%B8%8E%E5%8C%85/mark-img/image-20221208224421695.png)](https://github.com/JERRY-Z-J-R/I-love-you-3-thousand/blob/master/我爱你，不止三千遍/Node/05-npm与包/mark-img/image-20221208224421695.png)

## 3.6 卸载包

可以运行<font color='red'> `npm uninstall` </font>命令，来卸载指定的包：

```markdown
# 使用 npm uninstall 具体的包名来卸载包
npm uninstall moment
```

npm uninstall 命令执行成功后，会把对应的包从 node_modules 文件夹中删除，同时自动从 package.json 的 dependencies 中移除掉相应的部分，package-lock.json 同理。

> 注意：npm uninstall 没有简写形式，npm uninstall 可以一次卸载多个包，包与包之间用空格隔开。

[![image-20221208225831587](https://github.com/JERRY-Z-J-R/I-love-you-3-thousand/raw/master/%E6%88%91%E7%88%B1%E4%BD%A0%EF%BC%8C%E4%B8%8D%E6%AD%A2%E4%B8%89%E5%8D%83%E9%81%8D/Node/05-npm%E4%B8%8E%E5%8C%85/mark-img/image-20221208225831587.png)](https://github.com/JERRY-Z-J-R/I-love-you-3-thousand/blob/master/我爱你，不止三千遍/Node/05-npm与包/mark-img/image-20221208225831587.png)

## 3.7 devDependencies节点

如果某些包<font color='gree'>只在项目开发阶段</font>会用到，在<font color='gree'>项目上线之后不会用到</font>，则建议把这些包记录到 `devDependencies` 节点中。

与之对应的，如果某些包在<font color='gree'>开发</font>和<font color='gree'>项目上线之后</font>都需要用到，则建议把这些包记录到 `dependencies` 节点中。

您可以使用如下的命令，将包记录到 devDependencies 节点中：

```markdown
# 安装指定的包，并记录到 devDependencies 节点中
npm i 包名 -D
# 注意：上述命令是简写形式，等价于下面的完整写法
npm install 包名 --save-dev
```

例如：

[![image-20221208231148400](https://github.com/JERRY-Z-J-R/I-love-you-3-thousand/raw/master/%E6%88%91%E7%88%B1%E4%BD%A0%EF%BC%8C%E4%B8%8D%E6%AD%A2%E4%B8%89%E5%8D%83%E9%81%8D/Node/05-npm%E4%B8%8E%E5%8C%85/mark-img/image-20221208231148400.png)](https://github.com/JERRY-Z-J-R/I-love-you-3-thousand/blob/master/我爱你，不止三千遍/Node/05-npm与包/mark-img/image-20221208231148400.png)

> 注意：-D 或 --save-dev 后缀写到 npm install 或 包名 后面都可以。
>
> 即：`npm i webpack -D` 与 `npm i -D webpack` 是等同的。

说明：安装包需不需要指定 `-D`，一般来说在包的文档中都会说明。例如，我们去 npm 网站上搜索 webpack 进入其文档，就会发现有安装说明：

![](C:\Users\shizeyu\Desktop\notes\Ajax-vue\Snipaste_2023-03-08_16-51-31.png)

# 四、镜像源

## 4.1 为什么包下载速度慢

在使用 npm 下包的时候，默认从国外的 npm 官方服务器 https://registry.npmjs.org/ 进行下载，而目前国内的网络与外网是有 “阻隔” 的，因此下包速度会很慢，我们需要使用镜像源来解决这个问题。

## 4.2 淘宝npm镜像服务器

![](C:\Users\shizeyu\Desktop\notes\Ajax-vue\Snipaste_2023-03-08_16-53-58.png)

## 4.3 切换npm的下包镜像源

下包的镜像源，指的就是<font color='gree'>下包的服务器地址</font>。

```markdown
# 查看当前的下包服务器地址
npm config get registry
# 将下包的服务器地址切换为淘宝镜像源
npm config set registry=https://registry.npm.taobao.org/
# 检查镜像源是否切换成功
npm config get registry
```

[![image-20221208233625785](https://github.com/JERRY-Z-J-R/I-love-you-3-thousand/raw/master/%E6%88%91%E7%88%B1%E4%BD%A0%EF%BC%8C%E4%B8%8D%E6%AD%A2%E4%B8%89%E5%8D%83%E9%81%8D/Node/05-npm%E4%B8%8E%E5%8C%85/mark-img/image-20221208233625785.png)](https://github.com/JERRY-Z-J-R/I-love-you-3-thousand/blob/master/我爱你，不止三千遍/Node/05-npm与包/mark-img/image-20221208233625785.png)

> 注意：npm 淘宝镜像源地址已经更换了，新的地址是：https://registry.npmmirror.com/

## 4.4 nrm

为了更方便的切换下包的镜像源，我们可以安装 `nrm` 这个小工具，利用 `nrm` 提供的终端命令，可以快速查看和切换下包的镜像源。

```markdown
# 通过 npm 包管理器，将 nrm 安装为全局可用的工具
npm i nrm -g
```

[![image-20221208234458634](https://github.com/JERRY-Z-J-R/I-love-you-3-thousand/raw/master/%E6%88%91%E7%88%B1%E4%BD%A0%EF%BC%8C%E4%B8%8D%E6%AD%A2%E4%B8%89%E5%8D%83%E9%81%8D/Node/05-npm%E4%B8%8E%E5%8C%85/mark-img/image-20221208234458634.png)](https://github.com/JERRY-Z-J-R/I-love-you-3-thousand/blob/master/我爱你，不止三千遍/Node/05-npm与包/mark-img/image-20221208234458634.png)

```markdown
# 查看所有可用的镜像源
nrm ls
# 将下包的镜像源切换为 taobao 镜像
nrm use taobao
```

[![image-20221208235554902](https://github.com/JERRY-Z-J-R/I-love-you-3-thousand/raw/master/%E6%88%91%E7%88%B1%E4%BD%A0%EF%BC%8C%E4%B8%8D%E6%AD%A2%E4%B8%89%E5%8D%83%E9%81%8D/Node/05-npm%E4%B8%8E%E5%8C%85/mark-img/image-20221208235554902.png)](https://github.com/JERRY-Z-J-R/I-love-you-3-thousand/blob/master/我爱你，不止三千遍/Node/05-npm与包/mark-img/image-20221208235554902.png)

> ![image-20221208234645610](https://github.com/JERRY-Z-J-R/I-love-you-3-thousand/raw/master/%E6%88%91%E7%88%B1%E4%BD%A0%EF%BC%8C%E4%B8%8D%E6%AD%A2%E4%B8%89%E5%8D%83%E9%81%8D/Node/05-npm%E4%B8%8E%E5%8C%85/mark-img/image-20221208234645610.png)
>
> 新版的 Windows 系统中，nrm 默认使用不了，解决方法是：
>
> 1. 管理员方式打开终端执行：`set-ExecutionPolicy RemoteSigned`
> 2. 继续执行：`get-ExecutionPolicy`，如果输出为 `RemoteSigned ` 即为成功。
>
> ![image-20221208235125869](https://github.com/JERRY-Z-J-R/I-love-you-3-thousand/raw/master/%E6%88%91%E7%88%B1%E4%BD%A0%EF%BC%8C%E4%B8%8D%E6%AD%A2%E4%B8%89%E5%8D%83%E9%81%8D/Node/05-npm%E4%B8%8E%E5%8C%85/mark-img/image-20221208235125869.png)

# 五、包的分类

## 5.1 项目包

那些被安装到<font color='gree'>项目</font>的<font color='gree'> node_modules 目录</font>中的包，都是项目包。

项目包又分为两类，分别是：

- <font color='red'>开发依赖包</font>（被记录到 <font color='gree'>devDependencies</font> 节点中的包，只在开发期间会用到）
- <font color='red'>核心依赖包</font>（被记录到 <font color='gree'>dependencies</font> 节点中的包，在开发期间和项目上线之后都会用到）

```markdown
npm i 包名 -D	# 开发依赖包（会被记录到 devDependencies 节点下）
npm i 包名	# 核心依赖包（会被记录到 dependencies 节点下）
```

## 5.2 全局包

在执行 npm install 命令时，如果提供了<font color='red'> `-g` </font>参数，则会把包安装为<font color='red'>全局包</font>。

全局包默认会被安装到<font color='gree'> C:\Users\用户目录\AppData\Roaming\npm\node_modules </font>目录下。

[![image-20221209133414233](https://github.com/JERRY-Z-J-R/I-love-you-3-thousand/raw/master/%E6%88%91%E7%88%B1%E4%BD%A0%EF%BC%8C%E4%B8%8D%E6%AD%A2%E4%B8%89%E5%8D%83%E9%81%8D/Node/05-npm%E4%B8%8E%E5%8C%85/mark-img/image-20221209133414233.png)](https://github.com/JERRY-Z-J-R/I-love-you-3-thousand/blob/master/我爱你，不止三千遍/Node/05-npm与包/mark-img/image-20221209133414233.png)

如图，在该目录下就能发现之前全局安装的 nrm 工具包。

```
npm i 包名 -g				# 全局安装指定的包
npm uninstall 包名 -g 	# 卸载全局安装的包
```

注意：

- 只有<font color='red'>工具性质的包</font>，才有全局安装的必要性。因为它们提供了好用的终端命令。
- 判断某个包是否需要全局安装后才能使用，可以<font color='gree'>参考官方提供的使用说明</font>。



## 5.3 i5ting_toc

i5ting_toc 是一个可以把 md 文档转为 html 页面的小工具，使用步骤如下

```js
// 将 i5ting_toc 安装为全局包
npm install -g i5ting_toc
// 调用 i5ting_toc 轻松实现 md 转 html 功能
i5ting_toc -f 要转换的文件路径 -o
```



# 六、规范的包结构

在清楚了包的概念，以及如何下载和使用包之后，接下来，我们深入了解一下<font color='gree'>包的内部结构</font>。

一个规范的包，它的组成结构，必须符合以下 3 点要求：

- 包必须以<font color='gree'>单独的目录</font>而存在（例如：moment）
- 包的顶级目录下必须包含<font color='red'> package.json </font>这个包管理配置文件（moment 文件夹内包含 package.json）
- package.json 中必须包含<font color='red'> name、version、main </font>这三个属性，分别代表包的<font color='gree'>名字、版本号、包的入口</font>

![](C:\Users\shizeyu\Desktop\notes\Ajax-vue\Snipaste_2023-03-09_14-12-12.png)

> main 属性：当我们加载对应包时，例如：const moment = require('moment') 那么程序就去找 moment 中的 package.json 中的 main 属性，从而知道是要以 ./moment.js 为入口来加载该包。

# 七、开发与发布包

## 7.1 开发属于自己的包

**（1）需要实现的功能**

- <font color='red'>格式化时间</font>

> 当我们在网页上让用户提交一个表单并展示在页面上时，假如用户输入了一串 HTML 代码，那这段 HTML 代码将会被渲染到页面上，造成不堪设想的后果，所以我们要争对 HTML 字符串进行转义。

- <font color='red'>转义</font> HTML 中的<font color='red'>特殊字符</font>
- <font color='red'>还原</font> HTML 中的<font color='red'>特殊字符</font>

### 需要实现的功能

```js
// 1.导入自己得包
const htmlescapetool = require('itheima-utils')

// ----- 功能1：格式化日期 -----
const dt = htmlescapetool.dataFormat(new Date())
// 输出 202x-xx-xx xx:xx:xx
console.log(dt)
```

```js
// 1.导入自己得包
const htmlescapetool = require('itheima-utils')

// ----- 功能2：转义 HTML 中的特殊字符 -----
const htmlStr = '<h1 style="color: red;">你好！ &copy;<span>小黄! </span></h1>'
const str = htmlescapetool.htmlEscape(htmlStr)
// &lt;h1 style=&quot;color: red;&quot;&gt;你好！ &amp;copy;&lt;span&gt;小黄! &lt;/span&gt;&lt;/h1&gt;
console.log(str)
```

```js
// 1.导入自己得包
const htmlescapetool = require('itheima-utils')

// ----- 功能3：还原 HTML 中的特殊字符 -----
const rawHTML = htmlescapetool.htmlUnEscape(str)
// <h1 style="color: red;">你好！ &copy;<span>小黄! </span></h1>
console.log(rawHTML)
```



**（2）初始化包的基本结构**

1. 新建 html-escape-tool 文件夹，作为<font color='gree'>包的根目录</font>
2. 在 html-escape-tool 文件夹中，新建如下三个文件：
   - package.json（包管理配置文件）
   - index.js         （包的入口文件，可以自由取名）
   - README.md（包的说明文档）

![](C:\Users\shizeyu\Desktop\notes\Ajax-vue\Snipaste_2023-03-10_15-02-30.png)

**（3）初始化 package.json**

```js
{
  "name": "escape-tools",
  "version": "1.0.0",
  "main": "index.js",
  "description": "提供格式化时间、 HTML Escape 转义及还原功能",
  "keywords": ["html","escape","dataFormat","szy"],
  "license": "ISC"
}
```

>name : 上线包得名称（跟包所在得文件夹得名称没有关系）（包得名称不能重复 可以先去npm官网去检索一下）
>
>version：版本号
>
>main： 指定入口文件
>
>description：包简短得描述信息
>
>keywords：关键词
>
>license：开源许可协议 默认 ISC

**（4）在 index.js 中定义转义和还原 HTML 的方法**

```js
// 定义转义 HTML 字符串的函数
function htmlEscape(htmlstr) {
    return htmlstr.replace(/<|>|"|&/g, match => {
        switch (match) {
            case '<':
                return '&lt;'
            case '>':
                return '&gt;'
            case '"':
                return '&quot;'
            case '&':
                return '&amp;'
        }
    })
}

// 定义还原 HTML 字符串的函数
function htmlUnEscape(str) {
    return str.replace(/&lt;|&gt;|&quot;|&amp;/g, match => {
        switch (match) {
            case '&lt;':
                return '<'
            case '&gt;':
                return '>'
            case '&quot;':
                return '"'
            case '&amp;':
                return '&'
        }
    })
}

// 定义格式化时间的方法
function dateFormat(dtstr) {
  const dt = new Date(dtstr)
  
  const y = dt.getFullYear()
  const m = padZero(dt.getMonth())
  const d = padZero(dt.getDate())
  
  const hh = padZero(dt.getHours())
  const mm = padZero(dt.getMinutes())
  const ss = padZero(dt.getSeconds())

  return `${y}-${m}-${d} ${hh}:${mm}:${ss}`
}

// 定义补零的函数
function padZero(n) {
  return n > 9 ? n : '0' + n
}

module.exports = {
  dateFormat,
  htmlEscape,
  htmlUnEscape
}

```

> 可以测试一下功能：
>
> ![](C:\Users\shizeyu\Desktop\notes\Ajax-vue\Snipaste_2023-03-10_15-42-39.png)



**<font color='gree'>（5）将不同的功能进行模块化拆分</font>**

> 在真实的开发中，往往功能比较复杂，会有许多的 js 文件，一般不会把功能直接实现在 index.js（入口文件中），而是进行模块化插入，然后在 index.js 中导入。

改进：我们创建一个 src（源代码）目录，然后在里面创建 html-escape.js 文件，在该文件中实现代码并导出，最后在 index.js 中导入。

1. 将格式化时间的功能，拆分到<font color='red'> src -> dateFormat.js </font>中
2. 将处理 HTML 字符串 的功能，拆分到<font color='red'> src -> htmlEscape.js </font>中
3. 在 index.js 中，导入这两个模块，得到需要向外共享的方法
4. 在 index.js 中，使用 module.exports 把对应的方法暴漏共享出去

```js
// dateFormat.js

// 定义格式化时间的方法
function dateFormat(dtstr) {
  const dt = new Date(dtstr)

  const y = dt.getFullYear()
  const m = padZero(dt.getMonth())
  const d = padZero(dt.getDate())

  const hh = padZero(dt.getHours())
  const mm = padZero(dt.getMinutes())
  const ss = padZero(dt.getSeconds())

  return `${y}-${m}-${d} ${hh}:${mm}:${ss}`
}

// 定义补零的函数
function padZero(n) {
  return n > 9 ? n : '0' + n
}
module.exports = {
  dateFormat,
  padZero
}
------------------------------------------------------------
// htmlEscape.js

// 定义转义 HTML 字符串的函数
function htmlEscape(htmlstr) {
  return htmlstr.replace(/<|>|"|&/g, match => {
    switch (match) {
      case '<':
        return '&lt;'
      case '>':
        return '&gt;'
      case '"':
        return '&quot;'
      case '&':
        return '&amp;'
    }
  })
}

// 定义还原 HTML 字符串的函数
function htmlUnEscape(str) {
  return str.replace(/&lt;|&gt;|&quot;|&amp;/g, match => {
    switch (match) {
      case '&lt;':
        return '<'
      case '&gt;':
        return '>'
      case '&quot;':
        return '"'
      case '&amp;':
        return '&'
    }
  })
}
module.exports = {
  htmlEscape,
  htmlUnEscape
}

-------------------------------------------------------------
// index.js（入口文件）

const date = require('./src/dateFormat.js')
const escape = require('./src/htmlEscape.js')

// 转义运算符...
module.exports = {
  ...date,
  ...escape
}

```

**（6）编写包的使用说明文档**

包根目录中的<font color='red'> README.md </font>文件，是<font color='gree'>包的说明文档</font>。把包的使用说明，以 markdown 的格式写出来方便用户参考。

我们创建的这个包的 README.md 具体些什么内容，没有强制的要求。

通常包含以下6项内容：

安装方式、导入方式、格式化时间、转义 HTML 中特殊字符、还原 HTML 中特殊字符、开源协议

````markdown
## 安装

```
npm install escape-tools
```

## 导入

```js
const escapeTools = require('escape-tools')
```

## 格式化时间

方法：`dateFormat(date)`

```js
// 调用dateFormat方法格式化时间
const dtstr = escapeTools.dateFormat(new Date())
// 输出结果：2023-02-10 16:17:18
console.log(dtstr)
```

## 转义 HTML 字符

- `<`：`&lt;`
- `>`：`&gt;`
- `"`：`&quot;`
- `&`：`&amp;`

方法：`htmlEscape(htmlStr)`

```js
const htmlStr = '<h1 style="color: red;">测试test &copy;<span>xxxx! </span></h1>'
const str = escapeTools.htmlEscape(htmlStr)
console.log(str)
//&lt;h1 style=&quot;color: red;&quot;&gt;测试test &amp;copy;&lt;span&gt;xxxx! &lt;/span&gt;&lt;/h1&gt;
```

## 还原 HTML 字符

- `&lt;`：`<`
- `&gt;`：`>`
- `&quot;`：`"`
- `&amp;`：`&`

方法：`htmlUnEscape(str)`

```js
const rawHTML = escapeTools.htmlUnEscape(str)
console.log(rawHTML)
// <h1 style="color: red;">测试test &copy;<span>xxxx! </span></h1>
```

## 开源协议

ISC

````

**（7）本地测试**

![](C:\Users\shizeyu\Desktop\notes\Ajax-vue\Snipaste_2023-03-10_16-30-42.png)

## 7.2 发布包

**（1）注册 npm 账号**

[npm | Sign Up (npmjs.com)](https://www.npmjs.com/signup)

**（2）利用终端登录 npm 账号**

登录命令：<font color='red'>`npm login`</font>

> 注意：在运行 npm login 命令之前，必须先把<font color='gree'>下包的服务器</font>地址切换为<font color='gree'> npm 官方服务器</font>！

![](C:\Users\shizeyu\Desktop\notes\Ajax-vue\Snipaste_2023-03-13_11-03-35.png)

**（3）把包发布到 npm 上**

将终端切换到包的根目录之后，运行<font color='red'> `npm publish` </font>命令，即可将包发布到 npm 上。

> 注意：包名不能与 npm 仓库中已存在的包雷同！

![](C:\Users\shizeyu\Desktop\notes\Ajax-vue\Snipaste_2023-03-13_11-07-08.png)

到 npm 官网上查看：

![](C:\Users\shizeyu\Desktop\notes\Ajax-vue\Snipaste_2023-03-13_11-08-29.png)

![](C:\Users\shizeyu\Desktop\notes\Ajax-vue\Snipaste_2023-03-13_11-08-43.png)

![](C:\Users\shizeyu\Desktop\notes\Ajax-vue\Snipaste_2023-03-13_11-09-41.png)

![](C:\Users\shizeyu\Desktop\notes\Ajax-vue\Snipaste_2023-03-13_11-10-49.png)



## 7.3 更新包

比如，1.0.0 版本的文档有错误，我们对 README.md 进行了修复：

[![image-20221211212715569](https://github.com/JERRY-Z-J-R/I-love-you-3-thousand/raw/master/%E6%88%91%E7%88%B1%E4%BD%A0%EF%BC%8C%E4%B8%8D%E6%AD%A2%E4%B8%89%E5%8D%83%E9%81%8D/Node/05-npm%E4%B8%8E%E5%8C%85/mark-img/image-20221211212715569.png)](https://github.com/JERRY-Z-J-R/I-love-you-3-thousand/blob/master/我爱你，不止三千遍/Node/05-npm与包/mark-img/image-20221211212715569.png)

- `npm version patch` 升级补丁，此时 package 中的 version 会自动升级，变成 `"version": "1.0.1"`
- git 操作（若有）
- `npm publish` 发布更新

> 升级分 **补丁/次版本/主版本** 三种方式：
>
> - patch（补丁）`npm version patch`，1.0.0 —> 1.0.1
> - minor（次要版本）`npm version minor`，1.0.0 —> 1.1.0
> - major（主要版本）`npm version major`，1.0.0 —> 2.0.0

## 7.4 删除包

运行<font color='red'> `npm unpublish 包名 --force` </font>命令，即可从 npm 删除已经发布的包。

![](C:\Users\shizeyu\Desktop\notes\Ajax-vue\Snipaste_2023-03-13_11-14-00.png)

注意：

- npm unpublish 命令只能删除<font color='gree'> 72 小时以内</font>发布的包<（为了防止依赖消失事故）(然后就永远不能删除了)
- npm unpublish 删除的包，在<font color='gree'> 24 小时内</font>不允许重复发布

# 八、模块的加载机制

## 8.1 优先从缓存中加载

<font color='gree'>模块在第一次加载后会被缓存</font>，接下来的加载都会优先从缓存中加载，从而提高模块的加载效率。

这也意味着多次调用<font color='red'> `require()` </font>不会导致模块的代码被执行多次！

## 8.2 内置模块的加载机制

内置模块是由 Node.js 官方提供的模块，<font color='gree'>内置模块的加载优先级最高</font>

> 例如 node_modules 目录下有名字相同的包，在require('fs')时还是返回内置的fs模块

## 8.3 自定义模块的加载机制

使用 `require()` 加载自定义模块时，必须指定以<font color='gree'> `./` 或 `../` 开头的路径标识符</font>。在加载自定义模块时，如果没有指定 `./` 或 `../` 这样的路径标识符，则 Node.js 会把它当作<font color='red'>内置模块</font>或<font color='red'>第三方模块</font>进行加载（加载不到就会报错）。

同时，在使用 `require()` 导入自定义模块时，如果省略了文件的扩展名，则 Node.js 会按顺序分别尝试加载以下的文件：

1. 按照<font color='red'>确切的文件名</font>进行加载
2. 补全 .js 扩展名进行加载
3. 补全 .json 扩展名进行加载
4. 补全 .node 扩展名进行加载
5. 加载失败，终端报错

## 8.4 第三方模块的加载机制

如果传递给 `require()` 的模块标识符不是一个内置模块，也没有以 `./` 或 `../` 开头，则 Node.js 会从当前模块的父目录开始，尝试从 /node_modules 文件夹中加载第三方模块。

<font color='gree'>如果没有找到对应的第三方模块，则移动到再上一层父目录中，进行加载，直到文件系统的根目录。</font>

例如，假设在<font color='grree'> C:\Users\jerry\project\foo.js 文</font>件里调用了 `require('tools')`，则 Node.js 会按以下顺序查找：

1. C:\Users\jerry\project\node_modules\tools
2. C:\Users\jerry\node_modules\tools
3. C:\Users\node_modules\tools
4. C:\node_modules\tools
5. 加载失败，终端报错

## 8.5 目录作为模块

当把目录作为模块标识符，传递给 `require()` 进行加载的时候，有三种加载方式：

1. 在被加载的目录下查找一个叫做 package.json 的文件，并寻找 main 属性，作为 require() 加载的入口
2. 如果目录里没有 package.json 文件，或者 main 入口不存在或无法解析，则 Node.js 将会试图加载目录下的 index.js 文件
3. 如果以上两步都失败了，则 Node.js 会在终端打印错误消息，报告模块的缺失：Error: Cannot find module 'xxx'



------

# 【Express】

# 一、初始Express

## 1.1 Express简介

**（1）什么是 Express？**

官方给出的概念：Express 是<font color='gree'>基于 Node.js 平台，快速、开放、极简的 Web 开发框架</font>。

通俗的理解：Express 的作用和 Node.js 内置的 http 模块类似，<font color='gree'>是专门用来创建 Web 服务器的</font>。

<font color='red'>Express 的本质</font>：就是一个 npm 上的第三方的包，提供了快速创建 Web 服务器的便捷方法。

Express 的中文官网：http://www.expressjs.com.cn/

Express 的中文文档：http://nodejs.cn/express/

[![image-20221213144211088](https://github.com/JERRY-Z-J-R/I-love-you-3-thousand/raw/master/%E6%88%91%E7%88%B1%E4%BD%A0%EF%BC%8C%E4%B8%8D%E6%AD%A2%E4%B8%89%E5%8D%83%E9%81%8D/Node/06-express/mark-img/image-20221213144211088.png)](https://github.com/JERRY-Z-J-R/I-love-you-3-thousand/blob/master/我爱你，不止三千遍/Node/06-express/mark-img/image-20221213144211088.png)

**（2）进一步理解 Express**

思考：不使用 Express 能否创建 Web 服务器？

答案：能！使用 Node.js 提供的原生 http 模块即可。

------

思考：既生瑜何生亮（有了 http 内置模块，为什么还有用 Express）？

答案：http 内置模块用起来很复杂，开发效率低；Express 是基于内置的 http 模块进一步封装出来的，能够极大的提高开发效率。

------

思考：http 内置模块与 Express 是什么关系？

答案：类似于浏览器中 Web API 和 jQuery 的关系。<font color='gree'>后者是基于前者进一步封装出来的</font>。

**（3）Express 能做什么？**

对于前端程序员来说，<font color='gree'>最常见的两种服务器</font>，分别是：

- <font color='red'>Web 网站服务器</font>：专门对外提供 Web 网页资源的服务器。
- <font color='red'>API 接口服务器</font>：专门对外提供 API 接口的服务器。

使用 Express，我们可以方便、快速的创建<font color='red'> Web 网站</font>的服务器或<font color='red'> API 接口</font>的服务器。



## 1.2 Express的基本使用

### 1.2.1 安装

在项目所处的目录中，运行如下命令，即可将 express 安装到项目中使用：

```apl
npm i express@4.17.1
# 这里统一使用 4.17.1 版本来做演示
```

### 1.2.2 创建基本的Web服务器

```js
// 导入 express
const express = require('express');

// 创建 web 服务器 调用函数返回实例
const app = express();

// 启动 web 服务器
// app.listen(端口号, 启动成功后的回调函数)
app.listen(80, () => {
    console.log('express server running at http://127.0.0.1');
});
```



### 1.2.3 监听<font color='red'>GET请求</font>

通过 `app.get()` 方法，可以监听客户端的 GET 请求，具体的语法格式如下：

```js
// 参数1：客户端请求的 URL 地址
// 参数2：请求对应的处理函数
// 		req：请求对象（包含了与请求相关的属性与方法）
//		res：响应对象（包含了与响应相关的属性与方法）
app.get('请求URL', function(req, res) {
   // 处理     
});
```

### 1.2.4 监听<font color='red'>POST请求</font>

通过 `app.post()` 方法，可以监听客户端的 POST 请求，具体的语法格式如下：

```js
// 参数1：客户端请求的 URL 地址
// 参数2：请求对应的处理函数
// 		req：请求对象（包含了与请求相关的属性与方法）
//		res：响应对象（包含了与响应相关的属性与方法）
app.post('请求URL', function(req, res) {
   // 处理     
});
```

### 1.2.5 把内容<font color='red'>响应</font>给客户端

通过<font color='red'> `res.send()` </font>方法，可以把处理好的内容，发送给客户端：

```js
app.get('/user', (req, res) => {
    // 向客户端发送 JSON 对象（express 会自动将 js 对象转为 json）
    res.send({ name: 'zjr', age: '18', gender: '男' });
});

app.post('/user', (req, res) => {
    // 向客户端发送文本内容
    res.send('请求成功');
});
```

------

测试：

```js
// 导入 express
const express = require('express');

// 创建 web 服务器
const app = express();

// 监听客户端的 GET 和 POST 请求，并向客户端响应具体的内容
app.get('/user', (req, res) => {
    // 向客户端发送 JSON 对象（express 会自动将 js 对象转为 json）
    res.send({ name: 'zjr', age: '18', gender: '男' });
});

app.post('/user', (req, res) => {
    // 向客户端发送文本内容
    res.send('请求成功');
});

// 启动 web 服务器
// app.listen(端口号, 启动成功后的回调函数)
app.listen(80, () => {
    console.log('express server running at http://127.0.0.1');
});
```

运行：

[![image-20221213154814267](https://github.com/JERRY-Z-J-R/I-love-you-3-thousand/raw/master/%E6%88%91%E7%88%B1%E4%BD%A0%EF%BC%8C%E4%B8%8D%E6%AD%A2%E4%B8%89%E5%8D%83%E9%81%8D/Node/06-express/mark-img/image-20221213154814267.png)](https://github.com/JERRY-Z-J-R/I-love-you-3-thousand/blob/master/我爱你，不止三千遍/Node/06-express/mark-img/image-20221213154814267.png)

Apifox 测试：

[![image-20221213151456261](https://github.com/JERRY-Z-J-R/I-love-you-3-thousand/raw/master/%E6%88%91%E7%88%B1%E4%BD%A0%EF%BC%8C%E4%B8%8D%E6%AD%A2%E4%B8%89%E5%8D%83%E9%81%8D/Node/06-express/mark-img/image-20221213151456261.png)](https://github.com/JERRY-Z-J-R/I-love-you-3-thousand/blob/master/我爱你，不止三千遍/Node/06-express/mark-img/image-20221213151456261.png)

[![image-20221213151517593](https://github.com/JERRY-Z-J-R/I-love-you-3-thousand/raw/master/%E6%88%91%E7%88%B1%E4%BD%A0%EF%BC%8C%E4%B8%8D%E6%AD%A2%E4%B8%89%E5%8D%83%E9%81%8D/Node/06-express/mark-img/image-20221213151517593.png)](https://github.com/JERRY-Z-J-R/I-love-you-3-thousand/blob/master/我爱你，不止三千遍/Node/06-express/mark-img/image-20221213151517593.png)

> 注意：对于一个请求，只能 `res.send()` 一次！



### 1.2.6 获取URL中携带的查询参数

通过<font color='red'> `req.query` </font>对象，可以访问到客户端通过<font color='gree'>查询字符串</font>的形式，发送到服务器的参数。

> 默认情况下 req.query 是一个空对象

```js
app.get('/', (req, res) => {
    // req.query 默认是一个空对象
    // 客户端使用 ?name=zjr&age=20 这种查询字符串的形式，发送到服务器的参数
    // 可以通过 req.query 对象访问到，例如：
	// req.query.name  req.query.age
    console.log(req.query);
    console.log(req.query.name);
    console.log(req.query.age);
});
```

### 1.2.7 获取URL中的<font color='red'>动态参数</font>

通过<font color='red'> `req.params` </font>对象，可以访问到 URL 中，通过<font color='red'> `:` </font>匹配到的<font color='red'>动态参数</font>。

```js
// URL 地址中，可以通过 :参数名 的形式，匹配动态参数值
app.get('/user/:id', (req, res) => {
    // req.params 默认是一个空对象
    // 里面存放着通过 : 动态匹配到的参数值
    // 例如：http://127.0.0.1/user/1010929843210，则服务器收到的 1010929843210 就被赋给了 id 参数
    console.log(req.params);
    console.log(req.params.id);
});

app.get('/user/:id/:name', (req, res) => {
    // 例如：http://127.0.0.1/user/1010929843210/szy ，则服务器收到的 1010929843210 就被赋给了 id 参数
    // szy 就被赋给了 name 参数
    console.log(req.params);
    console.log(req.params.id);
});
```

------

测试：

```js
// 导入 express
const express = require('express');

// 创建 web 服务器
const app = express();

// 监听客户端的 GET 和 POST 请求，并向客户端响应具体的内容
app.get('/user', (req, res) => {
    // 向客户端发送 JSON 对象（express 会自动将 js 对象转为 json）
    res.send({ name: 'zjr', age: '18', gender: '男' });
});

app.post('/user', (req, res) => {
    // 向客户端发送文本内容
    res.send('请求成功');
});

app.get('/', (req, res) => {
    // req.query 默认是一个空对象
    // 客户端使用 ?name=zjr&age=20 这种查询字符串的形式，发送到服务器的参数
    // 可以通过 req.query 对象访问到，例如：
    // req.query.name	req.query.age
    res.send(req.query);
});

// URL 地址中，可以通过 :参数名 的形式，匹配动态参数值
app.get('/user/:id', (req, res) => {
    // req.params 默认是一个空对象
    // 里面存放着通过 : 动态匹配到的参数值
    res.send(req.params);
});

// 启动 web 服务器
// app.listen(端口号, 启动成功后的回调函数)
app.listen(80, () => {
    console.log('express server running at http://127.0.0.1');
});
```

Apifox 测试：

[![image-20221213155149127](https://github.com/JERRY-Z-J-R/I-love-you-3-thousand/raw/master/%E6%88%91%E7%88%B1%E4%BD%A0%EF%BC%8C%E4%B8%8D%E6%AD%A2%E4%B8%89%E5%8D%83%E9%81%8D/Node/06-express/mark-img/image-20221213155149127.png)](https://github.com/JERRY-Z-J-R/I-love-you-3-thousand/blob/master/我爱你，不止三千遍/Node/06-express/mark-img/image-20221213155149127.png)

[![image-20221213155141877](https://github.com/JERRY-Z-J-R/I-love-you-3-thousand/raw/master/%E6%88%91%E7%88%B1%E4%BD%A0%EF%BC%8C%E4%B8%8D%E6%AD%A2%E4%B8%89%E5%8D%83%E9%81%8D/Node/06-express/mark-img/image-20221213155141877.png)](https://github.com/JERRY-Z-J-R/I-love-you-3-thousand/blob/master/我爱你，不止三千遍/Node/06-express/mark-img/image-20221213155141877.png)

[![image-20221213160212006](https://github.com/JERRY-Z-J-R/I-love-you-3-thousand/raw/master/%E6%88%91%E7%88%B1%E4%BD%A0%EF%BC%8C%E4%B8%8D%E6%AD%A2%E4%B8%89%E5%8D%83%E9%81%8D/Node/06-express/mark-img/image-20221213160212006.png)](https://github.com/JERRY-Z-J-R/I-love-you-3-thousand/blob/master/我爱你，不止三千遍/Node/06-express/mark-img/image-20221213160212006.png)



## 1.3 托管静态资源

### 1.3.1 express.static()

> express.static() 是 Express内置中间件 ，详见下

express 提供了一个非常好用的函数，叫做<font color='red'> `express.static()`</font>，通过它，我们可以<font color='gree'>非常方便地创建一个静态资源服务器</font>！例如，通过如下代码就可以将 public 目录下的图片、CSS 文件、JavaScript 文件对外开放访问了：

```apl
app.use(express.static('public'));
```

现在，你就可以访问 public 目录中的所有文件了：

```js
http://localhost/images/bg.jpg
http://localhost/css/style.css
http://localhost/js/login.js
```

> <font color='red'>**注意：**</font>Express 在<font color='red'>指定的</font>静态目录中查找文件，并对外提供资源的访问路径，因此，<font color='gree'>存放静态文件的目录名（public）不会出现在 URL 中</font>。

```js
const express = require('express');
const app = express();

app.use(express.static('./public'));

app.listen(80, () => {
    console.log('express server running at http://127.0.0.1');
});
```

[![image-20221213163159099](https://github.com/JERRY-Z-J-R/I-love-you-3-thousand/raw/master/%E6%88%91%E7%88%B1%E4%BD%A0%EF%BC%8C%E4%B8%8D%E6%AD%A2%E4%B8%89%E5%8D%83%E9%81%8D/Node/06-express/mark-img/image-20221213163159099.png)](https://github.com/JERRY-Z-J-R/I-love-you-3-thousand/blob/master/我爱你，不止三千遍/Node/06-express/mark-img/image-20221213163159099.png)

[![image-20221213163117265](https://github.com/JERRY-Z-J-R/I-love-you-3-thousand/raw/master/%E6%88%91%E7%88%B1%E4%BD%A0%EF%BC%8C%E4%B8%8D%E6%AD%A2%E4%B8%89%E5%8D%83%E9%81%8D/Node/06-express/mark-img/image-20221213163117265.png)](https://github.com/JERRY-Z-J-R/I-love-you-3-thousand/blob/master/我爱你，不止三千遍/Node/06-express/mark-img/image-20221213163117265.png)



### 1.3.2 托管多个静态资源目录

如果要托管多个静态资源目录，请多次调用 `express.static()` 函数：

```apl
app.use(express.static('public'));
app.use(express.static('files'));
```

<font color='gree'>访问静态资源文件时，`express.static()` 函数会根据目录的添加顺序查找所需的文件</font>。

例如：先查找 public 中有没有，没有再去 files 中查找……

### 1.3.3 挂载<font color='red'>路径前缀</font>

如果希望在托管的<font color='gree'>静态资源访问路径</font>之前，<font color='gree'>挂载路径前缀</font>，则可以使用如下的方式：

```apl
app.use('/public', express.static('public'))
```

现在，你就可以通过带有 /public 前缀地址来访问 public 目录中的文件了：

```apl
http://localhost/public/images/kitten.jpg
http://localhost/public/css/style.css
http://localhost/public/js/app.js
```

## 1.4 nodemon

**（1）为什么要使用 nodemon**

在编写调试 Node.js 项目的时候，如果修改了项目的代码，则需要频繁的手动 close 掉，然后再重新启动，非常繁琐。现在，我们可以使用 [nodemon](https://www.npmjs.com/package/nodemon) 这个工具，它能够<font color='gree'>监听项目文件的变动</font>，当代码被修改后，nodemon 会<font color='gree'>自动帮我们重启项目</font>，极大方便了开发和调试！

**（2）安装 nodemon**

在终端中，运行如下命令，即可将 nodemon 安装为全局可用的工具：

```apl
npm install -g nodemon
```

**（3）使用 nodemon**

当基于 Node.js 编写了一个网站应用的时候，传统的方式，是运行<font color='red'> node app.js </font>命令，来启动项目。这样做的坏处是：代码被修改之后，需要手动重启项目。

现在，我们可以将 node 命令替换为 nodemon 命令，使用<font color='red'> nodemon app.js </font>来启动项目。这样做的好处是：代码被修改之后，会被 nodemon 监听到，从而实现自动重启项目的效果。

```apl
nodemon app.js
```

即：每一次修改代码并保存时，nodemon 会自动重启一次项目。

# 二、Express路由

## 2.1 路由的概念

### 2.1.1 什么是路由

广义上来讲，路由就是<font color='red'>映射关系</font>。

### 2.1.2 现实生活中的路由

在这里，路由是按键与服务之间的映射关系。

![](C:\Users\shizeyu\Desktop\notes\Ajax-vue\Snipaste_2023-03-14_16-07-45.png)

### 2.1.3 Express中的路由

在 Express 中，路由指的是<font color='red'> **客户端的请求** </font>与<font color='red'> **服务端处理函数** </font>之间的<font color='gree'>映射关系</font>。

Express 中的路由分 3 部分组成，分别是：<font color='gree'>**请求的类型**、**请求的 URL 地址**、**处理函数**</font>，格式如下：

```apl
// METHOD 即请求类型（GET、POST）
app.METHOD(PATH, HANDLER);
```

### 2.1.4 Express中的路由的例子

```js
// 匹配 GET 请求，且请求 URL 为 /
app.get('/', function (req, res) {
   res.send('Got a GET request');     
});

// 匹配 POST 请求，且请求为 URL 为 /
app.post('/', function (req, res) {
   res.send('Got a POST request');      
});
```

### 2.1.5 路由的匹配过程

每当一个请求到达服务器之后，<font color='gree'>需要先经过路由的匹配</font>，只有匹配成功之后，才会调用对应的处理函数。

在匹配时，会按照路由的顺序进行匹配，如果<font color='gree'>请求类型</font>和<font color='gree'>请求的 URL </font>同时匹配成功，则 Express 会将这次请求，转交给对应的 function 函数进行处理。

![](C:\Users\shizeyu\Desktop\notes\Ajax-vue\Snipaste_2023-03-14_16-16-41.png)

路由匹配的注意点：

- 按照<font color='gree'>定义的先后顺序</font>进行匹配
- <font color='gree'>请求类型</font>和<font color='gree'>请求的 URL </font>同时匹配成功，才会调用对应的处理函数



## 2.2 路由的使用

### 2.2.1 最简单的用法(没用)

在 Express 中使用路由最简单的方式，就是把路由挂载到 app 上，示例代码如下：

```js
const express = require('express');

// 创建 Web 服务器，命名为 app
const app = express();

// 挂载路由
app.get('/', (req, res) => {
    res.send('Get Request.');
});

// 挂载路由
app.post('/', (req, res) => {
    res.send('Post Request.');
});

app.listen(80, () => {
    console.log('server running at http://127.0.0.1');
});
```

### 2.2.2 <font color='red'>模块化</font>路由（推荐）

为了<font color='gree'>方便对路由进行模块化的管理</font>，Express <font color='red'>不建议</font>将路由直接挂载到 app 上，而是<font color='gree'>推荐将路由抽离为单独的模块</font>。

将路由抽离为单独模块的步骤如下：

1. 创建路由模块对应的 .js 文件
2. 调用<font color='red'> `express.Router()` </font>函数创建路由对象
3. 向路由对象上挂载具体的路由
4. 使用<font color='red'> `module.exports` </font>向外共享路由对象
5. 使用<font color='red'> `app.use()` </font>函数注册路由模块

**（1）创建路由模块 router/user.js**

```js
// 导入 express
const express = require('express');
// 创建路由对象
const router = express.Router();		

// 挂载获取用户列表
router.get('/user/list', function (req, res) {
    res.send('Get user list.');
});

// 挂载添加用户的路由
router.post('/user/add', function (req, res) {
    res.send('Add new user.');
});

// 向外导出路由对象
module.exports = router;
```

**（2）注册路由模块**

```js
// 导入路由模块
const userRouter = require('./router/user.js');

// 使用 app.use() 注册路由模块
app.use(userRouter);
```

------

实例代码：

```js
// router/user.js

// 导入 express
const express = require('express');
// 创建路由对象
const router = express.Router();

// 挂载获取用户列表
router.get('/user/list', function (req, res) {
    res.send('Get user list.');
});

// 挂载添加用户的路由
router.post('/user/add', function (req, res) {
    res.send('Add new user.');
});

// 向外导出路由对象
module.exports = router;

------------------------------------------------
// webtest.js

// 导入 express
const express = require('express');
// 创建 web 服务器
const app = express();

// 导入路由模块
const userRouter = require('./router/user.js');

// 使用 app.use() 注册路由模块
app.use(userRouter);

app.listen(80, () => {
    console.log('http://127.0.0.1');
});
```

[![image-20221213211450640](https://github.com/JERRY-Z-J-R/I-love-you-3-thousand/raw/master/%E6%88%91%E7%88%B1%E4%BD%A0%EF%BC%8C%E4%B8%8D%E6%AD%A2%E4%B8%89%E5%8D%83%E9%81%8D/Node/06-express/mark-img/image-20221213211450640.png)](https://github.com/JERRY-Z-J-R/I-love-you-3-thousand/blob/master/我爱你，不止三千遍/Node/06-express/mark-img/image-20221213211450640.png)

Apifox 测试：

[![image-20221213211745447](https://github.com/JERRY-Z-J-R/I-love-you-3-thousand/raw/master/%E6%88%91%E7%88%B1%E4%BD%A0%EF%BC%8C%E4%B8%8D%E6%AD%A2%E4%B8%89%E5%8D%83%E9%81%8D/Node/06-express/mark-img/image-20221213211745447.png)](https://github.com/JERRY-Z-J-R/I-love-you-3-thousand/blob/master/我爱你，不止三千遍/Node/06-express/mark-img/image-20221213211745447.png)

[![image-20221213211806480](https://github.com/JERRY-Z-J-R/I-love-you-3-thousand/raw/master/%E6%88%91%E7%88%B1%E4%BD%A0%EF%BC%8C%E4%B8%8D%E6%AD%A2%E4%B8%89%E5%8D%83%E9%81%8D/Node/06-express/mark-img/image-20221213211806480.png)](https://github.com/JERRY-Z-J-R/I-love-you-3-thousand/blob/master/我爱你，不止三千遍/Node/06-express/mark-img/image-20221213211806480.png)

> 在注册路由模块时，我们使用到了 app.use() 函数，而在之前托管静态资源 `app.use(express.static('public')) `时，也使用到了 `app.use()` 函数。
>
> 那 `app.use()` 函数到底是干什么的呢？
>
> 其实，<font color='gree'>`app.use()` 函数的作用，就是用来注册全局中间件！</font>（中间件相关概念后面讲）

## 2.3 为路由模块<font color='red'>添加前缀</font>

类似于托管静态资源时，为静态资源统一挂载访问前缀一样，路由模块添加前缀的方式也非常简单：

```js
// 导入路由模块
const userRouter = require('./router/user.js');

// 使用 app.use() 注册路由模块，并统一添加访问前缀 /api
app.use('/api', userRouter);
```

例如：

```apl
http://127.0.0.1/api/user/add
http://127.0.0.1/api/user/list
```

# 三、Express中间件

## 3.1 中间件的概念

### 3.1.1 什么是中间件

中间件（Middleware），特指<font color='gree'>业务流程</font>的<font color='red'>中间处理环境</font>。

特点：有输入，也有输出！

### 3.1.2 现实生活中的例子

在处理污水的时候，一般都要经过<font color='gree'>三个处理环节</font>，从而保证处理过后的废水，达到排放的标准。

[![image-20221214151430425](https://github.com/JERRY-Z-J-R/I-love-you-3-thousand/raw/master/%E6%88%91%E7%88%B1%E4%BD%A0%EF%BC%8C%E4%B8%8D%E6%AD%A2%E4%B8%89%E5%8D%83%E9%81%8D/Node/06-express/mark-img/image-20221214151430425.png)](https://github.com/JERRY-Z-J-R/I-love-you-3-thousand/blob/master/我爱你，不止三千遍/Node/06-express/mark-img/image-20221214151430425.png)

处理污水的这三个中间处理环节（上一级的输出是下一级的输入），就可以叫作中间件。

### 3.1.3 Express中间件的<font color='red'>调用流程</font>

当一个请求到达 Express 的服务器之后，可以连续调用多个中间件，从而对这次请求进行<font color='gree'>预处理</font>。

[![image-20221214152006656](https://github.com/JERRY-Z-J-R/I-love-you-3-thousand/raw/master/%E6%88%91%E7%88%B1%E4%BD%A0%EF%BC%8C%E4%B8%8D%E6%AD%A2%E4%B8%89%E5%8D%83%E9%81%8D/Node/06-express/mark-img/image-20221214152006656.png)](https://github.com/JERRY-Z-J-R/I-love-you-3-thousand/blob/master/我爱你，不止三千遍/Node/06-express/mark-img/image-20221214152006656.png)

### 3.1.4 Express中间件的<font color='red'>格式</font>

Express 的中间件，<font color='red'>本质</font>上就是一个<font color='gree'> **function** **处理函数**</font>，Express 中间件的格式如下：

![](C:\Users\shizeyu\Desktop\notes\Ajax-vue\Snipaste_2023-03-16_16-52-40.png)

注意：中间件函数的形参列表中，<font color='gree'>**必须包含 next 参数**</font>。而路由处理函数中只包含 req 和 res。

### 3.1.5 next函数的作用

<font color='red'>**next** **函数**</font>是实现<font color='gree'>多个中间件**连续调用**</font>的关键，它表示把流转关系<font color='red'>转交</font>给<font color='gree'>**下一个中间件或路由**</font>。

[![image-20221214154001061](https://github.com/JERRY-Z-J-R/I-love-you-3-thousand/raw/master/%E6%88%91%E7%88%B1%E4%BD%A0%EF%BC%8C%E4%B8%8D%E6%AD%A2%E4%B8%89%E5%8D%83%E9%81%8D/Node/06-express/mark-img/image-20221214154001061.png)](https://github.com/JERRY-Z-J-R/I-love-you-3-thousand/blob/master/我爱你，不止三千遍/Node/06-express/mark-img/image-20221214154001061.png)

## 3.2 Express中间件的初体验

### 3.2.1 <font color='red'>定义</font>中间件函数

可以通过如下的方式，定义一个最简单的中间件函数：

```js
// 常量 mw 所指向的，就是一个中间件函数
const mw = function (req, res, next) {
    console.log('这是一个最简单的中间件函数');
    // 注意：在当前中间件的业务处理完毕后，必须调用 next() 函数
    // 表示把流转关系转交给下一个中间件或路由器
    next();
};
```

### 3.2.2 <font color='red'>全局生效</font>的中间件

客户端发起的<font color='red'>任何请求</font>，到达服务器之后，<font color='gree'>都会触发的中间件</font>，叫作全局生效的中间件。

通过调用 <font color='red'>`app.use(中间件函数)`</font>，即可定义一个<font color='red'>全局生效</font>的中间件，示例代码如下：

```js
// 常量 mw 所指向的，就是一个中间件函数
const mw = function (req, res, next) {
    console.log('这是一个最简单的中间件函数');
    next();
};

// 全局生效的中间件
app.use(mw);
```

测试代码：

```js
const express = require('express');

const app = express();

// 定义一个最简单的中间件函数
const mw = function (req, res, next) {
    console.log('这是最简单的中间件函数');
    // 把流转关系，转交给下一个中间件或路由
    next();
};

// 将 mw 注册为全局生效的中间件
app.use(mw);

app.get('/', (req, res) => {
    console.log('经过路由')
    res.send('Home page.');
});

app.get('/user', (req, res) => {
    res.send('User page.');
});

app.listen(80, () => {
    console.log('http://127.0.0.1');
});
```

Apifox 测试：

> <font color='red'>先过中间件，然后通过路由</font>

![](C:\Users\shizeyu\Desktop\notes\Ajax-vue\Snipaste_2023-03-17_17-00-50.png)

[![image-20221214212100951](https://github.com/JERRY-Z-J-R/I-love-you-3-thousand/raw/master/%E6%88%91%E7%88%B1%E4%BD%A0%EF%BC%8C%E4%B8%8D%E6%AD%A2%E4%B8%89%E5%8D%83%E9%81%8D/Node/06-express/mark-img/image-20221214212100951.png)](https://github.com/JERRY-Z-J-R/I-love-you-3-thousand/blob/master/我爱你，不止三千遍/Node/06-express/mark-img/image-20221214212100951.png)

[![image-20221214212139237](https://github.com/JERRY-Z-J-R/I-love-you-3-thousand/raw/master/%E6%88%91%E7%88%B1%E4%BD%A0%EF%BC%8C%E4%B8%8D%E6%AD%A2%E4%B8%89%E5%8D%83%E9%81%8D/Node/06-express/mark-img/image-20221214212139237.png)](https://github.com/JERRY-Z-J-R/I-love-you-3-thousand/blob/master/我爱你，不止三千遍/Node/06-express/mark-img/image-20221214212139237.png)

### 3.2.3 定义<font color='red'>全局中间件</font>的<font color='gree'>简化形式</font>

```js
// 全局生效的中间件
app.use(function (req, res, next) {
	console.log('这是一个最简单的中间件函数');
	next();
});
```

代码示例：

```js
const express = require('express');

const app = express();

// 定义全局中间件的简化形式
app.use((req, res, next) => {
    console.log('这是最简单的中间件函数');
    // 把流转关系，转交给下一个中间件或路由
    next();
});

app.get('/', (req, res) => {
    res.send('Home page.');
});

app.get('/user', (req, res) => {
    res.send('User page.');
});

app.listen(80, () => {
    console.log('http://127.0.0.1');
});
```

> <font color='gree'>注意：对于一个请求，如果在全局中间件中 `res.send()` 过一次，那么后续，无论是全局中间件内，还是其他中间件或路由中的 `res.send()` 都会报错！</font>
>
> <font color='gree'>即：一个请求，只对应一个 req 及 res ，也只能有一个 `res.send()`。</font>

### 3.2.4 中间件的<font color='red'>作用</font>

多个中间件之间，<font color='gree'>**共享同一份** **req** **和** **res**</font>。基于这样的特性，我们可以在<font color='gree'>上游</font>的中间件中，<font color='red'>统一</font>为 req 或 res 对象添加<font color='gree'>自定义的属性或方法</font>，供<font color='gree'>下游</font>的中间件或路由进行使用。

![](C:\Users\shizeyu\Desktop\notes\Ajax-vue\Snipaste_2023-03-21_16-47-49.png)

>就像小船带着数据传输

代码示例：

```js
const express = require('express');

const app = express();

// 定义全局中间件的简化形式
app.use((req, res, next) => {
    // 获取到请求服务器的时间
    const time = Date.now();
    // 为 req 对象，挂载自定义属性，从而把时间共享给后面的所有路由
    req.startTime = time;
    // 把流转关系，转交给下一个中间件或路由
    next();
});

app.get('/', (req, res) => {
    res.send('Home page. ' + req.startTime);
});

app.get('/user', (req, res) => {
    res.send('User page. ' + req.startTime);
});

app.listen(80, () => {
    console.log('http://127.0.0.1');
});
```

Apifox 测试：

[![image-20221214215933674](https://github.com/JERRY-Z-J-R/I-love-you-3-thousand/raw/master/%E6%88%91%E7%88%B1%E4%BD%A0%EF%BC%8C%E4%B8%8D%E6%AD%A2%E4%B8%89%E5%8D%83%E9%81%8D/Node/06-express/mark-img/image-20221214215933674.png)](https://github.com/JERRY-Z-J-R/I-love-you-3-thousand/blob/master/我爱你，不止三千遍/Node/06-express/mark-img/image-20221214215933674.png)

### 3.2.5 定义<font color='red'>多个</font>全局中间件

可以使用 `app.use()` <font color='gree'>连续定义多个</font>全局中间件。客户端请求到达服务器之后，会按照中间件<font color='gree'>**定义的先后顺序**</font>依次进行调用，示例代码如下：

```js
// 第一个全局中间件
app.use(function (req, res, next) {
    console.log('调用了第1个全局中间件');
    next();
});

// 第2个全局中间件
app.use(function (req, res, next) {
    console.log('调用了第2个全局中间件');
    next();
});

// 请求这个路由，会依次触发上述两个全局中间件，然后再触发这个路由 
app.get('/user', (req, res) => {
    res.send('Home page.');
});
```

### 3.2.6 <font color='red'>局部生效</font>的中间件

<font color='red'>不使用</font><font color='gree'> `app.use()` </font>定义的中间件，叫做<font color='gree'>局部生效的中间件</font>，示例代码如下：

```js
// 定义中间件函数 mw1
const mw1 = function (req, res, next) {
    console.log('这是中间件函数');
    next();
};

// mw1 这个中间件只在该路由中生效，这种用法属于“局部生效的中间件”
app.get('/', mw1, function (req, res) {
    res.send('Home page.');
});

// mw1 这个中间件不会影响下面这个路由
app.get('/user', function (req, res) {
    res.send('User page.');
});
```

代码示例：

```js
const express = require('express');

const app = express();

// 定义中间件函数 mw1
const mw1 = function (req, res, next) {
    console.log('这是中间件函数');
    next();
};

// mw1 这个中间件只在该路由中生效，这种用法属于“局部生效的中间件”
app.get('/', mw1, function (req, res) {
    res.send('Home page.');
});

// mw1 这个中间件不会影响下面这个路由
app.get('/user', function (req, res) {
    res.send('User page.');
});

app.listen(80, () => {
    console.log('http://127.0.0.1');
});
```

Apifox 测试：

[![image-20221215094108340](https://github.com/JERRY-Z-J-R/I-love-you-3-thousand/raw/master/%E6%88%91%E7%88%B1%E4%BD%A0%EF%BC%8C%E4%B8%8D%E6%AD%A2%E4%B8%89%E5%8D%83%E9%81%8D/Node/06-express/mark-img/image-20221215094108340.png)](https://github.com/JERRY-Z-J-R/I-love-you-3-thousand/blob/master/我爱你，不止三千遍/Node/06-express/mark-img/image-20221215094108340.png)

[![image-20221215094137553](https://github.com/JERRY-Z-J-R/I-love-you-3-thousand/raw/master/%E6%88%91%E7%88%B1%E4%BD%A0%EF%BC%8C%E4%B8%8D%E6%AD%A2%E4%B8%89%E5%8D%83%E9%81%8D/Node/06-express/mark-img/image-20221215094137553.png)](https://github.com/JERRY-Z-J-R/I-love-you-3-thousand/blob/master/我爱你，不止三千遍/Node/06-express/mark-img/image-20221215094137553.png)

### 3.2.7 定义<font color='red'>多个</font>局部中间件

可以在路由中，通过如下两种<font color='gree'>等价</font>的方式，<font color='gree'>使用多个局部中间件</font>，他们按照定义的先后顺序执行：

```js
// 以下两种写法是“完全等价”的，可根据自己的喜好，选择任意一种方式进行使用
app.get('/', mw1, mw2, (req, res) => {
    res.send('Home page.');
});

=====
    
app.get('/', [mw1, mw2], (req, res) => {
    res.send('Home page.');
});
```

### 3.2.8 了解中间件的<font color='red'> 5个使用注意事项 </font>

1. **一定要在<font color='red'>路由之前</font>注册中间件！**
2. 客户端发送过来的请求，<font color='gree'>可以连续调用多个</font>中间件进行处理
3. 执行完中间件的业务代码之后，<font color='gree'>不要忘记调用 next() 函数</font>
4. 为了<font color='gree'>防止代码逻辑混乱</font>，调用 next() 函数后不要再写额外的代码
5. 连续调用多个中间件时，多个中间件之间，<font color='red'>共享</font> req 和 res 对象

## 3.3 中间件的分类

为了方便大家<font color='red'>理解</font>和<font color='red'>记忆</font>中间件的使用，Express 官方把<font color='red'>常见的中间件用法</font>，分成了<font color='red'> 5 大类</font>，分别是：

- <font color='red'>应用级别</font>的中间件
- <font color='red'>路由级别</font>的中间件
- <font color='red'>错误级别</font>的中间件
- <font color='red'>Express 内置</font>的中间件
- <font color='red'>第三方</font>的中间件

### 3.3.1 <font color='red'>应用级别</font>的中间件

> 就是一种叫法

通过<font color='gree'> `app.use()` 或 `app.get()` 或 `app.post()`，绑定到 app 实例上的中间件</font>，都叫做应用级别的中间件，代码示例如下：

```js
// 应用级别的中间件    （全局中间件）
app.use((req, res, next) => {
    // ...
    next();
});

// 应用级别的中间件    （局部中间件）
app.get('/', mw, (req, res) => {
    res.send('Home page.');
});
```

### 3.3.2 <font color='red'>路由级别</font>的中间件

绑定到<font color='gree'> `express.Router()` </font>实例上的中间件，叫做路由级别的中间件。它的用法和应用级别中间件没有任何区别。

只不过，<font color='gree'>应用级别中间件是绑定到 app 实例上，路由级别中间件绑定到 router 实例上</font>，代码示例如下：

```js
var app = express();
var router = express.Router();

// 路由级别的中间件
router.use(function (req, res, next) {
    // ...
    next();
});

app.use('/', router);
```

### 3.3.3 <font color='red'>错误级别</font>的中间件

错误级别中间件的<font color='red'>作用</font>：专门用来<font color='red'>捕获</font>整个项目中发生的异常错误，从而防止项目异常崩溃的问题。

<font color='red'>格式</font>：错误级别中间件的 function 处理函数中，<font color='gree'>必须有 4 个形参</font>，形参顺序从前到后，<font color='gree'>分别是 `err` 、`req`、 `res`、`next`</font>。

> 多一个 `err`

```js
app.get('/', function (req, res) {				// 路由
    throw new Error('服务器内部发生了错误！');		 // 人为抛出一个自定义的错误  
    res.send('Home Page.');						
});

app.use(function (err, req, res, next) {		// 错误级别的中间件，捕获错误
    console.log('发生了错误：' + err.message);	// 在服务器打印错误消息
    res.send('Error!' + err.message);			// 向客户端响应错误相关的内容
});
```

> <font color='gree'>**注意：错误级别的中间件，必须注册在所有路由之后！同时，即便没有 next()，错误级别的中间件也会自动捕捉到错误后立马生效！**</font>

若没有错误中间件：（崩溃了）

![](C:\Users\shizeyu\Desktop\notes\Ajax-vue\Snipaste_2023-04-10_15-30-11.png)

有错误中间件：

![](C:\Users\shizeyu\Desktop\notes\Ajax-vue\Snipaste_2023-04-10_15-31-11.png)

[![image-20221215101926536](https://github.com/JERRY-Z-J-R/I-love-you-3-thousand/raw/master/%E6%88%91%E7%88%B1%E4%BD%A0%EF%BC%8C%E4%B8%8D%E6%AD%A2%E4%B8%89%E5%8D%83%E9%81%8D/Node/06-express/mark-img/image-20221215101926536.png)](https://github.com/JERRY-Z-J-R/I-love-you-3-thousand/blob/master/我爱你，不止三千遍/Node/06-express/mark-img/image-20221215101926536.png)

### 3.3.4 <font color='red'>Express内置</font>的中间件

自 Express 4.16.0 版本开始，Express 内置了<font color='red'> 3 个</font>常用的中间件，极大的提高了 Express 项目的开发效率和体验：

1. <font color='red'>`express.static` </font>快速托管静态资源的内置中间件，例如：HTML 文件、图片、CSS 样式等（无兼容性）
2. <font color='red'>`express.json` </font>解析 JSON 格式的请求体数据（<font color='gree'>有兼容性</font>，仅在 4.16.0+ 版本中可用）
3. <font color='red'>`express.urlencoded` </font>解析 URL-encoded 格式的请求体数据（<font color='gree'>有兼容性</font>，仅在 4.16.0+ 版本中可用）

> 2和3也可以同时使用，会自动解析

```js
app.use('/public', express.static('public'))

// 配置解析 application/json 格式数据的内置中间件
app.use(express.json());
// 配置解析 application/x-www-form-urlencoded 格式数据的内置中间件
app.use(express.urlencoded({ extended: false }));
```

json 示例代码：

```js
const express = require('express');

const app = express();

// 注意：除了错误级别的中间件，其他的中间件，必须在路由之前进行配置
// 通过 express.json() 这个中间件，解析表单中的 JSON 格式的数据
app.use(express.json());

app.post('/user', (req, res) => {
    // 在服务器，可以使用 req.body 这个属性，来接受客服端发送过来的请求体数据
    // 默认情况下，如果不配置解析表单数据的中间件，则 req.body 默认为 undefined
    console.log(req.body);
    res.send('ok');
});

app.listen(80, () => {
    console.log('http://127.0.0.1');
});
```

Apifox 测试：

若没有定义中间件

![](C:\Users\shizeyu\Desktop\notes\Ajax-vue\Snipaste_2023-04-10_15-49-39.png)

![](C:\Users\shizeyu\Desktop\notes\Ajax-vue\Snipaste_2023-04-10_15-49-44.png)

否则：

![](C:\Users\shizeyu\Desktop\notes\Ajax-vue\Snipaste_2023-04-10_15-51-26.png)

[![image-20221215103931835](https://github.com/JERRY-Z-J-R/I-love-you-3-thousand/raw/master/%E6%88%91%E7%88%B1%E4%BD%A0%EF%BC%8C%E4%B8%8D%E6%AD%A2%E4%B8%89%E5%8D%83%E9%81%8D/Node/06-express/mark-img/image-20221215103931835.png)](https://github.com/JERRY-Z-J-R/I-love-you-3-thousand/blob/master/我爱你，不止三千遍/Node/06-express/mark-img/image-20221215103931835.png)

urlencoded 示例代码：

```js
const express = require('express');

const app = express();

// 注意：除了错误级别的中间件，其他的中间件，必须在路由之前进行配置
// 通过 express.urlencoded() 这个中间件，解析表单中的 x-www-form-urlencoded 格式的数据
app.use(express.urlencoded({ extended: false }));

app.post('/book', (req, res) => {
    // 在服务器，可以使用 req.body 这个属性，来接受客服端发送过来的请求体数据
    // 默认情况下，如果不配置解析表单数据的中间件，则 req.body 默认为 undefined
    console.log(req.body);
    res.send('ok');
});

app.listen(80, () => {
    console.log('http://127.0.0.1');
});
```

Apifox 测试：

[![image-20221215104727270](https://github.com/JERRY-Z-J-R/I-love-you-3-thousand/raw/master/%E6%88%91%E7%88%B1%E4%BD%A0%EF%BC%8C%E4%B8%8D%E6%AD%A2%E4%B8%89%E5%8D%83%E9%81%8D/Node/06-express/mark-img/image-20221215104727270.png)](https://github.com/JERRY-Z-J-R/I-love-you-3-thousand/blob/master/我爱你，不止三千遍/Node/06-express/mark-img/image-20221215104727270.png)

### 3.3.5 <font color='red'>第三方</font>的中间件

非 Express 官方内置的，而是由第三方开发出来的中间件，叫做第三方中间件。在项目中，大家可以<font color='red'>按需下载</font>并<font color='red'>配置</font>第三方中间件，从而提高项目的开发效率。

例如：在 express@4.16.0 之前的版本中，经常使用 body-parser 这个第三方中间件，来解析请求体数据。使用步骤如下：

- 运行 <font color='red'>`npm install body-parser` </font>安装中间件
- 使用 <font color='red'>`require`</font> 导入中间件
- 调用 <font color='red'>`app.use()`</font> 注册并使用中间件

<font color='red'>注意</font>：Express 内置的 express.urlencoded 中间件，就是基于 body-parser 这个第三方中间件进一步封装出来的。所以现在不用了

示例代码：

```js
const express = require('express');

const app = express();

// 导入解析表单数据的中间件 body-parser
const parser = require('body-parser');
// 使用 app.use() 注册中间件
app.use(parser.json());
app.use(parser.urlencoded({ extended: false }));

app.post('/book', (req, res) => {
    // 在服务器，可以使用 req.body 这个属性，来接受客服端发送过来的请求体数据
    // 默认情况下，如果不配置解析表单数据的中间件，则 req.body 默认为 undefined
    console.log(req.body);
    res.send('ok');
});

app.listen(80, () => {
    console.log('http://127.0.0.1');
});
```

Apifox 测试：

[![image-20221215105806336](https://github.com/JERRY-Z-J-R/I-love-you-3-thousand/raw/master/%E6%88%91%E7%88%B1%E4%BD%A0%EF%BC%8C%E4%B8%8D%E6%AD%A2%E4%B8%89%E5%8D%83%E9%81%8D/Node/06-express/mark-img/image-20221215105806336.png)](https://github.com/JERRY-Z-J-R/I-love-you-3-thousand/blob/master/我爱你，不止三千遍/Node/06-express/mark-img/image-20221215105806336.png)

[![image-20221215105821572](https://github.com/JERRY-Z-J-R/I-love-you-3-thousand/raw/master/%E6%88%91%E7%88%B1%E4%BD%A0%EF%BC%8C%E4%B8%8D%E6%AD%A2%E4%B8%89%E5%8D%83%E9%81%8D/Node/06-express/mark-img/image-20221215105821572.png)](https://github.com/JERRY-Z-J-R/I-love-you-3-thousand/blob/master/我爱你，不止三千遍/Node/06-express/mark-img/image-20221215105821572.png)

## 3.4 自定义中间件

### 3.4.1 <font color='red'>需求描述</font>与<font color='red'>实现步骤</font>

自己<font color='red'>手动模拟</font>一个类似于 express.urlencoded 这样的中间件，来<font color='gree'>解析 POST 提交到服务器的表单数据</font>。

实现步骤：

- 定义中间件
- 监听 req 的 data 事件
- 监听 req 的 end 事件
- 使用 querystring 模块解析请求体数据
- 将解析出来的数据对象挂载为 req.body
- 将自定义中间件封装为模块

### 3.4.2 定义中间件

使用 `app.use()` 来定义全局生效的中间件，代码如下：

```js
app.use(function (req, res, next) {
    // 中间件的业务逻辑
});
```

### 3.4.3 监听 req 的 <font color='red'>data</font> 事件

在中间件中，需要监听 req 对象的 data 事件，来获取客户端发送到服务器的数据。

如果数据量比较大，无法一次性发送完毕，则客户端会<font color='gree'>把数据切割后，分批发送到服务器</font>。所以 data 事件可能会触发多次，每一次触发 data 事件时，<font color='gree'>获取到数据只是完整数据的一部分</font>，需要手动对接收到的数据进行拼接。

```js
// 定义变量，用来存储客户端发送过来的请求体数据
let str = '';
// 监听 req 对象的 data 事件（客户端发送过来的新的请求体数据）
req.on('data', chunk => {
    // 拼接请求体数据，隐式转换为字符串
    str += chunk;
});
```

### 3.4.4 监听 req 的 <font color='red'>end</font> 事件

当请求体数据<font color='red'>接收完毕</font>之后，会自动触发 req 的 end 事件。

因此，我们可以在 req 的 end 事件中，<font color='gree'>拿到并处理完整的请求体数据</font>。示例代码如下：

```js
// 监听 req 对象的 end 事件（请求体发送完毕后自动触发）
req.on('end', () => {
    // 打印完整的请求体数据
    console.log(str);
    // 把字符串格式的请求体数据，解析成对象格式
    // ...
});
```

### 3.4.5 使用 querystring 模块解析请求体数据

Node.js 内置了一个<font color='red'> querystring </font>模块，<font color='gree'>专门用来处理查询字符串</font>。

通过这个模块提供的<font color='red'> parse() </font>函数，可以轻松把查询字符串，解析成对象的格式。示例代码如下：

```js
// 导入处理 querystring 的 Node.js 内置模块
const qs = require('querystring');

// 调用 qs.parse() 方法，把查询字符串解析为对象
const body = qs.parse(str);
```

### 3.4.6 将解析出来的数据对象挂载为 <font color='red'>req.body</font>

<font color='red'>上游</font>的<font color='gree'>中间件</font>和<font color='red'>下游</font>的<font color='gree'>中间件及路由</font>之间，<font color='gree'>**共享同一份** **req** **和** **res**</font>。因此，我们可以将解析出来的数据，挂载为 req 的自定义属性，命名为<font color='red'> req.body</font>，供下游使用。示例代码如下：

```js
req.on('end', () => {
    const body = qs.parse(str);	// 调用 qs.parse() 方法，把查询字符串解析为对象
    req.body = body;			// 将解析出来的请求体对象，挂载为 req.body 属性
    next();						// 最后，一定要调用 next() 函数，执行后续的业务逻辑
});
```

### 3.4.7 将自定义中间件<font color='red'>封装</font>为模块

为了优化代码的结构，我们可以把自定义的中间件函数，<font color='red'>封装为独立的模块</font>，示例代码如下：

```js
// 新建文件custom-body-parser.js 模块中的代码
const qs = require('querystring');
function bodyParser(req, res, next) {
    // 定义变量，用来存储客户端发送过来的请求体数据
	let str = '';
	// 监听 req 对象的 data 事件（客户端发送过来的新的请求体数据）
	req.on('data', chunk => {
    	// 拼接请求体数据，隐式转换为字符串
    	str += chunk;
	});
    
    // 监听 req 对象的 end 事件（请求体发送完毕后自动触发）
	req.on('end', () => {
    	const body = qs.parse(str);	// 调用 qs.parse() 方法，把查询字符串解析为对象
    	req.body = body;			// 将解析出来的请求体对象，挂载为 req.body 属性
    	next();						// 最后，一定要调用 next() 函数，执行后续的业务逻辑
	});
}
module.exports = bodyParser;	// 向外导出解析请求体数据的中间件函数

// -------------------------------------------------------------

// 导入自定义的中间件模块
const myBodyParser = require('custom-body-parser');
// 注册自定义的中间件模块
app.use(myBodyParser);
```

------

代码示例：

```js
// custom-body-parser.js

// 导入 Node.js 内置的 querystring 模块
const qs = require('querystring');

const bodyParser = (req, res, next) => {
    // 定义中间件具体的业务逻辑
    // 定义一个 str 字符串，专门用来存储客户端发送过来的请求体数据
    let str = '';
    // 监听 req 的 data 事件
    req.on('data', (chunk) => {
        str += chunk;
    });
    // 监听 req 的 end 事件
    req.on('end', () => {
        // 在 str 中存放的是完整的请求体数据
        // console.log(str)
        // 把字符串格式的请求体数据，解析成对象格式
        const body = qs.parse(str);
        req.body = body;
        next();
    });
};

// 导出模块
module.exports = bodyParser;
// webtest.js

// 导入 express 模块
const express = require('express');
// 创建 express 的服务器实例
const app = express();

// 导入自己封装的中间件模块
const customBodyParser = require('./custom-body-parser');
// 将自定义的中间件函数，注册为全局可用的中间件
app.use(customBodyParser);

app.post('/book', (req, res) => {
    res.send(req.body);
});

// 调用 app.listen 方法，指定端口号并启动 Web 服务器
app.listen(80, function () {
    console.log('Express server running at http://127.0.0.1');
});
```

Apifox 测试：

[![image-20221215112953903](https://github.com/JERRY-Z-J-R/I-love-you-3-thousand/raw/master/%E6%88%91%E7%88%B1%E4%BD%A0%EF%BC%8C%E4%B8%8D%E6%AD%A2%E4%B8%89%E5%8D%83%E9%81%8D/Node/06-express/mark-img/image-20221215112953903.png)](https://github.com/JERRY-Z-J-R/I-love-you-3-thousand/blob/master/我爱你，不止三千遍/Node/06-express/mark-img/image-20221215112953903.png)

# 四、Express编写接口

## 4.1 创建基本的服务器

```js
// 导入 express 模块
const express = require('express');
// 创建 express 的服务器实例
const app = express();

// write your code here...

// 调用 app.listen 方法，指定端口号并启动 web 服务器
app.listen(80, function () {
    console.log('Express server running at http://127.0.0.1');
});
```

## 4.2 创建API路由模块

```js
// apiRouter.js【路由模块】
const express = require('express');
const apiRouter = express.Router();

// bind your router here...

module.exports = apiRouter;

// ------------------------------------------

// app.js【导入并注册路由模块】
const apiRouter = require('./apiRouter.js');
// 把路由模块，注册到 app 上
app.use('/api', apiRouter);
```

## 4.3 编写GET接口

```js
apiRouter.get('/get', (req, res) => {
    // 获取到客户端通过查询字符串，发送到服务器的数据
    const query = req.query;
    // 调用 res.send() 方法，把数据响应给客户端
    res.send({
        status: 0,				// 状态：0 表示成功，1 表示失败
        msg: 'GET请求成功！',	 // 状态描述
        data: query				// 需要响应给客户端的具体数据
    });
});
```

## 4.4 编写POST接口

```js
apiRouter.post('/post', (req, res) => {
    // 获取客户端通过请求体，发送到服务器的 URL-encoded 数据
    const body = req.body;
    // 调用 res.send() 方法，把数据响应给客户端
    res.send({
        status: 0,				// 状态：0 表示成功，1 表示失败
        msg: 'POST请求成功！',	 // 状态描述消息
        data: body				// 需要响应给客户端的具体数据
    });
});
```

注意：如果要获取<font color='red'> URL-encoded 格式</font>的请求体数据，必须配置中间件 `app.use(express.urlencoded({ extended: false }))`，JSON 格式数据，同理。

------

代码示例：

```js
// apiRouter.js

const express = require('express');
const router = express.Router();

// 在这里挂载对应的路由
router.get('/get', (req, res) => {
  // 通过 req.query 获取客户端通过查询字符串，发送到服务器的数据
  const query = req.query;
  // 调用 res.send() 方法，向客户端响应处理的结果
  res.send({
    status: 0,				   // 0 表示处理成功，1 表示处理失败
    msg: 'GET 请求成功！',		// 状态的描述
    data: query                // 需要响应给客户端的数据
  });
});

// 定义 POST 接口
router.post('/post', (req, res) => {
  // 通过 req.body 获取请求体中包含的 url-encoded 格式的数据
  const body = req.body;
  // 调用 res.send() 方法，向客户端响应结果
  res.send({
    status: 0,
    msg: 'POST 请求成功！',
    data: body
  });
});

module.exports = router;
// webtest.js

// 导入 express
const express = require('express');
// 创建服务器实例
const app = express();

// 配置解析表单数据的中间件
// 注册解析表单数据的中间件，必须放在注册路由模块前，否则就不生效了
// 获取 URL-encoded 格式的请求体数据
app.use(express.urlencoded({ extended: false }));

// 导入 apiRouter 模块
const apiRouter = require('./router/apiRouter');
// 把路由模块，注册到 app 上
app.use('/api', apiRouter);

// 启动服务器
app.listen(80, () => {
    console.log('express server running at http://127.0.0.1');
});
```

Apifox 测试：

[![image-20221215125657999](https://github.com/JERRY-Z-J-R/I-love-you-3-thousand/raw/master/%E6%88%91%E7%88%B1%E4%BD%A0%EF%BC%8C%E4%B8%8D%E6%AD%A2%E4%B8%89%E5%8D%83%E9%81%8D/Node/06-express/mark-img/image-20221215125657999.png)](https://github.com/JERRY-Z-J-R/I-love-you-3-thousand/blob/master/我爱你，不止三千遍/Node/06-express/mark-img/image-20221215125657999.png)

[![image-20221215125729240](https://github.com/JERRY-Z-J-R/I-love-you-3-thousand/raw/master/%E6%88%91%E7%88%B1%E4%BD%A0%EF%BC%8C%E4%B8%8D%E6%AD%A2%E4%B8%89%E5%8D%83%E9%81%8D/Node/06-express/mark-img/image-20221215125729240.png)](https://github.com/JERRY-Z-J-R/I-love-you-3-thousand/blob/master/我爱你，不止三千遍/Node/06-express/mark-img/image-20221215125729240.png)

## 4.5 CORS跨域资源共享

> ## 什么是跨域？
>
> ## 一、为什么会出现[跨域](https://so.csdn.net/so/search?spm=1001.2014.3001.4498&q=跨域&t=&u=)问题
>
> 出于浏览器的同源策略限制。同源策略（Sameoriginpolicy）是一种约定，它是浏览器最核心也最基本的安全功能，如果缺少了同源策略，则浏览器的正常功能可能都会受到影响。可以说Web是构建在同源策略基础之上的，浏览器只是针对同源策略的一种实现。同源策略会阻止一个域的。javascript脚本和另外一个域的内容进行交互。所谓同源（即指在同一个域）就是两个页面具有相同的协议（protocol），主机（host）和端口号（port。
>
> ### 二、什么是跨域
>
> 1.当一个请求url的**[协议、域名、端口](https://so.csdn.net/so/search?spm=1001.2014.3001.4498&q=协议、域名、端口&t=&u=)**三者之间任意一个与当前页面url不同即为跨域。
>
> ![img](https://img-blog.csdnimg.cn/70e9de32598a4783acfafbf082ff3039.png)

### 4.5.1 接口的跨域问题

```html
<!DOCTYPE html>
<html lang="en">

<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>Document</title>
  <script src="https://cdn.staticfile.org/jquery/3.4.1/jquery.min.js"></script>
</head>

<body>
  <button id="btnGET">GET</button>
  <button id="btnPOST">POST</button>

  <script>
    $(function () {
      // 测试 GET 接口
      $('#btnGET').on('click', function () {
        $.ajax({
          type: 'GET',
          url: 'http://127.0.0.1/api/get',
          data: { bookname: '三国演义', author: '罗贯中' },
          success: function (res) {
            console.log(res);
          },
        });
      });

      // 测试 POST 接口
      $('#btnPOST').on('click', function () {
        $.ajax({
          type: 'POST',
          url: 'http://127.0.0.1/api/post',
          data: { bookname: '三国演义', author: '罗贯中' },
          success: function (res) {
            console.log(res);
          },
        });
      });

    });
  </script>
</body>

</html>
```

浏览器测试：

[![image-20221215130826990](https://github.com/JERRY-Z-J-R/I-love-you-3-thousand/raw/master/%E6%88%91%E7%88%B1%E4%BD%A0%EF%BC%8C%E4%B8%8D%E6%AD%A2%E4%B8%89%E5%8D%83%E9%81%8D/Node/06-express/mark-img/image-20221215130826990.png)](https://github.com/JERRY-Z-J-R/I-love-you-3-thousand/blob/master/我爱你，不止三千遍/Node/06-express/mark-img/image-20221215130826990.png)

刚才编写的 GET 和 POST 接口，存在一个很严重的问题：<font color='gree'>不支持跨域请求</font>。

> 因为，HTML 所打开的链接为：http://127.0.0.1:5500/index.html，而请求的 API 为 http://127.0.0.1/api/get 及 http://127.0.0.1/api/post，我们知道，只要 **协议、域名、端口号** 有一个不同（此处端口号不同），那么就属于跨域，浏览器就会默认阻止这种请求（丢弃响应数据，并报错）！

解决接口跨域问题的方案主要有两种：

- <font color='red'>CORS</font>（主流的解决方案，<font color='gree'>推荐使用</font>）
- <font color='red'>JSONP</font>（有缺陷的解决方案：只支持 GET 请求）

> 注意：之前我们之所以没有遇到跨域问题，是因为 Apifox 是基于服务器而不是浏览器发送请求的，而服务器与服务器直接是不存在跨域的！

### 4.5.2 使用<font color='red'> cors 中间件</font>解决跨域问题

cors 是 Express 的一个第三方中间件。通过安装和配置 cors 中间件，可以很方便地解决跨域问题。

使用步骤分为如下 3 步：

- 运行<font color='gree'> `npm install cors` 安装中间件</font>
- 使用<font color='gree'> `const cors = require('cors')` 导入中间件</font>
- 在路由之前调用<font color='gree'> `app.use(cors())` 配置中间件</font>

示例代码：

```js
// 导入 express
const express = require('express');
// 创建服务器实例
const app = express();

// 配置解析表单数据的中间件
// 注册解析表单数据的中间件，必须放在注册路由模块前，否则就不生效了
app.use(express.urlencoded({ extended: false }));

// 一定要在路由之前，配置 cors 这个中间件，从而解决跨域的问题
const cors = require('cors');
app.use(cors());

// 导入 apiRouter 模块
const apiRouter = require('./router/apiRouter');
// 把路由模块，注册到 app 上
app.use('/api', apiRouter);

// 启动服务器
app.listen(80, () => {
    console.log('express server running at http://127.0.0.1');
});
```

浏览器测试：

[![image-20221215135307441](https://github.com/JERRY-Z-J-R/I-love-you-3-thousand/raw/master/%E6%88%91%E7%88%B1%E4%BD%A0%EF%BC%8C%E4%B8%8D%E6%AD%A2%E4%B8%89%E5%8D%83%E9%81%8D/Node/06-express/mark-img/image-20221215135307441.png)](https://github.com/JERRY-Z-J-R/I-love-you-3-thousand/blob/master/我爱你，不止三千遍/Node/06-express/mark-img/image-20221215135307441.png)

### 4.5.3 什么是CORS

CORS （Cross-Origin Resource Sharing，跨域资源共享）由一系列<font color='red'> HTTP 响应头</font>组成，<font color='gree'>这些 HTTP 响应头决定浏览器是否阻止前端 JS 代码跨域获取资源</font>。

浏览器的<font color='gree'>同源安全策略</font>默认会阻止网页“跨域”获取资源。但如果接口服务器<font color='gree'>配置了 CORS 相关的 HTTP 响应头</font>，就可以<font color='gree'>解除浏览器端的跨域访问限制</font>。

![](C:\Users\shizeyu\Desktop\notes\Ajax-vue\Snipaste_2023-06-07_11-04-22.png)

### 4.5.4 CORS的注意事项

- CORS 主要在<font color='gree'>服务器端</font>进行配置。客户端浏览器<font color='gree'>无须做任何额外的配置</font>，即可请求开启了 CORS 的接口。
- CORS 在浏览器中有<font color='gree'>兼容性</font>。只有支持 XMLHttpRequest Level2 的浏览器，才能正常访问开启了 CORS 的服务端接口（例如：IE10+、Chrome4+、FireFox3.5+）。

### 4.5.5 CORS响应头部Access-Control-Allow-<font color='red'>Origin</font>

响应头部中可以携带一个 **Access-Control-Allow-Origin** 字段，其语法如下:

```apl
Access-Control-Allow-Origin: <origin> | *
```

其中，origin 参数的值指定了<font color='gree'>允许访问该资源的外域 URL</font>。

例如，下面的字段值将<font color='gree'>只允许</font>来自 [http://127.0.0.1:5500](http://127.0.0.1:5500/) 的请求：

```
res.setHeader('Access-Control-Allow-Origin', 'http://127.0.0.1:5500');
```

如果指定了 Access-Control-Allow-Origin 字段的值为<font color='gree'>通配符 `*`</font>，表示允许来自任何域的请求，示例代码如下：

```
res.setHeader('Access-Control-Allow-Origin', '*');
```

### 4.5.6 CORS响应头部Access-Control-Allow-<font color='red'>Headers</font>

默认情况下，CORS <font color='red'>仅</font>支持<font color='gree'>客户端向服务器</font>发送如下的 9 个<font color='red'>请求头</font>：

Accept、Accept-Language、Content-Language、DPR、Downlink、Save-Data、Viewport-Width、Width 、Content-Type （值仅限于 text/plain、multipart/form-data、application/x-www-form-urlencoded 三者之一）

如果客户端向服务器发送了<font color='gree'>额外的请求头信息</font>，则需要在<font color='gree'>服务器端</font>，通过 Access-Control-Allow-Headers <font color='gree'>对额外的请求头进行声明</font>，否则这次请求会失败！

```js
// 允许客户端向服务器发送额外的 Content-Type 请求头和 X-Custom-Header 请求头
// 注意：多个请求头之间使用英文的逗号进行分割
res.setHeader('Access-Control-Allow-Headers', 'Content-Type, X-Custom-header');
```

### 4.5.7 CORS响应头部Access-Control-Allow-Methods

默认情况下，CORS 仅支持客户端发起 GET、POST、HEAD 请求。

如果客户端希望通过<font color='gree'> PUT、DELETE </font>等方式请求服务器的资源，则需要在服务器端，通过 Access-Control-Alow-Methods 来<font color='gree'>指明实际请求所允许使用的 HTTP 方法</font>。

示例代码如下：

```js
// 只允许 POST、GET、DELETE、HEAD 请求方法
res.setHeader('Access-Control-Alow-Methods', 'POST, GET, DELETE, HEAD');
// 允许所有的 HTTP 请求方法
res.setHeader('Access-Control-Alow-Methods', '*');
```

### 4.5.8 CORS请求的分类

客户端在请求 CORS 接口时，根据<font color='gree'>请求方式</font>和<font color='gree'>请求头</font>的不同，可以将 CORS 的请求分为<font color='gree'>两大类</font>，分别是：

- <font color='gree'>简单请求</font>
- <font color='gree'>预检请求</font>

### 4.5.9 <font color='red'>简单请求</font>

同时满足以下两大条件的请求，就属于简单请求：

- <font color='gree'>请求方式</font>：GET、POST、HEAD 三者之一
- <font color='gree'>HTTP 头部信息</font>不超过以下几种字段：<font color='gree'>无自定义头部字段</font>、Accept、Accept-Language、Content-Language、DPR、Downlink、Save-Data、Viewport-Width、Width 、Content-Type（只限这三个值 application/x-www-form-urlencoded、multipart/form-data、text/plain）

### 4.5.10 <font color='red'>预检请求</font>

只要符合以下任何一个条件的请求，都需要进行预检请求：

- 请求方式为<font color='gree'> GET、POST、HEAD 之外的请求 Method 类型</font>
- 请求头中<font color='gree'>包含自定义头部字段</font>
- 向服务器发送了<font color='gree'> application/json 格式的数据</font>

在浏览器与服务器正式通信之前，浏览器<font color='gree'>会先发送 OPTION 请求进行预检，以获知服务器是否允许该实际请求</font>，所以这一次的 OPTION 请求称为 “预检请求”。<font color='gree'>服务器成功响应预检请求后，才会发送真正的请求，并且携带真实数据</font>。

所以，如果浏览器向服务器请求的数据为 application/json 格式的，那么要在服务器设置 `res.setHeader('Access-Control-Allow-Headers', 'Content-Type');`，表示可以接收额外的 `Content-Type` 请求头（默认只接收 application/x-www-form-urlencoded、multipart/form-data、text/plain）

### 4.5.11 <font color='red'>简单请求</font>和<font color='red'>预检请求</font>的区别

**<font color='red'>简单请求的特点</font>：**客户端与服务器之间<font color='gree'>只会发生一次请求</font>。

<font color='red'>**预检请求的特点：**</font>客户端与服务器之间会发生两次请求，<font color='gree'>OPTION 预检请求成功之后，才会发起真正的请求</font>。

![](C:\Users\shizeyu\Desktop\notes\Ajax-vue\Snipaste_2023-06-08_16-17-01.png)

## 4.6 JSONP接口（了解）

### 4.6.1 回顾JSONP的<font color='red'>概念</font>与<font color='red'>特点</font>

<font color='red'>概念</font>：浏览器端通过 `<script>` 标签的 `src` 属性，请求服务器上的数据，同时，服务器返回一个函数的调用。这种请求数据的方式叫做 JSONP。

<font color='red'>特点</font>：

- JSONP 不属于真正的 Ajax 请求，因为它没有使用 XMLHttpRequest 这个对象
- <font color='gree'>JSONP 仅支持 GET 请求，不支持 POST、PUT、DELETE 等请求</font>

### 4.6.2 创建JSONP接口的注意事项

如果项目中<font color='gree'>已经配置了 CORS 跨域资源共享</font>，为了**防止冲突**，<font color='gree'>必须在配置 CORS 中间件之前声明 JSONP 的接口</font>。否则 JSONP 接口会被处理成开启了 CORS 的接口。示例代码如下：

```js
// 优先创建 JSONP 接口【这个接口不会被处理成 CORS 接口】这里的/api是因为后买代码路由模块统一注册为了/api，随意这里手动加上
app.get('/api/jsonp', (req, res) => { });

// 再配置 CORS 中间件【后续的所有接口，都会被处理成 CORS 接口】
app.use(cors());

// 这是一个开启了 CORS 的接口
app.get('/api/get', (req, res) => { });
```

### 4.6.3 实现JSONP接口的步骤

1. <font color='gree'>获取</font>客户端发送过来的<font color='gree'>回调函数的名字</font>
2. <font color='gree'>得到要</font>通过 JSONP 形式<font color='gree'>发送给客户端的数据</font>
3. 根据前两步得到的数据，<font color='gree'>拼接出一个函数调用的字符串</font>
4. 把上一步拼接得到的字符串，响应给客户端的 `<script>` 标签进行解析执行

### 4.6.4 实现JSONP接口的具体代码

```js
app.get('/api/jsonp', (req, res) => {
    // 获取客户端发送过来的回调函数的名字
    const funcName = req.query.callback;
    // 得到要通过 JSONP 形式发送给客户端的数据
    const data = { name: 'zjr', age: 22};
    // 根据前两步得到的数据，拼接出一个函数调用的字符串
    const scriptStr = `${funcName}(${JSON.stringify(data)})`;
    // 把上一步拼接得到的字符串，响应给客户端的 <script> 标签进行解析执行
    res.send(scriptStr);
});
```

### 5 在网页中使用 jqury 发起JSONP请求

调用 @ajax() 函数，<font color='gree'>提供 JSONP 的配置选项</font>，从而发起JSONP请求，查看JSONP接口处理，：

```js
$('#btnJSONP').on('click', => {
	$.ajax({
    	method: 'GET',
        url: 'http://127.0.0.1/api/jsonp',
        dataType: 'jsonp', //表示发起jsonp请求
        success: function(res){
    		console.log(res)
		}
	})                  
})
```



# 五、Express中使用async

借助第三方库：[express-async-errors - npm (npmjs.com)](https://www.npmjs.com/package/express-async-errors)

------

[如何在 Express4.x 中愉快地使用 async - 掘金 (juejin.cn)](https://juejin.cn/post/6895888535301062670)

## 【前言】

为了能够更好地处理异步流程，一般开发者会选择 async 语法。

在 express 框架中可以直接利用 async 来声明中间件方法，但是对于该中间件的错误，无法通过错误捕获中间件来劫持到。

## 【错误处理中间件】

```
const express = require('express');
const app = express();
const PORT = process.env.PORT || 3000;

app.get('/', (req, res) => {
    const message = doSomething();
    res.send(message);
});

// 错误处理中间件
app.use(function (err, req, res, next) {
    return res.status(500).send('内部错误！');
});

app.listen(PORT, () => console.log(`app listening on port ${PORT}`));
```



以上述代码为例，中间件方法并没有通过 async 语法来声明，如果 doSomething 方法内部抛出异常，那么就可以在错误处理中间件中捕获到错误，从而进行相应地异常处理。

```
app.get('/', async (req, res) => {
    const message = doSomething();
    res.send(message);
});
```



而采用 async 语法来声明中间件时，一旦 doSomething 内部抛出异常，则错误处理中间件无法捕获到。

> 虽然可以利用 process 监听 unhandledRejection 事件来捕获，但是无法正确地处理后续流程。

## 【try/catch】

对于 async 声明的函数，可以通过 try/catch 来捕获其内部的错误，再使用 next 函数将错误递交给错误处理中间件，即可处理该场景：

```
app.get('/', async (req, res, next) => {
    try {
        const message = doSomething();
        res.send(message);
    } catch(err) {
        next(err);
    }
});
```



> 这种写法简单易懂，但是满屏的 try/catch 语法，对代码结构具有入侵性，会显得非常繁琐且不优雅。

## 【高阶函数】

对于基础扎实的开发来说，都知道 async 函数最终返回一个 Promise 对象，而对于 Promsie 对象应该利用其提供的 catch 方法来捕获异常。

那么在将 async 语法声明的中间件方法传入 use 之前，需要包裹一层 Promise 函数的异常处理逻辑，这时就需要利用高阶函数来完成这样的操作。

```
function asyncUtil(fn) {
    return function asyncUtilWrap(...args) {
        const fnReturn = fn(args);
        const next = args[args.length - 1];
        return Promise.resolve(fnReturn).catch(next);
    }
}

app.use(asyncUtil(async (req, res, next) => {
    const message = doSomething();
    res.send(message);
}));
```



> 相比较第一种方法，**「高阶函数减少了冗余代码，在一定程度上提高了代码的可读性。」**

上述两种方案基于扎实的 JavaScript 基础以及 Express 框架的熟练使用，接下来从源码的角度思考合适的解决方案。

## 【中间件机制】

Express 中主要包含三种中间件：

- 应用级别中间件
- 路由级别中间件
- 错误处理中间件

```
app.use = function use(fn) {
    var path = '/';
    
    // 省略参数处理逻辑...

    // 初始化内置中间件
    this.lazyrouter();
    var router = this._router;

    fns.forEach(function (fn) {
        // non-express app
        if (!fn || !fn.handle || !fn.set) {
            return router.use(path, fn);
        }
        
        // ...
    }, this);
    
    return this;
};
```



应用级别中间件通过 app.use 方法注册，**「其本质上也是调用路由对象上的中间件注册方法，只不过其默认路由为 '/'」**。

```
proto.use = function use(fn) {
    var offset = 0;
    var path = '/';

    // 省略参数处理逻辑...

    var callbacks = flatten(slice.call(arguments, offset));

    for (var i = 0; i < callbacks.length; i++) {
        var fn = callbacks[i];
        
        // ...

        // add the middleware
        debug('use %o %s', path, fn.name || '<anonymous>')

        var layer = new Layer(path, {
            sensitive: this.caseSensitive,
            strict: false,
            end: false
        }, fn);

        layer.route = undefined;

        this.stack.push(layer);
    }

    return this;
};
```



中间件的所有注册方式最终会调用上述代码，根据 path 和中间件处理函数生成 layer 实例，再通过栈来维护这些 layer 实例。

```
// 部分核心代码
proto.handle = function handle(req, res, out) {
    var self = this;
    var idx = 0;
    var stack = self.stack;
    
    next();

    function next(err) {
        var layerError = err === 'route' ? null : err;
    
    if (idx >= stack.length) {
        return;
    }

    var path = getPathname(req);

    // find next matching layer
    var layer;
    var match;
    var route;

        while (match !== true && idx < stack.length) {
            layer = stack[idx++];
            match = matchLayer(layer, path);
            route = layer.route;
        
            if (match !== true) {
                continue;
            }
        }

        // no match
        if (match !== true) {
            return done(layerError);
        }

        // this should be done for the layer
        self.process_params(layer, paramcalled, req, res, function (err) {
            if (err) {
                return next(layerError || err);
            }

            if (route) {
                return layer.handle_request(req, res, next);
            }
            
            trim_prefix(layer, layerError, layerPath, path);
        });
    }
    
    function trim_prefix(layer, layerError, layerPath, path) {
        if (layerError) {
            layer.handle_error(layerError, req, res, next);
        } else {
            layer.handle_request(req, res, next);
        }
    }
};
```



Express 内部通过 handle 方法来处理中间件执行逻辑，其利用**「闭包的特性」**缓存 idx 来记录当前遍历的状态。

该方法内部又实现了 next 方法来匹配当前需要执行的中间件，从遍历的代码可以明白**「中间件注册的顺序是非常重要的」**。

如果该流程存在异常，则调用 layer 实例的 handle.error 方法，这里仍然是**「遵循了 Node.js 错误优先的设计理念」**：

```
Layer.prototype.handle_error = function handle_error(error, req, res, next) {
    var fn = this.handle;
    
    if (fn.length !== 4) {
        // not a standard error handler
        return next(error);
    }

    try {
        fn(error, req, res, next);
    } catch (err) {
        next(err);
    }
};
```



**「内部通过判断函数的形参个数过滤掉非错误处理中间件」**。

如果 next 函数内部没有异常情况，则调用 layer 实例的 handle_request 方法：

```
Layer.prototype.handle_request = function handle(req, res, next) {
    var fn = this.handle;
    
    if (fn.length > 3) {
        // not a standard request handler
        return next();
    }

    try {
        fn(req, res, next);
    } catch (err) {
        next(err);
    }
};
```



**「handle 方法初始化执行了一次 next 方法，但是该方法每次调用最多只能匹配一个中间件」**，所以在执行 handle_error 和 handle_request 方法时，会将 next 方法透传给中间件，这样开发者就可以通过手动调用 next 方法的方式来执行接下来的中间件。

从上述中间件的执行流程中可以知晓，**「用户注册的中间件方法在执行的时候都会包裹一层 try/catch，但是 try/catch 无法捕获 async 函数内部的异常，这也就是为什么 Express 中无法通过注册错误处理中间件来拦截到 async 语法声明的中间件的异常的原因」**。

【修改源码】

找到本质原因之后，可以通过修改源码的方法来进行适配：

```
Layer.prototype.handle_request = function handle(req, res, next) {
    var fn = this.handle;

    if (fn.length > 3) {
        // not a standard request handler
        return next();
    }
    
    // 针对 async 语法函数特殊处理
    if (Object.prototype.toString.call(fn) === '[object AsyncFunction]') {
        return fn(req, res, next).catch(next);
    }

    try {
        fn(req, res, next);
    } catch (err) {
        next(err);
    }
};
```



上述代码在 handle_request 方法内部判断了中间件方法通过 async 语法声明的情况，从而采用 Promise 对象的 catch 方法来向下传递异常。

**「这种方式可以减少上层冗余的代码，但是实现该方式，可能需要 fork 一份 Express4.x 的源码，然后发布一个修改之后的版本，后续还要跟进官方版本的新特性，相应的维护成本非常高。」**

> express5.x 中将 router 部分剥离出了单独的路由库 —— router

【AOP（面向切面编程）】

为了解决上述方案存在的问题，我们可以尝试利用 AOP 技术在不修改源码的基础上对已有方法进行增强。

```
app.use(async function () {
    const message = doSomething();
    res.send(message);
});
```



以注册应用级别中间件为例，可以对 app.use 方法进行 AOP 增强：

```
const originAppUseMethod = app.use.bind(app);
app.use = function (fn) {
    if (Object.prototype.toString.call(fn) === '[object AsyncFunction]') {
        const asyncWrapper = function(req, res, next) {
            fn(req, res, next).then(next).catch(next);
        }
        return originAppUseMethod(asyncWrapper);
    }
    return originAppUseMethod(fn);
}
```



前面源码分析的过程中，app.use 内部是有 this 调用的，所以这里需要**「利用 bind 方法来避免后续调用过程中 this 指向出现问题。」**

然后就是利用 AOP 的核心思想，重写原始的 app.use 方法，通过不同的分支逻辑代理到原始的 app.use 方法上。

**「该方法相比较修改源码的方式，维护成本低。但是缺点也很明显，需要重写所有可以注册中间件的方法，不能够像修改源码那样一步到位。」**

【写在最后】

本文介绍了 Express 中使用 async 语法的四种解决方案：

- try/catch
- 高阶函数
- 修改源码
- AOP

除了 try/catch 方法性价比比较低，其它三种方法都需要根据实际情况去取舍，举个栗子：

如果你需要写一个 Express 中间件提供给各个团队使用，那么修改源码的方式肯定走不通，而 AOP 的方式对于你的风险太大，相比较下，第二种方案是最佳的实践方案。

> 评论区补充：
>
> ```
> npm i express-async-errors
> ```
>
> 
>
> ```
> const express = require('express')
> // 异步异常捕获
> require('express-async-errors');
> 
> // 后续无需任何操作，直接使用异步中间件即可！错误中间件能成功捕获异常
> ```
>
> 
>
> 这个库的实现非常巧妙，结合了高阶函数和AOP！

------

[让 Express 支持 async/await | NiuNiu's Note (liu-xin.me)](https://liu-xin.me/2017/10/07/让Express支持async-await/)

随着 Node.js v8 的发布，Node.js 已原生支持 async/await 函数，Web 框架 Koa 也随之发布了 Koa2 正式版，支持 async/await 中间件，为处理异步回调带来了极大的方便。

既然 Koa2 已经支持 async/await 中间件了，为什么不直接用 Koa，而还要去改造 Express 让其支持 async/await 中间件呢？因为 Koa2 正式版发布才不久，而很多老项目用的都还是 Express，不可能将其推倒用 Koa 重写，这样成本太高，但又想用到新语法带来的便利，那就只能对 Express 进行改造了，而且这种改造必须是对业务无侵入的，不然会带来很多的麻烦。

【直接使用 async/await】

让我们先来看下在 Express 中直接使用 async/await 函数的情况。

```
const express = require('express');
const app = express();
const { promisify } = require('util');
const { readFile } = require('fs');
const readFileAsync = promisify(readFile);
   
app.get('/', async function (req, res, next) {
    const data = await readFileAsync('./package.json');
    res.send(data.toString());
});

// Error Handler
app.use(function (err, req, res, next) {
    console.error('Error:', err);
    res.status(500).send('Service Error');
});
   
app.listen(3000, '127.0.0.1', function () {
    console.log(`Server running at http://${ this.address().address }:${ this.address().port }/`);
});
```



上面是没有对 Express 进行改造，直接使用 async/await 函数来处理请求，当请求 `http://127.0.0.1:3000/` 时，发现请求能正常请求，响应也能正常响应。这样似乎不对 Express 做任何改造也能直接使用 async/await 函数，但如果 async/await 函数里发生了错误呢？这个错误能不能被我们的错误处理中间件处理呢？现在我们去读取一个不存在文件，例如将之前读取的 `package.json` 换成 `age.json`。

```
app.get('/', async function (req, res, next) {
    const data = await readFileAsync('./age.json');
    res.send(data.toString());
});
```



现在我们去请求 `http://127.0.0.1:3000/` 时，发现请求迟迟不能响应，最终会超时。

而在终端报了如下的错误：

[![UnhandlerRejectionError](https://github.com/JERRY-Z-J-R/I-love-you-3-thousand/raw/master/%E6%88%91%E7%88%B1%E4%BD%A0%EF%BC%8C%E4%B8%8D%E6%AD%A2%E4%B8%89%E5%8D%83%E9%81%8D/Node/06-express/mark-img/unhandlererror.png)](https://github.com/JERRY-Z-J-R/I-love-you-3-thousand/blob/master/我爱你，不止三千遍/Node/06-express/mark-img/unhandlererror.png) 发现错误并没有被错误处理中间件处理，而是抛出了一个 `unhandledRejection` 异常，现在如果我们用 try/catch 来手动捕获错误会是什么情况呢？

```
app.get('/', async function (req, res, next) {
    try {
        const data = await readFileAsync('./age.json');
        res.send(datas.toString());
    } catch(e) {
        next(e);
    }
});
```



发现请求被错误处理中间件处理了，说明我们手动显式的来捕获错误是可以的，但是如果在每个中间件或请求处理函数里面加一个 try/catch 也太不优雅了，对业务代码有一定的侵入性，代码也显得难看。所以通过直接使用 async/await 函数的实验，我们发现对 Express 改造的方向就是能够接收 async/await 函数里面抛出的错误，又对业务代码没有侵入性。

【改造 Express】

在 Express 中有两种方式来处理路由和中间件，一种是通过 Express 创建的 app，直接在 app 上添加中间件和处理路由，像下面这样：

```
const express = require('express');
const app = express();
   
app.use(function (req, res, next) {
    next();
});

app.get('/', function (req, res, next) {
    res.send('hello, world');
});

app.post('/', function (req, res, next) {
    res.send('hello, world');
});
   
app.listen(3000, '127.0.0.1', function () {
    console.log(`Server running at http://${ this.address().address }:${ this.address().port }/`);
});
```



另外一种是通过 Express 的 Router 创建的路由实例，直接在路由实例上添加中间件和处理路由，像下面这样：

```
const express = require('express');
const app = express();
const router = express.Router();
app.use(router);
   
router.get('/', function (req, res, next) {
    res.send('hello, world');
});

router.post('/', function (req, res, next) {
    res.send('hello, world');
});
   
app.listen(3000, '127.0.0.1', function () {
    console.log(`Server running at http://${ this.address().address }:${ this.address().port }/`);
});
```



这两种方法可以混合起来用，现在我们思考一下怎样才能让一个形如 `app.get('/', async function(req, res, next){})` 的函数，让里面的 async 函数抛出的错误能被统一处理呢？要让错误被统一的处理当然要调用 `next(err)` 来让错误被传递到错误处理中间件，又由于 async 函数返回的是 Promise，所以肯定是形如这样的 `asyncFn().then().catch(function(err){ next(err) })`，所以按这样改造一下就有如下的代码：

```
app.get = function (...data) {
    const params = [];
    for (let item of data) {
        if (Object.prototype.toString.call(item) !== '[object AsyncFunction]') {
            params.push(item);
            continue;
        }
        const handle = function (...data) {
            const [ req, res, next ] = data;
            item(req, res, next).then(next).catch(next);
        };
        params.push(handle);
    }
    app.get(...params);
}
```



上面的这段代码中，我们判断 `app.get()` 这个函数的参数中，若有 async 函数，就采用 `item(req, res, next).then(next).catch(next);` 来处理，这样就能捕获函数内抛出的错误，并传到错误处理中间件里面去。但是这段代码有一个明显的错误就是最后调用 app.get()，这样就递归了，破坏了 app.get 的功能，也根本处理不了请求，因此还需要继续改造。 我们之前说 Express 两种处理路由和中间件的方式可以混用，那么我们就混用这两种方式来避免递归，代码如下：

```
const express = require('express');
const app = express();
const router = new express.Router();
app.use(router);
    
app.get = function (...data) {
    const params = [];
    for (let item of data) {
        if (Object.prototype.toString.call(item) !== '[object AsyncFunction]') {
            params.push(item);
            continue;
        }
        const handle = function (...data) {
            const [ req, res, next ] = data;
            item(req, res, next).then(next).catch(next);
        };
        params.push(handle);
    }
    router.get(...params);
}
```



像上面这样改造之后似乎一切都能正常工作了，能正常处理请求了。但通过查看 Express 的源码，发现这样破坏了 app.get() 这个方法，因为 app.get() 不仅能用来处理路由，而且还能用来获取应用的配置，在 Express 中对应的源码如下：

```
methods.forEach(function(method) {
    app[method] = function(path) {
        if (method === 'get' && arguments.length === 1) {
            // app.get(setting)
            return this.set(path);
        }
    
        this.lazyrouter();
        
        var route = this._router.route(path);
        route[method].apply(route, slice.call(arguments, 1));
        return this;
    };
});
```



所以在改造时，我们也需要对 app.get 做特殊处理。在实际的应用中我们不仅有 get 请求，还有 post、put 和 delete 等请求，所以我们最终改造的代码如下：

```
const { promisify } = require('util');
const { readFile } = require('fs');
const readFileAsync = promisify(readFile);
const express = require('express');
const app = express();
const router = new express.Router();
const methods = [ 'get', 'post', 'put', 'delete' ];
app.use(router);
    
for (let method of methods) {
    app[method] = function (...data) {
        if (method === 'get' && data.length === 1) return app.set(data[0]);
        const params = [];
        for (let item of data) {
            if (Object.prototype.toString.call(item) !== '[object AsyncFunction]') {
                params.push(item);
                continue;
            }
            const handle = function (...data) {
                const [ req, res, next ] = data;
                item(req, res, next).then(next).catch(next);
            };
            params.push(handle);
        }
        router[method](...params);
    };
}
      
app.get('/', async function (req, res, next) {
    const data = await readFileAsync('./package.json');
    res.send(data.toString());
});
      
app.post('/', async function (req, res, next) {
    const data = await readFileAsync('./age.json');
    res.send(data.toString());
});
    
router.use(function (err, req, res, next) {
    console.error('Error:', err);
    res.status(500).send('Service Error');
}); 
     
app.listen(3000, '127.0.0.1', function () {
    console.log(`Server running at http://${ this.address().address }:${ this.address().port }/`);
});
```



现在就改造完了，我们只需要加一小段代码，就可以直接用 async function 作为 handler 处理请求，对业务也毫无侵入性，抛出的错误也能传递到错误处理中间件。

------

# 【数据库】

## 1.1数据库的概念

自己上网搜

## 1.2常见的数据库及种类

数据库种类：

- <font color='gree'>MySQL数据库（目前使用最广泛、流行度最高的开源免费数据库；Community 社区免费版 + Enterprise 收费版）</font>
- Oracle 数据库（收费）
- SQL Server 数据库（收费）
- Mongodb 数据库（Community + Enterprise）

其中 MySQL数据库、Oracle 数据库、SQL Server 数据库属于<font color='gree'>传统型数据库</font>（又叫做：<font color='gree'>关系型数据库</font>或<font color='gree'> SQL 数据库</font>），这三种理念相同。

而 Mongodb 数据库属于<font color='gree'>新型数据库</font>（又叫做<font color='gree'>非关系型数据库</font>），他一定程度上弥补了SQL的不足。常见两种一同使用。

## 1.3传统型数据库的<font color='red'>数据组织结构</font>

数据的组织结构：指的就是数据以什么样的结构进行存储。

 ![](C:\Users\shizeyu\Desktop\notes\Ajax-vue\Snipaste_2023-06-09_10-16-09.png)

传统型数据库的数据结构架构，与 Excel 中数据的结构结构比较类似。

因此，我没可以对比着 Excel 来了解和学习传统型数据库的数据组织结构。

### 1. Excel 的数据组织结构

每个 Excel 中，数据的组织结构分别为工作簿、工作表、数据行、列这4部分

![](C:\Users\shizeyu\Desktop\notes\Ajax-vue\Snipaste_2023-06-09_10-21-11.png)

### 2. 传统型数据库的数据组织结构

在传统型数据库中，数据的组织结构分为<font color='gree'>数据库(database)、数据表(table)、数据行(row)、字段(field)</font>这4部分组成

1. <font color='red'>数据库</font>类似于 Excel 的<font color='pink'>工作簿</font>
2. <font color='red'>数据表</font>类似于 Excel 的<font color='pink'>工作表</font>
3. <font color='red'>数据行</font>类似于 Excel 的<font color='pink'>每一行数据</font>
4. <font color='red'>字段</font>类似于 Excel 的<font color='pink'>列</font>
5. 每个字段都有对应的数据类型

### 3. 实际开发中库、表、行、字段的关系

1. 在实际项目开发中，一般情况下，每个项目都对应<font color='gree'>独立的数据库</font>
2. 不同的数据，要存储刀数据库的不同表中，例如：用户数据存储到 users 表中，图书数据存储到books表中
3. 每个表中具体存储哪些信息，由字段来决定，例如：我们可以为 users 表设计 id、username、password 这3个字段。
4. 表中的行，表示每一条具体的数据。

------

# 【MySQL】

## 一、了解需要安装哪些MySQL相关软件

对于开发人员来说，只需要安装<font color='gree'>`MySQL Server`</font>和<font color='gree'>`MySQL Workbench`</font>这两个软件，就能满足开发的需要了。

- MySQL Server：<font color='gree'>专门用来提供数据存储和服务的软件</font>
- MySQL Workbench：<font color='gree'>可视化的 MySQL 管理工具</font>，通过他，可以方便的呢操作存储在 MySQL Server 中的数据。

## 二、MySQL 在windows 环境下的安装

在 windows 环境下的安装，只需要运行 <font color='red'>`mysql-installer-community-8.0.19.0.msi`</font>这个安装包，就能一次性把<font color='gree'>`MySQL Server`</font>和<font color='gree'>`MySQL Workbench`</font>都安装上，无需像 Mac 一样分别安装

> 若出现弹窗，是因为windows789系统缺少必要软件
>
> ![](C:\Users\shizeyu\Desktop\notes\Ajax-vue\Snipaste_2023-06-09_15-36-19.png)
>
> ![](C:\Users\shizeyu\Desktop\notes\Ajax-vue\Snipaste_2023-06-09_15-36-38.png)
>
> ![](C:\Users\shizeyu\Desktop\notes\Ajax-vue\Snipaste_2023-06-09_15-41-47.png)
>
> ![](C:\Users\shizeyu\Desktop\notes\Ajax-vue\Snipaste_2023-06-09_15-42-13.png)
>
> ![](C:\Users\shizeyu\Desktop\notes\Ajax-vue\Snipaste_2023-06-09_15-42-28.png)
>
> ![](C:\Users\shizeyu\Desktop\notes\Ajax-vue\Snipaste_2023-06-09_15-45-49.png)
>
>  ![](C:\Users\shizeyu\Desktop\notes\Ajax-vue\Snipaste_2023-06-09_15-47-09.png)
>
> ![](C:\Users\shizeyu\Desktop\notes\Ajax-vue\Snipaste_2023-06-09_15-47-34.png)
>
> ![](C:\Users\shizeyu\Desktop\notes\Ajax-vue\Snipaste_2023-06-09_15-48-35.png)
>
> ![](C:\Users\shizeyu\Desktop\notes\Ajax-vue\Snipaste_2023-06-09_15-49-19.png)
>
> ![](C:\Users\shizeyu\Desktop\notes\Ajax-vue\Snipaste_2023-06-09_15-49-54.png)
>
> ![](C:\Users\shizeyu\Desktop\notes\Ajax-vue\Snipaste_2023-06-09_15-51-59.png)
>
> ![](C:\Users\shizeyu\Desktop\notes\Ajax-vue\Snipaste_2023-06-09_15-52-26.png)
>
> ![](C:\Users\shizeyu\Desktop\notes\Ajax-vue\Snipaste_2023-06-09_15-56-08.png)
>
> ![](C:\Users\shizeyu\Desktop\notes\Ajax-vue\Snipaste_2023-06-09_15-57-18.png)

## 三、 使用 MySQL Workbench 管理数据库

### 3.1 <font color='red'>连接</font>数据库

![](C:\Users\shizeyu\Desktop\notes\Ajax-vue\Snipaste_2023-06-09_17-19-08.png)

### 3.2 了解主界面的<font color='red'>组成部分</font>

![](C:\Users\shizeyu\Desktop\notes\Ajax-vue\Snipaste_2023-06-09_17-23-27.png)

### 3.3 创建数据库

![](C:\Users\shizeyu\Desktop\notes\Ajax-vue\Snipaste_2023-06-09_17-32-26.png)

> 命名，中文和空格非法





------

# 【MySQL模块】

> 原创内容，转载请注明出处！

# 一、在Node.js中操作MySQL

## 1.1 在项目中操作MySQL的步骤

- 安装操作 MySQL 数据库的第三方模块（mysql）
- 通过 mysql 模块连接到 MySQL 数据库
- 通过 mysql 模块执行 SQL 语句

![](C:\Users\shizeyu\Desktop\notes\Ajax-vue\image-20221215145012349.png)

## 1.2 安装与配置mysql模块

### 1.2.1 安装mysql模块

mysql 模块是托管于 npm 上的第三方模块。它提供了在 Node.js 项目中连接和操作 MySQL 数据库的能力。

想要在项目中使用它，需要先运行如下命令，将 mysql 安装为项目的依赖包：

```
npm install mysql
```



### 1.2.2 配置mysql模块

在使用 mysql 模块操作 MySQL 数据库之前，必须先对 mysql 模块进行必要的配置，主要的配置步骤如下：

```
// 导入 mysql 模块
const mysql = require('mysql');
// 建立与 mysql 数据库的连接
const db = mysql.createPool({
    host: '127.0.0.1',		// MySQL IP 地址（Default: localhost）
    port: '3306',           // MySQL 端口号（Default: 3306）
    user: 'root',			// MySQL 账号
    password: '123456',		// 登录数据库的密码
    database: 'my_db_01'	// 目标数据库
});
```



### 1.2.3 测试mysql模块能否正常工作

调用 `db.query()` 函数，指定要执行的 SQL 语句，通过回调函数拿到执行的结果：

```
// 检测 mysql 模块能否正常工作
db.query('SELECT 1', (err, results) => {
    // 判断 err 是否为 null
    if (err) {
        return console.log(err.message);
    }
    // 只要能打印出 [ RowDataPacket { '1':1 } ] 的结果，就证明数据库连接正常
    console.log(results);
});
```



## 1.3 使用mysql模块操作MySQL数据库

### 1.3.1 查询数据

查询 users 表中所有的数据：

```
// 查询 users 表中的所有的用户数据
db.query('SELECT * FROM users', (err, results) => {
    // 查询失败
    if (err) {
        return console.log(err.message);
    }
    // SELECT 查询得到的 results 是一个数组
    // 查询成功
    console.log(results);
});
```



[![image-20221215172223576](https://github.com/JERRY-Z-J-R/I-love-you-3-thousand/raw/master/%E6%88%91%E7%88%B1%E4%BD%A0%EF%BC%8C%E4%B8%8D%E6%AD%A2%E4%B8%89%E5%8D%83%E9%81%8D/Node/07-mysql%E6%A8%A1%E5%9D%97/mark-img/image-20221215172223576.png)](https://github.com/JERRY-Z-J-R/I-love-you-3-thousand/blob/master/我爱你，不止三千遍/Node/07-mysql模块/mark-img/image-20221215172223576.png)

### 1.3.2 插入数据

向 users 表中新增数据， 其中 username 为 Spider-Man，password 为 pcc321。示例代码如下：

```
// 要插入到 users 表中的数据对象
const user = {
    username: 'Spider-Man',
    password: 'pcc321'
};

// 待执行的 SQL 语句，其中英文的 ? 表示占位符
const sqlStr = 'INSERT INTO users (username, password) VALUES (?, ?)';

// 使用数组的形式，依次为 ? 占位符指定具体的值
db.query(sqlStr, [user.username, user.password], (err, results) => {
    if (err) {
        return console.log(err.message);
    }
    // 注意：如果执行的是 INSERT INTO 插入语句，则 results 是一个对象
    // 受到影响的行数 === 1
    if (results.affectedRows === 1) {
        console.log('插入数据成功');
    }
});
```



[![image-20221215180517971](https://github.com/JERRY-Z-J-R/I-love-you-3-thousand/raw/master/%E6%88%91%E7%88%B1%E4%BD%A0%EF%BC%8C%E4%B8%8D%E6%AD%A2%E4%B8%89%E5%8D%83%E9%81%8D/Node/07-mysql%E6%A8%A1%E5%9D%97/mark-img/image-20221215180517971.png)](https://github.com/JERRY-Z-J-R/I-love-you-3-thousand/blob/master/我爱你，不止三千遍/Node/07-mysql模块/mark-img/image-20221215180517971.png)

### 1.3.3 插入数据的便捷方式

向表中新增数据时，如果数据对象的每个属性和数据表的**字段一一对应**，则可以通过如下方式快速插入数据：

```
// 要插入到 users 表中的数据对象
const user = {
    username: 'Super-Man', 
    password: 'pcc123'
};

// 待执行的 SQL 语句，其中英文的 ? 表示占位符
const sqlStr = 'INSERT INTO users SET ?';

// 直接将数据对象当作占位符的值
db.query(sqlStr, user, (err, results) => {
    if (err) {
        return console.log(err.message);
    }
    if (results.affectedRows === 1) {
        console.log('插入数据成功');
    }
});
```



### 1.3.4 更新数据

可以通过如下方式，更新表中的数据：

```
// 要更新的数据对象
const user = {
    id: 7,
    username:'aaa',
    password:'000'
};

// 要执行的 SQL 语句
const sqlStr = 'UPDATE users SET username=?, password=? WHERE id=?';

// 调用 db.query() 执行 SQL 语句的同时，使用数据依次为占位符指定具体的值
db.query(sqlStr, [user.username, user.password, user.id], (err, results) => {
    if (err) {
        return console.log(err.message);
    }
    // results 是一个对象
    if (results.affectedRows === 1) {
        console.log('更新数据成功');
    }
});
```



[![image-20221215182505224](https://github.com/JERRY-Z-J-R/I-love-you-3-thousand/raw/master/%E6%88%91%E7%88%B1%E4%BD%A0%EF%BC%8C%E4%B8%8D%E6%AD%A2%E4%B8%89%E5%8D%83%E9%81%8D/Node/07-mysql%E6%A8%A1%E5%9D%97/mark-img/image-20221215182505224.png)](https://github.com/JERRY-Z-J-R/I-love-you-3-thousand/blob/master/我爱你，不止三千遍/Node/07-mysql模块/mark-img/image-20221215182505224.png)

### 1.3.5 更新数据的便捷方式

```
// 要更新的数据对象
const user = {
    id: 8,
    username: 'aaaa', 
    password: '0000'
};

// 要执行的 SQL 语句
const sqlStr = 'UPDATE users SET ? WHERE id=?';

// 调用 db.query() 执行 SQL 语句的同时，使用数据依次为占位符指定具体的值
db.query(sqlStr, [user, user.id], (err, results) => {
    if (err) {
        console.log(err.message);
    }
    if (results.affectedRows === 1) {
        console.log('更新数据成功');
    }
});
```



### 1.3.6 删除数据

在删除数据时，推荐根据 id 这样的唯一标识，来删除对应的数据。实例如下：

```
// 要执行的 SQL 语句
const sqlStr = 'DELETE FROM users WHERE id=?';

// 调用 db.query() 执行 SQL 语句的同时，为占位符指定具体的值
// 注意：如果 SQL 语句中有多个占位符，则必须使用数组为每个占位符指定具体的值
//      如果 SQL 语句汇总只有一个占位符，则可以省略数组，直接写值
db.query(sqlStr, 8, (err, results) => {
    if (err) {
        console.log(err.message);
    }
    if (results.affectedRows === 1) {
        console.log('删除数据成功');
    }
});
```



[![image-20221215183134524](https://github.com/JERRY-Z-J-R/I-love-you-3-thousand/raw/master/%E6%88%91%E7%88%B1%E4%BD%A0%EF%BC%8C%E4%B8%8D%E6%AD%A2%E4%B8%89%E5%8D%83%E9%81%8D/Node/07-mysql%E6%A8%A1%E5%9D%97/mark-img/image-20221215183134524.png)](https://github.com/JERRY-Z-J-R/I-love-you-3-thousand/blob/master/我爱你，不止三千遍/Node/07-mysql模块/mark-img/image-20221215183134524.png)

### 1.3.7 标记删除

使用 DELETE 语句，会把真正的把数据从表中删除掉。为了保险起见，推荐使用标记删除的形式，来模拟删除的动作。

所谓的标记删除，就是在表中设置类似于 status 这样的状态字段，来标记当前这条数据是否被删除。

当用户执行了删除的动作时，我们并没有执行 DELETE 语句把数据删除掉，而是执行了 UPDATE 语句，将这条数据对应的 status 字段标记为删除即可。

```
// 标记删除：使用 UPDATE 语句代替 DELETE 语句；只更新数据的状态，并没有真正删除
db.query('UPDATE USERS SET status=1 WHERE id=?', 8, (err, results) => {
    if (err) {
        return console.log(err.message);
    }
    if (results.affectedRows === 1) {
        console.log('删除数据成功');
    }
});
```



[![image-20221215183404453](https://github.com/JERRY-Z-J-R/I-love-you-3-thousand/raw/master/%E6%88%91%E7%88%B1%E4%BD%A0%EF%BC%8C%E4%B8%8D%E6%AD%A2%E4%B8%89%E5%8D%83%E9%81%8D/Node/07-mysql%E6%A8%A1%E5%9D%97/mark-img/image-20221215183404453.png)](https://github.com/JERRY-Z-J-R/I-love-you-3-thousand/blob/master/我爱你，不止三千遍/Node/07-mysql模块/mark-img/image-20221215183404453.png)

## 1.4 其他补充

### 1.4.1 关于连接

实际上我们之前使用的 `mysql.createPool` 是创建连接池的方式，如果我们不需要连接池，那么应该这样：

首先，使用以下语句导入 mysql 模块：

```
const mysql = require('mysql');
```



其次，通过调用 createConnection() 方法并提供 MySQL 服务器上的详细信息（如主机，用户，密码和数据库），建立与 MySQL 数据库的连接，如下所示：

```
const connection = mysql.createConnection({
    host: 'localhost',
    user: 'root',
    password: '123456',
    database: 'test'
});
```



然后，在连接对象上调用 connect() 方法连接到 MySQL 数据库服务器：

connect() 方法接受一个具有 err 参数的回调函数，如果发生任何错误，它将提供详细的错误。

```
connection.connect(err => {
  if (err) {
    return console.error('error: ' + err.message);
  }
  console.log('Connected to the MySQL server.');
});
```



完整的程序代码如下所示：

```
const mysql = require('mysql');

const connection = mysql.createConnection({
    host: 'localhost',
    user: 'root',
    password: '123456',
    database: 'todoapp'
});

connection.connect(err => {
  if (err) {
    return console.error('error: ' + err.message);
  }

  console.log('Connected to the MySQL server.');
});
```



我们来运行并测试一下：

```
F:\worksp\mysql\nodejs\nodejs-connect>node connect.js
openssl config failed: error:02001003:system library:fopen:No such process
Connected to the MySQL server.
```



如果看到如上所示的 “connected to the MySQL server” 的消息，那么恭喜，您已经从 Node.js 应用程序成功连接到 MySQL 数据库服务器。

假设使用 MySQL 用户账号的密码有错，并尝试连接到数据，您将收到一条错误消息：

```
F:\worksp\mysql\nodejs\nodejs-connect>node connect.js
openssl config failed: error:02001003:system library:fopen:No such process
error: ER_ACCESS_DENIED_ERROR: Access denied for user 'root'@'localhost' (using password: YES)
```



请注意，今后你在 connection 对象上调用的每个方法都按顺序排队和执行。

关闭 Node.js 与 MySQL 数据库连接

要正常关闭数据库连接，请在 connection 对象上调用 end() 方法。

end() 方法确保在数据库连接关闭之前始终执行所有剩余的查询。

```
connection.end(err => {
  if (err) {
    return console.log('error:' + err.message);
  }
  console.log('Close the database connection.');
});
```



要立即强制连接，可以使用 destroy() 方法。 destroy() 方法保证不会再为连接触发回调或事件。

```
connection.destroy();
```



请注意，destroy() 方法不会像 end() 方法那样采取任何回调参数。

使用举例：

```
var mysql = require('mysql');
var connection = mysql.createConnection({
  host: 'localhost',
  user: 'root',
  password: '123456',
  database: 'my_db'
});
 
connection.connect();
 
connection.query('SELECT 1 + 1 AS solution', (error, results) => {
  if (error) throw error;
  console.log('The solution is: ', results[0].solution);
});
 
connection.end();
```



Node.js 模块的 MySQL 驱动程序提供了内置的连接池功能，假设您要创建一个具有 10 个连接的连接池：

```
const pool = mysql.createPool({
    connectionLimit: 10,	// 如果没有配置 connectionLimit 那么它默认就是 10
    host: 'localhost',
    user: 'root',
    password: '123456', 
    database: 'test'
});

pool.query('SELECT 1 + 1 AS solution', (error, results) => {
  if (error) throw error;
  console.log('The solution is: ', results[0].solution);
});
```



直接 pool.query() 的方式是 pool.getConnection() -> connection.query() -> connection.release() 代码流的快捷方式。

要从池中获取连接，可以使用 getConnection() 方法：

```
pool.getConnection((err, connection) => {
  // 执行查询
  // ...
});
```



要在完成连接后将其释放到池中，可以调用 connection.release()。 之后，连接将在池中可用，并可以由其他业务再次使用。

```
pool.getConnection((err, connection) => {
  // 执行查询
  // ...
  connection.release();
});
```



要关闭连接并将其从池中删除，请使用 connection.destroy() 方法。 如果下次需要，将在池中创建一个新的连接。

```
pool.getConnection((err, connection) => {
  // 执行查询
  // ...
  connection.destroy();
});
```



请注意，连接由池惰性创建。如果将池配置为允许最多 100 个连接，但同时只使用 5 个，则只会建立 5 个连接。

连接也是循环使用的，连接从池的顶部取出，然后返回到池的底部。

当从池中检索到以前的连接时，会向服务器发送一个 ping 包，以检查连接是否仍然正常。

当你完成使用池，你必须结束所有的连接，否则 Node.js 事件循环将保持活动，直到连接被 MySQL 服务器关闭。

如果在脚本中使用该池，或者需要优雅地关闭服务器时，通常会在结束前这样做。

要关闭池中的所有连接，请使用 pool 对象的 end() 方法，如下所示：

```
pool.end(err => {
  if (err) {
    return console.log(err.message);
  }
  // 关闭所有连接
});
```



注意：一旦执行了 pool.end()，那么 pool.getConnection 和其它操作将无法继续执行，如果已经在执行的任务那么会等待它执行完毕，新的任务则不再执行。

使用 pool.getConnection() 可以为后续查询共享连接状态。而使用 pool.query() 的话，不同的两次调用可能使用的是两个不同的连接并行运行。

```
var mysql = require('mysql');
var pool  = mysql.createPool(...);

pool.getConnection((err, connection) => {
  if (err) throw err;

  // 使用连接
  connection.query('SELECT something FROM sometable', (error, results) => {
    // 完成连接后就释放它
    connection.release();

    // 在释放后处理错误
    if (error) throw error;

    // 不要在这里使用连接，它已经返回到池中
  });
});
```



### 1.4.2 SQL注入

sql 语句中使用 `?` 作为查询参数占位符，值以数组的形式传入，那么这种方式默认就是防止 SQL 注入的！

如果 sql 是直接拼接的字符串值，那么为了防止 SQL 注入，必须对参数值事先调用 `mysql.escape()` 来过滤：

```
status = mysql.escape(status);
id = mysql.escape(id);
connection.query(`update tbl_module set module_status = ${status} where id = ${id}`);
```



实际上，`?` 占位符在背后就是自动调用了 `mysql.escape()`。

### 1.4.3 查询细节

还是看文档吧：[[mysql - npm (npmjs.com)](https://www.npmjs.com/package/mysql)](https://github.com/mysqljs/mysql#readme)

中文文档：[mysql - mysql中文文档翻译 - Breword 文档集合](https://www.breword.com/mysqljs-mysql)

### 1.4.4 更优推荐

- mysql2：[mysql2 - npm (npmjs.com)](https://www.npmjs.com/package/mysql2)，与 mysql 相同的 API，更快的性能，更多的功能，提供 Promise 封装！
- sequelize：[sequelize - npm (npmjs.com)](https://www.npmjs.com/package/sequelize)，Node.js 的 ORM 工具，可以将关系型数据库表映射为 JS 对象，同时提供非常强大的功能！

------

# 前后端身份认证

> 原创内容，转载请注明出处！

# 一、Web开发模式

目前主流的 Web 开发模式有两种，分别是：

- 基于服务端渲染的传统 Web 开发模式
- 基于前后端分离的新型 Web 开发模式

## 1.1 服务端渲染的Web开发模式

服务端渲染的概念：服务器发送给客户端的 HTML 页面，是在服务器通过字符串的拼接，动态生成的。因此，客户端不需要使用 Ajax 这样的技术额外请求页面的数据。

代码示例如下：

```
app.get('/index.html', (req, res) => {
    // 要渲染的数据
    const user = {
        name: 'zjr',
        age: 18
    };
    // 服务端通过字符串的拼接，动态生成 HTML 内容
    const html = `<h1>姓名：${user.name}，年龄：${user.age}</h1>`;
    // 把生成好的 HTML 页面响应给客户端
    res.send(html);
});
```



## 1.2 服务端渲染的优缺点

优点：

- **前端耗时少！**因为服务器端负责动态生成 HTML 内容，浏览器只需要直接渲染页面即可。
- **有利于 SEO！**因为服务器端响应的是完整的 HTML 页面内容，所以搜索引擎爬虫更容易爬取获得信息。

缺点：

- **占用服务器端资源！**由服务端完成 HTML 页面内容的生成，如果请求较多，会对服务器造成一定的访问压力。
- **开发效率低！**使用服务器端渲染，则无法进行分工合作，尤其对于前端复杂度高的项目，不利于项目高效开发。

## 1.3 前后端分离的Web开发模式

前后端分离的概念：前后端分离的开发模式，依赖于 Ajax 技术的广泛应用。简而言之，前后端分离的 Web 开发模式，就是后端只负责提供 API 接口，前端使用 Ajax 调用接口的开发模式。

## 1.4 前后端分离的优缺点

优点：

- **开发体验好！**前端专注于界面的开发，后端专注于 API 的开发，且前端有更多的选择性。
- **用户体验好！**Ajax 技术的广泛应用，极大的提高了用户的体验，可以轻松实现页面的局部刷新。
- **减轻了服务器端的渲染压力！**因为页面最终是在每个用户的浏览器中生成的。

缺点：

- **不利于 SEO！**。因为完整的 HTML 页面需要在客户端动态拼接完成，所以爬虫无法爬取页面的有效信息。（解决方案：利用 Vue、React 等前端框架的 SSR（server side render）技术能够很好的解决前后端分离下的 SEO 问题！）

> SEO：搜索引擎优化！
>
> 前后端分离不利于 SEO，为什么？
>
> 搜索引擎的基础爬虫的原理就是抓取你的 url，然后获取你的 html 源代码并解析。 当的页面采用了 vue 等 js 的数据绑定机制来展示页面数据，爬虫获取到的 html 是你的模型页面而不是最终数据的渲染页面，所以说用 Ajax 来渲染数据对 SEO 并不友好。

## 1.5 如何选择Web开发模式

不谈业务场景而盲目选择使用何种开发模式都是耍流氓。

- 比如企业级官网，主要功能是展示而没有复杂的交互，并且需要良好的 SEO，则这时我们就需要使用服务器端渲染。
- 而类似后台管理项目，交互性比较强，不需要考虑 SEO，那么就可以使用前后端分离的开发模式。

另外，具体使用何种开发模式并不是绝对的，为了同时兼顾首页的渲染速度和前后端分离的开发效率，一些网站采用了首屏服务端渲染 + 其他页面前后端分离的开发模式。

# 二、身份认证

## 2.1 什么是身份认证

身份认证（Authentication）又称 “身份验证”、“鉴权”，是指通过一定的手段，完成对用户身份的确认。

- 日常生活中的身份认证随处可见，例如：高铁的验票乘车，手机的密码或指纹解锁，支付宝或微信的支付密码等。
- 在 Web 开发中，也涉及到用户身份的认证，例如：各大网站的手机验证码登录、邮箱密码登录、二维码登录等。

## 2.2 为什么需要身份认证

身份认证的目的，是为了确认当前所声称为某种身份的用户，确实是所声称的用户。例如，你去找快递员取快递，你要怎么证明这份快递是你的。

在互联网项目开发中，如何对用户的身份进行认证，是一个值得深入探讨的问题。

## 2.3 不同开发模式下的身份认证

对于服务端渲染和前后端分离这两种开发模式来说，分别有着不同的身份认证方案：

- 服务端渲染推荐使用 **Session** **认证机制**
- 前后端分离推荐使用 **JWT** **认证机制**

# 三、Session认证机制

## 3.1 HTTP协议的无状态性

了解 HTTP 协议的无状态性是进一步学习 Session 认证机制的必要前提。

HTTP 协议的无状态性，指的是客户端的每次 HTTP 请求都是独立的，连续多个请求之间没有直接的关系，服务器不会主动保留每次 HTTP 请求的状态。

[![image-20221215192855055](https://github.com/JERRY-Z-J-R/I-love-you-3-thousand/raw/master/%E6%88%91%E7%88%B1%E4%BD%A0%EF%BC%8C%E4%B8%8D%E6%AD%A2%E4%B8%89%E5%8D%83%E9%81%8D/Node/08-%E5%89%8D%E5%90%8E%E7%AB%AF%E8%BA%AB%E4%BB%BD%E8%AE%A4%E8%AF%81/mark-img/image-20221215192855055.png)](https://github.com/JERRY-Z-J-R/I-love-you-3-thousand/blob/master/我爱你，不止三千遍/Node/08-前后端身份认证/mark-img/image-20221215192855055.png)

## 3.2 如何突破HTTP无状态的限制

对于超市来说，为了方便收银员在进行结算时给 VIP 用户打折，超市可以为每个 VIP 用户发放会员卡。

[![image-20221215192911804](https://github.com/JERRY-Z-J-R/I-love-you-3-thousand/raw/master/%E6%88%91%E7%88%B1%E4%BD%A0%EF%BC%8C%E4%B8%8D%E6%AD%A2%E4%B8%89%E5%8D%83%E9%81%8D/Node/08-%E5%89%8D%E5%90%8E%E7%AB%AF%E8%BA%AB%E4%BB%BD%E8%AE%A4%E8%AF%81/mark-img/image-20221215192911804.png)](https://github.com/JERRY-Z-J-R/I-love-you-3-thousand/blob/master/我爱你，不止三千遍/Node/08-前后端身份认证/mark-img/image-20221215192911804.png)

注意：现实生活中的会员卡身份认证方式，在 Web 开发中的专业术语叫做 **Cookie**。

## 3.3 什么是Cookie

Cookie 是存储在用户浏览器中的一段不超过 4 KB 的字符串。它由一个名称（Name）、一个值（Value）和其它几个用于控制 Cookie 有效期、安全性、使用范围的可选属性组成。

不同域名下的 Cookie 各自独立，每当客户端发起请求时，会自动把**当前域名下**所有未过期的 Cookie 一同发送到服务器。

Cookie 的几大特性：

- 自动发送
- 域名独立
- 过期时限
- 4KB 限制

## 3.4 Cookie在算法认证中的作用

客户端第一次请求服务器的时候，服务器通过响应头的形式，向客户端发送一个身份认证的 Cookie，浏览器会自动将 Cookie 保存在浏览器中。

随后，当浏览器每次请求服务器的时候，浏览器会自动将身份认证相关的 Cookie，通过请求头的形式发送给服务器，服务器即可验明客户端的身份。

[![image-20221215194007711](https://github.com/JERRY-Z-J-R/I-love-you-3-thousand/raw/master/%E6%88%91%E7%88%B1%E4%BD%A0%EF%BC%8C%E4%B8%8D%E6%AD%A2%E4%B8%89%E5%8D%83%E9%81%8D/Node/08-%E5%89%8D%E5%90%8E%E7%AB%AF%E8%BA%AB%E4%BB%BD%E8%AE%A4%E8%AF%81/mark-img/image-20221215194007711.png)](https://github.com/JERRY-Z-J-R/I-love-you-3-thousand/blob/master/我爱你，不止三千遍/Node/08-前后端身份认证/mark-img/image-20221215194007711.png)

## 3.5 Cookie不具有安全性

由于 Cookie 是存储在浏览器中的，而且浏览器也提供了读写 Cookie 的 API，因此 Cookie 很容易被伪造，不具有安全性。因此不建议服务器将重要的隐私数据，通过 Cookie 的形式发送给浏览器。

[![image-20221215194740416](https://github.com/JERRY-Z-J-R/I-love-you-3-thousand/raw/master/%E6%88%91%E7%88%B1%E4%BD%A0%EF%BC%8C%E4%B8%8D%E6%AD%A2%E4%B8%89%E5%8D%83%E9%81%8D/Node/08-%E5%89%8D%E5%90%8E%E7%AB%AF%E8%BA%AB%E4%BB%BD%E8%AE%A4%E8%AF%81/mark-img/image-20221215194740416.png)](https://github.com/JERRY-Z-J-R/I-love-you-3-thousand/blob/master/我爱你，不止三千遍/Node/08-前后端身份认证/mark-img/image-20221215194740416.png)

注意：千万不要使用 Cookie 存储重要且隐私的数据！比如用户的身份信息、密码等。

## 3.6 提高身份认证的安全性

为了防止客户伪造会员卡，收银员在拿到客户出示的会员卡之后，可以在收银机上进行刷卡认证。只有收银机确认存在的会员卡，才能被正常使用。

[![image-20221215194924023](https://github.com/JERRY-Z-J-R/I-love-you-3-thousand/raw/master/%E6%88%91%E7%88%B1%E4%BD%A0%EF%BC%8C%E4%B8%8D%E6%AD%A2%E4%B8%89%E5%8D%83%E9%81%8D/Node/08-%E5%89%8D%E5%90%8E%E7%AB%AF%E8%BA%AB%E4%BB%BD%E8%AE%A4%E8%AF%81/mark-img/image-20221215194924023.png)](https://github.com/JERRY-Z-J-R/I-love-you-3-thousand/blob/master/我爱你，不止三千遍/Node/08-前后端身份认证/mark-img/image-20221215194924023.png)

这种 “会员卡 + 刷卡认证” 的设计理念，就是 Session 认证机制的精髓。

## 3.7 Session的工作原理

[![image-20221215195150951](https://github.com/JERRY-Z-J-R/I-love-you-3-thousand/raw/master/%E6%88%91%E7%88%B1%E4%BD%A0%EF%BC%8C%E4%B8%8D%E6%AD%A2%E4%B8%89%E5%8D%83%E9%81%8D/Node/08-%E5%89%8D%E5%90%8E%E7%AB%AF%E8%BA%AB%E4%BB%BD%E8%AE%A4%E8%AF%81/mark-img/image-20221215195150951.png)](https://github.com/JERRY-Z-J-R/I-love-you-3-thousand/blob/master/我爱你，不止三千遍/Node/08-前后端身份认证/mark-img/image-20221215195150951.png)

# 四、在Express中使用Session认证

## 4.1 安装express-session中间件

在 Express 项目中，只需要安装 express-session 中间件，即可在项目中使用 Session 认证：

```
npm install express-session
```



## 4.2 配置express-session中间件

express-session 中间件安装成功后，需要通过 app.use() 来注册 session 中间件，示例代码如下：

```
// 导入 Session 中间件
const session = require('express-session');

// 配置 Session 中间件
app.use(session({
    secret: 'keyboard cat',		// secret 属性的值可以为任意字符串
    resave: false,				// 固定写法
    saveUninitialized: true		// 固定写法
}));
```



## 4.3 向session中存储数据

当 express-session 中间件配置成功后，即可通过 req.session 来访问和使用 session 对象，从而存储用户的关键信息：

```
app.post('/api/login', (req, res) => {
    // 判断用户提交的登录信息是否正确
    if (req.body.username !== 'admin' || req.body.password !== '000000') {
        return res.send({
            status: 1, 
            msg: '登录失败'
        });
    }
    
    req.session.user = req.body;	// 将用户的信息，存储到 Session 中
    req.session.islogin = true;		// 将用户的登录状态，存储到 Session 中
    
    res.send({
        status: 0,
        msg: '登录成功'
    });
});
```



## 4.4 从session中取数据

可以直接从 req.session 对象上获取之前存储的数据，示例代码如下：

```
// 获取用户姓名的接口
app.get('/api/username', (req, res) => {
    // 判断用户是否登录
    if (!req.session.islogin) {
        return res.send({
            status: 1,
            msg: 'fail'
        });
    }
    
    res.send({
        status: 0,
        msg: 'success',
        username: req.session.user.username
    });
});
```



## 4.5 清空session

调用 req.session.destroy() 函数，即可清空当前用户在服务器保存的 session 信息。

```
// 退出登录的接口
app.post('/api/logout', (req, res) => {
    // 清空当前客户端对应的 session 信息
    req.session.destroy();
    res.send({
        status: 0,
        msg: '退出登录成功'
    });
});
```



# 五、JWT认证机制

## 5.1 了解Session认证的局限性

Session 认证机制需要配合 Cookie 才能实现，由于 Cookie 默认不支持跨域访问，所以，当涉及到前端跨域请求后端接口的时候，需要做额外的配置，才能实现跨域 Session 认证。

注意：

- 当前端请求后端接口不存在跨域问题的时候，推荐使用 Session 身份认证机制。
- 当前端需要跨域请求后端接口的时候，不推荐使用 Session 身份认证机制，推荐使用 JWT 认证机制。

## 5.2 什么是JWT

JWT（英文全称：JSON Web Token）是目前最流行的跨域认证解决方案。

## 5.3 JWT的工作原理

[![image-20221215204010879](https://github.com/JERRY-Z-J-R/I-love-you-3-thousand/raw/master/%E6%88%91%E7%88%B1%E4%BD%A0%EF%BC%8C%E4%B8%8D%E6%AD%A2%E4%B8%89%E5%8D%83%E9%81%8D/Node/08-%E5%89%8D%E5%90%8E%E7%AB%AF%E8%BA%AB%E4%BB%BD%E8%AE%A4%E8%AF%81/mark-img/image-20221215204010879.png)](https://github.com/JERRY-Z-J-R/I-love-you-3-thousand/blob/master/我爱你，不止三千遍/Node/08-前后端身份认证/mark-img/image-20221215204010879.png)

总结：用户的信息通过 Token 字符串的形式，保存在客户端浏览器中。服务器通过还原 Token 字符串的形式来认证用户的身份。

## 5.4 JWT的组成部分

JWT 通常由三部分组成，分别是 Header（头部）、Payload（有效荷载）、Signature（签名）。

三者之间使用英文的 `.` 分 隔，格式如下：

```
Header.Payload.Signature
```



下面是 JWT 字符串的示例：

[![image-20221215204211017](https://github.com/JERRY-Z-J-R/I-love-you-3-thousand/raw/master/%E6%88%91%E7%88%B1%E4%BD%A0%EF%BC%8C%E4%B8%8D%E6%AD%A2%E4%B8%89%E5%8D%83%E9%81%8D/Node/08-%E5%89%8D%E5%90%8E%E7%AB%AF%E8%BA%AB%E4%BB%BD%E8%AE%A4%E8%AF%81/mark-img/image-20221215204211017.png)](https://github.com/JERRY-Z-J-R/I-love-you-3-thousand/blob/master/我爱你，不止三千遍/Node/08-前后端身份认证/mark-img/image-20221215204211017.png)

## 5.5 JWT三个部分各自的含义

JWT 的三个组成部分，从前到后分别是 Header、Payload、Signature。

其中：

- Payload 部分才是真正的用户信息，它是用户信息经过加密之后生成的字符串。
- Header 和 Signature 是安全性相关的部分，只是为了保证 Token 的安全性。

[![image-20221215204359726](https://github.com/JERRY-Z-J-R/I-love-you-3-thousand/raw/master/%E6%88%91%E7%88%B1%E4%BD%A0%EF%BC%8C%E4%B8%8D%E6%AD%A2%E4%B8%89%E5%8D%83%E9%81%8D/Node/08-%E5%89%8D%E5%90%8E%E7%AB%AF%E8%BA%AB%E4%BB%BD%E8%AE%A4%E8%AF%81/mark-img/image-20221215204359726.png)](https://github.com/JERRY-Z-J-R/I-love-you-3-thousand/blob/master/我爱你，不止三千遍/Node/08-前后端身份认证/mark-img/image-20221215204359726.png)

## 5.6 JWT的使用方式

客户端收到服务器返回的 JWT 之后，通常会将它储存在 localStorage 或 sessionStorage 中。

此后，客户端每次与服务器通信，都要带上这个 JWT 的字符串，从而进行身份认证。推荐的做法是把 JWT 放在 HTTP 请求头的 Authorization 字段中，格式如下：

```
Authorization: Bearer <token>
```



# 六、在Express中使用JWT

## 6.1 安装JWT相关包

运行如下命令，安装如下两个 JWT 相关的包：

```
npm install jsonwebtoken express-jwt
```



其中：

- jsonwebtoken 用于生成 JWT 字符串
- express-jwt 用于将 JWT 字符串解析还原成 JSON 对象

## 6.2 导入JWT相关包

使用 require() 函数，分别导入 JWT 相关的两个包：

```
// 导入用于生成 JWT 字符串的包
const jwt = require('jsonwebtoken');
// 导入用于将客户端发送过来的 JWT 字符串，解析还原成 JSON 对象的包
const expressJWT = require('express-jwt');
```



## 6.3 定义secret密钥

为了保证 JWT 字符串的安全性，防止 JWT 字符串在网络传输过程中被别人破解，我们需要专门定义一个用于加密和解密的 secret 密钥：

- 当生成 JWT 字符串的时候，需要使用 secret 密钥对用户的信息进行加密，最终得到加密好的 JWT 字符串
- 当把 JWT 字符串解析还原成 JSON 对象的时候，需要使用 secret 密钥进行解密

```
// secret 密钥的本质：就是一个字符串
const secretKey = 'I Love Node ^_^';
```



## 6.4 在登录成功后生成JWT字符串

调用 jsonwebtoken 包提供的 `sign()` 方法，将用户的信息加密成 JWT 字符串，响应给客户端：

```
// 登录接口
app.post('/api/login', function (req, res) => {
         // ... 省略登录失败情况下的代码
         
         // 调用 jwt.sign() 生成 JWT 字符串，三个参数分别是：用户信息对象、加密密钥、配置对象
         const tokenStr = jwt.sign({ username: userinfo.username }, secretKey, { expiresIn: '30s' });
         // 用户登录成功之后，生成 JWT 字符串，通过 token 属性响应给客户端
         res.send({
         	status: 200,
         	message: '登录成功！',
         	token: tokenStr;
         });
});
```



## 6.5 将JWT字符串还原为JSON对象

客户端每次在访问那些有权限接口的时候，都需要主动通过请求头中的 Authorization 字段，将 Token 字符串发送到服务器进行身份认证。

此时，服务器可以通过 express-jwt 这个中间件，自动将客户端发送过来的 Token 解析还原成 JSON 对象：

```
// 使用 app.use() 来注册中间件
// expressJWT( { secret: secretKey } ) 就是用来解析 Token 的中间件
// .unless({ path: [/^\/api\//] }) 用来指定哪些接口不需要访问权限
app.use(expressJWT({ secret: secretKey }).unless({ path: [/^\/api\//] }));
```



## 6.6 使用req.user获取用户信息

当 express-jwt 这个中间件配置成功之后，即可在那些有权限的接口中，使用 req.user 对象，来访问从 JWT 字符串中解析出来的用户信息了，示例代码如下：

```
// 这是一个有权限的 API 接口
app.get('/admin/getinfo', function(req, res) {
    // 只要配置成功了 express-jwt 这个中间件，就会把解析出来的用户信息，自动挂载到 req.user 属性上
    // 新版本把 req.user 被替换为了 req.auth
    console.log(req.user);
    res.send({
        status: 200,
        message: '获取用户信息成功',
        data: req.user
    });
});
```



> 注意：千万不要把密码这种信息加密到 token 中！

## 6.7 捕获解析JWT失败后产生的错误

当使用 express-jwt 解析 Token 字符串时，如果客户端发送过来的 Token 字符串过期或不合法，会产生一个解析失败的错误（UnauthorizedError），影响项目的正常运行。我们可以通过 Express 的错误中间件，捕获这个错误并进行相关的处理，示例代码如下：

```
app.use((err, req, res, next) => {
    // token 解析失败导致的错误
    if (err.name === 'UnauthorizedError') {
        return res.send({ status: 401, message: '无效的token' });
    }
    // 其它原因导致的错误
    res.send({ status: 500, message: '未知错误' });
});
```



## 6.8 JWT的优势与劣势

【优势】

1、更高的安全性！这个就不再叙述了，上文已经提到过。

2、服务器集群模式下，更比 Session 更方面实现！

[![image-20230207120123436](https://github.com/JERRY-Z-J-R/I-love-you-3-thousand/raw/master/%E6%88%91%E7%88%B1%E4%BD%A0%EF%BC%8C%E4%B8%8D%E6%AD%A2%E4%B8%89%E5%8D%83%E9%81%8D/Node/08-%E5%89%8D%E5%90%8E%E7%AB%AF%E8%BA%AB%E4%BB%BD%E8%AE%A4%E8%AF%81/mark-img/image-20230207120123436.png)](https://github.com/JERRY-Z-J-R/I-love-you-3-thousand/blob/master/我爱你，不止三千遍/Node/08-前后端身份认证/mark-img/image-20230207120123436.png)

[![image-20230207120157947](https://github.com/JERRY-Z-J-R/I-love-you-3-thousand/raw/master/%E6%88%91%E7%88%B1%E4%BD%A0%EF%BC%8C%E4%B8%8D%E6%AD%A2%E4%B8%89%E5%8D%83%E9%81%8D/Node/08-%E5%89%8D%E5%90%8E%E7%AB%AF%E8%BA%AB%E4%BB%BD%E8%AE%A4%E8%AF%81/mark-img/image-20230207120157947.png)](https://github.com/JERRY-Z-J-R/I-love-you-3-thousand/blob/master/我爱你，不止三千遍/Node/08-前后端身份认证/mark-img/image-20230207120157947.png)

这样一来，就不保存 session id 了，只是生成 token, 然后验证 token，用服务器 CPU 计算时间换取了 session 存储空间以及 session 同步所带来的设计成本！

解除了 session id 这个负担，可以说是无事一身轻，机器集群现在可以轻松地做水平扩展，用户访问量增大，直接加机器就行，这种无状态的感觉实在是太好了！

【劣势】

1. 占带宽，正常情况下要比 session id 更大，需要消耗更多流量，挤占更多带宽，假如你的网站每月有 10 万次的浏览，就意味着要多开销几十兆的流量。听起来并不多，但日积月累也是不小一笔开销。实际上，许多人会在 JWT 中存储的信息会更多
2. 无法在服务端注销，那么就很难解决劫持问题
3. 性能问题，JWT 的卖点之一就是加密签名，由于这个特性，接收方得以验证 JWT 是否有效且被信任。对于有着严格性能要求的 Web 应用，这并不理想，尤其对于单线程环境，可能造成性能的大量消耗（Node.js 中可以用子进程来单独负责加密解密的部分，从而更好的利用 CPU 空闲资源）
4. 同样不是绝对安全的！如果一个人的 token 被别人偷走了，那也没办法，服务器会认为小偷就是合法用户，这其实和一个人的 session id 被别人偷走是一样的
