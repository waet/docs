### 快递

```js
//路由引入
'js/services/expressPlan/index.js'//物流信息
'js/directives/express/index.js'//快递信息
```

```html
<!--页面引入-->
<express ng-cloak ng-if="directiveData"
         order-type="orderType"
         directive-data="directiveData"
         order-id="directiveData.id"
         corp-id="directiveData.corpId"
         mail-user="directiveData.cfmUser"
         valid-express="onValidExpress(params)" save-express="onSaveExpress(params)">
</express>
```

1. `order-type` ： 订单类型  必填
2. `directive-data` 订单详情 必填
3. `order-id` 订单id 必填
4. `corp-id` 企业id 必填
5. `mail-user` 邮寄人id  非必填
6. `valid-express` 邮寄页面验证方法 非必填
7. `save-express` 邮寄页面保存方法 非必填