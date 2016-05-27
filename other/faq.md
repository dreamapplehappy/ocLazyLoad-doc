# FAQ

> ### 我按需加载了一个指令,但是在我的页面上没有看到变化

#### 如果这个指令在你延迟加载它的定义之前就已经存在你的`DOM`中的话,你需要告诉`Angular`,它应该解析`DOM`并且重新编译这个新的指令.为了使`Angular`能够那样做到,你需要使用`$compile`服务.
#### *JavaScript*
```javascript
$ocLazyLoad.load('gridModule').then(function() {
  $compile(angular.element('body'))($scope);
});
```
#### 你应该使用[`ocLazyLoad directive`](https://oclazyload.readme.io/v1.0/docs/oclazyload-directive),这个指令就是为了这种情况而写的.

> ### 它能够卸载资源吗

#### 它不能够卸载资源,但是你可以移除`css`通过移除你文件中的`link`标签,大概是下面这个样子:
#### *JavaScript*
```javascript
$('link[href="/url/to/your/file.css"]').remove();
```

> ### 你有一个我能够使用的plnkr并且我能够在上面提问问题吗

#### 当让有,你可以使用这个[http://plnkr.co/edit/n4DG0bbC14Mm1uccBptd?p=preview](http://plnkr.co/edit/n4DG0bbC14Mm1uccBptd?p=preview)

> ### 我如何使用一个我刚刚延时加载的服务

#### 你应该使用`$injector`
#### *JavaScript*
```javascript
var app = angular.module("myApp", ["oc.lazyLoad"]);

app.controller('MyCtrl', function($scope, $ocLazyLoad, $injector) {
    $ocLazyLoad.load('ngDialog.js').then(function() {
        var ngDialog = $injector.get('ngDialog');
        ngDialog.open({
            template: 'dialogTemplate'
        });
    });
});
```

> ### 我能够延时加载所有的`AngularJS`模块吗

#### 当然不可以,虽然你可以延时加载几乎所有的模块,但是一些`原生`的模块是不能够延时加载的.因为他们被高度的集成到`AngularJS`中.下面是一些不能够延时加载的不完整的列表,其中包括:`ngAnimate`, `ngRoute`, `ngSanitizer`, `ngTouch`.(如果你在延时加载别的原生模块中遇到了困难,请告诉我们,以便修改上面那个列表)


















