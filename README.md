# PassGone 官方网站

[PassGone](https://passgone.exifmate.com/) —— 完全离线的文档密码找回工具（Windows）——的官方产品站。
中文主站 `/`，英文版 `/en/`，隐私政策 `/privacy/`。

## 隐私立场（同样适用于本站）

- 纯静态 HTML + CSS，无构建步骤、无 JavaScript 运行时依赖（仅原生 `onclick` 弹层切换）；
- 零统计、零追踪、零 Cookie、零表单、零第三方请求（字体 / 图标全部自托管）；
- 仓库不含任何用户数据、操作日志或凭据；永远不会加入分析类脚本。

## 目录结构

```
/                     中文主站
/en/                  English
/privacy/             隐私政策（中英同页切换）
/assets/              样式与图片（logo、收款码）
/favicon.ico|.png     站点图标（由应用图标 512px 派生）
/apple-touch-icon.png
/_headers             Cloudflare Pages 安全响应头
/robots.txt /sitemap.xml /.well-known/security.txt
/docs/site-design.md  设计说明（口径变更先改文档）
```

产品功能、版本对比、隐私等口径以 `docs/site-design.md` 记录的来源为准，修改口径须先回写文档。

## 部署（Cloudflare Pages）

1. 本仓库（`main` 分支）连接 Cloudflare Pages；
2. 构建命令留空，输出目录填 `/`（仓库根即站点根）；
3. 自定义域名：`passgone.exifmate.com`（CNAME 指向 Pages 分配的域名）。

## 开发

直接编辑静态文件即可；本地预览可用任意静态服务器，例如：

```bash
python -m http.server 8080
```
