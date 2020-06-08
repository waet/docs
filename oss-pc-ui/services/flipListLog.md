### 异动日志

```javascript

    app.controller('bookTicket', ['$scope',' $modal', 'flipListLog',
        function ($scope, $modal, flipListLog) {
            $modal.open(
                flipListLog.flipInit("lg", { "id": id, })
            ).result.then(function (item) {
            }, function () { });
        }
    ])
```