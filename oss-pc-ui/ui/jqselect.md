## 远程搜索 Jqselect 控件
当选项过多，视图范围内无法展示下，需要输入关键字进行检索时。

## OSS编写常用写法
```html
<input type="text" cancel id="corp_code" class="form-control"  ng-model="corpId" />
<jqselect
    key-word="corpId"
    use-style=""
    use-template="corp"
    use-length="1"
    use-ctrl="corpCtrl"
    query="prev"
    change-only="true"
    select-all="true"
>
```
<a name="Jqselect-Attributes"></a>
### [](#Jqselect-Attributes)Jqselect Attributes
| 参数         | 说明                                         | 类型    | 默认值 |
| ------------ | -------------------------------------------- | ------- | ------ |
| key-word     | 绑定值                                       | Scope   |        |
| use-template | 使用的模板                                   | String  |        |
| use-style    | 样式                                         | String  |        |
| use-length   | 当input框中 大于指定字符之后，出现渐进检索   | String  |        |
| change-only  | 是否只容许选择，不能手录入                   | Boolean | false  |
| select-all   | 是否在输入框没有任何值的时候，显示所有的数据 | Boolean | false  |
| forid        | 绑定input框id                                | String  |        |
| query        | 绑定input框, 值：`next`、 `prev`             |         |        |

<a name="Jqselect-Events"></a>
### [](#Jqselect-Events)Jqselect Events
| 参数           | 说明                                                         | 类型            | 默认值 |
| -------------- | ------------------------------------------------------------ | --------------- | ------ |
| use-ctrl       | 控件最终的回调函数，在选择之后，会把选中的对象作为`value` 传到方法里 | Function        |        |
| useCtrl.params | 请求数据的接口，传入的一些参数，比如企业id，部门id等。字段名交由编写模板的时候自行定义 | Object/Function |        |
| useCtrl.show   | 控件显示时触发                                               | Function        |        |
| useCtrl.hide   | 控件隐藏时触发 可在内执行其它控件的show来联动                | Function        |        |

## 新增模板编写规范
当你需要展示的数据不在模板内，那么则需要自己编写。


```javascript
// js/directives/yjdirectives.js
// 在 bussTemplate 对象下添加以下对象，[]

[模板名称]: {
    suggest: {
        // 数据加载方式
        useMode: "jsSourceMode",
        suggesthead: "请输入名称",
        source: {
            cached: true,
            conn: [interface中接口名称],
            param: function(term) {
                // 如果 useCtrl.params 是函数那么先执行一遍返回对象
                return $scope.useCtrl.params
            }
        },
        // 数据返回之后，通过处理、筛选之后，存放到缓存之中； return: []
        resultFun: function(result) {
            var pArr = [],
                datas = result || [];
            for (var i = 0, l = datas.length; i < l; i++) {
                var obj = datas[i];
                pArr.push({
                    id: obj.id,
                    name: obj.name
                    // ... 这里筛选出需要的数据
                });
            }
            return pArr;
        },
        // term 为文本框内的值，与 resultFun 值匹配；return: []
        filterFun: function(cachedData, term) {
            var results = [],
            if (!term) return cachedData;
            
            // 过滤规则
            var mather = new RegExp(term, "gi"); 
                
            for (var i = 0, l = cachedData.length; i < l; i++) {
                var obj = cachedData[i]
                // 根据需要过滤自段
                if (needFilter(term) && mather.test(obj.id) || mather.test(obj.name)) {
                    results.push(cachedData[i]);
                    break;
                }
            }
            return results;
        },
        // 创建suggest模板；return: string
        // 数据，分页起始，分页结束
        suggestTmpl: function(datas) {
            var html = "";
            if (datas.length == 0) {
                html += "对不起，无匹配，请重新输入";
            } else {
                html +=
                    '<li ng-repeat="suggestData in suggestDatas" ng-click="suggestClick(suggestData)" class="hover" ng-class="{\'cur\':suggestSelect.selected[$index]}"><span class="left">{{suggestData.by1}}</span><span class="right">{{suggestData.svalue}}<span></li>';
            }
            return html;
        },
        // 选中之后回调
        callback: function(value, param) {
            $scope.term = value.name;
            return $scope.term;
        }
    }
}
```