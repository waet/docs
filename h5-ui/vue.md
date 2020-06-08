# Vue 项目开发手册

架构的目的是管理复杂度，将复杂问题分而治之、有效管理，我们的具体方法如下：
<a name="2bd71fdc"></a>
## 参考目录
```
一. SPA or MPA
    1.SPA
    2.MPA
    3.SPA + MPA
    
二. 技术选型
    1.JS or TS
    2.JS 框架
    3.UI 框架
    4.对应框架依赖
    5.基于vue-cli 3.0
    
三. 项目架构设计
    1.架构图
    2.目录结构
    3.全局配置
    4.实例化插件
    5.请求、路由拦截器
    6.路由配置
    7.Service 服务层
    9.event bus
    8.状态管理与试图拆分
    
四. 开发细节与规范
    1.Vue组件化开发
    2.组件命名规范
    3.vue文件结构
    4.注释规范
    5.eslint配置
    6.method 自定义方法命名
    7.mock数据
    8.注意点

五. 打包
    1. webapp or web
    2. 上传cdn
```

---
<a name="5a0a32d4"></a>
# SPA or MPA

> 首先要思考我们的项目最终构建的是，还是，还是，通过他们的优缺点来分析：


<a name="SPA"></a>
## SPA
* 优点：

  * 体验好，路由之间跳转可定制转场动画，使用懒加载可有效减少首页白屏时间，相较于多页面减少了用户访问静态资源服务器的次数等。

  * 适用于经常需要进行局部页面跳转且不需要SEO的，如后台管理，非native app等。

* 缺点：

  * 初次加载时耗时多。

  * 导航不可用，如果一定要导航需要自行实现前进、后退。


<a name="MPA"></a>
## MPA
* 优点：

  * SEO优化实现简易。

  * 在适用weex开发时，vue-router跳转界面很生硬，效果不好。需要使用weex层面表现的实例。

  * 适用于官网页面、极度依赖seo的web和weex应用等。

* 缺点：

  * 页面间传递数据只能依赖URL，cookie，storage。

  * 页面切换需要继续从服务端加载资源，用户体验差。


<a name="a2cb976e"></a>
## SPA + MPA
* 该方式主要用于文章分享等，用户需要访问SPA的局部资源之类功能，可以把这部分资源以MPA方式抽离出克，使用户不需要加载完整个SPA资源即可访问，减轻静态资源服务器压力。


> 我们首先根据业务所需，来最终确定`构建主体`，而我们选择了`体验至上的 SPA`，并选用 `Vue` 技术栈。


---
<a name="15a472cc"></a>
# 技术选型
<a name="6a99fc33"></a>
## JS or TS
我：送分题，过！

