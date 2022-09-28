# nrm

## 1，什么是nrm

nrm 是一个 npm 源管理器，允许你快速地在 npm源间切换。

什么意思呢，npm默认情况下是使用npm官方源（使用npm config ls命令可以查看），在国内用这个源肯定是不靠谱的，一般我们都会用淘宝npm源：https://registry.npm.taobao.org/，修改源的方式也很简单，在终端输入：

```typescript
npm set registry https://registry.npm.taobao.org/
```

再npm config ls查看，已经切换成功。

那么，问题来了，如果哪天你又跑去国外了，淘宝源肯定是用不了的，又要切换回官网源，或者哪天你们公司有自己的私有npm源了，又需要切换成公司的源，这样岂不很麻烦？于是有了nrm。

## 2，nrm安装

```typescript
npm install -g nrm
```

## 3，nrm使用

**3.1查看可选源 星号代表当前使用源**

```typescript
nrm ls
```

![在这里插入图片描述](https://img-blog.csdnimg.cn/20210204162952234.png)
****3.1查看当前源**

安装完后可使用 nrm -V 显示版本，注意是大写V。

```typescript
nrm current
```

![在这里插入图片描述](https://img-blog.csdnimg.cn/20210204163109955.png)
**3.2 切换源**

```typescript
nrm use <registry>
```

其中，registry为源名。

比如：切换为taobao源

```typescript
nrm use taobao
```

![在这里插入图片描述](https://img-blog.csdnimg.cn/20210204163331422.png)

## 4，添加源

```typescript
nrm add <registry> <url>
```

其中，registry为源名，url为源地址。

比如：添加一个公司私有的npm源，源地址为：http://192.168.22.11:8888/repository/npm-public/，源名为cpm（随意取）。

```typescript
nrm add cpm http://192.168.22.11:8888/repository/npm-public/
```

![在这里插入图片描述](https://img-blog.csdnimg.cn/20210204163355571.png)

然后，查看是否添加成功

![在这里插入图片描述](https://img-blog.csdnimg.cn/2021020416340111.png)

## 5，删除源

```typescript
nrm del <registry>
```

其中，registry为源名。

比如：删除刚才添加的cpm源

```typescript
nrm del cpm
```

## 6，测试源速度

nrm test
其中，registry为源名。

比如：测试官方源和淘宝源的响应时间

```typescript
nrm test npm
```

![在这里插入图片描述](https://img-blog.csdnimg.cn/2021020416352495.png)

```typescript
nrm test taobao
```

![在这里插入图片描述](https://img-blog.csdnimg.cn/20210204163540669.png)



## 7, 安装报错解决

### 安装nrm，报错request@2.88.2: request has been deprecated, see https://github.com/request/request/issu

安装nrm，请求被拒绝：fetchMetadata: WARN deprecated request@2.88.2: request has been deprecated

先切换到淘宝镜像源：

```
npm config set registry https://registry.npm.taobao.org
```

查看是否切换成：

```
npm config get registry
```

![img](https://img-blog.csdnimg.cn/20200407164438558.png)

然后，解决

```
npm install nrm -g
```

![img](https://img-blog.csdnimg.cn/20200407164530182.png)

到此就可以了

查看镜像源：

```
nrm ls
```

 ![img](https://img-blog.csdnimg.cn/20200407164623105.png)

注意：

![img](https://img-blog.csdnimg.cn/20200407164656205.png)

如果 nrm ls 出错：请查看：https://blog.csdn.net/tangkthh/article/details/103440722



## 8, 常用命令

### 命令提示

  下面列出所有命令的中文示意：

1.  nrm -V ：查看当前nvm版本。
2.  nrm -h ：显示所有命令。
3.  nrm current ：显示当前源名称。
4.  nrm use <registry> ：切换源。
5.  nrm add <registry> <url> [home] ：添加一个源。比如公司自己的私有源等。
6.  nrm set-auth <registry> <value> [always] ：设置自定义源的授权信息。
7.  nrm set-email <registry> <value> ：给自定义源设置路径。
8.  nrm set-hosted-repo <registry> <value> ：设置发布到自定义源的npm托管仓储。
9.  nrm del <registry> ：删除自定义源。
10.  nrm home <registry> [browser] ：浏览器中打开源首页。
11.  nrm publish [options] [<tarball>|<folder>] ：发布包到自定义源，如果没有使用自定义源，则直接发布到npm。
12.  nrm test [registry] ：测试源的访问速度。不加registry时，测试所有的。



## 9,添加新奥公司源

```
nrm add local http://10.39.36.124:8080/nexus/repository/npm-public/
```

切换源

```
nrm use local
```

![](C:\Users\shizeyu\Desktop\notes\Ajax-vue\Snipaste_2022-09-28_15-18-35.png)