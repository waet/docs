# 接口

* 添加接口
    - 参数：js/service/interface.js
    
```javascript
    angular.module("yjcommon", []).factory("$conn", ["$http", function ($http) {
        var configs = {
            // 快递单管理-企业配送信息
            express: {
                findCityLocal: { url: apiurl + "/oss/bdc/bCity/findCityLocal", method: "jsonp" },
            },
            //国际机票
            intAirTk: {
                //POST /oss/queryGjFlight
                //航班查询
                queryGjFlight: { url: apiurl + "/oss/queryGjFlight", method: "jsonp", loading: "1" },
            }
        }
    })
```

* 调用

    ```javascript
    
    app.controller('test',['$conn',function($conn){
        $conn.getConn('express.findCityLocal')({
        	  "exportData": "string",
              "productType": 0,
              "acs": "string",
              "airTrainCode": "string",
              "terminal": "string",
              "productStatus": 0,
              "createdateStart": "string",
              "createdateEnd": "string",
              "pageNum": 0,
              "count": 0    
        },function(){
            //success callback
        },function(){
            //error callback
        })
    }])
    
    ```