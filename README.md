# CCET_web 网站维护说明

本仓库用于发布 Climate Change and Energy Transition Research Centre（CCETRC）网站。

- 网站：<https://nnu-ccet.cn/>
- 仓库：<https://github.com/waykire/CCET_web>
- 技术形式：HTML + CSS + JavaScript 静态单页网站，无需数据库或构建步骤。
- 发布方式：GitHub Pages 从 `main` 分支的仓库根目录发布。

## 1. 网站如何运行

```text
维护者修改文件 → 提交到 GitHub → 改动进入 main 分支
                                      ↓
                              GitHub Pages 自动发布
                                      ↓
                           访客打开 nnu-ccet.cn
```

GitHub 仓库保存文件及修改历史，GitHub Pages 提供网站访问服务。腾讯云/DNSPod 负责域名解析，将域名指向 GitHub Pages；日常更新内容不需要登录腾讯云或修改解析。

网站不依赖维护者电脑保持开机。本地修改不会自动上线；GitHub 上的修改也不会自动同步到本地，需要提交、推送或拉取。

**多人维护时，以仓库最新版本为准。不要用旧的整站备份覆盖仓库。**

## 2. 文件结构

```text
CCET_web/
├── README.md                 本维护说明
├── index.html                所有页面栏目与文字内容
├── CNAME                     自定义域名：nnu-ccet.cn
├── .nojekyll                 告诉 GitHub Pages 跳过 Jekyll 处理
├── assets/
│   ├── css/main.css          页面布局、颜色、字体和响应式样式
│   ├── js/main.js            导航、动画、论文筛选等交互
│   ├── img/
│   │   ├── team/             成员照片
│   │   ├── portfolio/        论文配图
│   │   └── …                 标志、首页背景、网站图标
│   └── vendor/               Bootstrap、AOS 等第三方资源
└── rui-zhu/pdf/               网页使用的论文 PDF（沿用现有目录名）
```

普通内容更新主要修改 `index.html`，并按需增加图片或 PDF。通常不需要改动 `assets/vendor/`、`CNAME` 和 `.nojekyll`。不要单独移动 PDF 目录，否则现有链接会失效。

## 3. 内容在哪里修改

在编辑器中打开 `index.html`，按下表搜索对应的 `id`。行号会随内容变化，建议按栏目定位。

| 网站栏目 | 搜索标记 | 常见修改 |
| --- | --- | --- |
| 首页 Home | `id="hero"` | 首页标题、介绍、背景图引用 |
| 简介 About | `id="about"` | 研究中心简介 |
| 研究 Research | `id="services"` | 研究方向、重点论文链接 |
| 论文 Publications | `id="publications"` | 论文标题、配图、摘要、链接和分类 |
| 成员 People | `id="team"` | 姓名、职称、单位、照片、排列顺序 |
| 联系 Contact | `id="contact"` | 地址、邮箱、电话、社交账号 |
| 招聘 Hiring | `id="hiring"` | 招聘要求、岗位及人数 |
| 页脚 | `id="footer"` | 单位名称、版权信息、底部链接 |

Contact 中目前仍有 `TBD` 联系方式占位文字，取得确认的信息后再更新。

### 修改或新增成员

下面是现有成员卡片的结构，可复制整个外层 `div` 后修改：

```html
<div class="col-lg-4 col-md-6 col-12" data-aos="fade-up" data-aos-delay="150">
  <article class="team-member">
    <div class="pic"><img src="assets/img/team/shanchuan-guo-uniform.png" alt="Shanchuan Guo" loading="lazy"></div>
    <div class="member-info">
      <h3>Shanchuan Guo</h3>
      <p class="member-role">Lecturer</p>
      <p class="member-affiliation">School of Geography<br>Nanjing Normal University</p>
    </div>
  </article>
</div>
```

