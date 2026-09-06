# PassGone 官方网站 — 需求与设计说明

> 状态：已定稿（v1.0.0） · 日期：2026-09-06
> 本文档先于代码存在；任何口径变更须先回写本文档。

## 1. 需求

为 PassGone（离线文档密码找回工具，Windows）建设官方产品站，结构参考同作者的 ExifMate
官网仓库，配色取自 PassGone 应用图标主色。

- **发布方式**：公开 GitHub 仓库 → Cloudflare Pages 静态托管，域名 `passgone.exifmate.com`
  （用户口述 "passgone@exifmate.com"，域名中 `@` 无效，按子域名口径理解；联系邮箱为
  `passgone@exifmate.com`，待用户确认）。
- **隐私红线（硬性）**：纯静态、零 JavaScript 运行时依赖（仅原生 `onclick` 切换弹层）、
  零分析/统计/追踪、零外部请求（无 CDN 字体、无外链图片）、无 Cookie、无表单。
  仓库内不得出现任何用户数据、操作日志、凭据或本地路径。
- **下载入口**：微软商店 `https://apps.microsoft.com/detail/9PNQWBH3W67T`（唯一权威渠道）。
- **产品口径来源**（权威，禁止编造）：PassGone 应用仓库的 `README.md`、`about_content.py`、
  `docs/PRIVACY.md`、`packaging/THIRD_PARTY_NOTICES.md`。应用版本 1.0.1。

## 2. 品牌配色（取自图标 ico/app_icon.png，像素取色）

| 用途 | 变量 | 值 | 来源 |
|---|---|---|---|
| 主色（品牌蓝） | `--accent` | `#17569B` | 图标背景亮部 |
| 深藏青 | `--accent-deep` | `#14357F` | 图标背景主色 |
| 金黄（钥匙/CTA） | `--gold` | `#FFC32B` | 钥匙主体 |
| 金黄 hover | `--gold-d` | `#F0AD0E` | 金黄加深 |
| 青绿（点缀） | `--teal` | `#179A9C` | 图标青绿字符 |
| Hero 渐变 | — | `#0D1B45 → #14357F → #1D5BA6` | 深蓝径向 |
| 正文墨色 | `--ink` | `#1B2340` | 偏藏青的深墨 |
| 背景 | `--bg` | `#F5F7FB` | 冷灰蓝底 |

图标构成：深蓝圆角方形背景，密码字符圆盘（白/青绿/亮蓝字符），金色钥匙斜穿 —
「忘掉的密码 + 找回的钥匙」。

## 3. 站点结构

```
/                     中文主站（lang=zh-CN）
/en/                  English（lang=en）
/privacy/             隐私政策（中英同页切换，内容来自应用 PRIVACY.md，未增删事实）
/assets/style.css     全站样式（ExifMate 版式骨架 + PassGone 配色）
/assets/img/          logo.png（320，og:image）、donate_qr.jpg（应用内同款收款码）
/favicon.ico|.png、/apple-touch-icon.png   全部由应用图标 512 派生
/robots.txt /sitemap.xml /_headers /.well-known/security.txt
```

主站信息架构（锚点，v1.1.0 起「格式多、速度快」前置，场景痛点后置）：
**支持格式 `#formats`（10 种格式图标芯片）→ GPU 提速 `#speed`（3 张统计卡 + 实测对比表）→
功能 `#features`（2×2）→ 为什么需要 `#pain`（6 卡 + 截图占位）→ 版本对比 `#compare` →
使用条款（警示框）→ 赞助（收款码弹层）→ 页脚**。

### 3.1 实测速度数据（权威口径，逐字使用，禁止改数）

来源：作者 2026-09-06 提供的实测数据。测试环境：ThinkPad T14P Gen3 ·
Intel Core Ultra 9 285H · 64GB 6400MHz · Intel Arc 140T。

| 来源 | 格式/加密类型 | CPU 平均 | GPU 平均 | 提升 |
|---|---|---|---|---|
| WPS 2016 Pro | doc（97-2003 RC4） | 64,135/s | 48,000,000/s | ≈748× |
| WPS 2016 Pro | docx（标准加密） | 890/s | 32,353/s | ≈36× |
| WinRAR 7.11 | RAR（RAR5） | 2,100/s | 10,760/s | ≈5× |
| WinRAR 7.11 | zip 新版（WinZip AES） | 75,477/s | 770,000/s | ≈10× |
| WinRAR | zip 旧版（ZipCrypto） | 74,896/s | 200,000,000/s | ≈2,670× |
| Word 2024 | doc（97-2003 RC4） | 72,333/s | 20,800,000/s | ≈288× |
| Word 2024 | docx（Agile 2013+） | 639/s | 1,374/s | ≈2.2× |

备注（原文）：加密越轻（RC4/ZipCrypto 这类无重迭代的设计）GPU 并行收益越大（数百到数千倍）；
带重迭代 KDF 的格式（Agile SHA512-10 万轮、RAR5 PBKDF2）GPU 收益约为 2-36×，但依然全面快于 CPU。

**宣传数字口径决定**：用户口述「约 2800 倍 / 2.1 亿次每秒」与上表（≈2,670× /
200,000,000/s）存在小幅出入；为保证首页宣传数字与所列实测表自洽，站点统一采用
**表内口径：最高 ≈2,670×、200,000,000/s（2 亿次/秒）**。如口述数字另有测量依据，经用户确认后全局替换。

JSON-LD：`SoftwareApplication`（version 1.0.1，SecurityApplication，offers ¥0）。

## 4. 各文件口径

- **免费版/完整版对比表**：六行口径与 README「免费版与完整版」逐行一致。
- **支持格式表**：Office（Agile）/ Office 旧版（RC4 CryptoAPI）/ PDF（RC4-40、AES-128 R2/R4、
  AES-256 R6）/ zip（ZipCrypto/AES）、7z、rar（需自备 UnRAR 后端）。
- **使用条款**：仅限本人拥有或已获授权文件；后果自负。全文与 README 一致。
- **隐私政策页**：六节中文 + 英文摘要，全部来自应用 `docs/PRIVACY.md`；另增「关于本网站」
  一节（陈述本站自身零追踪事实，属可代码验证的本仓内容）。
- **截图**：暂无成品截图，按 ExifMate 模式放虚线占位框，标注「商店上架后更新」。

## 5. 部署（Cloudflare Pages）

- 构建命令：无；输出目录：`/`（仓库根即站点根）。
- 生产分支 `main`；`_headers` 输出 nosniff / DENY / Referrer-Policy / Permissions-Policy。
- DNS：CNAME `passgone` → Pages 域名（用户侧操作）。

## 6. 版本

| 日期 | 版本 | 说明 |
|---|---|---|
| 2026-09-06 | site v1.0.0 | 首版：中文主站、英文版、隐私政策、全套图标与配套文件 |
| 2026-09-06 | site v1.1.0 | 卖点前置：格式芯片墙 + GPU 实测速度节（含实测表）；痛点场景后置；功能改 2×2 |
