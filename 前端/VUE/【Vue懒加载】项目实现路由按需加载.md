# 【Vue路由懒加载】项目实现路由按需加载

为什么使用Vue懒加载？

> 如果Vue不使用懒加载，运用webpack打包后的文件会异常的大，导致进入首页时需要加载的内容过多，出现长时间白屏的情况，即使是做了loading也是不利于用户体验的，但是运用懒加载则可以将页面进行划分，需要的时候加载页面，可以有效的分担首页所承担的加载压力，减少首页加载用时。


## 1、未使用懒加载
```javascript

import Vue from 'vue'
import Router from 'vue-router'
import HelloWorld from '@/components/HelloWorld' //import

Vue.use(Router)

export default new Router({
  routes: [
    {
      path: '/',
      name: 'HelloWorld',
      component: HelloWorld   //加载到页面
    }
  ]
})
```


##  2、Vue异步组件实现懒加载

- 方法如下：component：resolve=>(require(['需要加载的路由的地址'])，resolve)

```javascript
import Vue from 'vue'
import Router from 'vue-router'
/* 此处省去之前导入的HelloWorld模块 */
Vue.use(Router)

export default new Router({
  routes: [
    {
      path: '/',
      name: 'HelloWorld',
      component: resolve=>(require(["@/components/HelloWorld"],resolve))
    }
  ]
})
```

## 3、ES 提出的import方法，**（------最常用------）**

- 方法如下：const HelloWorld = （）=>import('需要加载的模块地址')

（不加 { } ，表示直接return）

```javascript
import Vue from 'vue'
import Router from 'vue-router'
Vue.use(Router)

const HelloWorld = ()=>import("@/components/HelloWorld")
export default new Router({
  routes: [
    {
      path: '/',
      name: 'HelloWorld',
      component:HelloWorld
    }
  ]
})
```


##  4、组件懒加载
与路由懒加载相同

1、原来组件中写法

```html
<template>
  <div class="hello">
  <One-com></One-com>
  1111
  </div>
</template>

<script> 
  import One from './one'
  export default {
    components:{
      "One-com": One
    },
    data () {
      return {
        msg: 'Welcome to Your Vue.js App'
      }
    }
  }
</script>
```

2、const方法

```html
<template>
  <div class="hello">
  <One-com></One-com>
  1111
  </div>
</template>

<script> 
    const One = ()=>import("./one");
    export default {
      components:{
        "One-com": One
      },
      data () {
        return {
          msg: 'Welcome to Your Vue.js App'
        }
      }
    }
</script>
```

3、异步方法

```html

<template>
  <div class="hello">
  <One-com></One-com>
  1111
  </div>
</template>

<script>
  export default {
    components:{
      "One-com":resolve=>(['./one'],resolve)
    },
    data () {
      return {
        msg: 'Welcome to Your Vue.js App'
      }
    }
  }
</script>
```



## **总结**

路由和组件的常用两种懒加载方式：

- 1、**Vue异步组件实现路由懒加载**

    component：resolve=>(['需要加载的路由的地址'，resolve])

- 2、**ES提出的import(推荐使用这种方式)**

   **const HelloWorld = （）=>import('需要加载的模块地址')**



**参考文档**

  - [博客1](https://www.cnblogs.com/xiaoxiaoxun/p/11001884.html)