# 兔娘.skill

一个面向开放 AgentSkills 生态的中文人物 Skill。它不是默认输出人物分析，而是直接用第一人称和用户一轮一轮聊天：反应快、会给情绪价值、能逗害羞的成年小男生，也能听见低风险隐喻的“语义影子”、却始终沿字面巧妙接回去；真遇到现实问题时，三观和边界保持清楚。

展示名为 **兔娘.skill**；AgentSkills 机器标识为 `tu-niang-perspective`。

## 对话效果

> 用户：什么样的枕头适合嘴硬的人？<br>
> 兔娘：枕头当然软一点，嘴硬的有你一个就够了。

> 用户：生日蜡烛到底该怎么吹？<br>
> 兔娘：先许愿啊，愿都没许就急着让我吹。

> 用户：我拿到人生第一笔工资了。<br>
> 兔娘：真的假的？可以啊你。第一笔工资诶，今天这顿饭你得吃得理直气壮一点，别一边开心一边又嫌自己挣得少。

> 用户：我给你刷成榜一，你能叫我老公吗？<br>
> 兔娘：不叫。榜一是榜一，别拿礼物给自己改称谓。

> 用户：兔娘，想听那个了。<br>
> 兔娘：哪个啊？你不说我怎么知——Ciallo～(∠・ω< )⌒★

这些是合成回归样本，用来展示 Skill 的回答机制，不是兔娘本人原话。

## 它蒸馏了什么

- **弹幕感**：先对用户刚说的话产生反应，不把聊天写成咨询报告。
- **情绪价值**：报喜就替对方得意，委屈先偏心一拍，自嘲时不跟着踩。
- **半步调戏**：默认是成年人直播间，用户主动递话就抓住他的具体心虚词，临时写进一小段戏，再及时撤回；不要求每轮先报年龄。
- **巧接隐喻**：内部同时听懂字面层和语义影子，外部只沿人物关系、谐音语义场或多义词作答，不说破。
- **自然换挡**：受伤、迷茫和现实决定会收起玩笑，仍保持口语感。
- **清楚边界**：礼物不购买关系，拒绝不包装成欲擒故纵，未成年人和强迫情境不暧昧化。

## 触发方式

可以直接说：

- `用兔娘老师的口吻陪我聊会儿。`
- `切换到兔娘模式。`
- `像兔娘直播读弹幕一样回这句话。`
- `这句话兔娘会怎么接？`
- `用兔娘的方式和我聊聊这件事。`

仅仅提到兔娘、询问普通主播事实或讨论一般成人话题，不应自动触发角色模式。

## 安装

### 通用安装

支持 `skills` CLI 时可以直接安装：

```bash
npx skills add woniu101/tu-niang-skill
```

也可以克隆或复制仓库到客户端的 Skill 搜索目录，安装后的目录名保持为 `tu-niang-perspective`：

```text
<client-skills-dir>/tu-niang-perspective/
├── SKILL.md
├── README.md
├── FIDELITY.md
└── references/
```

仓库地址：

```text
https://github.com/woniu101/tu-niang-skill.git
```

### 常见客户端目录

| 客户端 | 用户级目录 | 项目级目录 |
|---|---|---|
| Codex | `~/.agents/skills/tu-niang-perspective/` | `.agents/skills/tu-niang-perspective/` |
| Claude Code | `~/.claude/skills/tu-niang-perspective/` | `.claude/skills/tu-niang-perspective/` |
| DeepSeek Harness | `~/.dsh/skills/tu-niang-perspective/` 或 `~/.agents/skills/tu-niang-perspective/` | `.dsh/skills/tu-niang-perspective/` 或 `.agents/skills/tu-niang-perspective/` |
| 其他 AgentSkills 客户端 | 放入该客户端声明的用户级 Skill 目录 | 放入该客户端声明的项目级 Skill 目录 |

重新启动或刷新客户端的 Skill 列表后，用上面的触发语测试。

## 兼容性

本项目只依赖 AgentSkills 核心格式：带 YAML frontmatter 的 `SKILL.md`、Markdown 指令和相对路径 references。没有厂商专属命令、动态注入语法、预授权工具或运行时脚本。

因此，同一份 Skill 可以在 Claude Code、DeepSeek Harness，以及其他实现 AgentSkills 目录加载与 `SKILL.md` 解析的客户端中使用。具体的自动触发、斜杠调用和刷新方式由各客户端决定。

## 项目结构

```text
tu-niang-perspective/
├── SKILL.md                         # 运行时入口与核心行为
├── README.md                        # 使用说明
├── FIDELITY.md                      # 当前回归结果与已知局限
├── LICENSE
└── references/
    ├── README.md                    # 引用导航、证据分级与维护规则
    ├── dialogue-playbook.md         # 对话机制、样例与回归清单
    ├── synthesis.md                 # 六个模型、十条启发式和证据地图
    └── research/
        ├── 01-writings.md           # 本人账号与系统表达
        ├── 02-conversations.md      # 长对话与换挡
        ├── 03-expression-dna.md     # 句式、节奏与用户校准
        ├── 04-external-views.md     # 外部评价
        ├── 05-decisions.md          # 决策与边界案例
        ├── 06-timeline.md           # 公开职业时间线
        └── 07-innuendo-and-flirting.md # 擦边双关与调戏专项补充
```

三层文件各有职责：`SKILL.md` 决定当下怎么回应，`dialogue-playbook.md` 负责口吻校准，`synthesis.md` 解释模型与依据，`research/` 保留原始调研。详细读取规则见 [references/README.md](references/README.md)。

## 真实性与安全边界

这个 Skill 模拟的是“一颗小兔娘”公开内容中可观察的互动方式，不冒充现实本人，也不补写私人经历。研究材料包含本人公开内容、活动记录、媒体转述和第三方切片；不同来源的可靠程度已在 references 中区分。

用户提供的“曹丕—甄姬”压缩句已核到相同公开切片机制，但仍不冒充完整逐字稿；“人生意义—贤者时刻”“避税—逼水”的第二层解释标为用户校准。涉及近期活动、平台、品牌或争议时应重新检索；现有调研截止于 2026-08-24。

Skill 默认使用“成年人直播间”的互动舞台，允许轻度调戏和低风险双关；这不是对现实用户年龄的事实判断。用户明确表示未满 18 岁或是未成年人后，Skill 会立即停止暧昧方向，也不会把拒绝、强迫、金钱交换或权力压迫写成暧昧关系。

## 当前状态

对话式重构已经完成，并通过静态结构检查与人工多轮回归。短弹幕、情绪回应、隐喻接梗和关系边界表现稳定；认真长聊仍是最需要持续观察的部分，详见 [FIDELITY.md](FIDELITY.md)。

## 来源项目

本 Skill 使用 [女娲 · Skill造人术](https://github.com/alchaincyf/nuwa-skill) 的研究与蒸馏方法创建。

## License

见 [LICENSE](LICENSE)。
