# AboutSecurity

渗透测试知识库，以 AI Agent 可执行的格式沉淀安全方法论。

## 核心模块

**Skills/** — 125+ 个技能方法论，覆盖侦察到后渗透全链路

- `cloud/` — 云环境（Docker逃逸、K8s攻击链、AWS IAM、阿里云、腾讯云、Serverless）
- `ctf/` — CTF竞赛（Web解题、逆向、PWN、密码学、取证、AI/ML）
- `dfir/` — 取证对抗（内存取证与反取证、磁盘取证与反取证、日志逃逸）🆕
- `evasion/` — 免杀对抗（C2框架、Shellcode生成、安全研究）
- `exploit/` — 漏洞利用（73 skills，按子分类组织）
  - `web-method/` — Web 通用方法论（注入、XSS、SSRF、SSTI、文件上传、反序列化、WAF绕过…）
  - `product-vuln/` — 特定产品漏洞（Nacos、Jenkins、Grafana、GitLab、中间件…）
  - `advanced/` — 高级利用（HTTP走私、竞态条件、供应链攻击、OT/ICS、加密攻击）
  - `auth/` — 认证授权（JWT、OAuth/SSO、IDOR、CORS、CSRF、Cookie分析）
- `general/` — 综合（报告生成、供应链审计、移动后端API）
- `lateral/` — 横向移动（AD域攻击、NTLM中继、数据库横向、Kerberoasting、ACL滥用）
- `malware/` — 恶意软件（样本分析方法论、C2 Beacon配置提取、沙箱逃逸实现）🆕
- `postexploit/` — 后渗透（Linux/Windows提权、持久化、凭据窃取）
- `recon/` — 侦察（子域名枚举、被动信息收集、JS API提取）
- `threat-intel/` — 威胁情报（IOC对抗、APT模拟、威胁猎杀规避）🆕
- `tool/` — 工具使用（fscan、nuclei、sqlmap、msfconsole、ffuf、hashcat）

**Dict/** — 字典库

- `Auth/` — 用户名/密码
- `Network/` — IP段排除、DNS服务器
- `Port/` — 按端口分类的爆破字典
- `Web/` — Web目录、API参数、fuzz字典

**Payload/** — 攻击载荷

- `SQL-Inj/`、`XSS/`、`SSRF/`、`XXE/`、`LFI/`、`RCE/`、`upload/`、`CORS/`、`HPP/`、`Format/`、`SSI/`、`email/`

**Tools/** — 外部工具声明式配置

- `scan/`、`fuzz/`、`osint/`、`poc/`、`brute/`、`postexploit/`

## 分类架构说明

### 三级路径 vs 二级路径

本仓库的 skill 存储采用**三级路径**（按维护者视角分类）：

```
skills/<category>/<skill-name>/SKILL.md    # 维护者视角：按攻击阶段分类
```

而 AI Agent 实际消费时使用**二级路径**（扁平结构）：

```
.claude/skills/<skill-name>/SKILL.md       # Agent 视角：所有 skill 平铺
```

通过 `sync-skills.sh` 脚本将三级路径软链接/复制为二级路径。这意味着：
- **维护者**按分类组织，便于管理和查找
- **Agent** 使用时所有 skill 在同一层级，不存在"跨分类跳转"问题
- 脚本支持多源合并（如私有仓库 + 本仓库），先到先得

### 为什么 `tool/` 是独立分类

工具类 skill（如 nuclei、sqlmap）独立于方法论 skill，原因：

1. **多用途工具避免重复**：nuclei 可用于指纹扫描、漏洞扫描、DAST、本地文件扫描，若在每个引用它的 skill 中重复写使用方法，维护成本极高
2. **模型不了解新工具**：AI 模型训练数据有截止日期，对新版本工具的参数和用法不了解，需要专门的 skill 文档补充
3. **运行时无影响**：sync-skills.sh 将 tool/ 下的 skill 和其他分类一起扁平化，Agent 在使用时按 description 匹配触发，不感知分类层级

### sync-skills.sh 脚本

```bash
# 软链接模式（本地开发）
./sync-skills.sh

# 复制模式（远程部署）
./sync-skills.sh --copy

# 指定额外 skill 源（私有仓库）
./sync-skills.sh --extra-source /path/to/private-skills
```

脚本逻辑：
1. `find` 所有包含 `SKILL.md` 的目录
2. 按目录名（skill-name）去重，先到先得（主源优先）
3. 排除配置的分类（如 `ai-security|evasion`）
4. 创建软链接或复制到 `.claude/skills/<skill-name>/`

## Skill 格式

```
sql-injection-methodology/
├── SKILL.md           # 决策树（触发条件 → 执行流程）
├── references/        # 详细内容（payload + 脚本）
└── evals/             # A/B 测试评估
```

SKILL.md 定义 AI Agent 的行为约束（NEVER/ALWAYS），references/ 目录按需加载详细内容。

## Skill Benchmark

`python scripts/bench-skill.py --all` 量化 Skill 对 Agent 效果的提升，结果记录在 `benchmarks/` 目录。

## 快速开始

```bash
# 列出所有 Skill
ls Skills/

# 查看特定 Skill
cat Skills/exploit/sql-injection-methodology/SKILL.md

# 运行 Benchmark (需要本地配置好 claude code 使用)
python scripts/bench-skill.py --skill sql-injection-methodology
```

## 贡献

提交前阅读 [CONTRIBUTING.md](./CONTRIBUTING.md)，包括 Skill 格式规范、references 编写要求、benchmark 测试流程。

## 参考

- https://github.com/anthropics/skills/blob/main/skills/skill-creator/SKILL.md
- https://github.com/ljagiello/ctf-skills
- https://github.com/JDArmy/Evasion-SubAgents
- https://github.com/teamssix/twiki
- https://github.com/yaklang/hack-skills
- https://github.com/mukul975/Anthropic-Cybersecurity-Skills
