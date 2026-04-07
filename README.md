# share-helper

> OpenClaw skill · 内部分享材料制作工作流

一个完整的内部分享材料制作 skill，覆盖**选题 → 深度研究 → 内容大纲 → 完整内容 → HTML 幻灯片**全流程。

## 功能

- 支持指定主题或推荐选题两种模式
- 根据分享时长自动调整内容体量（5 / 10 / 15 / 20 / 30 分钟）
- 针对不同受众（PM、技术、领导层）调整内容风格
- 自动进行 web 搜索，整合背景知识与近期动态
- **多种设计风格可选**：Anthropic 极简专业风 / Apple 官网风 / 经典深色风
- 输出可在浏览器直接演示的 `slides.html`（支持键盘 + 点击翻页，平滑动画）
- **PDF 友好**：可直接通过 Chrome 打印导出 PDF，每页自动分页

## 输出文件

```
share-output/
├── outline.md    # 大纲（用户确认版）
├── content.md    # 完整内容 / 讲稿
└── slides.html   # HTML 幻灯片（浏览器直接打开，方向键翻页）
```

## 安装

```bash
# 通过 ClawHub CLI
clawdis install sophonrover/share-helper

# 或手动克隆
git clone https://github.com/sophonrover/share-helper ~/.openclaw/skills/share-helper
```

## 使用示例

```
帮我做个关于 AI Agent 的内部分享
我要给 PM 团队分享增长策略，30 分钟
推荐一些最近值得讲的 AI 话题
```

## 与 Claude Code 版本的区别

| 功能         | share-maker (Claude Code) | share-helper (OpenClaw) |
| ------------ | ------------------------- | ----------------------- |
| 研究工具     | deep-research / last30days / web-access sub-skills | 内置 web search |
| 输出格式     | HTML + PDF                | HTML only               |
| 运行环境     | Claude Code CLI           | OpenClaw                |

## License

MIT-0
