---
description: 罗轩
icon: traffic-light-stop
---

# OpenSpec：让 AI 照着「需求账本」写代码

OpenSpec 是一个专为 AI 编码助手设计的轻量级规范驱动开发（Spec-Driven Development）框架，核心主张是：**在让 AI 动手之前，先把需求写成结构化的规范文档，人和 AI 对齐之后再干活。**&#x5982;果你也有过这样的经历：和 AI 聊了两百条消息做了一个功能，三天后想让 AI 改个细节，它却完全不记得当初的设计约定，甚至自作主张把之前的逻辑改坏了——那这篇文章就是写给你的。下面按 WHAT（是什么）、WHY（为什么要用）、HOW（怎么用）三段展开。WHY 部分会重点对比 OpenSpec 和 Superpowers 的区别与结合用法——这两个框架经常被混为一谈，其实是互补关系。

***

### 一、WHAT：OpenSpec 是什么

OpenSpec 本质上是**一层存在于代码仓库里的「需求事实来源」**：用 Markdown 记录、随 Git 版本化、供任意 AI 编码工具消费。放到日常开发里理解：以前和 AI 结对编程，需求全散落在聊天记录里，换会话就丢、迭代多了就乱。OpenSpec 相当于给项目加了一本需求账本——每个功能先立一份「变更提案」，写清楚改什么、为什么改、分几步做；AI 照着账本干活，干完归档；账本永远反映系统的真实需求。

#### 1.1 核心目录结构

```undefined
openspec/
├── specs/                            # 主规范：当前系统需求的唯一事实来源
│   └── <能力域>/spec.md              #   按能力领域拆分（如 listing、queue-task）
└── changes/                          # 变更目录：一次功能变更一份独立提案
    └── add-configurable-sku-scene-images/
        ├── proposal.md               #   为什么要做这个变更
        ├── specs/                    #   对主规范的增量（Delta）
        ├── design.md                 #   技术方案（可选）
        └── tasks.md                  #   拆解后的实现任务清单
```

两个关键设计值得注意：

| 设计         | 说明                                                            |
| ---------- | ------------------------------------------------------------- |
| 主规范与变更分离   | `specs/` 是「系统现在是什么样」，`changes/` 是「系统即将变成什么样」。变更之间互不干扰，可以并行推进。 |
| Delta 增量机制 | 变更不直接改主规范，而是写成「增/改/删了哪些需求条目」的增量，归档时才合并进主规范，天然形成审计轨迹。          |

#### 1.2 工作流五阶段

OpenSpec 把一次功能变更的生命周期定义为五步：

1. **explore** — 梳理问题和现有代码，不急着出方案
2. **propose** — 起草 proposal.md、spec deltas、tasks.md，人在这一步审核把关
3. **apply** — AI 按 tasks.md 逐项实现
4. **verify** — 校验实现与规范是否一致
5. **archive** — 归档变更，delta 增量并入主规范

<figure><img src="https://euj0e90can.feishu.cn/space/api/box/stream/download/asynccode/?code=NWRhMjdhODU5YzY3MDQ4NDBjZTFmZDI1ZTI0MmE2ZmRfUDF2TTdtZWkyY1VhSzZkNmJOQnN1SXY0VWhVRzRYTjNfVG9rZW46THZFdGJqYlhqbzhHVjd4TWp2YWNGS2FibkpkXzE3OTAyNTI0NDY6MTc5MDI1NjA0Nl9WNA&#x26;add_watermark=true&#x26;scene_type=CCM" alt=""><figcaption></figcaption></figure>

#### 1.3 项目概况

* 开源项目，MIT 协议，GitHub：https://github.com/Fission-AI/OpenSpec（68k+ stars），官网：https://openspec.dev
* 轻量、可配置：支持自定义 Schema、模板和项目配置，多语言。存量项目可以渐进接入，不用一次性补齐所有文档，用到哪补到哪

***

### 二、WHY：为什么要用 OpenSpec

#### 2.1 纯聊天驱动 AI 编程的四大痛点

| 痛点    | 具体表现                                |
| ----- | ----------------------------------- |
| 需求丢失  | 关键约定埋在第 137 条消息里，新会话、新同事、新工具统统不知道   |
| 迭代困难  | 需求一变，AI 只能基于「记忆」打补丁，越补越歪            |
| 无审计轨迹 | 为什么三个月前这么设计？没人说得清，git log 里只有代码没有需求 |
| 团队协作难 | 你和 AI 达成的共识，对队友是黑盒；换个人接管，一切推倒重来     |

这些问题的共同根源只有一个：对话是易失性的，而需求需要持久性。OpenSpec 的解法就是把需求从聊天记录里抽出来，变成版本化的工程资产。

#### 2.2 OpenSpec vs Superpowers：一对好搭档，不是竞争者