<a name="a30b0c1e"></a>
## JS 框架
~~React~~，[Vue](https://cn.vuejs.org), ~~Angular~~

<a name="b5abae3d"></a>
## UI 框架
结合自身业务看是否需要使用

* PC：

  * [Element](http://element-cn.eleme.io/#/zh-CN)

  * [iView](https://www.iviewui.com/)

  * [Nuxt](https://zh.nuxtjs.org/guide)

  * [Ant Design](http://tangjinzhou.gitee.io/ant-design) 等

* 移动端：

  * [Vux](http://element-cn.eleme.io/#/zh-CN)

  * [Mint UI](https://mint-ui.github.io/#!/en)

  * [Muse UI](https://muse-ui.org/#/zh-CN)

  * [Onsen UI](https://onsen.io/v2/guide/vue/) 等


在此列出较为热门的。UI 框架很多，请大家妥善选择。

<a name="3d950117"></a>
## 对应框架依赖
* vuex 状态管理

* vue-router 单页应用必备

* axios HTTP库


<a name="1a0974e0"></a>
## 基于[vue-cli 3.x ](https://cli.vuejs.org/zh/guide/)
<a name="464343e4"></a>
##### Vue CLI 是一个基于 Vue.js 进行快速开发的完整系统：
* 一个丰富的官方插件集合，集成了前端生态中最好的工具。

* 一套完全图形化的创建和管理 Vue.js 项目的用户界面（GUI）。


Vue CLI 致力于将 Vue 生态中的工具基础标准化。它确保了各种构建工具能够基于智能的默认配置即可平稳衔接，这样你可以专注在撰写应用上，而不必花好几天去纠结配置的问题。

<a name="e68c3484"></a>
# 项目架构设计

<a name="65aa05f0"></a>
## 架构图

![](https://camo.githubusercontent.com/a6f0782cad04407110c6ae8eb83ff16e91b0cafd/687474703a2f2f70342e7168696d672e636f6d2f743031646165396333356564333362616531312e706e67#align=left&display=inline&height=347&originHeight=596&originWidth=1281&status=done&width=746)

<a name="c222403a"></a>
## 目录结构
```
src
 ├-- common              // 核心UI库
     ├── assets          // 资源目录 图片，样式，iconfont
     ├── utils           // 工具类
     ├── directives      // 拓展指令集合
     └── components      // 组件

 └── business            // 业务相关开发
     ├── assets          // 资源目录 图片，样式，iconfont
     ├── components      // 业务组件
     ├── config          // 项目配置，拦截器，开关
     ├── plugins         // 插件相关，生成路由、请求、store 等实例，并挂载 Vue 实例
     ├── directives      // 拓展指令集合
     ├── routes          // 路由配置
     ├── service         // 服务层
     ├── utils           // 工具类
     └── views           // 视图层
```

<a name="8e8aaafe"></a>
## 全局配置
<a name="ea3fbf83"></a>
##### 全局配置，拦截器目录结构
```
config
├──index.js             // 全局配置
├── interceptors        // 拦截器
    ├── index.js        // 入口文件
    ├── axios.js        // 请求/响应拦截
    ├── router.js       // 路由拦截
    └── ...
└── ...
```

<a name="8e8aaafe-1"></a>
##### 全局配置
```
// config/index.js

// 当前宿主平台 兼容多平台应该通过一些特定函数来取得
export const HOST_PLATFORM = 'WEB'
// 这个就不多说了
export const NODE_ENV = process.env.NODE_ENV || 'prod'

// 是否强制所有请求访问本地 MOCK
export const AJAX_LOCALLY_ENABLE = false

// 是否开启监控
export const MONITOR_ENABLE = true

// 路由默认配置，路由表并不从此注入
export const ROUTER_DEFAULT_CONFIG = {
    waitForData: true,
    transitionOnLoad: true
}

// axios 默认配置
export const AXIOS_DEFAULT_CONFIG = {
    timeout: 20000,
    maxContentLength: 2000,
    headers: {}
}

// vuex 默认配置
export const VUEX_DEFAULT_CONFIG = {
    strict: process.env.NODE_ENV !== 'production'
}

// API 默认配置
export const API_DEFAULT_CONFIG = {
    mockBaseURL: '',
    mock: true,
    debug: false,
    sep: '/'
}

// CONST 默认配置
export const CONST_DEFAULT_CONFIG = {
    sep: '/'
}

// 还有一些业务相关的配置
// ...

// 还有一些方便开发的配置
export const CONSOLE_REQUEST_ENABLE = true      

// 开启请求参数打印
export const CONSOLE_RESPONSE_ENABLE = true     

// 开启响应参数打印
export const CONSOLE_MONITOR_ENABLE = true      // 监控记录打印
```

<a name="e4b16561"></a>
## 实例化插件

<a name="d51f5d0c"></a>
###### plugins 目录结构
```
plugins
├── api.js              // 服务层 api 插件
├── axios.js            // 请求实例插件
├── const.js            // 服务层 const 插件
├── store.js            // vuex 实例插件
├── inject.js           // 注入 Vue 原型插件
└── router.js           // 路由实例插件
```

<a name="904cc78a"></a>
##### 实例化 _router_
```
// plugins/router.js

import Vue from 'vue'
import Router from 'vue-router'
import ROUTES from 'Routes'
import {ROUTER_DEFAULT_CONFIG} from 'Config/index'
import {routerBeforeEachFunc} from 'Config/interceptors/router'

Vue.use(Router)

// 注入默认配置和路由表
let routerInstance = new Router({
    ...ROUTER_DEFAULT_CONFIG,
    routes: ROUTES
})
// 注入拦截器
routerInstance.beforeEach(routerBeforeEachFunc)

export default routerInstance
```

<a name="cced2b7e"></a>
##### 实例化 _axios_
```
import axios from 'axios'
import {AXIOS_DEFAULT_CONFIG} from 'Config/index'
import {requestSuccessFunc, requestFailFunc, responseSuccessFunc, responseFailFunc} from 'Config/interceptors/axios'

let axiosInstance = {}

axiosInstance = axios.create(AXIOS_DEFAULT_CONFIG)

// 注入请求拦截
axiosInstance
    .interceptors.request.use(requestSuccessFunc, requestFailFunc)
// 注入失败拦截
axiosInstance
    .interceptors.response.use(responseSuccessFunc, responseFailFunc)

export default axiosInstance
```

<a name="0e06ad04"></a>
##### 往vue注入插件
```
import Vue from 'vue'

GLOBAL.vbus = new Vue()

// import 'Components'// 全局组件注册
import 'Directives' // 指令

// 引入插件
import router from 'Plugins/router'
import inject from 'Plugins/inject'
import store from 'Plugins/store'
// 引入组件库及其组件库样式
import VueOnsen from 'vue-onsenui'
import 'onsenui/css/onsenui.css'
import 'onsenui/css/onsen-css-components.css'
// 引入根组件
import App from './App'

Vue.use(inject)
Vue.use(VueOnsen)

// render
new Vue({
    el: '#app',
    router,
    store,
    template: '<App/>',
    components: { App }
})
```

<a name="7530c44e"></a>
## 请求、路由拦截器

**axios拦截器**
```
import { CONSOLE_REQUEST_ENABLE, CONSOLE_RESPONSE_ENABLE } from '../index.js'

export function requestSuccessFunc (requestObj) {
    CONSOLE_REQUEST_ENABLE && console.info('requestInterceptorFunc', `url: ${requestObj.url}`, requestObj)
    // 自定义请求拦截逻辑，可以处理权限，请求发送监控等
    // ...
    
    return requestObj
}

export function requestFailFunc (requestError) {
    // 自定义发送请求失败逻辑，断网，请求发送监控等
    // ...
    
    return Promise.reject(requestError);
}

export function responseSuccessFunc (responseObj) {
    CONSOLE_RESPONSE_ENABLE && console.info('responseInterceptorFunc', `url: ${responseObj.url}`, responseObj)
    // 自定义响应成功逻辑，全局拦截接口，根据不同业务做不同处理，响应成功监控等
    // ...
    // 假设我们响应体为
    // {
    //     code: 1010,
    //     msg: 'this is a msg',
    //     data: null
    // }
    
    let resData =  responseObj.data
    let {code} = resData
    
    switch(code) {
        case 0: // 如果业务成功，直接进成功回调  
            return resData.data;
        case 1111: 
            // 如果业务失败，根据不同 code 做不同处理
            // 比如最常见的授权过期跳登录
            // 特定弹窗
            // 跳转特定页面等
            
            location.href = xxx // 这里的路径也可以放到全局配置里
            return;
        default:
            // 业务中还会有一些特殊 code 逻辑，我们可以在这里做统一处理，也可以下方它们到业务层
            !responseObj.config.noShowDefaultError && GLOBAL.vbus.$emit('global.$dialog.show', resData.msg);
            return Promise.reject(resData);
    }
}

export function responseFailFunc (responseError) {
    // 响应失败，可根据 responseError.message 和 responseError.response.status 来做监控处理
    // ...
    return Promise.reject(responseError);
}
```

一般在拦截器适合进行全局事件（events bus）的注册和触发

**路由拦截器**
```
export function routerBeforeEachFunc (to, from, next) {
    // 这里可以做页面拦截，很多后台系统中也非常喜欢在这里面做权限处理
    
    next()
}
```

<a name="dedb0b7c"></a>
## 路由配置
```
routes
├── index.js            // 入口文件
├── common.js           // 公共路由，登录，提示页等
├── account.js          // 账户流程
├── register.js         // 挂号流程
└── ...
```

这里的拆分配置有两个注意的地方：

* 需要根据自己业务性质来决定，有的项目可能适合划分，有的项目更适合以划分。

* 在多人协作过程中，尽可能避免冲突，或者减少冲突。


<a name="9ff4713f"></a>
##### 懒加载

文章开头说到单页面静态资源过大，首次打开/每次版本升级后都会较慢，可以用懒加载来拆分静态资源，减少白屏时间，但开头也说到懒加载也有待商榷的地方：

* 如果异步加载较多的组件，会给静态资源服务器/ CDN 带来更大的访问压力的同时，如果当多个异步组件都被修改，造成版本号的变动，发布的时候会大大增加 CDN 被击穿的风险。

* 懒加载首次加载未被缓存的异步组件白屏的问题，造成用户体验不好。

* 异步加载通用组件，会在页面可能会在网络延时的情况下参差不齐的展示出来等。


<a name="6904f716"></a>
## Service 服务层

**服务层作为项目中的另一个核心之一**

目录结构
```
service
├── api
    ├── index.js             // 入口文件
    ├── order.js             // 订单相关接口配置
    └── ...
├── const                   
    ├── index.js             // 入口文件
    ├── order.js             // 订单常量接口配置
    └── ...
├── store                    // vuex 状态管理
├── expands                  // 拓展
    ├── monitor.js           // 监控
    ├── beacon.js            // 打点
    ├── localstorage.js      // 本地存储
    └── ...                  // 按需拓展
└── ...
```

首先抽离请求接口模型，可按照领域模型抽离 (service/api/index.js):
```
{
    user: [{
        name: 'info',
        method: 'GET',
        desc: '测试接口1',
        path: '/api/info',
        mockPath: '/api/info',
        params: {
            a: 1,
            b: 2
        }
    }, {
        name: 'info2',
        method: 'GET',
        desc: '测试接口2',
        path: '/api/info2',
        mockPath: '/api/info2',
        params: {
            a: 1,
            b: 2,
            b: 3
        }
    }],
    order: [{
        name: 'change',
        method: 'POST',
        desc: '订单变更',
        path: '/api/order/change',
        mockPath: '/api/order/change',
        params: {
            type: 'SUCCESS'
        }
    }]
    ...
}
```

定制下需要的几个功能：

* 请求参数自动截取。

* 请求参数不穿则发送默认配置参数。

* 需要命名空间。

* 通过全局配置开启调试模式。

* 通过全局配置来控制走本地 mock 还是线上接口等。


定制好功能，开始编写简单的 plugins/api.js 插件：

import axios from './axios'
import _pick from 'lodash/pick'
import _assign from 'lodash/assign'
import _isEmpty from 'lodash/isEmpty'

import { assert } from 'Utils/tools'
import { API_DEFAULT_CONFIG } from 'Config'
import API_CONFIG from 'Service/api'
```
class MakeApi {
    constructor(options) {
        this.api = {}
        this.apiBuilder(options)
    }


    apiBuilder({
    	sep = '|',
    	config = {},
    	mock = false, 
    	debug = false,
    	mockBaseURL = ''
    }) {
    	Object.keys(config).map(namespace => {
    		this._apiSingleBuilder({
                namespace, 
                mock, 
                mockBaseURL, 
                sep, 
                debug, 
                config: config[namespace]
            })
    	})
    }
    _apiSingleBuilder({
    	namespace, 
    	sep = '|',
    	config = {},
    	mock = false, 
    	debug = false,
    	mockBaseURL = ''
    }) {
        config.forEach( api => {
            const {name, desc, params, method, path, mockPath } = api
            let apiname = `${namespace}${sep}${name}`,// 命名空间
                url = mock ? mockPath : path,//控制走 mock 还是线上
                baseURL = mock && mockBaseURL
            
            // 通过全局配置开启调试模式。
            debug && console.info(`调用服务层接口${apiname}，接口描述为${desc}`)
            debug && assert(name, `${apiUrl} :接口name属性不能为空`)
            debug && assert(apiUrl.indexOf('/') === 0, `${apiUrl} :接口路径path，首字符应为/`)

            Object.defineProperty(this.api, `${namespace}${sep}${name}`, {
                value(outerParams, outerOptions) {
                
                    // 请求参数自动截取。
                    // 请求参数不穿则发送默认配置参数。
                    let _data = _isEmpty(outerParams) ? params : _pick(_assign({}, params, outerParams), Object.keys(params))
                    return axios(_normoalize(_assign({
                        url,
                        desc,
                        baseURL,
                        method
                    }, outerOptions), _data))
                }
            })      
        })
    }       
}

function _normoalize(options, data) {
    // 这里可以做大小写转换，也可以做其他类型 RESTFUl 的兼容
    if (options.method === 'POST') {
        options.data = data
    } else if (options.method === 'GET') {
        options.params = data
    }
    return options
} 
// 注入模型和全局配置，并暴露出去
export default new MakeApi({
	config: API_CONFIG,
	...API_DEFAULT_CONFIG
})['api']
```

挂载到原型
```
install: (Vue, options) => {
    Vue.prototype.$api = api
    // 需要挂载的都放在这里
}
```

这样我们可以在业务中愉快的使用业务层代码：
```
// .vue 中
export default {
    methods: {
        test() {
            this.$api['order/info']({
                a: 1,
                b: 2
            })
        }
    }
}
```

> 一般来说，多人协作时候大家都可以先看 api 是否有对应接口，当业务量上来的时候，也肯定会有人出现找不到，或者找起来比较费劲，这时候我们完全可以在 请求拦截器中，把当前请求的 url 和 api 中的请求做下判断，如果有重复接口请求路径，则提醒开发者已经配置相关请求，根据情况是否进行二次配置即可。


最终我们可以拓展 Service 层的各个功能：

**基础**

* api：异步与后端交互

* const：常量枚举

* store：Vuex 状态管理


**拓展**

* localStorage：本地数据，稍微封装下，支持存取对象即可

* monitor：监控功能，自定义搜集策略，调用 api 中的接口发送

* beacon：打点功能，自定义搜集策略，调用 api 中的接口发送

* ...


<a name="95d72736"></a>
## event bus

事件机制是js非常强大的一个能力，使用时要适当注册，及时卸载事件。避免事件管理的内存混乱。

事件机制的真正问题是很容易和。

使用的话，需要写清楚相相关注释和文档辅助。

使用方法：
```
// 把事件管理挂载到全局对象
GLOBAL.vbus = new Vue()

// 注册
GLOBAL.vbus.$on('somthing', doSomething())

// 触发
GLOBAL.vbus.$emit('somthing')

// 卸载
GLOBAL.vbus.$off('somthing')
```

<a name="a21f9b8e"></a>
## 状态管理与视图拆分
<a name="abdce9d8"></a>
##### 你是否真的需要使用vuex？

1. 第一类项目：业务/视图复杂度不高，不建议使用 Vuex，会带来开发与维护的成本，使用简单的 vbus 做好命名空间，来解耦即可。

1. 第二类项目：类似多人协作项目管理，有道云笔记，网易云音乐，微信网页版/桌面版等应用，功能集中，空间利用率高，实时交互的项目，无疑 Vuex 是较好的选择。这类应用中我们可以直接抽离业务领域模型：

store
├── index.js
├── actions.js        // 根级别 action
├── mutations.js      // 根级别 mutation
└── modules
        ├── user.js       // 用户模块
        ├── products.js   // 产品模块
        ├── order.js      // 订单模块
        └── ...

1. 第三类项目：后台系统或者页面之间业务耦合不高的项目，这类项目是占比应该是很大的，我们思考下这类项目：

> 全局共享状态不多，但是难免在某个模块中会有复杂度较高的功能(客服系统，实时聊天，多人协作功能等)，这时候如果为了项目的可管理性，我们也在 store 中进行管理，随着项目的迭代我们不难遇到这样的情况：


```
store/
├── ...
├── modules/
    ├── b.js
    └── ...
└── views/
    ├── ...
    └── a/
        ├── b.js
        └── ...
```

* 项目中模块可以自定决定是否使用 Vuex。（渐进增强）

* 从有状态管理的模块，跳转没有的模块，我们不想把之前的状态挂载到 store 上，想提高运行效率。（冗余）

* 让这类项目的状态管理变的更加可维护。（开发成本/沟通成本）


**实现**

我们借助 Vuex 提供的  和  一并解决这些问题，我们在 service/store 中放入全局共享的状态：
```
service/
└── store/
    ├── index.js
    ├── actions.js
    ├── mutations.js
    ├── getters.js
    └── state.js
```

> 一般这类项目全局状态不多，如果多了拆分 module 即可。


编写插件生成  实例：
```
import Vue from 'vue'
import Vuex from 'vuex'
import {VUEX_DEFAULT_CONFIG} from 'Config'
import commonStore from 'Service/store'

Vue.use(Vuex)

export default new Vuex.Store({
    ...commonStore,
    ...VUEX_DEFAULT_CONFIG
})
```

对一个需要状态管理页面或者模块进行分层：
```
views/
└── pageA/
    ├── index.vue
    ├── components/
        ├── a.vue
        ├── b.vue
        └── ...
    ├── children/
        ├── childrenA.vue
        ├── childrenB.vue
        └── ...
    └── store/
        ├── index.js
        ├── actions.js
        ├── moduleA.js  
        └── moduleB.js
```

module 中直接包含了 getters，mutations，state，我们在 store/index.js 中做文章：
```
import Store from 'Plugins/store'
import actions from './actions.js'
import moduleA from './moduleA.js'
import moduleB from './moduleB.js'

export default {
    install() {
        Store.registerModule(['pageA'], {
            actions,
            modules: {
                moduleA,
                moduleB
            },
            namespace: true
        })
    },
    uninstall() {
        store.unregisterModule(['pageA'])
    }
}
```

最终在 index.vue 中引入使用， **在页面跳转之前注册这些状态和管理状态的规则，在路由离开之前，先卸载这些状态和管理状态的规则：**
```
import store from './store'
import {mapGetters} from 'vuex'
export default {
    computed: {
        ...mapGetters('pageA', ['aaa', 'bbb', 'ccc'])
    },
    beforeRouterEnter(to, from, next) {
        store.install()
        next()
    },
    beforeRouterLeave(to, from, next) {
        store.uninstall()
        next()
    }
}
```

> 当然如果你的状态要共享到全局，就不执行 uninstall。


<a name="02d4ef79"></a>
# 开发细节与规范

<a name="d760793d"></a>
## Vue组件化开发

目录结构
```
// components 简易结构
components
├── common // 跨项目公共组件
    ├── dist
    ├── build
    ├── src      
        ├── modal
        ├── toast
        └── ...
    ├── index.js             
    └── package.json
└── business // 业务组件
    ├── user
    ├── home
    └── ...
```

<a name="48d989f6"></a>
##### 公用组件

common 中我们会存放 UI 组件库中的那些常见通用组件，在项目中直接通过设置别名来使用，如果其他项目需要使用，就发到 npm 上。

**其它项目引用组件**

假设我们发布的 npm 包叫 bm-ui，并且下载到了本地 npm i bm-ui -S:

修改项目的最外层打包配置，在 rules 里 babel-loader 或 happypack 中添加 include，node_modules/bm-ui：
```
// webpack.base.conf
...
    rules: [{
        test: /\.vue$/,
        loader: 'vue-loader',
        options: vueLoaderConfig
    },
    {
        test: /\.js$/,
        loader: 'babel-loader',
        // 这里添加
        include: [resolve('src'), resolve('test'), resolve('node_modules/bm-ui')]
    },{
    ...
    }]
...
```

然后直接在项目中使用即可：
```
import { modal } from 'bm-ui'
```

<a name="f58c24ad"></a>
##### 业务组件

业务组件一般放置该项目独有的组件

引用：
```
import { menu } from 'Components/business/user'
```

<a name="f02cf615"></a>
## 组件命名规范

**views 下的文件夹命名**

1. views 下面的文件夹代表着模块的名字

1. 由名词组成（car、order、cart）

1. 单词只能有一个（good: car order cart）（bad: carInfo carpage）

1. 尽量是名词（good: car）（bad: greet good）

1. 以小写开头（good: car）（bad: Car）


如：

**views 下面的 vue 文件代表着页面的名字**

1. 放在模块文件夹之下

1. 只有一个文件的情况下不会出现文件夹，而是直接放在 views 目录下面，如 Login Home

1. 尽量是名词

1. 大写开头，开头的单词就是所属模块名字（CarDetail、CarEdit、CarList）

1. 名字至少两个单词（good: CarDetail）（bad: Car）

1. 常用结尾单词有（Detail、Edit、List、Info、Report）

1. 以 Item 结尾的代表着组件（CarListItem、CarInfoItem），放在 components/business


<a name="301828e2"></a>
## vue 文件结构
```
<template>
    <div>
    <!--必须在div中编写页面-->
    </div>
</template>
<script>
    export default {
    components : {
    },
    data () {
        return {
        }
    },
    methods: {
    },
    mounted() {
    }
    }
</script>
<!--声明语言，并且添加scoped-->
<style lang="" scoped>
</style>
```

<a name="d6aac6c5"></a>
##### vue 方法放置顺序
1. components

1. props

1. data

1. created

1. mounted

1. activited

1. update

1. beforeRouteUpdate

1. methods

1. filter

1. computed

1. watch


注意：
* 一个方法不要超过30行

* 使用复制粘贴时，请思考能否适当抽象


<a name="f37651eb"></a>
## 注释规范
1. 公共组件使用说明

1. 各组件中重要函数或者类说明

1. 复杂的业务逻辑处理说明

1. 特殊情况的代码处理说明,对于代码中特殊用途的变量、存在临界值、函数中使用的hack、使用了某种算法或思路等需要进行注释描述

<a name="4649c29c"></a>
##### 文档注释
```
/**
 * （说明）
 * @method / @class / @module
 * @param {类型} 参数说明
 * @param {Number} [i=0] 位置下标
 * @param ...
 * ...
 * @return {Element} 指定元素
 */
```

<a name="ca2addf6"></a>
##### 普通注释
```
总是在单行注释符后留一个空格。例如：
// ...
```

<a name="04463040"></a>
## eslint配置
<a name="174e18f8"></a>
##### 为什么使用eslint？
* ESLint可以校验我们写的代码，给代码定义一个规范，项目里的代码必须按照这个规范写。

* 可以帮助我们避免一些非常低级的错误，一些格式上的问题导致我们在运行生产环境的时候出现一些不明所以的报错。

* 本规范特点之一是简洁。谁也不想为每个项目维护一份有成百上千行语句的代码风格配置文件。有此规范就够了。


查看Standard规则 请戳[这里](https://standardjs.com/rules-zhcn.html#javascript-standard-style)

<a name="a7b97f57"></a>
## method 自定义方法命名
1.动宾短语（good：jumpPage、openCarInfoDialog）（bad：go、nextPage、show、open、login）

2.ajax 方法以 get、post 开头，以 data 结尾（good：getListData、postFormData）（bad：takeData、confirmData、getList、postForm）

3.事件方法以 on 开头（onTypeChange、onUsernameInput）

4.init、refresh 单词除外

5.尽量使用常用单词开头（set、get、open、close、jump）

6.驼峰命名（good: getListData）（bad: get_list_data、getlistData）

<a name="bfd1addf"></a>
## Mock数据
作为专业的前端开发我们应该有一个自己的 `mock 平台`，当前后端定好接口格式，放入生成对应 `mock api`，这样就不必等待后端接口完成我们才能进行开发的尴尬。<br />最后前后端联调。
<a name="d546bd7a"></a>
##### EasyMock 点击前往[官网地址](https://easy-mock.com/)
<a name="826a06a9"></a>
##### Mock语法 [点击查看](https://github.com/nuysoft/Mock/wiki/Syntax-Specification)


<a name="ae5e2438"></a>
## 还有一些注意点

**data props 方法注意点**

1. 使用 data 里的变量时请先在 data 里面初始化

1. props 指定类型，也就是 type

1. props 改变父组件数据 基础类型用 $emit ，复杂类型直接改

1. ajax 请求数据用上 isLoading、isError 变量

1. 表单数据包裹一层 form {}


**生命周期方法注意点**

不在 mounted、created 之类的方法写逻辑，发起ajax请求。
```
<script>
    export default {
        ...
        methods: {
            animation() { ... }
        },
        created() {
            // 我们会把api层抽离放在一个地方供调用，我们的页面不应该去关心 *请求的路径或方法* 是什么。页面只要这个数据来展示等
            postCarList()
        },
        mounted() {
            //  统一这里做对dom的操作处理，并且方法封装好在menthods内
            this.animation();
        }
    }
</script>
```

<a name="5a9f36a7"></a>
# 打包
<a name="d30f4c05"></a>
## webapp or web

<a name="90c6b9c3"></a>
## 上传cdn


<a name="9415a826"></a>
# 最后
时下有各种成熟的方案，这里只是一个简单的构建分享，还有很多地方没有涉及，项目底层构建往往会成为前端忽略的地方，我们既要从一个大局观来看待一个大型项目，或者整条业务线，又要对每一行代码精益求精，对开发体验不断优化，慢慢累积才能应对未知的变化。


