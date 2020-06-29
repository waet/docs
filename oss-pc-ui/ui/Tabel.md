# Tabel 表格
用于展示多条结构类似的数据，可对数据进行排序、筛选、对比或其他自定义操作。

## 基础表格
基础的表格展示用法。
```html
<!-- 
样式类：
    .center .left .right 行内元素对齐
    .table-striped 斑马纹表格（奇数行灰色背景色）
    .show-ellipsis 显示省略号
    
常用过滤器：
    tofloat2:保留2位小数
    toNum:加 %（0.5 => 50%）
-->
<table class="table table-striped table-bordered table-condensed center table-hover smallth" ng-show="list.length > 0">
	<thead>
		<tr class="nopalr">
		<th>序号</th>
		<!-- something th -->
		</tr>
	</thead>
	<tbody>
		<tr ng-repeat="info in list" class="nopalr">
			<td>{{$index+1}}</td>
		    <!-- something td -->
            <td>
                <span class="show-ellipsis"></span>
            </td>
        </tr>
	</tbody>
</table>
```

- 常用样式类：
    - `.center` `.left` `.right` 行内元素对齐
    - `.table-striped` 斑马纹表格（奇数行灰色背景色）
    - `.show-ellipsis` 显示省略号
    - `.pointer` 悬浮手指
    - `.blueunLin` 蓝色下划线

- 常用过滤器：
    - `tofloat2` 保留2位小数
    - `toNum` 加 %（0.5 => 50%）

- 常用指令：
    - `high-lignt` tr选中高亮 绑定该条数据的 `trChecked` 属性



```html
    状态颜色
    <span ng-show="info.changeStatus==0"  style="color:#323232 ">已申请</span>
    <span ng-show="info.changeStatus==1"  style="color:#ff9600 ">已调度</span>
    <span ng-show="info.changeStatus==2"  style="color:#19a423 ">已复核</span>
    <span ng-show="info.changeStatus==3"  style="color:#2682e9 ">已完成</span>
    <span ng-show="info.changeStatus==4"  style="color:#19a423 ">改签待完成</span>
    <span ng-show="info.changeStatus==5"  style="color:#19a423 ">已取消</span>
    <span ng-show="info.changeStatus==6"  style="color:#19a423 ">改签中</span>
    <span ng-show="info.changeStatus==7"  style="color:#2682e9 ">已改签</span>
```


## 排序
对表格进行排序，可快速查找或对比数据。
```html
<table class="table table-striped table-bordered table-condensed center table-hover smallth" ng-show="list.length > 0">
    <thead>
    	<tr class="nopalr">
        	<th>
                <!-- 数字排序 -->
                <i class="fa pointer" 
                  ng-class="{
                    'fa-sort-numeric-asc blue': sort_price,
                    'fa-sort-numeric-desc': !sort_price
                  }" 
                ng-click="sort('price')"></i>
        	    金额
        	</th>
        	<th>
                <!-- 字母排序 -->
                <i class="fa pointer" 
                  ng-class="{
                    'fa-sort-alpha-asc blue': sort_tkNo,
                    'fa-sort-alpha-desc': !sort_tkNo
                  }" 
                ng-click="sort('tkNo')"></i>
        	    票号
        	</th>
        	<!-- something th -->
    	</tr>
    </thead>
    <tbody>
    	<tr ng-repeat="info in list" class="nopalr">
    		<td>{{ info.price }}</td>
    	    <!-- something td -->
        </tr>
    </tbody>
</table>
```
```javascript
// controller
// col: 需要排序字段名
$scope.pHsort = function(col) {
	$scope['sort_' + col] = !$scope['sort_' + col];
    $scope.data.sort = // 此处字段名根据实际接口为准
        $scope['sort_' + col] ? col + ' asc' : col + ' desc'
    
    // 查询事件
    // ...
}
```
在 `OSS` 中列表排序一般是交由后台处理

上面示例展示了给 `price`（数字） 字段和 `tkNo`（含字母） 进行排序。



