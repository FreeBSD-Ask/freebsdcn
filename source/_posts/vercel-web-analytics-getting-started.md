---
title: Vercel Web Analytics 入门指南
date: 2026-01-04
tags:
  - Vercel
  - Web Analytics
  - 部署
categories:
  - 教程
---

# Vercel Web Analytics 入门指南

本指南将帮助您在项目中开始使用 Vercel Web Analytics，展示如何启用它、将包添加到您的项目、将应用部署到 Vercel 以及在仪表板中查看数据。

**选择您的框架以查看在您的项目中使用 Vercel Web Analytics 的说明**。

## 前置要求

- 一个 Vercel 账户。如果您没有，可以[免费注册](https://vercel.com/signup)。
- 一个 Vercel 项目。如果您没有，可以[创建一个新项目](https://vercel.com/new)。
- 已安装 Vercel CLI。如果您没有，可以使用以下命令安装：

```bash
# 使用 pnpm
pnpm i vercel

# 使用 yarn
yarn i vercel

# 使用 npm
npm i vercel

# 使用 bun
bun i vercel
```

### 在 Vercel 中启用 Web Analytics

在 [Vercel 仪表板](/dashboard) 上，选择您的项目，然后点击 **Analytics** 标签，从对话框中点击 **Enable**。

> **💡 注意：** 启用 Web Analytics 将在您的下一次部署后添加新路由（作用域为 `/_vercel/insights/*`）。

## 为支持的框架添加 @vercel/analytics

对于以下框架：Next.js、Next.js App Router、SvelteKit、Remix、Create React App、Nuxt、Vue、Astro 等

### 将 `@vercel/analytics` 添加到您的项目

使用您选择的包管理器将 `@vercel/analytics` 包添加到您的项目：

```bash
# 使用 pnpm
pnpm i @vercel/analytics

# 使用 yarn
yarn i @vercel/analytics

# 使用 npm
npm i @vercel/analytics

# 使用 bun
bun i @vercel/analytics
```

### 将 Analytics 组件添加到您的应用

#### Next.js（Pages Router）

`Analytics` 组件是跟踪脚本的包装器，提供与 Next.js 的更无缝集成，包括路由支持。

如果您使用 `pages` 目录，请将以下代码添加到您的主应用文件：

```typescript
// pages/_app.tsx
import type { AppProps } from "next/app";
import { Analytics } from "@vercel/analytics/next";

function MyApp({ Component, pageProps }: AppProps) {
  return (
    <>
      <Component {...pageProps} />
      <Analytics />
    </>
  );
}

export default MyApp;
```

```javascript
// pages/_app.js
import { Analytics } from "@vercel/analytics/next";

function MyApp({ Component, pageProps }) {
  return (
    <>
      <Component {...pageProps} />
      <Analytics />
    </>
  );
}

export default MyApp;
```

#### Next.js（App Router）

`Analytics` 组件是跟踪脚本的包装器，提供与 Next.js 的更无缝集成，包括路由支持。

将以下代码添加到根布局：

```typescript
// app/layout.tsx
import { Analytics } from "@vercel/analytics/next";

export default function RootLayout({
  children,
}: {
  children: React.ReactNode;
}) {
  return (
    <html lang="en">
      <head>
        <title>Next.js</title>
      </head>
      <body>
        {children}
        <Analytics />
      </body>
    </html>
  );
}
```

```javascript
// app/layout.jsx
import { Analytics } from "@vercel/analytics/next";

export default function RootLayout({ children }) {
  return (
    <html lang="en">
      <head>
        <title>Next.js</title>
      </head>
      <body>
        {children}
        <Analytics />
      </body>
    </html>
  );
}
```

#### Remix

`Analytics` 组件是跟踪脚本的包装器，提供与 Remix 的无缝集成，包括路由检测。

将以下代码添加到您的根文件：

```typescript
// app/root.tsx
import {
  Links,
  LiveReload,
  Meta,
  Outlet,
  Scripts,
  ScrollRestoration,
} from "@remix-run/react";
import { Analytics } from "@vercel/analytics/remix";

export default function App() {
  return (
    <html lang="en">
      <head>
        <meta charSet="utf-8" />
        <meta name="viewport" content="width=device-width, initial-scale=1" />
        <Meta />
        <Links />
      </head>
      <body>
        <Analytics />
        <Outlet />
        <ScrollRestoration />
        <Scripts />
        <LiveReload />
      </body>
    </html>
  );
}
```

```javascript
// app/root.jsx
import {
  Links,
  LiveReload,
  Meta,
  Outlet,
  Scripts,
  ScrollRestoration,
} from "@remix-run/react";
import { Analytics } from "@vercel/analytics/remix";

export default function App() {
  return (
    <html lang="en">
      <head>
        <meta charSet="utf-8" />
        <meta name="viewport" content="width=device-width, initial-scale=1" />
        <Meta />
        <Links />
      </head>
      <body>
        <Analytics />
        <Outlet />
        <ScrollRestoration />
        <Scripts />
        <LiveReload />
      </body>
    </html>
  );
}
```

#### Nuxt

`Analytics` 组件是跟踪脚本的包装器，提供与 Nuxt 的更无缝集成，包括路由支持。

将以下代码添加到您的主组件：

```typescript
// app.vue
<script setup lang="ts">
import { Analytics } from '@vercel/analytics/nuxt';
</script>

<template>
  <Analytics />
  <NuxtPage />
</template>
```

```javascript
// app.vue
<script setup>
import { Analytics } from '@vercel/analytics/nuxt';
</script>

<template>
  <Analytics />
  <NuxtPage />
</template>
```

#### SvelteKit

`injectAnalytics` 函数是跟踪脚本的包装器，提供与 SvelteKit 的更无缝集成，包括路由支持。

将以下代码添加到主布局：

```typescript
// src/routes/+layout.ts
import { dev } from "$app/environment";
import { injectAnalytics } from "@vercel/analytics/sveltekit";

injectAnalytics({ mode: dev ? "development" : "production" });
```

```javascript
// src/routes/+layout.js
import { dev } from "$app/environment";
import { injectAnalytics } from "@vercel/analytics/sveltekit";

injectAnalytics({ mode: dev ? "development" : "production" });
```

#### Astro

`Analytics` 组件是跟踪脚本的包装器，提供与 Astro 的更无缝集成，包括路由支持。

将以下代码添加到您的基础布局：

```typescript
// src/layouts/Base.astro
---
import Analytics from '@vercel/analytics/astro';
{/* ... */}
---

<html lang="en">
  <head>
    <meta charset="utf-8" />
    <!-- ... -->
    <Analytics />
  </head>
  <body>
    <slot />
  </body>
</html>
```

> **💡 注意：** `Analytics` 组件在版本 `@vercel/analytics@1.4.0` 及更高版本中可用。
> 如果您使用的是更早版本，必须在 `astro.config.mjs` 文件中配置 Vercel 适配器的 `webAnalytics` 属性，如下面的代码所示。
> 有关更多信息，请参阅 [Astro 适配器文档](https://docs.astro.build/en/guides/integrations-guide/vercel/#webanalytics)。

```javascript
// astro.config.mjs
import { defineConfig } from "astro/config";
import vercel from "@astrojs/vercel/serverless";

export default defineConfig({
  output: "server",
  adapter: vercel({
    webAnalytics: {
      enabled: true, // 使用 @vercel/analytics@1.4.0 时设置为 false
    },
  }),
});
```

#### 纯 HTML

对于纯 HTML 网站，您可以将以下脚本添加到您的 `.html` 文件中：

```html
<!-- index.html -->
<script>
  window.va = window.va || function () { (window.vaq = window.vaq || []).push(arguments); };
</script>
<script defer src="/_vercel/insights/script.js"></script>
```

> **💡 注意：** 使用 HTML 实现时，无需安装 `@vercel/analytics` 包。但是，没有路由支持。

#### 其他框架

从包中导入 `inject` 函数，它将向您的应用添加跟踪脚本。**这应该在您的应用中仅调用一次，并且必须在客户端运行**。

> **💡 注意：** `inject` 函数不支持路由。

将以下代码添加到您的主应用文件：

```typescript
// main.ts
import { inject } from "@vercel/analytics";

inject();
```

```javascript
// main.js
import { inject } from "@vercel/analytics";

inject();
```

#### Create React App

`Analytics` 组件是跟踪脚本的包装器，提供与 React 的更无缝集成。

> **💡 注意：** 使用纯 React 实现时，没有路由支持。

将以下代码添加到主应用文件：

```typescript
// App.tsx
import { Analytics } from "@vercel/analytics/react";

export default function App() {
  return (
    <div>
      {/* ... */}
      <Analytics />
    </div>
  );
}
```

```javascript
// App.jsx
import { Analytics } from "@vercel/analytics/react";

export default function App() {
  return (
    <div>
      {/* ... */}
      <Analytics />
    </div>
  );
}
```

#### Vue

`Analytics` 组件是跟踪脚本的包装器，提供与 Vue 的更无缝集成。

> **💡 注意：** 如果您使用 `vue-router`，路由支持会自动启用。

将以下代码添加到您的主组件：

```typescript
// src/App.vue
<script setup lang="ts">
import { Analytics } from '@vercel/analytics/vue';
</script>

<template>
  <Analytics />
  <!-- your content -->
</template>
```

```javascript
// src/App.vue
<script setup>
import { Analytics } from '@vercel/analytics/vue';
</script>

<template>
  <Analytics />
  <!-- your content -->
</template>
```

## 部署您的应用到 Vercel

使用以下命令部署您的应用：

```bash
vercel deploy
```

如果您还没有这样做，我们还建议[连接您的项目的 Git 仓库](/docs/git#deploying-a-git-repository)，这将使 Vercel 能够在不使用终端命令的情况下将您的最新提交部署到 main。

一旦您的应用部署完毕，它将开始跟踪访问者和页面浏览。

> **💡 注意：** 如果一切设置正确，当您访问任何页面时，您应该能够在浏览器的 Network 标签中看到来自 `/_vercel/insights/view` 的 Fetch/XHR 请求。

## 在仪表板中查看您的数据

一旦您的应用部署完毕，并且用户访问了您的网站，您可以在仪表板中查看您的数据。

为此，请转到您的[仪表板](/dashboard)，选择您的项目，然后点击 **Analytics** 标签。

在有几天的访问者之后，您将能够开始通过查看和[过滤](/docs/analytics/filtering)面板来探索您的数据。

Pro 和 Enterprise 计划的用户还可以向其数据添加[自定义事件](/docs/analytics/custom-events)，以跟踪用户交互，例如按钮点击、表单提交或购买。

了解有关 Vercel Web Analytics 如何支持 [隐私和数据合规标准](/docs/analytics/privacy-policy) 的更多信息。

## 后续步骤

现在您已经设置了 Vercel Web Analytics，您可以探索以下主题来了解更多信息：

- [了解如何使用 `@vercel/analytics` 包](/docs/analytics/package)
- [了解如何设置自定义事件](/docs/analytics/custom-events)
- [了解数据过滤](/docs/analytics/filtering)
- [阅读隐私和合规信息](/docs/analytics/privacy-policy)
- [探索定价](/docs/analytics/limits-and-pricing)
- [故障排除](/docs/analytics/troubleshooting)
