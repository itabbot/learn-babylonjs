# 最简单的 PC 网页应用（ES 模块构建版）<!-- omit in toc -->

- [1. 使用](#1-使用)
  - [1.1. 准备工作](#11-准备工作)
  - [1.2. 安装依赖](#12-安装依赖)
  - [1.3. 编译和热重载（用于开发）](#13-编译和热重载用于开发)
  - [1.4. 编译和压缩（用于生产）](#14-编译和压缩用于生产)
- [2. 理解](#2-理解)

## 1. 使用

### 1.1. 准备工作

安装 [Node.js](https://nodejs.org) 环境。

### 1.2. 安装依赖

```sh
> npm install
```

### 1.3. 编译和热重载（用于开发）

```sh
> npm run dev

VITE v4.2.1  ready in 388 ms

  ➜  Local:   http://localhost:5173/
  ➜  Network: use --host to expose
  ➜  press h to show help
```

### 1.4. 编译和压缩（用于生产）

```sh
> npm run build

vite v4.2.1 building for production...
✓ 155 modules transformed.
dist/index.html                   0.44 kB
dist/assets/index-c6f4f801.css    0.13 kB │ gzip:   0.11 kB
dist/assets/index-22cdb8c5.js   774.53 kB │ gzip: 193.95 kB

(!) Some chunks are larger than 500 kBs after minification. Consider:
- Using dynamic import() to code-split the application
- Use build.rollupOptions.output.manualChunks to improve chunking: https://rollupjs.org/configuration-options/#output-manualchunks
- Adjust chunk size limit for this warning via build.chunkSizeWarningLimit.
✓ built in 3.44s
```

## 2. 理解

- 使用 Vue3 + Vite 搭建了本项目。
- 以 `index.html` 作为入口文件，页面中定义 `canvas` 画布元素用于渲染画面，同时指向 JavaScript 源码 `./src/main.js`。
- 在 `./src/main.js` 中引入样式表 `./src/style.css`。
- 在 `./src/main.js` 中以 `./src/App.vue` 作为根组件创建 Vue 应用实例，并挂载在 `#app` 元素之上。
- 在 `./src/App.vue` 中引入 **ES 模块构建版** 的 Babylon.js。
- 通过 Babylon 相关接口对象实例化渲染引擎、场景、相机、光源，并添加各种形状，最后循环渲染到画布，并监听浏览器大小的改变调整引擎
