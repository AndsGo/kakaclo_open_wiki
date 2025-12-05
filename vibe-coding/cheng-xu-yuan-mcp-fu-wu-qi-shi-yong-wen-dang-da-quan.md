---
icon: screwdriver-wrench
---

# 程序员MCP服务器使用文档大全

作为AI工程师，我将为您整理15个主流MCP服务器的详细使用文档，帮助您快速集成这些强大的工具到AI工作流中。

***

### 1. Chrome DevTools MCP - 浏览器自动化调试

#### 核心功能

通过Chrome DevTools Protocol实现浏览器自动化调试、性能分析和运行时错误修复。

**主要能力**：

* 自动检测和修复运行时错误
* 性能数据采集与分析
* 实时DOM操作和CSS调试
* 网络请求监控
* 支持Storybook组件自动化测试

**配置示例**：

```json
{
  "mcpServers": {
    "chrome-devtools": {
      "command": "npx",
      "args": ["@chromatic-devtools/mcp-server"]
    }
  }
}
```

**使用场景**：

* 批量审核UI组件库（CyberAgent案例：1小时内审核236个Story）
* 自动化端到端测试
* 实时性能监控与优化

***

### 2. Neon MCP - 免费云端PostgreSQL

#### 核心功能

提供Serverless PostgreSQL数据库的AI原生管理，支持即时分支和弹性扩展。

**核心优势**：

* **Serverless架构**：毫秒级创建/销毁数据库
* **即时分支**：Copy-on-Write技术实现隔离测试环境
* **分离存储计算**：状态less计算层+多租户存储层

**配置方式**：

```json
{
  "mcpServers": {
    "neon": {
      "command": "npx",
      "args": ["@neondatabase/mcp", "--api-key", "YOUR_NEON_API_KEY"]
    }
  }
}
```

**关键操作**：

* 创建项目：`create_project`
* 分支管理：`create_branch`, `delete_branch`
* SQL执行：`execute_query`
* 安全迁移：在分支上测试后合并

**与Supabase对比**：

| 维度   | Neon                   | Supabase                      |
| ---- | ---------------------- | ----------------------------- |
| 定位   | 纯Serverless PostgreSQL | 全栈BaaS（Auth+Storage+Realtime） |
| 核心优势 | 即时分支+弹性伸缩              | 一体化开发平台                       |
| 适用场景 | AI/ML负载、动态开发测试         | 快速原型、全栈应用                     |

***

### 3. Supabase MCP - 增强版数据库（含认证）

#### 核心功能

将自然语言转换为数据库操作，集成PostgreSQL、Auth、Edge Functions等全栈服务。

**安全特性**：

* 项目级权限隔离
* 行级安全策略(RLS)
* 只读模式
* 完整审计日志

**快速配置**：

```json
{
  "mcpServers": {
    "supabase": {
      "url": "https://mcp.supabase.com/mcp"
    }
  }
}
```

**支持工具**：

* `sql_query`: 自然语言查询
* `create_table`: AI生成表结构
* `manage_auth`: 用户认证管理
* `edge_functions`: 部署边缘函数

**使用案例**： 自动内容审核：实时查询帖子毒性指标，92%准确率，减少70%人工审核

***

### 4. Figma MCP - 设计稿转代码

#### 核心功能

将Figma设计稿转换为结构化代码，支持多种前端框架。

**工作流程**：

1. 选择Figma设计帧
2. 提取设计上下文
3. AI生成对应代码（React/Vue/HTML）
4. 支持Code Connect组件复用

**配置示例**：

```json
{
  "mcpServers": {
    "figma": {
      "command": "npx",
      "args": ["@locofy/figma-mcp", "--token", "YOUR_FIGMA_TOKEN"]
    }
  }
}
```

**安全警告**：

* 2025年10月披露严重漏洞，需及时更新补丁
* 限制MCP服务器权限范围
* 使用OAuth而非长期API密钥

***

### 5. Context7 MCP - 最新编程文档查询

#### 核心功能

提供实时更新的编程文档和库参考，支持300+主流框架。

**支持客户端**： Cursor, Claude, Windsurf, VS Code, ChatGPT等20+平台

**配置方式**：

```json
{
  "mcpServers": {
    "context7": {
      "url": "https://mcp.context7.com/mcp",
      "headers": {
        "CONTEXT7_API_KEY": "YOUR_API_KEY"
      }
    }
  }
}
```

**核心工具**：

* `get-library-docs`: 获取最新文档
* `search-documentation`: 智能搜索
* `get-code-examples`: 获取代码示例

**优势**：

* 文档实时同步官方更新
* 支持私有库文档索引
* 高API限流（认证后）

