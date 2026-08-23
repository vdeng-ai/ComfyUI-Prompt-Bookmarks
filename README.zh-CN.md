# ComfyUI Prompt Bookmarks

<p align="center">
  <strong>一个轻量、零额外依赖的 ComfyUI 个人提示词整理工具。</strong><br>
  在侧边栏中收藏、分组、搜索、复制和恢复提示词，无需增加节点，也不会占用画布空间。
</p>

<p align="center">
  <a href="README.md">English</a> · <a href="README.zh-CN.md">简体中文</a>
</p>

<p align="center">
  <img alt="ComfyUI" src="https://img.shields.io/badge/ComfyUI-sidebar%20extension-5b5bd6">
  <img alt="Extra dependencies" src="https://img.shields.io/badge/extra%20dependencies-none-2ea44f">
  <img alt="Workflow nodes" src="https://img.shields.io/badge/workflow%20nodes-none-2ea44f">
  <img alt="License" src="https://img.shields.io/badge/license-MIT-blue">
</p>

## 界面预览

### 不修改工作流画布，直接收藏当前提示词

![收藏当前提示词](docs/assets/prompt-bookmarks-save-dialog.webp)

### 在侧边栏浏览提示词，并自动关联生成的图片 / 视频预览

![带视频预览的 Prompt Bookmarks 侧边栏](docs/assets/prompt-bookmarks-video-preview.webp)

## 为什么做 Prompt Bookmarks？

在 ComfyUI 里不断试提示词很方便，但真正好用的提示词经常散落在不同工作流、文本文件、聊天记录或复制粘贴片段里。

**ComfyUI Prompt Bookmarks** 只专注一件事：**在 ComfyUI 内整理和复用你自己的提示词。**

- **轻量**：不引入额外前端框架运行时，也没有复杂服务层。
- **无需额外依赖**：不需要安装额外 Python 包，后端只使用 Python 标准库，包括 `sqlite3`。
- **无需增加工作流节点**：不会往你的工作流里塞 Prompt Loader / Saver 节点。
- **不影响画布**：所有功能都放在 ComfyUI 侧边栏中。
- **专注个人整理**：它是个人提示词收藏夹 / 提示词书签，不是市场、云同步平台或团队协作系统。
- **感知工作流**：记住每个工作流真正使用的提示词字段，并可一键恢复。

如果你在找 **ComfyUI 提示词管理器、Prompt Manager、Prompt Library、Prompt Organizer、Prompt Bookmarks**，这个项目的目标就是保持简单、够用、不打扰生成流程。

## 功能

- 纯侧边栏提示词库，**不增加任何工作流节点**
- 中文 / 英文界面
- 自动跟随当前工作流，并处理默认模板 UUID 冲突场景
- 可视化提示词字段选择器，只需勾选，不需要手填节点 ID
- 自动推荐 Prompt / Text 类字段
- Note / Markdown 类节点默认不勾选
- **定位**按钮可直接跳转到提示词所在节点
- 支持普通 ComfyUI Group 路径显示
- 支持 Group Node / Subgraph 对外暴露的可编辑文本字段
- 一条收藏可同时保存多个字段，例如：
  - 主提示词
  - 运镜 / 动作提示词
  - 负面提示词
- 按 **工作流 + 分组** 整理提示词
- 空分组可安全删除
- 搜索提示词
- 匹配工作流内一键应用 / 恢复
- 所有工作流均可复制提示词
- HTTP / 局域网环境下提供剪贴板降级方案
- SQLite 持久化，数据库存放在 ComfyUI user 目录
- 生成完成后可尝试自动关联图片 / 视频预览
- 只保存媒体引用，**不会复制生成文件**

## 安装

### ComfyUI Manager

项目已经包含 Comfy Registry 所需元数据，并正在准备加入 ComfyUI Manager 搜索。收录后可以搜索：

```text
ComfyUI Prompt Bookmarks
```

或：

