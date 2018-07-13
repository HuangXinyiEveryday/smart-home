# 一、使用Vue组件

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

# 二、使用vue-router

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

### 2.在src目录下新增routes文件夹，新增router.js文件

```js
import Vue from 'vue'
import Router from 'vue-router'
//引入子组件到路由
import doorcontact from '../views/doorcontact.vue'
import gps from '../views/gps.vue'
import mattress from '../views/mattress.vue'

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
import router from './routes/router.js'

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

# 三、添加ajax请求（使用axios插件）

vue使用router-link，进行页面路由时，axios请求不是在子组件执行，而是在父组件加载完毕后就执行了所有axios请求并获得结果。

因为app.vue父组件使用router-link，相当于包含组件，引入模块的用途，所以需要在使用时，灵活使用。

### 1.安装axios

通过cd进入项目工程目录

```
sudo npm instal axios
```

### 2.新增axiosConfig.js

在src文件夹下新增axios文件夹，在该文件下新增文件进行ajax的公共配置

```js
/**
 * ajax请求配置
 */
import axios from 'axios'
/**
 * axios实例化默认配置
 */
const Axios = axios.create({
   timeout: 10000,               // 请求超时时间
})

// 添加请求拦截器
Axios.interceptors.request.use(function (config) {
    // 在发送请求之前做些什么
    return config;
  }, function (error) {
    // 对请求错误做些什么
    return Promise.reject(error);
  });

// 添加响应拦截器
Axios.interceptors.response.use(function (response) {
    // 对响应数据做点什么
    return response;
}, function (error) {
    // 对响应错误做点什么
    return Promise.reject(error);
});
 // 最后暴露实例
export default Axios
```

### 3.允许前端跨域

在config文件夹下index.js文件，修改proxyTable

```js
  proxyTable: {
      '/api': {
      target: 'http://192.168.85.208:9000/',//设置你调用的接口域名和端口号
      changeOrigin: true,     //跨域
      pathRewrite: {
        '^/api': '/'          //这里理解成用‘/api’代替target里面的地址，后面组件中我们掉接口时直接用api代替 比如我要调用'http://192.168.95.208:9000/xxx/duty?time=2017-07-07 14:57:22'，直接写‘/api/xxx/duty?time=2017-07-07 14:57:22’即可
      }
```

### 4.axios中response返回结构

### 5.在组件中使用ajax方法

可以直接在vue组件中methods中使用ajax方法

```
//引入配置的axios文件
import ajax from '../axios/axiosConfig.js'
    export default {
        name: 'gps',
}
ajax({
//api为第三步config中index.js跨域设置的api，只有使用该api才可以进行跨域访问
  url:'/api/gps-server/DeviceGps/191',
  method:'GET',
  params:{access_token:'7fb76b82-45d4-4d0f-b35d-aab08591eee7'}
}).then(function(response){
//返回结果
var  tmp=response.data.data;
  alert(tmp.id);
});
```

注：因为response返回数据结构为data接收后端返回数据，后端返回中结构参见前后端接口url，所以需要response.data.data才能找到最终后端返回的数据

```
//返回数据结构
{
  "code": 0,
  "data": {
    "id": 0,
    "latitude": "string",
    "longitude": "string"
  },
  "msg": "成功"
}
```

