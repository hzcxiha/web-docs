## vue基础
[官方地址](https://cn.vuejs.org/)

### [安装](安装)

CDN

```
<script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>
```

NPM


```
npm install vue
```

命令行工具 (CLI)

推荐官方脚手架[vue-cli](https://cli.vuejs.org/zh/guide/)

vue-cli构建SPA应用


```
npm install -g @vue/cli
# OR
yarn global add @vue/cli

vue --version

vue create projectName
```
### Vue的插值表达式


```
<div id="app">
    <h1>{{ userName }}</h1>
    <h1>{{ userName + "搬家"}}</h1>
    <h1>{{ age + 1 }}</h1>
    <h1>{{ age > 18 ? "成年" : "未成年" }}</h1>
    <h1>{{ userName.split("").reverse().join("") }}</h1>
</div>

<script>
    var vm = new Vue({
        el:"#app",
        data:{
            userName:"xxx",
            age:18,
        }
    })
</script>
```
### Vue的基础指令

#### v-text

- v-text的值可以设置表达式，与差值表达式相同
- v-text会替换掉标签的内容


```
<div id="app">

    <!-- 这个显示的是小明 -->
    <h1 v-text="userName"></h1> 

    <!-- 这个显示的也是小明 -->
    <h1 v-text="userName">-----</h1>

    <!-- 使用v-text不会让浏览器渲染标签 -->
    <div v-text="htmlStr"></div>
</div>
<script>
    var vm = new Vue({
        el: "#app",
        data: {
            userName:"小明"
            htmlStr:"<h2>吵架</h>"
        }
    })
</script>
```

#### v-html

- v-html可以在HTML页面上渲染标签


```
<div id="app">
    <!-- 这里显示的是h2标签的 “吵架” -->
   <div v-html="htmlStr"></div>
</div>

<script>
    var vm = new Vue({
        el: "#app",
        data: {
            htmlStr:"<h2>吵架</h>"
        }
    })
</script>
```
#### v-bind

- v-bind 可以给标签动态绑定属性

   
```
<div id="app">

        <!-- 给img标签添加src地址 -->
        <img v-bind:src="imgSrc" alt="">
        <!-- 简写 -->
        <img :src="imgSrc" alt="">

        <!-- 给a标签添加href地址 -->
        <a :href="theHref">Vue官网</a>
        <!-- a标签地址的字符串拼接 -->
        <a :href="'delete.php?id=' + theId">删除</a>

        <!-- ES6的模板字符串 这样写也行 -->
        <a :href="'delete.php?id=${theId}'">删除</a>

        <!-- {red:flag} red是类名 flag为true时该标签设置这个类名 -->
        <p :class="{red:flag}">中午吃啥</p>
        <p :class="{red:age == 18}">中午吃啥</p>

    </div>

    <script>
        var vm = new Vue({
            el:"#app",
            data:{
                imgSrc:"https://cn.vuejs.org/images/logo.png",
                theId:111,
                theHref:"https://cn.vuejs.org/v2/api/#v-text",
                flag:true,
                age:1
            }
        })
    </script>
```

#### v-for

- v-for 遍历数组、json元素用

<div id="app">
        <ul>
            <!-- item 数组中的每一项 list data中的数组 -->
            <li v-for="item in list" :key="item.id">{{ item.id }}:{{ item.name }}</li>
        </ul>

        <ul>
             <!-- item 数组中的每一项 index数组的下标 -->
            <li v-for="(item,index) in list" :key="index">
                {{ index }} : {{ item.name }}
            </li>
        </ul>

        <ul>    
            <li v-for="value in user" :key="value">
                {{ value }}
            </li>
        </ul>

        <ul>
            <li v-for="(value,key,index) in user">
                {{ key }} : {{ value }} ------- {{ index }}
            </li>
        </ul>
    </div>

    <script>
        var vm = new Vue({
            el:"#app",
            data:{              
                list:[
                    {id:1,name:"xxx"},
                    {id:2,name:"zzz"},
                    {id:3,name:"ccc"}
                ],
                user:{name:"vvv",age:20}
            }
        })
    </script>

#### v-model

- v-model 可实现数据双向绑定，这个指令只能给input、textarea、select使用


```
<div id="app">
    <input type="text" v-model="msg" >
    <input type="text" :value="msg" >
    <h1>{{ msg }}</h1>
</div>

<script>
    var vm = new Vue({
        el:"#app",
        data:{
            msg:"Hello Vue"
        }
    })
</script>
```

#### v-on

- 绑定事件

```
<!-- 点击事件绑定 -->
<div v-on:click="changeName">点击改变name</div>
<!-- 这个是简写 -->
<button @click="changeName">点击改变name</button>


<!-- 函数传参 -->
<button @click="abc('ccc')">传参</button>

<!-- 获取时间对象 -->
<button @click="getEvent($event)">获取事件对象</button>

<!-- 事件修饰符-阻止默认事件 -->
<a href="http://www.baidu.com" @click.prevent="baidu">百度一下</a>

<!-- 按键修饰符 -->
<!-- 按回车键响应 -->
<input type="text" v-model="name" @keyDown.enter="submit">
<!-- 按65号键响应 -->
<input type="text" v-model="name" @keyDown.65="submit">


<!-- methods中的点击事件中的this 指的是 新建的Vue对象 -->
<script>
    var vm = new Vue({
        el:"#app",
        data:{
            name:"xxxx"
        },
        methods: {
            changeName(){
                console.log(this === vm);
                this.name = "zzz";
            },
            abc(newName) {
                this.name = newName;
            },
            getEvent(e) {
                console.log(e);
            },
            baidu() {
                console.log("百度一下");
            },
            submit() {
                alert("点击回车");
            }
        },
    })
</script>
```

#### v-if
- v-if 根据条件创建标签

```
<div id="app">
<!-- 只显示第一个p标签 -->
    <p v-if="age >= 18">已成年</p>
    <p v-if="age < 18">未成年</p>
</div>

<script>
    var vm = new Vue({
        el:"#app",
        data:{              
            age:18,
        }
    })
</script>
```
#### v-show
- v-show 标签全部创建 但是根据条件显示

```
<div id="app">
<!-- 标签都创建，只显示第一个p标签，第二个隐藏display -->
    <p v-show="age >= 18">已成年</p>
    <p v-show="age < 18">未成年</p>
</div>

<script>
    var vm = new Vue({
        el:"#app",
        data:{              
            age:18,
        }
    })
</script>
```
## 组件

### 注册组件
注册组件就是利用Vue.component()方法，先传入一个自定义组件的名字，然后传入这个组件的配置。


```
 Vue.component('mycomponent',{
    template: `<div>这是一个自定义组件</div>`,
    data () {
      return {
        message: 'hello world'
      }
    }
  })
```
如上方式，就已经创建了一个自定义组件，然后就可以在Vue实例挂在的DOM元素中使用它。


```
<div id="app">
    <mycomponent></mycomponent>
    <my-component></my-component>
</div>
<script>
  var app = new Vue({
    el: '#app',
    data: {
    },
    components: {
      'my-component': {
        template: `<div>这是一个局部的自定义组件，只能在当前Vue实例中使用</div>`,
      }
    }
  })
</script>

```
### class的方式定义组件

vue官网推荐[vue-class-component](https://github.com/vuejs/vue-class-component)




```
<script>
import Vue from 'vue'
import Component from 'vue-class-component'

@Component({
  props: {
    propMessage: String
  }
})
export default class App extends Vue {
  // 初始化数据 data可以声明成类属性形式
  msg = 123

  // 使用props
  helloMsg = 'Hello, ' + this.propMessage

  // 生命周期钩子声明  保留名称
  mounted () {
    this.greet()
  }

  // computed属性可以声明成类方法形式
  get computedMsg () {
    return 'computed ' + this.msg
  }

  // method方法可以声明成类方法形式
  greet () {
    alert('greeting: ' + this.msg)
  }
}
</script>
```
### 父组件到子组件通讯

通过 [props](https://cn.vuejs.org/v2/api/#props) 传递数据 (推荐)

prop 的定义应该尽量详细，至少需要指定其类型


```
<!-- 父组件 -->
<template>
    <div>
        <my-child :parentMessage="parentMessage"></my-child>
    </div>
</template>

<script>
    import MyChild from '@components/common/MyChild'

    export default {
        components: {
            MyChild
        },
        data() {
            return {
                parentMessage: "我是来自父组件的消息"
            }
        }
    }
</script>
```


```
<!-- 子组件 -->
<template>
    <div>
        <span>{{ parentMessage }}</span>
    </div>
</template>

<script>
    export default {
        props: {
            parentMessage: {
                type: String,
                default: '默认显示的信息'
                // require: true // 必填
            }
        }
    }
</script>
```
### refs 获取
可以通过在子组件添加ref属性，然后可以通过ref属性名称获取到子组件的实例。

```
<!-- 父组件 -->
<template>
    <div>
        <my-child ref="child"></my-child>
    </div>
</template>

<script>
    import MyChild from '@components/common/MyChild'

    export default {
        components: {
            MyChild
        },
        mounted() {
            console.log(this.$refs['child'].getData());
        }
    }
</script>

<!-- 子组件 -->
<script>
    export default {
        methods: {
            getData() {
                // do something...
            }
        }
    }
</script>
```

### 子组件到父组件通讯

通过 $emit 传递父组件数据


```
<!-- 父组件 -->
<template>
    <div>
        <my-child @childEvent="parentMethod"></my-child>
    </div>
</template>

<script>
    import MyChild from '@components/common/MyChild'

    export default {
        components: {
            MyChild
        },
        data() {
            return {
                parentMessage: '我是来自父组件的消息'
            }
        },
        methods: {
            parentMethod({ name, age }) {
                console.log(this.parentMessage, name, age)
            }
        }
    }
</script>
```


```
<!-- 子组件 -->
<template>
    <div>
        <h3>子组件</h3>
    </div>
</template>

<script>
    export default {
        mounted() {
            this.$emit('childEvent', { name: 'zhangsan', age:  10 })
        }
    }
</script>
```
### 计算属性computed
计算属性一般就是用来通过其他的数据算出一个新数据，而且它有一个好处就是它把新的数据缓存下来了，当其他的数据没有发生改变，它调用的是缓存的数据，这就极大的提高了我们程序的性能。



## vuex

[文档](https://vuex.vuejs.org/zh/installation.html)

### 引言

```
export default new Vuex.Store({
    state,
    getters,
    mutations,
    actions  
})
```
这就是一个典型的使用vuex生成的仓库

简单说一下后端做什么的？进行数据库操作，处理请求，根据请求分发响应。聊聊数据库的操作，不说API。首先，从数据库中取值得有一套取数据的API，我们给他们集中起个名字，既然是获取，那就叫**getter**。我们还得存数据呀。存数据就是对数据库的修改，这些API，我们也得给它起个名字，就叫**mutation**。

我们暂且称vuex就是“前端的数据库”。**State** 就是数据库。Mutations就是我们把数据存入数据库的 API，用来修改state 的。getters 是我们从数据库里取数据的 API，既然是取，肯定不能把数据库给改了，所以**getters得是一个“纯函数”，就是不会对原数据造成影响的函数**

**actions**呢？后端从前端拿到了数据，总要做个处理吧，处理完了再存到数据库中。其实这就是action的过程当然你也可以不做处理，直接丢到数据库，所以vuex也可以在action 中直接存，就是直接mutation。


现在，我们再来看看vuex的数据流。后（qian）端通过**action**处理数据，然后通过**mutation**把处理后的数据放入数据库（**state**）中，用时通过**getter**从数据库（state）中取。

### 正文
Vuex 是一个专为 Vue.js 应用程序开发的状态管理模式。它采用集中式存储管理应用的所有组件的状态，并以相应的规则保证状态以一种可预测的方式发生变化。

### store
每一个 Vuex 应用的核心就是 store（仓库）。“store”基本上就是一个容器，它包含着你的应用中大部分的状态 (state)。Vuex 和单纯的全局对象有以下两点不同：

1. Vuex 的状态存储是响应式的。当 Vue 组件从 store 中读取状态的时候，若 store 中的状态发生变化，那么相应的组件也会相应地得到高效更新。
2. 你不能直接改变 store 中的状态。改变 store 中的状态的唯一途径就是显式地提交 (commit) mutation。这样使得我们可以方便地跟踪每一个状态的变化，从而让我们能够实现一些工具帮助我们更好地了解我们的应用。

### State
每个应用将仅仅包含一个store实例，作为一个“唯一数据源”而存在。
可以通过this.$store.state直接获取state里的数据

### Getter
Vuex 允许我们在store中定义“getter”（可以认为是 store的计算属性）。就像计算属性一样，getter的返回值会根据它的依赖被缓存起来，且只有当它的依赖值发生了改变才会被重新计算。

Getter 接受 state 作为其第一个参数：

```
const store = new Vuex.Store({
  state: {
    todos: [
      { id: 1, text: '...', done: true },
      { id: 2, text: '...', done: false }
    ]
  },
  getters: {
    doneTodos: state => {
      return state.todos.filter(todo => todo.done)
    }
  }
})
```
我们可以很容易地在任何组件中使用它：


```
computed: {
  doneTodos () {
    return this.$store.getters.doneTodos
  }
}
```

### Mutation
更改 Vuex 的store中的状态的唯一方法是提交 mutation。Vuex中的mutation非常类似于事件：每个mutation都有一个字符串的 事件类型 (type)和一个回调函数(handler)。这个回调函数就是我们实际进行状态更改的地方，并且它会接受state作为第一个参数：


```
const store = new Vuex.Store({
  state: {
    count: 1
  },
  mutations: {
    increment (state) {
      // 变更状态
      state.count++
    }
  }
})
//当触发一个类型为 increment 的 mutation 时,需要以相应的 type 调用 store.commit 方法
store.commit('increment')
```
#### 提交载荷（Payload）

可以向 store.commit 传入额外的参数，即 mutation 的 载荷（payload）：


```
mutations: {
  increment (state, n) {
    state.count += n
  }
}

store.commit('increment', 10)
```
在大多数情况下，载荷应该是一个对象


```
mutations: {
  increment (state, payload) {
    state.count += payload.amount
  }
}

store.commit('increment', {
  amount: 10
})
```

### Action

- **Action 提交的是mutation，而不是直接变更状态。**
- **Action 可以包含任意异步操作。**


```
const store = new Vuex.Store({
  state: {
    count: 0
  },
  mutations: {
    increment (state) {
      state.count++
    }
  },
  actions: {
    increment (context) {
      context.commit('increment')
    }
  }
})
```
实践中，我们会经常用到 ES2015 的 参数解构 来简化代码（特别是我们需要调用 commit 很多次的时候）：


```
actions: {
  increment ({ commit }) {
    commit('increment')
  }
}
```

#### 分发 Action

Action 通过 store.dispatch 方法触发：

```
store.dispatch('increment')
```
我们可以在 action 内部执行异步操作：

```
actions: {
  incrementAsync ({ commit }) {
    setTimeout(() => {
      commit('increment')
    }, 1000)
  }
}

// 以载荷形式分发
store.dispatch('incrementAsync', {
  amount: 10
})

// 以对象形式分发
store.dispatch({
  type: 'incrementAsync',
  amount: 10
})
```
#### 在组件中分发 Action

在组件中使用 this.$store.dispatch('xxx') 分发 action，或者使用 mapActions 辅助函数将组件的 methods 映射为 store.dispatch 调用（需要先在根节点注入 store）：

```
import { mapActions } from 'vuex'

export default {
  // ...
  methods: {
    ...mapActions([
      'increment', // 将 `this.increment()` 映射为 `this.$store.dispatch('increment')`

      // `mapActions` 也支持载荷：
      'incrementBy' // 将 `this.incrementBy(amount)` 映射为 `this.$store.dispatch('incrementBy', amount)`
    ]),
    ...mapActions({
      add: 'increment' // 将 `this.add()` 映射为 `this.$store.dispatch('increment')`
    })
  }
}
```
## [TypeScript](https://www.tslang.cn/samples/index.html)

> TypeScript is a typed superset of JavaScript that compiles to plain JavaScript.

TypeScript是一个编译到纯JS的有类型定义的JS超集。
TS遵循当前以及未来出现的ECMAScript规范。TS不仅能兼容现有的JavaScript 代码，它也拥有兼容未来版本的JavaScript的能力。大多数TS的新增特性 都是基于未来的JavaScript提案，这意味着许多TS代码在将来很有可能会变成ECMA的标准.

2009年微软公司提出了TypeScript的第一个版本，是由C#之父Anders Hejlsberg 领导开发的, 了解C#的同学学起来就幸福了。

### TS有什么好处？

**TypeScript能从可维护性、健壮性等方面提高代码质量。**

常见的代码检查工具：JsHint / JsLint / EsLint

Eslint 这些语法检查的能提前检查出来这些错误，减少了调试的成本，减少了线上bug.


但是还有不足，比如一些参数类型，个数的错误检测不到。
谨慎的程序员会做个判空处理等，来避免这样的错误。如果未处理，在复杂的线上环境中，程序就有可能会崩溃。
而TS可以帮助我们避免这些问题，从而提高代码健壮性, 因为TS是强类型的语言，下面看下它怎样约束类型的。

#### 类型注解


```
let str: string = 'ts';
let isShow: boolean = true;
```


类型 | 描述
---|---
Boolean | 与JS相同
Number | 与JS相同
String | 与JS相同
Array | 与JS相同; 增加了泛型数组, 元组(Tuple)
Enum | enum类型是为了给一个数字集合更友好地命名
any | any类型可以表示任意JavaScript值

void | void就是any的对立面，即所有类型都不存在的时候。你会在一个没有返回值的函数看到它

### 对面向对象思想进行了增强

#### 接口（Interface）

TypeScript的核心原则之一是对值所具有的结构进行类型检查。 在TypeScript里，接口的作用就是为这些类型命名和为你的代码或第三方代码定义契约。


```
interface SquareConfig {
  color?: string;
  width?: number;
}
```

#### 泛型

泛型用来创建可重用的组件，一个组件可以支持多种类型的数据。 这样用户就可以以自己的数据类型来使用组件。

## vue-property-decorator

[文档](https://www.npmjs.com/package/vue-property-decorator)

[GitHub](https://github.com/kaorun343/vue-property-decorator#Provide)

[文章1](https://juejin.im/post/5c173a84f265da610e7ffe44)

[文章2](https://www.jianshu.com/p/88ff51bb9ebf)

### vue项目三步走

1. 建页面
1. 配路由
1. 增store（可有可无）