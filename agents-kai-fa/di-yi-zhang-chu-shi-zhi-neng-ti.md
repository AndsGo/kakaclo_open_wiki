---
description: sxl
icon: ghost
---

# 第一章 初识智能体

欢迎来到智能体的世界！在人工智能浪潮席卷全球的今天，**智能体（Agent）**&#x5DF2;成为驱动技术变革与应用创新的核心概念之一。无论你的志向是成为 AI 领域的研究者、工程师，还是希望深刻理解技术前沿的观察者，掌握智能体的本质，都将是你知识体系中不可或缺的一环。

为了解释什么是智能体，我们先从一个类比开始\[2]。

来见见 Alfred。Alfred 是一个**智能体**。

想象 Alfred **收到一个指令**，比如：“Alfred，我想来杯咖啡。”

因为 Alfred **理解自然语言**，他很快就明白了我们的请求。

在完成任务之前，Alfred 会进行**推理和规划**，弄清楚他需要的步骤和工具：

1. 去厨房
2. 使用咖啡机
3. 煮咖啡
4. 把咖啡拿回来

一旦有了计划，他就**必须行动**。为了执行计划，**他可以使用他所知道的工具列表中的工具**。

在这个例子中，为了煮咖啡，他使用了咖啡机。他启动咖啡机来煮咖啡。

<figure><img src="../.gitbook/assets/process.jpg" alt=""><figcaption></figcaption></figure>

### 1.1 什么是智能体？

> 在人工智能领域，智能体被定义为任何能够通过**传感器（Sensors）**&#x611F;知其所处**环境（Environment）**，并**自主**地通过**执行器（Actuators）**&#x91C7;取**行动（Action）**&#x4EE5;达成特定目标的实体。

真正赋予智能体"智能"的，是其**自主性（Autonomy）**。智能体并非只是被动响应外部刺激或严格执行预设指令的程序，它能够基于其感知和内部状态进行独立决策，以达成其设计目标。这种从感知到行动的闭环，构成了所有智能体行为的基础。

#### 1.1.1 传统智能体

在当前**大语言模型（Large Language Model, LLM）**&#x7684;热潮出现之前，人工智能的先驱们已经对“智能体”这一概念进行了数十年的探索与构建。这些如今我们称之为“传统智能体”的范式，并非单一的静态概念，而是经历了一条从简单到复杂、从被动反应到主动学习的清晰演进路线。

**传统智能体类型对比表**

| 类型                                        | 核心机制                    | 特点                    | 典型例子          | 优势               | 局限性                    |
| ----------------------------------------- | ----------------------- | --------------------- | ------------- | ---------------- | ---------------------- |
| **反射智能体 (Simple Reflex Agent)**           | 条件–动作规则 (if-then)       | 无记忆，仅依赖当前感知           | 自动恒温器         | 简单高效，反应快         | 无法处理复杂上下文，短视           |
| **基于模型的反射智能体 (Model-Based Reflex Agent)** | 内部世界模型 (World Model)    | 具备初级“记忆”，能推断不可直接感知的状态 | 隧道中的自动驾驶汽车    | 决策更连贯，能处理部分不可见信息 | 模型依赖设计者，仍有限制           |
| **基于目标的智能体 (Goal-Based Agent)**           | 目标驱动 + 规划 (Planning)    | 主动选择行动以达成未来目标         | GPS 导航系统      | 有前瞻性，能处理复杂任务     | 目标单一，缺乏权衡能力            |
| **基于效用的智能体 (Utility-Based Agent)**        | 效用函数 (Utility Function) | 在多个目标间权衡，最大化满意度       | 导航时考虑时间、油耗、拥堵 | 更接近人类理性决策        | 效用函数设计复杂，需大量先验知识       |
| **学习型智能体 (Learning Agent)**               | 性能元件 + 学习元件，强化学习 (RL)   | 能通过经验不断改进策略，自我进化      | AlphaGo Zero  | 不依赖人类预设，能发现新策略   | 学习过程需大量数据与计算，可能产生不可控行为 |

* **演进方向**：从被动反应 → 主动规划 → 理性权衡 → 自主学习。
* **关键突破**：每一代智能体都在解决前一代的局限性，逐步逼近“类人智能”。
* **现实意义**：这些传统智能体为今天的 **LLM 驱动智能体** 奠定了理论与实践基础。

