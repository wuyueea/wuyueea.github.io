---
title: claude code接入各大平台API
date: 2026-06-01 13:02:39
tags:
  - Claude Code
  - AI API
---
## 前言
在过去，我一直都是付费使用deepseek官方平台的API，充值的15块deepseek API调用费最近用得差不多了，前面也了解了很多第三方API中转站，譬如OpenRouter、ofox.io等，但是中转站非满血、不稳定的缺点加上要付费的设定就直接触犯了我的逆鳞，不想充钱。而又想到之前还看到一个薅羊毛的知乎帖子“别再花钱调APIKey了！2026最全免费大模型合集，国内外直连、不限额度都有”，抱着尝试的心态，决定来试试看。

## Google AI Studio（Gemini）
### 免费政策
`gemini-3.5-flash`       10 RPM  250 RPD
`gemini 3.1 Flash-Lite`  15 RPM  1000 RPD
`gemini-2.5-flash`       30 RPM  1440 RPD
### API接入步骤
#### 获取API key:
(1)访问[Google AI Studio](https://aistudio.google.com)。
(2)点击左下角“Get API key”进入“API密钥”界面。
(3)点击“创建 API 密钥”，进入密钥设置页，随便写个名字，比如 `Gemini API Key` ,新建个项目，随便取名，比如 `Gemini Project` ,然后点击“创建密钥”，密钥创建成功后跳出密钥复制界面，点击复制按钮把密钥复制到剪贴板（养成密钥创建好就复制密钥的习惯，多数平台当关闭这个界面后就不能复制密钥了）。
#### 配置cc switch：
(1)打开cc switch。
(2)点击右上角加号按钮"+"进入供应商添加页面，选择预设供应商里面的"Gemini Native"，往下滑，在"API key"栏目粘贴刚才复制的密钥，将“请求地址”栏目内容修改为 `https://generativelanguage.googleapis.com/v1beta` ；往下滑，修改“模型映射”栏目里面“模型角色”对应的“实际请求模型”，填写名称在上面的免费政策列出的三个模型任选，三个模型角色的调用模型可重复。
(3)最后点击右下角的“+ 添加”按钮保存。
(4)保存后会看到条目显示“需要路由”才能正常调用，现在点击主界面左上角cc switch图标旁边的设置按钮，进入设置页后点击“路由”,点击“本地路由”，打开下面的两个开关，一个是在主界面显示简易的开关按钮，方便控制路由；一个是总开关，和生成的简易开关功能相同。
(5)打开路由后就可以点击“启用”应用刚才设置好的配置了。

## GitHub Models
### 免费政策
模型：`gpt-5-mini`、`claude-haiku-4.5`、`oswe-vscode-prime`
额度：1并发、10 RPM、10000 TPM（比较特别的每分钟token限制）、150 RPD
### API接入步骤
#### 获取API key：
(1)访问[github](https://github.com)
(2)点击右上角头像 -> Settings（设置），进入设置页面，在左侧菜单最下方找到 Developer settings（开发者设置），点击进入。
(3)点击 Personal access tokens -> Tokens (classic)，点击 Generate new token -> Generate new token (classic)。给 Token 起个名字，比如 `Github models API` ，不需要勾选任何特定的仓库读写权限（全部留空即可），随便设置一个有效期。
(4)点击生成，生成后复制这个 Token（就是API key）。
#### 配置cc switch：
(1)打开cc switch。
(2)点击右上角加号按钮"+"进入供应商添加页面，选择预设供应商里面的"GitHub Copilot"，往下滑，添加API key较特别，绑定自己的github账号就行，用不上API key；将“请求地址”栏目内容修改为 `https://models.inference.ai.azure.com` ；修改“模型映射”的操作和上面一样，复制粘贴上面的免费模型名称就行，也可以点击“请求模型列表”，然后在旁边的下拉菜单中选择。
(3)最后点击右下角的“+ 添加”按钮保存。
(4)保存后同样会看到条目显示“需要路由”，和上面一样打开路由开关就行。
(5)打开路由后就可以点击“启用”应用刚才设置好的配置了。

## OpenRouter
### 免费政策
模型：提供一系列带有 `:free` 标签的完全免费模型，如 `qwen-2.5-coder-32b`、`llama-3.1-70b-instruct`、`gemini-2.5-flash`等。
额度：20 RPM,50 RPD -> 1,000 RPD(充值达到$10)
### API接入步骤
#### 获取API key：
(1)访问[OpenRouter](https://openrouter.ai)
(2)点击右上角头像 -> Preferences；在左侧侧边栏找到“API Keys”，点击“+ new key” ，起个名字，比如 `OpenRouter Free API` ，第四栏“Expiration”设置有效期，点击“Create”，创建成功后复制到剪贴板。
#### 配置cc switch
(1)打开cc switch。
(2)点击右上角加号按钮"+"进入供应商添加页面，选择预设供应商里面的“OpenRouter”。API key粘贴刚才复制的，将“请求地址”栏目内容修改为 `https://openrouter.ai/api/v1` ；API格式选择“OpenAI Chat Completions”；修改“模型映射”的操作和上面一样，复制粘贴上面的免费模型名称。
(3)最后点击右下角的“+ 添加”按钮保存。
(4)保存后同样会看到条目显示“需要路由”，和上面一样打开路由开关就行。
(5)打开路由后就可以点击“启用”应用刚才设置好的配置了。

## Cloudflare Workers AI
### 免费政策
模型：`llama-3-8b-instruct`、`deepseek-coder-6.7b-instruct`等
额度：10,000 个 Neurons（其他数据未知）
### API接入步骤
#### 获取API key：
(1)访问[Cloudflare 控制台](https://dash.cloudflare.com)
(2)左侧菜单栏点击“管理账户” -> “账户 API 令牌” ，点击“创建令牌”，随便填个名称，“权限策略” -> “自定义”里面选择“Workers AI”，设置“令牌过期时间”，然后点击“审核令牌”，审核结束后跳出的页面会显示两个信息“账户ID”和“API Token”，后面两个都需要，暂时不关闭此页面。
#### 配置cc switch
(1)打开cc switch。
(2)点击右上角加号按钮"+"进入供应商添加页面，供应商里面可能找不到带有“Cloudflare”字段的，选择自定义配置。填写供应商名称，如 `Cloudflare Workers AI` ,官网链接可选填，API key回到刚才的页面复制粘贴；将“请求地址”栏目内容修改为 `https://api.cloudflare.com/client/v4/accounts/你的ACCOUNT_ID/ai/v1` ，然后回到刚才的页面复制账户ID，替换url里面的对应位置；API格式选择“OpenAI Chat Completions”；修改“模型映射”的操作和上面一样，复制粘贴上面的免费模型名称。
(3)最后点击右下角的“+ 添加”按钮保存。
(4)保存后同样会看到条目显示“需要路由”，和上面一样打开路由开关就行。
(5)打开路由后就可以点击“启用”应用刚才设置好的配置了。

## Hugging Face
### 免费政策
模型：大小不超过 10B - 20B 的开源模型，如 `Meta-Llama-3-70B-Instruct`、`Qwen2.5-Coder-32B-Instruct`、`Mistral-7B-Instruct-v0.3`等。
额度：1-2个并发，10 RPM
### API接入步骤
#### 获取API key：
(1)访问[Hugging Face](https://huggingface.co)
(2)点击右上角头像 -> Access Tokens（访问令牌）；点击 Create new token ，“Token type”选择“read”，起个名字，比如 `Hugging Face Free API` ，点击“Create token”，创建成功后复制到剪贴板。
#### 配置cc switch
(1)打开cc switch。
(2)点击右上角加号按钮"+"进入供应商添加页面，供应商里面可能找不到带有“Hugging Face”字段的，选择自定义配置。填写供应商名称，如 `Hugging Face` ,官网链接可选填，API key粘贴刚才复制的；将“请求地址”栏目内容修改为 `https://api-inference.huggingface.co/v1` ；API格式选择“OpenAI Chat Completions”；修改“模型映射”的操作和上面一样，复制粘贴上面的免费模型名称。
(3)最后点击右下角的“+ 添加”按钮保存。
(4)保存后同样会看到条目显示“需要路由”，和上面一样打开路由开关就行。
(5)打开路由后就可以点击“启用”应用刚才设置好的配置了。

## 最后的碎碎念
通过上面的介绍，大家对免费额度应该有一定了解了，很明显的局限性在于并发、每分钟、每天的请求限制，以及考虑到免费调用的上下文截断、访问不稳定等各种缺陷，很显然，白嫖只适合个人随便玩玩，做做轻度工作，拿到生产环境是绝对不可能的，有大需求还是乖乖充钱。
另外，本人了解有限，有描述不到位、数据不准确的地方还请多多包涵。