# 交接文档：学术个人网站（Academic Pages）

> 更新时间：2026-10-28
> 项目目录：`D:\ssq_space\academic-site\`
> 需求原文：`lapis-cv-vscode-v2.0.0/forphd/pages/prompt.md`
> 下一位执行者（你本人，或可以访问 GitHub 的 agent）只需要按本文第四节操作。

## 一、当前状态

| 项 | 状态 |
|---|---|
| 基于官方模板建站 | ✅ 已完成。模板为 2026-10-27 从 `academicpages/academicpages.github.io` 的 `master` 分支下载的 zip，**不是 git clone**，因此没有模板的 git 历史 |
| 页面内容（英文） | ✅ Home、About、Research、Publications（1 篇）、Projects（2 个）、Experience、CV、Contact |
| 配置 | ✅ `_config.yml`（用户名已填 `pluto201`）、导航、GitHub Actions 工作流 |
| 文档 | ✅ `README.md`（使用说明）、`TODO.md`（待确认事实）、本文件 |
| 本地构建 | ✅ **已成功**，见第三节（注：本机现已无 Ruby，见第三节的 2026-10-28 更新） |
| Git 仓库 | ✅ 已 `git init`，分支 `main`，5 个提交，历史已重写脱敏，见第七节 |
| GitHub 仓库与发布 | ✅ **已上线**：`Pluto201/pluto201.github.io`（public），Actions 构建成功，**https://pluto201.github.io 可访问**（2026-10-28） |
| 线上验证 | ✅ 15 个 URL 全部 200；sitemap 17 条；内部链接 11 条无断链；无本地路径泄漏 |

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

本机环境（2026-10-27 验证时）：Windows 11、Node、Python 3.13.7。Ruby 3.3.6（RubyInstaller，带 Devkit）当时装在 `D:\INTERN\markdownProject\_tools\Ruby33`，**未修改系统 PATH**。

> ⚠️ **2026-10-28 更新**：项目已迁移到 `D:\ssq_space\academic-site\`，上述 `D:\INTERN\markdownProject\` 目录**已不存在**（其中的 Ruby 3.3.6 与全部辅助脚本一并丢失）。本机当前**没有 Ruby，也没有 Docker**，所以**本地构建路径当前不可用**，构建只能依赖 GitHub Actions。`vendor/bundle/ruby/3.3.0/gems/` 里 61 个 gem 仍然保留，重装 Ruby 3.3 即可离线恢复构建。Node 也已从 v20.19.5 变为 v22.22.3（nvm4w，`C:\nvm4w\nodejs` 是指向 `D:\program\nvm\nvm\v22.22.3` 的符号链接）。

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

**下一步（如需本地再看一次页面）**：需先重装 Ruby 3.3，然后：

```powershell
cd D:\ssq_space\academic-site
bundle exec jekyll serve -l -H localhost
```

`vendor/bundle` 中的 gem 齐全，`bundle install` 可离线完成。辅助脚本见第六节（已丢失，需重写）。

## 四、发布流程（✅ 已于 2026-10-28 完成）

> **方式 C**：不在本地构建，直接推送到 GitHub，由 Actions 完成构建。
> Actions 跑的是 Linux + Ruby 3.3（见 `5c6ae60`），且 `Gemfile.lock` 被 gitignore，**每次运行都会重新解析依赖**，依赖解析结果可能与本地不同。**第一次运行仍应按真实构建对待**；如果 build job 失败，看 "Build with Jekyll" 步骤的日志：Liquid 或 YAML 报错会给出文件名和行号，改完重新推送即可。常见原因见 `README.md` 第 9 节。

实际执行记录：

| # | 步骤 | 结果 |
|---|---|---|
| 1 | 处理 `TODO.md` 第一节 | ✅ 邮箱不公开、项目允许公开、雇主暂不公开（2026-10-28 确认）；CV PDF 仍待补 |
| 2 | `_config.yml` 填用户名 | ✅ `url`、`repository`、`author.github` 三处；`baseurl` 保持 `""` |
| 3 | 建公开仓库 | ✅ `Pluto201/pluto201.github.io`，public |
| 4 | 推送 | ✅ `git push -u origin main`（5 个提交，历史已脱敏） |
| 5 | Actions 构建 | ✅ "Deploy Academic Pages template site to Pages" 两个 job 全绿（run #40703601743） |
| 6 | 线上验证 | ✅ 15 个 URL 全 200；sitemap 17 条；内部链接无断链；无本地路径泄漏 |

> ⚠️ **还有一件手动事没做**：仓库 **Settings → Pages → Build and deployment → Source** 需要选择 **GitHub Actions**。
> 原因：`<user>.github.io` 仓库在首次推送时会被 GitHub 自动启用"从分支构建"，于是同时触发内置的 `pages build and deployment` 工作流——它用旧版 Jekyll 构建器、不加载本项目依赖，**该 run 必然失败**（`Build with Jekyll` 步骤红）。它不会覆盖线上站点（失败后 `Upload artifact` 与 `deploy` 均 skipped），但每次推送都会多一条失败记录、干扰排查。切到 GitHub Actions 后即停止。
>
> 如果将来要换仓库名（不是 `pluto201.github.io`），要把 `baseurl` 改成 `"/<repo>"`（见 README 第 7.2 节）。

## 五、已知问题和注意事项

- **工作流里的 action 版本**沿用模板当前写法（`actions/checkout@v7.0.1`、`ruby/setup-ruby@v1.328.0`、`actions/configure-pages@v6.0.0`、`actions/upload-pages-artifact@v5.0.0`、`actions/deploy-pages@v5`、**Ruby 3.3**）。本地无法验证 Actions，首次运行时请留意 Actions 日志。
- **本地构建用 Ruby 3.3.6，Actions 用 Ruby 3.3**；且 `Gemfile.lock` 已被 gitignore，Actions 每次运行都重新解析依赖，结果可能与本地不同。
- **Mermaid 图**依赖 jsDelivr CDN（模板默认行为），在本机离线预览时可能不显示，线上正常。字体图标同理。
- **社交分享图 `images/og-image.png`** 和 **favicon** 仍是模板默认图片。
- 模板自带的 `markdown_generator/`、`scripts/`、`Dockerfile` 保留了，但不会发布（已在 `exclude` 中）。
- `_pages/year-archive.html`、`category-archive.html`、`tag-archive.html` 是博客归档页，保留以便以后写博客，目前不在导航中。
- **`gh` CLI 本机没有安装**，所以改 Pages 设置这一步只能手动在网页上操作，或者临时安装 `gh` / 提供 PAT。
- **GitHub 内置的 `pages build and deployment` 工作流会失败**：`<user>.github.io` 仓库首次推送会被自动启用"从分支构建"，该工作流用旧 Jekyll 构建器、跑不了本项目依赖，必然红。它不影响线上站点（`Upload artifact` 与 `deploy` 均 skipped），但请到 **Settings → Pages → Source 选 GitHub Actions** 关掉它，否则每次推送都会多一条失败记录。

## 六、本轮新增的辅助脚本

曾放在 `D:\INTERN\markdownProject\_tools\` 下，**不属于网站仓库**，不会提交。⚠️ **2026-10-28：该目录已随项目迁移而丢失**，下列脚本需要时须重写：

| 文件 | 作用 |
|---|---|
| `do_bundle_install.sh` | 用阿里云镜像装 gem |
| `do_build.sh` / `do_prod_build.sh` | development / production 构建 |
| `do_serve_check.sh` | 起本地服务器并对 15 个 URL 做 HTTP 冒烟测试 |
| `check_links.py` | 扫描构建产物的 href/src，检查内部链接是否 404 |

`check_links.py` 用 `python -I <脚本> <site目录>` 调用（`-I` 隔离模式，避免当前目录的同名模块被误加载）。

## 七、推送前的隐私处理（2026-10-28）

按本人决定：**项目描述允许公开**，**雇主名称与邮箱不公开**。

推送到公开仓库前对全仓库做了一次敏感串扫描，发现并清除：

| 位置 | 原内容 | 处理 |
|---|---|---|
| `TODO.md` | 雇主中文名与英文正式名 | 从文档中移除，只保留"暂不公开"这个决定本身 |
| `HANDOVER.md` | 雇主邮箱域名 | 替换为 `[redacted]` |
| `TODO.md` / `HANDOVER.md` | 个人邮箱 | 替换为 GitHub noreply 地址 |
| 全部提交的作者与提交者元数据 | 个人邮箱 | 重写为 `Pluto201@users.noreply.github.com` |

因为仓库**从未推送过**（远端 0 个 ref，历史尚未公开），用 `git filter-branch --tree-filter` + `--env-filter` 重写了全部提交，上述字符串在**任何 commit 中都不再存在**。核对方法：

```bash
# 逐个提交扫描（敏感模式本身已刻意不在此文档中出现，故用占位符）
git rev-list --all | while read c; do git grep -l -E "<敏感模式>" $c; done
# 查看所有提交者邮箱
git log --all --format='%ae %ce'
```

> 本文档**刻意不写出被清除的敏感串原文**——否则这份文档自己就成了新的泄露点。同理，脱敏脚本本身也放在仓库之外，不进入任何提交。

> ⚠️ **给下一个接手的人**：`_config.yml` 的 `exclude` 只影响 **Jekyll 构建产物**，**不影响 GitHub 上文件是否可见**。凡是被 git 提交的 `TODO.md`、`HANDOVER.md` 这类内部文档，**推上去就是公开的**，`git log -p` 随时能翻出来。仓库从未推送过时是唯一一次能干净清除历史的机会，一旦推送再改就只是"掩盖"而非"删除"。
