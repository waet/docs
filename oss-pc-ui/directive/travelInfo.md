## 差旅信息段


- 参数
    - `data`: 数据源
        * type : `Object`
    - `cplx`: 产品类型
        * type : `String`
    - `order-type`: 订单类型
        * type : `String`

```JavaScript
    路由引入
    'js/directives/travelInfo/index.js',
    'js/services/violate/violateList.js',
```
```html
    <travel-info ng-cloak ng-if="directiveData" data="directiveData" cplx="cplx" order-type="orderType"></travel-info>
```

*数据源

```javascript

    // directive/travelInfo/index.js

    var params={
        corpCode:"",//企业编号
        corpName:"",//企业名称
        corpId:"",//企业ID
        tripType:"",//因公因私
        bookerName:"",//预订人名称
        booker:"",//预订人ID
        vipStatus:"",//差旅状态
        ccsqdNo:"",//出差申请编号
        ccsqdId:"",//出差申请单ID
        projectName:"",//项目名称
        projectCode:"",//项目编号
        projectId:"",//项目ID
        costCenterName:"",//成本中心名称
        costCenterCode:"",//成本中心编号
        costCenterId:"",//成本中心ID
        appId:"",//审批规则ID
        appCode:"",//审批规则编号
        appName:"",//审批规则名称
        violateitem:"",//违背事项说明 
        violateitemCode:"",//违背事项代码 
        reasonDesc:"",//违背原因说明 
        reasonCode:"",//违背原因代码
        ccsqdRemark:"",//出差备注
        subjectCode:"",//科目码
        ifSameOrder:"",//企业内部单号
        linkman:"",//联系人
        linkMobile:"",//联系电话
        linkEmail:"",//联系邮箱
        orderId:"",//订单ID
        orderStatus:"",//订单状态
        international:"",//国内国际。
        customerStatus:"",//与客户办理状态
        changeStatus:"",//改签状态
    }

```