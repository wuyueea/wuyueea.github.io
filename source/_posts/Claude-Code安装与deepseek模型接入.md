---
title: Claude Code安装与deepseek模型接入
date: 2026-05-14 16:21:07
tags:
  - Claude Code
  - deepseek
  - 教程
categories:
  - 技术
  - AI agent
---
## 前言
随着人工智能技术的迅速发展，许多强大的大模型如雨后春笋般不断涌现并飞速迭代。在近几年，因为openclaw的出现与随后兴起的龙虾热，AI的发展开始进入Agent时代，AI所扮演的角色开始从webchat的知识问答工具转变成有潜力渗透日常生活与融合个人工作流的强提效工具甚至“个人助手”。在本篇博客写作期间，较为出名的AI agent工具有Claude Code、Codex、OpenClaw、OpenCode、Hermes Agent等等，每种工具差别主要体现在model能力以及适用场景，出于对Claude Code框架设计哲学与CLI命令行工具的高效、脚本化、低资源占用等优势的考虑，本篇文章主要探讨Claude Code CLI的安装与国内高性价比大模型deepseek API的接入。

## 安装Node.js与Git
分别前往官方网站[Node.js 官网](https://nodejs.org/zh-cn)和[Git 官网](https://git-scm.com/)下载安装包，按默认选项完成安装。
然后在powershell一行行运行版本查看脚本测试安装是否成功：
```bash
node -v
npm -v
git --version
```
如果和下面一样返回类似的版本号就表明安装成功了，可以进入下一步了；若不成功，可将错误直接发给AI排查。
{% asset_img 环境安装测试.png "环境安装测试" %}

## 安装Claude Code CLI
在powershell一行行运行下列代码即可：
```bash
npm config set registry https://registry.npmmirror.com/ # 为npm包管理器配置国内镜像
npm install -g @anthropic-ai/claude-code # 安装Claude Code CLI
claude --version #运行版本检查
```
如果最后的版本检查代码和下面一样返回类似的版本号就表明安装成功了！
{% asset_img 2026-05-14T165548.png %}
这时可以在终端运行 `claude` 进入Claude Code 终端UI界面，但是会显示两行红色的报错 `Unable to connect to Anthropic sevices` 和 `Failed to connect to api.anthropic.com: ERR_BAD_REQUEST` ,主要的意思就是无法连接到官方服务器，这个虽然可以用魔法解决，但是后续的登录步骤又是一个麻烦事，所以后面将修改一个配置文件来直接跳过登录且本地使用Claude Code框架，然后接入国内大模型deepseek的API。

## 登录步骤绕过与deepseek接入
### 登录步骤绕过
进入文件资源管理器（也就是“此电脑”），在上方的路径导航栏中输入 `C:\Users\你的用户名` ，后面要更改为你电脑的的用户名名称，比如我的用户名是 `lenovo` （想要查找自己的用户名，可以进入控制面板，点击“用户账户”-“用户账户”，在里面就可以找到如下方的色块，上面的本地账户即你的用户名）。进入用户文件夹后，可以找到一个名为 `.claude.json` 的文件（后面的 `.json` 是文件扩展名，想要看到这个，就在文件资源管理器中依次点击“查看”-“显示”-“文件扩展名”），右击使用记事本打开，可以看到json格式的代码，上下两个大括号将中间的代码构成一个代码块，在下面大括号的前一行代码最后添加一个英文标点 `,` ，然后换行，输入两个空格，然后添加以下文本 `"hasCompletedOnboarding": true` ,最后保存并退出即可。
{% asset_img 2026-05-14T172127.png %}
现在再打开一个新终端，输入 `claude` 后，将会出现下面显示的提示，这不是报错，只是问你是否信任你刚才修改的配置文件，直接按回车就行，最后就正式进入Claude Code界面了。
{% asset_img 2026-05-14T173721.png %}

### 接入deepseek
虽然成功进入了Claude Code框架，但是内部没有接入大模型就是一个空壳，现在就是为了解决这个问题。
首先为了简化一些步骤以及节省时间，推荐下载一个小工具“cc switch”，前往[cc switch发布页](https://github.com/farion1231/cc-switch/releases)下载最新发布版即可。
然后，前往[deepseek开放平台](https://platform.deepseek.com)，注册登录后，点击左侧的“API keys”，创建API key，注意一定要复制自己的API key，关闭生成页面后就不能再进入复制了。
最后进入cc switch，上面的agent列表第一个应该就是Claude Code，如果没有，可以先去设置页设置，在主页切换到Claude Code的配置页后，点击右上角橙色的加号，选择预设供应商-粘贴API key-将下面的四个模型名称均修改为 `deepseek-v4-pro[1m]` 即可，还可以勾选下面的“最大强度思考”，最后保存退出。现在就可以打开一个新终端输入 `claude` ，按回车，进入Claude Code主界面后，就可以看到deepseek已经接入了，后面添加其他的模型API后，可以输入 `/model` 来切换模型，其他的自行探索。
{% asset_img 2026-05-14T175835.png %}

## 最后的碎碎念
OK啊，第3篇博客到此结束，没想到写这篇的时候文风变得正经了许多（捂脸），也许是因为学习这个已经有一段时间了吧，这篇算是一篇回忆性质的教学博客，往后也会在AI学习了花很多时间，到时候继续出学习记录，下期再见~