## 什么是 ChatGPT API？

ChatGPT 已经成为许多人日常工作的一部分，帮助完成写周报、翻译、查资料等任务。然而，网页版的 ChatGPT 有时无法满足特定需求。例如，如果你想创建一个关于 Apifox 知识的问答机器人，并在企业微信中使用，这时就需要用到 **ChatGPT API**。

![ChatGPT API](https://cdn.apifox.cn/blog/2025/08/image-61.png)

ChatGPT API 是由 OpenAI 提供的一种接口，能够将 ChatGPT 的强大聊天能力轻松集成到各种应用程序或服务中。

### ChatGPT API 提供的功能

以下是 ChatGPT API 的主要功能：

1. **自然语言语音识别**：支持多语言语音转文字和翻译。
2. **多模态图像生成**：通过文字描述生成高分辨率图像。
3. **智能代码生成**：快速生成代码段，支持多种编程语言。
4. **内容过滤与审查**：识别并过滤不当内容，支持多语言。
5. **大模型微调**：根据业务需求对模型进行个性化调整。
6. **文本嵌入**：将文本映射为固定长度的词向量，用于文本分析。

👉 [WildCard | 一分钟注册，轻松订阅海外线上服务](https://bit.ly/bewildcard)

## 如何调用 ChatGPT API？

许多人认为调用 API 是一件复杂的事情，需要写代码和研究数据结构。但实际上，通过 Apifox 提供的 API 文档，你可以轻松完成调用，甚至无需编写代码。

### 第一步：获取 ChatGPT API Key

调用 API 的第一步是获取 API Key。以下是具体步骤：

- 准备一个海外手机号接收验证码（可通过搜索引擎查找虚拟号码服务）。
- 使用魔法工具将网络环境切换到美国。
- 访问 [ChatGPT 开发者平台](https://platform.openai.com/)，注册并获取 API Key。

完成注册后，进入控制台，点击 **API keys**，然后创建一个新的密钥。

![获取 API Key](https://cdn.apifox.cn/blog/2025/08/image-63.png)

如果觉得上述流程复杂，也可以通过第三方平台购买 API Key（需注意信息安全）。

### 第二步：填写 API Key

获取 API Key 后，打开 [Apifox 提供的 API 文档](https://bit.ly/bewildcard)，点击“调试”按钮。

![填写 API Key](https://cdn.apifox.cn/blog/2025/08/image-64.png)

在“设置变量值”中输入你的 API Key。API Key 只会保存在本地，安全可靠。

### 第三步：调用 API

以图像生成 API 为例：

1. 找到“创建图像”接口。
2. 在 `prompt` 字段中输入描述（如“A colorful sunset over the mountains”）。
3. 设置分辨率（如 1024x1024）。
4. 点击“发送”。

![调用 API](https://cdn.apifox.cn/blog/2025/08/image-66.png)

稍等片刻，你将在返回的响应中看到生成的图像 URL，点击即可查看生成的图片。

## 调试 SSE API

当你与 ChatGPT 交互时，会发现对话是逐字输出的。这是因为 ChatGPT API 的聊天接口采用了 **SSE**（Server-Sent Events）方式返回响应。SSE 的优势在于可以实时显示答案，提升用户体验。

使用 Apifox 客户端可以轻松调试 SSE API：

1. 下载并安装 [Apifox](https://bit.ly/bewildcard)。
2. 在 Apifox 客户端中找到 OpenAI 项目，克隆到自己的团队。
3. 打开“生成聊天消息的自动完成”接口，填写需求内容。
4. 点击“发送”按钮，查看时间线中的响应内容。

![调试 SSE API](https://cdn.apifox.cn/blog/2025/08/image-76.png)

通过时间线功能，你可以优化 API 的服务性能。

## 将 ChatGPT 嵌入到你的应用

Apifox 提供了多种开发语言的示例代码，方便开发者快速集成 API。例如，以下是一个基于 Python Flask 的示例代码：

python
from flask import Flask, render_template, request
import http.client
import json

app = Flask(__name__)

@app.route('/')
def index():
    return render_template('index.html')

@app.route('/send', methods=['POST'])
def send():
    conn = http.client.HTTPSConnection("api.openai.com")
    payload = json.dumps({
       "model": "gpt-3.5-turbo",
       "messages": [
          {
             "role": "user",
             "content": "Hello!"
          }
       ],
       "stream": True
    })
    headers = {
       'Authorization': 'Bearer YOUR_API_KEY',
       'Content-Type': 'application/json'
    }
    conn.request("POST", "/v1/chat/completions", payload, headers)
    res = conn.getresponse()
    data = res.read()
    return data.decode("utf-8")

if __name__ == '__main__':
    app.run(port=5001)


通过以上代码，你可以轻松将 ChatGPT 的对话功能嵌入到自己的应用中。

## 使用 Apifox 生成强大的 API 文档

Apifox 是一款集 API 设计、开发、测试于一体的工具，支持一键生成强大的 API 文档。只需提供 Swagger JSON 文件，即可快速生成可调用的 API 文档。

![Apifox API 文档](https://cdn.apifox.cn/blog/2025/08/image-84.png)

**Apifox = Postman + Swagger + Mock + JMeter**，是开发者的全能助手。

👉 [WildCard | 一分钟注册，轻松订阅海外线上服务](https://bit.ly/bewildcard)