### 安装

```javascript
安装命令
cnpm install
# OR
yarn install

启动命令
cnpm run serve

编译
cnpm run build:dev //测试环境
cnpm run build  //正式环境

ICON 更新
cnpm run ld-icon  //图标地址维护 build/icon.js 
```

### 配置


* 正式环境
    * 文件名 .env.development.local
* 测试环境
    * 文件名 .env.production

```javascript
    VUE_APP_uireqprefix = ser 
    VUE_APP_cmpNo = xxxx //总公司代码

    VUE_APP_addressIp = https://m.xxxx.com //域名

    VUE_APP_addressUrl = https://m.xxx.com/ser //域名 支付调用

    VUE_APP_logo = qh_df.png  //默认logo 可为空
    VUE_APP_pageName = 商旅前端 // 登录页 title
    VUE_APP_compaySuper = xxxxxxxxxx //总公司id

```

* config/index.js

```javascript
    //动态接口地址

    API_DEFAULT_CONFIG.URL = {
        api: `${process.env.VUE_APP_addressIp}/${process.env.VUE_APP_uireqprefix}/yixServerObt`,
        parent: `${process.env.VUE_APP_addressIp}/${process.env.VUE_APP_uireqprefix}/parentAppurl`,
        mqc: `${process.env.VUE_APP_addressIp}/${process.env.VUE_APP_uireqprefix}/mqcServer`,
        // nginx: `//sfile${host.substr(host.indexOf('.'))}`  //静态文件地址  根据域名动态加载
        nginx:'https://sfile.xxxxx.com'   //静态文件地址 固定加载地址
    }
```
