# Input 输入框
通过鼠标或键盘输入字符

> Input 为受控组件，它总会显示 angular 绑定值。
> 
> 通常情况下，应当处理 `input` 事件，并更新scope的绑定值。否则，输入框内显示的值将不会改变。
> 

## 基础用法

```html
<input type="text" class="form-control" ng-model="value" />

<script>
var app = angular.module('myApp', []);
app.controller('myCtrl', function($scope) {
    $scope.value = '';
});
</script>
```

## 可清空
使用`cancel`属性即可得到一个可清空的输入框
```html
<input type="text" class="form-control" cancel ng-model="value" />
{{ value }}
<script>
var app = angular.module('myApp', []);
app.controller('myCtrl', function($scope) {
    $scope.value = '';
});
</script>
```
`cancel`还可接受对象，清空对象里的可枚举值  
`cancel1 - 9`用于联动清除其它数据
```html
<input type="text" class="form-control" 
    cancel="user" 
    cancel1="sex" 
    cancel2="room"
    ng-model="user.name" />

<h1>{{ user.name }}的ID为{{ user.id }}</h1>
<p>性别为: {{sex}}</p>
<p>所在房间: {{room}}</p>

<script>
var app = angular.module('myApp', []);
app.controller('myCtrl', function($scope) {
    $scope.user = {
        id: '001'
        name: 'Lee Chao'
    };
    $scope.sex = '男'
    $scope.room = 'three room'
});
</script>
```

### [](#Input-Attributes)Input Attributes
 参数 | 说明 | 类型 | 默认值 |
 --- | --- | --- | --- |
cancel | 可传Scope上的对象或字符串（不传默认清除ng-model上绑定的值） | Scope |  |
cancel1 - 9 | 只可传Scope上的字符串 | String |


> [常见正则规则](https://www.cnblogs.com/myzhibie/p/4365142.html)

### TODO LIST
- `date` input标签添加此属性即可使用日期控件