#### 1.1.2 LLM 智能体

以**GPT（Generative Pre-trained Transformer）**&#x4E3A;代表的大语言模型的出现，正在显著改变智能体的构建方法与能力边界。由大语言模型驱动的 LLM 智能体，其核心决策机制与传统智能体存在本质区别，从而赋予了其一系列全新的特性。

**传统智能体与 LLM 智能体对比**

<figure><img src="https://raw.githubusercontent.com/datawhalechina/Hello-Agents/main/docs/images/1-figures/1757242319667-2.png" alt=""><figcaption></figcaption></figure>

* **传统智能体**：像“专用工具”，擅长在明确规则下完成任务。
* **LLM 智能体**：更像一个“通用大脑”，能理解模糊目标、动态调整策略，并整合多种工具完成复杂任务。

总结而言，智能体是一个系统，它使用人工智能模型（通常是大语言模型）作为其核心推理引擎，以实现以下功能：

* **理解自然语言**：以有意义的方式解释和回应人类指令。
* **推理与规划**：分析信息、做出决策并制定解决问题的策略。
* **与环境交互**：收集信息、执行操作并观察这些操作的结果。

### 1.2 什么是LLM

现在你已经对智能体有了扎实的理解，现在我们探讨智能体的“大脑”：大型语言模型（LLM）。

#### 1.2.1 什么是大语言模型

大语言模型 (LLM) 是一种擅长理解和生成人类语言的人工智能模型。它们通过大量文本数据的训练，能够学习语言中的模式、结构，甚至细微差别。这些模型通常包含数千万甚至更多的参数。\[1]

如今，大多数大语言模型都是基于 Transformer 架构构建的 —— 这是一种基于“注意力”算法的深度学习架构。自 2018 年 Google 推出 BERT 以来，这种架构引起了广泛关注。

原始的 Transformer 架构如下所示，左侧是编码器（encoder），右侧是解码器（decoder）。

<figure><img src="../.gitbook/assets/transformer.jpg" alt=""><figcaption></figcaption></figure>

Transformer 有三种类型：

1. **编码器（Encoders）** 基于编码器的 Transformer 接收文本（或其他数据）作为输入，并输出该文本的密集表示（或嵌入）。
   * **示例**：Google 的 BERT
   * **用例**：文本分类、语义搜索、命名实体识别
   * **典型规模**：数百万个参数
2. **解码器（Decoders）** 基于解码器的 Transformer 专注于**逐个生成 token 以完成序列**。
   * **示例**：Meta 的 Llama
   * **用例**：文本生成、聊天机器人、代码生成
   * **典型规模**：数十亿（按美国用法，即 10^9）个参数
3. **序列到序列（编码器-解码器，Seq2Seq（Encoder–Decoder））** 序列到序列的 Transformer _结&#x5408;_&#x4E86;编码器和解码器。编码器首先将输入序列处理成上下文表示，然后解码器生成输出序列。
   * **示例**：T5、BART
   * **用例**：翻译、摘要、改写
   * **典型规模**：数百万个参数

大语言模型 (LLM) 的基本原理简单却极其有效：**其目标是在给定一系列前一个 token 的情况下，预测下一个 token**。

#### 1.2.2 Transformer 的token预测过程

理解下一个词元预测

大语言模型 (LLM) 被认为是**自回归**的，这意味着**一次通过的输出成为下一次的输入**。这个循环持续进行，直到模型预测下一个词元为 EOS（结束符）词元，此时模型可以停止。

<figure><img src="https://huggingface.co/datasets/agents-course/course-images/resolve/main/en/unit1/AutoregressionSchema.gif" alt=""><figcaption></figcaption></figure>

虽然对于学习智能体而言，整个过程可能相当技术化，但以下是简要概述：

* 一旦输入文本被**词元化**，模型就会计算序列的表示，该表示捕获输入序列中每个词元的意义和位置信息。
* 这个表示被输入到模型中，模型输出分数，这些分数对词汇表中每个词元作为序列中下一个词元的可能性进行排名。

