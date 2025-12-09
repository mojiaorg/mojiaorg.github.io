+++
date = '2025-12-09T17:01:44+08:00'
draft = false
title = 'Hugo发布文章心路历程'
+++

从零到上线：我的第一篇 Hugo 博客发布实录（含国内网络避坑指南）
2025年12月9日 · 阅读约 5 分钟

标签：#Hugo #GitHub Pages #静态博客 #技术笔记

最近我决定搭建一个属于自己的技术博客，选择了轻量、快速、开源的 Hugo 静态网站生成器，并托管在 GitHub Pages 上。整个过程看似简单，却踩了不少“中国特色”的坑——尤其是网络连接问题。今天，我就把从写文章到成功上线的完整流程记录下来，希望能帮后来者少走弯路。

🧩 第一步：创建新文章
Hugo 提供了便捷的命令来生成新文章：

powershell
编辑
hugo new posts/我的新文章.md
这会在 content/posts/ 目录下创建一个 Markdown 文件，内容类似：

md
编辑
+++
title = "我的新文章"
date = 2025-12-09T18:00:00+08:00
draft = true
+++

在这里写下你的思考……
⚠️ 关键提醒：默认 draft = true 表示这是草稿，不会在线上显示！

要让文章公开，必须将其改为 draft = false，或直接删除这一行。

🔍 第二步：本地预览验证
在推送前，务必本地预览：

powershell
编辑
hugo server -D
访问 http://localhost:1313，确认：

文章出现在首页
内容、图片、格式正常
无构建错误（如模板缺失、Front Matter 语法错误）
-D 参数表示包含草稿，方便调试。

🚧 第三步：最大的坑 —— Git 推送失败！
当我尝试推送时，反复遇到：

text
编辑
fatal: unable to access 'https://github.com/...': Failed to connect to github.com port 443
或

text
编辑
Recv failure: Connection was reset
这并非代码问题，而是中国大陆网络对 GitHub HTTPS 的干扰所致。

✅ 解决方案：改用 SSH 协议
生成 SSH 密钥（若未生成）：
powershell
编辑
ssh-keygen -t ed25519 -C "your_email@example.com"
将公钥添加到 GitHub：
复制 ~/.ssh/id_ed25519.pub 内容
访问 GitHub → Settings → SSH and GPG keys
点击 New SSH key 并粘贴
修改远程仓库地址为 SSH：
powershell
编辑
git remote set-url origin git@github.com:mojiaorg/mojiaorg.github.io.git
测试连接：
powershell
编辑
ssh -T git@github.com
看到 Hi mojiaorg! You've successfully authenticated... 即成功！
从此，git push 再也不受网络干扰！

📤 第四步：正确提交与推送
这里还有一个小陷阱：文件名编码问题。

我在 PowerShell 中看到 Git 提示：

text
编辑
Untracked files:
  "content/posts/\346\210\221\347\232\204\346\226\260\346\226\207\347\253\240.md"
这其实是 我的新文章.md 的 UTF-8 转义形式。解决方法很简单：

powershell
编辑
# 先确认真实文件名
dir content\posts\

# 再用真实名称添加
git add "content/posts/我的新文章.md"
git commit -m "feat: 发布《我的新文章》"
git push origin main
✅ 推送成功！输出显示：

text
编辑
To github.com:mojiaorg/mojiaorg.github.io.git
   xxxxx..xxxxx  main -> main
🌍 第五步：线上验证
等待 1~2 分钟后，访问：

👉 https://mojiaorg.github.io

强制刷新（Ctrl+F5），新文章赫然出现在首页！🎉

💡 经验总结
问题	解决方案
文章不显示	检查 draft = false
Git 推送超时	改用 SSH 协议
中文文件名乱码	用 dir 查看真实名称再添加
线上未更新	等待 + 强制刷新，检查 GitHub Actions 是否成功
🎁 结语
搭建个人博客不仅是技术实践，更是知识沉淀的开始。虽然过程中遇到了网络、编码、配置等小问题，但每解决一个，就离“掌控自己的数字花园”更近一步。

现在，轮到你了！

如果你也在尝试 Hugo + GitHub Pages，欢迎留言交流～

本文源码已同步至 GitHub，欢迎 Star 或 Fork！

Front Matter（用于 Hugo）
将以下内容放在文章最顶部（替换自动生成的部分）：

toml
编辑
+++
title = "从零到上线：我的第一篇 Hugo 博客发布实录（含国内网络避坑指南）"
date = 2025-12-09T19:00:00+08:00
draft = false
tags = ["Hugo", "GitHub Pages", "静态博客", "技术笔记"]
author = "Wine"
+++
你可以直接将这篇文章保存为 content/posts/hugo-blog-journey.md，然后：

powershell
编辑
git add content/posts/hugo-blog-journey.md
git commit -m "docs: 添加 Hugo 发布实录文章"
git push origin main
很快，它就会出现在你的博客上！✨