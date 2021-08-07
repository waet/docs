# 控制器

- app.controller 生成控制器
  - 入参 （name,array）
  - 'test' 控制器名称 不可重复并且与对应模板（html 页面）保持一致
  - [$scope,functio($scope){ }]
    - $scope Object 当前页面作用域
    - fn 功能实现
- `callback`: noop, //回调函数，

```javascript
    app.controller('test',['$scope','$conn',function($scope,$conn){
        $scope.obj={
            name:'张三'，
            list:[{key:1,value:2}]
            changeName:function(){
                $scope.obj.name='李四'
            },
             //查询 
            search:function(){
                //接口请求
                $conn.getConn('tk.getList')({
                    dateStart:'2020-01-01',
                    dateEnd:'2020-01-02'
                },function(res){
                    var cache=res.data||{}
                    $scope.list=cache.list||[]
                    swal.success('查询成功！')
                },function(){
                    swal.error('查询失败！')
                })
            }
        }
    }])
```
```html
    <div ng-controller="test">
        <div>{{obj.name}}</div>
        <button ng-click="obj.changeName()">点击</button>
        <button ng-click="obj.search()">查询</button>
    </div>
```

#### 页面传值

```js
//打开新页面 
window.open('#/payLogOrderDetail?id='+id,"_blank","width=1120px,height=560px,left=200px,top=70px,scrollbars=1")
 //当前页面路由跳转  {id:'123'} 传参
 $state.go('app.train.offlineList'，{id:'123'})
 //获取路由参数
 $scope.data = $location.search()||{}
```

