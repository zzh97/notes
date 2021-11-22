#### 1 从npm升级至yarn

##### 1.1 npm的问题

* `npm install`的时候**巨慢**。特别是新的项目拉下来要等半天，删除node_modules，重新install的时候依旧如此
* 同一个项目，安装的时候**无法保持一致性**。由于package.json文件中版本号的特点，下面三个版本号在安装的时候代表不同的含义

```
"5.0.3",
"~5.0.3",
"^5.0.3"
```

“5.0.3”表示安装指定的5.0.3版本，“～5.0.3”表示安装5.0.X中最新的版本，“^5.0.3”表示安装5.X.X中最新的版本。这就麻烦了，常常会出现同一个项目，有的同事是OK的，有的同事会由于安装的版本不一致出现bug

* 安装的时候，包会在同一时间下载和安装，中途某个时候，一个包抛出了一个错误，但是npm会继续下载和安装包。因为npm会把所有的日志输出到终端，有关错误包的错误信息就会在一大堆npm打印的警告中丢失掉，并且你甚至永远**不会注意到实际发生的错误**

##### 1.2 Yarn的优点

* **速度快**：并行安装（无论 npm 还是 Yarn 在执行包的安装时，都会执行一系列任务。npm 是按照队列执行每个 package，也就是说必须要等到当前 package 安装完成之后，才能继续后面的安装。而 Yarn 是同步执行所有任务，提高了性能），离线模式（如果之前已经安装过一个软件包，用Yarn再次安装时之间从缓存中获取，就不用像npm那样再从网络下载了）
* 安装**版本统一**：了防止拉取到不同的版本，Yarn 有一个锁定文件 (lock file) 记录了被确切安装上的模块的版本号
* **更简洁的输出**：npm 的输出信息比较冗长。在执行 `npm install <package>` 的时候，命令行里会不断地打印出所有被安装上的依赖
* **多注册来源处理**：所有的依赖包，不管他被不同的库间接关联引用多少次，安装这个包时，只会从一个注册来源去装，要么是 npm 要么是 bower, 防止出现混乱不一致

##### 1.3 Yarn和npm命令对比

>​                                       **npm** | **yarn**
>
>​                            npm install | yarn
>
>​       npm install react --save | yarn add react
>
>   npm uninstall react --save | yarn remove react
>
>npm install react --save-dev |  yarn add react --dev
>
>​                npm update --save | yarn upgrade

##### 1.4 使用npm安装yarn

```
npm install -g yarn
```

安装好后，测试是否安装成功

```
yarn -v
```

Yarn的官方文档：https://yarn.bootcss.com/docs/



#### 2 从vue-cli升级至vite

##### 2.1 Webpack开发服务器架构

Vue CLI是构建在Webpack之上的，因此开发服务器和构建功能和性能都将是Webpack的超集

Webpack的工作方式是，它通过解析应用程序中的每一个 `import` 和 `require` ，将整个应用程序构建成一个基于JavaScript的捆绑包，并在运行时转换文件（例如Sass、TypeScript、SFC）

这都是在服务器端完成的，依赖的数量和改变后构建/重新构建的时间之间有一个大致的线性关系

##### 2.2 Vite开发服务器架构

与Vue CLI类似，Vite也是一个提供基本项目脚手架和开发服务器的构建工具

然而，Vite并不是基于Webpack的，它有自己的开发服务器，利用浏览器中的原生ES模块。这种架构使得Vite比Webpack的开发服务器快了好几个数量级。Vite采用Rollup进行构建，速度也更快

Vite不捆绑应用服务器端。相反，它依赖于浏览器对JavaScript模块的原生支持（也就是ES模块，是一个比较新的功能）

浏览器将在需要时通过HTTP请求任何JS模块，并在运行时进行处理。Vite开发服务器将按需转换任何文件（如Sass、TypeScript、SFC）

这种架构避免了服务器端对整个应用的捆绑，并利用浏览器高效的模块处理，提供了一个明显更快的开发服务器

##### 2.3 vue-cli和vite的对比

>​                                  **Vue CLI 优点** | **Vite缺点 **
>
>​                  经历过战斗考验，可靠 | 只能针对现代浏览器（ES2015+）
>
>​                                   与Vue 2兼容 | 与CommonJS模块不完全兼容
>
>​       可以捆绑任何类型的依赖关系 | 处于测试阶段，仅支持Vue 3
>
>​                                  插件生态系统 | 最小的脚手架不包括Vuex、路由器等
>
>​       可以针对不同的目标进行构建 | 不同的开发服务器与构建工具
>
>​                                   **Vue CLI 缺点** | **Vite优点 **
>
>开发服务器速度与依赖数量成反比 | 开发服务器比Webpack快10-100倍

##### 2.4 安装vite

使用 NPM（我这会直接变成一个init的文件夹）:

```
npm init @vitejs/app
```

或

```
npm init @vitejs/app my-vue-app --template vue
```

使用 Yarn（用yarn就不会，而会让你输入名称）:

```
yarn create @vitejs/app
```

或

```
yarn create @vitejs/app my-vue-app --template vue
```

