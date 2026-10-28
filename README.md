# Shiquan Song: Academic Website

基于 [Academic Pages](https://github.com/academicpages/academicpages.github.io)（Jekyll，Minimal Mistakes 主题的分支）构建的个人学术网站。
定位：**AI Data Engineering × Optimization Research**。

- 需要你补充或确认的事实见 [`TODO.md`](TODO.md)。
- 当前进度和交接说明见 [`HANDOVER.md`](HANDOVER.md)。
- `README.md`、`TODO.md`、`HANDOVER.md` 都不会发布到网站上（已在 `_config.yml` 的 `exclude` 中）。

---

## 1. 目录结构

| 路径 | 作用 |
|---|---|
| `_config.yml` | 站点配置：名称、URL、侧边栏个人信息、集合、插件 |
| `_data/navigation.yml` | 顶部导航 |
| `_pages/home.md` | 首页（`/`） |
| `_pages/about.md` | About（`/about/`） |
| `_pages/research.md` | Research（`/research/`） |
| `_pages/publications.html` | 论文列表（`/publications/`），自动读取 `_publications/` |
| `_pages/portfolio.html` | 项目列表（`/projects/`），自动读取 `_portfolio/` |
| `_pages/experience.md` | 经历、教育和技能（`/experience/`） |
| `_pages/cv.md` | CV 页（`/cv/`） |
| `_pages/contact.md` | 联系方式（`/contact/`），从 `_config.yml` 读取 |
| `_publications/` | 每篇论文一个 Markdown 文件 |
| `_portfolio/` | 每个项目一个 Markdown 文件（网址前缀为 `/projects/`） |
| `_includes/cv-download.html` | CV 下载按钮：`files/cv.pdf` 存在时显示下载链接，否则显示 "available on request" |
| `files/` | PDF、BibTeX 等静态文件，网址为 `/files/<文件名>` |
| `images/` | 图片 |
| `.github/workflows/jekyll.yml` | GitHub Actions：构建并部署到 GitHub Pages |

与官方模板相比的主要改动：

- 删除了示例内容（示例论文、talks、teaching、博客、示例 PDF、talkmap 相关脚本和工作流），以及只适用于模板仓库本身的工作流（`bad-pr.yml`、`scrape_talks.yml`）。
- `_includes/author-profile.html`：`author.avatar` 为空时不显示头像（原模板始终显示）。
- `_config.yml`：`portfolio` 集合的网址前缀改为 `/projects/`；`exclude` 中加入文档和开发目录。
- `.github/workflows/jekyll.yml`：同时在 `main` 和 `master` 分支触发；给 `configure-pages` 步骤加了 `id: pages`。原模板缺少这个 id，导致 `--baseurl` 永远是空字符串，部署为项目站点时资源路径会出错。
- `Gemfile`：加入仅在 Windows 下生效的 `tzinfo-data`。

---

## 2. 本地运行

### 2.1 Windows

1. 安装 Ruby 3.1 到 3.3 中的任意版本，选择 **with Devkit** 的版本：<https://rubyinstaller.org/downloads/>。
   （安装 Ruby 3.4 也可以，但如果遇到 `csv`、`base64`、`bigdecimal` 之类的缺失报错，就退回到 3.3。）
2. 在本目录执行：

```powershell
gem install bundler
bundle config set --local path vendor/bundle
# 如果访问 rubygems.org 很慢，可以只在本机使用镜像（写入 .bundle/config，不会提交）：
# bundle config set --local mirror.https://rubygems.org https://mirrors.tuna.tsinghua.edu.cn/rubygems/
bundle install
bundle exec jekyll serve -l -H localhost
```

3. 打开 <http://localhost:4000>。

`assets/js/main.min.js`（导航折叠、深色模式等功能需要它）在 `.gitignore` 中，线上由 GitHub Actions 生成。本地预览前需要先生成一次（需要 Node.js）：

```powershell
npx --yes uglify-js@3 assets/js/plugins/jquery.greedy-navigation.js assets/js/_main.js assets/js/theme.js -c -m -o assets/js/main.min.js
# 访问 npm 慢时加上 --registry=https://registry.npmmirror.com
```

### 2.2 macOS / Linux

```bash
bundle config set --local path vendor/bundle
bundle install
bundle exec jekyll serve -l -H localhost
```

### 2.3 Docker（不想在本机安装 Ruby 时使用）

```bash
docker compose up
```

使用模板自带的 `Dockerfile`、`docker-compose.yaml` 和 `_config_docker.yml`。

### 2.4 只构建、不启动服务

```bash
bundle exec jekyll build        # 输出到 _site/
JEKYLL_ENV=production bundle exec jekyll build
```

> 修改 `_config.yml` 后需要重启 `jekyll serve` 才能生效。

---

## 3. 修改个人资料

全部在 `_config.yml` 中修改：

```yaml
title: "Shiquan Song"
url: "https://pluto201.github.io"   # 已填好
author:
  avatar: "profile.png"     # 可选：把图片放到 images/profile.png；留空则不显示头像
  bio: "AI Data Engineering × Optimization Research"
  location: "Beijing, China"
  email: "you@example.com"  # 留空则 Contact 页显示 "to be added"，侧边栏不显示
  github: "your-username"   # 只填用户名
  linkedin: "your-handle"   # 只填 linkedin.com/in/ 后面的部分
  googlescholar: "https://scholar.google.com/citations?user=..."
  orcid: "https://orcid.org/0000-..."
```

字段为空时，侧边栏不会显示对应的图标或链接，所以不会出现无效链接。

页面正文直接编辑 `_pages/*.md`。内部链接请写成 `{{ '/research/' | relative_url }}` 的形式，这样在设置了 `baseurl` 时链接仍然正确。

---

## 4. 添加论文

在 `_publications/` 下新建 `YYYY-MM-DD-short-name.md`：

```markdown
---
title: "Paper title"
collection: publications
category: manuscripts          # manuscripts = Journal Articles；conferences = Conference Papers
permalink: /publication/YYYY-short-name/
excerpt: 'One-sentence summary shown in the list.'
date: YYYY-MM-DD
venue: 'Journal or conference name'
paperurl: 'https://doi.org/...'
citation: 'Authors, "Title," <i>Venue</i>, vol. X, YYYY.'
---

Longer description, your contribution, links to code and BibTeX.
```

- 分类标题在 `_config.yml` 的 `publication_category` 中定义。
- BibTeX 文件放在 `files/`，正文里用 `[BibTeX]({{ '/files/xxx.bib' | relative_url }})` 链接。
- 列表按 `date` 倒序排列。
- 模板的 `markdown_generator/` 目录可以从 CSV 或 BibTeX 批量生成论文文件。

---

## 5. 添加项目

在 `_portfolio/` 下新建 Markdown 文件。文件名决定列表顺序，例如 `3-xxx.md`：

```markdown
---
title: "Project name"
permalink: /projects/project-slug/
excerpt: "One- or two-sentence summary shown on /projects/."
collection: portfolio
toc: true
toc_label: "On this page"
---

## Overview
## Problem and Motivation
## Architecture
## Technical Decisions
## My Contributions
## Engineering Challenges
## Results and Limitations
## Technologies
```

架构图可以直接用 Mermaid 代码块（```` ```mermaid ````），模板会在页面上自动渲染。首页的 "Selected projects" 需要手动在 `_pages/home.md` 中加入链接。

---

## 6. 替换 CV

1. 把英文 PDF 简历命名为 `cv.pdf`，放到 `files/` 目录。
2. 重新构建即可。首页和 `/cv/` 页的按钮会自动变成 "Download CV (PDF)"，不需要改代码。
3. `/cv/` 页的网页版内容在 `_pages/cv.md` 中修改，请和 PDF 保持一致。

---

## 7. 发布到 GitHub Pages

### 7.1 用户站点（推荐）：`https://pluto201.github.io`

1. 在 GitHub 新建一个**公开**仓库，名称必须是 `pluto201.github.io`，不要勾选初始化 README。
2. 修改 `_config.yml`（**本项目已经填好**）：
   ```yaml
   url: "https://pluto201.github.io"
   baseurl: ""
   repository: "pluto201/pluto201.github.io"
   author:
     github: "pluto201"
   ```
3. 推送代码（本项目已完成 `git init` 和首次提交，只需执行后面三行）：
   ```bash
   git add .
   git commit -m "Initial academic website"
   git branch -M main
   git remote add origin https://github.com/pluto201/pluto201.github.io.git
   git push -u origin main
   ```
4. 在仓库的 **Settings → Pages → Build and deployment → Source** 中选择 **GitHub Actions**。
5. 打开 **Actions** 标签页，等待 "Deploy Academic Pages template site to Pages" 运行成功（变成绿色）。如果在第 4 步之前已经触发过一次并失败，点 **Re-run all jobs**。
6. 访问 `https://pluto201.github.io`。

### 7.2 项目站点：`https://<username>.github.io/<repo>`

步骤同上，但仓库名可以任意，且：

```yaml
url: "https://<username>.github.io"
baseurl: "/<repo>"
```

工作流会把 GitHub Pages 提供的 `base_path` 传给 `--baseurl`，两者应保持一致。

### 7.3 上线后的检查

- [ ] 首页能打开，导航中 7 个链接都能打开（About、Research、Publications、Projects、Experience、CV、Contact）。
- [ ] 两个项目页能打开，Mermaid 架构图能渲染。
- [ ] 论文详情页的 DOI 链接能打开，BibTeX 能下载。
- [ ] `https://<你的地址>/sitemap.xml` 和 `/feed.xml` 能打开。
- [ ] 用手机或浏览器开发者工具的移动端模式检查首页。
- [ ] 侧边栏没有指向无效地址的图标。

---

## 8. 自定义域名

1. 在域名服务商处添加 DNS 记录：
   - 顶级域名（`example.com`）：添加 4 条 `A` 记录，分别指向 `185.199.108.153`、`185.199.109.153`、`185.199.110.153`、`185.199.111.153`；也可以添加对应的 `AAAA` 记录。
   - 子域名（`www.example.com`）：添加一条 `CNAME` 记录，指向 `<username>.github.io`。
2. 仓库 **Settings → Pages → Custom domain** 填入域名并保存。等证书签发后勾选 **Enforce HTTPS**。
   使用 GitHub Actions 部署时，以这里的设置为准，不需要在仓库里提交 `CNAME` 文件。
3. 修改 `_config.yml`：`url: "https://example.com"`，`baseurl: ""`。
4. 建议在 GitHub 账号的 **Settings → Pages** 中验证域名，防止被他人占用。

最新说明请以 GitHub 官方文档为准：<https://docs.github.com/en/pages/configuring-a-custom-domain-for-your-github-pages-site>。

---

## 9. 常见构建问题

| 现象 | 原因与处理 |
|---|---|
| `bundle install` 长时间不动 | 访问 rubygems.org 慢。只在本机配置镜像：`bundle config set --local mirror.https://rubygems.org https://mirrors.tuna.tsinghua.edu.cn/rubygems/` |
| Windows 下报 `tzinfo` / `TZInfo::DataSourceNotFound` | 执行 `bundle install`，确认 `Gemfile` 中有 `tzinfo-data` |
| 编译原生扩展失败（`Failed to build gem native extension`） | 没有安装 Devkit。运行 `ridk install`，选择 MSYS2 和 MINGW 开发工具链 |
| 修改 `_config.yml` 后页面没变化 | 重启 `jekyll serve` |
| 页面样式丢失、链接 404（部署后） | `url` / `baseurl` 与实际地址不一致。用户站点 `baseurl` 必须为 `""`；项目站点必须为 `"/<repo>"` |
| Actions 中 "Deploy" 步骤报权限错误 | Settings → Pages 的 Source 没有选择 GitHub Actions |
| Actions 中 `bundle install` 报平台错误 | 不要提交 `Gemfile.lock`（已在 `.gitignore` 中）。在 Windows 下生成的 lock 文件只包含 Windows 平台 |
| 本地页面中的 JS 功能（导航折叠、深色模式）不工作 | 缺少 `assets/js/main.min.js`。按第 2.1 节的 `npx uglify-js` 命令生成；线上由 Actions 自动生成 |
| Liquid 报错 `Liquid syntax error` | Markdown 正文中出现了 `{{` 或 `{%`。用 `{% raw %}...{% endraw %}` 包住 |
| YAML front matter 报错 | 检查冒号后面是否有空格；值里有冒号或引号时，整段用单引号包住，单引号本身写成 `''` |

---

## 10. 许可

主题代码来自 Academic Pages，使用 MIT 许可证（见 `LICENSE`）。网站文字内容版权归作者所有。
