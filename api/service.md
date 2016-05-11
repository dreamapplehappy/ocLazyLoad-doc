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
#### 你当然也可以在一个模板文件中

