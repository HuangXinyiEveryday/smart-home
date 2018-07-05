# 基于vue的项目构建

## 一、前期准备

#### 安装vue前，安装阿里源，加快下载速度

```
npm install -g cnpm --registry=https://registry.npm.taobao.org
```

集中不同方式安装vue，Vue.js 提供一个官方命令行工具，可用于快速搭建大型单页应用。因此我们一般选择第二种方式进行安装，第一种供前期学习了解，项目开发使用第二种方式

#### 1.安装vue2.0

```
sudo cnpm intall vue
```

#### 2.安装vue-cli脚手架工具（项目使用）

```
sudo cnpm install --global vue-cli
```

## 二、新增项目

#### 在某个目录下，创建一个基于webpack模板的新项目

```
vue init webpack my-project
vue init webpack-simple my-project
//my-project是你的项目名
//webpack-simple为构建精简的webpack项目
```

```
不应用ESLint
创建webpack模板项目时，如果你对ES6和ESLint不是很熟的话我个人不建议你应用它，因为要求比较严格，所以一不小心就报错，导致整个项目运行不起来，对于初学很痛苦。 可以参考以下进行选择
```

```bash
? Project name test
? Project description A Vue.js project
? Author test
? Vue build standalone
? Install vue-router? Yes
? Use ESLint to lint your code? No
? Set up unit tests Yes
? Pick a test runner jest
? Setup e2e tests with Nightwatch? Yes
? Should we run `npm install` for you after the project has been created? (recom
mended) npm
```

#### 安装依赖

```
 cd my-project        //到项目目录下
 npm install     //安装依赖,不要用cnpm安装，否则会丢失很多库
```

#### 运行新创建的vue项目

```
npm run dev
```

## 三、为项目新增vue-router依赖

1.进入第二步创建的项目文件，使用npm下载安装vue-router

```
cnpm install vue-router  --save  
//如果需要resource
cnpm install vue-router vue-resource --save
//（--save ：安装后放在package.json 的dependencies，这样方便我们查看等）
cnpm install vue-router@0.7.13  --save
//使用@指定router版本
```

```
//打开项目的package.json，如下存在vue-router，表示安装依赖成功
"dependencies": {
    "vue": "^2.5.2",
    "vue-router": "^3.0.1"
  },
```

2.测试一下，页面localhost:8080测试

```
npm run dev
```

# 四、使用Vue组件

新增单独的vue组件，类似html新增一个页面功能

### 1.一般在src/components文件夹下，存放vue组件信息

新增一个vue文件

<template></template>相当于html的html页面

<script></script>相当于js脚本

<style></style>相当于css样式

```vue
<template>
  <div id="first">
    <h1>标题</h1>
    <a>作者：{{ author}}</a>
  </div>
</template>

<script type="text/javascript">
export default{
  data(){
    return{
      author:"hxy"
    }
  }
}
</script>
<style>
</style>
```

### 2.修改App.vue(类似html的统一入口)

```vue
<template>
  <div id="app">
    <img src="./assets/logo.png">
    <first/>//自己新增的vue，在脚本中impor导入
  </div>
</template>

<script>
import first from './components/first.vue'
export default {
  name: 'App',
  data(){
    return {
    　　　　　　msg: 'Welcome to Your Vue.js App'
    　　　　}
  },
  components: {
    first
  }
}
</script>
```

这样就可以执行一个自己写的first网站了

# 五、使用vue-router

```
cnpm install vue-router --save
```

​	--save 可以理解成生产环境，会把依赖包名称添加到 package.json 文件 dependencies 键下，dependencies是运行时依赖。

　　--save-dev 则是开发环境， 添加到 package.json 文件 devDependencies 键下，devDependencies是开发时的依赖，如生产时不需要用到压缩库应该安装到devDependencies 。

### 1.在src目录下新增views文件夹

新增gps、mattress、doorcontact三个vue文件，其中举例：mattress.vue

```vue
<template>
    <div >
        <h1>床垫数据获取演示</h1>
        <a> 床垫数据获取演示 </a>
    </div>
</template>

<script type="text/javascript">
    export default {
        name: 'mattress',
    }
</script>
<style>
</style>
```

### 2.在src目录下新增router.js文件

```js
import Vue from 'vue'
import Router from 'vue-router'
//引入子组件到路由
import doorcontact from './views/doorcontact.vue'
import gps from './views/gps.vue'
import mattress from './views/mattress.vue'

Vue.config.productionTip = false
Vue.use(Router)
const router=new Router({
    // 路由配置
    routes: [
    {
      //路径url
        path: '/doorcontact',
        component: doorcontact
    }, {
        path: '/gps',
        component: gps
    }, {
        path: '/mattress',
        component: mattress
    }
    ]
})
export default router;

```

### 3.使用router，修改src下的main.js，引入router并指定当前vue实例

```js
// The Vue build version to load with the `import` command
// (runtime-only or standalone) has been set in webpack.base.conf with an alias.
import Vue from 'vue'
import App from './App'
import router from './router.js'

new Vue({
    el:'#app',
    router,
    render: h => h(App)
})

```

### 4.**添加路由链接和出口。**修改App.vue<template>添加链接和出口。

```vue
<template>
  <div id="app">
    <img src="./assets/logo.png">
    <first/>
    <div>
      <router-link to="/gps">gps数据获取演示</router-link>
      <br>
      <router-link to="/mattress">床垫数据获取演示</router-link>
      <br>
      <router-link to="/doorcontact">门磁数据获取演示 </router-link>
      <br>
    </div>
    <!-- 路由出口 -->
    <!-- 路由匹配到的组件将渲染在这里 -->
    <router-view></router-view>
  </div>
</template>
```

注意：vue里面只能有一个大的div，所有div都只能在大的div里面，不能并列

router-link是router路由

router-view渲染路由的视图

# 六、添加ajax请求（使用axios插件）

### 1.安装axios，通过cd进入项目工程目录

```
sudo npm instal axios
```

### 2.在main.js中引入axios，将vue组件的原型改成axios，添加如下代码

```
import axios from 'axios'
Vue.prototype.$http = axios/Vue.prototype.$ajax=axios
```

### 3.在组件中使用ajax方法

在main.js添加后，可以直接在组件的methods中使用$http/ajax命令，以床垫mattress.vue为例

```

```

