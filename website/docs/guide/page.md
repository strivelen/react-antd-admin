---
title: "页面"
sidebar_position: 1
---

:::tip

**约定：**页面文件应全部放到 `/src/page` 目录下，且不推荐文件夹嵌套。page下的直接子文件/子目录作为页面组件，并推荐用大驼峰命名。

:::

### step1：新建页面文件

在 `/src/page` 下创建你的页面文件，如：User.tsx, 并添加以下内容：

> ***文件名和默认导出的组件名应保持同名***

```js title="/src/page/User.tsx"
export default function User() {
  return <div> User Page </div>
}
```

当新建的页面内容较多时需要切分组件，建议新建一个页面目录（而不是页面文件），如下：

> ***明确状态归属，合理切分组件！！！*** 只用在当前页面的组件才需要放到页面目录(如：`/src/page/User/`)下，可复用的组件应该放在 `/src/component/[YOUR PUBLIC COMPONENT].js` 目录下。

```text
/page
  /User
    /index.js
    /UserInfo.tsx
    /UserOrder.tsx
```

### step2：添加路由

找到 `/src/app/routes.tsx` 文件, 添加如下内容：

```javascript title="/src/app/routes.tsx"
// 第一步：导入页面组件，例如：/src/page/User.tsx
const User = lazy(() => import('page/User'));

// 第二步：找到 routes 配置对象。
export const routes: RouteObject[] = [
  {
    path: '/user',
    element: <User />
  },
  // ... 其他页面的路由配置
  {
    path: '*',
    element: <NotFound />
  }
];

```

:::tip

路由的可配置选项见：[路由对象配置](https://reactrouter.com/en/main/hooks/use-routes)

:::

### step3：完成创建

到这里，页面的创建就完成了，现在访问：`http://localhost:3000/user` 即可看到您刚才创建的页面。