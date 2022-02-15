

- [x] Vue实例 
	- [x] 创建一个Vue实例  
	- [x] 数据和方法 
	- [x] 生命周期钩子 
	- [x] 生命周期图示 

- [ ] 模块语法 
  - [x] 插值
    - [x] 文本
    - [x] 原始HTML
    - [x] Attribute
    - [x] 使用JavaScript表达式

  - [x] 指令
    - [x] 参数
    - [x] 动态参数
    - [x] 修饰符

  - [x] 缩写
    - [x] v-bind 缩写   
      
      - ##### v-bind:id  ===  :id
      
    - [x] v-on 缩写
      
        - ##### v-on:click === @click
  
- [x] 计算属性和侦听器 
  - [x] 计算属性
    
    - ##### computed
    
    - [x] 基础例子
    - [x] 计算属性缓存 vs 方法
  - [x] 计算属性 vs 侦听属性
    
    - [x] 计算属性的setter
    
  - [x] 侦听器
  
    - ##### watch
  
- [ ] Class 与 Style 绑定 
  - [ ] 绑定HTML Class
    - [ ] 对象语法
    - [ ] 数组语法
    - [ ] 用在组件上

  - [ ] 绑定内联样式
    - [ ] 对象语法
    - [ ] 数组语法
    - [ ] 自动添加前缀
    - [ ] 多重值

- [ ] 条件渲染 
  - [ ] v-if 
    - [ ] 在<template> 元素上使用 v-if 条件渲染分组
    - [ ] v-else
    - [ ] v-else-if
    - [ ] 用key管理可复用的元素
  - [ ] v-show
  - [ ] v-if 与 v-show
  - [ ] v-if 与 v-for 一起使用

- [ ] 列表渲染 

- [ ] 事件处理 

- [ ] 表单绑定 

- [ ] 组件基础

深入了解组件

- [ ] 注册组件

- [ ] Prop

- [ ] 自定义事件

- [ ] 插槽

- [ ] 动态组件 &amp;&amp; 异步组件 

- [ ] 处理边界情况

过渡 &amp;&amp; 动画

- [ ] 进入/离开 &amp;&amp; 列表过渡

- [ ] 状态过渡



---



## 计算属性和侦听器

### 计算属性与methods异同

>  相同点： 计算属性（computed）与方法（methods）功能基本类似

>  不同点： computed是基于它的依赖缓存，只有相关依赖发生改变时，才会重新取值。而使用methods，在重新渲染的时候，函数总会重新调用执行。可以说使用computed性能会更好。



下列代码将简单介绍计算属性依赖缓存，而methods没有依赖缓存

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <script src="https://cdn.bootcss.com/vue/2.6.0/vue.js"></script>
    <title>Document</title>
</head>
<body>
    <div id="app3">
        <p>原字符串：{{message}}</p>
        <p>计算反转字符串：{{reverseMessage1}}</p>
        <p>计算反转字符串：{{reverseMessage1}}</p>
        <p>计算反转字符串：{{reverseMessage2()}}</p>
        <p>计算反转字符串：{{reverseMessage2()}}</p>
</div>
<script>
  var num = 1;
    new Vue({
        el: "#app3",
        data: {
            message: 'xiaoqi'
        },
        computed: {
            reverseMessage1:function () {
                num += 1;
                return num +  this.message.split('').reverse().join('');
            }
        },
        methods: {
            reverseMessage2() {
                num += 1;
                return num + this.message.split('').reverse().join('');
            }
        }
        
    })	
</script>
</body>
</html>
```

输出结果为下图，发现使用了两次computed方法后，因为计算属性依赖缓存，两次输出的结果都为 第二次计算的结果 : 2iqoaix ；

使用两次methods方法后，因为没有依赖缓存，两次结果为 旧值 + 1 

![计算属性和methods的区别](.\【Vue+Vuex+VueRouter官方文档解析】\计算属性和methods的区别.png)



### 计算属性和侦听器异同

>  computed是同步的，watch可以实现异步 
>
>  computed中的函数都是带返回值的，watch里面的函数可以不写返回值。 


下列代码实现功能： 使用侦听器监听count ，2s后清0

```html
<div id="app">
    {{count}}
    <button @click="count++">点击加一</button>
