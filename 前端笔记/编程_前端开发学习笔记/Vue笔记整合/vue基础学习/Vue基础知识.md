# Vue核心 Vue简介 初识

### 1.1. Vue 简介

#### 1.1.1. 官网

-  [英文官网](https://vuejs.org/)
-  [中文官网](https://cn.vuejs.org/)

#### 1.1.2. 介绍与描述

- **Vue** 是一套用来动态**构建用户界面**的**渐进式** JavaScript`框架

- - **构建用户界面**：把数据通过某种办法变成用户界面
  - **渐进式：** Vue`可以自底向上逐层的应用，简单应用只需要一个轻量小巧的核心库，复杂应用可以引入各式各样的`Vue`插件

-  作者：尤雨溪

![img](https://cdn.nlark.com/yuque/0/2022/png/1379492/1643034892163-5a414e93-a9a1-45c1-ad72-89bbf4f4eba5.png)

#### 1.1.3. Vue 的特点

1.  遵循`MVVM`模式 
2.  编码简洁，体积小，运行效率高，适合移动/PC端开发 

1.  它本身只关注 UI，可以引入其它第三方库开发项目
2. 采用**组件化**模式，提高代码复用率、且让代码更好维护

![img](https://cdn.nlark.com/yuque/0/2022/png/1379492/1643035195917-eb463d5c-5a77-43a6-914e-dd0f83b0ff80.png)

1. **声明式**编码，让编码人员无需直接操作`DOM`，提高开发效率

![img](https://cdn.nlark.com/yuque/0/2022/png/1379492/1643035526209-9cdf929a-b3db-4997-b1fe-74fd203037d8.png)

- 使用**虚拟DOM** 和 **Diff算法**，尽量复用`DOM`节点

![img](https://cdn.nlark.com/yuque/0/2022/png/1379492/1643035897962-d84f5075-0fd7-4d52-ad8c-31371d98bb08.png)

#### 1.1.4.与其他 JS 框架的关联

- 借鉴 angular 的 **模板** 和 **数据绑定** 技术
- 借鉴 react 的 **组件化** 和 **虚拟DOM** 技术

#### 1.1.5. Vue 周边库

- vue-cli：vue 脚手架
- vue-resource(axios)：ajax 请求

- vue-router：路由
- vuex：状态管理（它是 vue 的插件但是没有用 vue-xxx 的命名规则）

- vue-lazyload：图片懒加载
- vue-scroller：页面滑动相关

- mint-ui：基于 vue 的 UI 组件库（移动端）
- element-ui：基于 vue 的 UI 组件库（PC 端）

### 1.2. 初识 Vue

**前置工作**

1. 给浏览器安装 [**Vue Devtools**](https://cn.vuejs.org/v2/guide/installation.html#Vue-Devtools) 插件
2. 标签引入`Vue`包

1. （可选）阻止`vue`在启动时生成生产提示 **Vue.config.productionTip = false** 
2. **favicon** 需要将页签图标放在项目根路径，重新打开就有了（**shfit+F5** 强制刷新）

**初识Vue**

1. 想让`Vue`工作，就必须创建一个`Vue实例`，且要传入一个**配置**对象
2. root 容器里的代码依然符合`html规范`，只不过混入了一些特殊的`Vue语法`

1. root 容器里的代码被称为**Vue模板**
2. Vue 实例与容器是**一一对应**的

1. 真实开发中只有一个`Vue实例`，并且会配合着组件一起使用
2. **{{xxx}}**中的 xxx 要写 **js 表达式**，且 xxx 可以自动读取到`data`中的所有属性

**注意区分**：js 表达式 和 js代码（语句）

1. 1. 表达式：一个表达式会产生一个值，可以放在任何一个需要值的地方

a	a+b		demo(1)		x === y ? 'a' : 'b'

1. 1. js代码（语句）

if(){}		for(){}

1. 一旦`data`中的数据发生变化，那么模板中用到该数据的地方也会自动更新

```html
<!DOCTYPE html>
<html>
  <head>
    <meta charset="UTF-8" />
    <title>初识Vue</title>

    <!-- 引入Vue -->
    <script type="text/javascript" src="../js/vue.js"></script>

  </head>
  <body>

    <!-- 准备好一个容器 -->
    <div id="demo">
      <h1>Hello，{{ name.toUpperCase() }}，{{ address }}</h1>
    </div>

    <script type="text/javascript" >
      Vue.config.productionTip = false //阻止 vue 在启动时生成生产提示。

      // 创建Vue实例
      new Vue({
        el: '#demo',	// el用于指定当前Vue实例为哪个容器服务，值通常为css选择器字符串
        data: { 			// data中用于存储数据，数据供el所指定的容器去使用，值暂时先写成一个对象
          name: 'cess',
          address: '成都'
        }
      })
    </script>
  </body>
</html>
```

![img](https://cdn.nlark.com/yuque/0/2022/png/1379492/1643091131853-569879e9-abbb-428c-b9c8-c8d1b39d1c23.png)

# Vue核心 模板语法 数据绑定

### 1.3. 模板语法

`Vue`模板语法包括两大类

1. **插值语法**

功能：用于解析标签体内容

写法：**{{xxx}}**，xxx 是 **js 表达式**，可以直接读取到 data 中的所有区域

1. **指令语法** 

功能：用于解析标签（包括：标签属性、标签体内容、绑定事件…）

举例：**<a** **v-bind:** **href="xxx">** 或简写为 **<a**  **: ** **href="xxx">**，xxx 同样要写 **js 表达式**，可以直接读取到 data 中的所有属性

备注：`Vue`中有很多的指令，且形式都是 **v-xxx**，此处只是拿`v-bind`举例

```html
<!DOCTYPE html>
<html>
  <head>
    <meta charset="UTF-8" />
    <title>模板语法</title>
    <!-- 引入Vue -->
    <script type="text/javascript" src="../js/vue.js"></script>
  </head>
  <body>

    <div id="root">
      <h2>插值语法</h2>
      <h4>你好，{{ name }}</h4>
      <hr />
      <h2>指令语法</h2>
      <a v-bind:href="tencent.url.toUpperCase()" x="hello">点我去看{{ tencent.name }}1</a>
      <a :href="tencent.url" x="hello">点我去看{{ tencent.name }}2</a>
    </div>
  </body>

  <script type="text/javascript">
    Vue.config.productionTip = false //阻止 vue 在启动时生成生产提示。

    new Vue({
      el: '#root',
      data: {
        name: 'jack',
        tencent: {
          name: '开端',
          url: 'https://v.qq.com/x/cover/mzc00200mp8vo9b/n0041aa087e.html',
        }
      }
    })
  </script>
</html>
```

![img](https://cdn.nlark.com/yuque/0/2022/png/1379492/1643094836210-5e96118e-1e66-46ca-bef5-3937cb3c02f2.png)

### 1.4. 数据绑定

`Vue`中有2种**数据绑定**的方式

1. 1. 单向绑定**v-bind**数据只能从 data 流向页面
   2. 双向绑定**v-model**数据不仅能从 data 流向页面，还可以从页面流向 data

**备注** 

1. 1. 双向绑定一般都应用在**表单类元素**上，如 `<input>``<select>``<textarea>`等
   2. **v-model:value**可以简写为**v-model**，因为**v-model**默认收集的就是**value**值

```html
<!DOCTYPE html>
<html>
  <head>
    <meta charset="UTF-8" />
    <title>数据绑定</title>
    <!-- 引入Vue -->
    <script type="text/javascript" src="../js/vue.js"></script>
  </head>
  <body>
    
    <div id="root">
      <!-- 普通写法 -->
      <!-- 单向数据绑定：<input type="text" v-bind:value="name"><br/> -->
			<!-- 双向数据绑定：<input type="text" v-model:value="name"><br/> -->

      <!-- 简写 -->
      单向数据绑定：<input type="text" :value="name"><br/>
      双向数据绑定：<input type="text" v-model="name"><br/>

      <!-- 如下代码是错误的，因为 v-model 只能应用在表单类元素（输入类元素）上 -->
      <!-- <h2 v-model:x="name">你好啊</h2> -->
    </div>
    
      <script type="text/javascript">
    Vue.config.productionTip = false // 阻止 vue 在启动时生成生产提示。

    new Vue({
      el: '#root',
      data: {
        name: 'cess'
      }
    })
  </script>
  </body>
</html>
```

![img](https://cdn.nlark.com/yuque/0/2022/png/1379492/1643095682561-25f1b62b-aad3-4a31-a69f-aeed8fbcd6c3.png)

# Vue核心 el与data的两种写法

### 1.5. el 与 data 的两种写法

**el**有2种写法

1. 1. 创建`Vue`实例对象的时候配置**el** 属性
   2. 先创建`Vue`实例，随后再通过const v=new vue(){}      **v.$mount('#root')**指定`el`的值

**data**有2种写法

1. 1. 对象式：**data： { }**
   2. 函数式：**data() { return { } ** **必须有返回值**

如何选择：目前哪种写法都可以，以后到组件时，`data`必须使用函数，否则会报错

一个重要的原则

由`Vue`管理的函数，**一定不要写箭头函数**，否则 **this** 就不再是`Vue实例`了

```html
<!DOCTYPE html>
<html>
  <head>
    <meta charset="UTF-8" />
    <title>el与data的两种写法</title>
    <!-- 引入Vue -->
    <script type="text/javascript" src="../js/vue.js"></script>
  </head>
  
  <body>
    <div id="root">
      <h1>你好，{{name}}</h1>
    </div>
  </body>

  <script type="text/javascript">
    Vue.config.productionTip = false //阻止 vue 在启动时生成生产提示。

    // el的两种写法
    // const v = new Vue({
    // 	//el:'#root', // 第一种写法
    // 	data: {
    // 		name:'cess'
    // 	}
    // })
    // console.log(v)
    // v.$mount('#root') // 第二种写法

    // data的两种写法
    new Vue({
      el: '#root',
      // data的第一种写法：对象式
      // data:{
      // 	name:'cess'
      // }

      //data的第二种写法：函数式
      data() {
        console.log('@@@', this) // 此处的this是Vue实例对象
        return {
          name: 'cess'
        }
      }
    })
  </script>
</html>
```

# Vue核心 MVVM模型 数据代理

### 1.6. MVVM 模型

![img](https://cdn.nlark.com/yuque/0/2022/jpeg/1379492/1643097677438-36b4834c-18e8-4cd0-aa8e-c5f154e6bde0.jpeg)

**MVVM**模型

- M：模型 **Model**，`data`中的数据
- V：视图 **View**，模板代码

- VM：视图模型 **ViewModel**，`Vue实例`

观察发现

- `data`中所有的属性，最后都出现在了`vm`身上
- `vm`身上所有的属性 及`Vue原型`身上所有的属性，在 `Vue模板`中都可以直接使用

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>mvvm</title>
    <script src="../js/vue.js"></script>
</head>
<body>
  
    <div id="root">
        <h2>名称：{{ name }}</h2>
        <h2>战队：{{ rank }}</h2>
        <h2>测试：{{ $options }}</h2>
    </div>

    <script>
        Vue.config.productionTip = false
        new Vue({
            el: '#root',
            data: { 
                name: 'uzi',
                rank: 'RNG'
            }
        })
    </script>
</body>
</html>
```

![img](https://cdn.nlark.com/yuque/0/2022/png/1379492/1643033277589-dac130e9-ec27-4aeb-8d4d-07676879b92f.png)

### 1.7. Vue 中的数据代理

**Object.defineproperty**方法

```javascript
let number = 18
let person = {
  name: '张三',
  sex: '男',
}

Object.defineProperty(person, 'age', {
  // value:18,
  // enumerable:true,		// 控制属性是否可以枚举，默认值是false
  // writable:true,			// 控制属性是否可以被修改，默认值是false
  // configurable:true	// 控制属性是否可以被删除，默认值是false

  // 当有人读取person的age属性时，get函数(getter)就会被调用，且返回值就是age的值
  get() {
    console.log('有人读取age属性了')
    return number
  },

  // 当有人修改person的age属性时，set函数(setter)就会被调用，且会收到修改的具体值
  set(value) {
    console.log('有人修改了age属性，且值是', value)
    number = value
  }

})
// console.log(Object.keys(person))
console.log(person)
```

**数据代理：**通过一个对象代理对另一个对象中属性的操作（读/写）

```javascript
let obj = { x: 100 }
let obj2 = { y: 200 }

Object.defineProperty(obj2, 'x', {
  get() {
    return obj.x
  },
  set(value) {
    obj.x = value
  }
})
```

1. `Vue`中的数据代理通过`vm`对象来代理`data`对象中属性的操作（读/写）
2. `Vue`中数据代理的好处：更加方便的操作`data`中的数据

1. 基本原理

1. 1. 通过**object.defineProperty()** 把`data`对象中所有属性添加到`vm上
   2. 为每一个添加到`vm`上的属性，都指定一个 **getter** **setter**

1. 1. 在**getter** **setter**内部去操作（读/写）data中对 应的属

![img](https://cdn.nlark.com/yuque/0/2022/png/1379492/1643033436297-5d2d61ec-ed69-4706-a98d-afdbd53b383d.png)

`Vue`将`data`中的数据拷贝了一份到**_data**属性中，又将`_data`里面的属性提到`Vue实例`中（如name），通过`defineProperty`实现数据代理，这样通过`geter/setter`操作 name，进而操作`_data`中的 name。而`_data`又对`data`进行数据劫持，实现响应式

```html
<!DOCTYPE html>
<html>
  <head>
    <meta charset="UTF-8" />
    <title>Vue中的数据代理</title>
    <!-- 引入Vue -->
    <script type="text/javascript" src="../js/vue.js"></script>
  </head>
  <body>

    <div id="root">
      <h2>学校名称：{{ name }}</h2>
      <h2>学校地址：{{ address }}</h2>
    </div>

    <script type="text/javascript">
      Vue.config.productionTip = false

      const vm = new Vue({
        el: '#root',
        data: {
          name: '电子科技大学',
          address: '成都'
        }
      })
    </script>

  </body>
</html>

```

# Vue核心 事件处理

### 1.8. 事件处理

#### 1.8.1. 事件的基本用法

1. 使用**v-on:** **xxx**或**@** **xxx**绑定事件，其中 xxx 是事件名
2. 事件的回调需要配置在**methods**对象中，最终会在`vm`上

1. **methods**中配置的函数，**不要用箭头函数**，否则 **this** 就不是**vm**了
2. **methods**中配置的函数，都是被 **Vue**所管理的函数，**this** 的指向是**vm**或**组件实例对象**

1. **@click="demo"**和**@click="demo(** **$event** **)"**效果一致，但后者可以传参

```html
<!DOCTYPE html>
<html>
  <head>
    <meta charset="UTF-8" />
    <title>事件的基本使用</title>
    <!-- 引入Vue -->
    <script type="text/javascript" src="../js/vue.js"></script>
  </head>
  <body>

    <div id="root">
      <h2>欢迎来看{{name}}的笔记</h2>
      <!-- <button v-on:click="showInfo">点我提示信息</button> -->
      <button @click="showInfo1">点我提示信息1（不传参）</button>
      <button @click="showInfo2($event,66)">点我提示信息2（传参）</button>
    </div>

    <script type="text/javascript">
      Vue.config.productionTip = false //阻止 vue 在启动时生成生产提示。

      const vm = new Vue({
        el: '#root',
        data: {
          name: 'cess',
        },
        methods: {
          showInfo1(event) {
            console.log(event.target.innerText)
            // console.log(this) // 此处的this是vm
            alert('同学你好！')
          },
          showInfo2(event, number) {
            console.log(event, number)
            console.log(event.target.innerText)
            // console.log(this) // 此处的this是vm
            alert('同学你好！！')
          }
        }
      })
    </script>
  </body>
</html>
```

![img](https://cdn.nlark.com/yuque/0/2022/png/1379492/1643111598004-c8ad1c7c-2fd6-403a-aeb6-e8020eea7ca5.png)

#### 1.8.2. 事件修饰符

`Vue`中的事件修饰符

1. **prevent**	阻止默认事件（常用）
2. **stop**		阻止事件冒泡（常用）

1. **once**		事件只触发一次（常用）
2. **capture**	使用事件的捕获模式

1. **self**		只有event.target是当前操作的元素时才触发事件
2. **passive**	事件的默认行为立即执行，无需等待事件回调执行完毕

修饰符可以连续写，比如可以这么用：**@click.prevent.stop**="showInfo"

```html
<!DOCTYPE html>
<html>
  <head>
    <meta charset="UTF-8" />
    <title>事件修饰符</title>
    <!-- 引入Vue -->
    <script type="text/javascript" src="../js/vue.js"></script>
    <style>
      * {margin-top: 20px;}
      .demo1 {height: 50px;background-color: skyblue;}
      .box1 {padding: 5px;background-color: skyblue;}
      .box2 {padding: 5px;background-color: white;}
      .list {width: 200px;height: 200px;background-color: skyblue;overflow: auto;}
      li {height: 100px;}
    </style>
  </head>
  <body>

    <div id="root">
      <h2>欢迎来到{{ name }}学习</h2>
      <!-- 阻止默认事件（常用） -->
      <a href="http://www.atguigu.com" @click.prevent="showInfo">点我提示信息</a>

      <!-- 阻止事件冒泡（常用） -->
      <div class="demo1" @click="showInfo">
        <button @click.stop="showInfo">点我提示信息</button>
        <!-- 修饰符可以连续写 -->
        <!-- <a href="http://www.qq.com" @click.prevent.stop="showInfo">点我提示</a> -->
      </div>

      <!-- 事件只触发一次（常用） -->
      <button @click.once="showInfo">点我提示信息</button>

      <!-- 使用事件的捕获模式 -->
      <div class="box1" @click.capture="showMsg(1)">
        div1
        <div class="box2" @click="showMsg(2)">
          div2
        </div>
      </div>

      <!-- 只有event.target是当前操作的元素时才触发事件； -->
      <div class="demo1" @click.self="showInfo">
        <button @click="showInfo">点我提示信息</button>
      </div>

      <!-- 事件的默认行为立即执行，无需等待事件回调执行完毕； -->
      <!-- scroll是滚动条滚动，passsive没有影响 -->
      <!-- wheel是鼠标滚轮滚动，passive有影响 -->
      <ul @wheel.passive="demo" class="list">
        <li>1</li>
        <li>2</li>
        <li>3</li>
        <li>4</li>
      </ul>
    </div>

    <script type="text/javascript">
      Vue.config.productionTip = false

      new Vue({
        el: '#root',
        data: {
          name: '尚硅谷'
        },
        methods: {
          showInfo(e) {
            alert('同学你好！')
            // console.log(e.target)
          },
          showMsg(msg) {
            console.log(msg)
          },
          demo() {
            for (let i = 0; i < 100000; i++) {
              console.log('#')
            }
            console.log('累坏了')
          }
        }
      })
    </script>
  </body>
</html>
```

#### 1.8.3. 键盘事件

键盘上的每个按键都有自己的名称和编码，例如：Enter（13）。而`Vue`还对一些常用按键起了别名方便使用

1. **Vue** **中常用的按键别名**

回车`enter`

删除`delete`捕获“删除”和“退格”键

退出`esc`

空格`space`

换行`tab`特殊，必须配合`keydown`去使用

上`up`

下`down`

左`left`

右`right`

1. `Vue`未提供别名的按键，可以使用按键原始的`key`值去绑定，但注意要转为`kebab-case`（多单词小写短横线写法）
2. 系统修饰键（用法特殊）`ctrl` `alt` `shift` `meta`（`meta`就是`win`键）

1. 1. 配合**keyup**使用：按下修饰键的同时，再按下其他键，随后释放其他键，事件才被触发

指定 ctr+y 使用 **@keyup.ctr.y**

1. 1. 配合 **keydown**  使用：正常触发事件

1. 也可以使用`keyCode`去指定具体的按键（**不推荐**）
2. **Vue.config.keyCodes.自定义键名 = 键码**，可以去定制按键别名

```html
<!DOCTYPE html>
<html>
  <head>
    <meta charset="UTF-8" />
    <title>键盘事件</title>
    <!-- 引入Vue -->
    <script type="text/javascript" src="../js/vue.js"></script>
  </head>
  <body>

    <div id="root">
      <h2>欢迎打开{{name}}笔记</h2>
      <input type="text" placeholder="按下回车提示输入" @keyup.enter="showInfo"><br/>
      <input type="text" placeholder="按下tab提示输入" @keydown.tab="showInfo"><br/>
      <input type="text" placeholder="按下回车提示输入" @keydown.huiche="showInfo"><br/>
    </div>

    <script type="text/javascript">
      Vue.config.productionTip = false	// 阻止 vue 在启动时生成生产提示。
      Vue.config.keyCodes.huiche = 13		// 定义了一个别名按键

      new Vue({
        el: '#root',
        data: {
          name: 'cess'
        },
        methods: {
          showInfo(e) {
            // console.log(e.key,e.keyCode)
            console.log(e.target.value)
          }
        },
      })
    </script>
  </body>
</html>
```

![img](https://cdn.nlark.com/yuque/0/2022/png/1379492/1643114770358-b035234a-22c2-4f99-9b68-b41562654b47.png)

# Vue核心 计算属性 侦听属性

### 1.9. 计算属性

1. 差值语法实现

```html
<title>姓名案例_插值语法实现</title>
<script type="text/javascript" src="../js/vue.js"></script>

<div id="root">
  姓：<input type="text" v-model="firstName"> <br/>
  名：<input type="text" v-model="lastName"> <br/>
  全名：<span>{{ firstName }}-{{ lastName }}</span>
</div>

<script type="text/javascript">
  Vue.config.productionTip = false
  new Vue({
    el:'#root',
    data:{
      firstName:'张',
      lastName:'三'
    }
  })
</script>
```

![img](https://cdn.nlark.com/yuque/0/2022/png/1379492/1643116151610-7e2a1341-f9c2-4f5f-b408-be4a59678d0c.png)

1. `method`实现

**数据发生变化，模板就会被重新解析**

```html
<title>姓名案例_methods实现</title>
<script type="text/javascript" src="../js/vue.js"></script>

<div id="root">
  姓：<input type="text" v-model="firstName"><br/>
  名：<input type="text" v-model="lastName"><br/>
  全名：<span>{{ fullName() }}</span>
</div>

<script type="text/javascript">
  Vue.config.productionTip = false
  new Vue({
    el: '#root',
    data: {
      firstName: '张',
      lastName: '三'
    },
    methods: {
      fullName() {
        return this.firstName + '-' + this.lastName
      }
    },
  })
</script>
```

1. **computed** **计算属性**

1. 定义：要用的属性不存在，**需要通过已有属性计算得来**
2. 原理：底层借助了**Objcet.defineproperty()** 方法提供的`getter`和`setter`

1. `get`函数什么时候执行？

1. 1. 初次读取时会执行一次
   2. 当依赖的数据发生改变时会被再次调用

1. 优势：与`methods`实现相比，**内部有缓存机制**（复用），效率更高，调试方便 
2. 备注

1. 1. 计算属性最终会出现在`vm`上，直接读取使用即可
   2. 如果计算属性要被修改，那必须写 **set** **函数去响应修改**，且`set`中要引起计算时依赖的数据发生改变

1. 1. 如果计算属性确定不考虑修改，可以使用计算属性的简写形式

```html
<title>姓名案例_计算属性实现</title>
<script type="text/javascript" src="../js/vue.js"></script>

<div id="root">
  姓：<input type="text" v-model="firstName"> <br/>
  名：<input type="text" v-model="lastName"> <br/>
  测试：<input type="text" v-model="x"> <br/>	// 这里修改 不会调 fullName的get方法
  全名：<span>{{fullName}}</span> <br/>
  <!-- 全名：<span>{{fullName}}</span> <br/> -->
  <!-- 全名：<span>{{fullName}}</span> <br/> -->
</div>

<script type="text/javascript">
  Vue.config.productionTip = false
  const vm = new Vue({
    el: '#root',
    data: {
      firstName:'张',
      lastName:'三',
      x:'你好'
    },
    computed: {
      //完整写法
      // fullName: {
      // 	get() {
      // 		console.log('get被调用了')
      // 		return this.firstName + '-' + this.lastName
      // 	},
      // 	set(value) {
      // 		console.log('set', value)
      // 		const arr = value.split('-')
      // 		this.firstName = arr[0]
      // 		this.lastName = arr[1]
      // 	}
      // }

      // 简写
      fullName() {
        console.log('get被调用了')
        return this.firstName + '-' + this.lastName
      }
    }
  })
</script>
```

### 1.10. 侦听属性

```html
<title>天气案例</title>
<script type="text/javascript" src="../js/vue.js"></script>

<div id="root">
  <h3>今天天气很{{ info }}</h3>
  <!-- 绑定事件的时候：@xxx="yyy" yyy可以写一些简单的语句 -->
  <!-- <button @click="isHot = !isHot">切换天气</button> -->
  <button @click="changeWeather">切换天气</button>
</div>

<script type="text/javascript">
  Vue.config.productionTip = false
  const vm = new Vue({
    el:'#root',
    data:{
      isHot:true,
    },
    computed:{
      info(){
        return this.isHot ? '炎热' : '凉爽'
      }
    },
    methods: {
      changeWeather(){
        this.isHot = !this.isHot
      }
    }
  })
</script>
```

![img](https://cdn.nlark.com/yuque/0/2022/png/1379492/1643189114273-4b3ac032-4782-4920-a0ae-f600317d89b2.png)

#### 1.10.1. 侦听属性基本用法

**watch**监视属性

1. 当被监视的属性变化时，回调函数自动调用，进行相关操作
2. 监视的属性必须存在，才能进行监视，既可以监视`data`，也可以监视计算属性

1. 配置项属性**immediate:false** **，改为 true**，则初始化时调用一次 **handler(newValue,oldValue)**
2. 监视有两种写法

1. 1. 创建`Vue`时传入**watch: {}**配置
   2. 通过**vm.$watch()**监视

```html
<title>天气案例_监视属性</title>
<script type="text/javascript" src="../js/vue.js"></script>

<div id="root">
  <h2>今天天气很{{info}}</h2>
  <button @click="changeWeather">切换天气</button>
</div>

<script type="text/javascript">
  Vue.config.productionTip = false
  const vm = new Vue({
    el: '#root',
    data: {
      isHot: true,
    },
    computed: {
      info() {
        return this.isHot ? '炎热' : '凉爽'
      }
    },
    methods: {
      changeWeather() {
        this.isHot = !this.isHot
      }
    },
    // 方式一
    /* watch:{		
			isHot:{
				immediate:true,
				handler(newValue,oldValue){
					console.log('isHot被修改了',newValue,oldValue)
				}
			}
		} */
  })
  // 方式二
  vm.$watch('isHot', {		
    immediate: true, // 初始化时让handler调用一下
    //handler什么时候调用？当isHot发生改变时
    handler(newValue, oldValue) {
      console.log('isHot被修改了', newValue, oldValue)
    }
  })
</script>
```

#### 1.10.2. 深度侦听

1. `Vue`中的`watch`默认不监测对象内部值的改变（一层）
2. 在`watch`中配置**deep:true**可以监测对象内部值的改变（多层）

注意

1. `Vue`自身可以监测对象内部值的改变，但`Vue`提供的`watch`默认不可以
2. 使用`watch`时根据监视数据的具体结构，决定是否采用深度监视

```html
<title>天气案例_深度监视</title>
<script type="text/javascript" src="../js/vue.js"></script>

<div id="root">
  <h3>a的值是:{{ numbers.a }}</h3>
  <button @click="numbers.a++">点我让a+1</button>
  <h3>b的值是:{{ numbers.b }}</h3>
  <button @click="numbers.b++">点我让b+1</button>
  <button @click="numbers = {a:666,b:888}">彻底替换掉numbers</button>
  {{numbers.c.d.e}}
</div>

<script type="text/javascript">
  Vue.config.productionTip = false
  const vm = new Vue({
    el: '#root',
    data: {
      isHot: true,
      numbers: {
        a: 1,
        b: 1,
        c: {
          d: {
            e: 100
          }
        }
      }
    },
    watch: {
      // 监视多级结构中某个属性的变化
      /* 'numbers.a':{
				handler(){
					console.log('a被改变了')
				}
			} */
      // 监视多级结构中所有属性的变化
      numbers: {
        deep: true,
        handler() {
          console.log('numbers改变了')
        }
      }
    }
  })
</script>
```

![img](https://cdn.nlark.com/yuque/0/2022/png/1379492/1643190926819-fac77f80-8343-4a85-8960-c660c745f6ed.png)

#### 1.10.3. 侦听属性简写

如果监视属性除了`handler`没有其他配置项的话，可以进行简写

```html
<title>天气案例_监视属性_简写</title>
<script type="text/javascript" src="../js/vue.js"></script>

<div id="root">
  <h3>今天天气很{{ info }}</h3>
  <button @click="changeWeather">切换天气</button>
</div>

<script type="text/javascript">
  Vue.config.productionTip = false
  const vm = new Vue({
    el: '#root',
    data: {isHot: true,},
    computed: {info() {return this.isHot ? '炎热' : '凉爽'}},
    methods: {changeWeather() {this.isHot = !this.isHot}},
    watch: {
      // 正常写法
      // isHot: {
      // 	// immediate:true, //初始化时让handler调用一下
      // 	// deep:true,	//深度监视
      // 	handler(newValue, oldValue) {
      // 		console.log('isHot被修改了', newValue, oldValue)
      // 	}
      // },

      //简写
      isHot(newValue, oldValue) {
        console.log('isHot被修改了', newValue, oldValue, this)
      }
    }
  })

  //正常写法
  // vm.$watch('isHot', {
  // 	immediate: true, //初始化时让handler调用一下
  // 	deep: true,//深度监视
  // 	handler(newValue, oldValue) {
  // 		console.log('isHot被修改了', newValue, oldValue)
  // 	}
  // })l

  //简写
  // vm.$watch('isHot', (newValue, oldValue) => {
  // 	console.log('isHot被修改了', newValue, oldValue, this)
  // })
</script>
```

#### 1.10.4. 计算属性 VS 侦听属性

**computed**和**watch**之间的区别

- `computed`能完成的功能，`watch`都可以完成
- `watch`能完成的功能，`computed`不一定能完成，例如`watch`可以进行异步操作

两个重要的小原则

- 所有被**Vue**管理的函数，最好写成普通函数，这样 **this** 的指向才是**vm**或组件实例对象
- 所有不被**Vue**所管理的函数（定时器的回调函数、**ajax** 的回调函数等、**Promise** 的回调函数），最好写成箭头函数，这样 **this** 的指向才是**vm**或`组件实例对象`

![img](https://cdn.nlark.com/yuque/0/2022/png/1379492/1643192160919-8c757c7a-3406-4b48-84f5-e73779b6f580.png)

**使用计算属性**

```javascript
new Vue({
    el:'#root', 
    data:{ 
        firstName:'张',
        lastName:'三'
    },
    computed:{
    	fullName(){
		    return this.firstName + '-' + this.lastName
    	}
    }
})
```

**使用监听属性**

```javascript
new Vue({
  el:'#root',
  data:{
    firstName:'张',
    lastName:'三',
    fullName:'张-三'
  },
  watch:{
    firstName(val){
      setTimeout(()=>{
        this.fullName = val + '-' + this.lastName
      },1000);
    },
    lastName(val){
      this.fullName = this.firstName + '-' + val
    }
  }
})
```



# Vue核心 绑定样式 条件渲染

### 1.11. 绑定样式

**class**样式

- 写法：**:class=** **"xxx"**，xxx 可以是字符串、数组、对象
- **:style** **="[a,b]"**其中a、b是样式对象

- **:style** **="{fontSize: xxx}"**其中 xxx 是动态值

- - 字符串写法适用于：类名不确定，要动态获取 
  - 数组写法适用于：要绑定多个样式，个数不确定，名字也不确定 

- - 对象写法适用于：要绑定多个样式，个数确定，名字也确定，但不确定用不用 

```html
<style>
  .basic {width: 300px;height: 50px;border: 1px solid black;}
  .happy {border: 3px solid red;background-color: rgba(255, 255, 0, 0.644);
    background: linear-gradient(30deg, yellow, pink, orange, yellow);}
  .sad {border: 4px dashed rgb(2, 197, 2);background-color: skyblue;}
  .normal {background-color: #bfa;}
  .atguigu1 {background-color: yellowgreen;}
  .atguigu2 {font-size: 20px;text-shadow: 2px 2px 10px red;}
  .atguigu3 {border-radius: 20px;}
</style>

<div id="root">
  <!-- 绑定class样式--字符串写法，适用于：样式的类名不确定，需要动态指定 -->
  <div class="basic" :class="mood" @click="changeMood">{{name}}</div><br/><br/>

  <!-- 绑定class样式--数组写法，适用于：要绑定的样式个数不确定、名字也不确定 -->
  <div class="basic" :class="classArr">{{name}}</div><br/><br/>

  <!-- 绑定class样式--对象写法，适用于：要绑定的样式个数确定、名字也确定，但要动态决定用不用 -->
  <div class="basic" :class="classObj">{{name}}</div><br/><br/>

  <!-- 绑定style样式--对象写法 -->
  <div class="basic" :style="styleObj">{{name}}</div><br/><br/>

  <!-- 绑定style样式--数组写法 -->
  <div class="basic" :style="styleArr">{{name}}</div>
</div>

<script type="text/javascript">
  Vue.config.productionTip = false

  const vm = new Vue({
    el: '#root',
    data: {
      name: '尚硅谷',
      mood: 'normal',
      classArr: ['atguigu1', 'atguigu2', 'atguigu3'],
      classObj: {
        atguigu1: false,
        atguigu2: false,
      },
      styleObj: {
        fontSize: '40px',
        color: 'red',
      },
      styleObj2: {
        backgroundColor: 'orange'
      },
      styleArr: [
        {
          fontSize: '40px',
          color: 'blue',
        },
        {
          backgroundColor: 'gray'
        }
      ]
    },
    methods: {
      changeMood() {
        const arr = ['happy', 'sad', 'normal']
        const index = Math.floor(Math.random() * 3)
        this.mood = arr[index]
      }
    },
  })
</script>
```

![img](https://cdn.nlark.com/yuque/0/2022/png/1379492/1643202429722-6609403d-073f-48d1-bd74-99cc1d12df5a.png)

### 1.12. 条件渲染

**v-if**

-  写法 跟 if else 语法类似

**v-if=** **"表达式"**
**v-else-if=** **"表达式"**
**v-else**

-  适用于：切换频率较低的场景，因为不展示的`DOM`元素直接被移除
-  注意：**v-if**可以和**v-else-if** **v-else**一起使用，但要求结构不能被打断

```
v-show
```



- 写法：**v-show=** **"表达式"**
- 适用于：切换频率较高的场景

- 特点：不展示的`DOM`元素未被移除，仅仅是使用样式隐藏掉 **display: none** 

**备注**：使用 **v-if** 的时，元素可能无法获取到，而使用 **v-show** 一定可以获取到

```javascript
**template** 标签不影响结构，页面`html`中不会有此标签，但只能配合 **v-if** ，不能配合 **v-show**
<title>条件渲染</title>
<script type="text/javascript" src="../js/vue.js"></script>

<div id="root">
  <h2>当前的n值是:{{ n }}</h2>
  <button @click="n++">点我n+1</button>

  <!-- 使用v-show做条件渲染 -->
  <!-- <h2 v-show="false">欢迎来到{{name}}</h2> -->
  <!-- <h2 v-show="1 === 1">欢迎来到{{name}}</h2> -->

  <!-- 使用v-if做条件渲染 -->
  <!-- <h2 v-if="false">欢迎来到{{name}}</h2> -->
  <!-- <h2 v-if="1 === 1">欢迎来到{{name}}</h2> -->

  <!-- v-else和v-else-if -->
  <!-- <div v-show="n === 1">Angular</div> -->
  <!-- <div v-show="n === 2">React</div> -->
  <!-- <div v-show="n === 3">Vue</div> -->

  <!-- <div v-if="n === 1">Angular</div> -->
  <!-- <div v-else-if="n === 2">React</div> -->
  <!-- <div v-else-if="n === 3">Vue</div> -->
  <!-- <div v-else>哈哈</div> -->


  <!-- v-if与template的配合使用 -->
  <template v-if="n === 1">
    <h3>你好</h3>
    <h3>尚硅谷</h3>
    <h3>北京</h3>
  </template>

</div>

<script type="text/javascript">
  Vue.config.productionTip = false
  const vm = new Vue({
    el:'#root',
    data:{
      name:'尚硅谷',
      n:0
    }
  })
</script>
```

# Vue核心 列表渲染 数据监视

### 1.13. 列表渲染

#### 1.13.1. 基本列表

 **v-for** 指令

- 用于展示列表数据
- 语法： **<li** **v-for=** **"(item, index)** **of** **items"** **:key=** **"index">** ，这里`key`可以是`index`，更好的是遍历对象的唯一标识

- 可遍历：数组、对象、字符串（用的少）、指定次数（用的少）

```html
<title>基本列表</title>
<script type="text/javascript" src="../js/vue.js"></script>

<div id="root">
  <!-- 遍历数组 -->
  <h3>人员列表（遍历数组）</h3>
  <ul>
    <li v-for="(p,index) of persons" :key="index">{{ p.name }}-{{ p.age }}</li>
  </ul>

  <!-- 遍历对象 -->
  <h3>汽车信息（遍历对象）</h3>
  <ul>
    <li v-for="(value,k) of car" :key="k">{{ k }}-{{ value }}</li>
  </ul>

  <!-- 遍历字符串 -->
  <h3>测试遍历字符串（用得少）</h3>
  <ul>
    <li v-for="(char,index) of str" :key="index">{{ char }}-{{ index }}</li>
  </ul>

  <!-- 遍历指定次数 -->
  <h3>测试遍历指定次数（用得少）</h3>
  <ul>
    <li v-for="(number,index) of 5" :key="index">{{ index }}-{{ number }}</li>
  </ul>
</div>

<script type="text/javascript">
  Vue.config.productionTip = false
  new Vue({
    el: '#root',
    data: {
      persons: [
        { id: '001', name: '张三', age: 18 },
        { id: '002', name: '李四', age: 19 },
        { id: '003', name: '王五', age: 20 }
      ],
      car: {
        name: '奥迪A8',
        price: '70万',
        color: '黑色'
      },
      str: 'hello'
    }
  })
</script>
```

![img](https://cdn.nlark.com/yuque/0/2022/png/1379492/1643263695868-3b70dc42-4c92-4bb5-a736-ad9ab8ccebd3.png)

#### 1.13.2. key 的作用与原理

**原理**

![img](https://cdn.nlark.com/yuque/0/2022/png/1379492/1643033767087-2558e992-b48b-4b54-a9b8-86eb8534bd98.png)

![img](https://cdn.nlark.com/yuque/0/2022/png/1379492/1643033764359-6a37a493-bb51-4b3b-8b14-822a3df68d6e.png)

面试题：react``vue中的**key**有什么作用？（key的内部原理）

1. 虚拟DOM中key的作用：key 是  虚拟DOM 中对象的标识，当数据发生变化时，Vue 会根据 新数据 生成 新的 虚拟DOM ，随后 Vue 进行新 虚拟DOM 与旧 虚拟DOM 的差异比较，比较规则如下
2. 对比规则

1. 1. 旧`虚拟DOM`中找到了与新`虚拟DOM`相同的`key`

1. 1. 1. 若`虚拟DOM`中内容没变, 直接使用之前的`真实DOM`
      2. 若`虚拟DOM`中内容变了, 则生成新的`真实DOM`，随后替换掉页面中之前的`真实DOM`

1. 1.  旧`虚拟DOM`中未找到与新`虚拟DOM`相同的`key`

创建新的`真实DOM`，随后渲染到到页面

1. 用**index**作为**key**可能会引发的问题

1. 1. 若对数据进行逆序添加、逆序删除等**破坏顺序操作**，会产生没有必要的`真实DOM`更新 ==> 界面效果没问题，但效率低
   2. 若结构中还包含输入类的**DOM**：会产生错误DOM更新 ==> 界面有问题

1. 开发中如何选择`key`？

1. 1. 最好使用每条数据的唯一标识作为**key**，比如 id、手机号、身份证号、学号等唯一值
   2. 如果不存在对数据的逆序添加、逆序删除等破坏顺序的操作，仅用于渲染列表，使用**index**作为**key**是没有问题的

```html
<title>key的原理</title>
<script type="text/javascript" src="../js/vue.js"></script>

<div id="root">
  <h2>人员列表（遍历数组）</h2>
  <button @click.once="add">添加一个老刘</button>
  <ul>
    <li v-for="(p,index) of persons" :key="index">
      {{p.name}}-{{p.age}}
      <input type="text">
    </li>
  </ul>
</div>

<script type="text/javascript">
  Vue.config.productionTip = false
  new Vue({
    el: '#root',
    data: {
      persons: [
        { id: '001', name: '张三', age: 18 },
        { id: '002', name: '李四', age: 19 },
        { id: '003', name: '王五', age: 20 }
      ]
    },
    methods: {
      add() {
        const p = { id: '004', name: '老刘', age: 40 }
        this.persons.unshift(p)
      }
    },
  })
</script>
```

![img](https://cdn.nlark.com/yuque/0/2022/png/1379492/1643207518724-dd96127e-5443-4947-932c-b2a2f81403fb.png)

#### 1.13.3. 列表过滤

```html
<title>列表过滤</title>
<script type="text/javascript" src="../js/vue.js"></script>

<div id="root">
  <h2>人员列表</h2>
  <input type="text" placeholder="请输入名字" v-model="keyWord">
  <ul>
    <li v-for="(p,index) of filPersons" :key="p.id">
      {{ p.name }}-{{ p.age }}-{{ p.sex }}
    </li>
  </ul>
</div>

<script type="text/javascript">
  Vue.config.productionTip = false
  // 用 watch 实现
  // #region 
  /* new Vue({
			el: '#root',
			data: {
				keyWord: '',
				persons: [
					{ id: '001', name: '马冬梅', age: 19, sex: '女' },
					{ id: '002', name: '周冬雨', age: 20, sex: '女' },
					{ id: '003', name: '周杰伦', age: 21, sex: '男' },
					{ id: '004', name: '温兆伦', age: 22, sex: '男' }
				],
				filPersons: []
			},
			watch: {
				keyWord: {
					immediate: true,
					handler(val) {
						this.filPersons = this.persons.filter((p) => {
							return p.name.indexOf(val) !== -1
						})
					}
				}
			}
		}) */
  //#endregion

  // 用 computed 实现
  new Vue({
    el: '#root',
    data: {
      keyWord: '',
      persons: [
        { id: '001', name: '马冬梅', age: 19, sex: '女' },
        { id: '002', name: '周冬雨', age: 20, sex: '女' },
        { id: '003', name: '周杰伦', age: 21, sex: '男' },
        { id: '004', name: '温兆伦', age: 22, sex: '男' }
      ]
    },
    computed: {
      filPersons() {
        return this.persons.filter((p) => {
          return p.name.indexOf(this.keyWord) !== -1
        })
      }
    }
  }) 
</script>
```

![img](https://cdn.nlark.com/yuque/0/2022/png/1379492/1643209841363-2dbb95a7-f003-4da1-b456-9a5232f3cf90.png)

#### 1.13.4. 列表排序

```html
<title>列表排序</title>
<script type="text/javascript" src="../js/vue.js"></script>

<div id="root">
  <h2>人员列表</h2>
  <input type="text" placeholder="请输入名字" v-model="keyWord">
  <button @click="sortType = 2">年龄升序</button>
  <button @click="sortType = 1">年龄降序</button>
  <button @click="sortType = 0">原顺序</button>
  <ul>
    <li v-for="(p,index) of filPersons" :key="p.id">
      {{p.name}}-{{p.age}}-{{p.sex}}
      <input type="text">
    </li>
  </ul>
</div>

<script type="text/javascript">
  Vue.config.productionTip = false
  new Vue({
    el: '#root',
    data: {
      keyWord: '',
      sortType: 0, // 0原顺序 1降序 2升序
      persons: [
        { id: '001', name: '马冬梅', age: 30, sex: '女' },
        { id: '002', name: '周冬雨', age: 31, sex: '女' },
        { id: '003', name: '周杰伦', age: 18, sex: '男' },
        { id: '004', name: '温兆伦', age: 19, sex: '男' }
      ]
    },
    computed: {
      filPersons() {
        const arr = this.persons.filter((p) => {
          return p.name.indexOf(this.keyWord) !== -1
        })
        //判断一下是否需要排序
        if (this.sortType) {
          arr.sort((p1, p2) => {
            return this.sortType === 1 ? p2.age - p1.age : p1.age - p2.age
          })
        }
        return arr
      }
    }
  })
</script>
```

![img](https://cdn.nlark.com/yuque/0/2022/png/1379492/1643211061137-37aec6e3-9594-434d-b2d9-d31f752992e1.png)

#### 1.13.5. Vue 数据监视

**更新时的一个问题**

this.persons[0] = {id:'001',name:'马老师',age:50,sex:'男'} 更改`data`数据，`Vue`不监听，模板不改变

```html
<title>更新时的一个问题</title>
<script type="text/javascript" src="../js/vue.js"></script>

<div id="root">
  <h2>人员列表</h2>
  <button @click="updateMei">更新马冬梅的信息</button>
  <ul>
    <li v-for="(p,index) of persons" :key="p.id">
      {{p.name}}-{{p.age}}-{{p.sex}}
    </li>
  </ul>
</div>

<script type="text/javascript">
  Vue.config.productionTip = false

  const vm = new Vue({
    el: '#root',
    data: {
      persons: [
        { id: '001', name: '马冬梅', age: 30, sex: '女' },
        { id: '002', name: '周冬雨', age: 31, sex: '女' },
        { id: '003', name: '周杰伦', age: 18, sex: '男' },
        { id: '004', name: '温兆伦', age: 19, sex: '男' }
      ]
    },
    methods: {
      updateMei() {
        // this.persons[0].name = '马老师'	//奏效
        // this.persons[0].age = 50				//奏效
        // this.persons[0].sex = '男'			//奏效
        // this.persons[0] = {id:'001',name:'马老师',age:50,sex:'男'} //不奏效
        this.persons.splice(0, 1, { id: '001', name: '马老师', age: 50, sex: '男' })
      }
    }
  })
</script>
```

**模拟一个数据监测**

```javascript
let data = {
  name: '尚硅谷',
  address: '北京',
}

function Observer(obj) {
  // 汇总对象中所有的属性形成一个数组
  const keys = Object.keys(obj)
  // 遍历
  keys.forEach((k) => {
    Object.defineProperty(this, k, {
      get() {
        return obj[k]
      },
      set(val) {
        console.log(`${k}被改了，我要去解析模板，生成虚拟DOM.....我要开始忙了`)
        obj[k] = val
      }
    })
  })
}

// 创建一个监视的实例对象，用于监视data中属性的变化
const obs = new Observer(data)
console.log(obs)

// 准备一个vm实例对象
let vm = {}
vm._data = data = obs
```

**原理**

1.  **vue** **会监视** **data** **中所有层次的数据**
2. 如何监测**对象**中的数据？
   通过 **setter** 实现监视，且要在 **new Vue()** 时就传入要监测的数据 

- - 对象创建后追加的属性，`Vue`默认不做响应式处理
  - 如需给后添加的属性做响应式，请使用如下API

```
**Vue.set(target,propertyName/index,value)**
**vm.$set(target,propertyName/index,value)**
```

1. 如何监测**数组**中的数据？
   通过包裹数组更新元素的方法实现，本质就是做了两件事

1. 1. 调用原生对应的方法对数组进行更新
   2. 重新解析模板，进而更新页面

1. 在`Vue`修改数组中的某个元素一定要用如下方法 

 **push()**  **pop()**  **unshift()**  **shift()**  **splice()**  **sort()**  **reverse()** 这几个方法被`Vue`重写了

```
**Vue.set()** 或 **vm.$set()**
```

**特别注意**： **Vue.set()**  **和**  **vm.$set()**  **不能** **给** **vm** **或** **vm** **的** **根数据对象** **（** **data** **等）添加属性**

```html
<title>总结数据监视</title>
<style>button {margin-top: 10px;}</style>
<script type="text/javascript" src="../js/vue.js"></script>

<div id="root">
  <h1>学生信息</h1>
  <button @click="student.age++">年龄+1岁</button> <br />
  <button @click="addSex">添加性别属性，默认值：男</button> <br />
  <button @click="student.sex = '未知' ">修改性别</button> <br />
  <button @click="addFriend">在列表首位添加一个朋友</button> <br />
  <button @click="updateFirstFriendName">修改第一个朋友的名字为：张三</button> <br />
  <button @click="addHobby">添加一个爱好</button> <br />
  <button @click="updateHobby">修改第一个爱好为：开车</button> <br />
  <button @click="removeSmoke">过滤掉爱好中的抽烟</button> <br />
  <h3>姓名：{{ student.name }}</h3>
  <h3>年龄：{{ student.age }}</h3>
  <h3 v-if="student.sex">性别：{{student.sex}}</h3>
  <h3>爱好：</h3>
  <ul>
    <li v-for="(h,index) in student.hobby" :key="index">{{ h }} </li>
  </ul>
  <h3>朋友们：</h3>
  <ul>
    <li v-for="(f,index) in student.friends" :key="index">{{ f.name }}--{{ f.age }}</li>
  </ul>
</div>

<script type="text/javascript">
  Vue.config.productionTip = false

  const vm = new Vue({
    el: '#root',
    data: {
      student: {
        name: 'tom',
        age: 18,
        hobby: ['抽烟', '喝酒', '烫头'],
        friends: [
          { name: 'jerry', age: 35 },
          { name: 'tony', age: 36 }
        ]
      }
    },
    methods: {
      addSex() {
        // Vue.set(this.student,'sex','男')
        this.$set(this.student, 'sex', '男')
      },
      addFriend() {
        this.student.friends.unshift({ name: 'jack', age: 70 })
      },
      updateFirstFriendName() {
        this.student.friends[0].name = '张三'
      },
      addHobby() {
        this.student.hobby.push('学习')
      },
      updateHobby() {
        // this.student.hobby.splice(0,1,'开车')
        // Vue.set(this.student.hobby,0,'开车')
        this.$set(this.student.hobby, 0, '开车')
      },
      removeSmoke() {
        this.student.hobby = this.student.hobby.filter((h) => {
          return h !== '抽烟'
        })
      }
    }
  })
```

![img](https://cdn.nlark.com/yuque/0/2022/png/1379492/1643271851385-31e81d79-d006-45a4-bd6e-aadbec6b982a.png)



# Vue核心 收集表单数据 过滤器

### 1.14. 收集表单数据

收集表单数据

- 若`<input type="text"/>`，则`v-model`收集的是 **value** 值，用户输入的内容就是`value`值
- 若`<input type="radio"/>`，则`v-model`收集的是 **value** 值，且要给标签配置`value`属性

- 若`<input type="checkbox"/>` 

- - 没有配置`value`属性，那么收集的是 **checked** 属性（勾选 or 未勾选，是布尔值）
  - 配置了`value`属性

- - - `v-model`的初始值是**非数组**，那么收集的就是 **checked** （勾选 or 未勾选，是布尔值）
    - `v-model`的初始值是**数组**，那么收集的就是 **value** 组成的数组

`v-model`的三个修饰符

1. 1.  **lazy** 	失去焦点后再收集数据
   2.  **number** 输入字符串转为有效的数字

1. 1.  **trim** 	输入首尾空格过滤

```html
<title>收集表单数据</title>
<script type="text/javascript" src="../js/vue.js"></script>

<div id="root">
  <form @submit.prevent="demo">
    账号：<input type="text" v-model.trim="userInfo.account"> <br /><br />
    密码：<input type="password" v-model="userInfo.password"> <br /><br />
    年龄：<input type="number" v-model.number="userInfo.age"> <br /><br />
    性别：
    男<input type="radio" name="sex" v-model="userInfo.sex" value="male">
    女<input type="radio" name="sex" v-model="userInfo.sex" value="female"> <br /><br />
    爱好：
    学习<input type="checkbox" v-model="userInfo.hobby" value="study">
    打游戏<input type="checkbox" v-model="userInfo.hobby" value="game">
    吃饭<input type="checkbox" v-model="userInfo.hobby" value="eat">
    <br /><br />
    所属校区
    <select v-model="userInfo.city">
      <option value="">请选择校区</option>
      <option value="beijing">北京</option>
      <option value="shanghai">上海</option>
      <option value="shenzhen">深圳</option>
      <option value="wuhan">成都</option>
    </select>
    <br/><br/>
    其他信息：
    <textarea v-model.lazy="userInfo.other"></textarea> <br/><br/>
    <input type="checkbox" v-model="userInfo.agree">阅读并接受
    <a href="https://www.yuque.com/cessstudy">《用户协议》</a>
    <button>提交</button>
  </form>
</div>

<script type="text/javascript">
  Vue.config.productionTip = false

  new Vue({
    el: '#root',
    data: {
      userInfo: {
        account: '',
        password: '',
        age: 18,
        sex: 'female',
        hobby: [],
        city: 'beijing',
        other: '',
        agree: ''
      }
    },
    methods: {
      demo() {
        console.log(JSON.stringify(this.userInfo))
      }
    }
  })
</script>
```

![img](https://cdn.nlark.com/yuque/0/2022/png/1379492/1643274829514-6c5ec07b-771e-47bd-9ae8-9ca0a636bc01.png)

### 1.15. 过滤器（Vue3 已经移除）

定义：**对要显示的数据进行特定格式化后再显示**（适用于一些简单逻辑的处理）

注册过滤器：

 **Vue.filter(name, callback)** 全局过滤器

 **new Vue {filters: {}}**  局部过滤器

使用过滤器： **{{ xxx | 过滤器名}}**  或  **v-bind:属性 = "xxx | 过滤器名"**  

备注：

1. 1. 过滤器可以接收额外参数，多个过滤器也可以串联
   2. 并没有改变原本的数据，而是产生新的对应的数据



处理时间的库 **moment** 体积较大  **dayjs** 轻量级

```html
<!DOCTYPE html>
<html>
	<head>
		<meta charset="UTF-8" />
		<title>过滤器</title>
		<script type="text/javascript" src="../js/vue.js"></script>
		<script src="https://cdn.bootcdn.net/ajax/libs/dayjs/1.10.6/dayjs.min.js"></script>
	</head>
	<body>
		<div id="root">
			<h2>时间</h2>
            <h3>当前时间戳：{{time}}</h3>
            <h3>转换后时间：{{time | timeFormater()}}</h3>
			<h3>转换后时间：{{time | timeFormater('YYYY-MM-DD HH:mm:ss')}}</h3>
			<h3>截取年月日：{{time | timeFormater() | mySlice}}</h3>
		</div>
	</body>

	<script type="text/javascript">
		Vue.config.productionTip = false
		// 全局过滤器
		Vue.filter('mySlice',function(value){
			return value.slice(0,11)
		})
		new Vue({
            el:'#root',
            data:{
                time:1626750147900,
            },
			// 局部过滤器
            filters:{
                timeFormater(value, str="YYYY年MM月DD日 HH:mm:ss"){
                    return dayjs(value).format(str)
                }
            }
        })
	</script>
</html>
```

![img](https://cdn.nlark.com/yuque/0/2022/png/1379492/1643275984885-96a3c918-bfdc-4697-9eca-8ccdb0053182.png)

# Vue核心 内置指令 自定义指令

### 1.16. 内置指令

之前学过的指令： 

```
**v-bind** 	单向绑定解析表达式，可简写为 **:**
```

 **v-model** 	双向数据绑定

 **v-for** 		遍历数组 / 对象 / 字符串

```
**v-on** 		绑定事件监听，可简写为 **@**
```

 **v-show** 	条件渲染 (动态控制节点是否展示)

 **v-if** 		条件渲染（动态控制节点是否存存在）

 **v-else-if** 	条件渲染（动态控制节点是否存存在）

 **v-else** 	条件渲染（动态控制节点是否存存在）

#### 1.16.1. v-text 指令

 **v-text** 指令

作用：向其所在的节点中渲染文本内容 

与插值语法的区别： **v-text** 会替换掉节点中的内容， **{{xxx}}** 则不会，更灵活

```html
<title>v-text指令</title>
<script type="text/javascript" src="../js/vue.js"></script>

<div id="root">
  <div>你好，{{name}}</div>
  <div v-text="name"></div>
  <div v-text="str"></div>
</div>

<script type="text/javascript">
  Vue.config.productionTip = false
  new Vue({
    el:'#root',
    data:{
      name:'cess',
      str:'<h3>你好啊！</h3>'
    }
  })
</script>
```

![img](https://cdn.nlark.com/yuque/0/2022/png/1379492/1643288562593-79172b18-d290-4eb1-acf1-16f9d402275b.png)

#### 1.16.2. v-html 指令

 **v-html** 指令

作用：向指定节点中渲染包含`html`结构的内容 

与插值语法的区别： 

1. 1. 1.  **v-html** 会替换掉节点中所有的内容， **{{xxx}}** 则不会
      2.  **v-html** 可以识别 **html** 结构

严重注意 **v-html** 有安全性问题！！！ 

1. 1. 1. 在网站上动态渲染任意 **html** 是非常危险的，容易导致 **XSS** 攻击
      2. 一定要在可信的内容上使用 **v-html** ，永远不要用在用户提交的内容上！！！

```html
<title>v-html指令</title>
<script type="text/javascript" src="../js/vue.js"></script>

<div id="root">
  <div>你好，{{ name }}</div>
  <div v-html="str"></div>
  <div v-html="str2"></div>
</div>

<script type="text/javascript">
  Vue.config.productionTip = FontFaceSetLoadEvent
  new Vue({
    el:'#root',
    data:{
      name:'cess',
      str:'<h3>你好啊！</h3>',
      str2:'<a href=javascript:location.href="http://www.baidu.com?"+document.cookie>兄弟我找到你想要的资源了，快来！</a>',
    }
  })
</script>
```

![img](https://cdn.nlark.com/yuque/0/2022/png/1379492/1643288714174-ac150b6b-abbb-46a3-9075-1ec9f1224052.png)

#### 1.16.3. v-cloak 指令

 **v-cloak** 指令（没有值）

1. 1. 本质是一个特殊属性，`Vue`实例创建完毕并接管容器后，会删掉 **v-cloak** 属性
   2. 使用 **css** 配合 **v-cloak** 可以解决网速慢时页面展示出 **{{xxx}}** 的问题

```html
<title>v-cloak指令</title>

<style>
  [v-cloak] {
    display:none;
  }
</style>

<div id="root">
  <h2 v-cloak>{{ name }}</h2>
</div>

// 够延迟5秒收到vue.js
<script type="text/javascript" src="http://localhost:8080/resource/5s/vue.js"></script>

<script type="text/javascript">
  console.log(1)
  Vue.config.productionTip = false
  new Vue({
    el:'#root',
    data:{name:'cess'}
  })
</script>
```

![img](https://cdn.nlark.com/yuque/0/2022/png/1379492/1643291162075-31a34809-47e1-4155-a91b-1ae59e197ad6.png)

#### 1.16.4. v-once 指令

-  **v-once** 所在节点在初次动态渲染后，就视为静态内容了 
- 以后数据的改变不会引起 **v-once** 所在结构的更新，可以用于优化性能

```html
<title>v-once指令</title>
<script type="text/javascript" src="../js/vue.js"></script>

<div id="root">
  <h2 v-once>初始化的n值是: {{n}}</h2>
  <h2>当前的n值是: {{n}}</h2>
  <button @click="n++">点我n+1</button>
</div>

<script type="text/javascript">
  Vue.config.productionTip = false
  new Vue({ el: '#root', data: {n:1} })
</script>
```

![img](https://cdn.nlark.com/yuque/0/2022/png/1379492/1643291197561-2bb725a5-4597-49f4-819f-f20467c23326.png)

#### 1.16.5. v-pre 指令

1. 跳过 **v-pre** 所在节点的编译过程
2. 可利用它跳过：没有使用指令语法、没有使用插值语法的节点，会加快编译

```html
<title>v-pre指令</title>
<script type="text/javascript" src="../js/vue.js"></script>

<div id="root">
  <h2 v-pre>Vue其实很简单</h2>
  <h2 >当前的n值是:{{n}}</h2>
  <button @click="n++">点我n+1</button>
</div>

<script type="text/javascript">
  Vue.config.productionTip = false
  new Vue({ el:'#root', data:{n:1} })
</script>
```

![img](https://cdn.nlark.com/yuque/0/2022/png/1379492/1643291519381-84cfa52c-833d-4bfd-9e5c-b48b902f24fa.png)

### 1.17. 自定义指令

```
**directives**
```

**定义语法**

1. 局部指令

```javascript
new Vue({															
  directives:{ 
    指令名:配置对象 
  }   
})

new Vue({															
  directives:{ 
    指令名:回调函数 
  }   
})
```

1.  全局指令

```javascript
Vue.directive(指令名, 配置对象)
或
Vue.directive(指令名, 回调函数)


Vue.directive('fbind', {
    // 指令与元素成功绑定时（一上来）
    bind(element, binding) {	// element就是DOM元素，binding就是要绑定的
      element.value = binding.value
    },
    // 指令所在元素被插入页面时
    inserted(element, binding) {
      element.focus()
    },
    // 指令所在的模板被重新解析时
    update(element, binding) {
      element.value = binding.value
    }
})
```

**配置对象中常用的3个回调函数** 

 **bind(element, binding)** 	 指令与元素成功绑定时调用

 **inserted(element, binding)** 指令所在元素被插入页面时调用

 **update(element, binding)** 	 指令所在模板结构被重新解析时调用

```
**element** 就是`DOM`元素， **binding** 就是要绑定的对象，它包含以下属性：`name``value``oldValue``expression``arg``modifiers
```

**备注**

1. 1. 指令定义时不加 **v-** ，但使用时要加 **v-** 
   2. 指令名如果是多个单词，要使用 **kebab-case** 命名方式，不要用`camelCase`命名  

```javascript
new Vue({
	el: '#root',
	data: {
		n:1
	},
	directives: {
		'big-number'(element,binding) {
			element.innerText = binding.value * 10
		}
	}
})
```

回顾一个DOM操作

```html
<style>.demo{background-color: orange;}</style>

<body>
  <button id="btn">点我创建一个输入框</button>
</body>

<script type="text/javascript" >
  const btn = document.getElementById('btn')
  btn.onclick = ()=>{
    const input = document.createElement('input')

    input.className = 'demo'
    input.value = 99
    input.onclick = ()=>{alert(1)}

    document.body.appendChild(input)

    input.focus()
    input.parentElement.style.backgroundColor = 'skyblue'
  }
</script>
<title>自定义指令</title>
<script type="text/javascript" src="../js/vue.js"></script>

<div id="root">
  <h2>{{ name }}</h2>
  <h2>当前的n值是：<span v-text="n"></span> </h2>
  <!-- <h2>放大10倍后的n值是：<span v-big-number="n"></span> </h2> -->
  <h2>放大10倍后的n值是：<span v-big="n"></span> </h2>
  <button @click="n++">点我n+1</button>
  <hr />
  <input type="text" v-fbind:value="n">
</div>

<script type="text/javascript">
  Vue.config.productionTip = false

  // 定义全局指令
  /* Vue.directive('fbind',{
		// 指令与元素成功绑定时（一上来）
		bind(element,binding){
			element.value = binding.value
		},
		// 指令所在元素被插入页面时
		inserted(element,binding){
			element.focus()
		},
		// 指令所在的模板被重新解析时
		update(element,binding){
			element.value = binding.value
		}
	}) */

  new Vue({
    el: '#root',
    data: {
      name: '尚硅谷',
      n: 1
    },
    directives: {
      // big函数何时会被调用？
      // 1.指令与元素成功绑定时（一上来） 2.指令所在的模板被重新解析时
      /* 'big-number'(element,binding){
				// console.log('big')
				element.innerText = binding.value * 10
			}, */
      big(element, binding) {
        console.log('big', this) // 🔴注意此处的 this 是 window
        // console.log('big')
        element.innerText = binding.value * 10
      },
      fbind: {
        // 指令与元素成功绑定时（一上来）
        bind(element, binding) {
          element.value = binding.value
        },
        // 指令所在元素被插入页面时
        inserted(element, binding) {
          element.focus()
        },
        // 指令所在的模板被重新解析时
        update(element, binding) {
          element.value = binding.value
        }
      }
    }
  })
</script>
```

![img](https://cdn.nlark.com/yuque/0/2022/png/1379492/1643294260337-5955abe5-3c59-4a75-91b5-36ef16b9f54f.png)



# Vue核心 Vue生命周期

### 1.18. Vue生命周期

#### 1.18.1. 引出生命周期

**生命周期**

1. 1. 又名**生命周期回调函数**、生命周期函数、生命周期钩子
   2. 是什么：`Vue`在关键时刻帮我们调用的一些特殊名称的函数

1. 1. **生命周期函数的名字不可更改**，但函数的具体内容是程序员根据需求编写的
   2. 生命周期函数中的 **this** 指向是 **vm** 或 **组件实例对象** 

```html
<title>引出生命周期</title>
<script type="text/javascript" src="../js/vue.js"></script>

<div id="root">
  <h2 v-if="a">你好啊</h2>
  <h2 :style="{opacity}">看笔记学Vue</h2>
</div>

<script type="text/javascript">
  Vue.config.productionTip = false
  new Vue({
    el: '#root',
    data: {
      a: false,
      opacity: 1
    },
    methods: {
    },
    // 🔴Vue 完成模板的解析并把初始的真实 DOM 元素放入页面后（挂载完毕）调用 mounted
    mounted() {
      console.log('mounted', this)
      setInterval(() => {
        this.opacity -= 0.01
        if(this.opacity <= 0) this.opacity = 1
      }, 16)
    },
  })

  // 通过外部的定时器实现（不推荐）
  // setInterval(() => {
  // 		vm.opacity -= 0.01
  // 		if(vm.opacity <= 0) vm.opacity = 1
  // },16)
</script>
```

![img](https://cdn.nlark.com/yuque/0/2022/gif/1379492/1643297331036-4c4cb325-360e-42aa-bf7c-f7ae08c61a23.gif)

#### 1.18.2. 分析生命周期

![img](https://cdn.nlark.com/yuque/0/2022/png/1379492/1643297176928-5d5ac765-237c-462d-9188-84935e6c3c69.png)

```html
<title>分析生命周期</title>
	<script type="text/javascript" src="../js/vue.js"></script>

	<div id="root" :x="n">
		<h2 v-text="n"></h2>
		<h2>当前的n值是：{{ n }}</h2>
		<button @click="add">点我n+1</button>
		<button @click="bye">点我销毁vm</button>
	</div>

<script type="text/javascript">
	Vue.config.productionTip = false

	new Vue({
		el: '#root',
		// template:`
		// 	<div>
		// 		<h2>当前的n值是：{{n}}</h2>
		// 		<button @click="add">点我n+1</button>
		// 	</div>
		// `,
		data: {
			n: 1
		},
		methods: {
			add() { console.log('add')
				this.n++
			},
			bye() {
				console.log('bye')
				this.$destroy()
			}
		},
		watch: {
			n() {
				console.log('n变了')
			}
		},
		beforeCreate() {console.log('beforeCreate')},
		created() {console.log('created')},
		beforeMount() {console.log('beforeMount')},
		mounted() {console.log('mounted')},
		beforeUpdate() {console.log('beforeUpdate')},
		updated() {console.log('updated')},
		beforeDestroy() {console.log('beforeDestroy')},
		destroyed() {console.log('destroyed')},
	})
</script>
```

#### 1.18.3. 总结生命周期

**总结**

常用的生命周期钩子

1. 1.  **mounted** 发送`ajax`请求、启动定时器、绑定自定义事件、订阅消息等初始化操作 
   2.  **beforeDestroy** 清除定时器、解绑自定义事件、取消订阅消息等收尾工作 

关于**销毁** Vue`实例

1. 1. 销毁后借助`Vue`开发者工具看不到任何信息
   2. 销毁后自定义事件会失效，但原生`DOM`事件依然有效

1. 1. 一般不会在 **beforeDestroy** 操作数据，因为即便操作数据，也不会再触发更新流程了

```html
<title>引出生命周期</title>
<script type="text/javascript" src="../js/vue.js"></script>

<div id="root">
  <h2 :style="{opacity}">欢迎学习Vue</h2>
  <button @click="opacity = 1">透明度设置为1</button>
  <button @click="stop">点我停止变换</button>
</div>

<script type="text/javascript">
  Vue.config.productionTip = false
  new Vue({
    el: '#root',
    data: {
      opacity: 1
    },
    methods: {
      stop() {
        this.$destroy()
      }
    },
    // Vue完成模板的解析并把初始的真实DOM元素放入页面后（挂载完毕）调用mounted
    mounted() {
      console.log('mounted', this)
      this.timer = setInterval(() => {
        console.log('setInterval')
        this.opacity -= 0.01
        if (this.opacity <= 0) this.opacity = 1
      }, 16)
    },
    beforeDestroy() {
      clearInterval(this.timer)
      console.log('vm即将驾鹤西游了')
    },
  })
</script>
```

![img](https://cdn.nlark.com/yuque/0/2022/png/1379492/1643360078432-ea5d8d1d-fcf1-4da5-a3eb-e3624fd353b6.png)

# Vue组件化编程

### 2.1. 模块与组件、模块化与组件化

![img](https://cdn.nlark.com/yuque/0/2022/png/1379492/1643034111142-590bfdbc-e993-4f4f-9a75-110cba2f890d.png)

![img](https://cdn.nlark.com/yuque/0/2022/png/1379492/1643034111832-4a659e2d-4a13-4944-a153-ab038b65cbf0.png)

**模块**

1. 1. 理解：向外提供特定功能的 js 程序，一般就是一个 js 文件
   2. 为什么：js 文件很多很复杂

1. 1. 作用：复用、简化 js 的编写，提高 js 运行效率

**组件**

1. 1. 定义：**用来实现****局部****功能的****代码****和****资源****的****集合**（html/css/js/image…）
   2. 为什么：一个界面的功能很复杂

1. 1. 作用：复用编码，简化项目编码，提高运行效率

**模块化**

当应用中的 js 都以模块来编写的，那这个应用就是一个模块化的应用

**组件化**

当应用中的功能都是多组件的方式来编写的，那这个应用就是一个组件化的应用

### 2.2. 非单文件组件

**非单文件组件**：一个文件中包含有 n 个组件

**单文件组件**：一个文件中只包含有 1 个组件

#### 2.2.1. 基本使用

`Vue`中使用组件的三大步骤 

1. **定义组件**

- 使用 **Vue.extend(options)** 创建，其中`options`和`new Vue(options)`时传入的 **options** 几乎一样，但也有点区别

1. 1.   **el** 不要写，因为最终所有的组件都要经过一个`vm`的管理，由`vm`中的`el`才决定服务哪个容器
   2.   **data** 必须写成函数，避免组件被复用时，数据存在引用关系

1. **注册组件**

1. 1. 局部注册： **new Vue()** 的时候 **options** 传入 **components** 选项
   2. 全局注册： **Vue.component('组件名',组件)** 

1. **使用组件**

编写组件标签如 **<school></school>** 

```html
<title>基本使用</title>
<script type="text/javascript" src="../js/vue.js"></script>

<div id="root">
  <h2>{{msg}}</h2><hr>
  <!-- 第三步：编写组件标签 -->
  <school></school><hr>
  <student></student><hr>
  <hello></hello><hr>
</div>

<div id="root2">
  <hello></hello>
</div>

<script type="text/javascript">
  Vue.config.productionTip = false

  //第一步：创建school组件
  const school = Vue.extend({
    // el:'#root', //组件定义时，一定不要写el配置项，
    // 因为最终所有的组件都要被一个vm管理，由vm决定服务于哪个容器
    template: `
				<div class="demo">
					<h3>学校名称：{{schoolName}}</h3>
					<h3>学校地址：{{address}}</h3>
					<button @click="showName">点我提示学校名</button>	
  			</div>
			`,
    data() {
      return {
        schoolName: '尚硅谷',
        address: '北京昌平'
      }
    },
    methods: {
      showName() {
        alert(this.schoolName)
      }
    },
  })

  //第一步：创建student组件
  const student = Vue.extend({
    template: `
				<div>
					<h3>学生姓名：{{studentName}}</h3>
					<h3>学生年龄：{{age}}</h3>
  			</div>
			`,
    data() {
      return {
        studentName: '张三',
        age: 18
      }
    }
  })

  //第一步：创建hello组件
  const hello = Vue.extend({
    template: `
				<div>	
					<h3>你好啊！{{name}}</h3>
  			</div>
			`,
    data() {
      return {
        name: 'cess'
      }
    }
  })

  //第二步：全局注册组件
  Vue.component('hello', hello)

  //创建vm
  new Vue({
    el: '#root',
    data: {
      msg: '你好啊！'
    },
    //第二步：注册组件（局部注册）
    components: {
      school,
      student
    }
  })

  new Vue({
    el: '#root2',
  })
</script>
```

![img](https://cdn.nlark.com/yuque/0/2022/png/1379492/1643374501694-1ed5750f-5819-49ce-b470-c84039bb2356.png)

#### 2.2.2. 组件注意事项

**关于组件名**

- 一个单词组成

- - 第一种写法（首字母小写）：school
  - 第二种写法（**首字母大写**）：School

- 多个单词组成

- - 第一种写法（kebab-case 命名）：my-school
  - 第二种写法（**CamelCase 命名**）：MySchool（需要`Vue`脚手架支持）

- 备注

- - 组件名尽可能回避`HTML`中已有的元素名称，例如：h2、H2都不行
  - 可以使用 **name** 配置项指定组件在开发者工具中呈现的名字

**关于组件标签** 

- 第一种写法：`<school></school>`
- 第二种写法： **<school/>** （需要`Vue`脚手架支持）

- 备注：不使用脚手架时，`<school/>`会导致后续组件不能渲染

一个简写方式：`const school = **Vue.extend(options)** 可简写为`const school = **options** ，因为父组件`components`引入的时候会自动创建

```html
<title>几个注意点</title>
	<script type="text/javascript" src="../js/vue.js"></script>

	<div id="root">
		<h2>{{msg}}</h2>
		<school></school>
	</div>

<script type="text/javascript">
	Vue.config.productionTip = false

	//定义组件
	const school = Vue.extend({
		name: 'atguigu', // 组件给自己起个名字，用于在浏览器开发工具上显示
		template: `
				<div>
					<h3>学校名称：{{name}}</h3>	
					<h3>学校地址：{{address}}</h3>	
				</div>
			`,
		data() {
			return {
				name: '电子科技大学',
				address: '成都'
			}
		}
	})

	new Vue({
		el: '#root',
		data: {
			msg: '欢迎学习Vue!'
		},
		components: {
			school
		}
	})
</script>
```

![img](https://cdn.nlark.com/yuque/0/2022/png/1379492/1643375968692-be166774-5ae1-434e-83f2-26a7d3f03fcf.png)

#### 2.2.3. 组件的嵌套

![img](https://cdn.nlark.com/yuque/0/2022/png/1379492/1643034109512-1a1a9c24-a474-4022-83b6-b6a16216151a.png)

```html
<title>组件的嵌套</title>
<script type="text/javascript" src="../js/vue.js"></script>

<div id="root"></div>

<script type="text/javascript">
  Vue.config.productionTip = false

  //定义student组件
  const student = Vue.extend({
    name: 'student',
    template: `
				<div>
					<h4>学生姓名：{{name}}</h4>	
					<h4>学生年龄：{{age}}</h4>	
  			</div>
			`,
    data() {return {name: '尚硅谷',age: 18}}
  })

  //定义school组件
  const school = Vue.extend({
    name: 'school',
    template: `
				<div>
					<h3>学校名称：{{name}}</h3>	
					<h3>学校地址：{{address}}</h3>	
					<student></student>
 			  </div>
			`,
    data() {return {name: '尚硅谷',address: '北京'}},
    //注册组件（局部）
    components: { student }
  })

  //定义hello组件
  const hello = Vue.extend({
    template: `<h3>{{msg}}</h3>`,
    data() {return {msg: '欢迎来到尚硅谷学习！'}}
  })

  //定义app组件
  const app = Vue.extend({
    template: `
				<div>	
					<hello></hello>
					<school></school>
  			</div>
			`,
    components: { school, hello }
  })

  //创建vm
  new Vue({
    el: '#root',
    template: '<app></app>',
    //注册组件（局部）
    components: { app }
  })
</script>
```

![img](https://cdn.nlark.com/yuque/0/2022/png/1379492/1643376620047-6bde749d-8ece-4b36-aea8-fccf4767202e.png)

#### 2.2.4. VueComponent

关于 **VueComponent**

1. 1. **school** 组件本质是一个名为 **VueComponent** **的构造函数**，且不是程序员定义的，而是  **Vue.extend()**  生成的 
   2. 我们只需要写 **<school/>** 或 **<school></school>**，**Vue 解析时会帮我们创建 school 组件的实例对象**，即 **Vue** 帮我们执行的 **new VueComponent(options)**  

1. 1. 每次调用 **Vue.extend** ，返回的都是一个全新的 **VueComponent** ，即不同组件是不同的对象
   2. 关于 **this** 指向 

1. 1. 1. 组件配置中 **data** 函数、 **methods** 中的函数、 **watch** 中的函数、 **computed** 中的函数 它们的 **this** 均是  **VueComponent实例对象** 
      2.  **new Vue(options)** 配置中： **data** 函数、 **methods** 中的函数、 **watch** 中的函数、 **computed** 中的函数 它们的 **this** 均是  **Vue实例对象** 

1. 1.  **VueComponent** 的实例对象，以后简称 **vc** （**组件实例对象**） **Vue**的实例对象`，以后简称 **vm**   

```html
<title>VueComponent</title>
<script type="text/javascript" src="../js/vue.js"></script>

<div id="root">
  <school></school>
  <hello></hello>
</div>

<script type="text/javascript">
  Vue.config.productionTip = false

  // 定义school组件
  const school = Vue.extend({
    name: 'school',
    template: `
				<div>
					<h2>学校名称：{{name}}</h2>	
					<h2>学校地址：{{address}}</h2>	
					<button @click="showName">点我提示学校名</button>
  			</div>
			`,
    data() {return {name: '尚硅谷',address: '北京'}},
    methods: {showName() {console.log('showName', this)}},
  })

  const test = Vue.extend({
    template: `<span>atguigu</span>`
  })

  // 定义hello组件
  const hello = Vue.extend({
    template: `
				<div>
					<h2>{{msg}}</h2>
					<test></test>	
  			</div>
			`,
    data() {return {msg: '你好啊！'}},
    components: { test }
  })

  // console.log('@',school)
  // console.log('#',hello)

  // 创建vm
  const vm = new Vue({
    el: '#root',
    components: { school, hello }
  })
</script>
```

#### 2.2.5. 一个重要的内置关系

![img](https://cdn.nlark.com/yuque/0/2022/png/1379492/1643034116880-0c7ffd4b-f0ed-47b2-9638-3bb71344c4f1.png)

1. 一个重要的内置关系： **VueComponent.prototype.__proto__ === Vue.prototype** 
2. 为什么要有这个关系：让组件实例对象`vc`可以访问到 `Vue原型`上的属性、方法

### 2.3. 单文件组件

- `School.vue`

```vue
<template>
    <div id='Demo'>
        <h2>学校名称：{{name}}</h2>
        <h2>学校地址：{{address}}</h2>
        <button @click="showName">点我提示学校名</button>
    </div>
</template>

<script>
    export default {
        name:'School',
        data() {
            return {
                name:'UESTC',
                address:'成都'
            }
        },
        methods: {
            showName(){
                alert(this.name)
            }
        },
    }
</script>

<style>
    #Demo{
        background: orange;
    }
</style>
```

- `Student.vue`

```vue
<template>
    <div>
        <h2>学生姓名：{{name}}</h2>
        <h2>学生年龄：{{age}}</h2>
    </div>
</template>

<script>
    export default {
        name:'Student',
        data() {
            return {
                name:'cess',
                age:20
            }
        },
    }
</script>
```

- `App.vue`

```vue
<template>
    <div>
        <School></School>
        <Student></Student>
    </div>
</template>

<script>
    import School from './School.vue'
    import Student from './Student.vue'

    export default {
        name:'App',
        components:{
            School,
            Student
        }
    }
</script>
```

-  `main.js`

```javascript
import App from './App.vue'

new Vue({
    template:`<App></App>`,
    el:'#root',
    components:{App}
})
```

- `index.html`

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>单文件组件练习</title>
</head>
<body>
    <div id="root"></div>
    <script src="../../js/vue.js"></script>
    <script src="./main.js"></script>
</body>
</html>
```

# Vue CLI 初始化脚手架

### 3.1. 初始化脚手架

#### 3.1.1. 说明

1. `Vue脚手架`是 **Vue** 官方提供的标准化开发工具（开发平台）
2. 最新的版本是 4.x

1. 文档 [**Vue CLI**](https://cli.vuejs.org/zh/)

#### 3.1.2. 具体步骤

1. 如果下载缓慢请配置 **npm** 淘宝镜像 **npm config set registry http://registry.npm.taobao.org** 
2. 全局安装 **@vue/cli**  **npm install -g @vue/cli** 

1. 切换到创建项目的目录，使用命令创建项目 **vue create** **xxx** 
2. 选择使用 **vue** 的版本

1. 启动项目 **npm run serve** 
2. 打包项目 **npm run build** 

1. 暂停项目  **Ctrl+C** 

`Vue脚手架`隐藏了所有`webpack`相关的配置，若想查看具体的`webpack`配置，请执行

```
vue inspect > output.js
```

#### 3.1.3. 脚手架文件结构

```markdown
.文件目录
├── node_modules 
├── public
│   ├── favicon.ico: 页签图标
│   └── index.html: 主页面
├── src
│   ├── assets: 存放静态资源
│   │   └── logo.png
│   │── component: 存放组件
│   │   └── HelloWorld.vue
│   │── App.vue: 汇总所有组件
│   └── main.js: 入口文件
├── .gitignore: git版本管制忽略的配置
├── babel.config.js: babel的配置文件
├── package.json: 应用包配置文件 
├── README.md: 应用描述文件
└── package-lock.json: 包版本控制文件
```



```
src/components/School.vue
<template>
  <div class="demo">
    <h2>学校名称：{{ name }}</h2>
    <h2>学校地址：{{ address }}</h2>
    <button @click="showName">点我提示学校名</button>
  </div>
</template>

<script>
  export default {
    name: "School",
    data() {
      return {
        name: "UESTC",
        address: "成都",
      };
    },
    methods: {showName() {alert(this.name);},},
  };
</script>

<style>
  .demo {background-color: orange;}
</style>
src/components/Student.vue
<template>
  <div>
    <h2>学生姓名：{{ name }}</h2>
    <h2>学生年龄：{{ age }}</h2>
  </div>
</template>

<script>
  export default {
    name: "Student",
    data() {
      return {
        name: "cess",
        age: 18,
      };
    },
  };
</script>
src/App.vue
<template>
	<div>
		<img src="./assets/logo.png" alt="">
		<School></School>
		<Student></Student>
	</div>
</template>

<script>
	// 引入组件
	import School from './components/School.vue'
	import Student from './components/Student.vue'

	export default {
		name:'App',
		components:{ School, Student }
	}
</script>
src/main.js
// 该文件是整个项目的入口文件

import Vue from 'vue'				// 引入Vue
import App from './App.vue'	// 引入App组件，它是所有组件的父组件

Vue.config.productionTip = false

new Vue({
	el:'#app',
  render: h => h(App),			// render函数完成了这个功能：将App组件放入容器中
})// .$mount('#app')
public/index.html
<!DOCTYPE html>
<html lang="">
    <head>
        <meta charset="UTF-8">
      
        <!-- 针对IE浏览器的特殊配置，含义是让IE浏览器以最高渲染级别渲染页面 -->
        <meta http-equiv="X-UA-Compatible" content="IE=edge">
      
        <!-- 开启移动端的理想端口 -->
        <meta name="viewport" content="width=device-width, initial-scale=1.0">
      
        <!-- 配置页签图标 <%= BASE_URL %>是public所在路径，使用绝对路径 -->
        <link rel="icon" href="<%= BASE_URL %>favicon.ico">
      
        <!-- 配置网页标题 -->
        <title><%= htmlWebpackPlugin.options.title %></title>
    </head>
    <body>
      
      	<!-- 当浏览器不支持js时，noscript中的元素就会被渲染 -->
      	<noscript>
      		<strong>We're sorry but <%= htmlWebpackPlugin.options.title %> doesn't work properly without JavaScript enabled. Please enable it to continue.</strong>
    		</noscript>
          
        <!-- 容器 -->
        <div id="app"></div>
    </body>
</html>
```

![img](https://cdn.nlark.com/yuque/0/2022/png/1379492/1643446691351-d64acac5-b627-4501-9ac1-c45ad6d1b04b.png)

#### 3.1.4. render 函数

```javascript
import Vue from 'vue'
import App from './App.vue'

Vue.config.productionTip = false

new Vue({
  el:'#app',
  // render函数功能：将App组件放入容器中
  // 简写形式
  render: h => h(App),
  // 完整形式
  // render(createElement){
  //   return createElement(App)
  // }
})
```

#### 3.1.5. 关于不同版本的函数

1.   **vue.js** 与 **vue.runtime.xxx.js** 的区别 

1. 1. **vue.js** 是完整版的 **Vue** ，包含：核心功能+模板解析器
   2. **vue.runtime.xxx.js** 是运行版的`Vue`，只包含核心功能，没有模板解析器

`esm` 就是 ES6 module

1.  因为 **vue.runtime.xxx.js** 没有模板解析器，所以不能使用 **template** 配置项，需要使用 **render** 函数接收到的 **createElement** 函数去指定具体内容

#### 3.1.6. vue.config.js 配置文件

 **vue inspect > output.js** 可以查看到Vue脚手架的默认配置

使用 **vue.config.js** 可以对脚手架进行个性化定制，和 **package.json** 同级目录，详见 [**配置参考 | Vue CLI**](https://cli.vuejs.org/zh/config/#vue-config-js)

```javascript
module.exports = {
  pages: {
    index: {
      entry: 'src/index/main.js' // 入口
    }
  },
  lineOnSave: false	// 关闭语法检查

```

# Vue CLI ref props mixin plugin scoped

### 3.2. ref 属性

 **ref** 被用来给元素或子组件注册引用信息（id的替代者）

- 应用在 **html** 标签上获取的是真实`DOM元素`，应用在组件标签上获取的是组件实例对象`vc`
- 使用方式 

1. 1. 打标识：`<h1 ref="xxx"></h1>`或`<School ref="xxx"></School>`
   2. 获取： **this.$refs.****xxx** 

```vue
<template>
  <div>
    <h1 v-text="msg" ref="title"></h1>
    <button ref="btn" @click="showDOM">点我输出上方的DOM元素</button>
    <School ref="sch"/>
  </div>
</template>

<script>
  import School from './components/School'

  export default {
    name:'App',
    components:{ School },
    data() {
      return {
        msg:'欢迎学习Vue！'
      }
    },
    methods: {
      showDOM(){
        console.log(this.$refs.title)	// 真实DOM元素
        console.log(this.$refs.btn)		// 真实DOM元素
        console.log(this.$refs.sch)		// School组件的实例对象（vc）
      }
    },
  }
</script>
```

![img](https://cdn.nlark.com/yuque/0/2022/png/1379492/1643459981897-20c4d337-2ffb-49c5-b771-4a0d74f2c47d.png)

### 3.3. props 配置项

 **props** 让组件接收外部传过来的数据 

- 传递数据 **<Demo** **name="xxx" :age="18"****/>** 这里age前加`:`，通过v-bind使得里面的18是数字
- 接收数据

 第一种方式（只接收） **props:[****'name', 'age'****]**  

 第二种方式（限制类型） **props:{****name:String, age:Number****}** 

 第三种方式（限制类型、限制必要性、指定默认值） 

```javascript
props: {
    name: {
        type: String,	 // 类型
        required: true,// 必要性
        default: 'cess'// 默认值
    }
}
```

**备注**：**props是只读的**，`Vue`底层会监测你对`props`的修改，如果进行了修改，就会发出警告，若业务需求确实需要修改，那么请复制`props`的内容到`data`中，然后去修改`data`中的数据



```js
src/App.vue
<template>
  <div>
    <Student name="李四" sex="女" :age="18"/>
    <Student name="王五" sex="男" :age="18"/>
  </div>
</template>

<script>
  import Student from './components/Student'

  export default {
    name:'App',
    components:{ Student }
  }
</script>
src/components/Student.vue
<template>
  <div>
    <h1>{{ msg }}</h1>
    <h2>学生姓名：{{ name }}</h2>
    <h2>学生性别：{{ sex }}</h2>
    <h2>学生年龄：{{ myAge + 1 }}</h2>
    <button @click="updateAge">尝试修改收到的年龄</button>
  </div>
</template>

<script>
export default {
  name: "Student",
  data() {
    console.log(this);
    return {
      msg: "我是一个UESTC大学的学生",
      myAge: this.age,
    };
  },
  methods: { updateAge() { this.myAge++; }, },
  // 简单声明接收
  // props:['name','age','sex']

  // 接收的同时对数据进行类型限制
  //   props: {
  //     name: String,
  //     age: Number,
  //     sex: String,
  //   }

  // 接收的同时对数据：进行类型限制+默认值的指定+必要性的限制
  props: {
    name: {
      type: String, 	//name的类型是字符串
      required: true, //name是必要的
    },
    age: {
      type: Number,
      default: 99, //默认值
    },
    sex: {
      type: String,
      required: true,
    },
  },
};
</script>
```

![img](https://cdn.nlark.com/yuque/0/2022/png/1379492/1643462357799-42fb82fc-969a-4f41-b0dc-ae73f2fa38e1.png)

### 3.4. `mixin` 混入

1.  功能：可以把多个组件共用的配置提取成一个混入对象 
2.  使用方式

1. 1.  定义混入

```javascript
const mixin = {
    data() {....},
    methods: {....}
    ....
}
```

1. 1.  使用混入

1. 1. 1. 全局混入 **Vue.mixin(xxx)** 
      2. 局部混入 **mixins:['xxx']** 

**备注**

1. 组件和混入对象含有同名选项时，这些选项将以恰当的方式进行“合并”，在发生冲突时以组件优先

```javascript
var mixin = {
	data: function () {
		return {
    		message: 'hello',
            foo: 'abc'
    	}
  	}
}

new Vue({
  	mixins: [mixin],
  	data () {
    	return {
      		message: 'goodbye',
            	bar: 'def'
    	}
    },
  	created () {
    	console.log(this.$data)
    	// => { message: "goodbye", foo: "abc", bar: "def" }
  	}
})
```

1. 同名生命周期钩子将合并为一个数组，**因此都将被调用**。另外，混入对象的钩子将在组件自身钩子之前调用

```javascript
var mixin = {
  	created () {
    	console.log('混入对象的钩子被调用')
  	}
}

new Vue({
  	mixins: [mixin],
  	created () {
    	console.log('组件钩子被调用')
  	}
})

// => "混入对象的钩子被调用"
// => "组件钩子被调用"
```



```
src/mixin.js
export const hunhe = {
	methods: {
		showName(){
			alert(this.name)
		}
	},
	mounted() {
		console.log('你好啊！')
	},
}

export const hunhe2 = {
	data() {
		return {
			x:100,
			y:200
		}
	},
}
src/components/School.vue
<template>
  <div>
    <h2 @click="showName">学校名称：{{name}}</h2>
    <h2>学校地址：{{address}}</h2>
  </div>
</template>

<script>
  //引入一个hunhe
  import {hunhe,hunhe2} from '../mixin'

  export default {
    name:'School',
    data() {
      return {
        name:'尚硅谷',
        address:'北京',
        x:666
      }
    },
    mixins:[hunhe,hunhe2]	// 局部混入
  }
</script>
src/components/Student.vue
<template>
  <div>
    <h2 @click="showName">学生姓名：{{name}}</h2>
    <h2>学生性别：{{sex}}</h2>
  </div>
</template>

<script>
  import {hunhe,hunhe2} from '../mixin'

  export default {
    name:'Student',
    data() {
      return {
        name:'张三',
        sex:'男'
      }
    },
    mixins:[hunhe,hunhe2]	// 局部混入
  }
</script>
src/App.vue
<template>
  <div>
    <School/>
    <hr>
    <Student/>
  </div>
</template>

<script>
  import School from './components/School'
  import Student from './components/Student'

  export default {
    name:'App',
    components:{School,Student}
  }
</script>
src/main.js
import Vue from 'vue'
import App from './App.vue'
// import {mixin} from './mixin'

Vue.config.productionTip = false
// Vue.mixin(hunhe)		// 全局混合引入
// Vue.mixin(hunhe2)	// 全局混合

new Vue({
    el:"#app",
    render: h => h(App)
})
```

![img](https://cdn.nlark.com/yuque/0/2022/png/1379492/1643464071758-c6a1782c-1206-4a57-900d-260b78bceac4.png)

### 3.5. `plugin` 插件

1. 功能：用于增强`Vue`
2. 本质：包含`install`方法的一个对象，`install`的第一个参数是`Vue`，第二个以后的参数是插件使用者传递的数据

1. 定义插件（见下 src/plugin.js）

1. 使用插件： **Vue.use()** 



```
src/plugin.js
export default {
  install(Vue,x,y,z){
    console.log(x,y,z)
    //全局过滤器
    Vue.filter('mySlice', function(value){return value.slice(0,4)})

    //定义全局指令
    Vue.directive('fbind',{
      //指令与元素成功绑定时（一上来）
      bind(element,binding){element.value = binding.value},
      //指令所在元素被插入页面时
      inserted(element,binding){element.focus()},
      //指令所在的模板被重新解析时
      update(element,binding){element.value = binding.value}
    })

    //定义混入
    Vue.mixin({
      data() {return {x:100,y:200}},
    })

    //给Vue原型上添加一个方法（vm和vc就都能用了）
    Vue.prototype.hello = ()=>{alert('你好啊')}
  }
}
src/main.js
import Vue from 'vue'
import App from './App.vue'
import plugins from './plugins'	// 引入插件

Vue.config.productionTip = false

Vue.use(plugins,1,2,3)	// 应用（使用）插件

new Vue({
	el:'#app',
	render: h => h(App)
})
src/components/School.vue
<template>
  <div>
    <h2>学校名称：{{ name | mySlice }}</h2>
    <h2>学校地址：{{ address }}</h2>
    <button @click="test">点我测试一个hello方法</button>
  </div>
</template>

<script>
  export default {
    name:'School',
    data() {
      return {
        name:'尚硅谷atguigu',
        address:'北京',
      }
    },
    methods: {
      test(){
        this.hello()
      }
    },
  }
</script>
src/components/Student.vue
<template>
  <div>
    <h2>学生姓名：{{ name }}</h2>
    <h2>学生性别：{{ sex }}</h2>
    <input type="text" v-fbind:value="name">
  </div>
</template>

<script>
  export default {
    name:'Student',
    data() {
      return {
        name:'张三',
        sex:'男'
      }
    },
  }
</script>
```

![img](https://cdn.nlark.com/yuque/0/2022/png/1379492/1643466450842-b2d9f663-40fc-4044-97df-6552db14653a.png)

### 3.6. `scoped`样式

1. 作用：让样式在局部生效，防止冲突
2. 写法： **<style scoped>** 

`Vue`中的`webpack`并没有安装最新版，导致有些插件也不能默认安装最新版，如 `npm i less-loader@7`，而不是最新版



```
src/components/School.vue
<template>
  <div class="demo">
    <h2 class="title">学校名称：{{ name }}</h2>
    <h2>学校地址：{{ address }}</h2>
  </div>
</template>

<script>
  export default {
    name:'School',
    data() {
      return {
        name:'尚硅谷atguigu',
        address:'北京',
      }
    }
  }
</script>

<style scoped>
  .demo{
    background-color: skyblue;
  }
</style>
src/components/Student.vue
<template>
  <div class="demo">
    <h2 class="title">学生姓名：{{ name }}</h2>
    <h2 class="atguigu">学生性别：{{ sex }}</h2>
  </div>
</template>

<script>
  export default {
    name: 'Student',
    data() {
      return {
        name: '张三',
        sex: '男'
      }
    }
  }
</script>

<style lang="less" scoped>
  .demo {
    background-color: pink;
    .atguigu {
      font-size: 40px;
    }
  }
</style>
src/App.vue
<template>
  <div>
    <h1 class="title">你好啊</h1>
    <School/>
    <Student/>
  </div>
</template>

<script>
  import Student from './components/Student'
  import School from './components/School'

  export default {
    name: 'App',
    components: { School, Student }
  }
</script>

<style scoped>
  .title {
    color: red;
  }
</style>
```

![img](https://cdn.nlark.com/yuque/0/2022/png/1379492/1643468056061-42cadc59-cb6d-4e44-a0d4-c46e4221b0c7.png)



# Vue CLI Todo-List案例

### 3.7. Todo-List 案例

**组件化编码流程**

1. 拆分静态组件：组件要按照功能点拆分，命名不要与`html`元素冲突
2. 实现动态组件：考虑好数据的存放位置，数据是一个组件在用，还是一些组件在用

- - 一个组件在用：放在组件自身即可
  - **一些组件在用：放在他们共同的父组件上**（状态提升）

1. 实现交互：从绑定事件开始



 **props** 适用于

1. 1. 父组件 ==> 子组件 通信
   2. 子组件 ==> 父组件 通信（要求父组件先给子组件一个函数）



使用 **v-model** 时要切记：`v-model`绑定的值不能是`props`传过来的值，因为`props`是不可以修改的 

`props`传过来的若是对象类型的值，修改对象中的属性时`Vue`不会报错，但不推荐这样做



#### `src/App.vue`

```vue
<template>
  <div id="root">
    <div class="todo-container">
      <div class="todo-wrap">
        <MyHeader :addTodo="addTodo"/>
        <MyList :todos="todos" :checkTodo="checkTodo" :deleteTodo="deleteTodo"/>
        <MyFooter :todos="todos" 
                  :checkAllTodo="checkAllTodo" :clearAllTodo="clearAllTodo"/>
    	</div>
    </div>
  </div>
</template>

<script>
  import MyHeader from './components/MyHeader'
  import MyList from './components/MyList'
  import MyFooter from './components/MyFooter.vue'

  export default {
    name: 'App',
    components: { MyHeader, MyList, MyFooter },
    data() {
      return {
        // 由于todos是MyHeader组件和MyFooter组件都在使用，所以放在App中（状态提升）
        todos:[
          {id:'001',title:'抽烟',done:true},
          {id:'002',title:'喝酒',done:false},
          {id:'003',title:'开车',done:true}
        ]
      }
    },
    methods: {
      //添加一个todo
      addTodo(todoObj){
        this.todos.unshift(todoObj)
      },
      //勾选or取消勾选一个todo
      checkTodo(id){
        this.todos.forEach((todo)=>{
          if(todo.id === id) todo.done = !todo.done
        })
      },
      //删除一个todo
      deleteTodo(id){
        this.todos = this.todos.filter( todo => todo.id !== id )
      },
      //全选or取消全选
      checkAllTodo(done){
        this.todos.forEach((todo)=>{
          todo.done = done
        })
      },
      //清除所有已经完成的todo
      clearAllTodo(){
        this.todos = this.todos.filter((todo)=>{
          return !todo.done
        })
      }
    }
  }
</script>

<style>
  /*base*/
  body {background: #fff;}
  .btn {display: inline-block;padding: 4px 12px;margin-bottom: 0;font-size: 14px;
    line-height: 20px;text-align: center;vertical-align: middle;cursor: pointer;
    box-shadow: inset 0 1px 0 rgba(255, 255, 255, 0.2), 0 1px 2px rgba(0, 0, 0, 0.05);
    border-radius: 4px;}
  .btn-danger {color: #fff;background-color: #da4f49;border: 1px solid #bd362f;}
  .btn-danger:hover {color: #fff;background-color: #bd362f;}
  .btn:focus {outline: none;}
  .todo-container {width: 600px;margin: 0 auto;}
  .todo-container .todo-wrap {padding: 10px;border: 1px solid #ddd;border-radius: 5px;}
</style>
```

#### `src/components/MyHeader.vue`

```vue
<template>
	<div class="todo-header">
		<input type="text" placeholder="请输入你的任务名称，按回车键确认" 
           v-model="title" @keyup.enter="add"/>
	</div>
</template>

<script>
	import {nanoid} from 'nanoid'
	export default {
		name:'MyHeader',
		props:['addTodo'],	// 接收从App传递过来的addTodo
		data() {
			return {
				title:''				// 收集用户输入的title
			}
		},
		methods: {
			add(){
				// 校验数据
				if(!this.title.trim()) return alert('输入不能为空')
				// 将用户的输入包装成一个todo对象
				const todoObj = { id:nanoid(), title:this.title, done:false }
				// 通知App组件去添加一个todo对象
				this.addTodo(todoObj)
				// 清空输入
				this.title = ''
			}
		},
	}
</script>

<style scoped>
	/*header*/
	.todo-header input {width: 560px;height: 28px;font-size: 14px;
    border: 1px solid #ccc;border-radius: 4px;padding: 4px 7px;}
	.todo-header input:focus {outline: none;border-color: rgba(82, 168, 236, 0.8);
		box-shadow: inset 0 1px 1px rgba(0, 0, 0, 0.075), 0 0 8px rgba(82, 168, 236, 0.6);}
</style>
```

#### `src/components/MyList.vue`

```vue
<template>
  <ul class="todo-main">
    <MyItem v-for="todoObj in todos":key="todoObj.id" 
            :todo="todoObj" :checkTodo="checkTodo":deleteTodo="deleteTodo"/>
  </ul>
</template>

<script>
  import MyItem from './MyItem'

  export default {
    name:'MyList',
    components:{MyItem},
    // 声明接收App传递的数据，其中todos是自己用的，checkTodo和deleteTodo是给子组件MyItem用的
    props:['todos','checkTodo','deleteTodo']
  }
</script>

<style scoped>
  /*main*/
  .todo-main {margin-left: 0px;border: 1px solid #ddd;border-radius: 2px;padding: 0px;}
  .todo-empty {height: 40px;line-height: 40px;border: 1px solid #ddd;
    border-radius: 2px;padding-left: 5px;margin-top: 10px;}
</style>
```

#### `src/components/MyItem.vue`

```vue
<template>
  <li>
    <label>
      <!-- 如下代码也能实现功能，但是不太推荐，因为有点违反原则，因为修改了props -->
      <!-- <input type="checkbox" v-model="todo.done"/> -->
      <input type="checkbox" :checked="todo.done" @change="handleCheck(todo.id)"/>  
      <span>{{ todo.title }}</span>
    </label>
    <button class="btn btn-danger" @click="handleDelete(todo.id)">删除</button>
  </li>
</template>

<script>
  export default {
    name:'MyItem',
    //声明接收todo、checkTodo、deleteTodo
    props:['todo','checkTodo','deleteTodo'],
    methods: {
      // 勾选or取消勾选
      handleCheck(id){
        this.checkTodo(id)	// 通知App组件将对应的todo对象的done值取反
      },
      // 删除
      handleDelete(id){
        if(confirm('确定删除吗？')){
          this.deleteTodo(id)	// 通知App组件将对应的todo对象删除
        }
      }
    },
  }
</script>

<style scoped>
  /*item*/
  li {list-style: none;height: 36px;line-height: 36px;padding: 0 5px;
    border-bottom: 1px solid #ddd;}
  li label {float: left;cursor: pointer;}
  li label li input {vertical-align:middle; margin-right:6px; position:relative;top: -1px;}
  li button {float: right;display: none;margin-top: 3px;}
  li:before {content: initial;}
  li:last-child {border-bottom: none;}
  li:hover{background-color: #ddd;}
  li:hover button{display: block;}
</style>
```

#### `src/components/MyFooter.vue`

```vue
<template>
  <div class="todo-footer" v-show="total">
    <label>
      <!-- <input type="checkbox" :checked="isAll" @change="checkAll"/> -->
      <input type="checkbox" v-model="isAll"/>
    </label>
    <span>
      <span>已完成{{ doneTotal }}</span> / 全部{{ total }}
    </span>
    <button class="btn btn-danger" @click="clearAll">清除已完成任务</button>
  </div>
</template>

<script>
  export default {
    name:'MyFooter',
    props:['todos','checkAllTodo','clearAllTodo'],
    computed: {
      // 总数
      total(){
        return this.todos.length
      },
      // 已完成数
      doneTotal(){
        //此处使用reduce方法做条件统计
        return this.todos.reduce((pre,todo)=> pre + (todo.done ? 1 : 0) ,0)
      },
      // 控制全选框
      isAll:{
        //全选框是否勾选
        get(){
          return this.doneTotal === this.total && this.total > 0
        },
        //isAll被修改时set被调用
        set(value){
          this.checkAllTodo(value)
        }
      }
    },
    methods: {
      /* checkAll(e){
				this.checkAllTodo(e.target.checked)
			} */
      //清空所有已完成
      clearAll(){
        this.clearAllTodo()
      }
    },
  }
</script>

<style scoped>
  /*footer*/
  .todo-footer {height: 40px;line-height: 40px;padding-left: 6px;margin-top: 5px;}
  .todo-footer label {display: inline-block;margin-right: 20px;cursor: pointer;}
  .todo-footer label input {position: relative;top: -1px;vertical-align: middle;
    margin-right: 5px;}
  .todo-footer button {float: right;margin-top: 5px;}
</style>
```

![img](https://cdn.nlark.com/yuque/0/2022/png/1379492/1643548219463-885d25c6-49b8-426b-9833-fe023c1d2ede.png)



# Vue CLI 本地存储 自定义事件

### 3.8. WebStorage（js 本地存储）

存储内容大小一般支持 **5MB** 左右（不同浏览器可能还不一样） 

浏览器端通过 **Window.sessionStorage** 和 **Window.localStorage** 属性来实现本地存储机制 

相关API

 **xxxStorage.****setItem****('key', 'value')** 该方法接受一个键和值作为参数，会把键值对添加到存储中，如果键名存在，则更新其对应的值

 **xxxStorage.****getItem****('key')** 该方法接受一个键名作为参数，返回键名对应的值

 **xxxStorage.****removeItem****('key')** 该方法接受一个键名作为参数，并把该键名从存储中删除

 **xxxStorage.****clear****()** 该方法会清空存储中的所有数据

备注

- - `SessionStorage`存储的内容会随着浏览器窗口关闭而消失
  - `LocalStorage`存储的内容，需要手动清除才会消失

- - `xxxStorage.getItem(xxx)`如果 xxx 对应的 value 获取不到，那么`getItem()`的返回值是`null`
  - `JSON.parse(null)`的结果依然是`null`

localStorage

```html
<h2>localStorage</h2>
<button onclick="saveDate()">点我保存数据</button><br/>
<button onclick="readDate()">点我读数据</button><br/>
<button onclick="deleteDate()">点我删除数据</button><br/>
<button onclick="deleteAllDate()">点我清空数据</button><br/>

<script>
  let person = {name:"JOJO",age:20}

  function saveDate(){
    localStorage.setItem('msg','localStorage')
    localStorage.setItem('person',JSON.stringify(person))
  }
  function readDate(){
    console.log(localStorage.getItem('msg'))
    const person = localStorage.getItem('person')
    console.log(JSON.parse(person))
  }
  function deleteDate(){
    localStorage.removeItem('msg')
    localStorage.removeItem('person')
  }
  function deleteAllDate(){
    localStorage.clear()
  }
</script>
```

sessionStorage

```html
<h2>sessionStorage</h2>
<button onclick="saveDate()">点我保存数据</button><br/>
<button onclick="readDate()">点我读数据</button><br/>
<button onclick="deleteDate()">点我删除数据</button><br/>
<button onclick="deleteAllDate()">点我清空数据</button><br/>

<script>
  let person = {name:"JOJO",age:20}

  function saveDate(){
    sessionStorage.setItem('msg','sessionStorage')
    sessionStorage.setItem('person',JSON.stringify(person))
  }
  function readDate(){
    console.log(sessionStorage.getItem('msg'))
    const person = sessionStorage.getItem('person')
    console.log(JSON.parse(person))
  }
  function deleteDate(){
    sessionStorage.removeItem('msg')
    sessionStorage.removeItem('person')
  }
  function deleteAllDate(){
    sessionStorage.clear()
  }
</script>
```

#### 使用本地存储优化Todo-List

```
src/App.vue
<template>
	<div id="root">
		<div class="todo-container">
			<div class="todo-wrap">
				<MyHeader :addTodo="addTodo"/>
				<MyList :todos="todos" :checkTodo="checkTodo" :deleteTodo="deleteTodo"/>
				<MyFooter :todos="todos" :checkAllTodo="checkAllTodo" :clearAllTodo="clearAllTodo"/>
			</div>
		</div>
	</div>
</template>

<script>
	import MyHeader from './components/MyHeader'
	import MyList from './components/MyList'
	import MyFooter from './components/MyFooter.vue'

	export default {
		name:'App',
		components:{MyHeader,MyList,MyFooter},
		data() {
			return {
				// 🔴从本地存储中获得数据，null就创建空数组[]
				todos:JSON.parse(localStorage.getItem('todos')) || []
			}
		},
		methods: {
			//添加一个todo
			addTodo(todoObj){
				this.todos.unshift(todoObj)
			},
			//勾选or取消勾选一个todo
			checkTodo(id){
				this.todos.forEach((todo)=>{
					if(todo.id === id) todo.done = !todo.done
				})
			},
			//删除一个todo
			deleteTodo(id){
				this.todos = this.todos.filter( todo => todo.id !== id )
			},
			//全选or取消全选
			checkAllTodo(done){
				this.todos.forEach((todo)=>{
					todo.done = done
				})
			},
			//清除所有已经完成的todo
			clearAllTodo(){
				this.todos = this.todos.filter((todo)=>{
					return !todo.done
				})
			}
		},
    // 🔴数据发生改变就放到本地存储中，注意深度侦听，以及JSON转化为字符串
		watch: {
			todos:{
				deep:true,
				handler(value){
					localStorage.setItem('todos',JSON.stringify(value))
				}
			}
		},
	}
</script>
```

### 3.9. 组件的自定义事件

1. 一种组件间通信的方式，适用于：**子组件 ===> 父组件**
2. 使用场景：**子组件**想给**父组件**传数据，那么就要在**父组件中给子组件绑定自定义事件**（事件的回调在A中）

1.  绑定自定义事件

1. 1.  第一种方式，在父组件中 **<Demo** **@事件名="方法"****/>** 或`<Demo v-on:事件名="方法"/>`
   2.  第二种方式，在父组件中 **this.$refs.demo.$on('事件名',方法)** 

```javascript
<Demo ref="demo"/>
......
mounted(){
   this.$refs.demo.$on('atguigu',this.test)
}
```

1. 1.  若想让自定义事件只能触发一次，可以使用 **once** 修饰符，或 **$once** 方法 

1.  触发自定义事件 **this.$emit(****'事件名',数据****)**  
2.  解绑自定义事件 **this.$off(****'事件名'****)**  

1.  组件上也可以绑定原生 **DOM** 事件，需要使用 **native** 修饰符  `@click.**native**="show"`

上面绑定自定义事件，即使绑定的是原生事件也会被认为是自定义的，需要加 **native** ，加了后就将此事件给组件的根元素

1.  注意：通过`this.$refs.xxx.$on('事件名',回调函数)`绑定自定义事件时，回调函数要么配置在`methods`中，要么用箭头函数，否则 **this** 指向会出问题



```
src/App.vue
<template>
  <div class="app">
    <h1>{{ msg }}，学生姓名是:{{ studentName }}</h1>
		
    <!-- 通过父组件给子组件传递函数类型的props实现子给父传递数据 -->
    <School :getSchoolName="getSchoolName"/>

    <!-- 通过父组件给子组件绑定一个自定义事件实现子给父传递数据（第一种写法，使用@或v-on） -->
    <!-- <Student @atguigu="getStudentName" @demo="m1"/> -->

    <!-- 通过父组件给子组件绑定一个自定义事件实现子给父传递数据（第二种写法，使用ref） -->
    <Student ref="student" @click.native="show"/> <!-- 🔴native -->
  </div>
</template>

<script>
  import Student from './components/Student'
  import School from './components/School'

  export default {
    name:'App',
    components:{School,Student},
    data() {
      return {
        msg:'你好啊！',
        studentName:''
      }
    },
    methods: {
      getSchoolName(name){
        console.log('App收到了学校名：',name)
      },
      getStudentName(name,...params){
        console.log('App收到了学生名：',name,params)
        this.studentName = name
      },
      m1(){
        console.log('demo事件被触发了！')
      },
      show(){
        alert(123)
      }
    },
    mounted() {
      this.$refs.student.$on('atguigu',this.getStudentName) // 🔴绑定自定义事件
      // this.$refs.student.$once('atguigu',this.getStudentName) // 绑定自定义事件（一次性）
    },
  }
</script>

<style scoped>.app{background-color: gray;padding: 5px;}</style>
src/components/Student.vue
<template>
	<div class="student">
		<h2>学生姓名：{{name}}</h2>
		<h2>学生性别：{{sex}}</h2>
		<h2>当前求和为：{{number}}</h2>
		<button @click="add">点我number++</button>
		<button @click="sendStudentlName">把学生名给App</button>
		<button @click="unbind">解绑atguigu事件</button>
		<button @click="death">销毁当前Student组件的实例(vc)</button>
	</div>
</template>

<script>
	export default {
		name:'Student',
		data() {
			return {
				name:'张三',
				sex:'男',
				number:0
			}
		},
		methods: {
			add(){
				console.log('add回调被调用了')
				this.number++
			},
			sendStudentlName(){
				// 触发Student组件实例身上的atguigu事件
				this.$emit('atguigu',this.name,666,888,900)
				// this.$emit('demo')
				// this.$emit('click')
			},
			unbind(){
        // 🔴解绑
				this.$off('atguigu') //解绑一个自定义事件
				// this.$off(['atguigu','demo']) //解绑多个自定义事件
				// this.$off() //解绑所有的自定义事件
			},
			death(){
        // 销毁了当前Student组件的实例，销毁后所有Student实例的自定义事件全都不奏效
				this.$destroy()
			}
		},
	}
</script>

<style lang="less" scoped>
	.student{background-color: pink;padding: 5px;margin-top: 30px;}
</style>
```

#### 使用自定义事件优化Todo-List

```
src/App.vue
<template>
	<div id="root">
		<div class="todo-container">
			<div class="todo-wrap">
				<MyHeader @addTodo="addTodo"/>
				<MyList :todos="todos" :checkTodo="checkTodo" :deleteTodo="deleteTodo"/>
				<MyFooter :todos="todos" 
                  @checkAllTodo="checkAllTodo" @clearAllTodo="clearAllTodo"/>
			</div>
		</div>
	</div>
</template>

<script>
	import MyHeader from './components/MyHeader'
	import MyList from './components/MyList'
	import MyFooter from './components/MyFooter.vue'

	export default {
		name:'App',
		components:{MyHeader,MyList,MyFooter},
		data() {
			return {
				//由于todos是MyHeader组件和MyFooter组件都在使用，所以放在App中（状态提升）
				todos:JSON.parse(localStorage.getItem('todos')) || []
			}
		},
		methods: {
			//添加一个todo
			addTodo(todoObj){
				this.todos.unshift(todoObj)
			},
			//勾选or取消勾选一个todo
			checkTodo(id){
				this.todos.forEach((todo)=>{
					if(todo.id === id) todo.done = !todo.done
				})
			},
			//删除一个todo
			deleteTodo(id){
				this.todos = this.todos.filter( todo => todo.id !== id )
			},
			//全选or取消全选
			checkAllTodo(done){
				this.todos.forEach((todo)=>{
					todo.done = done
				})
			},
			//清除所有已经完成的todo
			clearAllTodo(){
				this.todos = this.todos.filter((todo)=>{
					return !todo.done
				})
			}
		},
		watch: {
			todos:{
				deep:true,
				handler(value){
					localStorage.setItem('todos',JSON.stringify(value))
				}
			}
		},
	}
</script>
src/components/MyHeader.vue
<template>
	<div class="todo-header">
		<input type="text" placeholder="请输入你的任务名称，按回车键确认" 
           v-model="title" @keyup.enter="add"/>
	</div>
</template>

<script>
	import {nanoid} from 'nanoid'
	export default {
		name:'MyHeader',
		data() {
			return {
				title:''	// 收集用户输入的title
			}
		},
		methods: {
			add(){
				//校验数据
				if(!this.title.trim()) return alert('输入不能为空')
				//将用户的输入包装成一个todo对象
				const todoObj = {id:nanoid(),title:this.title,done:false}
				//通知App组件去添加一个todo对象
				this.$emit('addTodo',todoObj)
				//清空输入
				this.title = ''
			}
		},
	}
</script>
src/components/MyFooter
<template>
	<div class="todo-footer" v-show="total">
		<label>
			<!-- <input type="checkbox" :checked="isAll" @change="checkAll"/> -->
			<input type="checkbox" v-model="isAll"/>
		</label>
		<span>
			<span>已完成{{ doneTotal }}</span> / 全部{{ total }}
		</span>
		<button class="btn btn-danger" @click="clearAll">清除已完成任务</button>
	</div>
</template>

<script>
	export default {
		name:'MyFooter',
		props:['todos'],
		computed: {
			//总数
			total(){
				return this.todos.length
			},
			//已完成数
			doneTotal(){
				return this.todos.reduce((pre,todo)=> pre + (todo.done ? 1 : 0) ,0)
			},
			//控制全选框
			isAll:{
				//全选框是否勾选
				get(){
					return this.doneTotal === this.total && this.total > 0
				},
				//isAll被修改时set被调用
				set(value){
					// this.checkAllTodo(value)
					this.$emit('checkAllTodo',value)
				}
			}
		},
		methods: {
			//清空所有已完成
			clearAll(){
				// this.clearAllTodo()
				this.$emit('clearAllTodo')
			}
		},
	}
</script>
```

# Vue CLI 全局事件总线 消息的订阅与发布

### 3.10. 全局事件总线（GlobalEventBus）

**一种可以在任意组件间通信的方式**，本质上就是一个对象，它必须满足以下条件

1. 所有的组件对象都必须能看见他 
2. 这个对象必须能够使用 **$on**  **$emit**  **$off** 方法去绑定、触发和解绑事件

**使用步骤**

1.  定义全局事件总线

```javascript
new Vue({
   	...
   	beforeCreate() {
   		Vue.prototype.$bus = this // 安装全局事件总线，$bus 就是当前应用的 vm
   	},
    ...
})
```

1. 使用事件总线 

1. 1. 接收数据：A组件想接收数据，则在A组件中给 **$bus** 绑定自定义事件，事件的回调留在A组件自身 

```javascript
export default {
    methods(){
        demo(data){...}
    }
    ...
    mounted() {
        this.$bus.$on('xxx',this.demo)
    }
}
```

1. 1. 提供数据： **this.$bus.$emit(**'xxx',**data)**  

1. 最好在`beforeDestroy`钩子中，用 **$off()** 去解绑当前组件所用到的事件



```
src/**main**.js
import Vue from 'vue'
import App from './App.vue'

Vue.config.productionTip = false

new Vue({
  el:'#app',
  render: h => h(App),
  beforeCreate() {
    Vue.prototype.$bus = this // 安装全局事件总线
  }
})
src/App.vue
<template>
	<div class="app">
		<School/>
		<Student/>
	</div>
</template>

<script>
	import Student from './components/Student'
	import School from './components/School'

	export default {
		name:'App',
		components:{ School, Student }
	}
</script>

<style scoped>.app{background-color: gray;padding: 5px;}</style>
src/components/**School**.vue
<template>
  <div class="school">
    <h2>学校名称：{{ name }}</h2>
    <h2>学校地址：{{ address }}</h2>
  </div>
</template>

<script>
  export default {
    name: "School",
    data() {
      return {
        name: "尚硅谷",
        address: "北京",
      };
    },
    mounted() {  //🔴
      // console.log('School',this)
      this.$bus.$on("hello", (data) => {
        console.log("我是School组件，收到了数据", data);
      });
    },
    beforeDestroy() {  //🔴
      this.$bus.$off("hello");
    },
  };
</script>

<style scoped>.school {background-color: skyblue;padding: 5px;}</style>
src/components/**Student**.vue
<template>
  <div class="student">
    <h2>学生姓名：{{ name }}</h2>
    <h2>学生性别：{{ sex }}</h2>
    <button @click="sendStudentName">把学生名给School组件</button> //🔴
  </div>
</template>

<script>
  export default {
    name:'Student',
    data() {
      return {
        name:'张三',
        sex:'男'
      }
    },
    methods: {  //🔴
      sendStudentName(){
        this.$bus.$emit('demo', this.name)
      }
    }
  }
</script>

<style scoped>.student{background-color: pink;padding: 5px;margin-top: 30px;}</style>
```

![img](https://cdn.nlark.com/yuque/0/2022/png/1379492/1643705880838-5cbf95b9-5461-48ee-9e33-c2256533665b.png)

**使用自定义事件优化Todo-List**

```
src/**mian**.js
import Vue from 'vue'
import App from './App.vue'
Vue.config.productionTip = false

new Vue({
  el:'#app',
  render: h => h(App),
  beforeCreate() {
    Vue.prototype.$bus = this
  },
})
src/App.vue
<template>
  <div id="root">
    <div class="todo-container">
      <div class="todo-wrap">
        <MyHeader @addTodo="addTodo" />
        <MyList :todos="todos"/>
        <MyFooter :todos="todos" @checkAllTodo="checkAllTodo" @clearAllTodo="clearAllTodo"/>
    </div>
    </div>
  </div>
</template>

<script>
  import MyHeader from "./components/MyHeader";
  import MyList from "./components/MyList";
  import MyFooter from "./components/MyFooter.vue";

  export default {
    name: "App",
    components: { MyHeader, MyList, MyFooter },
    data() {
      return {
        //由于todos是MyHeader组件和MyFooter组件都在使用，所以放在App中（状态提升）
        todos: JSON.parse(localStorage.getItem("todos")) || [],
      };
    },
    methods: {
      //添加一个todo
      addTodo(todoObj) {
        this.todos.unshift(todoObj);
      },
      //勾选or取消勾选一个todo
      checkTodo(id) {
        this.todos.forEach((todo) => {
          if (todo.id === id) todo.done = !todo.done;
        });
      },
      //删除一个todo
      deleteTodo(id) {
        this.todos = this.todos.filter((todo) => todo.id !== id);
      },
      //全选or取消全选
      checkAllTodo(done) {
        this.todos.forEach((todo) => {
          todo.done = done;
        });
      },
      //清除所有已经完成的todo
      clearAllTodo() {
        this.todos = this.todos.filter((todo) => {
          return !todo.done;
        });
      },
    },
    watch: {
      todos: {
        deep: true,
        handler(value) {
          localStorage.setItem("todos", JSON.stringify(value));
        },
      },
    },
    mounted() {
      this.$bus.$on("checkTodo", this.checkTodo);
      this.$bus.$on("deleteTodo", this.deleteTodo);
    },
    beforeDestroy() {
      this.$bus.$off("checkTodo");
      this.$bus.$off("deleteTodo");
    },
  };
</script>
src/components/MyItem.vue
<template>
<li>
  <label>
    <input type="checkbox" :checked="todoObj.done" @change="handleCheck(todoObj.id)"/>
    <span>{{ todoObj.title }}</span>
  </label>
  <button class="btn btn-danger" @click="handleDelete(todoObj.id)">删除</button>
  </li>
</template>

<script>
  export default {
    name: "MyItem",
    data() {
      return {};
    },
    props: ["todoObj"], // 声明接受todoObj对象
    methods: {
      handleCheck(id) {
        this.$bus.$emit('checkTodo', id)
      },
      handleDelete(id) {
        if (confirm('确定删除吗？')) {
          this.$bus.$emit('deleteTodo', id)
        }
      }
    },
  };
</script>
```

### 3.11. 消息的订阅与发布（基本不用）

消息订阅与发布（pubsub）消息订阅与发布是一种组件间通信的方式，适用于任意组件间通信 

**使用步骤**

1. 安装pubsub： **npm i pubsub-js**  
2. 引入： **import pubsub from 'pubsub-js'**  

1. 接收数据：A组件想接收数据，则在A组件中订阅消息，订阅的回调留在A组件自身  

```javascript
export default {
    methods: {
        demo(msgName, data) {...}
    }
    ...
    mounted() {
			this.pid = pubsub.subscribe('xxx',this.demo)
    }
}
```

1. 提供数据：`pubsub.publish('xxx',data)` 
2. 最好在`beforeDestroy`钩子中，使用`pubsub.unsubscribe(pid)`取消订阅



```
src/components/School.vue
<template>
	<div class="school">
		<h2>学校名称：{{name}}</h2>
		<h2>学校地址：{{address}}</h2>
	</div>
</template>

<script>
	import pubsub from 'pubsub-js'

	export default {
		name: 'School',
		data() {
			return {
				name:'尚硅谷',
				address:'北京',
			}
		},
		methods: {
			demo(msgName, data) {
				console.log('我是School组件，收到了数据：',msgName, data)
			}
		},
		mounted() {
			this.pubId = pubsub.subscribe('demo', this.demo) // 订阅消息
		},
		beforeDestroy() {
			pubsub.unsubscribe(this.pubId) // 取消订阅
		}
	}
</script>

<style scoped>
	.school{
		background-color: skyblue;
		padding: 5px;
	}
</style>
src/components/Student.vue
<template>
  <div class="student">
    <h2>学生姓名：{{name}}</h2>
    <h2>学生性别：{{sex}}</h2>
    <button @click="sendStudentName">把学生名给School组件</button>
  </div>
</template>

<script>
  import pubsub from 'pubsub-js'

  export default {
    name:'Student',
    data() {
      return {
        name:'JOJO',
        sex:'男',
      }
    },
    methods: {
      sendStudentName(){
        pubsub.publish('demo', this.name) // 发布消息
      }
    }
  }
</script>

<style scoped>
  .student{
    background-color: pink;
    padding: 5px;
    margin-top: 30px;
  }
</style>
```



**使用消息的订阅与发布优化Todo-List**

```
src/App.vue
<template>
<div id="root">
  <div class="todo-container">
    <div class="todo-wrap">
      <MyHeader @addTodo="addTodo"/>
      <MyList :todos="todos"/>
      <MyFooter :todos="todos" @checkAllTodo="checkAllTodo" @clearAllTodo="clearAllTodo"/>
  	</div>
  </div>
</div>
</template>

<script>
  import pubsub from 'pubsub-js'	// 习惯第三方库写上面
  import MyHeader from './components/MyHeader.vue'
  import MyList from './components/MyList.vue'
  import MyFooter from './components/MyFooter.vue'


  export default {
    name:'App',
    components: { MyHeader,MyList,MyFooter },
    data() {
      return {
        todos:JSON.parse(localStorage.getItem('todos')) || []
      }
    },
    methods:{
      //添加一个todo
      addTodo(todoObj){
        this.todos.unshift(todoObj)
      },
      //勾选or取消勾选一个todo
      checkTodo(_,id){
        this.todos.forEach((todo)=>{
          if(todo.id === id) todo.done = !todo.done
        })
      },
      //删除一个todo
      deleteTodo(id){
        this.todos = this.todos.filter(todo => todo.id !== id)
      },
      //全选or取消勾选
      checkAllTodo(done){
        this.todos.forEach(todo => todo.done = done)
      },
      //删除已完成的todo
      clearAllTodo(){
        this.todos = this.todos.filter(todo => !todo.done)
      }
    },
    watch:{
      todos:{
        deep:true,
        handler(value){
          localStorage.setItem('todos',JSON.stringify(value))
        }
      }
    },
    mounted(){
      this.pubId = pubsub.subscribe('checkTodo',this.checkTodo)	// 两种对比
      this.$bus.$on('deleteTodo',this.deleteTodo)
    },
    beforeDestroy(){
      pubsub.unsubscribe(this.pubId)
      this.$bus.$off('deleteTodo')
    }
  }
</script>

<style>
  body {
    background: #fff;
  }

  .btn {
    display: inline-block;
    padding: 4px 12px;
    margin-bottom: 0;
    font-size: 14px;
    line-height: 20px;
    text-align: center;
    vertical-align: middle;
    cursor: pointer;
    box-shadow: inset 0 1px 0 rgba(255, 255, 255, 0.2), 0 1px 2px rgba(0, 0, 0, 0.05);
    border-radius: 4px;
  }

  .btn-danger {
    color: #fff;
    background-color: #da4f49;
    border: 1px solid #bd362f;
  }

  .btn-danger:hover {
    color: #fff;
    background-color: #bd362f;
  }

  .btn:focus {
    outline: none;
  }

  .todo-container {
    width: 600px;
    margin: 0 auto;
  }
  .todo-container .todo-wrap {
    padding: 10px;
    border: 1px solid #ddd;
    border-radius: 5px;
  }
</style>
src/components/myItem.vue
<template>
    <li>
        <label>
            <input type="checkbox" :checked="todo.done" @click="handleCheck(todo.id)"/>
            <span>{{todo.title}}</span>
        </label>
        <button class="btn btn-danger" @click="handleDelete(todo.id,todo.title)">删除</button>
    </li>
</template>

<script>
    import pubsub from 'pubsub-js'
    export default {
        name:'MyItem',
        props:['todo'],
        methods:{
            handleCheck(id){                    
                pubsub.publish('checkTodo',id)
            },
            handleDelete(id,title){
                if(confirm("确定删除任务："+title+"吗？")){
                    this.$bus.$emit('deleteTodo',id)
                }
            }
        }
    }
</script>

<style scoped>
    li {
        list-style: none;
        height: 36px;
        line-height: 36px;
        padding: 0 5px;
        border-bottom: 1px solid #ddd;
    }

    li label {
        float: left;
        cursor: pointer;
    }

    li label li input {
        vertical-align: middle;
        margin-right: 6px;
        position: relative;
        top: -1px;
    }

    li button {
        float: right;
        display: none;
        margin-top: 3px;
    }

    li:before {
        content: initial;
    }

    li:last-child {
        border-bottom: none;
    }

    li:hover {
        background-color: #eee;
    }

    li:hover button{
        display: block;
    }
</style>
```



# Vue CLI $nextTick 过渡与动画

### 

### 3.12. $nextTick

**这是一个生命周期钩子**

 **this.$nextTick(回调函数)** 在下一次`DOM`更新结束后执行其指定的回调

什么时候用：当改变数据后，要基于更新后的新`DOM`进行某些操作时，要在 **nextTick** 所指定的回调函数中执行

**使用 $nextTick 优化 Todo-List**

```
src/components/MyItem.vue
<template>
  <li>
    <label>
      <input type="checkbox" :checked="todo.done" @change="handleCheck(todo.id)"/>
      <span v-show="!todo.isEdit">{{ todo.title }}</span>
      <input type="text" v-show="todo.isEdit" :value="todo.title"
        @blur="handleBlur(todo, $event)" ref="inputTitle"/>
    </label>
    <button class="btn btn-danger" @click="handleDelete(todo.id)">删除</button>
    <button v-show="!todo.isEdit" class="btn btn-edit" @click="handleEdit(todo)">
      编辑
    </button>
  </li>
</template>

<script>
export default {
  name: "MyItem",
  
  props: ["todo"],	// 声明接收todo
  methods: {
    handleCheck(id) {		// 勾选or取消勾选
      // 通知App组件将对应的todo对象的done值取反
      // this.checkTodo(id)
      this.$bus.$emit("checkTodo", id);
    },
    handleDelete(id) {	// 删除
      if (confirm("确定删除吗？")) {
        // 通知App组件将对应的todo对象删除
        // this.deleteTodo(id)
        this.$bus.$emit('deleteTodo',id)
      }
    },
    handleEdit(todo) {	// 编辑
      if (todo.hasOwnProperty("isEdit")) {
        todo.isEdit = true;
      } else {
        this.$set(todo, "isEdit", true);
      }
      this.$nextTick(function () {
        this.$refs.inputTitle.focus();
      });
    },
    handleBlur(todo, e) {	// 失去焦点回调（真正执行修改逻辑）
      todo.isEdit = false;
      if (!e.target.value.trim()) return alert("输入不能为空！");
      this.$bus.$emit("updateTodo", todo.id, e.target.value);
    },
  },
};
</script>
```

![img](https://cdn.nlark.com/yuque/0/2022/png/1379492/1643800652401-9b23b7ef-f617-45dd-8974-c6f30e620c2c.png)

### 3.13. 过渡与动画

`Vue`封装的过度与动画：在插入、更新或移除`DOM`元素时，在合适的时候给元素添加样式类名

![img](https://cdn.nlark.com/yuque/0/2022/png/1379492/1643034414605-e2a3f595-ac72-4c74-9f11-12e7578592c9.png)

写法

1. 准备好样式

- - 元素进入的样式

1. 1. 1.  **v-enter** 		 	进入的起点
      2.  **v-enter-active** 	进入过程中

1. 1. 1.  **v-enter-to** 	 	进入的终点

- -  元素离开的样式

1. 1. 1.  **v-leave** 			离开的起点
      2.  **v-leave-active** 	离开过程中

1. 1. 1.  **v-leave-to** 		离开的终点

1. 使用 **<transition>** 包裹要过度的元素，并配置 **name** 属性，此时需要将上面样式名的`v`换为`name`
2. 要让页面一开始就显示动画，需要添加 **appear** 

```vue
<transition name="hello" appear>
  <h1 v-show="isShow">你好啊！</h1>
</transition>

<style>
  .hello-enter-active{
    animation: hello 0.5s linear;
  }

  .hello-leave-active{
    animation: hello 0.5s linear reverse;
  }

  @keyframes hello {
    from{
      transform: translateX(-100%);
    }
    to{
      transform: translateX(0px);
    }
  }
</style>
```

1. 备注：若有多个元素需要过度，则需要使用 **<transition-group>** ，且每个元素都要指定 **key** 值

```vue
<transition-group name="hello" appear>
  <h1 v-show="!isShow" key="1">你好啊！</h1>
  <h1 v-show="isShow" key="2">尚硅谷！</h1>
</transition-group>
```

1. 第三方动画库 **Animate.css** 

```vue
<transition-group appear
          name="animate__animated animate__bounce"
          enter-active-class="animate__swing"
          leave-active-class="animate__backOutUp">
  <h1 v-show="!isShow" key="1">你好啊！</h1>
  <h1 v-show="isShow" key="2">尚硅谷！</h1>
</transition-group>
```



```
src/App.vue
<template>
	<div>
		<Test/>
		<Test2/>
		<Test3/>
	</div>
</template>

<script>
	import Test from './components/Test'
	import Test2 from './components/Test2'
	import Test3 from './components/Test3'

	export default {
		name:'App',
		components:{Test,Test2,Test3},
	}
</script>
src/components/test.vue
<template>
  <div>
    <button @click="isShow = !isShow">显示/隐藏</button>
    <transition name="hello" appear>
      <h1 v-show="isShow">你好啊！</h1>
    </transition>
  </div>
</template>

<script>
  export default {
    name: 'Test',
    data() {return {isShow:true}},
  }
</script>

<style scoped>
  h1{background-color: orange;}

  .hello-enter-active{
    animation: atguigu 0.5s linear;
  }

  .hello-leave-active{
    animation: atguigu 0.5s linear reverse;
  }

  @keyframes atguigu {
    from{transform: translateX(-100%);}
    to{transform: translateX(0px);}
  }
</style>
src/components/test2
<template>
  <div>
    <button @click="isShow = !isShow">显示/隐藏</button>
    <transition-group name="hello" appear>
      <h1 v-show="!isShow" key="1">你好啊！</h1>
      <h1 v-show="isShow" key="2">尚硅谷！</h1>
    </transition-group>
  </div>
</template>

<script>
  export default {
    name:'Test',
    data() {return {isShow:true}},
  }
</script>

<style scoped>
  h1 {
    background-color: orange;
    /* transition: 0.5s linear; */
  }
  /* 进入的起点、离开的终点 */
  .hello-enter,.hello-leave-to {
    transform: translateX(-100%);
  }
  .hello-enter-active,.hello-leave-active{
    transition: 0.5s linear;
  }
  /* 进入的终点、离开的起点 */
  .hello-enter-to,.hello-leave {
    transform: translateX(0);
  }
</style>
```

![img](https://cdn.nlark.com/yuque/0/2022/png/1379492/1643034415424-a54a8454-e483-4503-b477-305feae8496b.png)

```
src/components/test3
<template>
  <div>
    <button @click="isShow = !isShow">显示/隐藏</button>
    <transition-group appear
                      name="animate__animated animate__bounce"
                      enter-active-class="animate__swing"
                      leave-active-class="animate__backOutUp">
      <h1 v-show="!isShow" key="1">你好啊！</h1>
      <h1 v-show="isShow" key="2">尚硅谷！</h1>
    </transition-group>
  </div>
</template>

<script>
  import "animate.css"
  
  export default {
    name: "Test",
    data() {return {isShow: true,}},
  };
</script>

<style scoped>
  h1 {background-color: orange;}
</style>
```



**使用动画优化 Todo-List**

```
src/components/MyList.vue
<template>
  <ul class="todo-main">
    <transition-group name="todo" appear>
      <MyItem v-for="todoObj of todoList" :key="todoObj.id" :todoObj="todoObj"/>
    </transition-group>
  </ul>
</template>

<script>
  import MyItem from "./MyItem.vue";

  export default {
    name: "MyList",
    components: { MyItem },
    props: ["todoList"],
  };
</script>

<style scoped>
  /*main*/
  .todo-main {margin-left: 0px;border: 1px solid #ddd;border-radius: 2px;padding: 0px;}
  .todo-empty {height: 40px;line-height: 40px;border: 1px solid #ddd;border-radius: 2px;
    padding-left: 5px;margin-top: 10px;}

  .todo-enter-active {
    animation: atguigu 0.5s linear;
  }

  .todo-leave-active {
    animation: atguigu 0.5s linear reverse;
  }

  @keyframes atguigu {
    from {
      transform: translateX(100%);
    }
    to {
      transform: translateX(0px);
    }
  }
</style>
```

# Vue中的Ajax 配置代理 slot插槽

### 4.1. Vue脚手架配置代理

本案例需要下载`axios`库 **npm install axios** 

**配置参考文档 Vue-Cli devServer.proxy**

 **vue.config.js**  是一个可选的配置文件，如果项目的 (和 `package.json` 同级的) 根目录中存在这个文件，那么它会被 `@vue/cli-service` 自动加载。你也可以使用 `package.json` 中的 `vue` 字段，但是注意这种写法需要你严格遵照 JSON 的格式来写

#### 方法一

​	在`vue.config.js`中添加如下配置

```javascript
module.exports = {
  devServer:{
    proxy:"http://localhost:5000"
  }
}
```

说明

1. 优点：配置简单，请求资源时直接发给前端（8080）即可
2. 缺点：不能配置多个代理，不能灵活的控制请求是否走代理

1. 工作方式：若按照上述配置代理，当请求了前端不存在的资源时，才会将请求会转发给服务器 （优先匹配前端资源）

#### 方法二

​	编写`vue.config.js`配置具体代理规则

```javascript
module.exports = {
	devServer: {
      proxy: {
      '/api1': {													// 匹配所有以 '/api1'开头的请求路径
        target: 'http://localhost:5000',	// 代理目标的基础路径
        pathRewrite: {'^/api1':''},				// 代理往后端服务器的请求去掉 /api1 前缀
        ws: true,													// WebSocket
        changeOrigin: true,
        
      },
      '/api2': {
        target: 'http://localhost:5001',
        pathRewrite: {'^/api2': ''},
        changeOrigin: true
      }
    }
  }
}
/*
   changeOrigin设置为true时，服务器收到的请求头中的host为：localhost:5000
   changeOrigin设置为false时，服务器收到的请求头中的host为：localhost:8080
   changeOrigin默认值为true
*/
```

说明

1. 优点：可以配置多个代理，且可以灵活的控制请求是否走代理
2. 缺点：配置略微繁琐，请求资源时必须加前缀



```
vue.config.js
module.exports = {
    pages: {
        index: {
            entry: 'src/main.js',
        },
    },
    lintOnSave:false,
    // 开启代理服务器（方式一）
    // devServer: {
    //     proxy:'http://localhost:5000'
    // }

    //开启代理服务器（方式二）
	devServer: {
        proxy: {
            '/api1': {
                target: 'http://localhost:5000',
                pathRewrite:{'^/api1':''},
                // ws: true, //用于支持websocket,默认值为true
                // changeOrigin: true //用于控制请求头中的host值,默认值为true
            },
            '/api2': {
                target: 'http://localhost:5001',
                pathRewrite:{'^/api2':''},
            }
        }
    }
}
src/App.vue
<template>
	<div>
		<button @click="getStudents">获取学生信息</button>
		<button @click="getCars">获取汽车信息</button>
	</div>
</template>

<script>
	import axios from 'axios'
	export default {
		name:'App',
		methods: {
			getStudents() {
				axios.get('http://localhost:8080/students').then(
					response => {
						console.log('请求成功了',response.data)
					},
					error => {
						console.log('请求失败了',error.message)
					}
				)
			},
			getCars() {
				axios.get('http://localhost:8080/demo/cars').then(
					response => {
						console.log('请求成功了',response.data)
					},
					error => {
						console.log('请求失败了',error.message)
					}
				)
			}
		},
	}
</script>
```

![img](https://cdn.nlark.com/yuque/0/2022/png/1379492/1643811082232-aa7cfeb2-829f-4319-95c3-63c27e7747a9.png)

### 4.2. GitHub用户搜索案例

```
public/index.html
<!DOCTYPE html>
<html lang="">
    <head>
        <meta charset="UTF-8">
        <!-- 针对IE浏览器的特殊配置，含义是让IE浏览器以最高渲染级别渲染页面 -->
        <meta http-equiv="X-UA-Compatible" content="IE=edge">
        <!-- 开启移动端的理想端口 -->
        <meta name="viewport" content="width=device-width, initial-scale=1.0">
        <!-- 配置页签图标 -->
        <link rel="icon" href="<%= BASE_URL %>favicon.ico">
      
        <!-- 引入bootstrap样式 -->
        <link rel="stylesheet" href="<%= BASE_URL %>css/bootstrap.css">
      
        <!-- 配置网页标题 -->
        <title><%= htmlWebpackPlugin.options.title %></title>
    </head>
    <body>
        <!-- 容器 -->
        <div id="app"></div>
    </body>
</html>
src/main.js
import Vue from 'vue'
import App from './App.vue'

Vue.config.productionTip = false

new Vue({
    el:"#app",
    render: h => h(App),
    beforeCreate(){
        Vue.prototype.$bus = this
    }
})
src/App.vue
<template>
  <div class="container">
    <Search/>
    <List/>
  </div>
</template>

<script>
  import Search from './components/Search.vue'
  import List from './components/List.vue'

  export default {
    name:'App',
    components:{ Search, List },
  }
</script>
src/components/Search.vue
<template>
  <section class="jumbotron">
    <h3 class="jumbotron-heading">Search Github Users</h3>
    <div>
      <input type="text" placeholder="enter the name you search" v-model="keyWord"/>&nbsp;
      <button @click="searchUsers">Search</button>
    </div>
  </section>
</template>

<script>
import axios from "axios";
export default {
  name: "Search",
  data() {
    return {
      keyWord: "",
    };
  },
  methods: {
    searchUsers() {
      //请求前更新List的数据
      this.$bus.$emit("updateListData", {
        isLoading: true,
        errMsg: "",
        users: [],
        isFirst: false,
      });
      axios.get(`https://api.github.com/search/users?q=${this.keyWord}`).then(
        (response) => {
          console.log("请求成功了");
          this.$bus.$emit("updateListData", {	//请求成功后更新List的数据
            isLoading: false,
            errMsg: "",
            users: response.data.items,
          });
        },
        (error) => {
          this.$bus.$emit("updateListData", {	//请求后更新List的数据
            isLoading: false,
            errMsg: error.message,
            users: [],
          });
        }
      );
    },
  },
};
</script>
src/components/List.vue
<template>
  <div class="row">
    <!-- 展示用户列表 -->
    <div v-show="info.users.length" class="card" 
         v-for="user in info.users" :key="user.login">
      <a :href="user.html_url" target="_blank">
        <img :src="user.avatar_url" style="width: 100px" />
      </a>
      <p class="card-text">{{ user.login }}</p>
    </div>
    <!-- 展示欢迎词 -->
    <h1 v-show="info.isFirst">欢迎使用！</h1>
    <!-- 展示加载中 -->
    <h1 v-show="info.isLoading">加载中....</h1>
    <!-- 展示错误信息 -->
    <h1 v-show="info.errMsg">{{ info.errMsg }}</h1>
  </div>
</template>

<script>
export default {
  name: "List",
  data() {
    return {
      info: {
        isFirst: true,
        isLoading: false,
        errMsg: "",
        users: [],
      },
    };
  },
  mounted() {
    this.$bus.$on("updateListData", (dataObj) => {
      this.info = { ...this.info, ...dataObj };
    });
  },
};
</script>

<style scoped>
.album {min-height: 50rem; /* Can be removed; just added for demo purposes */
  padding-top: 3rem;padding-bottom: 3rem;background-color: #f7f7f7;}
.card {float: left;width: 33.333%;padding: 0.75rem;margin-bottom: 2rem;
  border: 1px solid #efefef;text-align: center;}
.card > img {margin-bottom: 0.75rem;border-radius: 100px;}
.card-text {font-size: 85%;}
</style>
```

![img](https://cdn.nlark.com/yuque/0/2022/png/1379492/1643034535089-857fa5f5-ab1c-41bd-b696-37c4ef970287.png)

### 4.3. vue-resource

`vue`项目常用的两个`Ajax`库

1. `axios`：通用的Ajax请求库，官方推荐，效率高
2. `vue-resource`：vue插件库，vue 1.x使用广泛，官方已不维护

下载 **vue-resource** 库 **npm i vue-resource** 



```
src/main.js
import Vue from 'vue'
import App from './App.vue'
import vueResource from 'vue-resource'

Vue.config.productionTip = false

Vue.use(vueResource)

new Vue({
    el:"#app",
    render: h => h(App),
    beforeCreate(){
        Vue.prototype.$bus = this
    }
})
src/App.vue
<template>
	<div class="container">
		<Search/>
		<List/>
	</div>
</template>

<script>
	import Search from './components/Search.vue'
	import List from './components/List.vue'

    export default {
        name:'App',
		components:{ Search, List },
	}
</script>
src/components/Search.vue
<template>
    <section class="jumbotron">
		<h3 class="jumbotron-heading">Search Github Users</h3>
		<div>
      <input type="text" placeholder="enter the name you search" v-model="keyWord"/>&nbsp;
      <button @click="getUsers">Search</button>
		</div>
    </section>
</template>

<script>
  export default {
    name:'Search',
    data() {
      return {
        keyWord:''
      }
    },
    methods: {
      getUsers(){
        //请求前更新List的数据
        this.$bus.$emit('updateListData',
                        {isLoading:true,errMsg:'',users:[],isFirst:false})
        this.$http.get(`https://api.github.com/search/users?q=${this.keyWord}`).then(
          response => {
            console.log('请求成功了')
            //请求成功后更新List的数据
            this.$bus.$emit('updateListData',
                            {isLoading:false,errMsg:'',users:response.data.items})
          },
          error => {
            //请求后更新List的数据
            this.$bus.$emit('updateListData',
                            {isLoading:false,errMsg:error.message,users:[]})
          }
        )
      }
    }
  }
</script>
src/components/List.vue
<template>
    <div class="row">
        <!-- 展示用户列表 -->
        <div class="card" v-show="info.users.length" v-for="user in info.users" :key="user.id">
            <a :href="user.html_url" target="_blank">
                <img :src="user.avatar_url" style='width: 100px'/>
            </a>
            <h4 class="card-title">{{user.login}}</h4>
        </div>
        <!-- 展示欢迎词 -->
        <h1 v-show="info.isFirst">欢迎使用！</h1>
        <!-- 展示加载中 -->
        <h1 v-show="info.isLoading">加载中...</h1>
        <!-- 展示错误信息 -->
        <h1 v-show="info.errMsg">{{errMsg}}</h1>
    </div>
</template>

<script>
    export default {
        name:'List',
        data() {
            return {
                info:{
                    isFirst:true,
                    isLoading:false,
                    errMsg:'',
                    users:[]
                }
            }
        },
        mounted(){
            this.$bus.$on('updateListData',(dataObj)=>{
                this.info = {...this.info,...dataObj}
            })
        },
        beforeDestroy(){
            this.$bus.$off('updateListData')
        }
    }
</script>
```

### 4.4. slot 插槽

  **<slot>** **插槽：**让父组件可以向子组件指定位置插入`html`结构，也是一种组件间通信的方式，

​      适用于 **父组件 ===> 子组件**

1. 分类：默认插槽、具名插槽、作用域插槽 
2. 使用方式

1. 1. 默认插槽

```vue
父组件中：
        <Category>
           <div>html结构1</div>
        </Category>
子组件中：Category
        <template>
            <div>
               <!-- 定义插槽 -->
               <slot>插槽默认内容...</slot>
            </div>
        </template>
```

1. 1. 具名插槽

父组件指明放入子组件的哪个插槽 **slot="****footer****"** ，如果是`template`可以写成 **v-slot:footer** 

```vue
父组件中：
        <Category>
            <template slot="center">
              <div>html结构1</div>
            </template>

            <template v-slot:footer>
               <div>html结构2</div>
            </template>
        </Category>
子组件中：
        <template>
            <div>
               <!-- 定义插槽 -->
               <slot name="center">插槽默认内容...</slot>
               <slot name="footer">插槽默认内容...</slot>
            </div>
        </template>
```

1. 1. 作用域插槽

 **scope** 用于父组件往子组件插槽放的`html`结构接收子组件的数据

理解：数据在组件的自身，但根据数据生成的结构需要组件的使用者来决定

（`games`数据在`Category`组件中，但使用数据所遍历出来的结构由`App`组件决定） 

```vue
父组件中：
        <Category>
            <template scope="scopeData">
                <!-- 生成的是ul列表 -->
                <ul>
                  <li v-for="g in scopeData.games" :key="g">{{g}}</li>
                </ul>
            </template>
        </Category>

        <Category>
            <template slot-scope="scopeData">
                <!-- 生成的是h4标题 -->
                <h4 v-for="g in scopeData.games" :key="g">{{g}}</h4>
            </template>
        </Category>
子组件中：
        <template>
            <div>
                <slot :games="games"></slot>
            </div>
        </template>
		
        <script>
            export default {
                name:'Category',
                props:['title'],
                //数据在子组件自身
                data() {
                    return {
                        games:['红色警戒','穿越火线','劲舞团','超级玛丽']
                    }
                },
            }
        </script>
```

**注意**：关于**样式**，既可以写在父组件中，解析后放入子组件插槽；也可以放在子组件中，传给子组件再解析

#### 4.4.1. 默认插槽

```
src/App.vue
<template>
	<div class="container">
		<Category title="美食" >
			<img src="https://s3.ax1x.com/2021/01/16/srJlq0.jpg" alt="">
		</Category>

		<Category title="游戏" >
			<ul>
				<li v-for="(g,index) in games" :key="index">{{g}}</li>
			</ul>
		</Category>

		<Category title="电影">
			<video controls src="http://clips.vorwaerts-gmbh.de/big_buck_bunny.mp4"></video>
		</Category>
	</div>
</template>

<script>
	import Category from './components/Category'
	export default {
		name:'App',
		components:{ Category },
		data() {
			return {
				foods:['火锅','烧烤','小龙虾','牛排'],
				games:['红色警戒','穿越火线','劲舞团','超级玛丽'],
				films:['《教父》','《拆弹专家》','《你好，李焕英》','《尚硅谷》']
			}
		},
	}
</script>

<style scoped>.container{display: flex;justify-content: space-around;}</style>
src/components/Category.vue
<template>
	<div class="category">
		<h3>{{ title }}分类</h3>
		<!-- 定义一个插槽（挖个坑，等着组件的使用者进行填充） -->
		<slot>我是一些默认值，当使用者没有传递具体结构时，我会出现</slot>
	</div>
</template>

<script>
	export default {
		name:'Category',
		props:['title']
	}
</script>

<style scoped>
	.category {background-color: skyblue;width: 200px;height: 300px;}
	h3 {text-align: center;background-color: orange;}
	video {width: 100%;}
	img {width: 100%;}
</style>
```

![img](https://cdn.nlark.com/yuque/0/2022/png/1379492/1643034535338-68fd72c0-7463-4f5a-a1f7-cdffb884c99e.png)

#### 4.4.2. 具名插槽

```
src/App.vue
<template>
	<div class="container">
		<Category title="美食" >
			<img slot="conter" src="https://s3.ax1x.com/2021/01/16/srJlq0.jpg" alt="">
			<a slot="footer" href="http://www.atguigu.com">更多美食</a>
		</Category>

		<Category title="游戏" >
			<ul slot="center">
				<li v-for="(g,index) in games" :key="index">{{g}}</li>
			</ul>
			<div class="foot" slot="footer">
				<a href="http://www.atguigu.com">单机游戏</a>
				<a href="http://www.atguigu.com">网络游戏</a>
			</div>
		</Category>

		<Category title="电影">
			<video slot="center" controls src="http://clips.vorwaerts-gmbh.de/big_buck_bunny.mp4"></video>
			<template v-slot:footer>
				<div class="foot">
					<a href="http://www.atguigu.com">经典</a>
					<a href="http://www.atguigu.com">热门</a>
					<a href="http://www.atguigu.com">推荐</a>
				</div>
				<h4>欢迎前来观影</h4>
			</template>
		</Category>
	</div>
</template>

<script>
	import Category from './components/Category'
	export default {
		name:'App',
		components:{Category},
		data() {
			return {
				foods:['火锅','烧烤','小龙虾','牛排'],
				games:['红色警戒','穿越火线','劲舞团','超级玛丽'],
				films:['《教父》','《拆弹专家》','《你好，李焕英》','《尚硅谷》']
			}
		},
	}
</script>

<style scoped>
	.container,.foot{display: flex;justify-content: space-around;}
	h4{text-align: center;}
</style>
src/components/Category.vue
<template>
	<div class="category">
		<h3>{{title}}分类</h3>
		<!-- 定义一个插槽（挖个坑，等着组件的使用者进行填充） -->
		<slot name="center">我是一些默认值，当使用者没有传递具体结构时，我会出现1</slot>
		<slot name="footer">我是一些默认值，当使用者没有传递具体结构时，我会出现2</slot>
	</div>
</template>

<script>
	export default {
		name:'Category',
		props:['title']
	}
</script>

<style scoped>
	.category{background-color: skyblue;width: 200px;height: 300px;}
	h3{text-align: center;background-color: orange;}
	video{width: 100%;}
	img{width: 100%;}
</style>
```

![img](https://cdn.nlark.com/yuque/0/2022/png/1379492/1643034536461-feaa7049-a15e-44ab-8995-cc0ec50a89cf.png)

#### 4.4.3. 作用域插槽

```
src/App.vue
<template>
	<div class="container">

		<Category title="游戏">
			<template scope="atguigu">
				<ul>
					<li v-for="(g,index) in atguigu.games" :key="index">{{g}}</li>
				</ul>
			</template>
		</Category>

		<Category title="游戏">
			<template scope="{games}">
				<ol>
					<li style="color:red" v-for="(g,index) in games" :key="index">{{g}}</li>
				</ol>
			</template>
		</Category>

		<Category title="游戏">
			<template slot-scope="{games}">
				<h4 v-for="(g,index) in games" :key="index">{{g}}</h4>
			</template>
		</Category>
	</div>
</template>

<script>
	import Category from './components/Category'
	export default {
		name:'App',
		components:{ Category },
	}
</script>

<style scoped>
	.container,.foot{display: flex;justify-content: space-around;}
	h4{text-align: center;}
</style>
src/components/Category.vue
<template>
	<div class="category">
		<h3>{{title}}分类</h3>
		<slot :games="games" msg="hello">我是默认的一些内容</slot>
	</div>
</template>

<script>
	export default {
		name:'Category',
		props:['title'],
		data() {
			return {
				games:['红色警戒','穿越火线','劲舞团','超级玛丽'],
			}
		},
	}
</script>

<style scoped>
	.category{background-color: skyblue;width: 200px;height: 300px;}
	h3{text-align: center;background-color: orange;}
	video{width: 100%;}
  img{width: 100%;}
</style>
```

![img](https://cdn.nlark.com/yuque/0/2022/png/1379492/1643968984388-adfffed8-79aa-4ef1-80a4-acbfd01b9e05.png)

# Vuex

### 5.1. 理解 Vuex

#### 5.1.1. Vuex 是什么

1. 概念：专门在`Vue`中实现集中式状态（数据）管理的一个`Vue`插件，对`Vue`应用中多个组件的共享状态进行集中式的管理（读/写），也是一种组件间通信的方式，且适用于任意组件间通信
2. [**Vuex Github地址**](https://github.com/vuejs/vuex)

![img](https://cdn.nlark.com/yuque/0/2022/png/1379492/1643034632699-15503880-2c10-44e1-bf8f-c088d0896ba6.png)
![img](https://cdn.nlark.com/yuque/0/2022/png/1379492/1643034632949-1f50dc65-b44d-4b00-bed1-10222a2e87e5.png)

#### 5.1.2. 什么时候使用 Vuex

1. 多个组件依赖于同一状态
2. 来自不同组件的行为需要变更同一状态

#### 5.1.3. Vuex 工作原理图

![img](https://cdn.nlark.com/yuque/0/2022/png/1379492/1643034632508-417c8676-569a-41e1-b7db-223fafbedfd7.png)

### 5.2. 求和案例

#### 5.2.1. 使用纯 vue 编写

![img](https://cdn.nlark.com/yuque/0/2022/png/1379492/1643983901187-53fc6663-8195-463f-99b0-69c406fd5a66.png)

```
src/App.vue
<template>
  <div>
    <Count/>
  </div>
</template>

<script>
import Count from "./components/Count.vue";

export default {
  name: "App",
  components: { Count },
};
</script>
src/components/Count.vue
<template>
  <div>
    <h2>当前求和为：{{ sum }}</h2>
    <select v-model.number="n">
      <option value="1">1</option>
      <option value="2">2</option>
      <option value="3">3</option>
    </select>
    <button @click="increment">+</button>
    <button @click="decrement">-</button>
    <button @click="incrementOdd">当前求和为奇数再加</button>
    <button @click="incrementWait">等一等再加</button>
  </div>
</template>

<script>
  export default {
    name: "Count",
    data() {
      return {
        sum: 0, // 当前的和
        n: 1, // 用户选择的数字
      };
    },
    methods: {
      increment() {
        this.sum += this.n;
      },
      decrement() {
        this.sum -= this.n;
      },
      incrementOdd() {
        if (this.sum % 2) {
          this.sum += this.n;
        }
      },
      incrementWait() {
        setTimeout(() => {
          this.sum += this.n;
        }, 500);
      },
    },
  };
</script>

<style>
  button {margin-left: 5px;}
</style>
```

#### 5.2.2. 搭建 Vuex 环境

1. 下载安装`vuex` **npm i vuex** 
2. 创建`src/store/index.js`该文件用于创建`Vuex`中最为核心的`store`

```javascript
import Vue from 'vue'
import Vuex from 'vuex'	// 引入Vuex

Vue.use(Vuex)	// 应用Vuex插件

const actions = {}		// 准备actions——用于响应组件中的动作
const mutations = {}	// 准备mutations——用于操作数据（state）
const state = {}			// 准备state——用于存储数据

// 创建并暴露store
export default new Vuex.Store({
	actions,
	mutations,
	state,
})
```

1. 在`src/main.js`中创建`vm`时传入 **store** 配置项

```javascript
import Vue from 'vue'
import App from './App.vue'
import store from './store'	// 引入store

Vue.config.productionTip = false

new Vue({
	el: '#app',
	render: h => h(App),
	store,										// 配置项添加store
	beforeCreate() {
		Vue.prototype.$bus = this
	}
})
```

#### 5.2.3. 使用 Vuex 编写

Vuex的基本使用

1. 初始化数据 **state** ，配置 **actions** 、 **mutations** ，操作文件 **store.js** 
2. 组件中读取`vuex`中的数据 **$store.state.数据** 

1. 组件中修改`vuex`中的数据 **$store.dispatch('action中的方法名',数据)**  

或 **$store.commit('mutations中的方法名',数据)**   

若没有网络请求或其他业务逻辑，组件中也可越过 **actions** ，即不写 **dispatch** ，直接编写 **commit** 



`src/store/index.js`该文件用于创建Vuex中最为核心的store

```javascript
import Vue from 'vue'
import Vuex from 'vuex'	// 引入Vuex

Vue.use(Vuex)	// 应用Vuex插件

// 准备actions——用于响应组件中的动作
const actions = {
	/* jia(context,value){
		console.log('actions中的jia被调用了')
		context.commit('JIA',value)
	},
	jian(context,value){
		console.log('actions中的jian被调用了')
		context.commit('JIAN',value)
	}, */
	jiaOdd(context,value){	// context 相当于精简版的 $store
		console.log('actions中的jiaOdd被调用了')
		if(context.state.sum % 2){
			context.commit('JIA',value)
		}
	},
	jiaWait(context,value){
		console.log('actions中的jiaWait被调用了')
		setTimeout(()=>{
			context.commit('JIA',value)
		},500)
	}
}
// 准备mutations——用于操作数据（state）
const mutations = {
	JIA(state,value){
		console.log('mutations中的JIA被调用了')
		state.sum += value
	},
	JIAN(state,value){
		console.log('mutations中的JIAN被调用了')
		state.sum -= value
	}
}
// 准备state——用于存储数据
const state = {
	sum:0 //当前的和
}

// 创建并暴露store
export default new Vuex.Store({
	actions,
	mutations,
	state,
})
src/components/Count.vue
<template>
	<div>
		<h1>当前求和为：{{ $store.state.sum }}</h1>
		<select v-model.number="n">
			<option value="1">1</option>
			<option value="2">2</option>
			<option value="3">3</option>
		</select>
		<button @click="increment">+</button>
		<button @click="decrement">-</button>
		<button @click="incrementOdd">当前求和为奇数再加</button>
		<button @click="incrementWait">等一等再加</button>
	</div>
</template>

<script>
	export default {
		name:'Count',
		data() {
			return {
				n:1, //用户选择的数字
			}
		},
		methods: {
			increment(){
				this.$store.commit('JIA',this.n)
			},
			decrement(){
				this.$store.commit('JIAN',this.n)
			},
			incrementOdd(){
				this.$store.dispatch('jiaOdd',this.n)
			},
			incrementWait(){
				this.$store.dispatch('jiaWait',this.n)
			},
		}
	}
</script>

<style lang="css">button{margin-left: 5px;}</style>
```

### 5.3. getters 配置项

1. 概念：当`state`中的数据需要经过加工后再使用时，可以使用 **getters** 加工，相当于**全局计算属性**
2. 在`store.js`中追加 **getters** 配置

```javascript
......

const getters = {
	bigSum(state){
		return state.sum * 10
	}
}

// 创建并暴露store
export default new Vuex.Store({
	......
	getters
})
```

1. 组件中读取数据 **$store.getters.bigSum** 



![img](https://cdn.nlark.com/yuque/0/2022/png/1379492/1644051052492-7080e13e-ce76-45d2-9f05-9a5585018837.png)

```
src/store/index.js
import Vue from 'vue'	// 引入Vue核心库
import Vuex from 'vuex'	// 引入Vuex

Vue.use(Vuex)	// 应用Vuex插件
   
// 准备actions对象——响应组件中用户的动作
const actions = {
    addOdd(context,value){
        console.log("actions中的addOdd被调用了")
        if(context.state.sum % 2){context.commit('ADD',value)}
    },
    addWait(context,value){
        console.log("actions中的addWait被调用了")
        setTimeout(()=>{context.commit('ADD',value)},500)
    },
}
// 准备mutations对象——修改state中的数据
const mutations = {
    ADD(state,value){state.sum += value},
    SUB(state,value){state.sum -= value}
}
// 准备state对象——保存具体的数据
const state = {
    sum:0 // 当前的和
}
// 准备getters对象——用于将state中的数据进行加工
const getters = {
    bigSum(){
        return state.sum * 10
    }
}
   
//创建并暴露store
export default new Vuex.Store({
    actions,
    mutations,
    state,
    getters
})
src/Count.vue
<template>
	<div>
		<h1>当前求和为：{{ $store.state.sum }}</h1>
		<h3>当前求和的10倍为：{{ $store.getters.bigSum }}</h3>
		<select v-model.number="n">
			<option value="1">1</option>
			<option value="2">2</option>
			<option value="3">3</option>
		</select>
		<button @click="increment">+</button>
		<button @click="decrement">-</button>
		<button @click="incrementOdd">当前求和为奇数再加</button>
		<button @click="incrementWait">等一等再加</button>
	</div>
</template>

<script>
	export default {
		name:'Count',
		data() {
			return {
				n:1,
			}
		},
		methods: {
			increment(){this.$store.commit('ADD',this.n)},
			decrement(){this.$store.commit('SUBTRACT',this.n)},
			incrementOdd(){this.$store.dispatch('addOdd',this.n)},
			incrementWait(){this.$store.dispatch('addWait',this.n)},
		},
	}
</script>

<style>button{margin-left: 5px;}</style>
```

### 5.4. 四个 map 方法的使用

1. **mapState方法：**用于帮助映射`state`中的数据为**计算属性**

```javascript
computed: {
  	// 借助mapState生成计算属性：sum、school、subject（对象写法一）
  	...mapState({sum:'sum',school:'school',subject:'subject'}),

  	// 借助mapState生成计算属性：sum、school、subject（数组写法二）
  	...mapState(['sum','school','subject']),
},
```

1. **mapGetters方法：**用于帮助映射`getters`中的数据为**计算属性**  

```javascript
computed: {
    //借助mapGetters生成计算属性：bigSum（对象写法一）
    ...mapGetters({bigSum:'bigSum'}),

    //借助mapGetters生成计算属性：bigSum（数组写法二）
    ...mapGetters(['bigSum'])
},
```

1. **mapActions方法：**用于帮助生成与`actions`对话的方法，即包含`$store.dispatch(xxx)`的函数  

```javascript
methods:{
    //靠mapActions生成：incrementOdd、incrementWait（对象形式）
    ...mapActions({incrementOdd:'jiaOdd',incrementWait:'jiaWait'})

    //靠mapActions生成：incrementOdd、incrementWait（数组形式）
    ...mapActions(['jiaOdd','jiaWait'])
}
```

1. **mapMutations方法：**用于帮助生成与`mutations`对话的方法，即包含`$store.commit(xxx)`的函数  

```javascript
methods:{
    //靠mapActions生成：increment、decrement（对象形式）
    ...mapMutations({increment:'JIA',decrement:'JIAN'}),
    
    //靠mapMutations生成：JIA、JIAN（对象形式）
    ...mapMutations(['JIA','JIAN']),
}
```

**注意**：`mapActions`与`mapMutations`使用时，若需要传递参数需要：**在模板中绑定事件时传递好参数**，否则参数是事件对象



```
src/components/Count.vue
<template>
	<div>
		<h1>当前求和为：{{ sum }}</h1>
		<h3>当前求和的10倍为：{{ bigSum }}</h3>
		<h3>我是{{ name }}，我在{{ school }}学习</h3>
		<select v-model.number="n">
			<option value="1">1</option>
			<option value="2">2</option>
			<option value="3">3</option>
		</select>
		<button @click="increment(n)">+</button>
		<button @click="decrement(n)">-</button>
		<button @click="addOdd(n)">当前求和为奇数再加</button>
		<button @click="addWait(n)">等一等再加</button>
	</div>
</template>

<script>
	import {mapState, mapGetters, mapMutations, mapActions} from 'vuex'	//🔴

	export default {
		name: 'Count',
		data() {
			return {
				n:1, //用户选择的数字
			}
		},
  computed: {		
			...mapState(['sum','school','name']),
			...mapGetters(['bigSum'])
		},
		methods: {
			...mapMutations({increment:'ADD', decrement:'SUBTRACT'}),
			...mapActions(['addOdd', 'addWait'])
		},
	}
</script>

<style>
	button{
		margin-left: 5px;
	}
</style>
```

### 5.5. 多组件共享数据案例

![img](https://cdn.nlark.com/yuque/0/2022/png/1379492/1644055080105-d6e7d6e7-3967-433d-bb8c-b7bdbf92347b.png)

```
src/App.vue
<template>
  <div>
    <Count/><hr/>
    <Person/>
  </div>
</template>

<script>
import Count from "./components/Count.vue";
import Person from "./components/Person.vue";

export default {
  name: "App",
  components: { Count, Person },
};
</script>
```

`src/store/index.js`该文件用于创建Vuex中最为核心的store

```javascript
import Vue from 'vue'
import Vuex from 'vuex'

Vue.use(Vuex)

const actions = {
	jiaOdd(context,value){
		console.log('actions中的jiaOdd被调用了')
		if(context.state.sum % 2){
			context.commit('JIA',value)
		}
	},
	jiaWait(context,value){
		console.log('actions中的jiaWait被调用了')
		setTimeout(()=>{
			context.commit('JIA',value)
		},500)
	}
}

//准备mutations——用于操作数据（state）
const mutations = {
	JIA(state,value){
		console.log('mutations中的JIA被调用了')
		state.sum += value
	},
	JIAN(state,value){
		console.log('mutations中的JIAN被调用了')
		state.sum -= value
	},
	ADD_PERSON(state,value){
		console.log('mutations中的ADD_PERSON被调用了')
		state.personList.unshift(value)
	}
}

//准备state——用于存储数据
const state = {
	sum: 0,
	school: '尚硅谷',
	subject: '前端',
	personList: []
}

//准备getters——用于将state中的数据进行加工
const getters = {
	bigSum(state){
		return state.sum*10
	}
}

//创建并暴露store
export default new Vuex.Store({
	actions,
	mutations,
	state,
	getters
})
src/components/Count.vue
<template>
	<div>
		<h1>当前求和为：{{ sum }}</h1>
		<h3>当前求和放大10倍为：{{ bigSum }}</h3>
		<h3>我在{{ school }}，学习{{ subject }}</h3>
		<h3 style="color:red">Person组件的总人数是：{{ personList.length }}</h3>
		<select v-model.number="n">
			<option value="1">1</option>
			<option value="2">2</option>
			<option value="3">3</option>
		</select>
		<button @click="increment(n)">+</button>
		<button @click="decrement(n)">-</button>
		<button @click="incrementOdd(n)">当前求和为奇数再加</button>
		<button @click="incrementWait(n)">等一等再加</button>
	</div>
</template>

<script>
	import {mapState,mapGetters,mapMutations,mapActions} from 'vuex'
	export default {
		name:'Count',
		data() {
			return {
				n:1, //用户选择的数字
			}
		},
		computed:{
			...mapState(['sum','school','subject','personList']),
			...mapGetters(['bigSum'])
		},
		methods: {
			...mapMutations({increment:'JIA',decrement:'JIAN'}),
			...mapActions({incrementOdd:'jiaOdd',incrementWait:'jiaWait'})
		}
	}
</script>

<style lang="css">button{margin-left: 5px;}</style>
src/components/Person.vue
<template>
	<div>
		<h1>人员列表</h1>
		<h3 style="color:red">Count组件求和为：{{ sum }}</h3>
		<input type="text" placeholder="请输入名字" v-model="name">
		<button @click="add">添加</button>
		<ul>
			<li v-for="p in personList" :key="p.id">{{ p.name }}</li>
		</ul>
	</div>
</template>

<script>
	import {nanoid} from 'nanoid'
  import { mapState } from "vuex"
  
	export default {
		name:'Person',
		data() {
			return {
				name:''
			}
		},
		computed:{
			personList(){return this.$store.state.personList},
			sum(){return this.$store.state.sum}
		},
		methods: {
			add(){
        if (this.name === "") return
				const personObj = {id:nanoid(),name:this.name}
				this.$store.commit('ADD_PERSON',personObj)
				this.name = ''
			}
		},
	}
</script>
```

### 5.6. 模块化+命名空间

1. 目的：让代码更好维护，让多种数据分类更加明确
2. 修改`store.js`

为了解决不同模块命名冲突的问题，将不同模块的 **namespaced: true** ，之后在不同页面中引入`getter``actions``mutations`时，需要加上所属的模块名

```javascript
const countAbout = {
  namespaced: true,	// 开启命名空间
  state: {x:1},
  mutations: { ... },
  actions: { ... },
  getters: {
    bigSum(state){ return state.sum * 10 }
  }
}

const personAbout = {
  namespaced: true,	// 开启命名空间
  state: { ... },
  mutations: { ... },
  actions: { ... }
}

const store = new Vuex.Store({
  modules: {
    countAbout,
    personAbout
  }
})
```

1.  开启命名空间后，组件中读取`state`数据 

```javascript
// 方式一：自己直接读取
this.$store.state.personAbout.list
// 方式二：借助mapState读取：
...mapState('countAbout',['sum','school','subject']),
```

1.  开启命名空间后，组件中读取`getters`数据

```javascript
//方式一：自己直接读取
this.$store.getters['personAbout/firstPersonName']
//方式二：借助mapGetters读取：
...mapGetters('countAbout',['bigSum'])
```

1.  开启命名空间后，组件中调用`dispatch`

```javascript
//方式一：自己直接dispatch
this.$store.dispatch('personAbout/addPersonWang',person)
//方式二：借助mapActions：
...mapActions('countAbout',{incrementOdd:'jiaOdd',incrementWait:'jiaWait'})
```

1.  开启命名空间后，组件中调用`commit`

```javascript
//方式一：自己直接commit
this.$store.commit('personAbout/ADD_PERSON',person)
//方式二：借助mapMutations：
...mapMutations('countAbout',{increment:'JIA',decrement:'JIAN'}),
```



![img](https://cdn.nlark.com/yuque/0/2022/png/1379492/1643034636483-b8708836-b803-4254-8ca0-5cbee6b77d5e.png)

```
src/store/index.js
import Vue from 'vue'
import Vuex from 'vuex'
import countOptions from './count'		// 引入count
import personOptions from './person'	// 引入person

Vue.use(Vuex)
   
//创建并暴露store
export default new Vuex.Store({
    modules:{
        countAbout:countOptions,
        personAbout:personOptions,
    }
})
src/store/count.js
export default {
    namespaced:true,
    actions: {
        addOdd(context,value){
            console.log("actions中的addOdd被调用了")
            if(context.state.sum % 2){
                context.commit('ADD',value)
            }
        },
        addWait(context,value){
            console.log("actions中的addWait被调用了")
            setTimeout(()=>{
                context.commit('ADD',value)
            },500)
        }
    },
    mutations: {
        ADD(state,value){ state.sum += value },
        SUBTRACT(state,value){ state.sum -= value }
    },
    state: {
        sum:0,
        school:'尚硅谷',
      	subject: '前端'
    },
    getters: {
        bigSum(state){ return state.sum * 10 }
    }
}
src/store/person.js
import axios from "axios"
import { nanoid } from "nanoid"

export default{
    namespaced:true,
    actions:{
        addPersonWang(context,value){
            if(value.name.indexOf('王') === 0){
                context.commit('ADD_PERSON',value)
            }else{
                alert('添加的人必须姓王！')
            }
        },
        addPersonServer(context){
            axios.get('http://api.uixsj.cn/hitokoto/get?type=social').then(
                response => {
                    context.commit('ADD_PERSON',{id:nanoid(),name:response.data})
                },
                error => { alert(error.message) }
            )
        }
    },
    mutations:{
        ADD_PERSON(state,value){
            console.log('mutations中的ADD_PERSON被调用了')
            state.personList.unshift(value)
        }
    },
    state:{
        personList:[]
    },
    getters:{
        firstPersonName(state){ return state.personList[0].name }
    }
}
src/components/Count.vue
<template>
	<div>
		<h1>当前求和为：{{ sum }}</h1>
		<h3>当前求和的10倍为：{{ bigSum }}</h3>
		<h3>我是{{ name }}，我在{{ school }}学习</h3>
		<h3 style="color:red">Person组件的总人数是：{{ personList.length }}</h3>
		<select v-model.number="n">
			<option value="1">1</option>
			<option value="2">2</option>
			<option value="3">3</option>
		</select>
		<button @click="increment(n)">+</button>
		<button @click="decrement(n)">-</button>
		<button @click="incrementOdd(n)">当前求和为奇数再加</button>
		<button @click="incrementWait(n)">等一等再加</button>
	</div>
</template>

<script>
	import {mapState,mapGetters,mapMutations,mapActions} from 'vuex'

	export default {
		name:'Count',
		data() {
			return {
				n:1, // 用户选择的数字
			}
		},
    computed:{
			...mapState('countAbout',['sum','school','name']),
      ...mapState('personAbout',['personList']),
			...mapGetters('countAbout',['bigSum']),
		}
		methods: {
			...mapMutations('countAbout',{increment:'ADD',decrement:'SUBTRACT'}),
			...mapActions('countAbout',{incrementOdd:'addOdd',incrementWait:'addWait'})
		},
	}
</script>

<style>button{margin-left: 5px;}</style>
src/components/Person.vue
<template>
	<div>
		<h1>人员列表</h1>
		<h3 style="color:red">Count组件求和为：{{ sum }}</h3>
        <h3>列表中第一个人的名字是：{{ firstPersonName }}</h3>
		<input type="text" placeholder="请输入名字" v-model="name">
		<button @click="add">添加</button>
        <button @click="addWang">添加一个姓王的人</button>
        <button @click="addPerson">随机添加一个人</button>
		<ul>
			<li v-for="p in personList" :key="p.id">{{ p.name }}</li>
		</ul>
	</div>
</template>

<script>
	import {nanoid} from 'nanoid'
	export default {
		name: 'Person',
		data() {
			return {
				name:''
			}
		},
		computed: {
			personList(){
				return this.$store.state.personAbout.personList
			},
			sum(){
				return this.$store.state.countAbout.sum
			},
      firstPersonName(){
        return this.$store.getters['personAbout/firstPersonName']
      }
		},
		methods: {
			add(){
				const personObj = {id:nanoid(),name:this.name}
				this.$store.commit('personAbout/ADD_PERSON',personObj)
				this.name = ''
			},
      addWang(){
        const personObj = {id:nanoid(),name:this.name}
        this.$store.dispatch('personAbout/addPersonWang',personObj)
        this.name = ''   
      },
      addPerson(){
        this.$store.dispatch('personAbout/addPersonServer')
      }
		},
	}
</script>
```





# Vue Router 相关理解 基本路由 多级路由

### 6.1 相关理解

#### 6.1.1 vue-router 的理解

- vue的一个插件库，专门用来实现SPA应用

#### 6.1.2 对SPA应用的理解

1. 单页Web应用（single page web application，**SPA**）
2. 整个应用只有一个完整的页面

1. 点击页面中的导航链接不会刷新页面，只会做页面的局部更新
2. 数据需要通过**ajax**请求获取

![img](https://cdn.nlark.com/yuque/0/2022/png/1379492/1644066696036-671cb003-dfdb-4402-8114-c151d60e27e0.png)

#### 6.1.3 路由的理解

1. 什么是路由? 

1. 1. 一个路由就是一组映射关系（key - value）
   2. `key`为**路径**，`value`可能是 **function** 或 **componen** 

1. 路由分类

1. 1.  后端路由

1. 1. 1. 理解：`value`是`function`，用于处理客户端提交的请求
      2. 工作过程：服务器接收到一个请求时，根据请求路径找到匹配的函数来处理请求，返回响应数据

1. 1.  前端路由

1. 1. 1. 理解：`value`是`component`，用于展示页面内容
      2. 工作过程：当浏览器的路径改变时，对应的组件就会显示

### 6.2 基本路由

1. 安装 **vue-router** ，命令 **npm i vue-router** 
2. 应用插件 **Vue.use(VueRouter)** 

1. 编写`router`配置项

```javascript
import VueRouter from 'vue-router'			// 引入VueRouter
import About from '../components/About'	// 路由组件
import Home from '../components/Home'		// 路由组件

// 创建router实例对象，去管理一组一组的路由规则
const router = new VueRouter({
	routes:[
		{
			path:'/about',
			component:About
		},
		{
			path:'/home',
			component:Home
		}
	]
})

//暴露router
export default router
```

1. 实现切换

<router-link></router-link>浏览器会被替换为a标签

**active-class**可配置高亮样式

```vue
<router-link active-class="active" to="/about">About</router-link>
```

1. 指定展示位 **<router-view></router-view>** 



![img](https://cdn.nlark.com/yuque/0/2022/png/1379492/1644071105496-fa99cb9a-ee5f-4041-995a-4c42e3067a22.png)

`src/router/index.js`该文件专门用于创建整个应用的路由器

```javascript
import VueRouter from 'vue-router'
// 引入组件
import About from '../components/About'
import Home from '../components/Home'

// 创建并暴露一个路由器
export default new VueRouter({
	routes:[
		{
			path:'/about',
			component:About
		},
		{
			path:'/home',
			component:Home
		}
	]
})
src/main.js
import Vue from 'vue'
import App from './App.vue'
import VueRouter from 'vue-router'	// 引入VueRouter
import router from './router'				// 引入路由器

Vue.config.productionTip = false

Vue.use(VueRouter)	// 应用插件

new Vue({
	el:'#app',
	render: h => h(App),
	router:router
})
src/App.vue
<template>
  <div>
    <div class="row">
      <div class="col-xs-offset-2 col-xs-8">
        <div class="page-header"><h2>Vue Router Demo</h2></div>
      </div>
    </div>
    <div class="row">
      <div class="col-xs-2 col-xs-offset-2">
        <div class="list-group">
					<!-- 原始html中我们使用a标签实现页面的跳转 -->
          <!-- <a class="list-group-item active" href="./about.html">About</a> -->
          <!-- <a class="list-group-item" href="./home.html">Home</a> -->

					<!-- Vue中借助router-link标签实现路由的切换 -->
					<router-link class="list-group-item" 
                       active-class="active" to="/about">About</router-link>
          <router-link class="list-group-item" 
                       active-class="active" to="/home">Home</router-link>
        </div>
      </div>
      <div class="col-xs-6">
        <div class="panel">
          <div class="panel-body">
						<!-- 指定组件的呈现位置 -->
            <router-view></router-view>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
	export default {
		name:'App'
	}
</script>
src/components/Home.vue
<template>
	<h2>我是Home的内容</h2>
</template>

<script>
	export default {
		name:'Home'
	}
</script>
src/components/About.vue
<template>
	<h2>我是About的内容</h2>
</template>

<script>
	export default {
		name:'About'
	}
</script>
```

### 6.3. 几个注意事项

1. 路由组件通常存放在 **pages** 文件夹，一般组件通常存放在 **components** 文件夹
   比如上一节的案例就可以修改为
   `src/pages/Home.vue`
   `src/pages/About.vue`
   `src/router/index.js`
   `src/components/Banner.vue`
   `src/App.vue`
2. 通过切换，“隐藏”了的路由组件，**默认是被销毁掉的，需要的时候再去挂载**

1. 每个组件都有自己的**$route**属性，里面存储着自己的路由信息
2. 整个应用只有一个**router**，可以通过组件的**$router**属性获取到

```javascript
// 该文件专门用于创建整个应用的路由器
import VueRouter from "vue-router";
import Home from '../pages/Home'
import About from '../pages/About'

export default new VueRouter({
    routes:[
        {
            path:'/about',
            component:About
        },
        {
            path:'/home',
            component:Home
        }
    ]
})
<template>
    <div class="col-xs-offset-2 col-xs-8">
        <div class="page-header"><h2>Vue Router Demo</h2></div>
    </div>
</template>

<script>
    export default {
        name:'Banner'
    }
</script>
<template>
  <div>
    <div class="row">
      <Banner/>
    </div>
    <div class="row">
      <div class="col-xs-2 col-xs-offset-2">
        <div class="list-group">
          <!-- 原始html中我们使用a标签实现页面跳转 -->
          <!-- <a class="list-group-item active" href="./about.html">About</a>
           <a class="list-group-item" href="./home.html">Home</a> -->
          <!-- Vue中借助router-link标签实现路由的切换 -->
          <router-link class="list-group-item" active-class="active" to="/about">
            About</router-link>
          <router-link class="list-group-item" active-class="active" to="/home">
            Home</router-link>
				</div>
			</div>
			<div class="col-xs-6">
				<div class="panel">
					<div class="panel-body">
						<!-- 指定组件的呈现位置 -->
						<router-view></router-view>
					</div>
				</div>
			</div>
		</div>
	</div>
</template>

<script>
	import Banner from './components/Banner.vue'
	export default {
		name:'App',
		components:{ Banner }
	}
</script>
```

### 6.4. 多级路由

1.  配置路由规则，使用 **children** 配置项

```javascript
routes:[
	{
		path:'/about',
		component:About,
	},
	{
		path:'/home',
		component:Home,
		children:[ 					// 通过children配置子级路由
			{
				path:'news', 		// 此处一定不要带斜杠，写成 /news
				component:News
			},
			{
				path:'message',	// 此处一定不要写成 /message
				component:Message
			}
		]
	}
]
```

1.  跳转（要写完整路径）

```vue
<router-link to="/home/news">News</router-link>
```



![img](https://cdn.nlark.com/yuque/0/2022/png/1379492/1644072950709-6a65f3b3-3ab0-4d65-8dae-b2dbf87df440.png)

```

src/pages/Home.vue
<template>
	<div>
		<h2>Home组件内容</h2>
		<div>
			<ul class="nav nav-tabs">
				<li><router-link class="list-group-item" 
                       active-class="active" to="/home/news">News</router-link></li>
				<li><router-link class="list-group-item" 
                       active-class="active" to="/home/message">Message</router-link></li>
			</ul>
			<router-view></router-view>
		</div>
	</div>
</template>

<script>
	export default {
		name:'Home',
	}
</script>
src/pages/News.vue
<template>
    <ul>
        <li>news001</li>
        <li>news002</li>
        <li>news003</li>
    </ul>
</template>

<script>
    export default {
        name:'News'
    }
</script>
src/pages/Message.vue
<template>
    <ul>
        <li>
            <a href="/message1">message001</a>&nbsp;&nbsp;
        </li>
        <li>
            <a href="/message2">message002</a>&nbsp;&nbsp;
        </li>
        <li>
            <a href="/message/3">message003</a>&nbsp;&nbsp;
        </li>
    </ul>
</template>

<script>
    export default {
        name:'News'
    }
</script>
src/router/index.js
//该文件专门用于创建整个应用的路由器
import VueRouter from "vue-router";
//引入组件
import Home from '../pages/Home'
import About from '../pages/About'
import News from '../pages/News'
import Message from '../pages/Message'

//创建并暴露一个路由器
export default new VueRouter({
    routes:[
        {
            path:'/about',
            component:About
        },
        {
            path:'/home',
            component:Home,
            children:[
                {
                    path:'news',
                    component:News
                },
                {
                    path:'message',
                    component:Message
                }
            ]
        }
    ]
})
```



# Vue Router query 命名路由 params props

### 6.5. 路由的 query 参数

1.  传递参数

```vue
<!-- 跳转并携带query参数，to的字符串写法 -->
<router-link :to="`/home/message/detail?id=${m.id}&title=${m.title}`">跳转</router-link>
				
<!-- 跳转并携带query参数，to的对象写法（推荐） -->
<router-link 
	:to="{
		path:'/home/message/detail',
		query:{
		   id: m.id,
       title: m.title
		}
	}"
>跳转</router-link>
```

1.  接收参数

```javascript
$route.query.id
$route.query.title
```



![img](https://cdn.nlark.com/yuque/0/2022/png/1379492/1644075915640-af4707c7-dfc5-4dd8-b82b-0d4474d70e4b.png)

```
src/router.index.js
import VueRouter from "vue-router";
import Home from '../pages/Home'
import About from '../pages/About'
import News from '../pages/News'
import Message from '../pages/Message'
import Detail from '../pages/Detail'

// 创建并暴露一个路由器
export default new VueRouter({
  routes:[
    {
      path:'/about',
      component:About
    },
    {
      path:'/home',
      component:Home,
      children:[
        {
          path:'news',
          component:News
        },
        {
          path:'message',
          component:Message,
          children:[
            {
              path:'detail',
              component:Detail
            }
          ]
        }
      ]
    }
  ]
})
src/pages/Message.vue
<template>
  <div>
    <ul>
      <li v-for="m in messageList" :key="m.id">
        <!-- 跳转路由并携带query参数，to的字符串写法 -->
        <!-- <router-link :to="`/home/message/detail?id=${m.id}&title=${m.title}`">
                      {{m.title}}
    				 </router-link>&nbsp;&nbsp; -->

        <!-- 跳转路由并携带query参数，to的对象写法 -->
        <router-link :to="{
                            path:'/home/message/detail',
                            query:{
                              id:m.id,
                              title:m.title
                            }
                          }">
          {{m.title}}
      </router-link>&nbsp;&nbsp;
      </li>
    </ul>
    <hr/>
    <router-view></router-view>
  </div>
</template>

<script>
  export default {
    name:'News',
    data(){
      return{
        messageList:[
          {id:'001',title:'消息001'},
          {id:'002',title:'消息002'},
          {id:'003',title:'消息003'}
        ]
      }
    }
  }
</script>
src/pages/Detail.vue
<template>
    <ul>
        <li>消息编号：{{ $route.query.id }}</li>
        <li>消息标题：{{ $route.query.title }}</li>
    </ul>
</template>

<script>
    export default {
        name:'Detail'
    }
</script>
```

### 6.6. 命名路由

命名路由

1. 作用：可以简化路由的跳转
2. 如何使用

1. 1. 给路由命名 

```javascript
{
	path:'/demo',
	component:Demo,
	children:[
		{
			path:'test',
			component:Test,
			children:[
				{
          name:'hello' // 给路由命名
					path:'welcome',
					component:Hello,
				}
			]
		}
	]
}
```

1. 1. 简化跳转

```vue
<!--简化前，需要写完整的路径 -->
<router-link to="/demo/test/welcome">跳转</router-link>

<!--简化后，直接通过名字跳转 -->
<router-link :to="{name:'hello'}">跳转</router-link>

<!--简化写法配合传递参数 -->
<router-link 
	:to="{
		name:'hello',
		query:{
		    id:666,
        title:'你好'
		}
	}"
>跳转</router-link>
```



```
src/router/index.js
import VueRouter from "vue-router";
import Home from '../pages/Home'
import About from '../pages/About'
import News from '../pages/News'
import Message from '../pages/Message'
import Detail from '../pages/Detail'

export default new VueRouter({
    routes:[
        {
            path:'/about',
            component:About
        },
        {
            path:'/home',
            component:Home,
            children:[
                {
                    path:'news',
                    component:News
                },
                {
                    path:'message',
                    component:Message,
                    children:[
                        {
                            name:'detail',	// name配置项为路由命名
                            path:'detail',
                            component:Detail
                        }
                    ]
                }
            ]
        }
    ]
})
src/pages/Message.vue
<template>
    <div>
        <ul>
            <li v-for="m in messageList" :key="m.id">
                <!-- 跳转路由并携带query参数，to的字符串写法 -->
                <!-- <router-link :to="`/home/message/detail?id=${m.id}&title=${m.title}`">
                    {{m.title}}
                </router-link>&nbsp;&nbsp; -->

                <!-- 跳转路由并携带query参数，to的对象写法 -->
                <router-link :to="{
                    name:'detail',	//使用name进行跳转
                    query:{
                        id:m.id,
                        title:m.title
                    }
                }">
                    {{m.title}}
                </router-link>&nbsp;&nbsp;
            </li>
        </ul>
        <hr/>
        <router-view></router-view>
    </div>
</template>

<script>
    export default {
        name:'News',
        data(){
            return{
                messageList:[
                    {id:'001',title:'消息001'},
                    {id:'002',title:'消息002'},
                    {id:'003',title:'消息003'}
                ]
            }
        }
    }
</script>
```

### 6.7. 路由的 params 参数

1. 配置路由，声明接收 **params** 参数

```javascript
{
	path:'/home',
	component:Home,
	children:[
		{
			path:'news',
			component:News
		},
		{
			component:Message,
			children:[
				{
					name:'xiangqing',
					path:'detail/:id/:title', // 🔴使用占位符声明接收params参数
					component:Detail
				}
			]
		}
	]
}
```

1. 传递参数

特别注意：路由携带 **params** 参数时，若使用`to`的对象写法，则**不能使用** **path** **配置项，必须使用** **name** **配置！**

```vue
<!-- 跳转并携带params参数，to的字符串写法 -->
<router-link :to="/home/message/detail/666/你好">跳转</router-link>
				
<!-- 跳转并携带params参数，to的对象写法 -->
<router-link 
	:to="{
		name:'xiangqing',
		params:{
		   id:666,
       title:'你好'
		}
	}"
>跳转</router-link>
```

1. 接收参数

```javascript
$route.params.id
$route.params.title
```



```
src/router/index.js
import VueRouter from "vue-router";
import Home from '../pages/Home'
import About from '../pages/About'
import News from '../pages/News'
import Message from '../pages/Message'
import Detail from '../pages/Detail'

export default new VueRouter({
    routes:[
        {
            path:'/about',
            component:About
        },
        {
            path:'/home',
            component:Home,
            children:[
                {
                    path:'news',
                    component:News
                },
                {
                    path:'message',
                    component:Message,
                    children:[
                        {
                            name:'xiangqing',
                            path:'detail/:id/:title',	// 使用占位符声明接收params参数
                            component:Detail
                        }
                    ]
                }
            ]
        }
    ]
})
src/pages/Message.vue
<template>
    <div>
        <ul>
            <li v-for="m in messageList" :key="m.id">
              
                <!-- 跳转路由并携带params参数，to的字符串写法 -->
                <!-- <router-link :to="`/home/message/detail/${m.id}/${m.title}`">
                    {{m.title}}
                </router-link>&nbsp;&nbsp; -->

                <!-- 跳转路由并携带params参数，to的对象写法 -->
                <router-link :to="{
                    name:'xiangqing',
                    params:{
                        id:m.id,
                        title:m.title
                    }
                }">
                    {{m.title}}
                </router-link>&nbsp;&nbsp;
            </li>
        </ul>
        <hr/>
        <router-view></router-view>
    </div>
</template>

<script>
    export default {
        name:'News',
        data(){
            return{
                messageList:[
                  {id:'001',title:'消息001'},
                  {id:'002',title:'消息002'},
                  {id:'003',title:'消息003'}
                ]
            }
        }
    }
</script>
src/pages/Detail.vue
<template>
  <ul>
    <li>消息编号：{{ $route.params.id }}</li>
    <li>消息标题：{{ $route.params.title }}</li>
  </ul>
</template>

<script>
    export default {
        name:'Detail'
    }
</script>
```

### 6.8. 路由的 props 配置

 **props** 作用：让路由组件更方便的收到参数

```javascript
{
	name:'xiangqing',
	path:'detail/:id',
	component:Detail,

	//第一种写法：props值为对象，该对象中所有的key-value的组合最终都会通过props传给Detail组件
	// props:{a:900}

	//第二种写法：props值为布尔值，为true时，则把路由收到的所有params参数通过props传给Detail组件
	// props:true
	
	//第三种写法：props值为函数，该函数返回的对象中每一组key-value都会通过props传给Detail组件
	props($route){
		return {
			id: $route.query.id,
			title: $route.query.title
		}
	}
}
```



```
src/router/index.js
import VueRouter from "vue-router";
import Home from '../pages/Home'
import About from '../pages/About'
import News from '../pages/News'
import Message from '../pages/Message'
import Detail from '../pages/Detail'

export default new VueRouter({
  routes:[
    {
      path: '/about',
      component: About
    },
    {
      path:'/home',
      component:Home,
      children:[
        {
          path:'news',
          component:News
        },
        {
          path:'message',
          component:Message,
          children:[
            {
              name:'xiangqing',
              path:'detail/:id/:title',
              component:Detail,
              // props的第一种写法，值为对象，
              // 该对象中的所有key-value都会以props的形式传给Detail组件
              // props:{a:1,b:'hello'}

              // props的第二种写法，值为布尔值，
              // 若布尔值为真，会把该路由组件收到的所有params参数，以props的形式传给Detail组件
              // props:true

              // props的第三种写法，值为函数
              props(params) { // 这里可以使用解构赋值
                return {
                  id: params.id,
                  title: params.title,
                }
              }
            }
          ]
        }
      ]
    }
  ]
})
src/pages/Message.vue
<template>
	<div>
    <ul>
      <li v-for="m in messageList" :key="m.id">
        <router-link :to="{
                name:'xiangqing',
                params:{
                    id:m.id,
                    title:m.title
                }
         }">
          	{{m.title}}
  			</router-link>&nbsp;&nbsp;
  		</li>
  	</ul>
    <hr/>
    <router-view></router-view>
  </div>
</template>

<script>
    export default {
        name:'News',
        data(){
            return{
                messageList:[
                    {id:'001',title:'消息001'},
                    {id:'002',title:'消息002'},
                    {id:'003',title:'消息003'}
                ]
            }
        }
    }
</script>
src/pages/Detail.vue
<template>
    <ul>
        <li>消息编号：{{ id }}</li>
        <li>消息标题：{{ title }}</li>
    </ul>
</template>

<script>
    export default {
        name:'Detail',
        props:['id','title']
    }
</script>
```



# Vue Router replace  编程式导航 缓存路由组件

### 6.9. 路由跳转的 replace 方法

1. 作用：**控制路由跳转时操作浏览器历史记录的模式**
2. 浏览器的历史记录有两种写入方式： **push** 和 **replace** 

 **push** 是追加历史记录

 **replace** 是替换当前记录，路由跳转时候默认为 **push** 方式

1. 开启 **replace** 模式

```
**<router-link** **:replace="true"** **...>News</router-link>**
```

简写 **<router-link** **replace** **...>News</router-link>** 

总结：浏览记录本质是一个栈，默认`push`，点开新页面就会在栈顶追加一个地址，后退，栈顶指针向下移动，改为`replace`就是不追加，而将栈顶地址替换



```
src/pages/Home.vue
<template>
  <div>
    <h2>Home组件内容</h2>
    <div>
      <ul class="nav nav-tabs">
        <li>
          <router-link replace class="list-group-item" active-class="active" 
                       to="/home/news">News</router-link>
    		</li>
        <li>
          <router-link replace class="list-group-item" active-class="active" 
                       to="/home/message">Message</router-link>
    		</li>
    </ul>
    <router-view></router-view>
    </div>
  </div>
</template>

<script>
  export default {
    name:'Home'
  }
</script>
```

### 6.10. 编程式路由导航（不用`<router-link>`）

作用：不借助`<router-link>`实现路由跳转，让路由跳转更加灵活

this.$router. **push({})** 	内传的对象与`<router-link>`中的`to`相同

this.$router. **replace({})** 	

this.$router. **forward()** 	前进

this.$router. **back()** 		后退

this.$router. **go(n)** 		可前进也可后退，n为正数前进n，为负数后退

```javascript
this.$router.push({
	name:'xiangqing',
  params:{
    id:xxx,
    title:xxx
  }
})

this.$router.replace({
	name:'xiangqing',
  params:{
    id:xxx,
    title:xxx
  }
})
```



![img](https://cdn.nlark.com/yuque/0/2022/png/1379492/1644152143098-41b0f79d-cf8d-4997-8e5f-43be322e5415.png)

```
src/components/Banner.vue
<template>
	<div class="col-xs-offset-2 col-xs-8">
		<div class="page-header">
			<h2>Vue Router Demo</h2>
			<button @click="back">后退</button>
			<button @click="forward">前进</button>
			<button @click="test">测试一下go</button>
		</div>
	</div>
</template>

<script>
	export default {
		name:'Banner',
		methods:{
			back(){
				this.$router.back()
			},
			forward(){
				this.$router.forward()
			},
			test(){
				this.$router.go(3)
			}
		},
	}
</script>
src/pages/Message.vue
<template>
    <div>
        <ul>
            <li v-for="m in messageList" :key="m.id">
                <router-link :to="{
                    name:'xiangqing',
                    params:{
                        id:m.id,
                        title:m.title
                    }
                }">
                    {{m.title}}
                </router-link>
                <button @click="showPush(m)">push查看</button>
                <button @click="showReplace(m)">replace查看</button>
            </li>
        </ul>
        <hr/>
        <router-view></router-view>
    </div>
</template>

<script>
    export default {
        name:'News',
        data(){
            return{
                messageList:[
                    {id:'001',title:'消息001'},
                    {id:'002',title:'消息002'},
                    {id:'003',title:'消息003'}
                ]
            }
        },
        methods:{
            showPush(m){
                this.$router.push({
                    name:'xiangqing',
                    query:{
                        id:m.id,
                        title:m.title
                    }
                })
            },
            showReplace(m){
                this.$router.replace({
                    name:'xiangqing',
                    query:{
                        id:m.id,
                        title:m.title
                    }
                })
            }
        }
    }
</script>
```

### 6.11. 缓存路由组件

作用：让不展示的路由组件保持挂载，不被销毁

```
**<keep-alive include="****News****">****<router-view></router-view>****</keep-alive>**
**<keep-alive :include="['****News****', '****Message****']">****<router-view></router-view>****</keep-alive>**
// 缓存一个路由组件
<keep-alive include="News"> // include中写想要缓存的组件名，不写表示全部缓存
    <router-view></router-view>
</keep-alive>

// 缓存多个路由组件
<keep-alive :include="['News','Message']"> 
    <router-view></router-view>
</keep-alive>
```



![img](https://cdn.nlark.com/yuque/0/2022/png/1379492/1644152767948-3e9e4103-b4b0-4261-ba33-a11006fc958e.png)

```
src/pages/News.vue
<template>
    <ul>
        <li>news001 <input type="text"></li>
        <li>news002 <input type="text"></li>
        <li>news003 <input type="text"></li>
    </ul>
</template>

<script>
    export default {
        name:'News'
    }
</script>
src/pages/Home.vue
<template>
  <div>
    <h2>Home组件内容</h2>
    <div>
      <ul class="nav nav-tabs">
        <li><router-link replace class="list-group-item" active-class="active" 
                       to="/home/news">News</router-link></li>
        <li><router-link replace class="list-group-item" active-class="active" 
                       to="/home/message">Message</router-link></li>
    	</ul>
      <keep-alive include="News">
        <router-view></router-view>
    	</keep-alive>
    </div>
  </div>
</template>

<script>
    export default {
        name:'Home'
    }
</script>
```





# Vue Router  activated deactivated 路由守卫

### 6.12. activated deactivated 

 **activated** 和 **deactivated** 是路由组件所独有的两个钩子，用于捕获路由组件的激活状态

具体使用

1.  **activated** 路由组件被激活时触发
2.  **deactivated** 路由组件失活时触发



![img](https://cdn.nlark.com/yuque/0/2022/gif/1379492/1644153618338-66b6e803-45c2-4042-a0c7-ef19053a7bc6.gif)

 `src/pages/News.vue`

```vue
<template>
    <ul>
        <li :style="{opacity}">欢迎学习vue</li>
        <li>news001 <input type="text"></li>
        <li>news002 <input type="text"></li>
        <li>news003 <input type="text"></li>
    </ul>
</template>

<script>
    export default {
        name:'News',
        data(){
            return{
                opacity:1
            }
        },
        activated(){
            console.log('News组件被激活了')
            this.timer = setInterval(() => {
                this.opacity -= 0.01
                if(this.opacity <= 0) this.opacity = 1
            },16)
        },
        deactivated(){
            console.log('News组件失活了')
            clearInterval(this.timer)
        }
    }
</script>
```

### 6.13. 路由守卫

作用：对路由进行权限控制 

分类：全局守卫、独享守卫、组件内守卫 

1. **全局守卫**

 **meta** 路由源信息

```javascript
// 全局前置守卫：初始化时、每次路由切换前执行
router.beforeEach((to,from,next) => {
	console.log('beforeEach',to,from)
	if(to.meta.isAuth){ // 判断当前路由是否需要进行权限控制
		if(localStorage.getItem('school') === 'atguigu'){ // 权限控制的具体规则
			next()	// 放行
		}else{
			alert('暂无权限查看')
		}
	}else{
		next()	// 放行
	}
})

// 全局后置守卫：初始化时、每次路由切换后执行
router.afterEach((to,from) => {
	console.log('afterEach',to,from)
	if(to.meta.title){ 
		document.title = to.meta.title //修改网页的title
	}else{
		document.title = 'vue_test'
	}
})
```

1. **独享守卫**

```javascript
beforeEnter(to,from,next){
	console.log('beforeEnter',to,from)
    if(localStorage.getItem('school') === 'atguigu'){
        next()
    }else{
        alert('暂无权限查看')
    }
}
```

1. **组件内守卫**

```vue
//进入守卫：通过路由规则，进入该组件时被调用
beforeRouteEnter (to, from, next) {... next()},

//离开守卫：通过路由规则，离开该组件时被调用
beforeRouteLeave (to, from, next) {... next()},
```



#### 6.13.1. 全局路由守卫

```
src/router/index.js
//该文件专门用于创建整个应用的路由器
import VueRouter from "vue-router";
//引入组件
import Home from '../pages/Home'
import About from '../pages/About'
import News from '../pages/News'
import Message from '../pages/Message'
import Detail from '../pages/Detail'


//创建一个路由器
const router = new VueRouter({
    routes:[
        {
            name:'guanyv',
            path:'/about',
            component:About,
            meta:{title:'关于'}
        },
        {
            name:'zhuye',
            path:'/home',
            component:Home,
            meta:{title:'主页'},
            children:[
                {
                    name:'xinwen',
                    path:'news',
                    component:News,
                    meta:{isAuth:true,title:'新闻'}
                },
                {
                    name:'xiaoxi',
                    path:'message',
                    component:Message,
                    meta:{isAuth:true,title:'消息'},
                    children:[
                        {
                            name:'xiangqing',
                            path:'detail',
                            component:Detail,
                            meta:{isAuth:true,title:'详情'},
                            props($route){
                                return {
                                    id:$route.query.id,
                                    title:$route.query.title,
                                }
														}
                        }
                    ]
                }
            ]
        }
    ]
})

// 🔴全局前置路由守卫————初始化的时候、每次路由切换之前被调用
router.beforeEach((to,from,next) => {
    console.log('前置路由守卫',to,from)
    if(to.meta.isAuth){
        if(localStorage.getItem('school')==='atguigu'){
            next()
        }else{
            alert('学校名不对，无权限查看！')
        }
    }else{
        next()
    }
})

// 🔴全局后置路由守卫————初始化的时候被调用、每次路由切换之后被调用
router.afterEach((to,from)=>{
	console.log('后置路由守卫',to,from)
	document.title = to.meta.title || '硅谷系统'
})

// 导出路由器
export default router
```

#### 6.13.2. 独享路由守卫

```
src/router/index.js
//该文件专门用于创建整个应用的路由器
import VueRouter from "vue-router";
//引入组件
import Home from '../pages/Home'
import About from '../pages/About'
import News from '../pages/News'
import Message from '../pages/Message'
import Detail from '../pages/Detail'


//创建一个路由器
const router = new VueRouter({
    routes:[
        {
            name:'guanyv',
            path:'/about',
            component:About,
            meta:{title:'关于'}
        },
        {
            name:'zhuye',
            path:'/home',
            component:Home,
            meta:{title:'主页'},
            children:[
                {
                    name:'xinwen',
                    path:'news',
                    component:News,
                    meta:{title:'新闻'},
                    // 🔴独享守卫，特定路由切换之后被调用
                    beforeEnter(to,from,next){
                        console.log('独享路由守卫',to,from)
                        if(localStorage.getItem('school') === 'atguigu'){
                            next()
                        }else{
                            alert('暂无权限查看')
                        }
                    }
                },
                {
                    name:'xiaoxi',
                    path:'message',
                    component:Message,
                    meta:{title:'消息'},
                    children:[
                        {
                            name:'xiangqing',
                            path:'detail',
                            component:Detail,
                            meta:{title:'详情'},
                            props($route){
                                return {
                                    id:$route.query.id,
                                    title:$route.query.title,
                                }
                            }
                        }
                    ]
                }
            ]
        }
    ]
})

//全局后置路由守卫————初始化的时候被调用、每次路由切换之后被调用
router.afterEach((to,from)=>{
	console.log('后置路由守卫',to,from)
	document.title = to.meta.title || '硅谷系统'
})

//导出路由器
export default router
```

#### 6.13.3. 组件内路由守卫

```
src/pages/About.vue
<template>
    <h2>我是About组件的内容</h2>
</template>

<script>
    export default {
        name:'About',
        // 通过路由规则，离开该组件时被调用
        beforeRouteEnter (to, from, next) {
            console.log('About--beforeRouteEnter',to,from)
            if(localStorage.getItem('school')==='atguigu'){
                next()
            }else{
                alert('学校名不对，无权限查看！')
            }
        },
        // 通过路由规则，离开该组件时被调用
        beforeRouteLeave (to, from, next) {
            console.log('About--beforeRouteLeave',to,from)
            next()
        }
    }
</script>
```

### 6.14. 路由器的两种工作模式

1.  对于一个`url`来说，什么是`hash值`？

  **#** **及其后面的内容就是** **hash值** 

1.  `hash值`不会包含在`HTTP`请求中，即：`hash值`不会带给服务器 
2.  **hash** 模式 

1. 1. 地址中永远带着#号，不美观
   2. 若以后将地址通过第三方手机app分享，若app校验严格，则地址会被标记为不合法

1. 1. 兼容性较好

1.   **history** 模式

1. 1. 地址干净，美观
   2. 兼容性和`hash`模式相比略差

1. 1. 应用部署上线时需要后端人员支持，解决刷新页面服务端404的问题

```javascript
const router =  new VueRouter({
	mode:'history',
	routes:[...]
})

export default router
```

# Vue UI 组件库

### 7.1 常用UI组件库

#### 7.1.1 移动端常用UI组件库

1. [Vant](https://youzan.github.io/vant)

1. [Cube UI](https://didi.github.io/cube-ui)

1. [Mint UI](http://mint-ui.github.io)
2. https://nutui.jd.com/#/

#### 7.1.2. PC端常用UI组件库

1. [Element UI](https://element.eleme.cn)

1. [IView UI](https://www.iviewui.com)

### 7.2. element-ui基本使用

1.  安装 element-ui： **npm i element-ui -S**  

1.  `src/main.js`

```javascript
import Vue from 'vue'
import App from './App.vue'
import ElementUI from 'element-ui';							// 引入ElementUI组件库
import 'element-ui/lib/theme-chalk/index.css';	// 引入ElementUI全部样式

Vue.config.productionTip = false

Vue.use(ElementUI)	// 使用ElementUI

new Vue({
    el:"#app",
    render: h => h(App),
})
```

1.  `src/App.vue`

```vue
<template>
	<div>
		<br>
		<el-row>
			<el-button icon="el-icon-search" circle></el-button>
			<el-button type="primary" icon="el-icon-edit" circle></el-button>
			<el-button type="success" icon="el-icon-check" circle></el-button>
			<el-button type="info" icon="el-icon-message" circle></el-button>
			<el-button type="warning" icon="el-icon-star-off" circle></el-button>
			<el-button type="danger" icon="el-icon-delete" circle></el-button>
		</el-row>
	</div>
</template>

<script>
	export default {
		name:'App',
	}
</script>
```

![img](https://gitee.com/kazamikazuki-picture-bed/drawing-bed-1/raw/master/vue/20210813231907.png)

### 7.3. element-ui按需引入

1.  安装 babel-plugin-component **npm i babel-plugin-component -D**  

1.  修改  **babel-config-js** 

```javascript
module.exports = {
  presets: [
    '@vue/cli-plugin-babel/preset',
    ["@babel/preset-env", { "modules": false }]
  ],
  plugins: [
    [
      "component",
      {        
        "libraryName": "element-ui",
        "styleLibraryName": "theme-chalk"
      }
    ]
  ]
}
```

1.  `src/main.js`:  

```javascript
import Vue from 'vue'
import App from './App.vue'
import { Button,Row } from 'element-ui'	// 按需引入

Vue.config.productionTip = false

Vue.component(Button.name, Button);
Vue.component(Row.name, Row);
/* 或写为
 * Vue.use(Button)
 * Vue.use(Row)
 */

new Vue({
    el:"#app",
    render: h => h(App),
})
```



