---
title: Filter 组件
sidebar_position: 1
---

查询组件

## 引入组件

```js
import Filter from 'component/Filter';
```

## 配置项

### * fieldsConfig

`type: FieldsConfig[]`

筛选字段配置项。

```ts
interface FieldsConfig {
  label: string;
  component: FormItemsKeys;
  fields: string;
  componentProps?: ComPropsType[FormItemsKeys];
  defaultValue?: any;
}
```

:::caution

注意，在配置 _fieldsConfig_ 属性时，每个筛选字段的可配置属性只有以上定义的接口类型 `FieldsConfig` 所示，如果需要传递组件用的一些属性，必须放在 _componentProps_ 对象内。如下：

:::

```js
// 假如我们要添加一个选择销售员的Select组件：
<Filter 
  fieldsConfig={[
    {
      label: "销售",
      fields: "Sales",
      component: "Select", // Select组件相关的一些配置属性必须全部放在componentProps对象内。
      componentProps: {
        // 如果销售员的数据来源是通过网络请求获取
        enumUrl: "/Enum/Sales", 
        // 如果销售员的数据来源来自本地
        options: [
          {
            label: "张三",
            value: "1"
          },
          {
            label: "李四",
            value: "2"
          }
        ],
        // ... 其他的组件属性，如：antd中Select组件的可配置属性。
      }
    }
  ]}
/>
```

### * onSubmit

`type: (fieldsValue: FormData) => void;`

触发查询事件。

### children

`type: ((form: FormInstance) => ReactNode) | ReactNode`

Filter子元素，一般用于放置页面级相关按钮组件，如：“新增”，“导出” 等。