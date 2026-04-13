# HTML模板参考文档

生成学习批注HTML时，严格遵循以下模板结构和CSS规范。

---

## 完整HTML骨架

```html
<!DOCTYPE html>
<html lang="zh-CN">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>[课程名称] · [章节主题] — 学习批注</title>
  <link href="https://fonts.googleapis.com/css2?family=Lora:ital,wght@0,400;0,600;0,700;1,400&family=IBM+Plex+Sans:wght@300;400;500;600&display=swap" rel="stylesheet">
  <style>
    /* === CSS变量 === */
    :root {
      --navy: #1B2A4A;
      --navy-light: #2C3E6B;
      --cream: #FAF8F3;
      --cream-dark: #F0EDE4;
      --text-primary: #2C2C2C;
      --text-secondary: #5A5A5A;
      --border-radius: 10px;

      /* 高亮色系 */
      --yellow-bg: #FFFBEB;  --yellow-border: #F59E0B;  --yellow-text: #92400E;
      --red-bg: #FFF1F2;     --red-border: #EF4444;     --red-text: #991B1B;
      --blue-bg: #EFF6FF;    --blue-border: #3B82F6;    --blue-text: #1E40AF;
      --green-bg: #F0FDF4;   --green-border: #22C55E;   --green-text: #166534;
      --purple-bg: #FAF5FF;  --purple-border: #A855F7;  --purple-text: #6B21A8;
    }

    * { box-sizing: border-box; margin: 0; padding: 0; }
    
    body {
      font-family: 'IBM Plex Sans', sans-serif;
      background: var(--cream);
      color: var(--text-primary);
      line-height: 1.7;
    }

    /* === 顶部导航栏 === */
    .top-nav {
      background: var(--navy);
      color: white;
      padding: 16px 32px;
      position: sticky;
      top: 0;
      z-index: 100;
      box-shadow: 0 2px 12px rgba(0,0,0,0.25);
    }
    .top-nav h1 {
      font-family: 'IBM Plex Sans', sans-serif;
      font-size: 1.1rem;
      font-weight: 600;
      margin-bottom: 10px;
    }
    .legend {
      display: flex;
      flex-wrap: wrap;
      gap: 12px;
      font-size: 0.78rem;
    }
    .legend-item {
      display: flex;
      align-items: center;
      gap: 5px;
      background: rgba(255,255,255,0.1);
      padding: 3px 8px;
      border-radius: 12px;
    }
    .legend-dot {
      width: 10px;
      height: 10px;
      border-radius: 50%;
    }
    .dot-yellow { background: #F59E0B; }
    .dot-red    { background: #EF4444; }
    .dot-blue   { background: #3B82F6; }
    .dot-green  { background: #22C55E; }
    .dot-purple { background: #A855F7; }

    /* === 章节导航条 === */
    .section-nav {
      background: var(--navy-light);
      padding: 10px 32px;
      display: flex;
      gap: 8px;
      flex-wrap: wrap;
      position: sticky;
      top: 72px;
      z-index: 99;
    }
    .section-nav a {
      color: rgba(255,255,255,0.85);
      text-decoration: none;
      font-size: 0.8rem;
      padding: 4px 12px;
      border-radius: 20px;
      border: 1px solid rgba(255,255,255,0.2);
      transition: all 0.2s;
    }
    .section-nav a:hover {
      background: rgba(255,255,255,0.15);
      color: white;
    }

    /* === 主体容器 === */
    .main-container {
      max-width: 1400px;
      margin: 0 auto;
      padding: 24px 32px;
    }

    /* === 章节标题 === */
    .section-header {
      font-family: 'IBM Plex Sans', sans-serif;
      font-size: 1.3rem;
      font-weight: 600;
      color: var(--navy);
      margin: 32px 0 16px;
      padding-bottom: 8px;
      border-bottom: 2px solid var(--navy);
    }

    /* === 双栏布局 === */
    .content-row {
      display: grid;
      grid-template-columns: 1fr 1fr;
      gap: 16px;
      margin-bottom: 16px;
      align-items: start;
    }

    /* === 左栏：原文 === */
    .original-pane {
      background: white;
      border-radius: var(--border-radius);
      padding: 20px 24px;
      box-shadow: 0 1px 6px rgba(0,0,0,0.07);
      font-family: 'Lora', serif;
      font-size: 0.92rem;
      line-height: 1.8;
    }
    .slide-label {
      font-family: 'IBM Plex Sans', sans-serif;
      font-size: 0.72rem;
      font-weight: 600;
      color: var(--navy);
      background: var(--cream-dark);
      padding: 2px 8px;
      border-radius: 4px;
      display: inline-block;
      margin-bottom: 8px;
      letter-spacing: 0.05em;
    }
    .original-pane h3 {
      font-family: 'Lora', serif;
      font-size: 1rem;
      font-weight: 700;
      color: var(--navy);
      margin-bottom: 8px;
    }
    .original-pane ul, .original-pane ol {
      padding-left: 20px;
      margin: 8px 0;
    }
    .original-pane li { margin-bottom: 4px; }

    /* 高亮样式 */
    .hl-yellow { background: #FEF3C7; border-bottom: 2px solid var(--yellow-border); padding: 0 2px; border-radius: 2px; }
    .hl-red    { background: #FEE2E2; border-bottom: 2px solid var(--red-border);    padding: 0 2px; border-radius: 2px; }
    .hl-blue   { background: #DBEAFE; border-bottom: 2px solid var(--blue-border);   padding: 0 2px; border-radius: 2px; }
    .hl-green  { background: #DCFCE7; border-bottom: 2px solid var(--green-border);  padding: 0 2px; border-radius: 2px; }
    .hl-purple { background: #F3E8FF; border-bottom: 2px solid var(--purple-border); padding: 0 2px; border-radius: 2px; }

    /* === 右栏：批注 === */
    .annotation-pane {
      display: flex;
      flex-direction: column;
      gap: 10px;
    }
    .annotation-card {
      border-radius: var(--border-radius);
      padding: 14px 16px;
      border-left: 4px solid;
      font-size: 0.85rem;
    }
    .annotation-card.yellow { background: var(--yellow-bg); border-color: var(--yellow-border); }
    .annotation-card.red    { background: var(--red-bg);    border-color: var(--red-border); }
    .annotation-card.blue   { background: var(--blue-bg);   border-color: var(--blue-border); }
    .annotation-card.green  { background: var(--green-bg);  border-color: var(--green-border); }
    .annotation-card.purple { background: var(--purple-bg); border-color: var(--purple-border); }
    .annotation-card.default { background: white; border-color: #CBD5E1; box-shadow: 0 1px 4px rgba(0,0,0,0.06); }

    .ann-label {
      font-weight: 600;
      font-size: 0.72rem;
      text-transform: uppercase;
      letter-spacing: 0.06em;
      margin-bottom: 4px;
      opacity: 0.7;
    }
    .ann-content { margin-bottom: 10px; }
    .ann-content:last-child { margin-bottom: 0; }

    .difficulty-badge {
      display: inline-block;
      font-size: 0.72rem;
      padding: 2px 7px;
      border-radius: 10px;
      font-weight: 600;
      margin-left: 4px;
    }
    .difficulty-hard   { background: #FEE2E2; color: #991B1B; }
    .difficulty-medium { background: #FEF3C7; color: #92400E; }
    .difficulty-easy   { background: #DCFCE7; color: #166534; }

    .link-tag {
      font-size: 0.75rem;
      color: var(--navy-light);
      font-style: italic;
    }

    /* 自测题 */
    .self-test {
      background: white;
      border: 1px solid #E2E8F0;
      border-radius: 8px;
      padding: 10px 14px;
      margin-top: 8px;
    }
    .self-test .q-label {
      font-weight: 600;
      font-size: 0.78rem;
      color: var(--navy);
      margin-bottom: 4px;
    }
    details summary {
      cursor: pointer;
      font-size: 0.78rem;
      color: #3B82F6;
      font-weight: 500;
      margin-top: 4px;
    }
    details[open] summary { color: #1E40AF; }
    details > div {
      margin-top: 8px;
      font-size: 0.82rem;
      padding: 8px;
      background: #F8FAFC;
      border-radius: 6px;
      border-left: 3px solid #3B82F6;
    }

    /* === 章节总结块 === */
    .chapter-summary {
      background: #F1F5F9;
      border-left: 5px solid var(--navy);
      border-radius: var(--border-radius);
      padding: 24px 28px;
      margin: 24px 0;
    }
    .chapter-summary h3 {
      font-family: 'IBM Plex Sans', sans-serif;
      font-size: 1rem;
      font-weight: 700;
      color: var(--navy);
      margin-bottom: 16px;
      display: flex;
      align-items: center;
      gap: 8px;
    }
    .summary-grid {
      display: grid;
      grid-template-columns: 1fr 1fr 1fr;
      gap: 16px;
      margin-bottom: 16px;
    }
    .summary-block {
      background: white;
      border-radius: 8px;
      padding: 14px;
      box-shadow: 0 1px 4px rgba(0,0,0,0.07);
    }
    .summary-block h4 {
      font-size: 0.75rem;
      font-weight: 700;
      color: var(--navy);
      text-transform: uppercase;
      letter-spacing: 0.05em;
      margin-bottom: 8px;
    }
    .mind-map {
      font-family: 'IBM Plex Sans', sans-serif;
      font-size: 0.83rem;
      line-height: 1.8;
    }
    .mind-map .level-1 { font-weight: 700; color: var(--navy); }
    .mind-map .level-2 { padding-left: 16px; color: #374151; }
    .mind-map .level-2::before { content: "├─ "; color: #94A3B8; }
    .mind-map .level-3 { padding-left: 32px; color: #6B7280; font-size: 0.78rem; }
    .mind-map .level-3::before { content: "└─ "; color: #CBD5E1; }
    
    .cornell-item { font-size: 0.83rem; margin-bottom: 6px; }
    .cornell-item strong { color: var(--navy); }
    
    .review-chips { display: flex; flex-wrap: wrap; gap: 6px; }
    .review-chip {
      background: var(--navy);
      color: white;
      font-size: 0.73rem;
      padding: 3px 10px;
      border-radius: 12px;
    }

    /* === 底部总览区 === */
    .overview-section {
      background: white;
      border-radius: var(--border-radius);
      padding: 28px 32px;
      margin-top: 32px;
      box-shadow: 0 2px 12px rgba(0,0,0,0.08);
    }
    .overview-section h2 {
      font-family: 'IBM Plex Sans', sans-serif;
      font-size: 1.1rem;
      font-weight: 700;
      color: var(--navy);
      margin-bottom: 20px;
      padding-bottom: 10px;
      border-bottom: 2px solid var(--cream-dark);
    }
    .overview-grid {
      display: grid;
      grid-template-columns: 1fr 1fr;
      gap: 28px;
    }
    .overview-col h3 {
      font-size: 0.88rem;
      font-weight: 700;
      color: var(--navy);
      margin-bottom: 12px;
      text-transform: uppercase;
      letter-spacing: 0.05em;
    }

    /* 速查清单 */
    .checklist-item {
      display: flex;
      align-items: flex-start;
      gap: 10px;
      padding: 8px 0;
      border-bottom: 1px solid var(--cream-dark);
      font-size: 0.85rem;
    }
    .checklist-item:last-child { border-bottom: none; }
    .checklist-item input[type="checkbox"] {
      margin-top: 3px;
      width: 16px;
      height: 16px;
      accent-color: var(--navy);
      flex-shrink: 0;
    }
    .checklist-item label { cursor: pointer; }
    .checklist-item .en-term {
      font-size: 0.75rem;
      color: var(--text-secondary);
      font-style: italic;
    }

    /* 概念索引 */
    .concept-group { margin-bottom: 16px; }
    .concept-group-title {
      font-size: 0.78rem;
      font-weight: 700;
      color: var(--navy);
      text-transform: uppercase;
      letter-spacing: 0.04em;
      margin-bottom: 6px;
    }
    .concept-item {
      padding: 6px 0;
      border-bottom: 1px solid var(--cream-dark);
      font-size: 0.83rem;
    }
    .concept-item:last-child { border-bottom: none; }
    .concept-zh { font-weight: 600; }
    .concept-en { color: var(--text-secondary); font-style: italic; font-size: 0.78rem; }
    .concept-def { color: var(--text-secondary); font-size: 0.8rem; margin-top: 2px; }

    /* === 响应式 === */
    @media (max-width: 900px) {
      .content-row { grid-template-columns: 1fr; }
      .summary-grid { grid-template-columns: 1fr; }
      .overview-grid { grid-template-columns: 1fr; }
      .top-nav { padding: 12px 16px; }
      .section-nav { top: 60px; padding: 8px 16px; }
      .main-container { padding: 16px; }
    }
  </style>
</head>
<body>

<!-- ① 顶部导航栏 -->
<nav class="top-nav">
  <h1>[课程名称] · [章节主题]</h1>
  <div class="legend">
    <span class="legend-item"><span class="legend-dot dot-yellow"></span>核心概念与定义</span>
    <span class="legend-item"><span class="legend-dot dot-red"></span>重点要求 / 高频考点</span>
    <span class="legend-item"><span class="legend-dot dot-blue"></span>数据 / 具体细节</span>
    <span class="legend-item"><span class="legend-dot dot-green"></span>操作步骤 / 格式规范</span>
    <span class="legend-item"><span class="legend-dot dot-purple"></span>方法论 / 底层原理</span>
  </div>
</nav>

<!-- ② 章节导航条 -->
<div class="section-nav">
  <a href="#section-1">§1 [章节名]</a>
  <!-- 按实际章节数量生成 -->
</div>

<!-- ③ 主体内容 -->
<div class="main-container">

  <!-- 章节标题 -->
  <h2 class="section-header" id="section-1">§1 [章节名称]</h2>

  <!-- 双栏内容行 -->
  <div class="content-row">
    <!-- 左栏：原文 -->
    <div class="original-pane">
      <span class="slide-label">Slide 1</span>
      <h3>[原文标题]</h3>
      <p>
        <span class="hl-yellow">[核心概念]</span>是指[原文内容]。
        <span class="hl-red">[高频考点内容]</span>，
        其中参数值为<span class="hl-blue">[具体数据]</span>。
      </p>
    </div>

    <!-- 右栏：批注 -->
    <div class="annotation-pane">
      <div class="annotation-card yellow">
        <div class="ann-label">📋 段落功能 / Paragraph Role</div>
        <div class="ann-content">[内容类型：核心概念 / 操作要求 / 背景信息 / 小结] — [在知识结构中的位置描述]</div>
      </div>

      <div class="annotation-card default">
        <div class="ann-label">🗝 康奈尔要点 / Key Notes</div>
        <div class="ann-content">
          <strong>关键词：</strong>[词1] · [词2] · [词3]<br>
          <strong>逻辑重心：</strong>[该段核心逻辑]<br>
          <span class="link-tag">Link to: [相关章节/概念]</span>
        </div>
      </div>

      <div class="annotation-card red">
        <div class="ann-label">⚠️ 记忆难点 / Memory Flags</div>
        <div class="ann-content">
          <strong>易错点：</strong>[容易混淆的地方]<br>
          <strong>记忆技巧：</strong>[类比/口诀/对比]<br>
          难度：<span class="difficulty-badge difficulty-hard">🔴 Hard</span>
        </div>
      </div>

      <div class="self-test">
        <div class="q-label">🧪 Self-Test</div>
        <p>Q: [核心问题]</p>
        <details>
          <summary>查看答案</summary>
          <div>[详细答案]</div>
        </details>
      </div>
    </div>
  </div>

  <!-- ④ 章节总结块（每章末尾插入） -->
  <div class="chapter-summary">
    <h3>📚 第[N]章 · 章节总结</h3>
    <div class="summary-grid">
      <!-- 思维导图 -->
      <div class="summary-block">
        <h4>🧠 知识树</h4>
        <div class="mind-map">
          <div class="level-1">[章节主题]</div>
          <div class="level-2">[一级子主题A]</div>
          <div class="level-3">[细节点a1]</div>
          <div class="level-3">[细节点a2]</div>
          <div class="level-2">[一级子主题B]</div>
          <div class="level-3">[细节点b1]</div>
        </div>
      </div>

      <!-- 康奈尔三句话 -->
      <div class="summary-block">
        <h4>✏️ 康奈尔总结</h4>
        <div class="cornell-item"><strong>What：</strong>[是什么——本章核心是什么]</div>
        <div class="cornell-item"><strong>So What：</strong>[为什么重要——对考试/实践的意义]</div>
        <div class="cornell-item"><strong>Now What：</strong>[我需要做什么——下一步行动]</div>
      </div>

      <!-- 间隔复习 -->
      <div class="summary-block">
        <h4>🔁 间隔复习提示</h4>
        <p style="font-size:0.78rem; color:#6B7280; margin-bottom:8px;">下次复习时重点检验：</p>
        <div class="review-chips">
          <span class="review-chip">[概念1]</span>
          <span class="review-chip">[概念2]</span>
          <span class="review-chip">[概念3]</span>
        </div>
      </div>
    </div>
  </div>

  <!-- ⑤ 底部全文总览区 -->
  <div class="overview-section">
    <h2>📖 全文总览</h2>
    <div class="overview-grid">
      <!-- 左列：重点速查清单 -->
      <div class="overview-col">
        <h3>✅ 重点速查清单</h3>
        <div class="checklist-item">
          <input type="checkbox" id="key1">
          <label for="key1">
            [中文描述考点]
            <br><span class="en-term">([English term])</span>
          </label>
        </div>
        <!-- 按红色高亮数量生成 -->
      </div>

      <!-- 右列：概念索引 -->
      <div class="overview-col">
        <h3>📌 概念索引</h3>
        <div class="concept-group">
          <div class="concept-group-title">[主题分类]</div>
          <div class="concept-item">
            <span class="concept-zh">[中文概念]</span>
            <span class="concept-en"> / [English Term]</span>
            <div class="concept-def">[1句话定义]</div>
          </div>
        </div>
      </div>
    </div>
  </div>

</div><!-- end main-container -->

</body>
</html>
```

