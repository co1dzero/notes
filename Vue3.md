# 认识Vue3

## 1. Vue3组合式API体验

> 通过 Counter 案例 体验Vue3新引入的组合式API

```vue
<script>
export default {
  data(){
    return {
      count:0
    }
  },
  methods:{
    addCount(){
      this.count++
    }
  }
}
</script>
```

```vue
<script setup>
import { ref } from 'vue'
const count = ref(0)
const addCount = ()=> count.value++
</script>
```

特点：

1. 代码量变少
2. 分散式维护变成集中式维护

## 2. Vue3更多的优势

![image.png](https://cdn.nlark.com/yuque/0/2023/png/274425/1678178235504-912ad469-1a9a-469d-a8dc-411a55963329.png#averageHue=%23f4dcdc&clientId=ud0819acc-4d21-4&from=paste&height=516&id=u779f92e3&name=image.png&originHeight=1032&originWidth=2372&originalType=binary&ratio=2&rotation=0&showTitle=false&size=301467&status=done&style=none&taskId=u2dca71ca-84b3-48aa-8f52-f746797fcd1&title=&width=1186)


# 使用create-vue搭建Vue3项目

## 1. 认识create-vue

> create-vue是Vue官方新的脚手架工具，底层切换到了 vite （下一代前端工具链），为开发提供极速响应


![image.png](https://cdn.nlark.com/yuque/0/2023/png/274425/1678178479590-ac164009-4a72-4448-85bf-67dc13f3d0c4.png#averageHue=%23feefbe&clientId=ud0819acc-4d21-4&from=paste&height=402&id=u05a93b8e&name=image.png&originHeight=804&originWidth=1606&originalType=binary&ratio=2&rotation=0&showTitle=false&size=221602&status=done&style=none&taskId=uf227924e-280a-4766-add6-d34b9331b0d&title=&width=803)

## 2. 使用create-vue创建项目

> 前置条件 - 已安装16.0或更高版本的Node.js

执行如下命令，这一指令将会安装并执行 create-vue

```bash
npm init vue@latest
```

![image.png](https://cdn.nlark.com/yuque/0/2023/png/274425/1678178685782-71a3b311-423d-4528-aae9-85e6068db452.png#averageHue=%23333332&clientId=ud0819acc-4d21-4&from=paste&height=477&id=u807a99d3&name=image.png&originHeight=954&originWidth=1364&originalType=binary&ratio=2&rotation=0&showTitle=false&size=488023&status=done&style=none&taskId=u4d75c82e-6b19-48a6-a9df-0ee44d9e92c&title=&width=682)

> <font color='gree'>*ts*</font>
>
> <font color='gree'>*jsx*</font>: reast 语法扩展
>
> <font color='gree'>*vue router*</font>
>
> <font color='gree'>*pinia*</font>：vuex替换升级
>
> <font color='gree'>*vitest*</font>：新一代测试框架
>
> <font color='gree'>*end to end testing solution*</font>：（E2E）（链测试）端到端测试 [详情](https://blog.csdn.net/seagal890/article/details/113800614)
>
> <font color='gree'>*ESlint*</font>：是一个静态代码分析工具，可以帮助开发者检查代码存在的语法问题
>
> <font color='gree'>*Prettier*</font> ： 前端代码格式化工具

# 熟悉项目和关键文件

![image.png](https://cdn.nlark.com/yuque/0/2023/png/274425/1678178749511-f4a42cbf-987b-46a7-9a01-9cd4f00a5fcf.png#averageHue=%23f1f1ef&clientId=ud0819acc-4d21-4&from=paste&height=541&id=u1ac1e797&name=image.png&originHeight=1082&originWidth=2256&originalType=binary&ratio=2&rotation=0&showTitle=false&size=595592&status=done&style=none&taskId=u38211dc7-742f-4d49-84f3-39a837eb254&title=&width=1128)

# 组合式API - setup选项

## 1. setup选项的写法和执行时机

写法

```vue
<script>
  export default {
    setup(){
      
    },
    beforeCreate(){
      
    }
  }
</script>
```

执行时机

> 在beforeCreate钩子之前执行

![image.png](https://cdn.nlark.com/yuque/0/2023/png/274425/1678179048672-603fdc19-4a41-4542-af55-702776625358.png#averageHue=%23fefefd&clientId=ud0819acc-4d21-4&from=paste&height=453&id=uf8697cce&name=image.png&originHeight=906&originWidth=1248&originalType=binary&ratio=2&rotation=0&showTitle=false&size=182575&status=done&style=none&taskId=u2cd1d681-f573-4456-9ddb-d2ab1f41805&title=&width=624)

## 2. setup中写代码的特点

> <font color='gree'>在setup函数中写的数据和方法需要在末尾以对象的方式return，才能给模版使用</font>

```vue
<script>
  export default {
    setup(){
      const message = 'this is message'
      const logMessage = ()=>{
        console.log(message)
      }
      // 必须return才可以
      return {
        message,
        logMessage
      }
    }
  }
</script>
```

## 3. `<script setup>`语法糖

> <font color='gree'>`script`标签添加 `setup`标记，不需要再写导出语句，默认会添加导出语句</font>

```vue
<script setup>
  const message = 'this is message'
  const logMessage = ()=>{
    console.log(message)
  }
</script>
```

![](C:\Users\shizeyu\Desktop\notes\Ajax-vue\Snipaste_2023-08-24_16-09-58.jpg)

# 组合式API - reactive和ref函数

## 1. reactive

> 接受<font color='gree'>对象类型数据的参数传入并返回一个响应式的对象</font>


```vue
<script setup>
 // 导入
 import { reactive } from 'vue'
 // 执行函数 传入参数 变量接收
 const state = reactive({
   msg:'this is msg'
 })
 const setSate = ()=>{
   // 修改数据更新视图
   state.msg = 'this is new msg'
 }
</script>

<template>
  {{ state.msg }}
  <button @click="setState">change msg</button>
</template>
```

## 2. ref

> <font color='gree'>接收简单类型或者对象类型的数据传入并返回一个响应式的对象</font> 
>
> <font color='gree'>脚本区域修改 `ref` 产生的响应式对象数据 必须通过 `.value` 属性</font>

```vue
<script setup>
 // 导入
 import { ref } from 'vue'
 // 执行函数 传入参数 变量接收
 const count = ref(0)
 const setCount = () => {
   // 修改数据更新视图必须加上.value
   count.value++
 }
</script>

<template>
  <button @click="setCount">{{count}}</button>
</template>
```

若打印 count ：

![](C:\Users\shizeyu\Desktop\notes\Ajax-vue\Snipaste_2023-08-24_16-20-11.jpg)

## 3. reactive 对比 ref

1. 都是用来生成响应式数据
2. 不同点
   1. reactive不能处理简单类型的数据
   2. ref参数类型支持更好，但是必须通过.value做访问修改
   3. ref函数内部的实现依赖于reactive函数
   4. reactive 默认开启 deep 深度监听
3. 在实际工作中的推荐
   1. <font color='gree'>推荐使用ref函数</font>，减少记忆负担，小兔鲜项目都使用ref

# 组合式API - computed

> 计算属性基本思想和Vue2保持一致，组合式API下的计算属性<font color='gree'>只是修改了API写法</font>

> 核心步骤：
>
> 1. 导入 computed 函数
> 2. 执行函数 在回调参数中`return`基于响应式数据做计算的值，用变量接收

```vue
<script setup>
// 导入
import {ref, computed } from 'vue'
// 原始数据
const count = ref(0)
// 计算属性
const doubleCount = computed(() => count.value * 2)

// 原始数据
const list = ref([1,2,3,4,5,6,7,8])
// 计算属性list
const filterList = computed(item => item > 2)
</script>
```

> <font color='gree'>跟 vue2 一样 计算属性的值是只读的（通常）</font>

# 组合式API - watch

> 侦听<font color='gree'>一个或者多个数据的变化</font>，数据变化时执行回调函数，俩个额外参数 immediate控制立刻执行，deep开启深度侦听

## 1. 侦听单个数据

```vue
<script setup>
  // 1. 导入watch
  import { ref, watch } from 'vue'
  const count = ref(0)
  // 2. 调用watch 侦听变化
  watch(count, (newValue, oldValue)=>{
    console.log(`count发生了变化，老值为${oldValue},新值为${newValue}`)
  })
</script>
```

## 2. 侦听多个数据

> 侦听多个数据，第一个参数可以改写成数组的写法

```vue
<script setup>
  // 1. 导入watch
  import { ref, watch } from 'vue'
  const count = ref(0)
  const name = ref('cp')
  // 2. 调用watch 侦听变化
  watch([count, name], ([newCount, newName],[oldCount,oldName])=>{
    console.log(`count或者name变化了，[newCount, newName],[oldCount,oldName])
  })
</script>
```

## 3. immediate

> 在侦听器<font color='gree'>创建时立即出发回调</font>，响应式数据变化之后继续执行回调


```vue
<script setup>
  // 1. 导入watch
  import { ref, watch } from 'vue'
  const count = ref(0)
  // 2. 调用watch 侦听变化
  watch(count, (newValue, oldValue)=>{
    console.log(`count发生了变化，老值为${oldValue},新值为${newValue}`)
  },{
    immediate: true
  })
</script>
```

## 4. deep

> 通过watch监听的ref对象默认是<font color='gree'>浅层侦听的，直接修改嵌套的对象属性不会触发回调执行，需要开启deep</font>
>
> reactive 默认开启 deep 深度监听

```vue
<script setup>
  // 1. 导入watch
  import { ref, watch } from 'vue'
  const state = ref({ count: 0 })
  // 2. 监听对象state
  watch(state, ()=>{
    console.log('数据变化了')
  })
  const changeStateByCount = ()=>{
    // 直接修改不会引发回调执行
    state.value.count++
  }
</script>

<script setup>
  // 1. 导入watch
  import { ref, watch } from 'vue'
  const state = ref({ count: 0 })
  // 2. 监听对象state 并开启deep
  watch(state, ()=>{
    console.log('数据变化了')
  },{deep:true})
  const changeStateByCount = ()=>{
    // 此时修改可以触发回调
    state.value.count++
  }
</script>

```

## 精确监听对象的某个属性

> 在不开启 deep 的前提下，侦听 age 的变化，只有 age 变化时才执行监听
>
> <font color='gree'>可以把第一个参数写成函数的写法，返回要监听的具体属性</font>

```vue
<script setup>
  // 1. 导入watch
  import { ref, watch } from 'vue'
  const info = ref({ name: 'cp', age: '18' })
  // 2. 监听对象state 并开启deep
  // info -> () => info.value.age
  watch(
    () => info.value.age,
    () => console.log('数据变化了')
  )
  const changeStateByCount = ()=>{
    // 此时修改可以触发回调
    state.value.count++
  }
</script>

```

![](C:\Users\shizeyu\Desktop\notes\Ajax-vue\Snipaste_2023-10-08_16-16-33.jpg)

# 组合式API - 生命周期函数

## 1. 选项式对比组合式

![image.png](https://cdn.nlark.com/yuque/0/2023/png/274425/1678183720098-4d40e806-bc0d-4c38-bcbe-9aed440f6b23.png#averageHue=%23cdd7e8&clientId=ud0819acc-4d21-4&from=paste&height=554&id=uc176ffaf&name=image.png&originHeight=1108&originWidth=2190&originalType=binary&ratio=2&rotation=0&showTitle=false&size=261737&status=done&style=none&taskId=u64291cff-e1f5-4709-ba14-700b20d39e8&title=&width=1095)

## 2. 生命周期函数基本使用

> 1. 导入生命周期函数
> 2. 执行生命周期函数，传入回调

```vue
<scirpt setup>
	import { onMounted } from 'vue'
	onMounted(()=>{
	  // 自定义逻辑
	})
</script>
```

## 3. 执行多次

> 生命周期函数执行多次的时候，会按照顺序<font color='gree'>依次执行</font>

```vue
<scirpt setup>
import { onMounted } from 'vue'
onMounted(()=>{
  // 自定义逻辑
})

onMounted(()=>{
  // 自定义逻辑
})
</script>
```

![](C:\Users\shizeyu\Desktop\notes\Ajax-vue\Snipaste_2023-10-08_16-25-31.jpg)

# 组合式API - 父子通信

## 1. 父传子

> 基本思想
>
> 1. 父组件中给<font color='gree'>子组件绑定属性</font>
> 2. 子组件内部通过<font color='gree'>props选项接收数据</font>
>
> <font color='gree'>`set up`语法糖下局部组件无需注册直接使用</font>

![](https://cdn.nlark.com/yuque/0/2023/png/274425/1678184258336-94b25c26-3150-456b-8981-64017ce7b021.png#averageHue=%2323282f&clientId=ud0819acc-4d21-4&from=paste&height=337&id=u6f845ad3&name=image.png&originHeight=674&originWidth=2402&originalType=binary&ratio=2&rotation=0&showTitle=false&size=416739&status=done&style=none&taskId=ubb5c9d64-f3d7-4a1b-bc05-9bf2af1e24d&title=&width=1201)

> 响应式数据传递：

![](C:\Users\shizeyu\Desktop\notes\Ajax-vue\Snipaste_2023-08-25_16-18-37.jpg)

## 2. 子传 父

> 基本思想
>
> 1. 父组件中给<font color='gree'>子组件标签通过@绑定事件</font>
> 2. 子组件内部通过<font color='gree'> `$emit` 方法触发事件</font>
>
> 相较之前只是增加了 编译器宏
>
> <font color='red'>编译器宏函数就是标识让代码重新编译成 以前 js 代码的函数方法</font>


![image.png](https://cdn.nlark.com/yuque/0/2023/png/274425/1678184380538-99cfc459-3e2e-4d2e-9162-350ef5f97ec6.png#averageHue=%23242830&clientId=ud0819acc-4d21-4&from=paste&height=388&id=u4588c125&name=image.png&originHeight=776&originWidth=2284&originalType=binary&ratio=2&rotation=0&showTitle=false&size=573924&status=done&style=none&taskId=ue5c30a58-7910-4a5b-8325-7e572c6348e&title=&width=1142)

# 组合式API - 模版引用

> 概念：通过<font color='gree'> ref标识 获取真实的 dom对象或者组件实例对象</font>
>
> vue2中：
>
> ![](C:\Users\shizeyu\Desktop\notes\Ajax-vue\Snipaste_2023-10-10_17-05-11.jpg)

## 1. 基本使用

> 实现步骤：
>
> 1. 调用`ref`函数生成一个`ref`对象
> 2. 通过`ref`标识绑定`ref`对象到标签
>
> <font color='gree'>相当dom对象放进ref创造的盒子内的 `value` 上，调用dom内的方法或变量时还是需要加 .value</font>

![image.png](https://cdn.nlark.com/yuque/0/2023/png/274425/1678184653565-b85c6f60-1089-4ad6-bed7-bbf781863db9.png#averageHue=%2324282f&clientId=ud0819acc-4d21-4&from=paste&height=442&id=u45efd4ee&name=image.png&originHeight=884&originWidth=1092&originalType=binary&ratio=2&rotation=0&showTitle=false&size=287093&status=done&style=none&taskId=u8dba8092-8819-44b3-a2ef-769257a611a&title=&width=546)

![](C:\Users\shizeyu\Desktop\notes\Ajax-vue\Snipaste_2023-08-25_16-50-27.jpg)

![](C:\Users\shizeyu\Desktop\notes\Ajax-vue\Snipaste_2023-10-11_10-42-09.jpg)

## 2. defineExpose

> 默认情况下在 `<script setup>`语法糖下<font color='gree'>组件内部的属性和方法是不开放</font>给父组件访问的，可以通过`defineExpose`编译宏<font color='gree'>指定哪些属性和方法容许访问</font>
> 说明：指定testMessage属性可以被访问到

![image.png](https://cdn.nlark.com/yuque/0/2023/png/274425/1678184774906-7486a911-d18c-42e8-9aa7-fe2caa35e104.png#averageHue=%23ecf2ee&clientId=ud0819acc-4d21-4&from=paste&height=292&id=u0d5c6487&name=image.png&originHeight=584&originWidth=2512&originalType=binary&ratio=2&rotation=0&showTitle=false&size=239701&status=done&style=none&taskId=ub87fd095-cc3e-4e44-92f6-7c9643f831a&title=&width=1256)

# 组合式API - provide和inject

## 1. 作用和场景

> 顶层组件向任意的底层组件<font color='gree'>传递数据和方法</font>，实现<font color='gree'>跨层组件通信</font>

![image.png](https://cdn.nlark.com/yuque/0/2023/png/274425/1678185158603-5ae6c0e5-7baa-4de9-8a54-d1864d6c45d3.png#averageHue=%23fdf6ef&clientId=ud0819acc-4d21-4&from=paste&height=596&id=ua50e576b&name=image.png&originHeight=1192&originWidth=2558&originalType=binary&ratio=2&rotation=0&showTitle=false&size=414782&status=done&style=none&taskId=u0792870d-aa73-4c03-8342-aaa56e5d8fb&title=&width=1279)

## 2. <font color='gree'>跨层传递普通数据</font>

> 实现步骤
>
> > <font color='gree'>需要各自引入`provide`和`inject`从`vue`</font>
>
> 1. 顶层组件通过 <font color='gree'>`provide` 函数提供数据</font>
> 2. 底层组件通过 <font color='gree'>`inject` 函数提供数据</font>


![image.png](https://cdn.nlark.com/yuque/0/2023/png/274425/1678185321144-61e96ddf-f56c-4d57-83bc-c3c6899f72b2.png#averageHue=%23e4efe5&clientId=ud0819acc-4d21-4&from=paste&height=435&id=u9eb7aecf&name=image.png&originHeight=870&originWidth=1736&originalType=binary&ratio=2&rotation=0&showTitle=false&size=242848&status=done&style=none&taskId=u3d40b793-c4bc-44e7-83d9-4df25e56a7d&title=&width=868)

## 3. 跨层传递响应式数据

> 在调用provide函数时，第二个参数设置为<font color='gree'>ref对象</font>

![image.png](https://cdn.nlark.com/yuque/0/2023/png/274425/1678185454566-b866e7f4-fa23-4c44-a199-8ca19b7d438e.png#averageHue=%2381b27d&clientId=ud0819acc-4d21-4&from=paste&height=473&id=u4efc7283&name=image.png&originHeight=946&originWidth=1732&originalType=binary&ratio=2&rotation=0&showTitle=false&size=237788&status=done&style=none&taskId=uf829094c-f2f8-4ca1-a8ed-c20f9eb79e4&title=&width=866)

## 4. 跨层传递方法

> 顶层组件可以向底层组件<font color='red'>传递方法</font>，<font color='gree'>底层组件调用方法修改顶层组件的数据</font>
>
> > <font color='red'>谁的数据谁修改</font>所以方法写在顶层组件内，因为数据也是在顶层内

![image.png](https://cdn.nlark.com/yuque/0/2023/png/274425/1678185556536-669d0753-2dda-41ae-a750-b0e32f837d42.png#averageHue=%2394b88e&clientId=ud0819acc-4d21-4&from=paste&height=391&id=u449ca48f&name=image.png&originHeight=782&originWidth=2556&originalType=binary&ratio=2&rotation=0&showTitle=false&size=242321&status=done&style=none&taskId=u80c0e832-0efd-4886-9a15-05ebfb4c772&title=&width=1278)

# 综合案例

![image.png](https://cdn.nlark.com/yuque/0/2023/png/274425/1678185631376-9e6cd19a-0788-42ab-90d4-1103fdbb80db.png#averageHue=%23fefefe&clientId=ud0819acc-4d21-4&from=paste&height=544&id=u35ff8500&name=image.png&originHeight=1088&originWidth=2302&originalType=binary&ratio=2&rotation=0&showTitle=false&size=455015&status=done&style=none&taskId=u6338b36f-65be-420e-af70-914bf97813d&title=&width=1151)

## 1. 项目地址

```bash
git clone  http://git.itcast.cn/heimaqianduan/vue3-basic-project.git
```

## 2. 项目说明

1. 模版已经配置好了案例必须的安装包
2. 案例用到的接口在 README.MD文件 中
3. 案例项目有俩个分支，main主分支为开发分支，complete分支为完成版分支供开发完参考



# 什么是pinia

https://pinia.web3doc.top/core-concepts/getters.html

Pinia 是 Vue 的专属<font color='gree'>状态管理库</font>，可以实现跨组件或页面共享状态，<font color='gree'>是 vuex 状态管理工具的替代品</font>，和 Vuex相比，具备以下优势

1. 提供更加简单的API （去掉了 mutation ）
2. 提供符合组合式API风格的API （和 Vue3 新语法统一）
3. 去掉了modules的概念，每一个store都是一个独立的模块
4. 搭配 TypeScript 一起使用提供可靠的类型推断

# 创建空Vue项目并安装Pinia

### 1. 创建空Vue项目

```bash
npm init vue@latest
```

### 2. 安装Pinia并注册

```bash
npm i pinia
```

```javascript
import { createPinia } from 'pinia'

const app = createApp(App)
// 以插件的形式注册
app.use(createPinia())
app.use(router)
app.mount('#app')
```

![](C:\Users\shizeyu\Desktop\notes\Ajax-vue\Snipaste_2023-10-12_15-43-50.jpg)

# 示例：实现counter

> 核心步骤：
>
> 1. 定义store
> 2. 组件使用store

1- 定义store

```javascript
// stores/counter.js
import { defineStore } from 'pinia'
import { ref } from 'vue'

export const useCounterStore = defineStore('counter', ()=>{
  // 数据 （state）
  const count = ref(0)

  // 修改数据的方法 （action）
  const increment = ()=>{
    count.value++
  }

  // 以对象形式返回
  return {
    count,
    increment
  }
})


----------更建议上面的方法--------------------------------


// stores/counter.js
import { defineStore } from 'pinia'

export const useCounterStore = defineStore('counter', {
  state: () => {
    return { count: 0 }
  },
  // 也可以定义为
  // state: () => ({ count: 0 })
  actions: {
    increment() {
      this.count++
    },
  },
})
```

2- 组件使用store

```vue
<script setup>
  // 1. 导入use方法
	import { useCounterStore } from '@/stores/counter'
  // 2. 执行方法得到store store里有数据和方法
  const counterStore = useCounterStore()
</script>

<template>
	<button @click="counterStore.increment">
    {{ counterStore.count }}
  </button>
</template>
```

# 示例：实现getters

> pinia 的 getters 直接使用<font color='red'> computed函数 </font>计算属性即可实现

```javascript
// 数据（state）
const count = ref(0)
// getter (computed)
const doubleCount = computed(() => count.value * 2)
```

![](C:\Users\shizeyu\Desktop\notes\Ajax-vue\Snipaste_2023-10-12_16-27-58.jpg)

# 异步action

> 思想：action函数既支持同步也支持异步，和在组件中发送网络请求写法保持一致
> 步骤：
>
> 1. store中定义action
> 2. 组件中触发action

1- store中定义action

```javascript
const API_URL = 'http://geek.itheima.net/v1_0/channels'

export const useCounterStore = defineStore('counter', ()=>{
  // 数据
  const list = ref([])
  // 异步action
  const loadList = async ()=>{
    const res = await axios.get(API_URL)
    list.value = res.data.data.channels
  }
  
  return {
    list,
    loadList
  }
})
```

2- 组件中调用action	

```vue
<script setup>
	import { useCounterStore } from '@/stores/counter'
    import { onMounted } from 'vue' 
  const counterStore = useCounterStore()
  // 调用异步action
  onMounted(() => {
      counterStore.loadList()
  })
</script>

<template>
	<ul>
    <li v-for="item in counterStore.list" :key="item.id">{{ item.name }}</li>
  </ul>
</template>
```

# 示例：storeToRefs保持响应式解构

> <font color='gree'>直接基于store进行解构赋值，响应式数据（state和getter）会丢失响应式特性，使用storeToRefs辅助保持响应式</font>
>
> storeToRefs 只负责数据的响应式，方法还是使用原来的方法解构赋值

```js
//响应式丢失 视图不再更新
const { count, doubleCount } = counterStore
//保持数据响应式
const { count, doubleCount } = storeToRefs(counterStore)
```



```vue
<script setup>
  import { storeToRefs } from 'pinia'
  import { useCounterStore } from '@/stores/counter'
  const counterStore = useCounterStore()
  // 使用它storeToRefs包裹之后解构保持响应式
  // 数据解构赋值
  const { count } = storeToRefs(counterStore)

  // 方法解构赋值
  const { increment } = counterStore
  
</script>

<template>
	<button @click="increment">
    {{ count }}
  </button>
</template>
```