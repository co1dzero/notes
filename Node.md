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

### 3.2.6 局部生效的中间件

不使用 `app.use()` 定义的中间件，叫做局部生效的中间件，示例代码如下：

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

### 3.2.7 定义多个局部中间件

可以在路由中，通过如下两种等价的方式，使用多个局部中间件，他们按照定义的先后顺序执行：

```
// 以下两种写法是“完全等价”的，可根据自己的喜好，选择任意一种方式进行使用
app.get('/', mw1, mw2, (req, res) => {
    res.send('Home page.');
});

app.get('/', [mw1, mw2], (req, res) => {
    res.send('Home page.');
});
```

### 3.2.8 了解中间件的5个使用注意事项

1. **一定要在路由之前注册中间件！**
2. 客户端发送过来的请求，可以连续调用多个中间件进行处理
3. 执行完中间件的业务代码之后，不要忘记调用 next() 函数
4. 为了防止代码逻辑混乱，调用 next() 函数后不要再写额外的代码
5. 连续调用多个中间件时，多个中间件之间，共享 req 和 res 对象

## 3.3 中间件的分类

为了方便大家理解和记忆中间件的使用，Express 官方把常见的中间件用法，分成了 5 大类，分别是：

- 应用级别的中间件
- 路由级别的中间件
- 错误级别的中间件
- Express 内置的中间件
- 第三方的中间件

### 3.3.1 应用级别的中间件

通过 `app.use()` 或 `app.get()` 或 `app.post()`，绑定到 app 实例上的中间件，都叫做应用级别的中间件，代码示例如下：

```
// 应用级别的中间件（全局中间件）
app.use((req, res, next) => {
    // ...
    next();
});

// 应用级别的中间件（局部中间件）
app.get('/', mw, (req, res) => {
    res.send('Home page.');
});
```

### 3.3.2 路由级别的中间件

绑定到 `express.Router()` 实例上的中间件，叫做路由级别的中间件。它的用法和应用级别中间件没有任何区别。

只不过，应用级别中间件是绑定到 app 实例上，路由级别中间件绑定到 router 实例上，代码示例如下：

```
var app = express();
var router = express.Router();

// 路由级别的中间件
router.use(function (req, res, next) {
    // ...
    next();
});

app.use('/', router);
```

### 3.3.3 错误级别的中间件

错误级别中间件的作用：专门用来捕获整个项目中发生的异常错误，从而防止项目异常崩溃的问题。

格式：错误级别中间件的 function 处理函数中，必须有 4 个形参，形参顺序从前到后，分别是 `err` 、`req`、 `res`、`next`。

```
app.get('/', function (req, res) {				// 路由
    throw new Error('服务器内部发生了错误！');		 // 人为抛出一个自定义的错误  
    res.send('Home Page.');						
});

app.use(function (err, req, res, next) {		// 错误级别的中间件
    console.log('发生了错误：' + err.message);	// 在服务器打印错误消息
    res.send('Error!' + err.message);			// 向客户端响应错误相关的内容
});
```

> 注意：错误级别的中间件，必须注册在所有路由之后！同时，即便没有 next()，错误级别的中间件也会自动捕捉到错误后立马生效！

