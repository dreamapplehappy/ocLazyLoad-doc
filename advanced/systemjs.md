# SystemJS
#### *这篇文档还在进行中,很快将会被完善*

## 简短示例
#### 结合使用`SystemJS`和`ocLazyLoad`的最简单的方式就是使用`System.import`API:
#### *JavaScript*
```javascript
import {coreStates} from 'js/core/states/app'

// Optionally, return to wherever this promise chain might be useful
System.import('js/core/states/app').then(function(m) {
  return $ocLazyLoad.load(m.coreStates);
}).then(function() {
  return Startup.awake();
})
```
#### `coreStates`看起来也许是下面这样的:
#### *JavaScript*
```javascript
export var coreStates = angular.module( 'core.states');
```
## 详细示例
#### 我们需要延时加载的那些模块看起来也许是下面这个样子.
#### *JavaScript*
```javascript
var secondModule = angular.module('secondModule', []);

secondModule.run(function () {
  console.log('secondModule::run');
});

export default secondModule;
```
#### 在上面的例子中我们把需要导出的模块作为了默认模块导出;这样的话一旦我们加载了这个模块,这个模块就会马上起作用.
#### *thirdModule.js*
```javascript
var thirdModule = angular.module('thirdModule', []);

thirdModule.run(function () {
  console.log('thirdModule::run');
});

export { thirdModule };
```
#### 在上面我们定义了另一个模块,但是没有作为默认模块导出;当然一旦我们加载了这个模块,它也会马上起作用.
#### *loaderModule.js*
```javascript
function lazySystem ($ocLazyLoad) {
  function load (src, key) {
    return System.import(src).then(function (loadedFile) {
      return $ocLazyLoad.load(loadedFile[key || 'default']);
    });
  }
  
  this.load = load;
}

var loaderModule = angular
  .module('loaderModule', ['oc.lazyLoad'])
  .service('lazySystem', lazySystem);

export { loaderModule };
```
#### `lazySystem`服务是一个封装的模块,它托管了我们的`.load`方法.运行`System.import`并且传入参数(你需要加载的文件路径),然后把这个结果返还给`$ocLazyLoad.load()`.
#### 通过给`.load`方法传递一个键值我们可以从已经加载的文件中获取一个指定的模块,如果没有指定键值的话,我们可以得到默认被导出的模块.
#### `$ocLazyLoad`将会把这个我们需要的模块作为一个`promise`返回.

#### *example.js*
```javascript
import { loaderModule } from './loaderModule'; 

var app = angular.module('app', [ loaderModule.name ]);

app.run(function (lazySystem) {
  lazySystem.load('./secondModule').then(function (loadedModule) {
    console.log(loadedModule);
  });

  lazySystem.load('./thirdModule', 'thirdModule').then(function (loadedModule) {
    console.log(loadedModule);
  });
});
```

#### 在我们的入口文件,(那个包含我们应用核心基础的文件),导出上面哪个`loaderModule`,在`run`表达式中,加载我们的第二个模块和第三个模块,我们可以看到它们各自的打印的结果.























