# Select 选择器

当选项过多时，使用下拉菜单展示并选择内容。

AngularJS 可以使用数组或对象创建一个下拉列表选项。

## 基本用法

### 使用 ng-options 创建选择框
```html
<select ng-init="selectedName = names[0]" ng-model="selectedName" ng-options="x for x in names"></select>
   <!-- ng-init 设置默认选中值 -->
   
<script>
var app = angular.module('myApp', []);
app.controller('myCtrl', function($scope) {
    $scope.names = ["Google", "Runoob", "Taobao"];
});
</script>
```

### ng-options 与 ng-repeat
```html
<select ng-model="selectedName">
    <option ng-selected="selectedName = names[0]" ng-repeat="x in names">{{x}}</option>
</select>
```
> ng-repeat 指令是通过数组来循环 HTML 代码来创建下拉列表，但 ng-options 指令更适合创建下拉列表，它有以下优势：
> 使用 ng-options 的选项可以是一个`对象`和`字符串`， ng-repeat 只能是一个`字符串`。

所以我们应该

### 尽量使用`ng-options`

```html
<select ng-model="selectedSite" ng-options="x.site for x in sites">
</select>

<h1>你选择的是: {{selectedSite.site}}</h1>
<p>网址为: {{selectedSite.url}}</p>

<select ng-model="selectedSiteUrl" ng-options="x.url as x.site for x in sites">
</select>

<p>你选择的网址为: {{selectedSiteUrl}}</p>

<script>
var app = angular.module('myApp', []);
app.controller('myCtrl', function($scope) {
   $scope.sites = [
	    {site : "Google", url : "http://www.google.com"},
	    {site : "Runoob", url : "http://www.runoob.com"},
	    {site : "Taobao", url : "http://www.taobao.com"}
	];
});
</script>
```

## optgroup 标签
通过 `optgroup` 标签把相关的选项组合在一起
```html
<select ng-model="selectedName" ng-options="value.id as value.ch group by value.group for value in data">
  <option value="">==全部==</option>
</select>
绑定的ID： {{selectedName}}

<script>
var app = angular.module('myApp', []);
app.controller('myCtrl', function($scope) {
    $scope.data = [
	    { group: '水果', ch: '苹果', id: '1' }, 
	    { group: '水果', ch: '香蕉', id: '2' },
	    { group: '饮料', ch: '可乐', id: '3' }, 
	    { group: '饮料', ch: '橙汁', id: '4' }
    ];
});
</script>
```
> 只能应用于一维数组，已分好类数组还是`ng-reapet`


