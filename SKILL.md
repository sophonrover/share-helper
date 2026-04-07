---
name: share-helper
description: Full workflow for creating internal presentation slides — from topic selection and deep research to outline, content writing, and HTML slides generation. Triggered when users ask to prepare internal sharing materials, presentations, or knowledge-sharing sessions. Outputs a browser-ready slides.html with keyboard navigation.
version: 1.0.0
metadata:
  openclaw:
    emoji: 🎯
    homepage: https://github.com/sophonrover/share-helper
---

# Share Helper · 内部分享材料制作

面向内部受众（同事、领导、团队）制作高质量分享材料，覆盖选题→研究→大纲→内容→HTML 幻灯片全流程。

输出物：`outline.md`（大纲）、`content.md`（完整内容）、`slides.html`（可直接演示的幻灯片）。

---

## 阶段一：收集基本信息

启动时，依次确认以下三项（未确认的逐一询问）：

### 1. 分享对象

询问受众，例如：产品经理、技术团队、领导层、全员。

受众决定内容深度和风格：
- **PM / 业务受众**：落地实践、业务价值、可操作建议
- **技术受众**：原理和实现路径，可使用技术术语
- **领导 / 管理层**：战略视角、行业趋势、决策参考

### 2. 分享主题

支持两种模式，询问用户选择：

**【指定】模式**：用户直接输入主题，确认后进入阶段二。

**【推荐】模式**：用户输入大方向，按以下格式推荐 4-5 个选题：

```
推荐选题：

① [主题名称]
   为什么值得分享：[1-2句，时效性或实践价值]
   适合受众：[与用户受众的匹配程度]

② ...
```

### 3. 分享时长

默认 15 分钟，按如下规则映射内容体量：

| 时长    | 内容字数     | 建议页数 |
| ------- | ------------ | -------- |
| 10 分钟 | ~1500 字     | 8-10 页  |
| 15 分钟 | ~2500 字     | 12-15 页 |
| 20 分钟 | ~3500 字     | 16-20 页 |
| 30 分钟 | ~5000 字     | 22-28 页 |

---

## 阶段二：深度研究

三项信息确认后，**自动开始研究，无需用户额外指令**。

### 研究执行顺序

**Step 1：系统性主题研究**

使用 web search 搜索主题背景，覆盖：
- 背景与发展脉络
- 核心概念与原理
- 主要应用场景与案例
- 行业现状与关键数据

**Step 2：近期动态补充**

搜索 `[主题] 最新进展 [当前年份]`，补充：
- 最新进展与热点讨论
- 近期值得关注的案例
- 社区主流观点与争议

**Step 3：整合研究结果**

告知用户："研究完成，共收集到 [X] 条关键信息，涵盖 [主要方向]，正在生成内容大纲。"

---

## 阶段三：制作内容大纲

研究完成后，**必须先输出大纲供用户确认，不要跳过直接输出内容**。

### 大纲格式

```markdown
# [分享主题]
**受众**：[分享对象]  **时长**：[X] 分钟  **页数**：约 [X] 页

---

## 开场（约 X 分钟）
- 引发兴趣的切入点（问题/数据/场景）
- 本次分享能带走什么

## 第一部分：[章节名]（约 X 分钟）
- 要点一
- 要点二

## 第二部分：[章节名]（约 X 分钟）
...

## 总结与行动建议（约 X 分钟）
- 核心结论（3 条以内）
- 对受众的具体建议
```

输出后询问："大纲是否符合预期？确认后开始内容创作。"

---

## 阶段四：内容创作

用户确认大纲后，按以下原则创作完整内容：

- **深入浅出**：用类比、案例、数据讲清楚复杂概念
- **有观点**：不只陈述事实，给出判断和建议
- **有结构**：每个部分有明确主旨句，逻辑递进清晰
- **可操作**：结合受众工作场景，给出具体行动建议

