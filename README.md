# Forma — AI Product Design Studio

一个**可运行、可审查、可扩展**的产品设计工作台 MVP。为“人类只提出需求、体验和审批，AI 完成规范与原型工作”的开发方式设计。

> ⚠️ 当前版本是 **V0.1 离线产品原型/工作台**，不是已接入 LLM 的完整 AI SaaS。AI 在这个阶段通过阅读 `AGENTS.md` 和编辑仓库来协作。所有原型数据均为 Mock，审批记录只存当前浏览器的 localStorage。

## 界面预览

![设计工作台总览](docs/screenshots/dashboard.webp)

![功能需求与交互流程联动](docs/screenshots/feature-workbench.webp)

## 立即运行

**最简单的方式：直接双击仓库内的 `preview.html`，无需安装任何软件。**

如果希望使用模块化开发模式，Node.js 20+ 运行：

```bash
npm run dev
```

打开 **http://localhost:5173**。

或者：

```bash
python -m http.server 5173
```

然后访问 **http://localhost:5173**。支持 Chrome、Edge、Firefox 最新版。不要直接通过 `file://` 双击 HTML（浏览器会阻止部分 ES module 加载）。

## 首次体验路线

1. 打开 **功能设计 → F001 游泳准备清单**，点击流程 01–04，观察右侧原型如何切换状态；点击 **播放完整流程** 看完成动画。
2. 切换 **方案 A/B**，了解两个方案共用字段但采用不同交互。
3. 进入 **方案对比**，并排操作、选定喜欢的方案。另一个方案仍然存在。
4. 进入 **设计系统**，实时切换海洋蓝 / 薄荷绿 / 莓果紫；查看语义 Tokens、排版和动效。
5. 在 **验收与反馈** 记录意见和勾选验收条件。
6. 点击 **导出设计包**，保存一个含需求、字段、流程、验收与审批意见的 JSON。

## 包含什么

- 三个有完整产品规格的示例功能：游泳准备、自然语言创建任务、今日智能推荐
- 人类可点击的交互步骤 + 真正可运行和自动重放的原型
- 支持独立状态的 A/B 方案对比，以及审批记录
- 页面级设计系统预览与语义 Token 主题切换
- 手动审查、反馈存档和功能设计包 JSON 导出
- 工程质量检查：`npm run check`（语法校验 + 结构校验 + 组件颜色硬编码检查 + 自动构建离线版）
- `AGENTS.md` 定义 AI 编程/设计必须遵循的规则

## 工程命令

```bash
npm run dev          # 本地服务器 http://localhost:5173
npm run test         # 结构与交互模型单元测试
npm run lint:design  # CSS 硬编码颜色规则检查
npm run check        # 执行全部检查
```

## 项目结构

```text
src/
  app.js              工作台路由/页面/方案管理
  data/features.js    每个功能的需求、业务字段、交互、验收
  components/         独立可运行原型（F001/F002/F003）
  styles/tokens.css   唯一主题色彩决策源
  styles/base.css     全局基础
  styles/components.css 界面组件样式（只引用 Tokens）
  lib/                图标、持久化、规格检查
scripts/              零依赖本地服务器、设计规范检查
tests/                自动检查
docs/                 架构、工作流、路线图
AGENTS.md             AI 协作开发强制规范
```

## 重要设计取舍

- **采用零依赖原生模块**，让你先克隆即跑、无网络即可试用；保留未来迁移 React/Storybook 的明确路径。当前**不包含** React 和 Storybook，避免误导。
- “方案”与“修订”不同：A/B 保留的是交互差异，细微修改通过 Git 历史追溯。
- 主题统一通过 `src/styles/tokens.css` 修改，不允许功能组件 CSS 写死颜色。
- 字段契约只说明 UI 需要什么数据，**不代表正式业务 API 已经支持**；真实接入时需对齐 OpenAPI / TypeScript 契约。
- 此工作台是受约束的研发工具，不限制你未来面向最终用户的 Generative UI 设计能力；动态生成代码必须另外做沙箱。

## 让 AI 接手开发

请先给 AI 提示：

> 请阅读仓库中的 AGENTS.md、docs/WORKFLOW.md、docs/ARCHITECTURE.md，严格按 Feature Package 的设计流程维护项目。我提供需求和审核反馈，你负责补齐需求、业务字段、方案、可运行原型及检查。不要覆盖已批准方案，不要在功能 CSS 硬编码颜色。每次提交前运行 `npm run check` 并报告变更范围。

## 后续规划

见 [`docs/ROADMAP.md`](docs/ROADMAP.md)。

MIT License — 可自由修改与扩展。