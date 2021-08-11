### 配送段（已废弃）

- 参数
    - `data`: 订单详情配送段字段
        * type : `String`
    - `order-type`: 订单类型
        * type : `String`
```JavaScript
路由引入
'js/directives/distribution/distribution.js',
```
```html
<distribution ng-cloak ng-if="directiveData" data="directiveData" order-type="orderType"></distribution>
```