安装依赖

```
npm install
```

```
yarn
```

运行

```
npm run dev
```

```
yarn run dev
```

Vite的官方文档：https://vitejs.cn/guide/



#### 3 Composition API

##### 3.1 data中的响应式数据

在vue2中是这样的

```
<template>
    <div>
        <h1>{{ msg }}</h1>
    </div>
</template>

<script>
	exports default {
		data() {
			return {
				msg: 'Hello Vue2'
			}
		},
	}
</script>
```

而在Vue3中是这样的

```
<!-- setup是一个语法糖，详情见注解 -->
<script setup>
// ref用于创建响应式变量
import { ref } from 'vue'
// const是JS的限定符，表示该变量地址不可变
const msg = reactive('Hello Vue3')
</script>

<template>
	<!-- 外层不需要一个单独的div -->
	<h1>{{ msg }}</h1>
</template>
```

注解：`<script setup>`中的setup是一个语法糖，相当于在`<script>`中创建setup函数，并自动把函数里声明的变量return出来；注意由于setup先于data和methods的解释，故不能使用this

##### 3.2 methods中的方法

在vue2中是这样的

```
<template>
    <div>
        <h1>{{ msg }}</h1>
        <button @click="changeMsg">Click Me</button>
    </div>
</template>

<script>
	exports default {
		data() {
			return {
				msg: 'Hello Vue2'
			}
		},
		methods: {
			changeMsg () {
				this.msg = 'The msg has been Changed'
			}
		}
	}
</script>
```

而在Vue3中是这样的

```
<script setup>
// ref用于创建响应式变量，和reactive相比（在script中使用需要加value）
import { ref } from 'vue'
const msg = ref('Hello Vue3')
const changeMsg = function () {
	msg.value = 'The msg has been Changed'
}
</script>

<template>
	<h1>{{ msg }}</h1>
	<button @click="changeMsg">Click Me</button>
</template>
```

##### 3.3 生命周期

在vue2中是这样的

```
<template>
    <div>
        <h1>{{ msg }}</h1>
        <button @click="changeMsg">Click Me</button>
    </div>
</template>

<script>
	exports default {
		data() {
			return {
				msg: 'Hello Vue2'
			}
		},
		methods: {
			changeMsg () {
				this.msg = 'The msg has been Changed'
			}
		}
		mounted () {
			this.msg = 'Hello Vue2 (mounted)'
		}
	}
</script>
```

而在Vue3中是这样的

```
<script setup>
// 生命周期需要引入（Vue3中没有Created）
import { ref, onMounted } from 'vue'
const msg = ref('Hello Vue3')
const changeMsg = function () {
	msg.value = 'The msg has been Changed'
}
onMounted (() => {
	msg.value = 'Hello Vue3 (mounted)'
})
</script>

<template>
	<h1>{{ msg }}</h1>
	<button @click="changeMsg">Click Me</button>
</template>
```

##### 3.4 父向子通信

在vue2中是这样的

```
<template>
    <div>
        <h1>{{ msg }}</h1>
        <button @click="changeMsg">Click Me</button>
        <p>{{ fatherMsg }}</p>
    </div>
</template>

<script>
	exports default {
		props: {
			fatherMsg: String
		}
		data() {
			return {
				msg: 'Hello Vue2'
			}
		},
		methods: {
			changeMsg () {
				this.msg = 'The msg has been Changed'
			}
		}
		mounted () {
			this.msg = 'Hello Vue2 (mounted)'
		}
	}
</script>
```

父组件

```
<script>
    import HelloWorld from './components/HelloWorld.vue'
    exports default {
        componentes: {
            HelloWorld
        }
    }
</script>

<template>
  <HelloWorld msg="Hello Vue3" />
</template>
```

而在Vue3中是这样的

```
<script setup>
import { ref, onMounted } from 'vue'
// 组件通信的设置
defineProps({
  fatherMsg: String
})
const msg = ref('Hello Vue3')
const changeMsg = function () {
	msg.value = 'The msg has been Changed'
}
onMounted (() => {
	msg.value = 'Hello Vue3 (mounted)'
})
</script>

<template>
	<h1>{{ msg }}</h1>
	<button @click="changeMsg">Click Me</button>
	<p>{{ fatherMsg }}</p>
</template>
```

父组件

```
<script setup>
// 可以直接用<HelloWorld />
import HelloWorld from './components/HelloWorld.vue'
</script>

<template>
  <HelloWorld msg="Hello Vue2" />
</template>
```

##### 3.5 子向父通信

在vue2中是这样的

```
<template>
    <div>
        <h1 @click="$emit('getChildMsg', msg)">{{ msg }}(alert by click)</h1>
        <button @click="changeMsg">Click Me</button>
        <p>{{ fatherMsg }}</p>
    </div>
</template>

<script>
	exports default {
		props: {
			fatherMsg: String
		}
		data() {
			return {
				msg: 'Hello Vue2'
			}
		},
		methods: {
			changeMsg () {
				this.msg = 'The msg has been Changed'
			}
		}
		mounted () {
			this.msg = 'Hello Vue2 (mounted)'
		}
	}
</script>
```

