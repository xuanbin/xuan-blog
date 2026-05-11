---
title: 工具箱
date: 2026-05-11 15:00:00
updated: 2026-05-11 15:00:00
top_img: false
comments: false
toc:
  enable: true
  position: left
aside: true
---

{% raw %}
<style>
/* ====== Butterfly 适配工具箱样式 ====== */
.tb-container { max-width: 900px; margin: 0 auto; }
.tb-hero {
  text-align: center; padding: 0.6rem 0 0.8rem;
}
.tb-hero-icon {
  font-size: 1.8rem; display: inline-block;
  animation: tbBounce 2s ease infinite;
}
@keyframes tbBounce {
  0%,100% { transform: translateY(0); }
  50% { transform: translateY(-4px); }
}
.tb-hero h1 {
  font-size: 1.3rem; font-weight: 700; color: #4c1d95;
  margin: 0.3rem 0 0.4rem; letter-spacing: -0.02em;
}
.tb-hero p {
  color: #6b7280; font-size: 0.88rem; max-width: 480px; margin: 0 auto;
  line-height: 1.6;
}
.tb-tags {
  display: flex; justify-content: center; gap: 8px; margin-top: 1rem; flex-wrap: wrap;
}
.tb-tag {
  display: inline-flex; align-items: center; gap: 4px;
  padding: 5px 14px; border-radius: 20px; font-size: 0.82rem; font-weight: 500;
  background: linear-gradient(135deg, #eff6ff, #f0f9ff);
  color: #2563eb; border: 1px solid rgba(37,99,235,0.15);
}
.tb-section { margin-bottom: 2.5rem; }
.tb-section-title {
  display: flex; align-items: center; gap: 10px;
  font-size: 1.2rem; font-weight: 700; color: #1f2937;
  margin-bottom: 1rem; padding-bottom: 0.6rem;
  border-bottom: 2px solid #e5e7eb;
}
.tb-section-title .tb-sec-icon { font-size: 1.3rem; }
.tb-grid {
  display: grid; grid-template-columns: repeat(auto-fill, minmax(260px, 1fr));
  gap: 16px;
}
.tb-card {
  background: #fff; border: 1px solid #e5e7eb; border-radius: 14px;
  padding: 1.25rem; cursor: pointer; transition: all 0.25s ease;
  position: relative; overflow: hidden;
}
.tb-card:hover {
  border-color: #93c5fd; transform: translateY(-3px);
  box-shadow: 0 8px 25px rgba(59,130,246,0.12), 0 2px 8px rgba(0,0,0,0.04);
}
.tb-card::after {
  content: ''; position: absolute; top: 0; left: 0; right: 0; height: 3px;
  background: linear-gradient(90deg, var(--tb-accent, #3b82f6), var(--tb-accent2, #8b5cf6));
  opacity: 0; transition: opacity 0.25s ease;
}
.tb-card:hover::after { opacity: 1; }
.tb-card-header { display: flex; align-items: center; gap: 12px; margin-bottom: 0.75rem; }
.tb-card-icon {
  width: 44px; height: 44px; border-radius: 12px;
  display: flex; align-items: center; justify-content: center;
  font-size: 1.35rem; flex-shrink: 0;
}
.tb-card-title { font-size: 1rem; font-weight: 600; color: #1f2937; }
.tb-card-desc { font-size: 0.85rem; color: #6b7280; line-height: 1.6; margin-bottom: 0.85rem; }
.tb-card-tags { display: flex; flex-wrap: wrap; gap: 5px; }
.tb-card-tag {
  padding: 2px 10px; border-radius: 12px; font-size: 0.73rem;
  background: #f3f4f6; color: #6b7280; font-family: 'SF Mono', 'Fira Code', monospace;
}

/* ====== 工具面板样式 ====== */
.tb-tool-area { display: none; }
.tb-tool-area.active { display: block; animation: tbFadeIn 0.35s ease; }
@keyframes tbFadeIn { from{opacity:0;transform:translateY(10px);} to{opacity:1;transform:translateY(0);} }

.tb-tool-header {
  display: flex; align-items: center; gap: 12px; margin-bottom: 1.25rem;
  padding: 1rem 1.25rem; background: #fff; border: 1px solid #e5e7eb;
  border-radius: 14px;
}
.tb-back-btn {
  width: 36px; height: 36px; border-radius: 10px; border: 1px solid #d1d5db;
  background: #f9fafb; color: #6b7280; display: flex; align-items: center;
  justify-content: center; cursor: pointer; font-size: 1.1rem; transition: all 0.2s;
  text-decoration: none;
}
.tb-back-btn:hover { border-color: #3b82f6; color: #3b82f6; background: #eff6ff; }
.tb-tool-header h2 { font-size: 1.15rem; font-weight: 700; color: #1f2937; margin: 0; }

.tb-tabs { display: flex; gap: 4px; margin-bottom: 1.25rem; overflow-x: auto; padding-bottom: 4px; -webkit-overflow-scrolling: touch; }
.tb-tab {
  padding: 8px 18px; border-radius: 10px; font-size: 0.87rem; font-weight: 500;
  cursor: pointer; white-space: nowrap; transition: all 0.2s;
  background: transparent; border: 1px solid transparent; color: #6b7280;
  user-select: none;
}
.tb-tab:hover { color: #374151; background: #f3f4f6; }
.tb-tab.active { color: #2563eb; background: #eff6ff; border-color: #bfdbfe; font-weight: 600; }

.tb-panel { display: none; }
.tb-panel.active { display: block; animation: tbFadeIn 0.3s ease; }

.tb-layout { display: grid; grid-template-columns: 1fr 1fr; gap: 16px; }
@media (max-width: 768px) { .tb-layout { grid-template-columns: 1fr; } .tb-grid { grid-template-columns: 1fr; } }

.tb-box {
  background: #fff; border: 1px solid #e5e7eb; border-radius: 14px; padding: 1.15rem;
}
.tb-box-label {
  display: flex; align-items: center; justify-content: space-between;
  font-size: 0.78rem; font-weight: 600; color: #6b7280;
  text-transform: uppercase; letter-spacing: 0.04em; margin-bottom: 0.65rem;
}

textarea.tb-input, textarea.tb-output {
  width: 100%; min-height: 640px; background: #f9fafb; border: 1px solid #e5e7eb;
  border-radius: 10px; padding: 12px; color: #1f2937;
  font-family: 'SF Mono','Fira Code','Cascadia Code','Consolas',monospace;
  font-size: 0.86rem; line-height: 1.6; resize: vertical;
  outline: none; transition: all 0.2s;
}
textarea.tb-input:focus, textarea.tb-output:focus {
  border-color: #93c5fd; box-shadow: 0 0 0 3px rgba(59,130,246,0.1);
}
textarea.tb-input::placeholder { color: #9ca3af; }
.tb-output {
  min-height: 640px; color: #059669; background: #f0fdf4; border-color: #bbf7d0;
  white-space: pre-wrap; word-break: break-all;
}
.tb-output.has-content { border-color: #86efac; box-shadow: 0 0 0 3px rgba(16,185,129,0.06); }

.tb-btn-row { display: flex; gap: 8px; margin-top: 0.85rem; flex-wrap: wrap; }
.tb-btn {
  padding: 7px 18px; border-radius: 10px; font-size: 0.84rem; font-weight: 600;
  cursor: pointer; border: none; transition: all 0.2s;
  display: inline-flex; align-items: center; gap: 5px;
  font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', sans-serif;
}
.tb-btn-primary {
  background: linear-gradient(135deg, #3b82f6, #2563eb); color: #fff;
  box-shadow: 0 2px 8px rgba(59,130,246,0.25);
}
.tb-btn-primary:hover { transform: translateY(-1px); box-shadow: 0 4px 14px rgba(59,130,246,0.35); }
.tb-btn-secondary {
  background: #f3f4f6; color: #4b5563; border: 1px solid #e5e7eb;
}
.tb-btn-secondary:hover { background: #e5e7eb; color: #1f2937; }
.tb-btn-copy {
  background: #ecfdf5; color: #059669; border: 1px solid #a7f3d0; padding: 4px 12px; font-size: 0.78rem;
}
.tb-btn-copy:hover { background: #d1fae5; }

select.tb-select, input[type="number"].tb-num, input[type="text"].tb-txt {
  background: #f9fafb; border: 1px solid #e5e7eb; border-radius: 10px;
  padding: 7px 12px; color: #1f2937; font-size: 0.86rem;
  font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', sans-serif;
  outline: none; transition: all 0.2s;
}
select.tb-select:focus, input.tb-num:focus, input.tb-txt:focus {
  border-color: #93c5fd; box-shadow: 0 0 0 3px rgba(59,130,246,0.1);
}
input[type="checkbox"].tb-cb { accent-color: #3b82f6; width: 16px; height: 16px; vertical-align: middle; }
.tb-form-row { display: flex; gap: 10px; align-items: center; flex-wrap: wrap; margin-top: 0.75rem; }
.tb-form-label { font-size: 0.84rem; color: #4b5563; font-weight: 500; }

/* Toast */
.tb-toast {
  position: fixed; bottom: 1.5rem; right: 1.5rem; z-index: 99999;
  background: #059669; color: #fff;
  padding: 10px 20px; border-radius: 10px; font-size: 0.9rem; font-weight: 600;
  box-shadow: 0 4px 20px rgba(5,150,105,0.35); opacity: 0; transform: translateY(12px);
  transition: all 0.3s ease; pointer-events: none;
  letter-spacing: 0.01em;
}
.tb-toast.show { opacity: 1; transform: translateY(0); pointer-events: auto; }

/* 密码生成器特殊样式 */
.tb-pwd-result { font-family: 'SF Mono','Fira Code',monospace; font-size: 1.15rem; letter-spacing: 0.06em; color: #2563eb; word-break: break-all; }
.tb-pwd-bars { display: flex; gap: 4px; margin-top: 8px; }
.tb-pwd-bar { height: 4px; flex: 1; border-radius: 2px; background: #e5e7eb; transition: all 0.3s; }
.tb-pwd-bar.weak { background: #ef4444; }
.tb-pwd-bar.fair { background: #f59e0b; }
.tb-pwd-bar.strong { background: #22c55e; }

/* 时间戳结果 */
.tb-ts-item { display: flex; justify-content: space-between; padding: 8px 0; border-bottom: 1px solid #f3f4f6; font-size: 0.87rem; }
.tb-ts-item:last-child { border-bottom: none; }
.tb-ts-lbl { color: #6b7280; }
.tb-ts-val { font-family: 'SF Mono','Fira Code',monospace; color: #2563eb; font-weight: 500; }

/* 进制转换网格 */
.tb-conv-grid { display: grid; grid-template-columns: 1fr 1fr; gap: 10px; margin-top: 0.85rem; }
.tb-conv-item { background: #f9fafb; border: 1px solid #e5e7eb; border-radius: 10px; padding: 10px 14px; }
.tb-conv-lbl { font-size: 0.72rem; color: #9ca3af; text-transform: uppercase; letter-spacing: 0.05em; margin-bottom: 3px; }
.tb-conv-val { font-family: 'SF Mono','Fira Code',monospace; font-size: 0.92rem; color: #2563eb; word-break: break-all; }

/* 正则输入行 */
.tb-regex-row { display: flex; gap: 8px; margin-bottom: 0.85rem; }
.tb-regex-row input { flex: 1; }
.tb-flag-group { display: flex; gap: 12px; margin-bottom: 0.85rem; }
.tb-flag-label { display: flex; align-items: center; gap: 4px; font-size: 0.82rem; color: #6b7280; cursor: pointer; }

/* 统计结果 */
.tb-stat-item { display: flex; justify-content: space-between; padding: 8px 0; border-bottom: 1px solid #f3f4f6; font-size: 0.87rem; }
.tb-stat-item:last-child { border-bottom: none; }
.tb-stat-val { font-family: 'SF Mono','Fira Code',monospace; color: #2563eb; font-weight: 600; font-size: 1rem; }

/* Unix 权限 */
.tb-chmod-check { display: flex; align-items: center; gap: 6px; margin-bottom: 6px; font-size: 0.83rem; color: #4b5563; }
.tb-chmod-role { font-size: 0.78rem; color: #9ca3af; width: 42px; display: inline-block; font-weight: 600; }

/* 分类颜色变量 */
.tb-cat-encode { --tb-accent: #3b82f6; --tb-accent2: #60a5fa; }
.tb-cat-encode .tb-card-icon { background: #eff6ff; }
.tb-cat-convert { --tb-accent: #8b5cf6; --tb-accent2: #a78bfa; }
.tb-cat-convert .tb-card-icon { background: #f5f3ff; }
.tb-cat-generate { --tb-accent: #10b981; --tb-accent2: #34d399; }
.tb-cat-generate .tb-card-icon { background: #ecfdf5; }
.tb-cat-text { --tb-accent: #f59e0b; --tb-accent2: #fbbf24; }
.tb-cat-text .tb-card-icon { background: #fffbeb; }
.tb-cat-calc { --tb-accent: #ef4444; --tb-accent2: #f87171; }
.tb-cat-calc .tb-card-icon { background: #fef2f2; }

/* JSON 树形视图 */
.tb-json-tree { font-family: 'SF Mono','Fira Code','Consolas',monospace; font-size: 0.85rem; line-height: 1.8; }
.tb-json-tree .jt-children { margin-left: 20px; border-left: 1px dashed #d1d5db; padding-left: 12px; }
.tb-json-tree .jt-root { padding-left: 0; }
.tb-json-tree .jt-item { display: flex; align-items: baseline; padding: 1px 0; white-space: nowrap; }
.tb-json-tree .jt-toggle { cursor: pointer; width: 16px; height: 16px; display: inline-flex; align-items: center; justify-content: center; color: #6b7280; font-size: 0.65rem; flex-shrink: 0; user-select: none; }
.tb-json-tree .jt-toggle:hover { color: #2563eb; }
.tb-json-tree .jt-toggle.jt-collapsed::before { content: '▶'; }
.tb-json-tree .jt-toggle.jt-expanded::before { content: '▼'; }
.tb-json-tree .jt-toggle.jt-leaf { visibility: hidden; }
.tb-json-tree .jt-key { color: #7c3aed; font-weight: 500; white-space: normal; word-break: break-all; }
.tb-json-tree .jt-colon { color: #6b7280; margin: 0 4px; flex-shrink: 0; }
.tb-json-tree .jt-string { color: #059669; white-space: normal; word-break: break-all; }
.tb-json-tree .jt-number { color: #2563eb; flex-shrink: 0; }
.tb-json-tree .jt-boolean { color: #dc2626; flex-shrink: 0; }
.tb-json-tree .jt-null { color: #9ca3af; font-style: italic; flex-shrink: 0; }
.tb-json-tree .jt-bracket { color: #6b7280; flex-shrink: 0; font-weight: 600; }
.tb-json-tree .jt-count { color: #9ca3af; font-size: 0.75rem; margin-left: 4px; flex-shrink: 0; }
.tb-json-tree .jt-close-bracket { margin-left: -8px; }
.tb-json-tab { padding: 4px 14px; border-radius: 8px; font-size: 0.82rem; font-weight: 500; cursor: pointer; color: #6b7280; transition: all 0.2s; user-select: none; }
.tb-json-tab:hover { color: #374151; background: #f3f4f6; }
.tb-json-tab.active { color: #2563eb; background: #eff6ff; }

@media (max-width: 768px) {
  .tb-hero h1 { font-size: 1.1rem; }
  .tb-hero p { font-size: 0.82rem; }
  .tb-container { padding: 0 0.5rem; }
}
</style>

<div class="tb-container" id="tbApp">

  <!-- ========== 首页视图 ========== -->
  <div class="tb-view" id="tbHomeView">

    <div class="tb-hero">
      <div class="tb-hero-icon">🧰</div>
      <h1>开发者工具箱</h1>
      <p>编码转换 · 文本处理 · 密码生成 · JSON 处理 · 进制转换 · 正则测试 · 时间戳 · UUID，一站式在线工具，数据不离开你的设备 🔒</p>
    </div>

    <!-- 编码工具 -->
    <div class="tb-section">
      <div class="tb-section-title"><span class="tb-sec-icon">🔐</span> 编码工具</div>
      <div class="tb-grid tb-cat-encode">
        <div class="tb-card" onclick="tbShowTool('encode')">
          <div class="tb-card-header"><div class="tb-card-icon">{ }</div><div class="tb-card-title">JSON 格式化</div></div>
          <div class="tb-card-desc">JSON 美化、压缩、校验，支持语法高亮预览</div>
          <div class="tb-card-tags"><span class="tb-card-tag">format</span><span class="tb-card-tag">validate</span><span class="tb-card-tag">minify</span></div>
        </div>
        <div class="tb-card" onclick="tbShowTool('encode')">
          <div class="tb-card-header"><div class="tb-card-icon">🔗</div><div class="tb-card-title">URL 编解码</div></div>
          <div class="tb-card-desc">URL Encode/Decode，快速转义特殊字符</div>
          <div class="tb-card-tags"><span class="tb-card-tag">encodeURIComponent</span><span class="tb-card-tag">decodeURI</span></div>
        </div>
        <div class="tb-card" onclick="tbShowTool('encode')">
          <div class="tb-card-header"><div class="tb-card-icon">📦</div><div class="tb-card-title">Base64 编解码</div></div>
          <div class="tb-card-desc">文本与 Base64 互转，支持中文自动编码</div>
          <div class="tb-card-tags"><span class="tb-card-tag">btoa</span><span class="tb-card-tag">atob</span><span class="tb-card-tag">UTF-8</span></div>
        </div>
        <div class="tb-card" onclick="tbShowTool('encode')">
          <div class="tb-card-header"><div class="tb-card-icon">🔑</div><div class="tb-card-title">MD5 加密</div></div>
          <div class="tb-card-desc">计算字符串 MD5 哈希值，支持大小写切换</div>
          <div class="tb-card-tags"><span class="tb-card-tag">hash</span><span class="tb-card-tag">digest</span></div>
        </div>
      </div>
    </div>

    <!-- 转换工具 -->
    <div class="tb-section">
      <div class="tb-section-title"><span class="tb-sec-icon">🔄</span> 转换工具</div>
      <div class="tb-grid tb-cat-convert">
        <div class="tb-card" onclick="tbShowTool('convert')">
          <div class="tb-card-header"><div class="tb-card-icon">🕐</div><div class="tb-card-title">时间戳转换</div></div>
          <div class="tb-card-desc">Unix 时间戳 ↔ 日期时间 双向转换</div>
          <div class="tb-card-tags"><span class="tb-card-tag">timestamp</span><span class="tb-card-tag">ISO 8601</span></div>
        </div>
        <div class="tb-card" onclick="tbShowTool('convert')">
          <div class="tb-card-header"><div class="tb-card-icon">🔢</div><div class="tb-card-title">进制转换</div></div>
          <div class="tb-card-desc">二进制/八进制/十进制/十六进制互转</div>
          <div class="tb-card-tags"><span class="tb-card-tag">bin</span><span class="tb-card-tag">oct</span><span class="tb-card-tag">hex</span></div>
        </div>
      </div>
    </div>

    <!-- 生成工具 -->
    <div class="tb-section">
      <div class="tb-section-title"><span class="tb-sec-icon">🎲</span> 生成工具</div>
      <div class="tb-grid tb-cat-generate">
        <div class="tb-card" onclick="tbShowTool('generate')">
          <div class="tb-card-header"><div class="tb-card-icon">🔐</div><div class="tb-card-title">随机密码</div></div>
          <div class="tb-card-desc">自定义长度和字符类型，带强度指示器</div>
          <div class="tb-card-tags"><span class="tb-card-tag">secure</span><span class="tb-card-tag">customizable</span></div>
        </div>
        <div class="tb-card" onclick="tbShowTool('generate')">
          <div class="tb-card-header"><div class="tb-card-icon">🆔</div><div class="tb-card-title">UUID 生成</div></div>
          <div class="tb-card-desc">批量生成 UUID v4，支持格式自定义</div>
          <div class="tb-card-tags"><span class="tb-card-tag">v4</span><span class="tb-card-tag">batch</span></div>
        </div>
      </div>
    </div>

    <!-- 文本工具 -->
    <div class="tb-section">
      <div class="tb-section-title"><span class="tb-sec-icon">📝</span> 文本工具</div>
      <div class="tb-grid tb-cat-text">
        <div class="tb-card" onclick="tbShowTool('text')">
          <div class="tb-card-header"><div class="tb-card-icon">🔍</div><div class="tb-card-title">正则表达式测试</div></div>
          <div class="tb-card-desc">实时测试正则匹配，支持 g/i/m 标志位</div>
          <div class="tb-card-tags"><span class="tb-card-tag">regex</span><span class="tb-card-tag">test</span><span class="tb-card-tag">match</span></div>
        </div>
        <div class="tb-card" onclick="tbShowTool('text')">
          <div class="tb-card-header"><div class="tb-card-icon">📊</div><div class="tb-card-title">文本对比 Diff</div></div>
          <div class="tb-card-desc">两段文本逐行对比，高亮差异部分</div>
          <div class="tb-card-tags"><span class="tb-card-tag">diff</span><span class="tb-card-tag">compare</span></div>
        </div>
        <div class="tb-card" onclick="tbShowTool('text')">
          <div class="tb-card-header"><div class="tb-card-icon">📏</div><div class="tb-card-title">字数统计</div></div>
          <div class="tb-card-desc">字符数、单词数、行数、中文字数实时统计</div>
          <div class="tb-card-tags"><span class="tb-card-tag">counter</span><span class="tb-card-tag">chinese</span></div>
        </div>
      </div>
    </div>

    <!-- 计算工具 -->
    <div class="tb-section">
      <div class="tb-section-title"><span class="tb-sec-icon">🧮</span> 计算工具</div>
      <div class="tb-grid tb-cat-calc">
        <div class="tb-card" onclick="tbShowTool('calculate')">
          <div class="tb-card-header"><div class="tb-card-icon">📏</div><div class="tb-card-title">单位换算</div></div>
          <div class="tb-card-desc">长度、重量、温度等常用单位互相换算</div>
          <div class="tb-card-tags"><span class="tb-card-tag">length</span><span class="tb-card-tag">weight</span><span class="tb-card-tag">temp</span></div>
        </div>
        <div class="tb-card" onclick="tbShowTool('calculate')">
          <div class="tb-card-header"><div class="tb-card-icon">🖥️</div><div class="tb-card-title">Unix 权限计算</div></div>
          <div class="tb-card-desc">数字权限 ↔ 符号权限 ↔ chmod 命令</div>
          <div class="tb-card-tags"><span class="tb-card-tag">chmod</span><span class="tb-card-tag">rwx</span><span class="tb-card-tag">777</span></div>
        </div>
      </div>
    </div>

  </div><!-- /tbHomeView -->

  <!-- ========== 编码工具面板 ========== -->
  <div class="tb-tool-area" id="tbEncodeArea">
    <div class="tb-tool-header">
      <a class="tb-back-btn" onclick="tbShowHome()" title="返回首页">←</a>
      <span style="font-size:1.3rem;">🔐</span>
      <h2>编码工具</h2>
    </div>
    <div class="tb-tabs">
      <div class="tb-tab active" data-panel="tbJsonPanel">JSON 格式化</div>
      <div class="tb-tab" data-panel="tbUrlPanel">URL 编解码</div>
      <div class="tb-tab" data-panel="tbB64Panel">Base64</div>
      <div class="tb-tab" data-panel="tbMd5Panel">MD5 加密</div>
    </div>

    <!-- JSON -->
    <div class="tb-panel active" id="tbJsonPanel">
      <div class="tb-layout">
        <div class="tb-box">
          <div class="tb-box-label">输入 JSON</div>
          <textarea class="tb-input" id="tbJsonIn" placeholder='{"name": "DevToolbox", "version": "1.0"}'></textarea>
          <div class="tb-btn-row">
            <button class="tb-btn tb-btn-primary" onclick="tbJsonFmt()">✨ 格式化</button>
            <button class="tb-btn tb-btn-secondary" onclick="tbJsonMin()">📦 压缩</button>
            <button class="tb-btn tb-btn-secondary" onclick="tbJsonVal()">✅ 校验</button>
          </div>
        </div>
        <div class="tb-box">
          <div class="tb-box-label"><span>输出结果</span><button class="tb-btn tb-btn-copy" onclick="tbCopy('tbJsonOut',this)">复制</button></div>
          <textarea class="tb-output" id="tbJsonOut" readonly placeholder="等待输入..."></textarea>
          <div id="tbJsonTree" style="display:none;overflow:auto;max-height:800px;margin-top:8px;"></div>
          <div style="display:flex;gap:4px;margin-top:8px;">
            <span class="tb-json-tab active" id="tbJsonTabText" onclick="tbJsonView('text')">📄 文本</span>
            <span class="tb-json-tab" id="tbJsonTabTree" onclick="tbJsonView('tree')">🌳 树形</span>
          </div>
        </div>
      </div>
    </div>

    <!-- URL -->
    <div class="tb-panel" id="tbUrlPanel">
      <div class="tb-layout">
        <div class="tb-box">
          <div class="tb-box-label">输入文本</div>
          <textarea class="tb-input" id="tbUrlIn" placeholder="https://example.com?q=你好&lang=zh"></textarea>
          <div class="tb-btn-row">
            <button class="tb-btn tb-btn-primary" onclick="tbUrlEnc()">🔗 URL 编码</button>
            <button class="tb-btn tb-btn-secondary" onclick="tbUrlDec()">🔓 URL 解码</button>
          </div>
        </div>
        <div class="tb-box">
          <div class="tb-box-label"><span>输出结果</span><button class="tb-btn tb-btn-copy" onclick="tbCopy('tbUrlOut',this)">复制</button></div>
          <textarea class="tb-output" id="tbUrlOut" readonly placeholder="等待输入..."></textarea>
        </div>
      </div>
    </div>

    <!-- Base64 -->
    <div class="tb-panel" id="tbB64Panel">
      <div class="tb-layout">
        <div class="tb-box">
          <div class="tb-box-label">输入文本</div>
          <textarea class="tb-input" id="tbB64In" placeholder="Hello 世界！"></textarea>
          <div class="tb-btn-row">
            <button class="tb-btn tb-btn-primary" onclick="tbB64Enc()">📦 编码</button>
            <button class="tb-btn tb-btn-secondary" onclick="tbB64Dec()">📂 解码</button>
          </div>
        </div>
        <div class="tb-box">
          <div class="tb-box-label"><span>输出结果</span><button class="tb-btn tb-btn-copy" onclick="tbCopy('tbB64Out',this)">复制</button></div>
          <textarea class="tb-output" id="tbB64Out" readonly placeholder="等待输入..."></textarea>
        </div>
      </div>
    </div>

    <!-- MD5 -->
    <div class="tb-panel" id="tbMd5Panel">
      <div class="tb-layout">
        <div class="tb-box">
          <div class="tb-box-label">输入文本</div>
          <textarea class="tb-input" id="tbMd5In" placeholder="输入要计算 MD5 的文本..."></textarea>
          <div class="tb-btn-row"><button class="tb-btn tb-btn-primary" onclick="tbMd5Calc()">🔑 计算 MD5</button></div>
          <div class="tb-form-row" style="margin-top:10px;"><label class="tb-form-label"><input type="checkbox" class="tb-cb" id="tbMd5Up" onchange="tbMd5Calc()"> 大写输出</label></div>
        </div>
        <div class="tb-box">
          <div class="tb-box-label"><span>MD5 结果</span><button class="tb-btn tb-btn-copy" onclick="tbCopy('tbMd5Out',this)">复制</button></div>
          <textarea class="tb-output" id="tbMd5Out" readonly placeholder="等待输入..." style="font-size:1rem;letter-spacing:0.08em;"></textarea>
        </div>
      </div>
    </div>
  </div><!-- /tbEncodeArea -->

  <!-- ========== 转换工具面板 ========== -->
  <div class="tb-tool-area" id="tbConvertArea">
    <div class="tb-tool-header">
      <a class="tb-back-btn" onclick="tbShowHome()" title="返回首页">←</a>
      <span style="font-size:1.3rem;">🔄</span>
      <h2>转换工具</h2>
    </div>
    <div class="tb-tabs">
      <div class="tb-tab active" data-panel="tbTsPanel">时间戳转换</div>
      <div class="tb-tab" data-panel="tbBasePanel">进制转换</div>
    </div>

    <!-- 时间戳 -->
    <div class="tb-panel active" id="tbTsPanel">
      <div class="tb-layout">
        <div class="tb-box">
          <div class="tb-box-label">时间戳 → 日期</div>
          <input type="text" class="tb-txt" id="tbTsIn" placeholder="如 1715400000" style="width:100%;padding:10px 14px;font-size:0.95rem;border-radius:10px;">
          <div class="tb-btn-row">
            <button class="tb-btn tb-btn-primary" onclick="tbTsToDate()">🕐 转换</button>
            <button class="tb-btn tb-btn-secondary" onclick="tbTsNow()">⏱️ 当前时间戳</button>
          </div>
          <div class="tb-box-label" style="margin-top:1.1rem;">日期 → 时间戳</div>
          <input type="text" class="tb-txt" id="tbDateIn" placeholder="如 2026-05-11 15:30:00" style="width:100%;padding:10px 14px;font-size:0.95rem;border-radius:10px;">
          <div class="tb-btn-row">
            <button class="tb-btn tb-btn-primary" onclick="tbDateToTs()">🕐 转换</button>
            <button class="tb-btn tb-btn-secondary" onclick="tbDateNow()">📅 当前日期</button>
          </div>
        </div>
        <div class="tb-box">
          <div class="tb-box-label">转换结果</div>
          <div id="tbTsOut"></div>
        </div>
      </div>
    </div>

    <!-- 进制 -->
    <div class="tb-panel" id="tbBasePanel">
      <div class="tb-layout">
        <div class="tb-box">
          <div class="tb-box-label">输入数值</div>
          <input type="text" class="tb-txt" id="tbBaseIn" placeholder="如 255 或 FF" style="width:100%;padding:10px 14px;font-size:0.95rem;border-radius:10px;">
          <div class="tb-form-row">
            <label class="tb-form-label">当前进制:</label>
            <select class="tb-select" id="tbBaseFrom">
              <option value="10" selected>十进制 (10)</option>
              <option value="2">二进制 (2)</option>
              <option value="8">八进制 (8)</option>
              <option value="16">十六进制 (16)</option>
            </select>
          </div>
          <div class="tb-btn-row"><button class="tb-btn tb-btn-primary" onclick="tbBaseConv()">🔄 转换</button></div>
        </div>
        <div class="tb-box">
          <div class="tb-box-label">转换结果</div>
          <div class="tb-conv-grid" id="tbBaseOut">
            <div class="tb-conv-item"><div class="tb-conv-lbl">二进制 (2)</div><div class="tb-conv-val" id="tbBinVal">—</div></div>
            <div class="tb-conv-item"><div class="tb-conv-lbl">八进制 (8)</div><div class="tb-conv-val" id="tbOctVal">—</div></div>
            <div class="tb-conv-item"><div class="tb-conv-lbl">十进制 (10)</div><div class="tb-conv-val" id="tbDecVal">—</div></div>
            <div class="tb-conv-item"><div class="tb-conv-lbl">十六进制 (16)</div><div class="tb-conv-val" id="tbHexVal">—</div></div>
          </div>
        </div>
      </div>
    </div>
  </div><!-- /tbConvertArea -->

  <!-- ========== 生成工具面板 ========== -->
  <div class="tb-tool-area" id="tbGenerateArea">
    <div class="tb-tool-header">
      <a class="tb-back-btn" onclick="tbShowHome()" title="返回首页">←</a>
      <span style="font-size:1.3rem;">🎲</span>
      <h2>生成工具</h2>
    </div>
    <div class="tb-tabs">
      <div class="tb-tab active" data-panel="tbPwdPanel">随机密码</div>
      <div class="tb-tab" data-panel="tbUuidPanel">UUID 生成</div>
    </div>

    <!-- 密码 -->
    <div class="tb-panel active" id="tbPwdPanel">
      <div class="tb-layout">
        <div class="tb-box">
          <div class="tb-box-label">密码配置</div>
          <div class="tb-form-row"><label class="tb-form-label">长度:</label><input type="number" class="tb-num" id="tbPwdLen" value="16" min="4" max="128" style="width:80px;"></div>
          <div class="tb-form-row" style="margin-top:10px;"><label class="tb-form-label"><input type="checkbox" class="tb-cb" id="tbPwdUp" checked> 大写字母 A-Z</label></div>
          <div class="tb-form-row"><label class="tb-form-label"><input type="checkbox" class="tb-cb" id="tbPwdLo" checked> 小写字母 a-z</label></div>
          <div class="tb-form-row"><label class="tb-form-label"><input type="checkbox" class="tb-cb" id="tbPwdNu" checked> 数字 0-9</label></div>
          <div class="tb-form-row"><label class="tb-form-label"><input type="checkbox" class="tb-cb" id="tbPwdSy"> 特殊符号 !@#$...</label></div>
          <div class="tb-btn-row">
            <button class="tb-btn tb-btn-primary" onclick="tbGenPwd()">🎲 生成密码</button>
            <button class="tb-btn tb-btn-secondary" onclick="tbGenPwd()">🔄 重新生成</button>
          </div>
        </div>
        <div class="tb-box">
          <div class="tb-box-label"><span>生成结果</span><button class="tb-btn tb-btn-copy" onclick="tbCopy('tbPwdOut',this)">复制</button></div>
          <div class="tb-output tb-pwd-result" id="tbPwdOut" style="min-height:auto;padding:18px;text-align:center;">点击「生成密码」开始 ✨</div>
          <div class="tb-pwd-bars" id="tbPwdBars"><div class="tb-pwd-bar"></div><div class="tb-pwd-bar"></div><div class="tb-pwd-bar"></div><div class="tb-pwd-bar"></div></div>
        </div>
      </div>
    </div>

    <!-- UUID -->
    <div class="tb-panel" id="tbUuidPanel">
      <div class="tb-layout">
        <div class="tb-box">
          <div class="tb-box-label">UUID 配置</div>
          <div class="tb-form-row"><label class="tb-form-label">数量:</label><input type="number" class="tb-num" id="tbUuidCnt" value="5" min="1" max="20" style="width:80px;"></div>
          <div class="tb-form-row" style="margin-top:10px;">
            <label class="tb-form-label"><input type="checkbox" class="tb-cb" id="tbUuidUp"> 大写</label>
            <label class="tb-form-label" style="margin-left:16px;"><input type="checkbox" class="tb-cb" id="tbUuidNoDash"> 去掉连字符</label>
          </div>
          <div class="tb-btn-row"><button class="tb-btn tb-btn-primary" onclick="tbGenUuid()">🆔 生成 UUID</button></div>
        </div>
        <div class="tb-box">
          <div class="tb-box-label"><span>生成结果</span><button class="tb-btn tb-btn-copy" onclick="tbCopy('tbUuidOut',this)">复制全部</button></div>
          <textarea class="tb-output" id="tbUuidOut" readonly placeholder="点击「生成 UUID」开始" style="min-height:180px;"></textarea>
        </div>
      </div>
    </div>
  </div><!-- /tbGenerateArea -->

  <!-- ========== 文本工具面板 ========== -->
  <div class="tb-tool-area" id="tbTextArea">
    <div class="tb-tool-header">
      <a class="tb-back-btn" onclick="tbShowHome()" title="返回首页">←</a>
      <span style="font-size:1.3rem;">📝</span>
      <h2>文本工具</h2>
    </div>
    <div class="tb-tabs">
      <div class="tb-tab active" data-panel="tbRegexPanel">正则表达式</div>
      <div class="tb-tab" data-panel="tbDiffPanel">文本对比</div>
      <div class="tb-tab" data-panel="tbCounterPanel">字数统计</div>
    </div>

    <!-- 正则 -->
    <div class="tb-panel active" id="tbRegexPanel">
      <div class="tb-layout">
        <div class="tb-box">
          <div class="tb-box-label">正则表达式</div>
          <div class="tb-regex-row"><input type="text" class="tb-txt" id="tbRegexPat" placeholder="如 \\d+ 或 ^[a-z]+$" style="flex:1;padding:10px 14px;font-size:0.95rem;border-radius:10px;"></div>
          <div class="tb-flag-group">
            <label class="tb-flag-label"><input type="checkbox" class="tb-cb" id="tbFlgG" checked> g 全局</label>
            <label class="tb-flag-label"><input type="checkbox" class="tb-cb" id="tbFlgI"> i 忽略大小写</label>
            <label class="tb-flag-label"><input type="checkbox" class="tb-cb" id="tbFlgM"> m 多行</label>
          </div>
          <div class="tb-box-label">测试文本</div>
          <textarea class="tb-input" id="tbRegexTxt" placeholder="粘贴要测试的文本..."></textarea>
          <div class="tb-btn-row"><button class="tb-btn tb-btn-primary" onclick="tbRegexTest()">🔍 测试匹配</button></div>
        </div>
        <div class="tb-box">
          <div class="tb-box-label">匹配结果</div>
          <textarea class="tb-output" id="tbRegexOut" readonly placeholder="输入正则和测试文本后点击「测试匹配」"></textarea>
        </div>
      </div>
    </div>

    <!-- Diff -->
    <div class="tb-panel" id="tbDiffPanel">
      <div class="tb-layout">
        <div class="tb-box">
          <div class="tb-box-label">原始文本 (A)</div>
          <textarea class="tb-input" id="tbDiffA"></textarea>
        </div>
        <div class="tb-box">
          <div class="tb-box-label">修改文本 (B)</div>
          <textarea class="tb-input" id="tbDiffB"></textarea>
          <div class="tb-btn-row"><button class="tb-btn tb-btn-primary" onclick="tbTextDiff()">📊 对比</button></div>
          <div class="tb-box-label" style="margin-top:1rem;">对比结果</div>
          <textarea class="tb-output" id="tbDiffOut" readonly placeholder="输入文本 A 和 B 后点击「对比」" style="min-height:120px;"></textarea>
        </div>
      </div>
    </div>

    <!-- 统计 -->
    <div class="tb-panel" id="tbCounterPanel">
      <div class="tb-layout">
        <div class="tb-box">
          <div class="tb-box-label">输入文本</div>
          <textarea class="tb-input" id="tbCntInput" oninput="tbUpdateCount()"></textarea>
        </div>
        <div class="tb-box">
          <div class="tb-box-label">统计结果</div>
          <div id="tbCntOut">
            <div class="tb-stat-item"><span class="tb-ts-lbl">字符数 (含空格)</span><span class="tb-stat-val" id="tbCntChars">0</span></div>
            <div class="tb-stat-item"><span class="tb-ts-lbl">字符数 (无空格)</span><span class="tb-stat-val" id="tbCntNoSp">0</span></div>
            <div class="tb-stat-item"><span class="tb-ts-lbl">单词数</span><span class="tb-stat-val" id="tbCntWords">0</span></div>
            <div class="tb-stat-item"><span class="tb-ts-lbl">行数</span><span class="tb-stat-val" id="tbCntLines">0</span></div>
            <div class="tb-stat-item"><span class="tb-ts-lbl">中文字数</span><span class="tb-stat-val" id="tbCntZh">0</span></div>
          </div>
        </div>
      </div>
    </div>
  </div><!-- /tbTextArea -->

  <!-- ========== 计算工具面板 ========== -->
  <div class="tb-tool-area" id="tbCalcArea">
    <div class="tb-tool-header">
      <a class="tb-back-btn" onclick="tbShowHome()" title="返回首页">←</a>
      <span style="font-size:1.3rem;">🧮</span>
      <h2>计算工具</h2>
    </div>
    <div class="tb-tabs">
      <div class="tb-tab active" data-panel="tbUnitPanel">单位换算</div>
      <div class="tb-tab" data-panel="tbChmodPanel">Unix 权限</div>
    </div>

    <!-- 单位换算 -->
    <div class="tb-panel active" id="tbUnitPanel">
      <div class="tb-layout">
        <div class="tb-box">
          <div class="tb-box-label">单位换算</div>
          <div class="tb-form-row">
            <label class="tb-form-label">类型:</label>
            <select class="tb-select" id="tbUnitType" onchange="tbPopUnits()">
              <option value="length">长度</option>
              <option value="weight">重量</option>
              <option value="temp">温度</option>
            </select>
          </div>
          <div class="tb-form-row" style="margin-top:10px;">
            <input type="number" class="tb-num" id="tbUnitVal" value="1" style="width:110px;padding:8px 12px;">
            <select class="tb-select" id="tbUnitFrom" onchange="tbUnitConv()"></select>
            <span style="color:#9ca3af;">→</span>
            <select class="tb-select" id="tbUnitTo" onchange="tbUnitConv()"></select>
          </div>
          <div class="tb-btn-row"><button class="tb-btn tb-btn-primary" onclick="tbUnitConv()">🔄 换算</button></div>
        </div>
        <div class="tb-box">
          <div class="tb-box-label">换算结果</div>
          <div class="tb-output" id="tbUnitOut" style="min-height:120px;display:flex;align-items:center;justify-content:center;font-size:1.15rem;color:#2563eb;background:#eff6ff;border-color:#bfdbfe;">输入数值开始换算</div>
        </div>
      </div>
    </div>

    <!-- Unix 权限 -->
    <div class="tb-panel" id="tbChmodPanel">
      <div class="tb-layout">
        <div class="tb-box">
          <div class="tb-box-label">Unix 文件权限</div>
          <div class="tb-form-row"><label class="tb-form-label">权限值 (0-777):</label><input type="text" class="tb-txt" id="tbChmodIn" placeholder="如 755" maxlength="3" style="width:90px;" oninput="tbChmodCalc()"></div>
          <div class="tb-form-row" style="margin-top:10px;"><label class="tb-form-label">或勾选权限:</label></div>
          <div style="margin-top:8px;">
            <div class="tb-chmod-check"><span class="tb-chmod-role">拥有者</span><label class="tb-flag-label"><input type="checkbox" class="tb-cb" id="tbCoR" onchange="tbChmodFromCb()"> r</label><label class="tb-flag-label"><input type="checkbox" class="tb-cb" id="tbCoW" onchange="tbChmodFromCb()"> w</label><label class="tb-flag-label"><input type="checkbox" class="tb-cb" id="tbCoX" onchange="tbChmodFromCb()"> x</label></div>
            <div class="tb-chmod-check"><span class="tb-chmod-role">群组</span><label class="tb-flag-label"><input type="checkbox" class="tb-cb" id="tbCgR" onchange="tbChmodFromCb()"> r</label><label class="tb-flag-label"><input type="checkbox" class="tb-cb" id="tbCgW" onchange="tbChmodFromCb()"> w</label><label class="tb-flag-label"><input type="checkbox" class="tb-cb" id="tbCgX" onchange="tbChmodFromCb()"> x</label></div>
            <div class="tb-chmod-check"><span class="tb-chmod-role">其他</span><label class="tb-flag-label"><input type="checkbox" class="tb-cb" id="tbCaR" onchange="tbChmodFromCb()"> r</label><label class="tb-flag-label"><input type="checkbox" class="tb-cb" id="tbCaW" onchange="tbChmodFromCb()"> w</label><label class="tb-flag-label"><input type="checkbox" class="tb-cb" id="tbCaX" onchange="tbChmodFromCb()"> x</label></div>
          </div>
          <div class="tb-btn-row"><button class="tb-btn tb-btn-primary" onclick="tbChmodCalc()">🖥️ 计算</button></div>
        </div>
        <div class="tb-box">
          <div class="tb-box-label">计算结果</div>
          <div id="tbChmodOut">
            <div class="tb-stat-item"><span class="tb-ts-lbl">数字权限</span><span class="tb-stat-val" id="tbChmodNum">—</span></div>
            <div class="tb-stat-item"><span class="tb-ts-lbl">符号权限</span><span class="tb-stat-val" id="tbChmodSym" style="font-family:'SF Mono','Fira Code',monospace;">—</span></div>
            <div class="tb-stat-item"><span class="tb-ts-lbl">chmod 命令</span><span class="tb-stat-val" id="tbChmodCmd" style="font-size:0.88rem;">—</span></div>
          </div>
        </div>
      </div>
    </div>
  </div><!-- /tbCalcArea -->

</div><!-- /tbApp -->

<div class="tb-toast" id="tbToast"></div>

<script>
// ====== 导航 ======
function tbShowHome(){document.getElementById('tbHomeView').style.display='';['tbEncodeArea','tbConvertArea','tbGenerateArea','tbTextArea','tbCalcArea'].forEach(function(id){document.getElementById(id).style.display='none';});window.scrollTo({top:0,behavior:'smooth'});}
function tbShowTool(cat){document.getElementById('tbHomeView').style.display='none';
var map={encode:'tbEncodeArea',convert:'tbConvertArea',generate:'tbGenerateArea',text:'tbTextArea',calculate:'tbCalcArea'};
if(map[cat])document.getElementById(map[cat]).style.display='block';window.scrollTo({top:0,behavior:'smooth'});}

// Tab 切换
document.addEventListener('DOMContentLoaded',function(){
// ====== 示例数据初始化 ======
document.getElementById('tbJsonIn').value='{\n  "name": "开发者工具箱",\n  "version": "1.0.0",\n  "features": ["JSON", "URL", "Base64", "MD5"],\n  "author": "xuan",\n  "isOpenSource": true,\n  "stats": { "users": 12800, "rating": 4.9 }\n}';
document.getElementById('tbUrlIn').value='https://example.com/search?q=Hexo教程&category=博客&page=1';
document.getElementById('tbB64In').value='Hello 世界！Welcome to DevToolbox 🚀';
document.getElementById('tbMd5In').value='Hello World';
document.getElementById('tbTsIn').value=Math.floor(Date.now()/1000);
document.getElementById('tbDateIn').value=new Date().toISOString().slice(0,19).replace('T',' ');
document.getElementById('tbBaseIn').value='255';
document.getElementById('tbRegexPat').value='\\d+';
document.getElementById('tbRegexTxt').value='联系邮箱: support@example.com，电话: 400-888-8888，订单号: 20240611001';
document.getElementById('tbDiffA').value='function hello() {\n  console.log("Hello");\n  return 42;\n}';
document.getElementById('tbDiffB').value='function hello() {\n  console.log("Hello World");\n  return 43;\n}';
document.getElementById('tbChmodIn').value='755';
// ====== 自动触发各工具计算 ======
tbJsonFmt();
tbUrlEnc();
tbB64Enc();
tbMd5Calc();
tbTsToDate();
tbDateToTs();
tbBaseConv();
tbRegexTest();
tbTextDiff();
tbChmodCalc();
document.querySelectorAll('.tb-tab').forEach(function(el){el.addEventListener('click',function(){
var parent=this.closest('.tb-tool-area');if(!parent)return;
parent.querySelectorAll('.tb-tab').forEach(function(t){t.classList.remove('active');});
parent.querySelectorAll('.tb-panel').forEach(function(p){p.classList.remove('active');});
this.classList.add('active');
var panel=document.getElementById(this.dataset.panel);if(panel)panel.classList.add('active');
});});});

// Toast
function tbToast(msg){
  var el=document.getElementById('tbToast');
  el.textContent=msg;el.classList.add('show');
  setTimeout(function(){el.classList.remove('show');},1500);
}
function tbCopy(id,btn){
  var el=document.getElementById(id);
  if(!el||!el.textContent||el.textContent.includes('等待')||el.textContent.includes('点击'))return;
  navigator.clipboard.writeText(el.textContent).then(function(){
    tbToast('✅ 已复制到剪贴板');
    if(btn){var orig=btn.textContent;btn.textContent='已复制 ✓';btn.style.background='#059669';btn.style.color='#fff';btn.style.borderColor='#059669';
      setTimeout(function(){btn.textContent=orig;btn.style.background='';btn.style.color='';btn.style.borderColor='';},1500);}
  });
}
function tbSetOut(id,text){var el=document.getElementById(id);if(!el)return;el.textContent=text;el.classList.add('has-content');}

// ====== JSON ======
var tbJsonLastObj = null;
function tbJsonFmt(){try{var o=JSON.parse(document.getElementById('tbJsonIn').value);tbJsonLastObj=o;tbSetOut('tbJsonOut',JSON.stringify(o,null,2));}catch(e){tbJsonLastObj=null;tbSetOut('tbJsonOut','JSON 格式错误:\n'+e.message);}}
function tbJsonMin(){try{var o=JSON.parse(document.getElementById('tbJsonIn').value);tbJsonLastObj=o;tbSetOut('tbJsonOut',JSON.stringify(o));}catch(e){tbJsonLastObj=null;tbSetOut('tbJsonOut','JSON 格式错误:\n'+e.message);}}
function tbJsonVal(){try{var o=JSON.parse(document.getElementById('tbJsonIn').value);tbJsonLastObj=o;tbSetOut('tbJsonOut','JSON 格式正确！');}catch(e){tbJsonLastObj=null;tbSetOut('tbJsonOut','校验失败:\n'+e.message);}}
function tbJsonView(mode){
  var textTab=document.getElementById('tbJsonTabText');var treeTab=document.getElementById('tbJsonTabTree');
  var textOut=document.getElementById('tbJsonOut');var treeOut=document.getElementById('tbJsonTree');
  if(mode==='text'){textTab.classList.add('active');treeTab.classList.remove('active');textOut.style.display='';treeOut.style.display='none';}
  else{treeTab.classList.add('active');textTab.classList.remove('active');textOut.style.display='none';treeOut.style.display='';tbJsonRenderTree();}
}
function tbJsonTryParse(){
  try{var o=JSON.parse(document.getElementById('tbJsonIn').value);tbJsonLastObj=o;return true;}catch(e){return false;}
}
function tbJsonRenderTree(){
  var el=document.getElementById('tbJsonTree');
  if(!tbJsonLastObj){
    var raw=document.getElementById('tbJsonIn').value;
    try{tbJsonLastObj=JSON.parse(raw);}catch(e){}
  }
  if(!tbJsonLastObj){
    el.innerHTML='<div style="color:#6b7280;padding:20px;text-align:center;">请先输入有效的 JSON</div>';
    return;
  }
  var isArr=Array.isArray(tbJsonLastObj);
  var id='jt_'+Math.random().toString(36).slice(2,10);
  var count=isArr?tbJsonLastObj.length:Object.keys(tbJsonLastObj).length;
  var typeStr=isArr?' ['+count+' 项]':' ['+count+' 个属性]';
  var openBr=isArr?'[':'{';
  var closeBr=isArr?']':'}';
  var html='<div class="jt-root"><div class="jt-item"><span class="jt-toggle jt-expanded" onclick="tbJsonToggle(this)" data-target="'+id+'"></span><span class="jt-bracket">'+openBr+'</span><span class="jt-count">'+typeStr+'</span></div><div class="jt-children" id="'+id+'">';
  if(isArr){tbJsonLastObj.forEach(function(v,i){html+=tbJsonBuildTree(v,i,closeBr);});}
  else{Object.keys(tbJsonLastObj).forEach(function(k){html+=tbJsonBuildTree(tbJsonLastObj[k],k,closeBr);});}
  html+='<div class="jt-item"><span class="jt-toggle jt-leaf"></span><span class="jt-bracket">'+closeBr+'</span></div></div></div>';
  el.innerHTML='<div class="tb-json-tree">'+html+'</div>';
}
function tbJsonBuildTree(obj,key,closeBr){
  var type=typeof obj;var isArr=Array.isArray(obj);
  var openBr=isArr?'[':'{';
  var closeBracket=closeBr||'';
  if(obj===null){return'<div class="jt-item"><span class="jt-toggle jt-leaf"></span><span class="jt-key">'+tbJsonEsc(key)+'</span><span class="jt-colon">:</span><span class="jt-null">null</span>'+(closeBracket?'<span class="jt-bracket">'+closeBracket+'</span>':'')+'</div>';}
  if(type==='string'){return'<div class="jt-item"><span class="jt-toggle jt-leaf"></span><span class="jt-key">'+tbJsonEsc(key)+'</span><span class="jt-colon">:</span><span class="jt-string">"'+tbJsonEsc(obj)+'"</span>'+(closeBracket?'<span class="jt-bracket">'+closeBracket+'</span>':'')+'</div>';}
  if(type==='number'){return'<div class="jt-item"><span class="jt-toggle jt-leaf"></span><span class="jt-key">'+tbJsonEsc(key)+'</span><span class="jt-colon">:</span><span class="jt-number">'+obj+'</span>'+(closeBracket?'<span class="jt-bracket">'+closeBracket+'</span>':'')+'</div>';}
  if(type==='boolean'){return'<div class="jt-item"><span class="jt-toggle jt-leaf"></span><span class="jt-key">'+tbJsonEsc(key)+'</span><span class="jt-colon">:</span><span class="jt-boolean">'+obj+'</span>'+(closeBracket?'<span class="jt-bracket">'+closeBracket+'</span>':'')+'</div>';}
  if(type==='object'){
    var keys=Object.keys(obj);var len=keys.length;
    if(len===0){return'<div class="jt-item"><span class="jt-toggle jt-leaf"></span><span class="jt-key">'+tbJsonEsc(key)+'</span><span class="jt-colon">:</span><span class="jt-bracket">'+openBr+closeBracket+' '+closeBracket+'</span></div>';}
    var id='jt_'+Math.random().toString(36).slice(2,10);
    var countStr=isArr?' ['+len+' 项]':' ['+len+' 个属性]';
    var html='<div class="jt-item"><span class="jt-toggle jt-expanded" onclick="tbJsonToggle(this)" data-target="'+id+'"></span><span class="jt-key">'+tbJsonEsc(key)+'</span><span class="jt-colon">:</span><span class="jt-bracket">'+openBr+'</span><span class="jt-count">'+countStr+'</span></div>';
    html+='<div class="jt-children" id="'+id+'">';
    keys.forEach(function(k){html+=tbJsonBuildTree(obj[k],k,isArr?']':'}',false);});
    html+='<div class="jt-item"><span class="jt-toggle jt-leaf"></span><span class="jt-bracket">'+(isArr?']':'}')+'</span></div></div>';
    return html;
  }
  return '';
}
function tbJsonEsc(s){return String(s).replace(/&/g,'&amp;').replace(/</g,'&lt;').replace(/>/g,'&gt;').replace(/"/g,'&quot;');}
function tbJsonToggle(el){var target=document.getElementById(el.dataset.target);if(!target)return;
  if(el.classList.contains('jt-expanded')){el.classList.remove('jt-expanded');el.classList.add('jt-collapsed');target.style.display='none';}
  else{el.classList.remove('jt-collapsed');el.classList.add('jt-expanded');target.style.display='';}
}

// ====== URL ======
function tbUrlEnc(){tbSetOut('tbUrlOut',encodeURIComponent(document.getElementById('tbUrlIn').value));}
function tbUrlDec(){try{tbSetOut('tbUrlOut',decodeURIComponent(document.getElementById('tbUrlIn').value));}catch(e){tbSetOut('tbUrlOut','解码失败');}}

// ====== Base64 ======
function tbB64Enc(){try{tbSetOut('tbB64Out',btoa(unescape(encodeURIComponent(document.getElementById('tbB64In').value))));}catch(e){tbSetOut('tbB64Out','编码失败');}}
function tbB64Dec(){try{tbSetOut('tbB64Out',decodeURIComponent(escape(atob(document.getElementById('tbB64In').value))));}catch(e){tbSetOut('tbB64Out','解码失败，请检查输入');}}

// ====== MD5 (简化实现) ======
function tbSimpleMD5(s){
function cmn(q,a,b,x,s,t){a=tbAdd32(tbAdd32(a,q),tbAdd32(x,t));return tbAdd32((a<<s)|(a>>>(32-s)),b);}
function ff(a,b,c,d,x,s,t){return cmn((b&c)|((~b)&d),a,b,x,s,t);}
function gg(a,b,c,d,x,s,t){return cmn((b&d)|(c&(~d)),a,b,x,s,t);}
function hh(a,b,c,d,x,s,t){return cmn(b^c^d,a,b,x,s,t);}
function ii(a,b,c,d,x,s,t){return cmn(c^(b|(~d)),a,b,x,s,t);}
function md5cycle(x,k){var a=x[0],b=x[1],c=x[2],d=x[3];
a=ff(a,b,c,d,k[0],7,-680876936);d=ff(d,a,b,c,k[1],12,-389564586);c=ff(c,d,a,b,k[2],17,606105819);b=ff(b,c,d,a,k[3],22,-1044525330);
a=ff(a,b,c,d,k[4],7,-176418897);d=ff(d,a,b,c,k[5],12,1200080426);c=ff(c,d,a,b,k[6],17,-1473231341);b=ff(b,c,d,a,k[7],22,-45705983);
a=ff(a,b,c,d,k[8],7,1770035416);d=ff(d,a,b,c,k[9],12,-1958414417);c=ff(c,d,a,b,k[10],17,-42063);b=ff(b,c,d,a,k[11],22,-1990404162);
a=ff(a,b,c,d,k[12],7,1804603682);d=ff(d,a,b,c,k[13],12,-40341101);c=ff(c,d,a,b,k[14],17,-1502002290);b=ff(b,c,d,a,k[15],22,1236535329);
a=gg(a,b,c,d,k[1],5,-165796510);d=gg(d,a,b,c,k[6],9,-1069501632);c=gg(c,d,a,b,k[11],14,643717713);b=gg(b,c,d,a,k[0],20,-373897302);
a=gg(a,b,c,d,k[5],5,-701558691);d=gg(d,a,b,c,k[10],9,38016083);c=gg(c,d,a,b,k[15],14,-660478335);b=gg(b,c,d,a,k[4],20,-405537848);
a=gg(a,b,c,d,k[9],5,568446438);d=gg(d,a,b,c,k[14],9,-1019803690);c=gg(c,d,a,b,k[3],14,-187363961);b=gg(b,c,d,a,k[8],20,1163531501);
a=gg(a,b,c,d,k[13],5,-1444681467);d=gg(d,a,b,c,k[2],9,-51403784);c=gg(c,d,a,b,k[7],14,1735328473);b=gg(b,c,d,a,k[12],20,-1926607734);
a=hh(a,b,c,d,k[5],4,-378558);d=hh(d,a,b,c,k[8],11,-2022574463);c=hh(c,d,a,b,k[11],16,1839030562);b=hh(b,c,d,a,k[14],23,-35309556);
a=hh(a,b,c,d,k[1],4,-1530992060);d=hh(d,a,b,c,k[4],11,1272893353);c=hh(c,d,a,b,k[7],16,-155497632);b=hh(b,c,d,a,k[10],23,-1094730640);
a=hh(a,b,c,d,k[13],4,681279174);d=hh(d,a,b,c,k[0],11,-358537222);c=hh(c,d,a,b,k[3],16,-722521979);b=hh(b,c,d,a,k[6],23,76029189);
a=hh(a,b,c,d,k[9],4,-640364487);d=hh(d,a,b,c,k[12],11,-421815835);c=hh(c,d,a,b,k[15],16,530742520);b=hh(b,c,d,a,k[2],23,-995338651);
a=ii(a,b,c,d,k[0],6,-198630844);d=ii(d,a,b,c,k[7],10,1126891415);c=ii(c,d,a,b,k[14],15,-1416354905);b=ii(b,c,d,a,k[5],21,-57434055);
a=ii(a,b,c,d,k[12],6,1700485571);d=ii(d,a,b,c,k[3],10,-1894986606);c=ii(c,d,a,b,k[10],15,-1051523);b=ii(b,c,d,a,k[1],21,-2054922799);
a=ii(a,b,c,d,k[8],6,1873313359);d=ii(d,a,b,c,k[15],10,-30611744);c=ii(c,d,a,b,k[6],15,-1560198380);b=ii(b,c,d,a,k[13],21,1309151649);
a=ii(a,b,c,d,k[4],6,-145523070);d=ii(d,a,b,c,k[11],10,-1120210379);c=ii(c,d,a,b,k[2],15,718787259);b=ii(b,c,d,a,k[9],21,-343485551);
x[0]=tbAdd32(a,x[0]);x[1]=tbAdd32(b,x[1]);x[2]=tbAdd32(c,x[2]);x[3]=tbAdd32(d,x[3]);}
function md5blk(s){var a=[],i;for(i=0;i<64;i+=4)a[i>>2]=s.charCodeAt(i)+(s.charCodeAt(i+1)<<8)+(s.charCodeAt(i+2)<<16)+(s.charCodeAt(i+3)<<24);return a;}
function tbAdd32(a,b){return(a+b)&0xFFFFFFFF;}
function rhex(n){var s='',j;for(j=0;j<4;j++)s+=((n>>(j*8))&0xFF).toString(16).padStart(2,'0');return s;}
function hex(x){var i;for(i=0;i<x.length;i++)x[i]=rhex(x[i]);return x.join('');}
function md5_raw(s){var n=s.length,st=[1732584193,-271733879,-1732584194,271733878],i;for(i=64;i<=n;i+=64)md5cycle(st,md5blk(s.substring(i-64,i)));s=s.substring(i-64);var tail=[0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0];for(i=0;i<s.length;i++)tail[i>>2]|=s.charCodeAt(i)<<((i%4)<<3);tail[i>>2]|=0x80<<((i%4)<<3);if(i>55){md5cycle(st,tail);tail=[0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0];}tail[14]=n*8;md5cycle(st,tail);return st;}
var utf8=unescape(encodeURIComponent(s));return hex(md5_raw(utf8));
}
function tbMd5Calc(){var t=document.getElementById('tbMd5In').value;if(!t){tbSetOut('tbMd5Out','请输入文本');return;}var h=tbSimpleMD5(t);if(document.getElementById('tbMd5Up').checked)h=h.toUpperCase();tbSetOut('tbMd5Out',h);}

// ====== 时间戳 ======
function tbTsToDate(){var v=document.getElementById('tbTsIn').value.trim();if(!v)return;var d=new Date(parseInt(v)*1000);if(isNaN(d)){tbRenderTs('无效的时间戳');return;}tbRenderTs('日期时间: '+d.toLocaleString('zh-CN')+'\nISO 格式: '+d.toISOString()+'\nUTC 时间: '+d.toUTCString());}
function tbDateToTs(){var v=document.getElementById('tbDateIn').value.trim();if(!v)return;var d=new Date(v);if(isNaN(d)){tbRenderTs('无效的日期格式');return;}tbRenderTs('时间戳(秒): '+Math.floor(d.getTime()/1000)+'\n时间戳(毫秒): '+d.getTime());}
function tbTsNow(){document.getElementById('tbTsIn').value=Math.floor(Date.now()/1000);tbTsToDate();}
function tbDateNow(){document.getElementById('tbDateIn').value=new Date().toISOString().slice(0,19).replace('T',' ');tbDateToTs();}
function tbRenderTs(text){var el=document.getElementById('tbTsOut');el.innerHTML=text.split('\n').map(function(l){if(l.includes(': ')){var p=l.split(': ');return'<div class="tb-ts-item"><span class="tb-ts-lbl">'+p[0]+'</span><span class="tb-ts-val">'+(p[1]||'')+'</span></div>';}return'<div style="color:#374151;padding:4px 0;">'+l+'</div>';}).join('');}

// ====== 进制 ======
function tbBaseConv(){var v=document.getElementById('tbBaseIn').value.trim();var f=parseInt(document.getElementById('tbBaseFrom').value);if(!v)return;try{var num=parseInt(v,f);if(isNaN(num))throw new Error();document.getElementById('tbBinVal').textContent=num.toString(2);document.getElementById('tbOctVal').textContent=num.toString(8);document.getElementById('tbDecVal').textContent=num.toString(10);document.getElementById('tbHexVal').textContent=num.toString(16);}catch(e){['tbBinVal','tbOctVal','tbDecVal','tbHexVal'].forEach(function(id){document.getElementById(id).textContent='错误';});}}

// ====== 密码 ======
function tbGenPwd(){var len=parseInt(document.getElementById('tbPwdLen').value)||16;var ch='';
if(document.getElementById('tbPwdUp').checked)ch+='ABCDEFGHIJKLMNOPQRSTUVWXYZ';
if(document.getElementById('tbPwdLo').checked)ch+='abcdefghijklmnopqrstuvwxyz';
if(document.getElementById('tbPwdNu').checked)ch+='0123456789';
if(document.getElementById('tbPwdSy').checked)ch+='!@#$%^&*()_+-=[]{}|;:,.<>?';
if(!ch){tbSetOut('tbPwdOut','请至少选择一种字符类型');return;}
var pwd='';for(var i=0;i<len;i++)pwd+=ch[Math.floor(Math.random()*ch.length)];
tbSetOut('tbPwdOut',pwd);
var bars=document.querySelectorAll('#tbPwdBars .tb-pwd-bar');var sc=0;if(pwd.length>=8)sc++;if(pwd.length>=12)sc++;if(/[A-Z]/.test(pwd)&&/[a-z]/.test(pwd))sc++;if(/[0-9]/.test(pwd))sc++;if(/[^A-Za-z0-9]/.test(pwd))sc++;
bars.forEach(function(b,i){b.className='tb-pwd-bar';if(i<sc)b.classList.add(sc<=2?'weak':sc<=3?'fair':'strong');});}

// ====== UUID ======
function tbGenUuid(){var cnt=parseInt(document.getElementById('tbUuidCnt').value)||5;var up=document.getElementById('tbUuidUp').checked;var nd=document.getElementById('tbUuidNoDash').checked;var r='';for(var i=0;i<cnt;i++){var u='xxxxxxxx-xxxx-4xxx-yxxx-xxxxxxxxxxxx'.replace(/[xy]/g,function(c){var r=Math.random()*16|0;return(c==='x'?r:(r&0x3|0x8)).toString(16);});if(nd)u=u.replace(/-/g,'');if(up)u=u.toUpperCase();r+=u+'\n';}tbSetOut('tbUuidOut',r.trim());}

// ====== 正则 ======
function tbRegexTest(){var pat=document.getElementById('tbRegexPat').value;var txt=document.getElementById('tbRegexTxt').value;if(!pat||!txt){tbSetOut('tbRegexOut','请输入正则表达式和测试文本');return;}try{var fl=(document.getElementById('tbFlgG').checked?'g':'')+(document.getElementById('tbFlgI').checked?'i':'')+(document.getElementById('tbFlgM').checked?'m':'');var re=new RegExp(pat,fl);var m=txt.match(re);if(!m){tbSetOut('tbRegexOut','没有找到匹配');return;}tbSetOut('tbRegexOut','找到 '+m.length+' 个匹配:\n\n'+m.slice(0,20).join('\n')+(m.length>20?'\n... (共 '+m.length+' 个)':''));}catch(e){tbSetOut('tbRegexOut','正则表达式错误:\n'+e.message);}}

// ====== Diff ======
function tbTextDiff(){var a=document.getElementById('tbDiffA').value;var b=document.getElementById('tbDiffB').value;if(!a&&!b){tbSetOut('tbDiffOut','请输入文本 A 和 B');return;}var la=a.split('\n'),lb=b.split('\n');var ml=Math.max(la.length,lb.length);var r='';for(var i=0;i<ml;i++){var lai=la[i]||'',lbi=lb[i]||'';if(lai===lbi)r+='  '+lai+'\n';else{if(lai)r+='− '+lai+'\n';if(lbi)r+='+ '+lbi+'\n';}}tbSetOut('tbDiffOut',r);}

// ====== 统计 ======
function tbUpdateCount(){var t=document.getElementById('tbCntInput').value;document.getElementById('tbCntChars').textContent=t.length;document.getElementById('tbCntNoSp').textContent=t.replace(/\s/g,'').length;document.getElementById('tbCntWords').textContent=t.trim()?t.trim().split(/\s+/).length:0;document.getElementById('tbCntLines').textContent=t?t.split('\n').length:0;document.getElementById('tbCntZh').textContent=(t.match(/[\u4e00-\u9fff]/g)||[]).length;}

// ====== 单位换算 ======
var tbUnitData={length:{units:['米','千米','厘米','毫米','英尺','英寸','英里'],rates:[1,1000,0.01,0.001,0.3048,0.0254,1609.34]},weight:{units:['克','千克','磅','盎司'],rates:[1,1000,453.592,28.3495]},temp:{units:['摄氏度','华氏度','开尔文']}};
function tbPopUnits(){var tp=document.getElementById('tbUnitType').value;var fr=document.getElementById('tbUnitFrom');var to=document.getElementById('tbUnitTo');fr.innerHTML='';to.innerHTML='';tbUnitData[tp].units.forEach(function(u,i){fr.add(new Option(u,i));to.add(new Option(u,i));});to.selectedIndex=1;tbUnitConv();}
function tbUnitConv(){var tp=document.getElementById('tbUnitType').value;var val=parseFloat(document.getElementById('tbUnitVal').value);if(isNaN(val)){document.getElementById('tbUnitOut').textContent='请输入有效数值';document.getElementById('tbUnitOut').style.color='#ef4444';document.getElementById('tbUnitOut').style.background='#fef2f2';return;}
var fi=parseInt(document.getElementById('tbUnitFrom').value);var ti=parseInt(document.getElementById('tbUnitTo').value);var res;if(tp==='temp'){var k;if(fi===0)k=val+273.15;else if(fi===1)k=(val-32)*5/9+273.15;else k=val;if(ti===0)res=k-273.15;else if(ti===1)res=(k-273.15)*9/5+32;else res=k;}else{var data=tbUnitData[tp];res=(val*data.rates[fi])/data.rates[ti];}
document.getElementById('tbUnitOut').textContent=val+' '+tbUnitData[tp].units[fi]+' = '+res.toFixed(6)+' '+tbUnitData[tp].units[ti];
document.getElementById('tbUnitOut').style.color='#2563eb';document.getElementById('tbUnitOut').style.background='#eff6ff';}

// ====== Unix 权限 ======
function tbToSym(d){return((d&4)?'r':'-')+((d&2)?'w':'-')+((d&1)?'x':'-');}
function tbChmodCalc(){var v=document.getElementById('tbChmodIn').value.trim();if(!/^[0-7]{1,3}$/.test(v)){['tbChmodNum','tbChmodSym','tbChmodCmd'].forEach(function(id){document.getElementById(id).textContent='错误';});return;}
var p=v.padStart(3,'0');var sym=tbToSym(p[0])+tbToSym(p[1])+tbToSym(p[2]);
document.getElementById('tbChmodNum').textContent=p;
document.getElementById('tbChmodSym').textContent=sym;
document.getElementById('tbChmodCmd').textContent='chmod '+p+' file.txt';
}
function tbChmodFromCb(){
var o=(document.getElementById('tbCoR').checked?4:0)+(document.getElementById('tbCoW').checked?2:0)+(document.getElementById('tbCoX').checked?1:0);
var g=(document.getElementById('tbCgR').checked?4:0)+(document.getElementById('tbCgW').checked?2:0)+(document.getElementById('tbCgX').checked?1:0);
var a=(document.getElementById('tbCaR').checked?4:0)+(document.getElementById('tbCaW').checked?2:0)+(document.getElementById('tbCaX').checked?1:0);
document.getElementById('tbChmodIn').value=''+o+g+a;tbChmodCalc();
}

// 初始化
(function(){tbPopUnits();})();
</script>
{% endraw %}