将完整内容保存为 `content.md`，每页 slides 内容单独成节。

---

## 阶段五：生成 HTML 幻灯片

基于 `content.md` 生成 `slides.html`，直接写入文件。

### 设计要求

- 简洁专业，适合内部分享场合
- 中文字体：`"PingFang SC", "Hiragino Sans GB", "Microsoft YaHei", sans-serif`
- 每页一个核心信息点，信息密度适中
- 关键数据和结论用视觉方式突出（大字号、色块）
- 配色方案：主色 + 辅助色不超过 3 种，背景统一
- 支持键盘左右方向键翻页，显示当前页码

### HTML 结构模板

```html
<!DOCTYPE html>
<html lang="zh-CN">
<head>
  <meta charset="UTF-8">
  <title>[主题]</title>
  <style>
    * { margin: 0; padding: 0; box-sizing: border-box; }
    body {
      font-family: "PingFang SC", "Hiragino Sans GB", "Microsoft YaHei", sans-serif;
      background: #0f1117; color: #e8eaf0;
      width: 100vw; height: 100vh; overflow: hidden;
    }
    .slide {
      display: none; width: 100vw; height: 100vh;
      flex-direction: column; justify-content: center;
      align-items: center; padding: 60px 80px;
      position: absolute; top: 0; left: 0;
    }
    .slide.active { display: flex; }
    .slide-num {
      position: fixed; bottom: 20px; right: 30px;
      font-size: 14px; opacity: 0.4;
    }
    h1 { font-size: 2.8em; margin-bottom: 0.4em; }
    h2 { font-size: 2em; margin-bottom: 0.6em; }
    p, li { font-size: 1.25em; line-height: 1.7; }
    ul { text-align: left; }
    /* 根据内容自定义主题色和布局 */
  </style>
</head>
<body>

  <section class="slide active" id="slide-1">
    <!-- 封面 -->
  </section>

  <section class="slide" id="slide-2">
    <!-- 内容页 -->
  </section>

  <!-- ... 更多页面 ... -->

  <div class="slide-num">
    <span id="cur">1</span> / <span id="total"></span>
  </div>

  <script>
    const slides = document.querySelectorAll('.slide');
    let cur = 0;
    document.getElementById('total').textContent = slides.length;

    function go(n) {
      slides[cur].classList.remove('active');
      cur = (n + slides.length) % slides.length;
      slides[cur].classList.add('active');
      document.getElementById('cur').textContent = cur + 1;
    }

    document.addEventListener('keydown', e => {
      if (e.key === 'ArrowRight' || e.key === 'ArrowDown') go(cur + 1);
      if (e.key === 'ArrowLeft'  || e.key === 'ArrowUp')   go(cur - 1);
    });
  </script>
</body>
</html>
```

生成完成后告知用户：

```
✅ 分享材料制作完成！

📁 输出文件：
  • slides.html  — 在浏览器中打开，左右方向键翻页
  • content.md   — 完整文字内容（可作为讲稿参考）
  • outline.md   — 大纲

如需调整内容或风格，告诉我即可。
```

---

## 错误处理

| 情况           | 处理方式                               |
| -------------- | -------------------------------------- |
| 研究结果不足   | 告知用户并询问是否补充具体资料         |
| 用户跳过大纲   | 提醒确认大纲是重要的对齐步骤           |
| 内容与受众不符 | 重新调整风格后输出                     |

---

## 快速参考

```
用户输入示例 → 触发路径

"帮我做个关于 AI Agent 的内部分享"
→ 询问受众 → 确认主题 → 询问时长 → 研究 → 大纲 → 内容 → HTML

"我要给 PM 团队分享增长策略，30 分钟"
→ 受众已知(PM) → 主题已知 → 时长已知 → 直接研究

"推荐一些最近值得讲的 AI 话题"
→ 推荐模式 → 询问受众和大方向 → 输出推荐选题
```
