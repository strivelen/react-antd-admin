---
title: "CRUDTemplate组件"
sidebar_position: 3
---

此组件快速生成一个具有表单及支持增删改查的页面，同时在此基础上也可以扩展其他功能

## 引入组件

```js
import CRUDTemplate from 'component/CRUDTemplate';
```

## 配置项

### * queryFields

`type: FieldsConfig[]`

必传，表格列表筛选条件。具体配置方式可查看 [Filter组件的 _fieldsConfig_ 属性](./filter#-fieldsconfig)

```tsx
// 例子：
<CRUDTemplate 
  queryFields={[
    {
      label: "姓名",
      fields: "Name",
      component: "Input",
      // componentProps: {},
      // defaultValue: '张三'
    },
    // ...更多字段
  ]}
/>
```

### * tableConfig

`type: TableConfig`

必传，表格配置项，具体参考[Table 组件](./table)。

```js
// 例子：
<CRUDTemplate 
  tableConfig={{
    api: "/User/List",
    columns: [
      {
        title: "姓名",
        dataIndex: "Name",
        key: "Name",
        sorter: true,
      }
    ]
  }}
/>
```

### actions

`type: FilterChildren`

非必传，此属性主要用来渲染页面级的按钮组件，如：新增，导出等。

```js
// 例子：
<CRUDTemplate 
  actions={
    <>
      <ExportAction
        option={{
          api: "",
          params: {},
        }}
        actionCom={({ onAction }) => (
          <Button
            style={{ marginLeft: 20 }}
            type="primary"
            onClick={onAction}
          >
            导出
          </Button>
        )}
      />
      {/* ... 其他按钮组件 */}
    </>
  }
/>
```
## TS类型

```ts
interface CRUDTemplateProps {
  queryFields: FieldsConfig[];
  tableConfig: TableConfig;
  actions?: FilterChildren;
}

interface FieldsConfig {
  label: string;
  component: FormItemsKeys;
  fields: string;
  componentProps?: ComPropsType[FormItemsKeys];
  defaultValue?: any;
}

interface TableConfig extends UseTableParams {
  columns: ColumnType<any>[];
  rowKey?: string;
}

interface UseTableParams {
  api: Api;
  initFilterValue?: object;
  isPagination?: boolean;
  pagerLocation?: TablePaginationPosition[];
  isInvertedOrder?: boolean;
  sortName?: string;
  isDefaultInit?: boolean;
}

type FilterChildren = ((form: FormInstance) => ReactNode) | ReactNode;
```

## 组件示例

```javascript
import CRUDTemplate, {
  AddAction,
  UpdateAction,
  DeleteAction,
  ExportAction,
  ViewAction
} from 'component/CRUDTemplate';

function UserManagePage() {
  return <CRUDTemplate
    queryFields={[
      {
        label: "姓名",
        fields: "Name",
        component: "Input",
        // componentProps: {},
        // defaultValue: '张三'
      },
      // ...更多字段
    ]}
    tableConfig={{
      api: { url: "/User/List", params: {} }, // 没有参数可以直接写为api: "/User/List"
      columns: [
        {
          title: "姓名",
          dataIndex: "Name",
          key: "Name",
          sorter: true,
        },
        {
          title: "年龄",
          dataIndex: "Age",
          key: "Age",
        },
        {
          title: "链接",
          key: "columnAction",
          render: (_) => {
            return <a>跳转</a>;
          },
        },
        {
          title: "创建时间",
          dataIndex: "CreateTime",
          key: "CreateTime",
        },
        {
          title: "操作",
          key: "action",
          render: (_, record, index) => {
            return (
              <>
                <a>查看</a>
                <Divider type="vertical" />
                <a>修改</a>
                <Divider type="vertical" />
                <a>删除</a>
              </>
            );
          },
        },
      ],
    }}
    actions={(filterForm) => {
      return (
        <>
          <AddAction
            option={{
              width: 690,
              title: "新增用户",
              submitApi: { url: "/User/Add" },
              fields: {
                Name: {
                  rules: [{ required: true, message: "请输入姓名" }],
                  label: "姓名",
                  component: "Input",
                  // initialValue: '张三'
                },
                CreateTime: {
                  // isFillLine: true,
                  component: "DatePicker",
                  componentProps: {
                    format: "YYYY-MM-DD",
                  },
                  label: "创建时间",
                  initialValue: "2023-01-01",
                },
                UserAvatar: {
                  isFillLine: true,
                  component: "SingleImgUpload",
                  componentProps: {},
                  label: "用户头像",
                  initialValue:
                    "https://i.picsum.photos/id/866/536/354.jpg?hmac=tGofDTV7tl2rprappPzKFiZ9vDh5MKj39oa2D--gqhA",
                }
              },
            }}
            actionCom={({ onAction }) => (
              <Button type="primary" onClick={onAction}>
                新增
              </Button>
            )}
          />
          <ExportAction
            option={{
              api: "",
              params: {},
            }}
            actionCom={({ onAction }) => (
              <Button
                style={{ marginLeft: 20 }}
                type="primary"
                onClick={onAction}
              >
                导出
              </Button>
            )}
          />
        </>
      );
    }}
  />
}
```
