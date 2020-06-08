## 企业相关的控件

#### 查询预订 头部组件

- 参数
    - `selectCorp`: 企业操作对象
        * type : `Object`
    - `initCorpno`: 初始化（回显）企业  企业ID 
        * type : `String`
    - `initBooker`: 初始化（回显）预订人 ID
        * type : `String`

```html
    <!--企业选择 -->
    <selectcorp select-corp="selectCorp" init-corpno="initCorpno" init-booker="initBooker"></selectcorp>

```

- 方法
    - `corpEmpOpenInit function(size, {}){}`: 弹出选择企业选择员工
    - `travelAppOpenInit function(size, {}){}`: 企业申请单

```javascript
    //services/corpService

    app.controller('bookTicket', ['$scope',' $modal', 'corpService',
        function ($scope, $modal, corpService) {
            $scope.initCorpno=company.corpNo;
            $scope.initBooker=booker.empId;

            $scope.selectCorp = {};
            $scope.selectCorp.changeCorp = function (res) {//改变企业数据
                var cache = res.data || {};
                corpInfo.corpId = cache.id;
                $scope.requesting.corpId=cache.id;
                zcGnjp = cache.zcGnjp;
                commonService.sessionset('company', cache);
            }
            $scope.selectCorp.cleanCorp = function () {//清除企业数据回调
                $scope.requesting.corpId = "";
                $scope.bookerlist = "";
                $scope.booker = "";
                $scope.tvRqstNam = "";
            }
            //选择预订人 回调
            $scope.selectCorp.setBooker = function (resp) {
                $scope.booker = resp[0];
                commonService.sessionset("booker", resp[0]);
            }
            //清除预订人
            $scope.selectCorp.cleanBooker = function () {
                $scope.booker = "";
                commonService.sessionremove("booker");
            }

            if (!corpInfo.corpId) {
                swal.warning('请选择企业！');
                return false;
            }
            $modal.open(
                corpService.corpEmpOpenInit("lg", { corpId: corpInfo.corpId, mod: "" }, $scope.emplist.emp || [])
            ).result.then(function (item) {
                $scope.ddrs = false;
                $scope.emplist.emp1 = item;
                initCheckbox(item);
                $scope.emplist.emp = $scope.emplist.emp1;
                commonService.sessionset("reseruser", $scope.emplist.emp1);
            })

            var params = {
                'corpId': corpInfo.corpId,
                'mod': "radio"
            };
            $modal.open(
                corpService.travelAppOpenInit("lg", params)
            ).result.then(function (item) {
                if (!item) { return false };
                commonService.sessionremove('tvresult');
            })


        }
    ])

```