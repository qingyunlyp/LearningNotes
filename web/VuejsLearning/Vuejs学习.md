# Vuejs学习

## 认识Vue

### 为什么学习Vuejs？

- 公司原有项目使用Vue进行重构
- 公司新项目使用Vue的技术栈
- 换工作，招聘前端的需求中，10个有8个对Vue有或多或少的要求
- 知道Vuejs非常火，是前端必备的技能

### 简单认识Vuejs

- Vue（读音/vjuː/,类似于view），不要读错。

- Vue是一个渐进式的框架，什么是渐进式呢？

  > 渐进式意味着你可以将Vue作为应用的一部分嵌入其中，带来更丰富的交互体验	
  >
  > 如果你希望将更多的业务逻辑使用Vue实现，那么由Vue的核心库以及其生态系统，比如`Core`+`Vue-router`+`Vuex`，可以满足各种各样的需求

- Vue有很多特点和web开放中常见的高级功能。

  > 解耦视图和数据
  >
  > 可复用的组件
  >
  > 前端路由技术
  >
  > 状态管理
  >
  > 虚拟DOM

- 学习Vuejs的前提

  > 不需要具备其他类似于Anglar、React，甚至是JQuery的经验。
  >
  > 需要一定的HTML、CSS、JavaScript基础

## Vuejs安装

### 安装方式

#### 直接CDN引入

```html
<!--v2官方文档 开发环境版本，包含了有帮助的命令行警告 -->
<script src="https://cdn.jsdelivr.net/npm/vue@2/dist/vue.js"></script>
<!--v2官方文档 生产环境版本，优化了尺寸和速度 -->
<script src="https://cdn.jsdelivr.net/npm/vue@2"></script>
<!--v3官方文档-->
<script src="https://unpkg.com/vue@3/dist/vue.global.js"></script>
```

#### 下载和引入

- **开发环境：**`<script src="./js/vue.js"></script>`
- **生产环境：**`<script src="./js/vue.min.js"></script>`

#### npm安装

 用webpack和CLI的使用该方式

## Vuejs初体验

### hello Vuejs

```html
<div id="app">{{message}}</div>
<script src="./js/vue.js"></script>
<script>
    //  let（变量）/const（常量）
    // 编程范式：声明式编程
    const app = new Vue({
        el:"#app",  //用于挂载管理的元素
        data:{//定义数据
            message:"Vue初体验", 
        }
    })
    // 元素js的做法（编程范式：命令式编程）
    // 1.创建元素，设置id属性
    // 2.定义一个变量message
    // 3.将message变量放在前面的div元素中显示
    // 4.修改message数据
    // 5.将修改后的数据替换到div元素
</script>
```

![image-20221014214359181](https://gitee.com/qingyunlyp/picstore/raw/master/img/202210142143228.png)

#### 代码做了什么？

- 创建了一个Vue对象

- 创建Vue对象的时候传入了一些`options:{}`

  > `{}`中包含了`el`属性，该属性决定了这个对象挂载到哪一个元素上，很明显，我们这里挂载到了id为app的元素上
  >
  > `{}`中包含了`data`属性，该属性会存储一些**数据**
  >
  > > 这些数据可以是我们直接定义出来的，比如上面这样
  > >
  > > 也可能来自网络，从服务器加载

- 浏览器执行代码流程D:\LearningNotes\LearningNotes\web\VuejsLearning\code\01.Vue初体验.html D:\LearningNotes\LearningNotes\web\VuejsLearning\code\02.Vue列表展示.html

  执行到10行代码，显示出对应的HTML

  执行到13行代码创建Vue实例，并且对原HTML进行解析和修改

- 目前代码可以做到响应式

### Vue列表展示

```html
<div id="app">
    <div class="animes">
        <ul v-for="item in animes">
            <li>{{item}}</li>
        </ul>
    </div>
</div>
<script src="./js/vue.js"></script>
<script>
    const app = new Vue({
        el:"#app",
        data:{
            animes:['海贼王','火影忍者','死神','盾之勇者成名录','尸兄']  
        }
    })
</script>
```

![image-20221014221754111](https://gitee.com/qingyunlyp/picstore/raw/master/img/202210142217164.png)

**列表数据：**从服务器请求一个列表，将列表展示在HTML

- 在html中使用v-for指令
- 数据是响应式，数据变化，展示也会变化

### 案例计数器

```html
<div id="app">
    当前计数：{{num}}
    <button v-on:click="add">+1</button>
    <button v-on:click="sub">-1</button>
</div>
<script src="./js/vue.js"></script>
<script>
    const app = new Vue({
        el:"#app",
        methods:{
            add:function(){
                console.log("执行add");
                this.num++;
            },
            sub:function(){
                console.log("执行sub");
                this.num--;
            }
        },
        data:{
            num:0
        }
    })
</script>
```

小计数器：

点击+1：num+1；<br>点击-1：num-1；

- 使用`methods`属性，用于在Vue对象中定义方法。
- 使用`@click`指令监听某个元素的点击事件（方法在`methods`中定义）

## Vuejs的MVVM

MVVM实际上是M、V、VM，即Model、View、ViewModel的缩写，是一种基于前端开发的构架模式。

Vue中的MVVM

![Vue MVVM](https://gitee.com/qingyunlyp/picstore/raw/master/img/202210151240606.jpg)

- DOM Listeners：DOM监听（实际上就是事件监听，v-model底层也用到了事件）
- DOM Binding：数据绑定（数据填充到视图层）
- Plain JavaScript Object：普通的JavaScript对象

1. **View层：**<br>	==视图层==，在开发中，通常就是DOM层，主要作用就是给用户展示各种信息。
2. **Model层：**<br>	==数据层==，数据可能是我们固定的死数据，但更多的是来自服务器，从网络上请求下来的数据。
3. **ViewModel层：**<br>	==视图模型层==，视图模型层是View和Model沟通的桥梁。一方面它实现了数据绑定（Data Binding）,将Model的改变实时的反应到View中；另一方面实现了DOM监听（DOM Listener），当DOM发生一些事件时，可以监听到，并在需要的情况下改变对应的Data

![image-20221015110836420](https://gitee.com/qingyunlyp/picstore/raw/master/img/202210151108510.png)

## Vue的options选项

创建Vue实例的时候，会传入对象options。

**options可以包含那些选项呢？**<br>[详情解析](https://v2.cn.vuejs.org/v2/api/)：[API — Vue.js (vuejs.org)](https://v2.cn.vuejs.org/v2/api/)

**其中最基础的有：**

- **`el`**:

  > **类型:**`string | HTMLElement`
  >
  > **作用：**决定之后Vue实例会管理哪一个DOM

- **`data`**:

  > **类型:**`Object | Function（组件中data必须是一个函数）`
  >
  > **作用：**Vue实例对应的数据对象

- **`methods`**:

  > **类型:**`{[key:string]:Function}`
  >
  > **作用：**定义属于Vue的一些方法，可以在其他地方调用，也可以在指令中使用

## Vue生命周期

![image-20221015110836420](https://gitee.com/qingyunlyp/picstore/raw/master/img/202210151804492.png)











