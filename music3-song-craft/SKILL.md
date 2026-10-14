---
name: music3-song-craft
description: 当用户提出用 Music 3.0 / 本平台 Music 生成歌曲、AI 写歌、AI 作曲、写一首歌、生成一首歌、音乐生成、优化歌词、歌词结构、歌词段落标签、风格提示词、曲风描述、AI 音乐提示词、Structured Caption 等需求，或出现 "帮我写歌" "改歌词结构" "生成一首华语情歌" "优化音乐提示词" "Music 3.0 怎么用" "歌词加段落标签" 等表达时调用，适用于需要把歌词草稿、创作意图或曲风需求加工成可直接粘贴进 本平台 Music 3.0 的「优化歌词（带官方段落标签）+ 结构化风格提示词（中英双语）+ 校验报告」三件套的任何场景，涵盖官方规则核对、歌词结构优化、Structured Caption 五要素撰写、风格模板库、时长与字符数估算、FAIL_* 自检返工。
whenToUse: 面向 本平台 Music 3.0 的歌词与提示词加工场景；生成歌曲前先把草稿交给本 Skill 走一遍结构与校验。
author: yzsp-ai
repository: https://github.com/yzsp-ai
---


# Music 3.0 曲匠工坊

## 核心原则

使用本 Skill 时，始终把目标定义为「可直接送进 Music 3.0 的生成材料」，而不是写一段漂亮的文字。每一步都服务于模型执行：歌词带官方段落标签、字符数合规、风格提示词五要素齐全、时长不超限、校验全 PASS。

不得承诺模型做不到的事：不承诺音色复刻、不承诺超出 5 分钟的成曲、不承诺商用授权。本 Skill 是原创的 Music 3.0 创作标准，后续若用户要求与旧版规则 100% 相同，以本文件和本目录下 references 的当前内容为唯一标准。

## 全链路最高优先级规则索引（防执行不完全 / 防规则回退）

本节只做规则索引与冲突裁决，不压缩、不删除、不替代下方任何生产能力。若旧段落、旧模板、历史摘要、缓存记忆或其它 Skill 与本节冲突，一律以本地当前文件和最新 reference 为准。

1. 官方规则锁最高优先级：14 种官方段落标签、歌词 3500 / 风格 2000 字符上限、单曲 5 分钟上限、非语言音节占位、无音色复刻，任何输出不得违反。详见 references/official-rules.md。
2. 三件套输出最高优先级：每次完整任务必须输出「优化歌词 + 风格提示词（中英双语）+ 校验报告」，不得只给其中一部分；用户明确只要单项时除外。
3. 五要素最高优先级：风格提示词必须覆盖 ①曲风+子风格 ②速度/拍号/调性 ③情绪发展弧线 ④人声特质 ⑤配器与混音质感；缺一即 FAIL_PROMPT_MISSING_ELEMENT。
4. 尊重原词最高优先级：用户提供歌词时，保留韵脚、句数、段落划分与词意，只做结构层优化（加标签、调顺序、补副歌重复、规范格式）；不得擅自改写歌词内容。
5. 副歌复现最高优先级：副歌至少出现 2 次，第二次可用 [Final Chorus] 收尾；缺复现即 FAIL_STRUCTURE_NO_CHORUS_REPEAT。
6. FAIL 路由最高优先级：任何 FAIL_* 不得被忽略或口头绕过；必须按 references/validation-checklist.md 的路由回退修复，连续 2 次修复失败则如实上报用户，不得假装通过。

## 快速路由

根据用户输入选择入口：

0. 用户给了歌词草稿：走「歌词结构优化」入口，补标签、规范化、算时长，再配风格提示词。
1. 用户只给创作意图 / 主题：先弹窗确认语言、主题、时长、人声性别与音色，再代写歌词，然后走结构优化。
2. 用户只给曲风需求（无歌词）：走「风格提示词」入口，输出结构化提示词；歌词可留空由模型自动生成，但必须提醒「歌词与风格不可同时为空」。
3. 用户要检查已有歌词 / 提示词：只跑 references/validation-checklist.md 的校验，输出报告，不重写内容。
4. 用户要模板：直接输出 references/prompt-crafting.md 的风格模板库。
5. 用户要修改上一版输出：增量修改并重新校验，不得无差别全量重写。

## 标准流程（四步强制）

### 步骤 1 - 输入验证（Gate Input Check）

