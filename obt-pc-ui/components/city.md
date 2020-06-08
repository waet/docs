# 城市

* 调用
- init function 参数：
    - `useTeml`: "", //使用的模板
    - `useLength`: "2", //当input框中 大于指定字符之后，出现渐进检索  2|1
    - `changeOnly`: false, //是否只容许选择，不能手录入
    - `selectAll`: false, //是否在输入框没有任何值的时候，显示所有的数据，默认false。如果此项，在执行filter方法时，所有的值都应该被选中
    - `useStyle`: [420, 0, 0], //[width, top, left ] eg:[0, 12, 32 ] 
    - `listStyle`:[300,0,0],
    - `param`: function () { return {} }, //获取数据时额外的参数
    - `callback`: noop, //回调函数，

```javascript
    var jqselect=require("jqselect"); //引入

    jqselect.init('#departAirportName',{//挂载DOM ID
        useTeml: 'internationArriveCity',//模板名称  jqselect.js
        changeOnly: true,
        useStyle: [510, 0, 39],
        callback: function (data) {// object
            if( !!data ){
                var arr=data
                app.params.departAirport=arr.threeCode
                app.depart={
                    departAirport:(arr.jcZdCode||arr.threeCode),
                    departAirportName:arr.cityName
                }
                $("#departAirport").val((arr.jcZdCode||arr.threeCode));
                $("#departAirportName").val(arr.cityName+'('+(arr.jcZdCode||arr.threeCode)+')');
                publicData.depInt=arr.international
            }
        }
    })

```