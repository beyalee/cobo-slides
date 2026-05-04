# cobo-slides

> Cobo 品牌 HTML 演示技能，适用于 Claude Code。  
> 一行命令安装，输入主题，Claude 自动生成符合 Cobo 官网配色的产品演示幻灯片。

---

## 安装

```bash
git clone https://github.com/beyalee/cobo-slides ~/.claude/skills/cobo-slides
```

安装后 Claude Code 会自动识别，无需重启。

---

## 使用方式

**1. 直接描述主题**，Claude 自动生成：

```
帮我做一个 Cobo MPC 钱包的客户演示
```

**2. 上传 PDF / PPT，转换为 HTML：**

```
把这份 PPT 转成 HTML @产品介绍.pdf
```

Claude 会：
1. 询问演示主题、受众、章节结构
2. 给出大纲让你确认
3. 生成完整 Cobo 品牌风格的单文件 HTML
4. 在浏览器中打开预览

---

## 生成效果

-  **黑色背景** — `#0d0d0d`，与 cobo.com 官网一致
-  **紫色高亮** — `#7C7FE8`，与官网 "trusted" 强调色相同
-  **Plus Jakarta Sans** — 简洁现代的正文字体
-  **固定顶部导航** — Logo + 章节 Tab + 页码，随滚动高亮当前章节
-  **入场动画** — 每页内容依次淡入，章节切换流畅
-  **响应式** — 桌面 / 平板 / 手机均可演示
-  **零依赖** — 单个 `.html` 文件，离线可用

---

## 导出分享

生成后 Claude 会询问是否需要：

**导出 PDF：**
```bash
bash scripts/export-pdf.sh my-deck.html
```

**部署到公网链接（Vercel）：**
```bash
bash scripts/deploy.sh my-deck.html
```

---

## 文件结构

```
cobo-slides/
├── SKILL.md              # 主技能逻辑（Claude 读取）
├── COBO_BRAND.md         # 完整品牌规范：CSS 变量 + 组件库 + 产品词汇表
├── viewport-base.css     # 强制响应式基础样式
├── html-template.md      # JS 控制器架构参考
├── animation-patterns.md # 动画片段参考
└── scripts/
    ├── deploy.sh         # 部署到 Vercel
    └── export-pdf.sh     # 导出 PDF
```

---

## 依赖

- [Claude Code](https://claude.ai/code)（需登录 Anthropic 账户）
- 生成 HTML 无需任何本地依赖
- 导出 PDF 需要 Node.js（首次运行自动安装 Playwright）
- 部署需要 Vercel CLI（`npx vercel login`）

---

## 维护

更新品牌色或新增组件，编辑 `COBO_BRAND.md` 即可。  
Claude 每次生成前都会读取最新版本。
