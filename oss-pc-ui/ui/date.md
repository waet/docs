## 日期选择器

   [日历控件文档](http://www.jemui.com/uidoc/jedate.html#core) 

```html
<input type="text" class="workinput wicon inpstart" ng-model="query.dateStart" readonly />
```

```javascript
var app = angular.module('myApp', []);
app.controller('myCtrl',[ '$scope','commonService',function($scope,commonService) {
    $scope.query={
        dateStart:commonService.formatDate().date//当天
    }
    //S 日期控件
    var start = {
        isinitVal: true,
        format: 'YYYY-MM-DD',
        festival: true,
        ishmsVal: false,
        choosefun: function(elem, val, date) {
            elem.val(date).trigger('change');
        }
    }
    $('.inpstart').jeDate(start);
  
}]);
```

