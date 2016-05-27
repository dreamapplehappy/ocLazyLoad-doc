# 配合路由
#### `$ocLazyLoad`能够和路由很好的结合使用,尤其是`ui-router`.因为它返回一个`promise`,
#### 我们使用angular的`resolve`属性确保我们的组件是在我们的视图被`resolved`之前加载的.

#### *JavaScript*
```javascript
$stateProvider.state('index', {
  url: "/", // root route
  views: {
    "lazyLoadView": {
      controller: 'AppCtrl', // This view will use AppCtrl loaded below in the resolve
      templateUrl: 'partials/main.html'
    }
  },
  resolve: { // Any property in resolve should return a promise and is executed before the view is loaded
    loadMyCtrl: ['$ocLazyLoad', function($ocLazyLoad) {
      // you can lazy load files for an existing module
             return $ocLazyLoad.load('js/AppCtrl.js');
    }]
  }
});
```
#### 如果你是在嵌套的路由中使用,那么需要注意的是:你需要在父路由中包含`resolve`属性,并且按照顺序去加载你的子路由需要的组件,

#### *JavaScript*
```javascript
$stateProvider.state('parent', {
  url: "/",
  resolve: {
    loadMyService: ['$ocLazyLoad', function($ocLazyLoad) {
             return $ocLazyLoad.load('js/ServiceTest.js');
    }]
  }
})
.state('parent.child', {
    resolve: {
        test: ['loadMyService', '$ServiceTest', function(loadMyService, $ServiceTest) {
            // you can use your service
            $ServiceTest.doSomething();
        }]
    }
});
```

#### 当然相邻的`resolves`也是可以使用这种方式的,不过注意顺序.

#### *JavaScript*
```javascript
$stateProvider.state('index', {
  url: "/",
  resolve: {
    loadMyService: ['$ocLazyLoad', function($ocLazyLoad) {
             return $ocLazyLoad.load('js/ServiceTest.js');
    }],
        test: ['loadMyService', '$serviceTest', function(loadMyService, $serviceTest) {
            // you can use your service
            $serviceTest.doSomething();
        }]
    }
});
```

#### 当然,如果你想立即使用这些加载的文件,你不需要去定义两个`resolves`,你也可以使用`injector`(注入器)去获取这些加载的文件中的这些服务(*这种方法可以在任何一种情况下工作,不仅仅是在路由中*)

#### *JavaScript*
```javascript
$stateProvider.state('index', {
  url: "/",
  resolve: {
    loadMyService: ['$ocLazyLoad', '$injector', function($ocLazyLoad, $injector) {
      return $ocLazyLoad.load('js/ServiceTest.js').then(function() {
        var $serviceTest = $injector.get("$serviceTest");
        $serviceTest.doSomething();
      });
    }]
  }
});
```




















