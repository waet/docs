### 公共方法

```js
//文件地址： webapp\js\services\commonService.js
```

#### 使用方法

```js
app.controller('test',['$state','$location','commonService',function($state,$location,commonService){
  	commonService.localset(name,value)//存储本地缓存
    commonService.localget(name)//获取本地缓存
    commonService.sessionget(name)//存储临时缓存
    commonService.sessionset(name,value)//存储临时缓存
    commonService.setTitle(name)//设置页面标题
    commonService.formatDate(date,num)//日期方法
    
}])
```