<figure><img src="https://huggingface.co/datasets/agents-course/course-images/resolve/main/en/unit1/DecodingFinal.gif" alt=""><figcaption></figcaption></figure>

Transformer 架构的一个关键方面是**注意力机制**。在预测下一个词时，句子中的每个词并不是同等重要的；例如，在句子 _“The capital of France is …”_ 中，“France” 和 “capital” 这样的词携带了最多的意义。

<figure><img src="https://huggingface.co/datasets/agents-course/course-images/resolve/main/en/unit1/AttentionSceneFinal.gif" alt=""><figcaption></figcaption></figure>

#### 1.2.3 LLM 为什么会“思考”

**LLM 的推理 = 模式匹配 × 注意力机制 × 大规模参数的涌现能力**

它并不真的思考，但它能：

1. **全局读取上下文（Attention）**
2. **构建内在隐含结构（抽象向量空间）**
3. **按推理模式生成最可能的下一步（统计学习）**
4. **规模足够大时会涌现出接近逻辑思考的能力**

你看到的“推理”其实是：

> **从庞大语言共性中提取规则，再通过 Attention 实时匹配并模拟推理结构。**

#### 1.2.4 提示词对大语言模型很重要

考虑到大语言模型（LLM）的唯一工作是通过查看每个输入词元来预测下一个词元，并选择哪些词元是“重要的”，因此你提供的输入序列的措辞非常重要。

你提供给大语言模型的输入序列被称&#x4E3A;_&#x70;rompt_。精心设计提示可以更容易地**引导大语言模型的生成朝着期望的输出方向进行**。

### 1.3 智能体的构成与运行原理

#### 1.3.1 任务环境定义

PEAS 模型是人工智能领域里一个非常常见的分析框架，用来描述和设计智能体（Agent）的工作环境与目标。它的名字来自四个关键要素：**Performance measure（性能度量）、Environment（环境）、Actuators（执行器）、Sensors（传感器）**。

四个组成部分

* **Performance measure（性能度量）** 衡量智能体是否“成功”的标准。比如自动驾驶汽车的性能度量可以是：安全性、到达目的地的速度、乘客舒适度、燃油效率等。
* **Environment（环境）** 智能体所处的外部世界。它包含智能体需要感知和影响的所有事物。比如自动驾驶汽车的环境包括：道路、交通规则、其他车辆、行人、天气状况等。
* **Actuators（执行器）** 智能体用来作用于环境的工具或部件。比如自动驾驶汽车的执行器包括：方向盘、油门、刹车、车灯、喇叭等。
* **Sensors（传感器）** 智能体用来感知环境的工具。比如自动驾驶汽车的传感器包括：摄像头、雷达、激光雷达（LiDAR）、GPS、速度计等。

<figure><img src="https://raw.githubusercontent.com/datawhalechina/Hello-Agents/main/docs/images/1-figures/1757242319667-6.png" alt=""><figcaption></figcaption></figure>

通过定义这些要素，开发人员可以更清晰地构想AI代理的目标、交互方式和限制。

#### 1.3.2 智能体的运行机制

在定义了智能体所处的任务环境后，我们来探讨其核心的运行机制。智能体并非一次性完成任务，而是通过一个持续的循环与环境进行交互，这个核心机制被称为 **智能体循环 (Agent Loop)**。如图 所示，该循环描述了智能体与环境之间的动态交互过程，构成了其自主行为的基础。

<figure><img src="https://raw.githubusercontent.com/datawhalechina/Hello-Agents/main/docs/images/1-figures/1757242319667-5.png" alt=""><figcaption></figcaption></figure>

这个循环主要包含以下几个相互关联的阶段：

1. **感知 (Perception)**：这是循环的起点。智能体通过其传感器（例如，API 的监听端口、用户输入接口）接收来自环境的输入信息。这些信息，即**观察 (Observation)**，既可以是用户的初始指令，也可以是上一步行动所导致的环境状态变化反馈。
2.  思考 (Thought)

    ：接收到观察信息后，智能体进入其核心决策阶段。对于 LLM 智能体而言，这通常是由大语言模型驱动的内部推理过程。如图所示，“思考”阶段可进一步细分为两个关键环节：

    * **规划 (Planning)**：智能体基于当前的观察和其内部记忆，更新对任务和环境的理解，并制定或调整一个行动计划。这可能涉及将复杂目标分解为一系列更具体的子任务。
    * **工具选择 (Tool Selection)**：根据当前计划，智能体从其可用的工具库中，选择最适合执行下一步骤的工具，并确定调用该工具所需的具体参数。