聊规范驱动开发，绕不开另一个当红框架 Superpowers（obra/superpowers，Claude Code 生态最流行的 Skills 集合之一）。很多人问：这俩是不是一回事？不是。**它们一个管「做什么」，一个管「怎么做」，层次完全不同。**

| 维度    | OpenSpec                               | Superpowers                                                       |
| ----- | -------------------------------------- | ----------------------------------------------------------------- |
| 本质    | 规范资产层：一组存在于仓库里的 Markdown 需求文档 + CLI 工具 | 流程纪律层：一套可组合的开发流程 Skills（brainstorming、TDD、writing-plans 等 20+ 模块） |
| 回答的问题 | What & Why——系统该是什么样、为什么                | How——按什么工序把活干漂亮                                                   |
| 持久性   | spec 随 Git 版本化，跨会话、跨团队、跨工具长期有效         | 纪律在当次开发过程中生效，设计文档是过程产物，没有系统级的沉淀                                   |
| 核心机制  | Delta 增量、变更提案、归档合并、审计轨迹                | 脑暴收敛 → 计划拆解 → 子代理执行 → TDD 红绿重构 → 两阶段代码审查                          |
| 协作面   | 人和人对齐（spec 是团队共同语言）                    | 人和 AI 对齐（管住 AI 不乱来）                                               |
| 强项    | 需求不漂移、可回溯、可交接                          | 代码质量高、过程严谨、不写裸奔代码                                                 |

打个比方：OpenSpec 是点菜单，Superpowers 是后厨规矩。菜单上写清楚菜名、口味、忌口，任何一个厨子拿到都能做——需求跟着单子走，不跟着厨子走。后厨规矩决定这道菜做出来是及格还是惊艳：先备菜、控火候、出锅前尝一口。只有菜单没有规矩，菜能吃，但上限看厨子发挥；只有规矩没有菜单，手艺再好也不知道你今晚想吃什么。两者各自的短板恰好是对方的长处：

* OpenSpec 只定义了「提案 → 实现 → 验证 → 归档」的骨架，不约束实现过程中的工程纪律——没有 TDD、没有强制脑暴、没有代码审查关卡
* Superpowers 的 brainstorming 和 writing-plans 产出设计文档与任务清单，但这些产物散落在会话或工作区里，没有沉淀和增量合并机制——项目做久了，「系统当前完整需求」依然无处可查

#### 2.3 结合用法：Superpowers 的工序 × OpenSpec 的账本

把两者的流水线对齐之后，结合方式非常自然：Superpowers 的每个阶段产物，都落到 OpenSpec 对应的文件里。

| Superpowers 技能                       | 承接的 OpenSpec 环节      | 产出落到哪里                                    |
| ------------------------------------ | -------------------- | ----------------------------------------- |
| brainstorming（脑暴收敛）                  | explore → propose 前半 | 沉淀进 `proposal.md` 的动机与方案讨论                |
| writing-plans（计划拆解）                  | propose 后半           | 任务清单写入 `tasks.md`（保留 OpenSpec 的 Delta 格式） |
| executing-plans（子代理逐任务执行）            | apply                | AI 照着 `tasks.md` 干活                       |
| test-driven-development（红绿重构）        | apply 期间             | 测试用例同时是对规范的验收锚点                           |
| requesting-code-review（两阶段审查）        | verify               | 审查基准从「计划」升级为「spec + 计划」                   |
| finishing-a-development-branch（收尾合并） | archive              | 分支合并的同时执行变更归档                             |

串成一条完整的组合流水线：

```undefined
/opsx:explore            （OpenSpec：梳理现状）
  → brainstorming        （Superpowers：脑暴收敛方案）
  → /opsx:propose        （OpenSpec：落成 proposal.md + deltas + tasks.md，人工审核）
  → executing-plans      （Superpowers：逐任务执行）
  → TDD 红绿重构          （Superpowers：贯穿 apply 全程）
  → /opsx:verify         （OpenSpec：实现对照 spec 校验）
  → 代码审查              （Superpowers：spec 合规 + 代码质量两道关卡）
  → /opsx:archive        （OpenSpec：delta 并入主规范，留档）
```

什么时候用哪个，可以记三句话：

> 小修小补直接聊，正经功能先立 spec。 做什么，问 OpenSpec；怎么做，问 Superpowers。 需求一变先改 delta，AI 永远照账本干。

#### 2.4 什么场景值得上 OpenSpec

适合的场景：多模块持续迭代的中大型项目（ERP、SaaS 平台这类，需求条目多、生命周期长）；多人加多 AI 工具协作、需要统一需求语言的团队；想渐进补文档的存量项目——Delta 机制允许用到哪补到哪。不适合的场景：一次性脚本、原型验证、个人小工具。给这些东西立 spec，成本大于收益，纯属于仪式感。

