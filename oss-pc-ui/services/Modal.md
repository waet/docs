# Modal 模态框
$modal只有一个方法：open，该方法的传入一个对象：

## 基础用法
$modal.open 调用后会直接在页面中弹出相应的模态框

template模板
```html
<form class="form-validation">
  <div class="modal-header" style="background-color:#eff8ff;border-radius: 6px;">
    <div class="modal-title" style="position: relative;padding-left: 0;color: #0982df;font-size: 12px;font-weight: bold;">标题
      <a href="" class="right"><i class="glyphicon glyphicon-remove right" ng-click="cancel()" style="position: absolute;top:5px;right: 5px"></i></a>
    </div>
  </div>

  <div class="modal-body form-horizontal">
  </div>

  <div class="modal-footer">
    <div class="center">
      <a href="javascript:;" class="btn btn-sm seleBtn" ng-click="submit()">确 定</a>
      <a href="javascript:;" class="btn btn-default cancelBtn" ng-click="cancel()">关 闭</a>
    </div>
  </div>
</form>
```

```javascript
$scope.fn = function () {
    var params = {} // 需要传到模态框控制器内的参数
    
    $modal.open({
      templateUrl: 'modal.html',
      controller: 'modalCtrl',
      size:'lg',
      resolve: {
        params: function () {
          return params
        },
      }
    }).result.then(function (result) {
      if (result) {
        // on confirm
      }
    }); 
}
```

`modalCtrl` 的代码可单独写个文件，亦可与父控制器写一个文件。（视代码复杂程度而定）

模态框控制器为单独文件的需要把文件路径添加到需要用到的页面的路由配置上，例

```javascript
function ($ocLazyLoad, uiLoad) {
  return uiLoad.load([
      // ...
      'js/controllers/callCenter/modalCtrl.js',
      // ...
  ])
  // ...
}
```

控制器代码，例：

```javascript
app.controller('modalCtrl', ['$scope', '$state', '$conn', '$modalInstance', 'commonService', 'params',
  function ($scope, $state, $conn, $modalInstance, commonService, params) {
  
  // your code
  $scope.submit = function (result) {
    // ...
    $scope.cancel(true)
  }

  // 关闭模态框
  $scope.cancel = function(result){
    $modalInstance.close(result); //关闭页面
  }
}])
```

### [](#Modal-Attributes)Modal Attributes
 参数 | 说明 | 类型 | 默认值 |
 --- | --- | --- | --- |
templateUrl | 模态窗口的地址 | String |  |
scope | 一个作用域为模态的内容使用（$modal会创建一个当前作用域的子作用域） | String | $rootScope |
controller | 模态窗口的地址 | String/Function |  |
size | 窗口大小，可选值为`sm` `lg`  | String | md |
backdrop | 是否在点击遮罩层后关闭模态框 | Boolean | true |
keyboard | 当按下Esc时，模态框是否关闭 | Boolean | true |
resolve | 定义一个成员并将他传递给$modal指定的控制器 | Object |  |
windowClass | 指定一个class并被添加到模态窗口中 | String |  |




