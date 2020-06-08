### 短信

```javascript

    app.controller('bookTicket', ['$scope',' $modal', 'smsService',
        function ($scope, $modal, smsService) {
            var items = {
                "infoId": $scope.details.id, /*订单ID*/
                "phone": $scope.details.linkMobile, /*联系人电话*/
                'corpId':$scope.details.corpId,  /*企业ID*/
                'ceneId':13313,
                'psg':$scope.details.bookerName //发送人
            }
            var modalInstance = $modal.open(smsService.smsOpenInit('md',items));
        }
    ])
```