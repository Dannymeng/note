## CSS

### px,em,ren,vm,vh的区别是什么

面试口诀： 一绝三香（相）

>  px :  **绝**对单位，网页开发基础长度单位，即1像素
>
> em： **相**对单位，相对当前盒子字体大小进行计算
>
> rem： **相**对单位，相对根元素html字体大小进行计算
>
> vm+vh : **相**对单位，相对当前网页视口宽度和高度进行计算



### 如何实现左边定宽，右边自适应

**非严格意义**（需要手动修改）

> float + calc
>
> inline-block-calc
>
> position + padding

**严格意义（重点）** 

> flex 布局   (第二个元素 : flex: 1)
>
> table布局  （display: table-cell）
>
> grid布局    (父级元素   display: grid  ； grid-template-columns: 200px auto;)



```html
  <div class="box-wrapper">
    <div class="left-box">
      left-box 
    </div>
    <div class="right-box">
      right-box
    </div>
  </div>
```

flex

```
   .box-wrapper {
      width: 600px;
      height: 400px;
      border:1px solid #000;
      /* flex布局 */
      display: flex;
    }   

    .left-box {
      width: 200px;
      height: 100%;
      background: red;
    }
  
    .right-box {
      background: blue;
      flex: 1;
    }
```

table布局

```html
  .box-wrapper {
      width: 600px;
      height: 400px;
      border: 1px solid #000;
      /* table 布局 */
      display: table;
    }

    .left-box {
      width: 200px;
      height: 100%;
      background: red;
      display: table-cell;
    }
  
    .right-box {
      height: 100%;
      background: blue;
      display: table-cell;
    }
```

grid :



```html
  .box-wrapper {
      width: 600px;
      height: 400px;
      border:1px solid #000;
      display: grid;
      /* 声明列的宽度 */
      grid-template-columns: 200px auto;
    }

    .left-box {
      background: red;
    }
    .right-box {
      background: blue;
    }
```

float + calc

```html
    .box-wrapper {
      width: 600px;
      height: 400px;
      border: 1px solid #000;
    }
    .left-box {
      float:left;
      width: 200px;
      height: 100%;
      background: red;
    }
    .right-box {
      float: right;
      width: calc(100% - 200px);
      height: 100%;
      background: blue;
    }
```



### 如何实现绝对居中

定宽高

> 绝对定位 + 负margin值
>
> 绝对定位 + margin auto

不定宽高

> 绝对定位 + transform
>
> table-cell
>
> flex布局



```html
<div class="box-wrapper">
    <div class="box"></div>
</div>

```



（定宽高）绝对定位 + 负margin值

```html
    .box-wrapper {
      width: 300px;
      height: 300px;
      border: 1px solid red;
      /* 关键因素 */
      position: relative;
    }

    .box {
      width: 100px;
      height: 100px;
      background: blue;
      /* 关键因素 */
      position: absolute;
      left: 50%;   
      top: 50%;   
      margin-left: -50px;
      margin-top: -50px;
    }
```

（定宽高）绝对定位 + margin auto

```html
    .box-wrapper {
      width: 300px;
      height: 300px;
      border: 1px solid red;
      /* 关键因素 */
      position: relative;
    }

    .box {
      width: 100px;
      height: 100px;
      background: blue;
      /* 关键因素 */
      position: absolute;
      top: 0;
      left: 0;
      right: 0;
      bottom: 0;
      margin: auto;
    }
```



（不定宽高）绝对定位 + transform

```html
    .box-wrapper {
      width: 200px;
      height: 200px;
      border: 1px solid red;
      /* 关键因素 */
      position: relative;
    }

    .box {
      background: yellow;
      /* 关键因素 */
      position: absolute;
      left: 50%;
      top: 50%;
      transform: translate(-50%, -50%);
    }
```

(不定宽高) table-cell

```html
    .box-wrapper {
      width: 300px;
      height: 300px;
      border: 1px solid red;
      /* 关键因素 */
      display: table-cell;
      vertical-align: middle; /* 把此元素放置在父元素的中部。 */
      text-align: center;
    }

    .box {
      /* 关键因素 */
      background: yellow;
      display: inline-block;
    }
```

(不定宽高) flex布局

```html
    .box-wrapper {
      width: 300px;
      height: 300px;
      border: 1px solid red;
      /* 关键因素 */
      display: flex;
      justify-content: center;      /* 横轴上居中显示 */
      align-items: center;  /* 纵轴上居中显示 */
    }
  
    .box {
      background: blue;
    }
```







 

