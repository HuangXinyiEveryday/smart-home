## 一、封装统一网关，跨域请求

### config/index.js

```js
  proxyTable: {
      '/api': {
      target: 'http://192.168.85.208:9000',//设置你调用的接口域名和端口号
      changeOrigin: true,     //跨域
      pathRewrite: {
        '^/api': '/'          //这里理解成用‘/api’代替target里面的地址，后面组件中我们掉接口时直接用api代替 比如我要调用'http://192.168.85.208:9000/xxx/duty?time=2017-07-07 14:57:22'，直接写‘/api/xxx/duty?time=2017-07-07 14:57:22’即可
      }
    }
  }
```

在配置中的target里面设置统一调用后台的服务器和端口

## 二、进行ajax基本配置

### src/axios/axiosConfig.js

```js
import axios from 'axios'
/**
 * axios实例化默认配置
 */
const Axios = axios.create({
   timeout: 10000,  // 请求超时时间
   baseURL:'/api',//访问的后端服务器url，调用跨域config中index的api
   params:{
     access_token:'1f4ae0b4-7a13-40de-85e0-160caa70e06b'
   }
})
```

创建新的axios实例（也可以直接进行默认配置），请求超时时间，默认的url，参数中配置基本的access_token等基本信息

，其他基本配置参考中文文档。

## 三、基本api模块封装

### src/axios/getToken.js

```
公共js访问后台获取token值，别的vue或js需要调用，只需要import即可
```

```js
import axios from 'axios'


/**
 * axios实例化,进行获取token
 */
const AxiosToken = axios.create({
   timeout: 10000,  // 请求超时时间
   baseURL:'/api',//访问的后端服务器url，调用跨域config中index的api
   params:{
     username:'hxy123',
     password:'111111',
     grant_type:'password'
   },
   headers:{
    'Content-Type':'application/json',
    'Authorization':'Basic YW5kcm9pZDphbmRyb2lk'
  },

})

//使用获取token的axios方法
AxiosToken({
  url:'/auth-server/oauth/token',
  method:'POST',
}).then(function(response){
token=response.data.access_token;
console.log(token);
});
```

此时得到的token只能在then内部使用，无法供其他组件使用，需要使用vuex+store进行组件通信

### src/axios/gpsUrl.js

```js
//配置gps相关url
const gpsUrl='/gps-server'
const id=191
/*
gps相关url
 */
//DeviceGps查询gps位置信息
const getGps=gpsUrl+'/DeviceGps/'+id
const getAll=gpsUrl+'/all/'
//提供外部访问接口
export {
 getGps,
 getAll
};

```

相关模块，定义相关模块的Url的基本模块，将url在该模块进行配置，通过export提供外部访问接口

## 四、基本组件调用

### src/views/gps.vue

```vue
<template>
    <div >
        <h1>gps数据获取演示</h1>
        <a> gps数据获取演示 </a>
    </div>
</template>

<script type="text/javascript">
//引入axiosConfig的文件
//导入js模块，import *表示将所有都引入，并重命名为gpsUrl    
import * as gpsUrl from '../axios/gpsUrl.js'
//导入公共配置    
import axios from '../axios/axiosConfig.js'

export default {
        name: 'gps'
}
axios({
    //使用gpsUrl的getGps常量作为url，和axiosConfig中的baseUrl进行拼接
  url:gpsUrl.getGps,
    //使用get方法，param使用axiosConifg的参数传递
  method:'GET',
}).then(function(response){
    //返回的结果
var  tmp=response.data.data;
console.log(tmp.id);
});
</script>
<style>
</style>
```

