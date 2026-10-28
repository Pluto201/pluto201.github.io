# 交接文档：学术个人网站（Academic Pages）

> 更新时间：2026-10-28
> 项目目录：`D:\INTERN\markdownProject\lapis\academic-site\`
> 需求原文：`lapis-cv-vscode-v2.0.0/forphd/pages/prompt.md`
> 下一位执行者（你本人，或可以访问 GitHub 的 agent）只需要按本文第四节操作。

## 一、当前状态

| 项 | 状态 |
|---|---|
| 基于官方模板建站 | ✅ 已完成。模板为 2026-10-27 从 `academicpages/academicpages.github.io` 的 `master` 分支下载的 zip，**不是 git clone**，因此没有模板的 git 历史 |
| 页面内容（英文） | ✅ Home、About、Research、Publications（1 篇）、Projects（2 个）、Experience、CV、Contact |
| 配置 | ✅ `_config.yml`（用户名已填 `pluto201`）、导航、GitHub Actions 工作流 |
| 文档 | ✅ `README.md`（使用说明）、`TODO.md`（待确认事实）、本文件 |
| 本地构建 | ✅ **已成功**，见第三节 |
| Git 仓库 | ✅ 已 `git init`，分支 `main`，首次提交 `104f030`（260 个文件） |
| GitHub 仓库与发布 | ❌ 未创建、未推送。**网站目前没有上线** |

## 二、内容来源与真实性处理

- 网站内容来自工作区内你已经填写的材料。冲突时按以下优先级取用：`interview-handbook/00-fact-conflicts.md`（你亲自确认过的回答）＞ `forphd/HANDOVER.md` 和 `forphd/CV_change_report_and_checklist.md` ＞ `interview-handbook/*/01-mainline.md` ＞ `prompt.md` ＞ `resume.md`。
- 有疑问的内容没有写上网站，全部登记在 `TODO.md`。其中第五、六节逐条列出了 prompt 或简历中的说法与网站最终写法的差异。
- 最重要的几处差异：
  - 不再使用"成功率提升 20%"，改为"失败率约 10% → 约 7%"。
  - 新架构中不出现 Spark、Hive、DataX。
  - 模型写作 Qwen3.6 27B。
  - 100% 准确率注明"在迁移 Cube 之前测得，澄清后答对也计为正确，不代表泛化能力"。
  - "10 分钟以内"写成目标，不写成已实现。
  - 公司名称没有写，只写 "state-owned enterprise, Beijing"。
- 没有使用的个人信息：邮箱、手机号、照片、公司名称。是否公开由你决定。

## 三、验证记录

> 这一节记录在本机实际执行过的命令和结果。

本机环境：Windows 11 22631、Node v20.19.5、Python 3.13.7。原本没有安装 Ruby。为了验证构建，在 `D:\INTERN\markdownProject\_tools\Ruby33` 安装了 Ruby 3.3.6（RubyInstaller，带 Devkit）。安装时**没有修改系统 PATH**，也没有关联文件类型。不需要时可以运行该目录下的 `unins000.exe` 卸载。

- `bundle install`：**已成功**（2026-10-27 晚）。rubygems.org 仍然很慢（15 秒才拿到响应头），但阿里云镜像可用。本地配置写在该仓库的 `.bundle/config`（已被 gitignore，不会提交）：
  ```yaml
  BUNDLE_PATH: "vendor/bundle"
  BUNDLE_MIRROR__HTTPS://RUBYGEMS__ORG/: "https://mirrors.aliyun.com/rubygems"
  BUNDLE_JOBS: "4"
  ```
  结果：62 个 gem 全部装好，其中 `bigdecimal`、`json`、`prism`、`eventmachine`、`http_parser.rb` 需要编译原生扩展，耗时最长。
- `assets/js/main.min.js`：用 `npx uglify-js@3`（npmmirror 镜像）在本地生成。该文件已被 gitignore，线上由 Actions 生成。

### 构建结果

- ✅ **`bundle exec jekyll build` 成功**（development 和 `JEKYLL_ENV=production` 两种模式都跑通，退出码 0）。
- ✅ **`bundle exec jekyll serve` 冒烟测试通过**：15 个 URL 全部返回 200 —— `/`、`/about/`、`/research/`、`/publications/`、`/projects/`、`/experience/`、`/cv/`、`/contact/`、两个项目页、`/publication/2024-saecmo/`、`/sitemap.xml`、`/feed.xml`、`/robots.txt`、`/files/song2024saecmo.bib`。`/resume` 通过 `redirects.json` 跳到 `/cv/`，生产构建里生成的 meta refresh 指向 `https://pluto201.github.io/cv/`。
- ✅ **内部链接检查通过**（`D:\INTERN\markdownProject\_tools\check_links.py`，解析构建产物里的 href/src）：21 个 HTML 页面、53 个内部链接，无断链。
- ✅ `sitemap.xml` 生成 17 条 URL，全部是 `https://pluto201.github.io/...` 绝对地址，没有本地路径泄漏。
- ⚠️ **仍未在浏览器里看过渲染效果**：桌面端、移动端、深色模式、Mermaid 图的实际显示都没有肉眼确认过。Mermaid 依赖 jsDelivr CDN（`assets/js/_main.js` 里 `MERMAID_URL`），本地离线预览可能不显示，线上正常。
- ⚠️ 构建日志里有大量 Sass `DEPRECATION WARNING`（`if()`、`lighten()` 等），全部来自模板自带的 `_sass/vendor/susy` 和 `_sass/layout/_forms.scss`，**不影响构建**，不用管。

### 本轮修掉的问题

1. **论文页链接 404**（三处）：`permalink` 写成了 `/publication/2024-saecmo`（无尾斜杠），Jekyll 生成的是 `publication/2024-saecmo.html` 文件，而页面里链接指向 `/publication/2024-saecmo`，访问会 404。已把 permalink 和三处链接统一成目录式 `/publication/2024-saecmo/`。**注意：其余页面全部是目录式，只有论文页原来不是。**
2. **`temp.md` 会被发布**：根目录下的 `temp.md`（内部工作笔记，内容为"Dify 工作流 / DolphinScheduler 调度脚本"等）不在 `exclude` 里，被 Jekyll 当静态文件原样复制到 `_site/temp.md`，上线后 `https://pluto201.github.io/temp.md` 可直接下载。已在 `_config.yml` 的 `exclude` 加入 `temp.md`，并加进 `.gitignore`（文件保留在本地，只是不发布、不提交）。

**下一步（如需本地再看一次页面）**：

```powershell
cd academic-site
$env:PATH = "D:\INTERN\markdownProject\_tools\Ruby33\bin;$env:PATH"
bundle exec jekyll serve -l -H localhost
```

## 四、发布步骤（需要能访问 GitHub）

> **已选定方式 C**：不在本地构建，直接推送到 GitHub，由 Actions 完成第一次构建。
> 虽然本地现在已经能成功构建，但 Actions 跑的是 Linux + Ruby 3.1，依赖解析结果可能不同，**第一次 Actions 运行仍然要当第一次真实构建对待**。如果 build job 失败，请先看 "Build with Jekyll" 步骤的日志：Liquid 或 YAML 报错会给出文件名和行号，修改后重新推送即可。常见原因见 `README.md` 第 9 节。

1. **先处理 `TODO.md` 第一节**：邮箱、项目公开授权、雇主名称、CV PDF（GitHub 用户名已于 2026-10-27 定为 `pluto201` 并填入 `_config.yml`）。
2. ~~修改 `_config.yml`，把 `GITHUB_USERNAME` 替换为实际用户名~~ ✅ 已完成：`url`、`repository`、`author.github` 三处都是 `pluto201`，`baseurl` 保持 `""`。
3. 在 GitHub 新建**公开**仓库 `pluto201.github.io`，不要初始化任何文件。
4. 在 `academic-site/` 目录执行（`git init` 和首次提交已完成）：
   ```bash
   git remote add origin https://github.com/pluto201/pluto201.github.io.git
   git push -u origin main
   ```
   提交用的身份是仓库级的 `pluto201 <Pluto201@users.noreply.github.com>`（全局的 `songshiquan <[redacted]>` 未改动）。
5. 仓库 **Settings → Pages → Source** 选择 **GitHub Actions**。
6. 在 **Actions** 页面确认工作流 "Deploy Academic Pages template site to Pages" 的 build 和 deploy 两个 job 都成功。第一次推送如果发生在第 5 步之前，需要点 **Re-run all jobs**。
7. 按 `README.md` 第 7.3 节逐项检查线上页面。

如果使用的不是 `pluto201.github.io` 这个仓库名，要把 `baseurl` 改成 `"/<repo>"`（见 README 第 7.2 节）。

## 五、已知问题和注意事项

- **工作流里的 action 版本**沿用模板当前写法（`actions/checkout@v7.0.1`、`ruby/setup-ruby@v1.328.0`、`actions/configure-pages@v6.0.0`、`actions/upload-pages-artifact@v5.0.0`、`actions/deploy-pages@v5`、Ruby 3.1）。本地无法验证 Actions，首次运行时请留意 Actions 日志。
- **本地构建用 Ruby 3.3.6，Actions 用 Ruby 3.1**，依赖解析结果可能不同；`Gemfile.lock` 已被 gitignore，不要提交。
- **Mermaid 图**依赖 jsDelivr CDN（模板默认行为），在本机离线预览时可能不显示，线上正常。字体图标同理。
- **社交分享图 `images/og-image.png`** 和 **favicon** 仍是模板默认图片。
- 模板自带的 `markdown_generator/`、`scripts/`、`Dockerfile` 保留了，但不会发布（已在 `exclude` 中）。
- `_pages/year-archive.html`、`category-archive.html`、`tag-archive.html` 是博客归档页，保留以便以后写博客，目前不在导航中。
- **`gh` CLI 本机没有安装**，所以建仓库、改 Pages 设置这两步目前只能手动在网页上操作，或者临时安装 `gh` / 提供 PAT。

## 六、本轮新增的辅助脚本

都在 `D:\INTERN\markdownProject\_tools\` 下，**不属于网站仓库**，不会提交：

| 文件 | 作用 |
|---|---|
| `do_bundle_install.sh` | 用阿里云镜像装 gem |
| `do_build.sh` / `do_prod_build.sh` | development / production 构建 |
| `do_serve_check.sh` | 起本地服务器并对 15 个 URL 做 HTTP 冒烟测试 |
| `check_links.py` | 扫描构建产物的 href/src，检查内部链接是否 404 |

`check_links.py` 用 `python -I <脚本> <site目录>` 调用（`-I` 隔离模式，避免当前目录的同名模块被误加载）。