***

### 三、HOW：怎么用

#### 3.1 安装与初始化

```bash
# 安装（npm / pnpm / bun / yarn 均可）
npm install -g @fission-ai/openspec@latest

# 在项目根目录初始化
cd your-project
openspec init
```

初始化时选择你使用的 AI 工具（Claude Code、Codex、Cursor……），OpenSpec 会生成对应的斜杠命令配置。以 `/opsx:` 系列命令为例：

| 命令              | 作用                                          |
| --------------- | ------------------------------------------- |
| `/opsx:explore` | 梳理问题，理解代码库现状                                |
| `/opsx:propose` | 起草 proposal.md、specs/ 增量、design.md、tasks.md |
| `/opsx:apply`   | 按 tasks.md 逐项实现                             |
| `/opsx:verify`  | 校验实现与规范是否一致                                 |
| `/opsx:archive` | 归档完成的变更，增量并入主规范                             |

#### 3.2 走一遍完整流程（真实案例：Odoo 刊登模块加「SKU 场景图」）

下面用一个真实项目举例。ozon\_listing 模块（Odoo 17 的 Ozon 刊登系统）要新增「可配置 SKU 场景图」能力，让运营可以在现有的纯背景主图（clean 模式）和 AI 场景图（scene 模式）之间切换。这个变更涉及生成服务、资源池、异步任务、刊登参数、失败修复和前端界面十几处链路，是个典型的「必须先立 spec 再动手」的需求。**第一步：提出变更**

```undefined
/opsx:propose 支持 SKU 场景图模式：基于 AI 短标题和源 SKU 图生成场景主图，可配置切换
```

AI 探索代码库后，生成变更目录 `openspec/changes/add-configurable-sku-scene-images/`：

```undefined
add-configurable-sku-scene-images/
├── .openspec.yaml                 # 变更元信息（schema: spec-driven）
├── README.md
├── proposal.md                    # 为什么改、改什么、影响面
├── design.md                      # 技术决策与取舍
├── specs/
│   └── configurable-sku-images/
│       └── spec.md                # 对主规范的 Delta 增量
└── tasks.md                       # 实现任务清单
```

**第二步：人工审核提案**这是整个流程中人最重要的把关点。先看 `proposal.md` 的 Why 和 What Changes，真实文件长这样（节选）：

> **Why**：当前 Ozon 刊登资料只生成和使用纯背景、轻微换角度的 `sku_image`，无法按运营需要产出结合 AI 短标题与源 SKU 图的真实商品场景图。同时，图片生成、资源分配、刊登参数、手工重生成、失败自动修复和历史资料补全分别持有自己的处理逻辑，若只局部切换会造成展示图片与实际刊登图片不一致。**What Changes**（摘录几条）：
>
> * 新增系统级 SKU 主图风格参数，在纯背景图模式与场景图模式之间切换，默认保持现有行为
> * 新增独立的 SKU 场景图资源类型，场景图使用源 SKU 图作为视觉依据，并将 AI 短标题用于构建英文生成提示词
> * 统一所有入口的图片模式解析：首次生成、重新生成、失败自动修复、补全生成步骤均遵循所选模式
> * 明确并发一致性：一次已入队的生成任务使用入队时确定的图片模式，不因运行期间修改系统参数而混用两种资源

注意最后一条。「任务运行到一半，系统参数被人改了怎么办」这种边界问题，靠聊天记录是守不住的，只有写进 spec 才会成为 AI 实现时的硬约束。再看 Delta 格式的 spec 增量（`specs/configurable-sku-images/spec.md` 节选）：

```markdown
## ADDED Requirements

### Requirement: 系统参数选择 SKU 图片模式
系统 SHALL 提供一个系统级 SKU 图片模式参数，合法值为纯背景图模式和场景图模式。
参数缺失、为空或取值非法时 MUST 回退到纯背景图模式，以保持现有行为兼容。

#### Scenario: 非法参数安全回退
- **WHEN** 系统参数包含不受支持的值
- **THEN** 系统记录可诊断的告警并按纯背景图模式处理

### Requirement: 两种 SKU 图片资源独立共存
系统 SHALL 保持 `sku_image` 表示现有纯背景 SKU 主图，并以独立资源类型保存 SKU 场景图。
生成或重生成一种模式的图片 MUST NOT 删除、停用或覆盖另一种模式的有效图片。

#### Scenario: 从纯背景模式切换到场景模式
- **WHEN** 资源池已包含纯背景图且系统参数切换为场景图模式
- **THEN** 新场景图存入独立资源集合，原纯背景图继续保留
```

