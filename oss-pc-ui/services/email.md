### 邮件

```javascript

    app.controller('bookTicket', ['$scope',' $modal', 'emailService',
        function ($scope, $modal, emailService) {
			var items = {
				"infoId": $scope.details.detailsList.id, /*订单ID*/
				"email": $scope.details.detailsList.linkEmail, /*联系人邮箱*/
				"type": "11001" //订单类型
			}
			$modal.open(
				emailService.emailOpenInit('md', items)
			).result.then(function (result) {

			});
        }
    ])
```