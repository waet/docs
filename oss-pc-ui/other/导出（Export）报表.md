# 导出（Export）报表

## “导出” Methods

```javascript
// 导出

/**
 * acs: 权限码
 * title: 弹出窗口的标题
 * datItems: [{
 * 	colName: '', sn: 1, colZdm: ''
 * 	colName: '', sn: 2, colZdm: ''
 * },{
 * 	colName: '', sn: 100, colZdm: ''
 * 	colName: '', sn: 101, colZdm: ''
 * 	colName: '', sn: 102, colZdm: ''
 * }] // 每个元素 sn 不重复
 * exportUrl: 导出api
 * queryModel: 导出api的入参对象 一般和列表查询条件一样
 */
$scope.toExp = function () {
	if ($scope.tableList.length > 0) {
		var datItems = [{
			label: '信息段1',
			checked: false,
			field: [
    			{ colName: '字段1', sn: 1, colZdm: 'row1' },
    			{ colName: '字段2', sn: 2, colZdm: 'row2' }
    	    ]
		}, {
			label: '信息段2',
			checked: false,
			field: [
				{ colName: '字段3', sn: 3, colZdm: 'row3' },
				{ colName: '字段4', sn: 4, colZdm: 'row4' },
				{ colName: '字段5', sn: 5, colZdm: 'row5' }
			]
		}]
		
		common.sessionset('dataString', {
			acs: '*******',
			title: '弹出窗口标题',
			datItems: datItems,
			exportUrl: 'interface.interface',
			queryModel: {
				"acs": '210040201',
				"query1": ,
				"query2": ,
				"query3": 
			}
		});
		window.open('#/customExport', '_blank', 'width=1060px,height=660px,left=200px,top=70px;');
	} else {
		swal.warning(['无法导出！', '未查询到相关数据！']);
	}
}
```
