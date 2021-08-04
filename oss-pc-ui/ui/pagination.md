# 分页

###### 分页是全局组件，无需引入

```html
<custom-pagination ng-show="model.postlist.length" count="model.count" page="model.pageNum" adapter="model.queryList()" total="model.total"></custom-pagination>

```

| 参数名称 |         说明         |       类型       | 默认值 |
| :------: | :------------------: | :--------------: | :----: |
|   page   |         页数         | String \| Number |   1    |
|  total   |         总数         | String \| Number |   0    |
|  count   |    每页展示的数量    | String \| Number |   0    |
| adapter  | 切换分页后的回调方法 |     Function     |  null  |

