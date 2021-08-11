### 调度

- 参数
    - `param`: 参数对象
        * type : `Object`

```javascript
    路由引入
    'js/services/dispatch.js',

    app.controller('bookTicket', ['$scope',' $modal', 'dispatch',function ($scope, $modal, dispatch) {
            // 调度前验证
             $conn.getConn('outTkCtrl.dispatchPreCheck')({
                "orderId":info.id,
                "djlx": info.orderType,
                "version":info.version
            },function (resp) {//检查是否可以操作
                var cache=resp.data||{}
                var ifCurrentDept=cache.ifCurrentDept
                var orderStatus=cache.orderStatus
                if(!ifCurrentDept){
                    swal.warning("订单不在本部门，不可进行此操作")
                    return
                }
                if(orderStatus==3||orderStatus==4 || orderStatus==5||orderStatus==6){
                    swal.warning("订单状态发生变化，此状态下不可调度，请刷新后重试")
                    return
                }
                //调度参数
                var param={
                    baseData:[
                        {key:'订单类型:',value:$filter('orderType')(info.orderType)},//
                        {key:'产品名称:',value:info.productName},
                        {key:'机场/火车站 :',value:info.airportName},
                        {key:'航站楼:',value:info.terminal},
                        {key:'类型 :',value:$filter('setOutModel')(info.setOutModel)},
                        {key:'有效期 :',value:info.validityStart?(info.validityStart+''+info.validityEnd):''},
                        {key:'服务时间:',value:''},
                        {key:'备注:',value:''},
                    ],
                    defaultDept1:{
                        name:'出票部门',
                        isDisabled:false,//是否禁用
                        isShow:true,//是否显示
                    },
                    defaultDept2:{
                        name:'配送办理部门',
                        isDisabled:false
                    },
                    djlx: info.orderType, //订单类型
                    info: info, //订单信息
                    outTime:false,//显示出票时限
                    showAutoTicket:false,// 显示是否自动出票
                }
                //调度
                $modal.open(
                    dispatch.openscheduling("lg", param)
                ).result.then(function(result) {
                    if(result) $scope.airService.search()
                })

            }, function (res) {
                if (res.errCode == '1001') {
                    swal.warning(res.errMsg)
                }
            })
        }
    ])
```