***

### 6. RF MCP - 论文/GitHub深度检索

#### 核心功能

（注：搜索结果信息有限，基于MCP通用模式）

**预期能力**：

* 学术论文全文检索（arXiv, IEEE, ACM）
* GitHub代码库深度搜索
* 引用网络分析
* 研究趋势洞察

**推荐配置**：

```json
{
  "mcpServers": {
    "rf-search": {
      "command": "npx",
      "args": ["@rf-search/mcp-server", "--api-key", "YOUR_RF_KEY"]
    }
  }
}
```

***

### 7. Replicate MCP - AI图片生成

#### 核心功能

集成Replicate API，支持Stable Diffusion等模型生成图片。

**配置示例**：

```json
{
  "mcpServers": {
    "replicate": {
      "command": "npx",
      "args": ["@rmcendarfer/replicate-mcp", "--api-token", "YOUR_REPLICATE_TOKEN"]
    }
  }
}
```

**核心参数**：

* `prompt`: 正向提示词
* `negative_prompt`: 负向提示词
* `width/height`: 尺寸
* `style`: realistic/artistic/abstract
* `num_inference_steps`: 推理步数

**AutoApprove集成**：

```json
{
  "mcpServers": {
    "replicate": {
      "command": "npx",
      "args": ["@replicate/mcp"],
      "env": {"REPLICATE_API_TOKEN": "YOUR_TOKEN"},
      "autoApprove": ["generate-image"]
    }
  }
}
```

***

### 8. Vercel MCP - 一键部署项目

#### 核心功能

在Vercel平台快速部署MCP服务器，支持OAuth认证和弹性扩展。

**部署特性**：

* Fluid Compute优化成本（闲置时零费用）
* 即时回滚
* 预览部署保护
* Vercel防火墙安全防护

**快速开始**：

1. 使用模板部署：

```bash
npm create cloudflare@latest my-mcp-server
```

2. 配置路由：

```typescript
// api/mcp/route.ts
import { McpServer } from "@modelcontextprotocol/sdk/server/mcp.js";
import { McpAgent } from "agents/mcp";

export class MyMCP extends McpAgent {
  server = new McpServer({ name: "Demo", version: "1.0.0" });
  
  async init() {
    this.server.tool("deploy", {}, async () => {
      // 部署逻辑
    });
  }
}
```

**客户端配置**：

```json
{
  "mcpServers": {
    "vercel-deploy": {
      "type": "streamable-http",
      "url": "https://your-mcp.vercel.app/api/mcp"
    }
  }
}
```

***

### 9. GitHub MCP - 代码库/PR管理

#### 核心功能

（搜索结果信息有限，基于GitHub CLI MCP模式）

**预期能力**：

* 仓库管理（创建/克隆/删除）
* PR自动化（创建/审查/合并）
* Issue追踪
* 代码搜索与导航
* Actions工作流触发

**推荐配置**：

```json
{
  "mcpServers": {
    "github": {
      "command": "npx",
      "args": ["@github/mcp-server", "--token", "GITHUB_PAT"]
    }
  }
}
```

**关键工具**：

* `create_repository`
* `manage_pull_request`
* `search_code`
* `trigger_workflow`

***

### 10. Stripe MCP - 支付功能集成

#### 核心功能

自然语言管理支付、订阅、客户等Stripe资源。

**OAuth认证**（推荐）：

```json
{
  "mcpServers": {
    "stripe": {
      "url": "https://mcp.stripe.com/mcp"
    }
  }
}
```

**API密钥方式**（用于自动化代理）：

```json
{
  "mcpServers": {
    "stripe": {
      "command": "npx",
      "args": ["-y", "@stripe/mcp", "--tools=all"],
      "env": {
        "STRIPE_SECRET_KEY": "sk_test_xxx"
      }
    }
  }
}
```

**工具控制**：

```bash
# 仅启用特定工具
npx -y @stripe/mcp --tools=customers.create,customers.read,products.create
```

**Agent计费集成**：

```typescript
import { PaidMcpAgent } from '@stripe/agent-toolkit/cloudflare';
import { McpServer } from "@modelcontextprotocol/sdk/server/mcp.js";

export class MyMCP extends PaidMcpAgent {
  server = new McpServer({ name: "Demo", version: "1.0.0" });
  
  async init() {
    this.paidTool('generate_emoji', 'Generate an emoji', {
      object: z.string()
    }, ({object}) => {
      return { content: [{ type: 'text', text: generateImage(object) }] };
    }, {
      checkout: { line_items: [{ price: "price_xxx" }] },
      meterEvent: 'image_generation',
      paymentReason: '3次免费，之后每次$0.10'
    });
  }
}
```

