# 配置

### 可以在你angular应用的`config`函数中通过`$ocLazyLoadProvider`来配置这个服务.
#### *javascript*
```javascript
angular.module('app', ['oc.lazyLoad'])
  .config(['$ocLazyLoadProvider', function($ocLazyLoadProvider) {
      $ocLazyLoadProvider.config({
        // ...
      });
}]);
```
### 配置的选项如下:

| 参数名        | 类型          | 默认值  |
| ------------- |:-------------:| -----:|
| `debug`      | **Boolean** | **false** |
| `events`      | **Boolean**      |   **false** |
| `modules` | **Array of Objects(对象数组)**      |    **undefined** |

+ ### `debug`: 当出现错误的时候,`$ocLazyLoad`返回的`promise`将会被`rejected`;如果你将这个参数设置为`true`,`$ocLazyLoad`会将这些错误打印在控制台上.
  #### *javascript*
  ```javascript
  $ocLazyLoadProvider.config({
    debug: true
  });
  ```
+ ### `events`: 当你加载一个模块,一个组件,或者是一个文件(js/css/template)的时候;`$ocLazyLoad`能够广播一个事件,将这个选项设置为`true`去激活它.这些事件分别是`ocLazyLoad.moduleLoaded`, `ocLazyLoad.moduleReloaded`, `ocLazyLoad.componentLoaded`, `ocLazyLoad.fileLoaded`.
  #### *javascript*
  ```javascript
  $ocLazyLoadProvider.config({
    events: true
  });
  ```
  #### *javascript*
  ```javascript
  $scope.$on('ocLazyLoad.moduleLoaded', function(e, module) {
    console.log('module loaded', module);
  });
  ```
+ ### `modules`: 为以后的使用预先定义你的模块配置,你必须在这里定义你的模块名字,以便我们稍后能够通过索引找到它.
  ### *javascript*
  ```javascript
  $ocLazyLoadProvider.config({
    modules: [{
      name: 'TestModule',
      files: ['js/TestModule.js']
    }]
  });
  ```
  ### *javascript*
  ```javascript
  $ocLazyLoad.load('TestModule'); // will load the predefined configuration
  ```  
  