[![image-20221215101926536](https://github.com/JERRY-Z-J-R/I-love-you-3-thousand/raw/master/%E6%88%91%E7%88%B1%E4%BD%A0%EF%BC%8C%E4%B8%8D%E6%AD%A2%E4%B8%89%E5%8D%83%E9%81%8D/Node/06-express/mark-img/image-20221215101926536.png)](https://github.com/JERRY-Z-J-R/I-love-you-3-thousand/blob/master/我爱你，不止三千遍/Node/06-express/mark-img/image-20221215101926536.png)

### 3.3.4 Express内置的中间件

自 Express 4.16.0 版本开始，Express 内置了 3 个常用的中间件，极大的提高了 Express 项目的开发效率和体验：

1. `express.static` 快速托管静态资源的内置中间件，例如：HTML 文件、图片、CSS 样式等（无兼容性）
2. `express.json` 解析 JSON 格式的请求体数据（有兼容性，仅在 4.16.0+ 版本中可用）
3. `express.urlencoded` 解析 URL-encoded 格式的请求体数据（有兼容性，仅在 4.16.0+ 版本中可用）

```
// 配置解析 application/json 格式数据的内置中间件
app.use(express.json());
// 配置解析 application/x-www-form-urlencoded 格式数据的内置中间件
app.use(express.urlencoded({ extended: false }));
```

json 示例代码：

```
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

[![image-20221215103931835](https://github.com/JERRY-Z-J-R/I-love-you-3-thousand/raw/master/%E6%88%91%E7%88%B1%E4%BD%A0%EF%BC%8C%E4%B8%8D%E6%AD%A2%E4%B8%89%E5%8D%83%E9%81%8D/Node/06-express/mark-img/image-20221215103931835.png)](https://github.com/JERRY-Z-J-R/I-love-you-3-thousand/blob/master/我爱你，不止三千遍/Node/06-express/mark-img/image-20221215103931835.png)

urlencoded 示例代码：

```
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

### 3.3.5 第三方的中间件

非 Express 官方内置的，而是由第三方开发出来的中间件，叫做第三方中间件。在项目中，大家可以按需下载并配置第三方中间件，从而提高项目的开发效率。

例如：在 express@4.16.0 之前的版本中，经常使用 body-parser 这个第三方中间件，来解析请求体数据。使用步骤如下：

- 运行 `npm install body-parser` 安装中间件
- 使用 `require` 导入中间件
- 调用 `app.use()` 注册并使用中间件

注意：Express 内置的 express.urlencoded 中间件，就是基于 body-parser 这个第三方中间件进一步封装出来的。

示例代码：

```
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

### 3.4.1 需求描述与实现步骤

自己手动模拟一个类似于 express.urlencoded 这样的中间件，来解析 POST 提交到服务器的表单数据。

实现步骤：

- 定义中间件
- 监听 req 的 data 事件
- 监听 req 的 end 事件
- 使用 querystring 模块解析请求体数据
- 将解析出来的数据对象挂载为 req.body
- 将自定义中间件封装为模块

### 3.4.2 定义中间件

使用 `app.use()` 来定义全局生效的中间件，代码如下：

```
app.use(function (req, res, next) {
    // 中间件的业务逻辑
});
```

### 3.4.3 监听req的data事件

在中间件中，需要监听 req 对象的 data 事件，来获取客户端发送到服务器的数据。

如果数据量比较大，无法一次性发送完毕，则客户端会把数据切割后，分批发送到服务器。所以 data 事件可能会触发多次，每一次触发 data 事件时，获取到数据只是完整数据的一部分，需要手动对接收到的数据进行拼接。

```
// 定义变量，用来存储客户端发送过来的请求体数据
let str = '';
// 监听 req 对象的 data 事件（客户端发送过来的新的请求体数据）
req.on('data', chunk => {
    // 拼接请求体数据，隐式转换为字符串
    str += chunk;
});
```

### 3.4.4 监听req的end事件

当请求体数据接收完毕之后，会自动触发 req 的 end 事件。

因此，我们可以在 req 的 end 事件中，拿到并处理完整的请求体数据。示例代码如下：

```
// 监听 req 对象的 end 事件（请求体发送完毕后自动触发）
req.on('end', () => {
    // 打印完整的请求体数据
    console.log(str);
    // 把字符串格式的请求体数据，解析成对象格式
    // ...
});
```

### 3.4.5 使用querystring模块解析请求体数据

Node.js 内置了一个 querystring 模块，专门用来处理查询字符串。

通过这个模块提供的 parse() 函数，可以轻松把查询字符串，解析成对象的格式。示例代码如下：

```
// 导入处理 querystring 的 Node.js 内置模块
const qs = require('querystring');

// 调用 qs.parse() 方法，把查询字符串解析为对象
const body = qs.parse(str);
```

### 3.4.6 将解析出来的数据对象挂载为req.body

上游的中间件和下游的中间件及路由之间，**共享同一份** **req** **和** **res**。因此，我们可以将解析出来的数据，挂载为 req 的自定义属性，命名为 req.body，供下游使用。示例代码如下：

```
req.on('end', () => {
    const body = qs.parse(str);	// 调用 qs.parse() 方法，把查询字符串解析为对象
    req.body = body;			// 将解析出来的请求体对象，挂载为 req.body 属性
    next();						// 最后，一定要调用 next() 函数，执行后续的业务逻辑
});
```

### 3.4.7 将自定义中间件封装为模块

为了优化代码的结构，我们可以把自定义的中间件函数，封装为独立的模块，示例代码如下：

```
// custom-body-parser.js 模块中的代码
const qs = require('querystring');
function bodyParser(req, res, next) {
    // ...
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

```
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

```
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

```
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

```
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

```
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

注意：如果要获取 URL-encoded 格式的请求体数据，必须配置中间件 `app.use(express.urlencoded({ extended: false }))`，JSON 格式数据，同理。

------

代码示例：

```
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

### 4.5.1 接口的跨域问题

```
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

刚才编写的 GET 和 POST 接口，存在一个很严重的问题：不支持跨域请求。

因为，HTML 所打开的链接为：http://127.0.0.1:5500/index.html，而请求的 API 为 http://127.0.0.1/api/get 及 http://127.0.0.1/api/post，我们知道，只要 **协议、域名、端口号** 有一个不同（此处端口号不同），那么就属于跨域，浏览器就会默认阻止这种请求（丢弃响应数据，并报错）！

解决接口跨域问题的方案主要有两种：

- CORS（主流的解决方案，推荐使用）
- JSONP（有缺陷的解决方案：只支持 GET 请求）

> 注意：之前我们之所以没有遇到跨域问题，是因为 Apifox 是基于服务器而不是浏览器发送请求的，而服务器与服务器直接是不存在跨域的！

### 4.5.2 使用cors中间件解决跨域问题

cors 是 Express 的一个第三方中间件。通过安装和配置 cors 中间件，可以很方便地解决跨域问题。

使用步骤分为如下 3 步：

- 运行 `npm install cors` 安装中间件
- 使用 `const cors = require('cors')` 导入中间件
- 在路由之前调用 `app.use(cors())` 配置中间件

示例代码：

```
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

CORS （Cross-Origin Resource Sharing，跨域资源共享）由一系列 HTTP 响应头组成，这些 HTTP 响应头决定浏览器是否阻止前端 JS 代码跨域获取资源。

浏览器的同源安全策略默认会阻止网页“跨域”获取资源。但如果接口服务器配置了 CORS 相关的 HTTP 响应头，就可以解除浏览器端的跨域访问限制。

[![image-20221215114555175](https://github.com/JERRY-Z-J-R/I-love-you-3-thousand/raw/master/%E6%88%91%E7%88%B1%E4%BD%A0%EF%BC%8C%E4%B8%8D%E6%AD%A2%E4%B8%89%E5%8D%83%E9%81%8D/Node/06-express/mark-img/image-20221215114555175.png)](https://github.com/JERRY-Z-J-R/I-love-you-3-thousand/blob/master/我爱你，不止三千遍/Node/06-express/mark-img/image-20221215114555175.png)

### 4.5.4 CORS的注意事项

- CORS 主要在服务器端进行配置。客户端浏览器无须做任何额外的配置，即可请求开启了 CORS 的接口。
- CORS 在浏览器中有兼容性。只有支持 XMLHttpRequest Level2 的浏览器，才能正常访问开启了 CORS 的服务端接口（例如：IE10+、Chrome4+、FireFox3.5+）。

### 4.5.5 CORS响应头部Access-Control-Allow-Origin

响应头部中可以携带一个 **Access-Control-Allow-Origin** 字段，其语法如下:

```
Access-Control-Allow-Origin: <origin> | *
```

其中，origin 参数的值指定了允许访问该资源的外域 URL。

例如，下面的字段值将只允许来自 [http://127.0.0.1:5500](http://127.0.0.1:5500/) 的请求：

```
res.setHeader('Access-Control-Allow-Origin', 'http://127.0.0.1:5500');
```

如果指定了 Access-Control-Allow-Origin 字段的值为通配符 `*`，表示允许来自任何域的请求，示例代码如下：

```
res.setHeader('Access-Control-Allow-Origin', '*');
```

### 4.5.6 CORS响应头部Access-Control-Allow-Headers

默认情况下，CORS 仅支持客户端向服务器发送如下的 9 个请求头：

Accept、Accept-Language、Content-Language、DPR、Downlink、Save-Data、Viewport-Width、Width 、Content-Type （值仅限于 text/plain、multipart/form-data、application/x-www-form-urlencoded 三者之一）

如果客户端向服务器发送了额外的请求头信息，则需要在服务器端，通过 Access-Control-Allow-Headers 对额外的请求头进行声明，否则这次请求会失败！

```
// 允许客户端向服务器发送额外的 Content-Type 请求头和 X-Custom-Header 请求头
// 注意：多个请求头之间使用英文的逗号进行分割
res.setHeader('Access-Control-Allow-Headers', 'Content-Type, X-Custom-header');
```

### 4.5.7 CORS响应头部Access-Control-Allow-Methods

默认情况下，CORS 仅支持客户端发起 GET、POST、HEAD 请求。

如果客户端希望通过 PUT、DELETE 等方式请求服务器的资源，则需要在服务器端，通过 Access-Control-Alow-Methods 来指明实际请求所允许使用的 HTTP 方法。

示例代码如下：

```
// 只允许 POST、GET、DELETE、HEAD 请求方法
res.setHeader('Access-Control-Alow-Methods', 'POST, GET, DELETE, HEAD');
// 允许所有的 HTTP 请求方法
res.setHeader('Access-Control-Alow-Methods', '*');
```

### 4.5.8 CORS请求的分类

客户端在请求 CORS 接口时，根据请求方式和请求头的不同，可以将 CORS 的请求分为两大类，分别是：

- 简单请求
- 预检请求

### 4.5.9 简单请求

同时满足以下两大条件的请求，就属于简单请求：

- 请求方式：GET、POST、HEAD 三者之一
- HTTP 头部信息不超过以下几种字段：无自定义头部字段、Accept、Accept-Language、Content-Language、DPR、Downlink、Save-Data、Viewport-Width、Width 、Content-Type（只限这三个值 application/x-www-form-urlencoded、multipart/form-data、text/plain）

### 4.5.10 预检请求

只要符合以下任何一个条件的请求，都需要进行预检请求：

- 请求方式为 GET、POST、HEAD 之外的请求 Method 类型
- 请求头中包含自定义头部字段
- 向服务器发送了 application/json 格式的数据

在浏览器与服务器正式通信之前，浏览器会先发送 OPTION 请求进行预检，以获知服务器是否允许该实际请求，所以这一次的 OPTION 请求称为 “预检请求”。服务器成功响应预检请求后，才会发送真正的请求，并且携带真实数据。

所以，如果浏览器向服务器请求的数据为 application/json 格式的，那么要在服务器设置 `res.setHeader('Access-Control-Allow-Headers', 'Content-Type');`，表示可以接收额外的 `Content-Type` 请求头（默认只接收 application/x-www-form-urlencoded、multipart/form-data、text/plain）

### 4.5.11 简单请求和预检请求的区别

**简单请求的特点：**客户端与服务器之间只会发生一次请求。

**预检请求的特点：**客户端与服务器之间会发生两次请求，OPTION 预检请求成功之后，才会发起真正的请求。

[![image-20221215140358435](https://github.com/JERRY-Z-J-R/I-love-you-3-thousand/raw/master/%E6%88%91%E7%88%B1%E4%BD%A0%EF%BC%8C%E4%B8%8D%E6%AD%A2%E4%B8%89%E5%8D%83%E9%81%8D/Node/06-express/mark-img/image-20221215140358435.png)](https://github.com/JERRY-Z-J-R/I-love-you-3-thousand/blob/master/我爱你，不止三千遍/Node/06-express/mark-img/image-20221215140358435.png)

## 4.6 JSONP接口（了解）

### 4.6.1 回顾JSONP的概念与特点

概念：浏览器端通过 `<script>` 标签的 `src` 属性，请求服务器上的数据，同时，服务器返回一个函数的调用。这种请求数据的方式叫做 JSONP。

特点：

- JSONP 不属于真正的 Ajax 请求，因为它没有使用 XMLHttpRequest 这个对象
- JSONP 仅支持 GET 请求，不支持 POST、PUT、DELETE 等请求

### 4.6.2 创建JSONP接口的注意事项

如果项目中已经配置了 CORS 跨域资源共享，为了**防止冲突**，必须在配置 CORS 中间件之前声明 JSONP 的接口。否则 JSONP 接口会被处理成开启了 CORS 的接口。示例代码如下：

```
// 优先创建 JSONP 接口【这个接口不会被处理成 CORS 接口】
app.get('/api/jsonp', (req, res) => { });

// 再配置 CORS 中间件【后续的所有接口，都会被处理成 CORS 接口】
app.use(cors());

// 这是一个开启了 CORS 的接口
app.get('/api/get', (req, res) => { });
```

### 4.6.3 实现JSONP接口的步骤

1. 获取客户端发送过来的回调函数的名字
2. 得到要通过 JSONP 形式发送给客户端的数据
3. 根据前两步得到的数据，拼接出一个函数调用的字符串
4. 把上一步拼接得到的字符串，响应给客户端的 `<script>` 标签进行解析执行

### 4.6.4 实现JSONP接口的具体代码

```
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



