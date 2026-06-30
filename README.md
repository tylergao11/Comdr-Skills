# Comdr-Skills

Cocos Creator 3.x 专精 AI coding skills。给 Claude/Codex 注入资深 Cocos 开发者的设计判断力——不教 API，只教**什么时候该用什么**和**为什么**。

## 安装

```bash
# 克隆到 Claude Code skills 目录
git clone https://github.com/tylergao11/Comdr-Skills.git ~/.claude/skills/comdr-skills

# 或者：作为项目 skills
cp -r skills/* your-project/.claude/skills/
cp -r agents/* your-project/.claude/agents/

# Codex：安装指定 skill
python ~/.codex/skills/.system/skill-installer/scripts/install-skill-from-github.py \
  --repo tylergao11/Comdr-Skills \
  --ref master \
  --path skills/cocos-creator-3x-judgment \
  --path skills/qzxz-migration-boundary \
  --path skills/open-os
```

## Skills

| Skill | 做什么 |
|---|---|
| `cocos-lifecycle` | 组件生命周期非直觉行为（onLoad 时序、destroy vs removeFromParent、场景切换交叠） |
| `cocos-assets` | 资源系统设计约束（引用计数陷阱、bundle 拆还是合、图集策略） |
| `cocos-ui` | UI 适配思路模型（两层适配、Widget 拉伸、Layout resizeMode、渲染排序） |
| `cocos-conventions` | 实战约定（硬编码→单一真相源、Interface 中心化、MVC 实际形态、节点引用策略、找 bug 纪律） |
| `cocos-pitfalls` | 平台硬坑（纹理压缩、TTF 字体、JSC vs V8、微信小游戏限制） |
| `comdr-workflow` | Comdr 与 Coding 协作判断——什么时候走 MCP tool、什么时候直接写代码 |
| `open-os` | 开放作业体系：先探针、定边界、定验收，再修改代码和文档资产 |
| `cocos-creator-3x-judgment` | Codex 版 Cocos 3.x 判断层：生命周期、资源、UI、平台、代码审查、编辑器/代码边界 |
| `qzxz-migration-boundary` | qzxz 七张血战 Lua→TS 迁移边界：主游戏/子游戏、PB 协议、缓存/UI/资源审计 |

## Subagents

| Agent | 用途 |
|---|---|
| `cocos-reviewer` | Cocos 3.x TypeScript 代码审查 |
| `cocos-planner` | Cocos 项目架构规划 |

## 设计原则

- 每条内容通过"删掉这句 Claude 还会不会"审计
- 只保留 Cocos 引擎特有、Claude 不可能从通用知识推理的内容
- Skills 教**怎么想**（设计思路、选择依据），Comdr 负责**怎么做**（编辑器操作）

## 联动

[Comdr](https://github.com/tylergao11/Comdr) — Cocos 编辑器 AI 操作体。Comdr-Skills 提供编码智能，Comdr 提供编辑器操作，两者配合覆盖完整 Cocos 开发工作流。