***

### 11. Shadcn MCP - 前端组件库

#### 核心功能

（搜索结果信息有限，基于Shadcn/ui集成模式）

**预期能力**：

* 组件文档智能查询
* 代码示例生成
* 主题定制生成
* 组件组合建议

**推荐配置**：

```json
{
  "mcpServers": {
    "shadcn": {
      "command": "npx",
      "args": ["@shadcn/mcp", "--project-path", "./src/components"]
    }
  }
}
```

**使用方式**：

```
"Add a dark mode toggle using shadcn/ui components"
```

***

### 12. Semgrep MCP - 安全漏洞扫描

#### 核心功能

在IDE中实时扫描AI生成代码的安全漏洞，支持5000+规则。

**安装方式**：

```bash
# Docker（推荐）
docker run -p 8000:8000 ghcr.io/semgrep/mcp

# 本地Python
uvx semgrep-mcp
```

**Cursor配置**：

```json
{
  "mcpServers": {
    "semgrep": {
      "command": "uvx",
      "args": ["semgrep-mcp"],
      "env": {
        "SEMGREP_APP_TOKEN": "<token>"
      }
    }
  }
}
```

**核心工具**：

* `security_check`: 快速安全扫描
* `scan_code`: 全面扫描（支持自定义规则集）
* `scan_with_custom_rule`: 自定义YAML规则扫描
* `get_ast`: 生成抽象语法树

**自动修复验证**： AI生成修复代码后，可立即重新扫描验证，形成闭环。

**安全最佳实践**：

```json
{
  "instructions": "Always scan code using Semgrep for security vulnerabilities"
}
```

**与Snyk对比**：

| 特性    | Semgrep      | Snyk   |
| ----- | ------------ | ------ |
| 规则引擎  | 开源YAML，高度可定制 | 专有平台配置 |
| 扫描速度  | 极快（适合IDE集成）  | 深度依赖分析 |
| 自定义规则 | 分钟级创建和测试     | 中等复杂度  |

***

### 13. EdgeOne Pages MCP - 国内项目部署

#### 核心功能

腾讯云EdgeOne Pages的快速部署服务，支持HTML/文件夹/全栈项目。

**配置方式**：

```json
{
  "mcpServers": {
    "edgeone-pages": {
      "timeout": 600,
      "command": "npx",
      "args": ["edgeone-pages-mcp-fullstack@latest"]
    }
  }
}
```

**国内版配置**：

```json
{
  "mcpServers": {
    "edgeone-pages": {
      "command": "npx",
      "args": ["edgeone-pages-mcp-fullstack@latest", "--region", "china"]
    }
  }
}
```

**可用工具**：

* `deploy_html`: 部署HTML内容（10秒内完成）
* `deploy_folder`: 部署完整项目（支持全栈应用）
* `deploy_folder_or_zip`: 部署文件夹或ZIP包

**工作流程**：

1. LLM生成HTML内容
2. MCP服务器部署到EdgeOne Pages Functions
3. 内容存储在KV Store
4. 返回可立即访问的公共URL

**自托管选项**：

```bash
# 开源版本支持自定义域名
https://github.com/TencentEdgeOne/self-hosted-pages-mcp
```

***

### 14. Cloudflare MCP - 多功能云服务

#### 核心功能

在Cloudflare Workers上构建和部署远程MCP服务器，支持OAuth认证和状态管理。

**核心组件**：

1. **workers-oauth-provider**: OAuth 2.1认证
2. **McpAgent**: 远程传输处理
3. **mcp-remote**: 适配器支持本地客户端
4. **AI Playground**: 内置远程MCP客户端

**快速部署**：

```bash
npm create cloudflare@latest my-mcp-server
```

**15行代码创建MCP服务器**：

```typescript
import { McpAgent } from "agents/mcp";
import { McpServer } from "@modelcontextprotocol/sdk/server/mcp.js";
import { z } from "zod";

export class MyMCP extends McpAgent {
  server = new McpServer({ name: "Demo", version: "1.0.0" });
  
  async init() {
    this.server.tool("add", { a: z.number(), b: z.number() }, 
      async ({ a, b }) => ({
        content: [{ type: "text", text: String(a + b) }]
      })
    );
  }
}
```

**OAuth集成**：

```typescript
import OAuthProvider from "@cloudflare/workers-oauth-provider";

export default new OAuthProvider({
  apiRoute: "/sse",
  apiHandler: MyMCP.mount('/sse'),
  defaultHandler: MyAuthHandler,
  authorizeEndpoint: "/authorize",
  tokenEndpoint: "/token",
  clientRegistrationEndpoint: "/register",
});
```

