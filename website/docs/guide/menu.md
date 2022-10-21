---
title: "侧边栏菜单"
sidebar_position: 2
---

## 配置项

### * Name

`type: String;`

必传，菜单名称。

### * Url

`type: String;`

必传，点击菜单要跳转到的路由，如："/user"

:::tip

若当前配置的菜单有子菜单时，不需要设置此属性，父级菜单只提供折叠子菜单功能。

:::

### Icon

`type: String;`

菜单图标，值是 [iconfont](https://www.iconfont.cn/) 图标名称，如：“icon-xihuan”

### Children

`type: Array;`

子菜单，配置方式同此文档配置项。例如：

```js title="/src/app/config.ts"
menu: [
    {
        Name: "设置",
        Icon: "icon-gengduo",
        Children: [
            {
                Name: "权限配置",
                Url: "/permissionsSetting"
            },
            {
                Name: "系统设置",
                Url: "/systemSetting"
            }
        ]
    }
]
```
## 配置本地菜单

当配置本地菜单时，要注意 `/src/app/config.ts` 中的 `isUseServerMenu` 属性必须为 `false` ，然后在当前配置文件中找到 `menu` 属性配置本地菜单。

***注意 `menu` 属性只能作为本地菜单数据使用，且不能和服务端菜单数据混用。***

## 使用服务端菜单数据

### 第一步

将 `/src/app/config.ts` 中的 `isUseServerMenu` 属性置为 `true`。

### 第二步

找到 `/src/api/User.ts` 文件，找到 `fetchUserMenu` 方法。

```javascript title="/src/api/User.ts"
/**
 * 获取用户菜单
 */
export const fetchUserMenu = async () => {
  const menuData = await axios.get<any, ExpandRecursively<MenuItem[]>>(
    '/User/PageList'
  );
  // ... 在此处将menuData转换为符合 MenuItem[] 类型的数据。
  return menuData;
};
```

1. 修改api接口
2. 注意axios返回的菜单数据类型，确认是否是：`MenuItem[]`
3. `menuData` 即服务器菜单数据。在 `return` 时，`menuData` 必须符合类型 `MenuItem[]`。