3. **行动 (Action)**：决策完成后，智能体通过其执行器（Actuators）执行具体的行动。这通常表现为调用一个选定的工具（如代码解释器、搜索引擎 API），从而对环境施加影响，意图改变环境的状态。

行动并非循环的终点。智能体的行动会引起**环境 (Environment)** 的**状态变化 (State Change)**，环境随即会产生一个新的**观察 (Observation)** 作为结果反馈。这个新的观察又会在下一轮循环中被智能体的感知系统捕获，形成一个持续的“感知-思考-行动-观察”的闭环。智能体正是通过不断重复这一循环，逐步推进任务，从初始状态向目标状态演进。

#### 1.3.3 智能体的感知与行动

在工程实践中，为了让 LLM 能够有效驱动这个循环，我们需要一套明确的**交互协议 (Interaction Protocol)** 来规范其与环境之间的信息交换。

在许多现代智能体框架中，这一协议体现在对智能体每一次输出的结构化定义上。智能体的输出不再是单一的自然语言回复，而是一段遵循特定格式的文本，其中明确地展示了其内部的推理过程与最终决策。

这个结构通常包含两个核心部分：

* **Thought (思考)**：这是智能体内部决策的“快照”。它以自然语言形式阐述了智能体如何分析当前情境、回顾上一步的观察结果、进行自我反思与问题分解，并最终规划出下一步的具体行动。
* **Action (行动)**：这是智能体基于思考后，决定对环境施加的具体操作，通常以函数调用的形式表示。

例如，一个正在规划旅行的智能体可能会生成如下格式化的输出：

```
Thought: 用户想知道北京的天气。我需要调用天气查询工具。
Action: get_weather("北京")Copy to clipboardErrorCopied
```

这里的`Action`字段构成了对外部世界的指令。一个外部的**解析器 (Parser)** 会捕捉到这个指令，并调用相应的`get_weather`函数。

行动执行后，环境会返回一个结果。例如，`get_weather`函数可能返回一个包含详细天气数据的 JSON 对象。然而，原始的机器可读数据（如 JSON）通常包含 LLM 无需关注的冗余信息，且格式不符合其自然语言处理的习惯。

因此，感知系统的一个重要职责就是扮演传感器的角色：将这个原始输出处理并封装成一段简洁、清晰的自然语言文本，即观察。

```
Observation: 北京当前天气为晴，气温25摄氏度，微风。Copy to clipboardErrorCopied
```

这段`Observation`文本会被反馈给智能体，作为下一轮循环的主要输入信息，供其进行新一轮的`Thought`和`Action`。

综上所述，通过这个由 Thought、Action、Observation 构成的严谨循环，LLM 智能体得以将内部的语言推理能力，与外部环境的真实信息和工具操作能力有效地结合起来。

### 1.4 动手体验：5 分钟实现第一个智能体

在前面的小节，我们学习了智能体的任务环境、核心运行机制以及 `Thought-Action-Observation` 交互范式。在本节中，我们将引导您使用几行简单的 Python 代码，从零开始构建一个可以工作的智能旅行助手。这个过程将遵循我们刚刚学到的理论循环，让您直观地感受到一个智能体是如何“思考”并与外部“工具”互动的。

在本案例中，我们的目标是构建一个能处理分步任务的智能旅行助手。需要解决的用户任务定义为："你好，请帮我查询一下今天北京的天气，然后根据天气推荐一个合适的旅游景点。"要完成这个任务，智能体必须展现出清晰的逻辑规划能力。它需要先调用天气查询工具，并将获得的观察结果作为下一步的依据。在下一轮循环中，它再调用景点推荐工具，从而得出最终建议。

#### 1.4.1 准备工作

（1）指令模板

