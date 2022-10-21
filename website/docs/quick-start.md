---
sidebar_position: 2
title: 快速开始
---

import Tabs from '@theme/Tabs';
import TabItem from '@theme/TabItem';

现在来创建一个后台管理系统网站。

### 你需要做什么

- 安装[Node.js](https://nodejs.org/en/download/)14.x或以上版本。

## 创建项目

<Tabs>
  <TabItem value="yarn" label="Yarn" default>

```bash
yarn create react-app [project-name] --template ant-admin
```
  </TabItem>
  <TabItem value="npm" label="npm">

```bash
npm create-react-app [project-name] --template ant-admin
```
  </TabItem>
</Tabs>

项目模板在下载下来后会自动安装项目依赖，因此不需要手动安装项目依赖。

#### 本地运行：

```bash
# Yarn
yarn start

# npm
npm start
```

#### 生产构建：

```bash
# Yarn
yarn build

# npm
npm build
```

构建后的生产包在项目下的 `build` 目录，有关部署的详细信息。请参阅 [部署部分](https://facebook.github.io/create-react-app/docs/deployment) 。

在开发模式下运行程序，使用浏览器打开  [http://localhost:3000](http://localhost:3000) 进行查看。

## 项目配置

### 第一步：网络请求相关配置

1. 打开 `/src/app/config.ts` 文件，找到 `apiHosts` 属性，将此属性值改为您将要使用的后台服务hosts。如：“ http://api.baidu.com/api ”。如果您的接口在请求时需要携带 `sessionkey`，那么将 `apiSessionKey` 属性的值改为您的sessionKey Name。

2. 打开 `/src/util/axios.ts` 文件，找到 `DTOModel` ts接口（此接口描述的是api返回值对象的主体结构类型），修改此 `interface` 类型并修复由此引发的当前文件产生的ts提示错误。

3. 自此就完成了网络请求相关配置。

### 第二步：登录流程相关调整

此模板自带登录页面，进入 `/src/page/Login/Login.tsx` 文件根据需求自行调整。

### 第三步：页面权限相关配置

找到 `/src/component/RequireAuth.tsx` 文件根据需求自行调整。

### ✔ 完成

走完这三步，项目相关配置完成，接下来即可进行业务开发。