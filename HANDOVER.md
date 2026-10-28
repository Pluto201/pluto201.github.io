# 交接文档：学术个人网站（Academic Pages）

> 更新时间：2026-10-27
> 项目目录：`D:\INTERN\markdownProject\lapis\academic-site\`
> 需求原文：`lapis-cv-vscode-v2.0.0/forphd/pages/prompt.md`
> 下一位执行者（你本人，或可以访问 GitHub 的 agent）只需要按本文第四节操作。

## 一、当前状态

| 项 | 状态 |
|---|---|
| 基于官方模板建站 | ✅ 已完成。模板为 2026-10-27 从 `academicpages/academicpages.github.io` 的 `master` 分支下载的 zip，**不是 git clone**，因此没有模板的 git 历史 |
| 页面内容（英文） | ✅ Home、About、Research、Publications（1 篇）、Projects（2 个）、Experience、CV、Contact |
| 配置 | ✅ `_config.yml`、导航、GitHub Actions 工作流 |
| 文档 | ✅ `README.md`（使用说明）、`TODO.md`（待确认事实）、本文件 |
| 本地构建 | 见第三节 |
| Git 仓库 | ❌ 尚未 `git init`，尚未提交 |
| GitHub 仓库与发布 | ❌ 未创建、未发布。**网站目前没有上线** |

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

本机环境：Windows 10 22631、Node v20.19.5、Python 3.13.7。原本没有安装 Ruby。为了验证构建，在 `D:\INTERN\markdownProject\_tools\Ruby33` 安装了 Ruby 3.3.6（RubyInstaller，带 Devkit）。安装时**没有修改系统 PATH**，也没有关联文件类型。不需要时可以运行该目录下的 `unins000.exe` 卸载。

- `bundle install`：rubygems.org 访问很慢，本机通过 `.bundle/config` 使用了清华镜像（这个文件已被 gitignore，不会提交）。
- `assets/js/main.min.js`：用 `npx uglify-js@3`（npmmirror 镜像）在本地生成。该文件已被 gitignore，线上由 Actions 生成。

### 构建结果

- ❌ **没有完成 Jekyll 构建**。在本机，Ruby 连接 `index.rubygems.org:443` 时反复超时（PowerShell 访问同一地址正常，属于间歇性问题），30 分钟内一个 gem 都没有下载下来。换成清华镜像后，Bundler 退回到逐个下载 gemspec 的旧索引方式，速度过慢，也放弃了。
- ✅ **静态检查已通过**（用 Python 脚本完成）：`_config.yml`、`_data/navigation.yml` 和所有页面的 front matter 都能被 YAML 正常解析；导航和页面正文中的 27 个内部链接都指向存在的 permalink。唯一的例外是 `/sitemap.xml`，它由 `jekyll-sitemap` 插件在构建时生成，属于正常情况。
- ❌ 没有在浏览器中查看页面效果，包括桌面端、移动端和 Mermaid 渲染。

**下一步（在网络正常的环境中执行）**：

```powershell
cd academic-site
bundle install
bundle exec jekyll build      # 应该没有报错
bundle exec jekyll serve -l -H localhost
```

也可以直接推送到 GitHub，由 Actions 完成构建（Linux + Ruby 3.1，网络没有问题），再查看 Actions 日志。

## 四、发布步骤（需要能访问 GitHub）

> **已选定方式 C**：不在本地构建，直接推送到 GitHub，由 Actions 完成第一次构建。
> 因为本地从来没有成功构建过，**第一次 Actions 运行就是第一次真实构建**。如果 build job 失败，请先看 "Build with Jekyll" 步骤的日志：Liquid 或 YAML 报错会给出文件名和行号，修改后重新推送即可。常见原因见 `README.md` 第 9 节。

1. **先处理 `TODO.md` 第一节**：GitHub 用户名、邮箱、项目公开授权、雇主名称、CV PDF。
2. 修改 `_config.yml`，把 `GITHUB_USERNAME` 替换为实际用户名（共 2 处：`url`、`repository`），并填写 `author.github`。
3. 在 GitHub 新建**公开**仓库 `<username>.github.io`，不要初始化任何文件。
4. 在 `academic-site/` 目录执行：
   ```bash
   git init
   git add .
   git status            # 确认没有 vendor/、.bundle/、_site/、Gemfile.lock、assets/js/main.min.js
   git commit -m "Initial academic website based on Academic Pages"
   git branch -M main
   git remote add origin https://github.com/<username>/<username>.github.io.git
   git push -u origin main
   ```
5. 仓库 **Settings → Pages → Source** 选择 **GitHub Actions**。
6. 在 **Actions** 页面确认工作流 "Deploy Academic Pages template site to Pages" 的 build 和 deploy 两个 job 都成功。第一次推送如果发生在第 5 步之前，需要点 **Re-run all jobs**。
7. 按 `README.md` 第 7.3 节逐项检查线上页面。

如果使用的不是 `<username>.github.io` 这个仓库名，要把 `baseurl` 改成 `"/<repo>"`（见 README 第 7.2 节）。

## 五、已知问题和注意事项

- **工作流里的 action 版本**沿用模板当前写法（`actions/checkout@v7.0.1`、`ruby/setup-ruby@v1.328.0`、`actions/configure-pages@v6.0.0`、`actions/upload-pages-artifact@v5.0.0`、`actions/deploy-pages@v5`、Ruby 3.1）。这些在本机无法验证，首次运行时请留意 Actions 日志。
- **Mermaid 图**依赖 jsDelivr CDN（模板默认行为），在本机离线预览时可能不显示，线上正常。字体图标同理。
- **社交分享图 `images/og-image.png`** 和 **favicon** 仍是模板默认图片。
- 模板自带的 `markdown_generator/`、`scripts/`、`Dockerfile` 保留了，但不会发布（已在 `exclude` 中）。
- `_pages/year-archive.html`、`category-archive.html`、`tag-archive.html` 是博客归档页，保留以便以后写博客，目前不在导航中。
