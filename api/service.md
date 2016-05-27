# 服务
### 内容列表
+ #### Load方法
+ #### 使用配置选项
+ #### 参数列表
+ #### 附加方法

### # Load方法
#### `$ocLazyLoad`服务的`load`方法返回一个`promise`,它支持单个或者多个文件作为依赖进行加载.
#### 通过一个文件加载一个或者多个模块或者组件:
#### *javaScript*
```javascript
$ocLazyLoad.load('testModule.js');
```
#### 通过多个文件加载一个或者多个模块或者组件:
#### *javaScript*
```javascript
$ocLazyLoad.load(['testModule.js', 'testModuleCtrl.js', 'testModuleService.js']);
```
#### 当通过多个文件加载一个模块或者多个模块时,在必要的情况下需要指定加载文件的类型:
#### *注意: 当加载类似`requireJS`格式的文件时(例如,使用`js!`作为开头,),不要指定文件的扩展名.*你可以选择其中的一种.
#### *javaScript*
```javascript
$ocLazyLoad.load([
   'testModule.js',
   {type: 'css', path: 'testModuleCtrl'},
   {type: 'html', path: 'testModuleCtrl.html'},
   {type: 'js', path: 'testModuleCtrl'},
   'js!testModuleService',
   'less!testModuleLessFile'
]);
```
#### 当然你也可以加载外部的文件库(不仅仅是`angular`的)
#### *javaScript*
```javascript
$ocLazyLoad.load([
    'testModule.js', 
    'bower_components/bootstrap/dist/js/bootstrap.js', 
    'anotherModule.js'
]);
```
#### 如果你想加载模板,也是可以的;不过这个模板文件应该是`angular`可以识别的模板.它应该是下面这个样子:
#### *HTML*
```html
<script type="text/ng-template" id="partials/template1.html">
  Content of the template.
</script>
```
#### 你当然也可以在一个模板文件中放置不同的模板,但是要确保它们分别使用不同的`id`.
#### *HTML*
```html
<script type="text/ng-template" id="partials/template1.html">
  Content of the first template.
</script>

<script type="text/ng-template" id="partials/template2.html">
  Content of the second template.
</script>
```

### # 使用配置选项
#### 有两种方式为`load`函数去定义我们的配置选项,你可以通过使用`load`函数的第二个可选参数,为我们加载的所有的模块定义配置.当然你也可以为每一个加载的模块定义配置.
#### 例如,下面的两个是等价的(**除了第一个例子中的前两个文件不会被缓存外**)

#### *JavaScript*
```javascript
$ocLazyLoad.load([{
  files: ['testModule.js', 'bower_components/bootstrap/dist/js/bootstrap.js'],
  cache: false
},{
  files: ['anotherModule.js'],
  cache: true
}]);
```
#### 和
#### *JavaScript*
```javascript
$ocLazyLoad.load(
  ['testModule.js', 'bower_components/bootstrap/dist/js/bootstrap.js', 'anotherModule.js'],
  {cache: false}
);
```
#### 如果你使用原生的模板加载器加载一个模板,你可以使用来自`$http`服务的任何参数
#### (查看: [https://docs.angularjs.org/api/ng/service/$http#usage](https://docs.angularjs.org/api/ng/service/$http#usage))
#### *JavaScript*
```javascript
$ocLazyLoad.load(
  ['partials/template1.html', 'partials/template2.html'],
  {cache: false, timeout: 5000}
);
```

### # 参数列表
#### 下面是你可以使用的一些参数
| 参数名        | 类型          | 默认值  |
| ------------- |:-------------:| -----:|
| `cache`      | **Boolean** | **true** |
| `reconfig`      | **Boolean**      |   **false** |
| `rerun`      | **Boolean**      |   **false** |
| `serie`      | **Boolean**      |   **false** |
| `insertBefore` | **Boolean**      |    **undefined** |

#### 参数`cache: false`适用于所有的原生加载器(**浏览器默认所有的请求都被缓存了**).如果你使用它,加载器会在路径的后面追加一个时间戳以便绕过浏览器的缓存.
#### *JavaScript*
```javascript
$ocLazyLoad.load({
  cache: false,
  files: ['testModule.js', 'bower_components/bootstrap/dist/js/bootstrap.js']
});
```

#### 在默认情况下,如果你重新加载一个模块,以前的配置模块不会被重新调用(因为如果重新调用配置模块可能会导致一些意外).但是如果你确实需要再一次重新执行哪个配置函数的话,使用参数`reconfig: true`.
#### *JavaScript*
```javascript
$ocLazyLoad.load({
  reconfig: true,
  files: ['testModule.js', 'bower_components/bootstrap/dist/js/bootstrap.js']
});
```

#### 同样的情况也许会发生在`run`代码块,使用`rerun: true`重新运行`run`代码块:
#### *JavaScript*
```javascript
$ocLazyLoad.load({
  rerun: true,
  files: ['testModule.js', 'bower_components/bootstrap/dist/js/bootstrap.js']
});
```

#### 默认情况下,原生的加载器会同时平行的加载你的那些文件,如果你需要按顺序加载你的文件,你可以使用参数`serie: true`:
#### *JavaScript*
```javascript
$ocLazyLoad.load({
  serie: true,
  files: [
    'bower_components/angular-strap/dist/angular-strap.js',
    'bower_components/angular-strap/dist/angular-strap.tpl.js'
  ]
});
```
#### 那些延时加载的文件,在默认情况下会被插入到`head`元素的最后一个子节点之前.你当然可以重写这个选项通过使用`insertBefore: 'cssSelector'`(这个*cssSelector*在默认情况下使用的是`document.querySelector`,如果可以使用`jQuery`的话,那么它使用的就是`jQuery`的选择器)
#### *JavaScript*
```javascript
$ocLazyLoad.load({
  insertBefore: '#load_css_before',
  files: ['bower_components/bootstrap/dist/css/bootstrap.css']
});
```
### # 附加方法
#### `$ocLazyLoad`提供了一些额外的方法可能会在一些特殊的情况下帮到你
+ #### `setModuleConfig(moduleConfig)`: 让你定义一个模块的配置对象
+ #### `getModuleConfig(moduleName)`: 获取一个模块的配置对象
+ #### `getModules()`: 返回已经加载的模块的列表
+ #### `isLoaded('moduleName' or [modulesNames])`: 检查一个模块或者一个模块列表是否已经加载到`Angular`.
+ #### `inject('moduleName' or [modulesNames])`: 如果你使用`RequireJS`,`SystemJS`或者其他的,你可以是手动的注入这些加载的模块,但是你需要提供这些正在被加载的模块的名字(除非你在加载这些文件之前或者之后使用了`toggleWatch`)
+ #### `toggleWatch(boolean)`: 让`ocLazyLoad`知道它应该监测`angular.module`以便加载了新的模块.这个方法只在你自己使用`inject`方法时有用.别忘了在使用之后关闭这个方法,应为它会导致意想不到的结果.
