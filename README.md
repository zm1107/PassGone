<div align="center">

<img src="assets/img/logo.png" width="170" alt="PassGone">

# PassGone

**忘掉的是密码，找回来的是文件。**

完全离线的文档密码找回工具（Windows）

**🛡️ 完全离线 &nbsp;·&nbsp; ⚡ GPU 实测最高 ≈2,670× &nbsp;·&nbsp; 🗂️ 10 种格式 &nbsp;·&nbsp; 🧠 字典 + 规则双引擎 &nbsp;·&nbsp; ⏸️ 断点续跑 &nbsp;·&nbsp; 🔁 智能去重 &nbsp;·&nbsp; 🌐 中英双语**

`Windows 10 / 11` · `免费版 + 完整版（一次性买断，终身免费升级）`

[官网 passgone.exifmate.com](https://passgone.exifmate.com) · [从微软商店下载](https://apps.microsoft.com/detail/9PNQWBH3W67T) · [隐私政策](https://passgone.exifmate.com/privacy/)

🍗 找回来了？[请作者吃个鸡腿](#请作者吃个鸡腿)

</div>

## 支持格式

| 类型 | 格式 | 加密 |
|---|---|---|
| Office 新版 | docx / xlsx / pptx | Agile 加密（Word / WPS 标准导出） |
| Office 旧版 | doc / xls / ppt | RC4 CryptoAPI |
| PDF | RC4-40、AES-128（R2/R4）、AES-256（R6） | 全系加密标准 |
| 压缩包 | zip、7z、rar | zip（ZipCrypto / AES）；rar 需自备 UnRAR 后端 |

## GPU 实测速度

开启 GPU 加速（可选组件 hashcat）后，旧版 zip（ZipCrypto）实测每秒尝试 **200,000,000 次**，最高提速 **≈2,670 倍**。

| 来源 | 格式 / 加密类型 | CPU 计算（平均） | GPU 计算（平均） | 提升 |
|---|---|---|---|---|
| WPS 2016 Pro | doc（97-2003 RC4） | 64,135/s | 48,000,000/s | ≈748× |
| WPS 2016 Pro | docx（标准加密） | 890/s | 32,353/s | ≈36× |
| WinRAR 7.11 | RAR（RAR5） | 2,100/s | 10,760/s | ≈5× |
| WinRAR 7.11 | zip 新版（WinZip AES） | 75,477/s | 770,000/s | ≈10× |
| WinRAR | zip 旧版（ZipCrypto） | 74,896/s | 200,000,000/s | ≈2,670× |
| Word 2024 | doc（97-2003 RC4） | 72,333/s | 20,800,000/s | ≈288× |
| Word 2024 | docx（Agile 2013+） | 639/s | 1,374/s | ≈2.2× |

> 测试环境：ThinkPad T14P Gen3 · Intel Core Ultra 9 285H · 64GB 6400MHz · Intel Arc 140T。
> 加密越轻（RC4 / ZipCrypto 这类无重迭代的设计），GPU 并行收益越大（数百到数千倍）；带重迭代 KDF 的格式（Agile SHA512-10 万轮、RAR5 PBKDF2）GPU 收益约为 2-36×，但依然全面快于 CPU。

## 它能帮你解决什么

| 你遇到的麻烦 | PassGone 的答案 |
|---|---|
| 加密文档密码忘了一半，只记得大概用过的词 | 导入 txt/csv 字典（每行一个密码），多个字典自动去重合并 |
| 记得组成但排列忘了：名字+生日+数字？ | 勾选大小写/数字/特殊符号，自定义字符，设定长度区间自动生成组合 |
| 几十万候选跑到一半要关机 | 按文件指纹记录进度（区块粒度），重启后自动续跑，绝不重复尝试 |
| 文件多、单个太慢 | 按 CPU 核数多进程并行，界面实时显示每秒速度与预计剩余时间 |
| CPU 太慢等不起 | 一键启用 GPU 加速（可选组件 hashcat），Office 全格式数十倍提速 |
| 同一份文件复制了多份 | 以内容哈希识别，自动合并为一条记录，共享找回结果 |

## 免费版与完整版

| | 免费版 | 完整版 |
|---|---|---|
| 图形界面 / 全部格式探测 | ✓ | ✓ |
| 密码规则生成 | 长度 ≤ 4 位 | 不限 |
| 自定义字典导入 | — | ✓ |
| 并行计算 | 最多 2 线程 | 不限（本机全部核心） |
| 找回记录缓存 | 最近 2 条 | 最近 100 条 |
| 升级 | — | 一次性买断，终身免费升级 |

完整版在微软商店内以附加组件形式购买，价格以[商店页面](https://apps.microsoft.com/detail/9PNQWBH3W67T)为准。

## 使用条款

仅可用于找回**本人拥有或已获明确授权**的文件的密码；严禁用于获取他人文件、侵犯他人隐私或任何违法行为；使用本软件产生的一切法律后果由使用者自行承担。

## 隐私

PassGone **完全离线运行**：应用不含联网功能，不收集任何信息，你添加的文件始终留在你自己的电脑上。详见[隐私政策](https://passgone.exifmate.com/privacy/)。

## 反馈与支持

- 🐛 Bug 与功能建议：微软商店页面的支持渠道
- 📧 邮件：passgone@exifmate.com

## 关于本仓库

本仓库托管 PassGone 官方网站（passgone.exifmate.com）源码：纯静态、零追踪（无统计、无 Cookie、无外部请求），站点口径以 [`docs/site-design.md`](docs/site-design.md) 为准。应用本身为闭源分发，基于下列开源组件构建，许可声明随软件分发。

## 致谢

PassGone 站在以下优秀开源项目的肩膀上，向原作者与开源社区致以诚挚谢意：

| 项目 | 用途 | 许可证 |
|---|---|---|
| [Python](https://www.python.org) / Tcl-Tk | 运行时与 GUI | PSF / Tcl-Tk License |
| [pikepdf](https://github.com/pikepdf/pikepdf) | PDF 读取与口令校验 | MPL-2.0 |
| [qpdf](https://github.com/qpdf/qpdf) | PDF 加密核心 | Apache-2.0 |
| [msoffcrypto-tool](https://github.com/nolze/msoffcrypto-tool) | Office 加密文档处理 | MIT |
| [olefile](https://github.com/decalage2/olefile) | OLE/CFB 结构读取 | MIT |
| [pyzipper](https://github.com/danifunker/pyzipper) | AES-Zip 读写 | MIT |
| [py7zr](https://github.com/miurahr/py7zr) | 7z 格式支持 | LGPL-2.1 |
| [rarfile](https://github.com/markokr/rarfile) | RAR 结构读取 | MIT |
| [Pillow](https://python-pillow.org) | 图标资产处理 | MIT-CMU |
| [hashcat](https://hashcat.net/hashcat/)（可选，用户自备） | GPU 加速后端 | MIT |
| [PyInstaller](https://pyinstaller.org)（打包用） | 可执行文件封装 | GPL-2.0（引导器例外） |

感谢所有开源贡献者——你们让独立开发者也能造出专业级的工具。

## 请作者吃个鸡腿

如果 PassGone 帮到了你，欢迎请作者吃个鸡腿 🍗——你的支持就是持续更新的动力。

<p align="center">
  <img src="assets/img/donate_qr.jpg" alt="微信收款码" width="260">
</p>

> 微信「扫一扫」上方收款码即可支持，金额随意，心意最重要。
