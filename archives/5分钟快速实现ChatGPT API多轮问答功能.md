最近，ChatGPT异常火爆。在亲自使用了几个月后，我发现它确实能显著提高生产力。对于开发者来说，有时需要在自己的项目中加入智能问答功能。经过简单研究，我找到了一种简单易用的方法，分享给大家参考。

---

## 1. 安装 `openai` 库

我们可以直接使用 Python 中的 `openai` 库来调用 ChatGPT。

### 安装步骤

1. 打开命令行，运行以下命令安装 `openai` 库：
   bash
   pip install openai
   
2. 如果遇到 `pip` 版本过低的问题，可以先升级：
   bash
   pip install --upgrade pip
   
3. 如果安装成功但无法调用库，可能是版本问题，尝试以下命令更新：
   bash
   pip install -U openai
   

### 注意事项

- **Windows 用户**：按 `Win+R`，输入 `cmd` 打开命令行，建议以管理员权限运行。
- 如果安装过程中遇到网络问题，可以尝试切换网络或使用 Anaconda 安装。

---

## 2. 获取 API Key

在调用接口前，需要申请一个 API Key。以下是获取方式：

1. 前往 [OpenAI官网](https://platform.openai.com/account/api-keys) 注册账号并申请 API Key（需科学上网）。
2. API Key 的格式类似于：`sk-xxxxxxxxxxxxxxxxxxxxxxxxxxxx`。

---

## 3. 模型简介

OpenAI 提供了两个专为聊天设计的模型：

- **gpt-3.5-turbo**：需要在 `content` 中明确指定角色和问题内容。
- **gpt-3.5-turbo-0301**：更关注问题内容，对角色部分要求较低（有效期至 6 月 1 日）。

---

## 4. 参数详解

以下是调用 ChatGPT API 时常用的参数：

- **model**：模型名称，可选 `gpt-3.5-turbo` 或 `gpt-3.5-turbo-0301`。
- **messages**：JSON 格式，包含问题描述或角色定义。
- **temperature**：控制结果随机性，`0.0` 表示固定结果，`0.9` 表示更随机。
- **max_tokens**：最大字数，API 支持的最大 token 数为 4096。
- **top_p**：生成文本时考虑概率最高的词语，建议设置为 `1`。
- **frequency_penalty**：控制重复性，建议设置在 `0.6` 到 `1` 之间。
- **stream**：是否流式输出，`True` 表示逐步返回结果，`False` 表示一次性返回。

### `messages` 字段详解

`messages` 字段用于指定角色类型，主要包括以下三种角色：

- **System**：系统角色，负责接受用户请求并转发给助手处理。
- **User**：用户角色，与聊天机器人交互的用户。
- **Assistant**：助手角色，负责生成回答。

示例代码：
python
model = "gpt-3.5-turbo"
messages = [
    {"role": "system", "content": "You are a helpful assistant."},
    {"role": "user", "content": "What year is this year?"},
    {"role": "assistant", "content": "2025"},
    {"role": "user", "content": " xxxx ?"}
]


---

## 5. 调用接口

完成 `openai` 库安装后，可以编写代码实现多轮问答功能。

### 多轮问答示例

python
# -*- coding: utf-8 -*-
import openai

api_key = "在这里填入你的KEY"

openai.api_key = api_key

def askChatGPT(messages):
    MODEL = "gpt-3.5-turbo"
    response = openai.ChatCompletion.create(
        model=MODEL,
        messages=messages,
        temperature=1
    )
    return response['choices'][0]['message']['content']

def main():
    messages = [{"role": "user", "content": ""}]
    while True:
        try:
            text = input('问：')
            if text == 'quit':
                break
            # 添加用户问题
            d = {"role": "user", "content": text}
            messages.append(d)
            # 获取回答
            text = askChatGPT(messages)
            d = {"role": "assistant", "content": text}
            print('答：' + text + '\n')
            messages.append(d)
        except:
            messages.pop()
            print('ChatGPT：error\n')

if __name__ == '__main__':
    main()


运行代码后，在控制台输入问题并按回车，即可获得 ChatGPT 的回答。

### 单次问答示例

python
# -*- coding: utf-8 -*-
import openai

def openai_reply(content, apikey):
    openai.api_key = apikey
    response = openai.ChatCompletion.create(
        model="gpt-3.5-turbo-0301",
        messages=[
            {"role": "user", "content": content}
        ],
        temperature=0.5,
        max_tokens=2048,
        top_p=1,
        frequency_penalty=0.7,
    )
    return response.choices[0].message.content

if __name__ == '__main__':
    content = '我比较喜欢大海，请给我推荐几个景点。'
    ans = openai_reply(content, '在这里填入你的KEY')
    print(ans)


---

## 6. 总结

以上是调用 ChatGPT 接口的完整步骤。如果运行代码时遇到问题，可以尝试以下方法：

1. 找到当前 Python 环境的安装目录。
2. 进入 `openai` 库文件夹（如 `D:\environment\python39\Lib\site-packages\openai`）。
3. 替换 `api_requestor.py` 文件。

👉 [WildCard | 一分钟注册，轻松订阅海外线上服务](https://bit.ly/bewildcard)

理性看待人工智能的发展，正确认识人的不可替代性。让 AI 成为我们生产和生活中的得力助手。

---
