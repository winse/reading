---
name: reading-notes
description: 将微信读书划线整理成结构化读书笔记网页
metadata:
  type: skill
  version: 1.0.0
---

# Reading Notes — 微信读书划线整理技能

将微信读书的划线笔记整理成结构化的 HTML 读书笔记。

## 结构规范

```
我的心得（独立于书籍的实战经验）

书中摘录（按原书章节组织）
  ├── 摘录 1 · 章节标题
  ├── 摘录 2 · 章节标题
  └── ...

实用模板（命令模板等可复用内容）
```

**原则：心得和摘录分开，结构清晰不纠缠。**

## 文件

| 文件 | 说明 |
|------|------|
| `{book-slug}-notes.html` | 单本书的读书笔记 |
| `index.html` | 读书笔记目录首页 |
| `notes.css` | 通用样式文件（所有笔记共用） |

## HTML 模板

```html
<h1>《书名》读书笔记</h1>
<a class="book-link" href="weread://reading?bId={bookId}">打开书籍</a>
<a class="book-link" href="index.html" style="background:#666">返回目录</a>

<!-- 我的心得 -->
<div class="intro-section">
  <h2>写在前面：我的 XXX 使用心得</h2>
  <ol>
    <li><strong>心得标题</strong><br>心得内容...</li>
  </ol>
</div>

<!-- 书中摘录 -->
<div class="section">
  <h2 id="1">摘录 1 · 章节标题</h2>
  <blockquote class="quote">原文引用</blockquote>
  <p>简短解读</p>
</div>

<!-- 实用模板 -->
<div class="section">
  <h2>实用模板</h2>
  <table>
    <tr><th>场景</th><th>内容</th></tr>
  </table>
</div>

<p class="footer">
  读书笔记 &middot; 微信读书划线整理 &middot; <a href="weread://reading?bId={bookId}">打开原书</a>
</p>
```

## 样式

所有笔记引用 `notes.css`，只需添加 `<link rel="stylesheet" href="notes.css">`。

## 封面图片

每本书的封面图存储在 `images/{bookId}-cover.jpg`。

**下载封面步骤：**

1. 调 `/book/info` 获取 `cover` 字段（公网可访问的 CDN 地址）
2. 下载封面：
   ```bash
   curl -o images/{bookId}-cover.jpg "https://cdn.weread.qq.com/weread/cover/..."
   ```
3. HTML 中引用：`images/{bookId}-cover.jpg`

**微信读书私有 CDN 问题：**

`weread-1258476243.file.myqcloud.com` 链接需要认证，直接 `<img>` 嵌入无法显示。必须通过 `/book/info` 获取公开 CDN 地址后下载。

## 深度链接

| 类型 | URL |
|------|-----|
| 打开书籍 | `weread://reading?bId={bookId}` |