```text
Prompt Bookmarks
```

### 手动安装

```bash
cd /path/to/ComfyUI/custom_nodes
git clone https://github.com/vdeng-ai/ComfyUI-Prompt-Bookmarks.git
```

重启 ComfyUI，并刷新浏览器。侧边栏会出现书签图标。

**正常使用不需要执行 `pip install`，不需要 `requirements.txt`，不需要安装 Node.js 包，也不需要前端构建。**

## 快速使用

1. 在 ComfyUI 打开一个工作流。
2. 从侧边栏打开 **提示词收藏**。
3. 点击 **选择提示词字段**。
4. 勾选你希望一起收藏和恢复的文本字段。
5. 点击 **收藏当前提示词**。
6. 输入收藏名称和可选分组。
7. 后续点击 **应用** 可恢复这些字段，或点击 **复制** 在其他地方使用。

插件内部会记录 node ID 和 widget 名称用于重新定位字段，但这些只是内部实现细节，用户不需要自己管理。

## 它刻意不做什么

Prompt Bookmarks 希望保持小而专注，因此不会扩展成：

- 工作流管理器
- 模型管理器
- Prompt 市场
- 云同步服务
- AI 自动改写提示词工具

收藏项也不会同时保存 sampler、模型、seed、CFG 等生成参数；本项目专注的是你的 **Prompt 文本库**。

## Group、Group Node 与 Subgraph

当前采用保守的兼容策略：

- **普通画布 Group**：完全支持，并显示类似 `Video Generation › Character Prompt › text` 的路径。
- **Group Node / Subgraph 对外暴露的文本字段**：支持。
- **Subgraph 内部未暴露的隐藏文本字段**：不直接修改，需要先暴露到外层。

这样可以避免绑定脆弱的内部图路径，并降低 ComfyUI 前端变化带来的兼容风险。

## 语言

可从侧边栏齿轮菜单，或者 ComfyUI Application Settings 的 `PromptBookmarks` 分类中选择：

- **自动**：尽量跟随 ComfyUI / 浏览器语言
- **简体中文**
- **English**

## 自动预览关联

执行成功后，Prompt Bookmarks 可以读取 ComfyUI history，根据已经配置的提示词字段重建内容并计算 fingerprint，将匹配的生成结果关联到对应收藏。

插件**不会复制图片或视频**，数据库中只保存对 ComfyUI 原始输出文件的引用。

常见图片格式以及 MP4、WebM、MOV、MKV、M4V 视频输出均可在 ComfyUI 返回标准文件元数据时被识别。

## 数据位置

提示词数据库存放在 custom node 仓库之外：

```text
<ComfyUI user directory>/prompt_bookmarks/prompt_bookmarks.db
```

因此更新、重新拉取或重装插件仓库不会删除你的提示词收藏。

## 兼容性说明

- 自动发现针对当前/root canvas 上可编辑的字符串字段。
- Subgraph 内部隐藏字段需要先暴露。
- 支持跨工作流 **复制**。
- 为避免错误写入其他节点布局，跨工作流 **应用** 默认禁用。
- 自动媒体关联为 best-effort，不会阻塞正常生成。

## 开发

后端测试无需第三方依赖：

```bash
python -m unittest discover -s tests -v
```

前端语法检查：

```bash
for file in web/*.js; do node --check "$file"; done
```

开发路线见 [docs/DEVELOPMENT_PLAN.md](docs/DEVELOPMENT_PLAN.md)。

## Comfy Registry / Manager

Registry 元数据位于 [`pyproject.toml`](pyproject.toml)。仓库同时提供手动触发的 GitHub Actions 发布流程；维护者在配置 `REGISTRY_ACCESS_TOKEN` 后即可发布到 Comfy Registry。

ComfyUI Manager 当前处于旧节点数据库与官方 Comfy Registry 并行过渡阶段，因此项目会同时兼容两条发现/安装路径。

## License

MIT
