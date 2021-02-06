### 日历  (废弃)

- 参数
    - `selected`: 回调
        * type : `function`

```html

    <ld-date
      ref="date1"
      @selected="dateChange"
      :mode="2"
      :date="departDate.date"
      :min-date="minDate"
      :max-date="maxDate"
    />

```

```javascript

    import ldDate from 'Common/ldDate'

    //参数

   	props: {
		date: {
			//选择的日期（此属性和startDate,endDate互斥）
			type: [String, Object],
			default: ''
		},
		startDate: {
			//开始日期
			type: [String, Object],
			default: ''
		},
		endDate: {
			//结束日期
			type: [String, Object, Date],
			default: ''
		},
		priceList: {
			//价格日历数组
			type: [Array, Object],
			default: function() {
				return []
			}
		},
		disabledList: {
			//设定不允许点击的日期
			type: [Array, Object],
			default: function() {
				return []
			}
		},
		initMonthCount: {
			//初始化月的个数
			type: [String, Number],
			default: '12'
		},
		initPreMonthCount: {
			//初始化date或者startDate之前几个月的日历数据
			type: [String, Number],
			default: 0
		},
		mode: {
			//模式（默认1），1酒店，2飞机往返
			type: [String, Number],
			default: 1
		},
		switchMonth: {
			//是否开始切换月份模式
			type: [String, Boolean],
			default: false
		},
		preDisabled: {
			//小于初始的日期的全部disabled置灰
			type: [String, Boolean],
			default: false
		},
		allAbled: {
			//全部日期都可选
			type: [String, Boolean],
			default: false
		},
		lang: {
			type: [String],
			default: 'cn'
		},
		// 可选的最小时间
		minDate: {
			type: [String],
			default: ''
		},
		// 可选的最大时间
		maxDate: {
			type: [String],
			default: ''
		},
		themeColor: {
			type: [String, Object, Date],
			default: '#c9995e'
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
		startTip:{
			type: [String],
			default: '去程'
		},
		endTip:{
			type: [String],
			default: '返程'
		},
		startendtip:{
			type: String,
			default: '去/返'
		},
	},

```