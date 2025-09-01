# Prompt Agent MCP是什么？

## Prompt 

### USER PROMPT

### SYSTEM PROMPT
包含角色，性格，背景知识，语气，系统自动将System Prompt发送给AI模型

一般是系统预设的，但可以修改：
- ChatGPT:Customize ChatGPT;用户写下偏好，偏好自动变成SystemPrompt的一部分

## **AI自动化**

- AutoGPT 
    - 负责在模型、工具和最终用户之间传话的程序叫做AI Agent
    - 提供AI调用的函数或者服务叫做Agent Tool

**AI**概率模型存在**返回格式**不正确的问题
- Cline：采用多次返回解决形式


## AI Agent与AI模型之间的通信方式

### FunctionCalling
ChatGPT，Claude，Gemini推出FunctionCalling的功能

**核心思想**：统一格式，规范描述，进行标准化处理

Ex：每个Tool都用一个JSON对象来定义工具名；**JSON对象**从SystemPrompt中抽象出来

FunctionCalling规定了AI使用工具时应该返回的格式，所以System Prompt中的格式定义也可以删除掉

使用相同的格式，人们就能更加有针对性的训练AI模型**Why**

EX：回复格式固定，AI服务器端可以自己检测，不仅降低用户端的开发难度，也节省了用户端重试带来的**Token**开销

#### FuctionCalling的问题
没有统一的标准，大厂定义的API都不一样，开源模型还不支持Function Calling；

跨模型通用的AI Agent麻烦，因此，System Prompt与FunctionCalling并存

-----

## AI Agent与Agent Tools通信方式

### 便捷做法
- AI Agent与Agent Tools写在同一个程序里面，直接函数调用即可（相同进程）

### MCP通信协议
Tool变成服务统一托管，让所有的Agent来调用；
- 运行Tool的服务叫做MCP Server
- 调用Agent叫做MCP Client


MCP通信协议专门**规范**Agent和Tool服务之间是怎么进行交互的；即MCP Server与MCP Client通信
1. 通信格式
2. 通用接口（查看Tool，功能描述，参数，格式等等接口）
3. 除了普通函数调用的形式，MCP Server也可以直接提供数据，类似文件读写的服务（Resource），为Agent提供提示词的模版叫做Prompt

- MCP Server既可以和Agent跑在同一台机器上，通过标准输入输出进行通信
- 也可以部署在网络上通过HTTP进行通信

**Notes：** MCP是为了AI而制定出来的标准， 但实际上MCP本身和AI模型没有关系，并不关心Agent调用什么模型，只负责帮Agent管理工具、资源和提示词


# AI Agent搭建

## docstring

## API和API文档

### 模型的API：KEY
- 不直接写入代码，不安全；可以直接放入环境变量里面

EX：GEMINI_API_KEY,但手动更改很麻烦，常见做法写入 .env


## 库PydanticAI

### Model Providers



## AI模型Google的Gemini