</div>
<script>
    new Vue({
    el: "#app",
    data: {
        count: 1
    },
    watch: {
        count: function(val) {
            var  that = this;
            window.setTimeout(function() {
                that.count = 0;
            },2000)
        }
    }
    })
</script>
```



### 计算属性实现简单实战

 实例：通过计算属性、指令等实现简单的购物车 

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>计算属性综合案例</title>
    <script src="https://cdn.bootcss.com/vue/2.6.0/vue.js"></script>
    
    <style>
        table {
                border: 1px solid black;
                width: 100%;
            }
        
        th {
            height: 50px;
            }
        th, td {
            border-bottom: 1px solid #ddd;
            text-align: center;
            }
    </style>  
</head>
<body>
    <div id="app">
        <table>
            <tr>
                <th>序号</th>
                <th>商品名称</th>
                <th>购买单价</th>
                <th>购买数量</th>
                <th>操作</th>
            </tr>
            <tr v-for="(result,id) in resultJson" :id="resultJson.id">
                <td>{{result.id}}</td>
                <td>{{result.goodsName}}</td>
                <td>{{result.goodsPrice}}</td>
                <td><button :disabled="result.count == 0" @click="handleClick1(id,result.count)">-</button>{{result.count}}<button  @click="handleClick2(id,result.count)">+</button></td>
                <td><button @click="handleClick3(id,result.count)">移除</button></td>
            </tr>
        </table>
        <h3 >总价格：{{totalprice}}</h3> 
    </div>
    <script>
        var vm = new Vue({
            el: "#app",
            data: {
                    resultJson: [{
                        id: '1',
                        goodsName: '华为',
                        goodsPrice: 5099,
                        count: 1
                    },{
                        id: '2',
                        goodsName: 'xiaomi 6',
                        goodsPrice: 4099,
                        count: 1
                    },{
                        id: '3',
                        goodsName: 'iphone X',
                        goodsPrice: 3099,
                        count: 1
                    }]
            },
            methods: {
                handleClick1(id,count){
                    this.resultJson[id].count -= 1                   
                },
                handleClick2(id,count){
                    this.resultJson[id].count += 1 
                },
                handleClick3(id,count){
                    this.resultJson[id].count = 0
                }
            },
            computed: {
                totalprice(){
                    var price = 0;
                    for(var i = 0; i < this.resultJson.length;  i++){
                        price += this.resultJson[i].count * this.resultJson[i].goodsPrice
                    }
                    return price
                }
            }
        })

    </script>
</body>
</html
```

![计算属性综合实战](.\【Vue+Vuex+VueRouter官方文档解析】\计算属性综合实战.png)

