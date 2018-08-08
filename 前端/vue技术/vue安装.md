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
sudo vue init webpack my-project
sudo vue init webpack-simple my-project

//my-project是你的项目名
//webpack-simple为构建精简的webpack项目
```

```
不应用ESLint
创建webpack模板项目时，如果你对ES6和ESLint不是很熟的话我个人不建议你应用它
因为要求比较严格，所以一不小心就报错，导致整个项目运行不起来，对于初学很痛苦。 可以参考以下进行选择
```

    ? Project name test
    ? Project description A Vue.js project
    ? Author test
    ? Vue build standalone
    ? Install vue-router? Yes
    ? Use ESLint to lint your code? No
    ? Set up unit tests Yes
    ? Pick a test runner jest
    ? Setup e2e tests with Nightwatch? Yes
    ? Should we run `npm install` for you after the project has been created? (recommended) npm

#### 安装依赖

```
 cd my-project 
  //到项目目录下
 npm install 
 //安装依赖,不要用cnpm安装，否则会丢失很多库
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



