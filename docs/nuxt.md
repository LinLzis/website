---
id: nuxt
title: Nuxt.js
sidebar_label: Introduction
---

[![Serverless Nuxtjs Tencent Cloud](https://img.serverlesscloud.cn/2020310/1583829094342-nuxt.js%20_%E9%95%BF.png)](http://serverless.com)

# 腾讯云 Nuxt.js Serverless Component

简体中文 | [English](https://github.com/serverless-components/tencent-nuxtjs/blob/v2/README.en.md)

## 简介

**腾讯云[Nuxt.js](https://github.com/nuxt/nuxt.js)组件** - 通过使用[**Tencent Serverless Framework**](https://github.com/serverless/components/tree/cloud) , 基于云上 Serverless 服务（如 API 网关、云函数等），实现“0”配置，便捷开发，极速部署采用 Nuxt.js 框架的网页应用，Nuxt.js 组件支持丰富的配置扩展，提供了目前便捷实用，开发成本低的网页应用项目的开发/托管能力。

特性介绍：

- [x] **按需付费** - 按照请求的使用量进行收费，没有请求时无需付费
- [x] **"0"配置** - 只需要关心项目代码，之后部署即可，Serverless Framework 会搞定所有配置。
- [x] **极速部署** - 部署速度快，仅需几秒，部署你的整个应用。
- [x] **实时日志** - 通过实时日志的输出查看业务状态，便于直接在云端开发应用。
- [x] **云端调试** - 可在云端直接进行项目调试，从而避免本地环境的差异。
- [x] **便捷协作** - 通过云端控制台的状态信息和部署日志，方便进行多人协作开发。

## 快速开始

0. [**准备**](#0-准备)
1. [**安装**](#1-安装)
1. [**配置**](#2-配置)
1. [**部署**](#3-部署)
1. [**开发调试**](#4-开发调试)
1. [**查看状态**](#5-查看部署状态)
1. [**移除**](#6-移除)

更多资源：

- [**账号配置**](#账号配置)
- [**更多组件**](#更多组件)
- [**FAQ**](#FAQ)

### 0. 准备

#### 初始化 Nuxt.js 项目

首先，在本地创建根目录，并初始化一个 Nuxt.js 项目

```bash
$ npx create-nuxt-app serverless-nuxtjs
$ cd serverless-nuxtjs
```

> 注意：本教程中的 Nuxt 项目使用 JavaScript 与 Npm 安装包进行构建，初始化项目的时候请选择相应的选项

### 1. 安装

通过 npm 全局安装 [serverless cli](https://github.com/serverless/serverless)

```bash
$ npm install -g serverless
```

### 2. 配置

在项目根目录创建 `serverless.yml` 文件，在其中进行如下配置

```bash
$ touch serverless.yml
```

```yml
# serverless.yml
component: nuxtjs # (必填) 组件名称，此处为nuxtjs
name: nuxtjsDemo # (必填) 实例名称
org: orgDemo # (可选) 用于记录组织信息，默认值为您的腾讯云账户 appid
app: appDemo # (可选) 该 nuxt.js 项目名称
stage: dev # (可选) 用于区分环境信息，默认值是 dev

inputs:
  src:
    src: ./
    exclude:
      - .env
  region: ap-guangzhou
  runtime: Nodejs10.15
  apigatewayConf:
    protocols:
      - http
      - https
    environment: release
```

- 点此查看[更多配置及说明](https://github.com/serverless-components/tencent-nextjs/tree/v2/docs/configure.md)

### 3. 部署

#### 3.1 构建静态资源

进入到 nuxt 项目目录下，构建静态资源

```bash
$ cd src && npm run build
```

#### 3.2 部署到云端

回到在 serverless.yml 文件所在的项目根目录，运行以下指令进行部署：

```bash
# 进入项目根目录 serverless-nuxtjs
$ sls deploy

serverless ⚡ framework
Action: "deploy" - Stage: "dev" - App: "appDemo" - Instance: "nuxtjsDemo"

region: ap-guangzhou
apigw:
  serviceId:   service-4v2jx72g
  subDomain:   service-4v2jx72g-1258834142.gz.apigw.tencentcs.com
  environment: release
  url:         https://xxxxxx.gz.apigw.tencentcs.com/release/
scf:
  functionName: nuxtjs_component_mm518kl
  runtime:      Nodejs10.15
  namespace:    default

139s › nuxtjsDemo › Success
```

部署时需要进行身份验证，如您的账号未 [登陆](https://cloud.tencent.com/login) 或 [注册](https://cloud.tencent.com/register) 腾讯云，您可以直接通过 `微信` 扫描命令行中的二维码进行授权登陆和注册。

> 注意: 如果希望查看更多部署过程的信息，可以通过`sls deploy --debug` 命令查看部署过程中的实时日志信息，`sls`是 `serverless` 命令的缩写。 `sls` 是 `serverless` 命令的简写。

### 4. 开发调试

部署了 Nuxt.js 应用后，可以通过开发调试能力对该项目进行二次开发，从而开发一个生产应用。在本地修改和更新代码后，不需要每次都运行 `serverless deploy` 命令来反复部署。你可以直接通过 `serverless dev` 命令对本地代码的改动进行检测和自动上传。

可以通过在 `serverless.yml`文件所在的目录下运行 `serverless dev` 命令开启开发调试能力。

`serverless dev` 同时支持实时输出云端日志，每次部署完毕后，对项目进行访问，即可在命令行中实时输出调用日志，便于查看业务情况和排障。

### 5. 查看部署状态

在`serverless.yml`文件所在的目录下，通过如下命令查看部署状态：

```
$ serverless info
```

### 6. 移除

在`serverless.yml`文件所在的目录下，通过以下命令移除部署通过以下命令移除部署的 API 网关，移除后该组件会对应删除云上部署时所创建的所有相关资源。

```bash
$ sls remove
```

和部署类似，支持通过 `sls remove --debug` 命令查看移除过程中的实时日志信息，`sls`是 `serverless` 命令的缩写。

### 账号配置

当前默认支持 CLI 扫描二维码登录，如您希望配置持久的环境变量/秘钥信息，也可以本地创建 `.env` 文件

```bash
$ touch .env # 腾讯云的配置信息
```

在 `.env` 文件中配置腾讯云的 SecretId 和 SecretKey 信息并保存

如果没有腾讯云账号，可以在此 [注册新账号](https://cloud.tencent.com/register)。

如果已有腾讯云账号，可以在 [API 密钥管理](https://console.cloud.tencent.com/cam/capi) 中获取 `SecretId` 和`SecretKey`.

```text
# .env
TENCENT_SECRET_ID=123
TENCENT_SECRET_KEY=123
```

> 注意：海外 ip 登录时，需要在`.env`文件中添加`SERVERLESS_PLATFORM_VENDOR=tencent` ，使 sls 默认使用 tencent 组件

## 更多组件

可以在 [Serverless Components](https://github.com/serverless/components) repo 中查询更多组件的信息。

## 项目迁移 - 自定义 express 服务

如果你的 Nuxt.js 项目本身运行就是基于 `express` 自定义服务的，那么你需要在项目中自定义入口文件 `sls.js`，需要参考你的服务启动文件进行修改，以下是一个模板文件：

```js
const path = require('path');
const express = require('express');
const {Nuxt} = require('nuxt');

// not report route for custom monitor
const noReportRoutes = ['/_next', '/static'];

async function createServer(custom) {
  const server = express();
  // get next config
  let configPath = path.join(__dirname, '..', 'nuxt.config.js');
  if (custom) {
    configPath = path.join(__dirname, 'nuxt.config.js');
  }
  const config = require(configPath);
  config.dev = false;

  // Init Nuxt.js
  const nuxt = new Nuxt(config);
  await nuxt.ready();

  // Give nuxt middleware to express
  // app.use(nuxt.render)
  server.all('*', (req, res, next) => {
    noReportRoutes.forEach((route) => {
      if (req.path.indexOf(route) === 0) {
        req.__SLS_NO_REPORT__ = true;
      }
    });
    return nuxt.render(req, res, next);
  });

  // define binary type for response
  // if includes, will return base64 encoded, very useful for images
  server.binaryTypes = ['*/*'];

  return server;
}

module.exports = createServer;
```

## 自定义监控

当在部署 Next.js 应用时，如果 `serverless.yml` 中未指定 `role`，默认会尝试绑定 `QCS_SCFExcuteRole`，并且开启自定义监控，帮助用户收集应用监控指标。对于为自定义入口文件的项目，会默认上报除含有 `/_next` 和 `/static` 的路由。如果你想自定义上报自己的路由性能，那么可以自定义 `sls.js` 入口文件，对于无需上报的路由，在 express 服务的 `req` 对象上添加 `__SLS_NO_REPORT__` 属性值为 `true` 即可。比如：

```js
server.get('/no-report', (req, res) => {
  req.__SLS_NO_REPORT__ = true;
  return handle(req, res);
});
```

那么用户在访问 `GET /no-report` 路由时，就不会上报自定义监控指标。

## License

MIT License

Copyright (c) 2020 Tencent Cloud, Inc.
