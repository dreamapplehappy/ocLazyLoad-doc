# 快速入门
### 1.下载`ocLazyLoad.js`,我们可以在它[git仓库](https://github.com/ocombe/ocLazyLoad)的`dist`目录中找到它.当然我们也可以通过下面两种方式去安装它:
+ #### `bower install oclazyload`
+ #### `npm install oclazyload`

### 2.将`oc.lazyLoad`添加到你的应用中去
#### *将这个模块添加到你的应用中*
```javascript
var myApp = angular.module("MyApp", ["oc.lazyLoad"]);
```
### 3.延时加载
#### *加载模块的基本示例*
```javascript
myApp.controller("MyCtrl", function($ocLazyLoad) {
  $ocLazyLoad.load('testModule.js');
});
```

### 通过使用`$ocLazyLoad`你可以延时加载你的模块;不过,如果你想加载任何组件(控制器,服务,过滤器,等等)但是却不想定义一个模块,通过使用`$ocLazyLoad`也是完全可以做到的.(**不过需要注意的是,你要确保你加载的这些组件是存在于一个已有的模块中**)
### 通过`$ocLazyLoad`有很多种方式去加载你的文件,选择你喜欢的一种方式去使用吧.
### 不过别忘记了,如果你要开始使用的话,这些文档是不足够的,在`examples`目录里去看那些示例吧.