```
AGENT_SYSTEM_PROMPT = """
你是一个智能旅行助手。你的任务是分析用户的请求，并使用可用工具一步步地解决问题。
​
# 可用工具:
- `get_weather(city: str)`: 查询指定城市的实时天气。
- `get_attraction(city: str, weather: str)`: 根据城市和天气搜索推荐的旅游景点。
​
# 行动格式:
你的回答必须严格遵循以下格式。首先是你的思考过程，然后是你要执行的具体行动，每次回复只输出一对Thought-Action：
Thought: [这里是你的思考过程和下一步计划]
Action: [这里是你要调用的工具，格式为 function_name(arg_name="arg_value")]
​
# 任务完成:
当你收集到足够的信息，能够回答用户的最终问题时，你必须在`Action:`字段后使用 `finish(answer="...")` 来输出最终答案。
​
请开始吧！
"""
```

工具 1：查询真实天气 使用免费的天气查询服务 `wttr.in`

工具 2：搜索并推荐旅游景点 search\_attraction 使用 tavily-python,可以去[tavily](https://www.tavily.com/)注册每月有免费额度

#### 1.4.2 接入大模型

通过 `OpenAI`库使用，我们可以通过 [ModelScope](https://modelscope.cn/docs/model-service/API-Inference/intro) 获取`Qwen`系列的免费（`OpenAI`）兼容格式的API。

#### 1.4.3 执行行动循环

下面的主循环将整合所有组件，并通过格式化后的 Prompt 驱动 LLM 进行决策。

```
import re
# --- 1. 配置LLM客户端 ---
# 请根据您使用的服务，将这里替换成对应的凭证和地址
API_KEY = "YOUR_API_KEY"
BASE_URL = "YOUR_BASE_URL"
MODEL_ID = "YOUR_MODEL_ID"
TAVILY_API_KEY="YOUR_Tavily_KEY"
os.environ['TAVILY_API_KEY'] = "YOUR_TAVILY_API_KEY"
​
llm = OpenAICompatibleClient(
    model=MODEL_ID,
    api_key=API_KEY,
    base_url=BASE_URL
)
​
# --- 2. 初始化 ---
user_prompt = "你好，请帮我查询一下今天北京的天气，然后根据天气推荐一个合适的旅游景点。"
prompt_history = [f"用户请求: {user_prompt}"]
​
print(f"用户输入: {user_prompt}\n" + "="*40)
​
# --- 3. 运行主循环 ---
for i in range(5): # 设置最大循环次数
    print(f"--- 循环 {i+1} ---\n")
    
    # 3.1. 构建Prompt
    full_prompt = "\n".join(prompt_history)
    
    # 3.2. 调用LLM进行思考 
    llm_output = llm.generate(full_prompt, system_prompt=AGENT_SYSTEM_PROMPT)
    # 模型可能会输出多余的Thought-Action，需要截断
    match = re.search(r'(Thought:.*?Action:.*?)(?=\n\s*(?:Thought:|Action:|Observation:)|\Z)', llm_output, re.DOTALL)
    if match:
        truncated = match.group(1).strip()
        if truncated != llm_output.strip():
            llm_output = truncated
            print("已截断多余的 Thought-Action 对")
    print(f"模型输出:\n{llm_output}\n")
    prompt_history.append(llm_output)
    
    # 3.3. 解析并执行行动
    action_match = re.search(r"Action: (.*)", llm_output, re.DOTALL)
    if not action_match:
        print("解析错误:模型输出中未找到 Action。")
        break
    action_str = action_match.group(1).strip()
    
    if action_str.startswith("finish"):
        final_answer = re.search(r'finish\(answer="(.*)"\)', action_str).group(1)
        print(f"任务完成，最终答案: {final_answer}")
        break
    
    tool_name = re.search(r"(\w+)\(", action_str).group(1)
    args_str = re.search(r"\((.*)\)", action_str).group(1)
    kwargs = dict(re.findall(r'(\w+)="([^"]*)"', args_str))
​
    if tool_name in available_tools:
        observation = available_tools[tool_name](**kwargs)
    else:
        observation = f"错误:未定义的工具 '{tool_name}'"
​
    # 3.4. 记录观察结果
    observation_str = f"Observation: {observation}"
    print(f"{observation_str}\n" + "="*40)
    prompt_history.append(observation_str)
​
```

通过以上步骤，我们构建了一个完整的、由真实 LLM 驱动的智能体。其核心在于“工具”和“提示工程”的结合，这正是当前主流智能体框架（如 LangChain、LlamaIndex 等）的设计精髓。

#### 1.3.4 运行案例分析

```
用户输入: 你好，请帮我查询一下今天北京的天气，然后根据天气推荐一个合适的旅游景点。
========================================
--- 循环 1 ---
​
正在调用大语言模型...
大语言模型响应成功。
模型输出:
Thought: 首先需要获取北京今天的天气情况，之后再根据天气情况来推荐旅游景点。
Action: get_weather(city="北京")
​
Observation: 北京当前天气:Sunny，气温26摄氏度
========================================      
--- 循环 2 ---
​
正在调用大语言模型...
大语言模型响应成功。
模型输出:
Thought: 现在已经知道了北京今天的天气是晴朗且温度适中，接下来可以基于这个信息来推荐一个适合的旅游景点了。
Action: get_attraction(city="北京", weather="Sunny")
​
Observation: 北京在晴天最值得去的旅游景点是颐和园，因其美丽的湖景和古建筑。另一个推荐是长城，因其壮观的景观和历史意义。
========================================
--- 循环 3 ---
​
正在调用大语言模型...
大语言模型响应成功。
模型输出:
Thought: 已经获得了两个适合晴天游览的景点建议，现在可以根据这些信息给用户提供满意的答复。
Action: finish(answer="今天北京的天气是晴朗的，气温26摄氏度，非常适合外出游玩。我推荐您去颐和园欣赏美丽的湖景和古建筑，或者前往长城体验其壮观的景观和深厚的历史意义。希望您有一个愉快的旅行！
")
​
任务完成，最终答案: 今天北京的天气是晴朗的，气温26摄氏度，非常适合外出游玩。我推荐您去颐和园欣赏美丽的湖景和古建筑，或者前往长城体验其壮观的景观和深厚的历史意义。希望您有一个愉快的旅行！
​
```

上面的代码来源于 hello-agents开源文档, [源码查看](https://github.com/datawhalechina/hello-agents/blob/main/code/chapter1/FirstAgentTest.py)

### 1.5智能体框架

#### 1.5.1常见智能体框架

智能体不再是被动的工具，而是主动的目标追求者，现这种自主协作的思路百花齐放，涌现了大量优秀的框架和产品，从早期的 BabyAGI、AutoGPT，到如今更为成熟的 CrewAI、AutoGen、MetaGPT、LangGraph 等优秀框架，共同推动着这一领域的高速发展。虽然具体实现千差万别，但它们的架构范式大致可以归纳为几个主流方向：

1. **单智能体自主循环**：这是早期的典型范式，如 **AgentGPT** 所代表的模式。其核心是一个通用智能体通过“思考-规划-执行-反思”的闭环，不断进行自我提示和迭代，以完成一个开放式的高层级目标。
2. **多智能体协作**：这是当前最主流的探索方向，旨在通过模拟人类团队的协作模式来解决复杂问题。它又可细分为不同模式： **角色扮演式对话**：如 **CAMEL** 框架，通过为两个智能体（例如，“程序员”和“产品经理”）设定明确的角色和沟通协议，让它们在一个结构化的对话中协同完成任务。 **组织化工作流**：如 **MetaGPT** 和 **CrewAI**，它们模拟一个分工明确的“虚拟团队”（如软件公司或咨询小组）。每个智能体都有预设的职责和工作流程（SOP），通过层级化或顺序化的方式协作，产出高质量的复杂成果（如完整的代码库或研究报告）。**AutoGen** 和 **AgentScope** 则提供了更灵活的对话模式，允许开发者自定义智能体间的复杂交互网络。
3. **高级控制流架构**：诸如 **LangGraph** 等框架，则更侧重于为智能体提供更强大的底层工程基础。它将智能体的执行过程建模为状态图（State Graph），从而能更灵活、更可靠地实现循环、分支、回溯以及人工介入等复杂流程。

这些不同的架构范式，共同推动着自主智能体从理论构想走向更广泛的实际应用，使其有能力应对日益复杂的真实世界任务。在我们的后续章节中，也会感受不同类型框架之间的差异和优势。

#### 1.5.2 Workflow 和 Agent 的差异

现在我们公司目前用到最多的还是 Workflow。

我们有必要对 Workflow 和 Agent 的差异展开讨论，尽管它们都旨在实现任务自动化，但其底层逻辑、核心特征和适用场景却截然不同。

简单来说，**Workflow 是让 AI 按部就班地执行指令，而 Agent 则是赋予 AI 自由度去自主达成目标。**

<figure><img src="https://raw.githubusercontent.com/datawhalechina/Hello-Agents/main/docs/images/1-figures/1757242319667-18.png" alt=""><figcaption></figcaption></figure>

如图 所示，工作流是一种传统的自动化范式，其核心是**对一系列任务或步骤进行预先定义的、结构化的编排**。它本质上是一个精确的、静态的流程图，规定了在何种条件下、以何种顺序执行哪些操作。一个典型的案例：某企业的费用报销审批流程。员工提交报销单（触发）-> 如果金额小于 500 元，直接由部门经理审批 -> 如果金额大于 500 元，先由部门经理审批，再流转至财务总监审批 -> 审批通过后，通知财务部打款。整个过程的每一步、每一个判断条件都被精确地预先设定。

与工作流不同，基于大型语言模型的智能体是一个**具备自主性的、以目标为导向的系统**。它不仅仅是执行预设指令，而是能够在一定程度上理解环境、进行推理、制定计划，并动态地采取行动以达成最终目标。LLM 在其中扮演着“大脑”的角色。一个典型的例子，便是我们在 1.3 节中写的智能旅行助手。当我们向它下达一个新指令，例如：**“你好，请帮我查询一下今天北京的天气，然后根据天气推荐一个合适的旅游景点。”** 它的处理过程充分展现了其自主性：

1. **规划与工具调用：** Agent 首先会把任务拆解为两个步骤：① 查询天气；② 基于天气推荐景点。随即，它会自主选择并调用“天气查询 API”，并将“北京”作为参数传入。
2. **推理与决策：** 假设 API 返回结果为“晴朗，微风”。Agent 的 LLM 大脑会基于这个信息进行推理：“晴天适合户外活动”。接着，它会根据这个判断，在它的知识库或通过搜索引擎这个工具中，筛选出北京的户外景点，如故宫、颐和园、天坛公园等。
3. **生成结果：** 最后，Agent 会综合信息，给出一个完整的、人性化的回答：“今天北京天气晴朗，微风，非常适合户外游玩。为您推荐前往【颐和园】，您可以在昆明湖上泛舟，欣赏美丽的皇家园林景色。”

在这个过程中，没有任何写死的`if天气=晴天 then 推荐颐和园`的规则。如果天气是“雨天”，Agent 会自主推理并推荐国家博物馆、首都博物馆等室内场所。**这种基于实时信息进行动态推理和决策的能力，正是 Agent 的核心价值所在。**

### 总结

1. 智能体是通过传感器感知环境，自主通过执行器采取行动以达成目标的实体，具有自主性等核心特征。
2. LLM是擅长理解和生成人类语言的AI模型，基于Transformer架构，通过大量文本训练学习语言模式。
3. 智能体的核心运行机制包括智能体循环和交互协议，通过感知、思考、行动和观察不断与环境交互。
4. 常见智能体框架有单智能体自主循环、多智能体协作和高级控制流架构等类型。

### 参考文献

1.[https://datawhalechina.github.io/hello-agents/#/./chapter1/%E7%AC%AC%E4%B8%80%E7%AB%A0%20%E5%88%9D%E8%AF%86%E6%99%BA%E8%83%BD%E4%BD%93](https://datawhalechina.github.io/hello-agents/#/./chapter1/%E7%AC%AC%E4%B8%80%E7%AB%A0%20%E5%88%9D%E8%AF%86%E6%99%BA%E8%83%BD%E4%BD%93)

2.[https://huggingface.co/learn/agents-course/zh-CN/unit1/what-are-agents](https://huggingface.co/learn/agents-course/zh-CN/unit1/what-are-agents)

<br>
