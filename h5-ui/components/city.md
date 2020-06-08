### 城市

- 参数
    - `selected`: 回调
        * type : `function`

```html

    <city
      ref="city"
      :sys-type="way"
      @selected="cityChange"
      :tab-index="roundtrip"
      :cplx="cplx"
      :city-type="0"
    />

```

```javascript

    import City from 'Common/city'

    props: {
		placeholder:{
			type:String,
			default:'请输入城市/机场'
		},
		sysType: {
			type: Number,
			default: 1,//标识符 ||去程返程   传入什么返回什么
		},
		// 国际国内
		tabIndex: {
			type: [Number, String],
			default: 0 // 0 国内 1 国际 
		},
		cityType: {
			type: Number,
			default: 0 // 0 机票 1 酒店 2火车票
		},
		cplx:{
			type:String,
			default:'10901'
		},
		/*
        *挂载节点
        *值为选择器 例如 .tkEdit  #app body
        * 主要解决弹出式头部底部 被当前页面头部底部覆盖的问题
        * 最好挂载到当前页面的根节点上 页面跳转后会相应的移除该控件
        * 没有上面问题 不需传入
        * */
		element:{
			type:String,
			default:''
		},
		showTab:{
			type:Boolean,
			default:true
		},
		isCar:{
			type:Boolean,
			default:false
		}
	}

```