### 支付

- 参数
    - `id`: 订单id
        * type : `String`
    - `orderType`: 订单类型
        * type : `String`

```javascript
    路由引入
    'js/utils/compute.js',
    'js/services/qrCode/index.js',
    'js/services/qrCode/qrCode.js',
    'js/services/payment.js',

    app.controller('bookTicket', ['$scope',' $modal', 'pay',
        function ($scope, $modal, pay) {
            var params={
                'id':id, //订单id
                'orderType':11019 //订单类型
            }
            $modal.open(
                pay.payInit("lg",params)
            ).result.then(function(item) {
                    $scope.obj.btnClick(1);
            })
        }
    ])
```