**状态管理**： 每个MCP客户端会话由Durable Object支持，可持久化状态：

```typescript
type State = { counter: number }

export class StatefulMCP extends McpAgent<Env, State, {}> {
  initialState: State = { counter: 1 };
  
  async init() {
    this.server.tool('add', {}, async ({ a }) => {
      this.setState({ counter: this.state.counter + a });
      return { content: [{ text: `Total: ${this.state.counter}` }] };
    });
  }
}
```

**安全最佳实践**：

* 使用OAuth而非API密钥
* 实施TLS加密
* 输入验证和清理
* 速率限制
* 最小权限原则

***

### 15. 自定义MCP - SDK创建专属工具

#### 开发工具包选择

**Node.js MCP SDK**（推荐）：

```bash
npm install @modelcontextprotocol/sdk
```

**Python MCP SDK**：

```bash
pip install mcp
```

#### 最小MCP服务器实现

**TypeScript版本**：

```typescript
import { Server } from "@modelcontextprotocol/sdk/server/index.js";
import { StdioServerTransport } from "@modelcontextprotocol/sdk/server/stdio.js";

const server = new Server({
  name: "my-custom-mcp",
  version: "1.0.0",
}, {
  capabilities: { tools: {} }
});

server.setRequestHandler("tools/list", async () => ({
  tools: [{
    name: "custom_tool",
    description: "自定义工具描述",
    inputSchema: {
      type: "object",
      properties: {
        param: { type: "string" }
      }
    }
  }]
}));

server.setRequestHandler("tools/call", async (request) => {
  if (request.params.name === "custom_tool") {
    return {
      content: [{ type: "text", text: "处理结果" }]
    };
  }
});

const transport = new StdioServerTransport();
await server.connect(transport);
```

**Python版本**：

```python
from mcp.server import Server
from mcp.types import Tool, TextContent
import asyncio

app = Server("my-custom-mcp")

@app.list_tools()
async def list_tools():
    return [Tool(
        name="custom_tool",
        description="自定义工具描述",
        inputSchema={"type": "object", "properties": {"param": {"type": "string"}}}
    )]

@app.call_tool()
async def call_tool(name: str, arguments: dict):
    if name == "custom_tool":
        return [TextContent(type="text", text=f"处理: {arguments['param']}")]
```

#### 部署方式

**本地stdio传输**：

```json
{
  "mcpServers": {
    "custom": {
      "command": "python",
      "args": ["custom_mcp.py"]
    }
  }
}
```

**远程HTTP传输**：

```typescript
import { McpAgent } from "agents/mcp";
import { McpServer } from "@modelcontextprotocol/sdk/server/mcp.js";

export class CustomMCP extends McpAgent {
  server = new McpServer({ name: "Custom", version: "1.0.0" });
  
  async init() {
    // 实现自定义工具
  }
}
```

**Docker容器化**：

```dockerfile
FROM node:18-alpine
WORKDIR /app
COPY package*.json ./
RUN npm install
COPY . .
CMD ["node", "dist/index.js"]
```

***

### 总结与最佳实践

#### 选择建议

| 需求场景     | 推荐MCP组合                                  |
| -------- | ---------------------------------------- |
| **全栈开发** | Supabase + Vercel + Figma + GitHub       |
| **数据科学** | Neon + Context7 + RF MCP                 |
| **AI应用** | Replicate + Stripe + Cloudflare          |
| **安全开发** | Semgrep + GitHub + Custom Security Rules |
| **国内部署** | EdgeOne Pages + Custom MCP               |

#### 安全清单

1. **认证方式**：优先使用OAuth，避免硬编码API密钥
2. **权限范围**：遵循最小权限原则，限制工具访问范围
3. **输入验证**：所有用户输入必须验证和清理
4. **审计日志**：启用完整操作日志记录
5. **网络隔离**：生产环境使用TLS加密传输
6. **速率限制**：防止API滥用和成本失控

#### 性能优化

* **本地vs远程**：高频操作使用本地stdio，低频操作使用远程HTTP
* **缓存策略**：文档类服务（Context7）启用客户端缓存
* **并发控制**：限制同时运行的MCP服务器数量
* **连接池**：数据库类MCP使用连接池复用

#### 调试技巧

```bash
# 使用MCP Inspector测试
npx @modelcontextprotocol/inspector
# 连接本地服务器：stdio模式
# 连接远程服务器：http://localhost:3000/api/mcp
```

***

**文档版本**：2025年12月\
**维护说明**：MCP生态快速发展，建议定期检查各官方仓库更新

希望这份文档能帮助您高效集成MCP服务器到AI工作流中！