---

## 内容填充指南

### 五类高亮识别规则

| 维度 | 识别特征 | 示例 |
|------|----------|------|
| 🟡 核心概念 | 带有"是指/定义为/称为"的定义句 | "均值是指数据的算术平均值" |
| 🔴 高频考点 | 带有"必须/要求/重点/注意"等强调词，或历年考点 | "必须使用APA第7版格式" |
| 🔵 具体数据 | 数字、百分比、参数名、取值范围 | "α = 0.05，n > 30" |
| 🟢 操作步骤 | 步骤化内容，带有序号或"首先/然后/最后" | "Step 1: 建立原假设" |
| 🟣 底层原理 | 解释"为什么"的方法论性内容 | "基于中心极限定理，当n足够大时…" |

### 批注难度标准

- 🔴 **Hard**：抽象原理、易混淆概念、多步推导、反直觉结论
- 🟡 **Medium**：需要记忆的流程/格式、有条件的规则
- 🟢 **Easy**：定义明确、直观、有直接对应的内容

### 段落功能分类

- **核心概念**：定义某个重要术语或原理
- **操作要求**：规定具体格式、步骤或标准
- **背景信息**：提供上下文、历史、动机
- **数据/参数**：给出具体数值或技术细节
- **小结**：汇总本节或本章内容

---

## 注意事项

1. **每个`content-row`对应一个幻灯片或一个内容块**，左右栏严格对齐
2. **批注卡片颜色**跟随该段最主要的高亮维度（如段落同时含黄色和红色，以红色为主）
3. **自测题**必须是可独立回答的封闭式问题，答案完整
4. **章节总结块**必须在每个`section-header`对应内容的最后一个`content-row`之后插入
5. **底部总览**只出现一次，在所有章节内容之后
6. **幻灯片编号**：若原材料有明确幻灯片编号则使用，否则顺序标注
7. **移动端适配**：CSS已包含响应式，无需额外处理
