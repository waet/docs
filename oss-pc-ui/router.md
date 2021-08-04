##### 

# 路由

* 添加路由
    - 参数：js/config.router.js
    
```javascript
    angular.module('app').run(['$rootScope', '$state', '$stateParams',
        function ($rootScope, $state, $stateParams) {
            $rootScope.$state = $state;
            $rootScope.$stateParams = $stateParams;
        }
    ]).config(['$stateProvider', '$urlRouterProvider',
        function ($stateProvider, $urlRouterProvider) {
            $urlRouterProvider.otherwise('/access/signin');
            $stateProvider.state('app', {
                'abstract': true,
                url: '/app',
                templateUrl: 'tpl/app.html',
                resolve: {
                    deps: ['uiLoad',
                    function (uiLoad) {
                        return uiLoad.load([
                        'js/controllers/index/index.js',
                        'js/services/websocket.js',
                        'js/plugins/dist/es6-promise.min.js',
                        'js/controllers/index/UniMediaCtrl.js',
                        ]);
                    }
                    ]
                }
            })
            // 导出
            .state('customExport', {
                url: '/customExport',
                templateUrl: 'tpl/custom/export.html',
                params: {},
                resolve: {
                    deps: ['$ocLazyLoad', 'uiLoad',
                        function ($ocLazyLoad, uiLoad) {
                        return uiLoad.load('tpl/custom/export.js')
                            .then(function () {
                            return $ocLazyLoad.load('yjcommon');
                            });
                        }
                    ]
                }
            })
     
                //客户对账单管理
                .state('app.finance.vipAccount', {
                    url: '/vipAccount',
                    template: '<div ui-view class="fade-in"></div>'
                })
                // 客户对账单管理
                .state('app.finance.vipAccount.list', {
                    url: '/vipAccountList',
                    templateUrl: 'js/controllers/finance/vipAccount/index.html',
                    resolve: {
                        deps: ['$ocLazyLoad', 'uiLoad',
                            function ($ocLazyLoad, uiLoad) {
                                return uiLoad.load([
                                        'js/controllers/finance/vipAccount/index.js',
                                    ])
                                    .then(function () {
                                        return $ocLazyLoad.load('yjcommon');
                                    });
                            }
                        ]
                    }
                })
                // 客户对账单管理 详情
                .state('vipAccountDetail', {
                    url: '/vipAccountDetail',
                    templateUrl: 'js/controllers/finance/vipAccount/details/index.html',
                    resolve: {
                        deps: ['$ocLazyLoad', 'uiLoad',
                            function ($ocLazyLoad, uiLoad) {
                                return uiLoad.load([
                                        'js/controllers/finance/vipAccount/details/index.js',
                                        'js/controllers/finance/vipAccount/theDetail/index.js',
                                        'js/controllers/finance/vipAccount/result/index.js',
                                        'js/services/checkbox-widget.js',
                                        'js/services/qrCode/index.js',
                                        'js/services/qrCode/qrCode.js',
                                    ])
                                    .then(function () {
                                        return $ocLazyLoad.load('yjcommon');
                                    });
                            }
                        ]
                    }
                })
    }]
```

* 路由跳转
    ```javascript
    
    app.controller('test',['$state','$location',function($state,$location){
        //当前页面路由跳转  {id:'123'} 传参
        $state.go('app.train.offlineList'，{id:'123'})
        //打开一个新窗口 单独显示这个页面 固定写法
        window.open('#/customExport', "_blank", "width=1250px,height=640px,left=200px,top=70px,scrollbars=1")
    	//获取参数
    	$scope.data = $location.search()||{}
    
    }])
    
    ```

#### 添加菜单

-  菜单页面 nav.html   :  webapp\tpl\blocks\nav.html

```html
<ul class="nav nav-sub dk">
    <li ui-sref-active="active" acs="1060216">
        <a ui-sref="app.finance.vipAccount.list">
            <i class="icon iconfont iconthird-nav"> </i>
            <span>客户对账单管理</span>
        </a>
    </li>
</ul>
```

- acs 菜单权限码
- ui-sref 路由地址
- i class 菜单显示图标