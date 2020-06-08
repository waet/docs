### 签注

```javascript

    app.controller('bookTicket', ['$scope',' $modal', 'flipNoteList',
        function ($scope, $modal, flipNoteList) {
            $modal.open(
                flipNoteList.noteInit("lg", {
                    "id": id,
                    "orderType": 11024
                })
            ).result.then(function (item) {
                $scope.query();
            }, function () { });
        }
    ])
```