1. 将照片放入 `assets/img/team/`，使用清楚的英文文件名，例如 `givenname-surname-uniform.webp`。
2. 修改 `img` 的 `src` 路径和 `alt` 姓名，以及 `h3`、`member-role`、`member-affiliation`。
3. 需要换行时使用 `<br>`，不要破坏已有 HTML 标签。
4. 卡片在 HTML 中的先后顺序就是显示顺序。桌面宽屏每行三位，较窄屏幕会自动调整；要放在第一行第三位，就将完整卡片放在第三个位置。
5. `data-aos-delay` 仅控制动画延迟，不控制成员排序。新增卡片时可参照相邻值设置。

照片建议采用正方形、浅灰绿色背景、相近的人像大小与构图，例如 800 × 800 像素。页面会将照片裁成圆形并自适应显示，但 CSS 不会自动统一照片背景和人物比例，应先准备好图片。PNG 和 WebP 都可使用，优先控制体积并保持面部清晰。

当前 Guo 和 Dang 的职称均为 `Lecturer`；Guo 的单位为 `School of Geography / Nanjing Normal University`。实际人员信息调整应以确认后的内容为准。

### 修改或新增论文

1. 在 `id="publications"` 内复制一整个 `portfolio-item isotope-item` 卡片。
2. 将配图放入 `assets/img/portfolio/`；需要提供 PDF 时放入 `rui-zhu/pdf/`，也可直接使用 DOI 或期刊页面链接。
3. 同时更新图片链接和标题链接两处 `href`，以及图片 `src`、`alt`、论文标题和介绍文字。
4. 为卡片保留适用的分类，可使用一个或多个：

   - `filter-energy-transition`
   - `filter-climate-change`
   - `filter-risk-management`
   - `filter-information-geography`

5. 如果 Research 栏目也引用了这篇论文，搜索旧文件名或旧 URL，核对所有引用位置。

增加全新分类时，需同时更新筛选按钮的 `data-filter` 和卡片上的对应 class。只增加论文时通常不需要修改 JavaScript。

### 调整外观

修改 `assets/css/main.css` 中对应栏目样式。例如 People 的样式可搜索 `Team Section` 或 `.team .team-member`。全站颜色位于文件开头的 CSS 变量中。修改后需同时检查桌面和手机宽度，避免只对某一张卡片临时调整导致其他成员显示不一致。

## 4. 如何修改和提交

维护者应使用自己的 GitHub 账号。仓库所有者可在 **Settings → Collaborators** 中邀请长期维护人员，对方接受邀请后获得协作权限，无需共享账号密码。

### 方式 A：GitHub 网页编辑，适合少量文字修改

1. 打开仓库，找到 `index.html`，点击编辑按钮。
2. 搜索需要修改的栏目或姓名，修改对应文字。
3. 点击 **Commit changes**，填写清楚的说明，例如“更新成员职称”。
4. 建议选择创建新分支并发起 **Pull Request（修改申请）**，由负责人查看差异后合并到 `main`。

拥有写权限且分支规则允许时，也可以直接提交到 `main`；这会触发正式网站更新。当前仓库没有配置供每个 Pull Request 自动预览的网站，提交申请并不代表改动已上线。

如果涉及多张图片、PDF 或较大版式调整，使用下面的本地方式更便于一起预览和提交。

### 方式 B：本地编辑，适合图片和布局修改

先安装 Git 和文本编辑器（例如 VS Code），再将仓库克隆到自己的工作目录：

```bash
git clone https://github.com/waykire/CCET_web.git
cd CCET_web
```

已有本地副本时，不需要重复克隆。每次开始修改前，先用 `git status` 确认没有未处理的本地改动，再同步主分支并创建本次工作分支：

```bash
git switch main
git pull --ff-only origin main
git switch -c update-people
```

`update-people` 是示例分支名，每次任务可换成新的描述性名称。如果同步失败或提示冲突，先处理现有改动，不要强制覆盖远程。

修改并完成预览后，只添加本次需要的文件。例如，只修改成员文字时：

```bash
git diff
git add index.html
git diff --cached
git commit -m "Update People information"
git push -u origin update-people
```

如果增加了照片或 PDF，也要用 `git add` 添加对应的实际文件路径。首次提交如提示缺少身份信息，按 Git 提示配置自己的姓名和提交邮箱；推送时使用自己的 GitHub 登录授权。

