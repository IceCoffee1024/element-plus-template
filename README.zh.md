# Element Plus Template

基于 Vue 3 + Vite + Element Plus 的前端模板，集成文件式路由、组件按需加载、UnoCSS、SASS 主题与暗黑模式等常用能力。

[![Vue](https://img.shields.io/badge/Vue-3.x-brightgreen.svg)](https://vuejs.org/)
[![Vite](https://img.shields.io/badge/Vite-7.x-747bff.svg)](https://vitejs.dev/)
[![Element Plus](https://img.shields.io/badge/Element%20Plus-2.x-409EFF.svg)](https://element-plus.org/)
[![License](https://img.shields.io/badge/License-MIT-blue.svg)](LICENSE)

## 简介

本项目基于官方 `element-plus-vite-starter` 进行定制，目标是提供一个开箱即用、便于扩展的 Vue 3 工程基础。

## 主要特性

- Vite + Vue 3 + TypeScript
- Element Plus：通过 `unplugin-vue-components` 自动按需引入（SASS 样式）
- 文件式路由：通过 `unplugin-vue-router` 从 `src/pages` 自动生成路由与类型声明
- UnoCSS：原子化样式（包含 typography preset）
- SASS 主题定制：统一从 `src/styles/element/index.scss` 注入变量
- 暗黑模式：使用 `@vueuse/core` 的 `useDark/useToggle`，并启用 Element Plus 暗黑 CSS Vars
- ESLint：基于 `@antfu/eslint-config`（含格式化与 UnoCSS 规则）

## 快速开始

推荐使用 pnpm（项目 `package.json` 已声明 `packageManager`）。

安装依赖：

```bash
pnpm install
```

开发启动：

```bash
pnpm dev
```

构建：

```bash
pnpm build
```

预览构建产物：

```bash
pnpm preview
```

代码检查与类型检查：

```bash
pnpm lint
pnpm typecheck
```

## 项目结构

```text
.
├─ public/                     # 静态资源
├─ src/
│  ├─ assets/                   # 图片等资源
│  ├─ components/               # 组件（含 layouts）
│  │  └─ layouts/               # BaseHeader / BaseSide 等布局组件
│  ├─ composables/              # 组合式函数（如暗黑模式）
│  ├─ pages/                    # 文件式路由页面目录
│  ├─ styles/                   # 全局样式与 Element Plus 主题
│  │  ├─ element/
│  │  │  ├─ index.scss          # Element Plus 主题入口（namespace/变量）
│  │  │  └─ dark.scss           # 暗黑主题变量覆写
│  │  └─ index.scss             # 全局样式（含暗黑 css-vars 引入）
│  ├─ App.vue
│  ├─ main.ts                   # 应用入口（注册 Router / UnoCSS / 全局样式）
│  ├─ components.d.ts           # 组件自动导入声明（生成）
│  └─ typed-router.d.ts         # 路由类型声明（生成）
├─ eslint.config.js
├─ uno.config.ts
├─ vite.config.ts
└─ tsconfig.json
```

## 路由约定（文件式路由）

路由由 `src/pages` 自动生成，无需手写 routes。

示例（与当前目录一致）：

- `src/pages/index.vue` → `/`
- `src/pages/nav/2.vue` → `/nav/2`
- `src/pages/nav/1/item-1.vue` → `/nav/1/item-1`

入口处使用：

- `createRouter({ history: createWebHashHistory(), routes })`
- `routes` 来自 `vue-router/auto-routes`

路由类型声明输出到 `src/typed-router.d.ts`。

## Element Plus 主题与命名空间

- 本项目在 `src/styles/element/index.scss` 中将 Element Plus 的命名空间设置为 `ep`，并覆写部分主题变量。
- `vite.config.ts` 通过 `css.preprocessorOptions.scss.additionalData` 全局注入该主题入口，确保组件样式使用同一套变量。
- `src/styles/index.scss` 引入 `element-plus/theme-chalk/src/dark/css-vars.scss`，用于暗黑模式的 CSS 变量。

## 暗黑模式

- 逻辑：`src/composables/dark.ts`（基于 `@vueuse/core`）
- 示例：`BaseHeader` 中提供暗黑切换按钮

## 常见问题

### 如何修改别名（alias）？

在 `vite.config.ts` 中可看到 `~/` 映射到 `src/`。

### 如何修改开发端口？

当前未在 `vite.config.ts` 中显式配置端口（Vite 默认 5173）。如需修改，可在 `vite.config.ts` 增加：

```ts
export default defineConfig({
  server: {
    port: 5173,
  },
});
```

## 相关链接

- Vue 3：https://vuejs.org/
- Vite：https://vitejs.dev/
- Element Plus：https://element-plus.org/
- 上游模板：https://github.com/element-plus/element-plus-vite-starter

## 许可证

[MIT License](LICENSE)
