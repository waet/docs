### oss 地址配置

* 复制 src/main/resources/js/parent-appurl.js文件 到src/main/webapp/js/目录下

```javascript
var uireqprefix="${uireqprefix}"; //本地默认 ser
var cmpNo="${cmpNo}";//本地默认 总公司代码
//根据总公司代码定页面风格样式
var global={
	'cmpNo':cmpNo||'DEFAULT',
	'QHHK':'qhhkStyle',
	'ZDJSL':'zdjslStyle',
	'DEFAULT':'defaultStyle',
	'CCKH':'cckhStyle'
};
if(!global[cmpNo]){
	global.cmpNo='DEFAULT'
}

//除了本地开发需要配置IP，其他环境为空
//"http://www.xxxxx.com" 测试环境地址
//"http://www.xxxxx.com" 生产环境地址
// 本地要使用这个

var address_ip = "http://wwww.xxxx.com";//地址


var apiurl = address_ip + "/" + uireqprefix + "/yixServerOss";
var apiurlAdapter = address_ip + "/" + uireqprefix + "/adapterServer";
var apiurlMqc = address_ip + "/" + uireqprefix + "/mqcServer";
var jsfile = address_ip + "/" + uireqprefix + "/yixServerOss";
var uploadurl = address_ip + "/" + uireqprefix + "/parentSystemDfs";
var pmsAddsUrl = address_ip + "/" + uireqprefix + "/singaServer";
var pmsUrl = address_ip + "/" + uireqprefix + "/singaServer";
var bdcServer = address_ip + "/" + uireqprefix + "/bdcServer";
var emuiurl=address_ip +"/ui-em";

var n = window.location.hostname
var nginxPath = '//sfile' + n.substr(n.indexOf('.'));

```

### 文件压缩  

​	只限于  config.router.js  和 interface.js

1. 压缩命令配置：package.json>scripts>compress
2. 安装uglify压缩 cnpm install uglify-js -g
3. 执行压缩 npm run compress

