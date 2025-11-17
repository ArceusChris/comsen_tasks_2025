很多人现在用的AI对话工具往往就是deepseek.com或者豆包kimi什么的，部分比较有技术水平的会翻墙去用ChatGPT、Gemini等。但是这些都有一些问题，比如有些需要付费订阅（ChatGPT 20美元/月），一般来说订阅了一个AI服务就不会同时用别的了。但是有时候我们需要用到不同的模型，比如，分析问题是用ChatGPT5，写论文时要用Gemini 2.5 pro，这样的话只订阅一家不够用，订阅两家又太亏了。而且有的时候还会有订阅了，但是一个月没怎么用，导致订阅花费的20美元浪费了的情况。

而使用下面的方法可以实现效果：

- 按量计费，用多少计费多少（例如，对话一次0.005元），这样用得少的话就不需要花费过多的订阅费
    
- 模型更多：可以同时选择多种模型，如下图
    

![](https://hust-comsen.feishu.cn/space/api/box/stream/download/asynccode/?code=ZGIyZDRlMDE0MzMwOWMwOWQ5MTg3MWY0MGY5M2ZiZTBfUlVtbnVCcU5CMDl6WVdranE4SnVpN01TclpvcE1uaTdfVG9rZW46THM5N2JPRUo3b2htbnZ4T09YR2NmWVpRblFmXzE3NjMzODExNjA6MTc2MzM4NDc2MF9WNA)

云雾 + CherryStudio 大模型API调用教程

> 只需一个 API 密钥，就能调用超过 200 种不同的 AI 模型，OpenRouter 和 Cherry Studio 如何让你轻松管理复杂的 AI 工具链？

### 核心概念

- 云雾（[https://yunwu.ai/](https://yunwu.ai/)）: 一个 AI 模型路由平台，它将超过 200 种不同的 AI 模型（如 [GPT 系列](https://zhida.zhihu.com/search?content_id=259398719&content_type=Article&match_order=1&q=GPT+%E7%B3%BB%E5%88%97&zhida_source=entity)、[Claude](https://zhida.zhihu.com/search?content_id=259398719&content_type=Article&match_order=1&q=Claude&zhida_source=entity)、[Gemini](https://zhida.zhihu.com/search?content_id=259398719&content_type=Article&match_order=1&q=Gemini&zhida_source=entity) 等）集成到一个统一的 API 接口中。用户只需一个 云雾 的API 密钥，就能调用众多模型，而无需为每个模型单独注册和管理密钥。
    
    ![](https://hust-comsen.feishu.cn/space/api/box/stream/download/asynccode/?code=NWM2MjU5MWU1OTY5Y2ZjZDI1N2VkZjQ5NTA3YmIyOWVfWXEycW1ZbXYxd1Nnc0tOb281ZGhGbHV6WWpDUGlyUGtfVG9rZW46VG44VmJrOXZOb005Szd4NUo4dGNWQzdvbktoXzE3NjMzODExNjA6MTc2MzM4NDc2MF9WNA)
    

云雾 API 平台概览

- **Cherry Studio**: 一款功能强大的桌面 AI 助手客户端，支持集成和管理多种大模型 API 平台，方便用户在统一的界面中与不同的 AI 模型进行交互。
    

  

### 第一步：获取 云雾 API 密钥

  

1. 访问 云雾 官方网站并完成注册或登录。
    
2. 点击 控制台-钱包 进行充值。一版初始充值10元就够用很久
    

![](https://hust-comsen.feishu.cn/space/api/box/stream/download/asynccode/?code=ZDYwYThlYzFmZTk1MzllZTY0MzQxOGI5MGNjYTI2MDRfTlE2Qll1MEJSMkJ3ZVNYbWJ4QnFWRThzQlBXc2RCdnlfVG9rZW46U2hleGJTdUEzb3Q3a0d4WDNOemNkUUtEbk9mXzE3NjMzODExNjA6MTc2MzM4NDc2MF9WNA)

3. 进入账户设置或 API 密钥（Keys）管理页面。
    
4. 前往API key管理界面，创建一个新的 API 密钥（API Key），并将其复制保存。这个密钥将以 `sk-or-v1-...`开头。如果不知道API是什么可以看这篇文章：
    

API是什么: 一篇讲透API - 吕攻城师的文章 - 知乎 [https://zhuanlan.zhihu.com/p/347125981](https://zhuanlan.zhihu.com/p/347125981)

创建新API密钥

![](https://hust-comsen.feishu.cn/space/api/box/stream/download/asynccode/?code=ODQ0MWJkYzBmODdkYjdiMDE1MDg3ZGE0ODZkNDFiOGVfWkY3T3FSaGxFY3BaZFZZQkhWT0tjTnRvcnJKcEM2Z0FfVG9rZW46REFiSGJ2Z25Tb3Y0WlV4NFgwa2NLT3RJbklkXzE3NjMzODExNjA6MTc2MzM4NDc2MF9WNA)

一版来说，模型分组选择“自动选择”即可

![](https://hust-comsen.feishu.cn/space/api/box/stream/download/asynccode/?code=MGExYzRmNjYxZWFiYzJiN2NkNzcxYjhmNWIyN2I4YzRfTmtValFaMDJXZGpYWGtFdmVsblBqOGN5Q0FZNjlrSWdfVG9rZW46S2NZRGJNeHBYb1o2OEN4ak0wSGNkVTdnblBoXzE3NjMzODExNjA6MTc2MzM4NDc2MF9WNA)

生成完后，复制API密钥（sk-XXXX）

### 第二步：在 Cherry Studio 中配置 OpenRouter

1. **安装软件**: 前往 Cherry Studio 官网（[https://www.cherry-ai.com/](https://www.cherry-ai.com/)）下载并安装客户端。
    
2. **添加平台**: 打开 Cherry Studio，在左侧菜单栏找到并点击“设置”。在设置页面中，选择“模型平台”选项卡，点击添加。
    
    ![](https://hust-comsen.feishu.cn/space/api/box/stream/download/asynccode/?code=MTVkNTIxN2JmMmRiZDViZDhiMjE2NTk1ZTI1MzUxNjlfM1hlbm0zYnNpM1h3RTBoZ1VpQzJhSDZuWWhDSEhUS2ZfVG9rZW46VTFDYWJEVWZCb2RKZ1h4ZnBkQWNGVThXbkhmXzE3NjMzODExNjA6MTc2MzM4NDc2MF9WNA)
    
    ![](https://hust-comsen.feishu.cn/space/api/box/stream/download/asynccode/?code=NDE2YTcwMjhlMzU2MTEwOWM2ZTVhODViM2JhOTVlNmVfNmROeUNsb0lBSlRucEE4ajBVZ0tsMnhwWk9HSTU5U2hfVG9rZW46R3RuT2JkckZob0JCQ3N4N1BFRWN3ck8zbmloXzE3NjMzODExNjA6MTc2MzM4NDc2MF9WNA)
    

  

3. **填入密钥**: 将你在第一步中复制的 API 密钥粘贴到相应输入框中。API地址填：_**[https://yunwu.ai](https://yunwu.ai/)**_
    

Cherry Studio中填入API key

### 第三步：添加并使用 gpt-5-chat-latest 模型

  

1. **管理模型**: 在 Cherry Studio 的 云雾 配置页面，点击“管理”按钮。Cherry Studio 会自动检测你的 API 密钥所能访问的所有模型。
    
2. **选择模型**: 在弹出的模型列表中，你可以搜索或直接找到 gpt-5-chat-latest。
    
    1. **注意**: gpt-5-chat-latest 是一个较新模型，其在 云雾 上的具体可用性取决于官方的集成进度。如果找不到该模型，你可以选择其他可用模型（模型列表在：[https://yunwu.ai/pricing](https://yunwu.ai/pricing)），如 GPT-4o 或任何免费模型进行测试。
        
3. **添加并检查**: 勾选你想要使用的模型（例如 gpt-5-chat-latest），确认添加。完成后，可以点击“检查”按钮，测试 API 密钥和模型配置是否正确。
    
      
    

### 第四步：开始 AI 对话

1. **进入对话界面**: 返回 Cherry Studio 的主界面，进入“助手”或“聊天”页面。
    
2. **选择模型**: 在对话窗口顶部的模型下拉菜单中，选择你刚刚添加的 gpt-5-chat-latest。
    
3. **发送请求**: 在输入框中输入你的问题或指令，然后发送。Cherry Studio 会通过 云雾 将你的请求发送给 gpt-5-chat-latest，并将结果显示在窗口中。
    
      
    

### 注意事项

  

- **密钥准确性**: 确保你填写的 API 密钥完全正确，否则会收到认证失败的错误。
    
- **网络与延迟**: 调用 API 时可能会因为网络问题出现卡顿或响应缓慢，可以稍后重试。部分模型在返回内容前可能会先输出一些空行。
    
- **免费模型**: OpenRouter 提供了许多免费模，你可以用它们来测试配置是否成功。