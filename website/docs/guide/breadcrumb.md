---
title: 面包屑
sidebar_position: 3
---

:::tip

***侧边栏菜单绑定的页面会自动渲染面包屑，非菜单页面需要手动配置面包屑（手动配置面包屑参考: 自定义面包屑）！！！***

当然，如果侧边栏菜单绑定页面自动渲染出的面包屑不符合您的需求，则可以自定义当前菜单页面的面包屑。

:::

## 自定义面包屑

```typescript
type Breadcrumb = Array<string | { name: string; path: string }>

dispatch(setBreadcrumb(["自定义1", "自定义2"] as Breadcrumb))
```

**自定义面包屑示例：**

```javascript
import { useAppDispatch } from 'app/hooks';
import { setBreadcrumb } from 'features/layout/layoutSlice';
import { Button } from 'antd';

function CustomBreadcrumb() {
  const dispatch = useAppDispatch();
  return (
    <>
      <Button
        type="primary"
        onClick={() => {
          dispatch(
            setBreadcrumb([
              '自定义1',
              { name: '跳转至首页', path: '/' },
              '自定义3'
            ])
          );
        }}
      >
        点击改变当前页面的面包屑
      </Button>
    </>
  );
}
```
