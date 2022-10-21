---
title: Table 组件
sidebar_position: 2
---

## 引入组件

```js
import Table from 'component/Table';
```

## 配置项

### * api

`type: string | { url: string; params?: object }`

必须，表格列表API。

### * columns

`type: ColumnType<any>[]`

必须，配置表格表头列。具体请参考：[antd中的Table组件columns属性](https://ant.design/components/table-cn/#Column)。

### rowKey

`type: string`

Table中dataSource的主键。

### isPagination

`type: boolean`

是否分页。

### pagerLocation

`type: TablePaginationPosition[]`

分页器位置，具体参考：[position属性](https://ant.design/components/table-cn/#pagination)

### isInvertedOrder

`type: boolean`

是否倒序排列。

### sortName

`type: string`

排序字段。

### initFilterValue

`type: object`

table初始化时携带的查询参数。

### isDefaultInit

`type: boolean`

table组件是否默认初始化。

## 组件示例

```js
<Table
  isPagination={false}
  pagerLocation={['bottomCenter']}
  sortName="Name"
  isInvertedOrder={true}
  api="/User/List"
  columns={[
    {
      title: '姓名',
      dataIndex: 'Name',
      key: 'Name'
      // sorter: true
    },
    {
      title: '创建时间',
      dataIndex: 'CreateTime',
      key: 'CreateTime'
    },
    {
      title: '操作',
      key: 'action',
      render: (text, record, index) => {
        // eslint-disable-next-line jsx-a11y/anchor-is-valid
        return <a onClick={() => console.log('查看')}>查看</a>;
      }
    }
  ]}
/>
```