然后到 GitHub 创建 Pull Request，说明改动和检查结果，由负责人合并到 `main`。合并后，下次工作前重新同步 `main`。这个审核流程是维护建议，是否强制执行取决于仓库的分支保护设置。

## 5. 本地预览与发布检查

简单文字和布局修改可以先用浏览器打开本地 `index.html`。如本地文件模式出现资源限制，使用本地 HTTP 服务预览；例如，在已安装 Python 的电脑上，在仓库根目录运行：

```bash
python -m http.server 8000 --bind 127.0.0.1
```

然后打开 <http://127.0.0.1:8000/>，检查结束后按 `Ctrl+C` 停止服务。Windows 上如安装的是 Python 启动器，可将命令中的 `python` 替换为 `py`。此服务仅用于本地预览，不会发布网站。

提交前检查：

- [ ] 姓名、职称、单位、论文及联系方式准确。
- [ ] 所有图片正常显示；成员顺序与头像裁剪正确。
- [ ] 导航、论文筛选、PDF 和外部链接可用。
- [ ] 缩窄浏览器窗口或使用手机视图后，没有明显重叠或横向溢出。
- [ ] 文件路径使用 `/`，且大小写与真实文件名一致；没有 `C:\`、`F:\` 或 `file:///` 等本地路径。
- [ ] 提交中仅包含需要公开的网站文件，没有无关草稿、原始简历或凭据。

改动合并到 `main` 后：

1. 在仓库 **Actions** 中查看 Pages 构建/部署任务是否成功。
2. 在 **Settings → Pages** 中查看发布地址；当前配置为 `main` 分支、`/(root)`。
3. 等待部署完成，再打开 <https://nnu-ccet.cn/> 检查实际页面。
4. 如果仍看到旧内容，尝试强制刷新（Windows 常用 `Ctrl+F5`）或无痕窗口，并确认查看的提交已经部署。

不要为了普通内容更新改动 DNS、`CNAME` 或 HTTPS 配置。根目录入口文件名应保持为 `index.html`。

## 6. 常见问题与恢复

| 现象 | 优先检查 |
| --- | --- |
| 本地改了，线上没变化 | 是否已推送；改动是否进入 `main`；Pages 部署是否完成 |
| GitHub 已更新，本地还是旧内容 | 本地切换到 `main` 后同步；先处理未提交改动 |
| 图片或 PDF 在线上打不开 | 文件是否提交；路径及大小写是否完全一致 |
| 修改了照片，但仍显示旧图 | 等待部署并强制刷新；必要时更换文件名，同时更新 `src` |
| 成员排序不对 | 检查完整卡片在 HTML 中的先后顺序，而非动画延迟 |
| 新论文不出现在某分类 | 卡片上的 `filter-*` 是否匹配筛选按钮 |
| 域名打不开 | 先检查 Pages 部署与域名验证状态，再由域名管理员检查 DNS |

改错时优先通过新的提交恢复正确内容。可以从文件历史中找到旧版，将需要恢复的部分提交为一次新修改；通过 Pull Request 合并的改动，也可在 GitHub 提供 **Revert** 按钮时创建回退申请。恢复进入 `main` 并部署后生效，不要用强制推送覆盖共享历史。

## 7. 维护原则和参考资料

- 一次提交围绕一个清楚的修改目的，便于审核和恢复。
- 保持现有目录和命名习惯；移动或改名文件时同步修正所有引用。
- 保留第三方模板和库中的作者、来源及许可说明。
- 网站结构或发布方式调整后，同步更新本 README。

参考：[GitHub 网页编辑文件](https://docs.github.com/en/repositories/working-with-files/managing-files/editing-files)、[协作流程](https://docs.github.com/en/get-started/using-github/github-flow)、[邀请协作者](https://docs.github.com/en/repositories/managing-your-repositorys-settings-and-features/repository-access-and-collaboration/inviting-collaborators-to-a-personal-repository)。
