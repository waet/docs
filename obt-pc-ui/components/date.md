# 日历

## 查询预订

```javascript

    $("#breakDate").dateRangePicker({
        autoClose: true,//选中关闭
        singleDate : true,//单日期
        showShortcuts: false,
        startDate: "$0",//当前日期 开始日期
        monthSelect: true,
        language: common.getCookie('userLanguage'),
        yearSelect: function(current, moment) {
            var y = moment().get('year');
            return [y - 1, y + 1];
        },
        blur:function(that){//选中回调
            app.params.returnDate=that.val()
            app.arriveDate=dateUtil.formatDate(app.params.returnDate)
        }
    })

```

## 订单列表

- 参数：
    - `type`: 日期格式
    - `value`: $d 当前日期，-7 相对当前日期天数差

```javascript

    $("#dateStart").ECalendar({
            type:"date",
            value:["$d",-7], //初始值
            //minday: ["$d",-60],
            //maxday: ["$d",90],
            callback:function(v,e){} //回调函数
    });

```