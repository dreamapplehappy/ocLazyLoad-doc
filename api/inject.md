# 依赖注入

#### 为了方便起见,你也可以在模块的依赖注入部分里加载这些依赖,当然你要定义好你需要加载的这些模块;记住这种方法只对那些需要延时加载的模块起作用.

#### *JavaScript*
```javascript
angular.module('MyModule', ['pascalprecht.translate', {
    files: [
        '/components/TestModule/TestModule.js',
        '/components/bootstrap/css/bootstrap.css',
        '/components/bootstrap/js/bootstrap.js'
    ],
    cache: false
}]);
```
#### 或者你也可以使用更简单方式(*如果你不需要一些额外的参数的话*)
#### *JavaScript*
```javascript
angular.module('MyModule', ['pascalprecht.translate', [
  '/components/TestModule/TestModule.js',
  '/components/bootstrap/css/bootstrap.css',
  '/components/bootstrap/js/bootstrap.js'
]]);
```