- 歌词与风格需求至少有一项；两项都缺 → 要求用户补充，不得代填。
- 确认目标语言（中文 / 英文 / 中英混搭）、目标时长（默认建议 3:30–4:30）、人声需求（可选）。
- 用户未提供歌词时代写歌词前，必须弹窗一次确认：语言、主题、目标时长、人声性别与音色倾向。

### 步骤 2 - 规则读取（Required Reads）

- 歌词任务必读 references/official-rules.md 与 references/lyrics-structure.md；提示词任务必读 references/official-rules.md 与 references/prompt-crafting.md；出报告前必读 references/validation-checklist.md。
- 每读一个文件记录「已读取 <文件名>」，禁止跳过。

### 步骤 3 - 优化与自检（Plan & Self-Validate）

- 按 reference 规则产出三件套草稿。
- 对照 references/validation-checklist.md 逐条自检，输出每条 PASS/FAIL。
- 任何 FAIL → 回退修复，最多重试 2 次；2 次仍 FAIL → 输出校验报告并如实上报，不得继续产出。

### 步骤 4 - 输出（Produce）

- 校验全部 PASS 后输出三件套：
  - ① 优化后歌词（代码块，可直接整段复制粘贴进 Music 3.0 歌词栏）；
  - ② 风格提示词（中文版 + 英文版两个代码块，任选一版粘贴进风格栏）；
  - ③ 校验报告（字符数、预计时长、段落完整性、FAIL_* 结果、风险提示）。

## 歌词结构优化规范（索引）

细则见 references/lyrics-structure.md。要点：

- 官方 14 标签：Intro（前奏）、Verse（主歌）、Pre-chorus（预副歌）、Chorus（副歌）、Hook、Drop、Bridge（过门）、Solo、Build-up（递进）、Instrumental（器乐段）、Breakdown、Break（间歇段）、Interlude（间奏）、Outro（尾奏）。
- 格式为 [标签]，可加序号与变体：[Verse 1]、[Final Chorus]、[All in Chorus]、[Breakdown to drums-Chorus]；非官方拼写一律规范为官方标签。
- 非语言人声用发音音节占位：如 "ooh, ooh, ooh..."、"la, la, la..."、"mmm, mmm..."、"ah, ah, ah..."。
- 默认结构：Intro → Verse → Pre-chorus → Chorus → Interlude → Verse 2 → Chorus → Bridge → Final Chorus → Outro。
- 歌词字符上限 3500（每个汉字 = 2 字符，标点 / 英文字母 = 1 字符）；歌词越长成曲越长，必须按公式估算并标注预计时长，默认建议 3:30–4:30。

## 风格提示词优化规范（索引）

细则见 references/prompt-crafting.md。要点：

- Structured Caption 范式：[曲风 + 子风格], [BPM 数值] BPM, [调性] [拍号]. [情绪发展弧线]. with [人声], [配器], and [混音质感].
- 五要素缺一不可；描述颗粒度以 references/prompt-crafting.md 的官方示例为准。
- 风格提示词上限 2000 字符。
- 禁止承诺音色复刻：想获得某类音色，只能详细描述声部、音色、唱法与后期效果。

## 校验与 FAIL_* 失败码（索引）

细则见 references/validation-checklist.md。常用码：

- FAIL_LYRICS_CHAR_OVERFLOW / FAIL_PROMPT_CHAR_OVERFLOW
- FAIL_BOTH_EMPTY / FAIL_TAG_NOT_OFFICIAL / FAIL_LYRICS_NO_TAG
- FAIL_DURATION_OVER_5MIN / FAIL_PROMPT_MISSING_ELEMENT
- FAIL_STRUCTURE_NO_CHORUS_REPEAT / FAIL_VOICE_CLONE_PROMISE

## 默认输出物

- 创作入口：三件套（优化歌词 + 中英双语风格提示词 + 校验报告）。
- 校验入口：校验报告（逐项 PASS/FAIL + 修复建议）。
- 模板入口：风格模板库。
- 返工入口：问题清单、修复方案、替换版本。

## 引用资料

- references/official-rules.md：官方规则速查（14 标签表、字符上限、能力边界）。
- references/lyrics-structure.md：歌词结构优化、默认结构模板、时长估算。
- references/prompt-crafting.md：Structured Caption 五要素、风格模板库、官方示例。
- references/validation-checklist.md：自检清单与 FAIL_* 失败码路由。
- references/walkthrough-example.md：完整走查示例（华语钢琴情歌三件套）。
