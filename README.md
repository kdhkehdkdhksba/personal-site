# 鲁志鹏的个人网站

一个纯静态的求职名片站。没有框架、没有构建步骤，双击 `index.html` 或起个本地服务就能看。

## 目录结构

```
personal-site/
├── index.html        首页：我是谁、现在在做什么、学习记录、技能、联系
├── log/index.html    学习记录页
├── log/files/        记录里附带的原始文件（docx / xlsx / pdf 都放这里）
├── site.css          全站样式（配色、字体、间距都在顶部 :root 里）
├── nav.js            顶部导航（名字、链接、深色模式）
├── og.png            发链接时的预览图（1200×630）
└── README.md         这份说明
```

所有路径都是相对路径（`site.css`、`nav.js`、`log/`），所以整站放在域名根目录或 `/仓库名/` 子目录下都能正常打开。

## 日常更新：改文字

直接打开 `index.html`，找到对应段落改字即可。文件里已经用中文注释分好了区：

- 首屏（`id="hero"`）—— 名字、专业、目标、自我介绍
- 现在在做什么（`id="now"`）—— 每个学期换一次
- 学习记录（`id="log"`）—— 首页只放最新两条
- 技能与证书（`id="skills"`）
- 联系（`id="contact"`）

## 加一条学习记录

1. 打开 `log/index.html`；
2. 复制一个 `.reflect-item` 整块，粘在最上面（时间倒序）；
3. 改日期、标题、描述；
4. 回到 `index.html`，把首页那两条换成新的。

## 给某条记录加附件

1. 把文件放进 `log/files/`，文件名用英文（比如 `word-layout.docx`），避免网址里出现中文；
2. 在 `log/index.html` 对应条目里加一行：

```html
<p class="file"><a href="files/文件名.docx" download>下载原文 · Word 文档（.docx，122 KB）</a></p>
```

3. 大小写顺手写清楚（文件右键属性能看到）。

## 加一个新页面（比如以后的项目详情）

1. 新建文件夹 `projects/项目名/index.html`，照着 `log/index.html` 的结构写；
2. `head` 里的路径按层级改相对路径：子目录页面写 `../../site.css`、`../../nav.js`；
3. `<script src="../../nav.js" data-root="../.." defer>` —— `data-root` 是"走到站根的相对前缀"，首页是 `.`，一层子目录是 `..`，两层是 `../..`；
4. 在 `nav.js` 的 `LINKS` 里加一条，全站导航就都有了。

## 改名字、导航、配色

- 名字和导航：改 `nav.js` 顶部 `SITE_NAME` 和 `LINKS`。
- 配色和宽度：改 `site.css` 里 `:root` 的变量，深色模式改下面的 `:root[data-theme="dark"]`。
- 别动组件部分（`.contact-btn`、`.rowitem` 这些），只改变量就够。

## 部署

纯静态，三条路任选：

- **GitHub Pages**：仓库 Settings → Pages → 选分支根目录。注意仓库名会成为网址里的子路径（`用户名.github.io/仓库名/`），本站的相对路径已经能适配。
- **Cloudflare Pages / Vercel**：构建命令留空，输出目录填 `personal-site`（或仓库根目录）。
- 本地先看效果：`python -m http.server 8000`，浏览器打开 `http://localhost:8000`。直接双击 `index.html` 也能看，只是 `log/` 这类目录跳转在 `file://` 下偶尔不灵，用本地服务最稳。

部署后建议把 `index.html` 里的 `og:image` 改成完整网址（如 `https://你的域名/og.png`），这样在微信、QQ 里转发才会有预览图。

## 四年里该往里加什么

- 大一：Office、工程制图、高数这些课的成绩和产出，竞赛入门
- 大二：三维建模、机械设计课程设计、第一次竞赛作品
- 大三：专业核心课、项目作品、寒暑假实习
- 大四：毕业设计、求职材料、实习成果

每加一样，就在学习记录里写一条「做了什么 + 结果」。别写空话，写能验证的事。
