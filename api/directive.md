# 指令

#### 指令的使用方法和服务是很相似的.但是值得注意的地方是,只有当你的那些需要加载的模块加载完成之后,指令里面的内容才会被加载并且编译.
#### 这意味着你可以在`oc-lazy-load`指令中使用指令,这些指令是延时加载的(`lazy loaded`).
#### 使用和服务中相同的参数

#### *HTML*
```html
<div oc-lazy-load="['js/testModule.js', 'partials/lazyLoadTemplate.html']">
  <!-- Use a directive from TestModule -->
  <test-directive></test-directive>
</div>
```
#### 你也可以使用变量存储参数
####  *JavaScript*
```javascript
$scope.lazyLoadParams = [
  'js/testModule.js',
  'partials/lazyLoadTemplate.html'
];
```
#### *HTML*
```html
<div oc-lazy-load="lazyLoadParams"></div>
```
