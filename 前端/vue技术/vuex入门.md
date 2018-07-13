如果想要将vue后台的数据给给个组件使用，vuex 官方文档https://vuex.vuejs.org/zh/

Vuex 是一个专为 Vue.js 应用程序开发的**状态管理模式**。它采用集中式存储管理应用的所有组件的状态，并以相应的规则保证状态以一种可预测的方式发生变化。

## 一、安装vuex（进入新建项目的文件夹，安装vuex）

```
sudo npm install vuex --save -dev
```

## 二、建立目录结构（官方项目结构目录）

```
 store
    ├── store.js          # 我们组装模块入口并导出 store 的地方
    ├── actions.js        # 根级别的 action,存放异步读取修改常量数据的方法
    ├── mutations.js      # 根级别的 mutation，存放同步读取修改常量数据的方法
    ├── data.js           # 全局数据存放的地方
    └── modules//文件夹
        
```

三、