[参考文章](https://blog.csdn.net/qq_41257129/article/details/90257492)



## 生命周期钩子





| 函数          | 调用时间              |
| ------------- | --------------------- |
| beforeCreate  | vue实例初始化之前调用 |
| created       | vue实例初始化之后调用 |
| beforeMount   | 挂载到DOM树之前调用   |
| mounted       | 挂载到DOM树之后调用   |
| beforeUpdate  | 数据更新之前调用      |
| updated       | 数据更新之后调用      |
| beforeDestroy | vue实例销毁之前调用   |
| destroyed     | vue实例销毁之后调用   |

下面结合代码和浏览器控制台打印的日志，查看Vue的8个主要生命周期钩子

### 1. beforeCreate：

 这个阶段vue实例刚刚在内存中创建，此时data和methods这些都没初始化好。

### 2. created：

 这个阶段vue实例在内存中已经创建好了，data和methods也能够获取到了，但是模板还没编译。
 ![beforeCreate+created](E:\Typora_workspace\学习\前端\笔记\VUE\【Vue+Vuex+VueRouter官方文档解析】\beforeCreate+created.png)

### 3. beforeMount：

 这个阶段完成了模板的编译，但是还没挂载到页面上。

### 4. mounted：

 这个阶段，模板编译好了，也挂载到页面中了，页面也可以显示了。

![beforeMount+mounted](E:\Typora_workspace\学习\前端\笔记\VUE\【Vue+Vuex+VueRouter官方文档解析】\beforeMount+mounted.png)

### 5. beforeUpdate:

 转态更新之前执行此函数，此时data中数据的状态值已经更新为最新的，但是页面上显示的数据还是最原始的，还没有重新开始渲染DOM树。

先改变data里数据：

```javascript
vm.information = 'danny is noy my name';
```

### 6. updated：

 这个阶段是转态更新完成后执行此函数，此时data中数据的状态值是最新的，而且页面上显示的数据也是最新的，DOM节点已经被重新渲染了。

![beforeUpdate+updated](E:\Typora_workspace\学习\前端\笔记\VUE\【Vue+Vuex+VueRouter官方文档解析】\beforeUpdate+updated.png)

### 7. beforeDestroy：

 beforeDestroy阶段处于vue实例被销毁之前，当然，这个阶段vue实例还能用。

 销毁Vue实例：

```javascript
 vm.$destroy();
```

### 8. destroyed：

 这个阶段在vue实例销毁后调用，此时所有实例指示的所有东西都会解除绑定，事件监听器也都移除，子实例也被销毁。

![beforeDestroy+destroyed](E:\Typora_workspace\学习\前端\笔记\VUE\【Vue+Vuex+VueRouter官方文档解析】\beforeDestroy+destroyed.png)

 **官方文档里的生命周期图** :

![生命周期钩子图](.\【Vue+Vuex+VueRouter官方文档解析】\生命周期钩子图.png)





```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <script src="https://cdn.bootcss.com/vue/2.4.2/vue.js"></script>
</head>
<body>

    <div id="app">
        {{information}}
    </div>
    
    <script>
        var vm = new Vue({
            el: "#app",
            data: {
                information: "My name is danny"
            },
            beforeCreate: function(){
             // 传入该阶段简介与this，this就是该阶段的vue实例
                  show('beforeCreate vue实例初始化之前',this);
            },
            created: function(){
                    show('created vue实例初始化之后',this);
            },
            beforeMount: function(){
                show('beforeMount 挂载之前',this);
            },
            mounted: function(){
                show('mounted 挂载结束之后',this);
            },
            beforeUpdate: function(){
                show('beforeUpdate 更新前状态',this);
            },
            updated: function(){
                show('updated 更新后状态',this);
            },
            beforeDestroy: function() {
                show('beforeDestroy 销毁之前',this);
            },
            destroyed: function() {
                show('destroyed 销毁之后',this);
            } 
        })

        function show(inf, obj){
            console.group("%c%s",'color:red',inf);
            console.log("------------------------------------------");
            console.log('获取vue实例data里的数据: ' + obj.information);
            // console.log(obj.information);
            console.log("------------------------------------------");
            console.log('挂载的对象，就是DOM：' + obj.$el);
            // console.log(obj.$el);
            console.log("------------------------------------------");
            console.log('页面上已经挂载的DOM：' + document.getElementById('app').innerHTML);
            // console.log(document.getElementById('app').innerHTML);
        }

    </script>
</body>
</html>
```



![生命周期钩子代码日志解析](.\【Vue+Vuex+VueRouter官方文档解析】\生命周期钩子代码日志解析.png)



[参考文档1](https://bbs.huaweicloud.com/blogs/278913)

[参考文档2](https://segmentfault.com/a/1190000011381906)

