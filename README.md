# AboutSecurity

安全资源 — 字典、Payload、AI 技能剧本、外部工具配置

与原开源版本 https://github.com/ffffffff0x/AboutSecurity (22年停更) 相比
- 重构了 web 目录扫描字典内容
- 大量字典去重,优化
- 添加了qa文档,默认密码文档
- 新增 Skills 技能剧本库 (供 AI Agent 使用)
- 新增 Tools 外部工具声明式配置库

---

## Manual

* **Dic**
    * Auth : 认证字典
        * 账号和密码。
    * Network : 网络
        * 排除的私有 IP 段、本地 IP 段、dns 服务器列表。
    * Port : 端口字典
        * 按照端口渗透的想法,将不同端口承载的服务可爆破点作为字典内容。
    * Regular : 规则字典
        * 各种规则、排列的字典整理。
    * Web : Web 字典
        * 顾名思义,在 web 渗透过程中出现的可爆破点作为字典内容。
* **Payload**
    * Burp
    * CORS
    * email
    * Format
    * HPP
    * LFI
    * OOB
    * SQL-Inj
    * SSI
    * XSS
    * XXE
* **Skills** — AI Agent 技能剧本 (Playbook)
    * recon : 侦察类 (资产侦察、子域名、OSINT、社工等)
    * exploit : 漏洞利用类 (Web 漏洞、API Fuzz、爆破等)
    * postexploit : 后渗透类 (提权、持久化、凭据收集等)
    * lateral : 内网渗透类 (AD 攻击、横向移动、跳板等)
    * cloud : 云环境类 (IAM 审计、元数据利用等)
    * general : 综合类 (全链路、红队评估、报告生成等)
* **Tools** — 外部工具声明式 YAML 配置
    * scan : 扫描工具 (nmap, masscan)
    * fuzz : Fuzz 工具 (dirsearch)
* **Doc**
    * **Checklist** : 渗透测试过程中的检查项,杜绝少测、漏测的情况。
    * **Cheatsheet** : 渗透测试信息收集表,渗透测试时直接复制一副作为参考、信息记录、方便团队协作、出报告等。
    * **出报告专用** : 记录部分平常渗透测试遇到的案例。
    * **行业名词**