父组件

```
<script>
    import HelloWorld from './components/HelloWorld.vue'
    exports default {
        componentes: {
            HelloWorld
        }
        methods: {
        	logChildMsg (str) {
              alert (str)
            }
        }
    }
</script>

<template>
  <HelloWorld msg="Hello Vue2" @getChildMsg="logChildMsg" />
</template>
```

而在Vue3中是这样的

```
<script setup>
import { ref, onMounted } from 'vue'
// 组件通信的设置
defineProps({
  fatherMsg: String
})
defineEmits([
  'getChildMsg'
])
const msg = ref('Hello Vue3')
const changeMsg = function () {
	msg.value = 'The msg has been Changed'
}
onMounted (() => {
	msg.value = 'Hello Vue3 (mounted)'
})
// 暴露出去的属性（用于ref获取）
defineExpose({
	msg
});
</script>

<template>
	<h1 @click="$emit('getChildMsg', msg)">{{ msg }}(alert by click)</h1>
	<button @click="changeMsg">Click Me</button>
	<p>{{ fatherMsg }}</p>
</template>
```

父组件

```
<script setup>
import HelloWorld from './components/HelloWorld.vue'
import { ref, onMounted } from 'vue'
// 通过自定义事件获取子组件的值
const logChildMsg = function (str) {
  alert (str)
}
// 通过ref获取子组件的值
const child = ref();
// 不加mounted的话，值还没获取到就打印了
onMounted(()=>{
  console.log('child', child.value.msg);
})
</script>

<template>
  <HelloWorld ref="child" msg="Hello Vue3 (click me)" @getChildMsg="logChildMsg" />
</template>
```



#### 4 TypeScript

```
<script setup lang="ts">

defineProps<{
  msg: string
}>()

</script>
```



#### Vue Router

```
npm install vue-router@4
```



在src下新建router/index.ts，并写入

```
import { createRouter, createWebHashHistory, createWebHistory, RouteRecordRaw } from 'vue-router'
import App from './App.vue'

const routes: Array<RouteRecordRaw> = [
    {
        path: '/',
        component: App
    },

]

const router = createRouter({
    // history: createWebHashHistory(),
    history: createWebHistory(),
    routes
})

export default router
```



在main.ts中写入

```
import { createApp } from 'vue'
import App from './App.vue'
import router from './router'

const app = createApp(App)
app.use(router)
app.mount('#app')
```





```
import { createRouter } from 'vue-router'

router.push('')

<router-view />

<router-link to="">jump to</router-link>
```



#### Vuex

```
npm install vuex@next --save
```



```
yarn add vuex@next --save
```



在src下新建store/index.ts，并写入

```
import { createStore } from 'vuex'

export default createStore({
    state: {
        userName: '张三',
    },
    mutations: {
    },
    actions: {
    },
    modules: {
    }
})
```



在main.ts中写入

```
import { createApp } from 'vue'
import App from './App.vue'
import router from './router'
import store from './store'

const app = createApp(App)
app.use(router)
app.use(store)
app.mount('#app')
```





```
import { useStore } from 'vuex'

const store = useStore()

console.log (store.state.userName)
```



#### 封装自己的对象

在src下新建zh/index.ts，并写入

```
const zh = {
	name: 'zh',
	send(msg: string) {
		console.log (`${zh}: ${msg}`)
	}
}

export default zh;
```



在main.ts中写入

```
import { createApp } from 'vue'
import App from './App.vue'
import router from './router'
import store from './store'
import zh from './zh'

const app = createApp(App)
app.use(router)
app.use(store)
app.mount('#app')

app.config.globalProperties.$zh = zh
```



绑定在vue上下文中

```
import { getCurrentInstance } from 'vue'

const { proxy } = useCurrentInstance();

proxy.$zh.send('hello')
```



绑定在window上

在main.ts中写入

```
window.zh = zh
```



在env.d.ts中写入

```
// 设置Window类中定义zh字段（否则直接window.zh过不了ts的检测）
interface Window  {
  zh: any;
}
```



```
const zh = window.zh
zh.send('hello')
```



#### Axiso

```
import axios from 'axios'

axios
.get(baseUrl + url, { params: json })
.then((res) => {
	yesCall(res.data);
})
.catch((err) => {
    console.log("zh失败:", url, err);
    noCall(err)
});

axios({
    url: baseUrl + url,
    method: 'POST',
    data: json
})
.then((res: any) => {
    let data = res.data
    yesCall(data);
})
.catch((err) => {
    console.log("zh失败:", url, err);
    noCall(err)
});
```



#### Fetch

```
send_f(parms:{url:string, method:string, data:any, success:Function, fail:Function}) {
    let {url, method='POST', data={}, success=()=>{}, fail=()=>{}} = parms
    let body:string | null = JSON.stringify(data)
    if (method == 'GET') {
        body = null
    }
    fetch(baseUrl + url, {
        body, // must match 'Content-Type' header
        method, // *GET, POST, PUT, DELETE, etc.
        mode: 'no-cors',
    })
    .then(response => success(response))
    .catch(err => fail(err));
}
```