`ADDED / MODIFIED / REMOVED` 描述对主规范的增量改动；每个 Requirement 用 `SHALL / MUST / MUST NOT` 级别的规范语句表述，配 `WHEN / THEN` 场景验收。这份真实 spec 里还写了「并发准备同一 SKU 时，唯一冲突方不得覆盖胜出结果」「模型调用期间不得持有排他锁」这类可测试的工程细节——验收标准写得越像测试用例，AI 实现得越不跑偏。技术方案有分歧时，`design.md` 用 Goals / Non-Goals / Decisions 结构记录取舍。比如这个变更里有一条决策是「保留 `sku_image`、新增 `sku_scene_image`，而不是在原资源 JSON 里加 style 字段」，理由也写得很清楚：混存会使历史数据无法可靠判断风格，重生成时容易误退役另一类图片。三个月后有人问「为什么是两个资源类型」，答案就在这里。**第三步：按任务实现**

```undefined
/opsx:apply add-configurable-sku-scene-images
```

AI 照着 `tasks.md` 逐项打勾实现。真实的任务清单按主题分成 9 组共 70 多条，每组内再编号：

```markdown
## 2. AI 标题与场景图生成
- [ ] 2.1 将场景图步骤依赖明确接到池级 field_translation 步骤，
      验证整个步骤成功前保持等待且不消耗图片重试
- [ ] 2.5 在 SKU 图片异步 worker 中实现 preparation：无锁初检和读缓存、
      无排他锁调用模型、返回后独立短事务锁定并复核四项版本再按唯一键提交
- [ ] 2.8 实现场景图策略，使用源 SKU 图并通过 Flux 2 Klein 4B edits
      路径调用，验证请求包含图片文件、英文 prompt、模型和目标尺寸

## 9. 回归与验收
- [ ] 9.3 在测试环境使用 ALK000166、ALK012065 等 6 个真实 SPU 复测
      Flux 2 Klein 4B edits 接口并验收场景图
```

这份清单有两个细节值得学。一是每条任务都自带验收方式（「验证……」），AI 做完就能自查，不需要人来当验收员；二是验收组里直接写了真实测试数据——具体到 SPU 编号，而不是「找几个商品测一下」的空话。**第四步：验证与归档**

```undefined
/opsx:verify add-configurable-sku-scene-images    # 实现对照 spec 校验
/opsx:archive add-configurable-sku-scene-images   # delta 并入 specs/ 主规范
```

归档后，`configurable-sku-images` 能力正式并入 `openspec/specs/` 主规范。此后任何人（或任何 AI 工具）接手这个模块，读 spec 就能知道系统当前支持两种 SKU 图片模式、并发语义是什么、哪些行为是刻意保持的兼容性回退——不用考古聊天记录和 git log。

***

### 扩展：完整研发流水线架构

> 以下为后续完善的架构目标，当前 OpenSpec 已覆盖核心五阶段（explore → propose → apply → verify → archive），完整流水线将在此基础上扩展需求分级、双模型打磨、测试闭环等能力。

#### 全链路流程

<figure><img src="https://euj0e90can.feishu.cn/space/api/box/stream/download/asynccode/?code=MWJlNjljMzEwN2M0ZDNiMzQyZWU0YmMwMTUzMmMxYzFfZjduOGJQUGhydDhpN3lrMk5aa3k3elR2NjhnZ1o5ZGNfVG9rZW46RURVRmJyZHlpb3loMUF4RTQzaGNzdjhHbmNlXzE3OTAyNTI0NDY6MTc5MDI1NjA0Nl9WNA&#x26;add_watermark=true&#x26;scene_type=CCM" alt=""><figcaption></figcaption></figure>

#### 节点说明

1. **聊通需求（业务对话）**：流程起点，完成业务侧需求的初步沟通对齐
2. **路由分级（规则 + 模型判定）**：对需求进行大小分类，匹配不同处理路径——大需求进入规格打磨环节，小需求可直接跳转至开发环节
3. **spec 双模型打磨（起草 + 审查交替）**：针对大需求完成需求规格说明书的 AI 双模型迭代打磨
4. **人工终审（拍板放行）**：完成需求规格的最终人工审核确认，作为开发的准入依据
5. **开发模型（按 tasks.md 实现）**：依照任务文档执行开发工作
6. **测试 / 修复模型（锚定 spec Scenario）**：对照需求规格的场景要求完成测试、问题修复；测试不通过则打回开发环节修复，设置重试轮次上限
7. **归档（并入主规范）**：开发测试完成后将产出内容归档，纳入整体规范库

### 结语

AI 编码助手解决的是「写得快」，OpenSpec 解决的是「写得对、改得稳、查得回」。它不生产代码，生产的是共识——人与人的共识、人与 AI 的共识、今天与三个月后的共识。Superpowers 管住 AI 的手，OpenSpec 管住 AI 的脑。两者叠加，才是 AI 时代完整的工程化答案。