## 表尾合计行
若表格展示的是各类数字，可以在表尾显示各列的合计。
```html
<table class="table table-striped table-bordered table-condensed center table-hover smallth" ng-show="list.length > 0">
	<thead>
		<tr class="nopalr">
		<th>序号</th>
		<!-- something -->
		</tr>
	</thead>
	<tbody>
		<tr ng-repeat="info in list" class="nopalr">
			<td>{{$index+1}}</td>
		    <!-- something -->
            <td></td>
        </tr>
	</tbody>
	
	<!-- 小计、合计 -->
	<tfoot>
		<!-- 
		样式类：
    		.heji td { 常用于小计、合计
            	font-weight: bold;
            	text-align: right;
            }
            .heji .txt-left {
            	text-align: left;
            }
            
        常用过滤器：
            yjsum:计算整个数组的某个字段
            使用:list | yjsum:'计算字段'|fixed2
        -->
		<tr class="heji nopalr">
			<td colspan="*"></td>
	 		<td class="txt-left">小计：</td>
	 		<td class="right">{{list|yjsum:'fcny'|fixed2}}</td>
		</tr>
		<tr class="heji nopalr">
			<td colspan="*"></td>
	 		<td class="txt-left">合计：</td>
	 		<td>{{sum.fcny|fixed2}}</td>
		</tr>	
	</tfoot>			
</table>
```
## 多级表头
数据结构比较复杂的时候，可使用多级表头来展现数据的层次关系。
```html
<table class="table table-striped table-bordered table-condensed center table-hover smallth" ng-show="list.length > 0">
	<thead>
		<tr class="nopalr">
			<th rowspan="2">日期</th>
			<th rowspan="2">姓名</th>
			<th colspan="3">地址</th>
			<th colspan="2">联系方式</th>
		</tr>
		<tr>
		    <th>省份</th>
		    <th>市区</th>
		    <th>详细地址</th>
		    <th>手机号码</th>
		    <th>邮箱地址</th>
		</tr>
	</thead>
	<tbody>
		<tr ng-repeat="info in list" class="nopalr">
			<td>{{$index+1}}</td>
		    <!-- something td -->
            <td>
                <span class="show-ellipsis"></span>
            </td>
        </tr>
	</tbody>
</table>
```


## 固定表头
纵向内容过多时，可选择固定表头。


## 固定列
横向内容过多时，可选择固定列。

# 分页
当数据量过多时，使用分页分解数据。
## 基础用法
```html
<pagination class="pagination-sm-s m-t-none m-b" 
    boundary-links="true" 
    rotate="false"
    total-items="vm.totalElements" // 总共多少条数据
    ng-change="vm.pageChanged()" // 点击页面跳转
    max-size="10" // 展示多少页码
    ng-model="vm.pageNum" // 当前页
    items-per-page="vm.count" // 每页多少条数据
    first-text="首页"
    last-text="最后一页"
    next-text="下一页"
    previous-text="上一页">
</pagination>
```

## OSS编写常用写法
配合下拉框设置展示数目
```html
<!--S 分页-->
<div  ng-show="salesDetails.length>0" >
	<div class="pagefixed"  style="margin-bottom: 18px;">
		<div class="Fright bg-blue  padRL20 padT5">
			<span>共 <span class="page-color">{{total}}</span> 条, 展示</span>
		    <label>
              <select  ng-model="data.count" ng-change="pageChanged(count)">
                <option value="20">20</option>
                <option value="30">30</option>
                <option value="50">50</option>
                <option value="100">100</option>
                <option value="200">200</option>
              </select>
            </label>
		    <span>条</span>
		</div>
        <div class="Fright bg-blue padT5 padL20">
            <pagination 
        	  boundary-links="true"
              total-items="total" 
              items-per-page="data.count" 
              ng-change="pageChanged(count)" 
              ng-model="data.pageNum" 
              class="pagination-sm-s m-t-none m-b" 
              previous-text="上一页" 
              next-text="下一页" 
              first-text="首页" 
              last-text="尾页"
              max-size="5" 
              rotate="false">
    		</pagination>
    	</div>
	</div>
</div>
<!--E 分页-->
```
```javascript
// app.controller('xxx')

/*分页start*/
$scope.pageNum = 1;
$scope.count = 20;
$scope.$watch("count", countChange);

//分页方法
$scope.pageChanged = function(count) {
	$scope.count = count;
	$scope.search();
}

function countChange(countNew, countOld) {
	if(countOld != countNew) {
		$scope.count = countNew;
		$scope.search();
	}
}
/*分页 end*/
```