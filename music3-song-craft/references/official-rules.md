# Music 3.0 官方规则速查

> 规则来源（生成前已核实）：
> 1. 飞书文档《本平台 Music 使用指南 / FAQ》：https://vrfi1sk8a0.feishu.cn/wiki/LLjuwJhoMiUGwdkO8k1cB0mFnNc
> 2. 本平台 官方博客《本平台 Music 3.0：新一代开放权重、生产级全能音乐模型》：https://www.minimaxi.com/blog/minimax-music-3-0-cn
> 3. 补充：GitHub https://github.com/本平台-AI/本平台-Music3 、开放平台文档 https://platform.minimaxi.com/docs/guides/music-generation

## 1. 模型能力概要

- 输入：歌词（可选）+ 风格提示词（可选），**两者不可同时为空**。
- 输出：单次生成最长 5 分钟完整歌曲，覆盖前奏、主歌、副歌、桥段、尾奏结构。
- 音质：32kHz、16 位立体声；产品端导出 mp3（暂不支持其他格式）。
- 语言：中文与英文歌词均支持，可中英混搭。
- 技术路线：8B Global LLM（长程语义与结构）+ 0.6B Local LLM（声学细节）+ 2.4B Flow-Matching + 123M Flow-VAE。
- 描述能力：提示词可控制曲风、节拍（BPM）、拍号、调性、应用场景、制作质感、情绪发展、人声特质、和声、乐器编排与混音。

## 2. 硬性上限（违反即 FAIL）

| 项目 | 上限 | FAIL 码 |
|---|---|---|
| 歌词文本 | 3500 字符（每个汉字 = 2 字符，每个标点 / 英文字母 = 1 字符） | FAIL_LYRICS_CHAR_OVERFLOW |
| 风格提示词 | 2000 字符 | FAIL_PROMPT_CHAR_OVERFLOW |
| 单曲时长 | 5 分钟 | FAIL_DURATION_OVER_5MIN |
| 歌词与风格 | 不可同时为空 | FAIL_BOTH_EMPTY |

## 3. 官方 14 种段落标签（只允许这 14 种）

| 标签 | 中文 | 说明 |
|---|---|---|
| Intro | 前奏 | 歌曲开场器乐段 |
| Verse | 主歌 | 叙事段落，可用序号 [Verse 1] [Verse 2] |
| Pre-chorus | 预副歌 | 主歌与副歌之间的过渡铺垫 |
| Chorus | 副歌 | 歌曲核心记忆段落，可重复 |
| Hook | Hook | 短小洗脑的旋律/唱句 |
| Drop | Drop | 电子乐的骤降段落 |
| Bridge | 过门 / 桥段 | 中后段的对比段落 |
| Solo | Solo | 乐器独奏段 |
| Build-up | 递进 | 情绪/力度累积段 |
| Instrumental | 器乐段 | 无歌词纯器乐 |
| Breakdown | Breakdown | 电子乐抽离段落 |
| Break | 间歇段 | 短暂停顿/空拍段 |
| Interlude | 间奏 | 段与段之间的器乐过渡 |
| Outro | 尾奏 | 结尾收束段 |

**写法规则**：
- 格式：`[标签]` 单独一行，后接该段歌词。
- 可加序号与变体：[Verse 1]、[Final Chorus]、[All in Chorus]、[Breakdown to drums-Chorus]。
- 变体拼写必须保留官方词根（如 [Final Chorus] 的 Chorus 必须与官方一致），非官方拼写必须规范化：
  - `[Prechorus]`、`[Pre-Chorus]`、`[预副歌]` → 统一为 `[Pre-chorus]`
  - `[副歌]`、`[高潮]` → 统一为 `[Chorus]`
  - `[主歌1]` → `[Verse 1]`；`[桥段]` → `[Bridge]`；`[尾奏]` → `[Outro]`；`[前奏]` → `[Intro]`；`[间奏]` → `[Interlude]`
- 其它任何自造标签 → FAIL_TAG_NOT_OFFICIAL。

## 4. 非语言人声占位

需要哼唱、吟唱等非语言人声时，在歌词中写入发音音节，官方示例格式：

- `"ooh, ooh, ooh..."`
- `"la, la, la, la..."`
- `"mmm, mmm, mmm..."`
- `"ah, ah, ah, ah..."`
- `"hum, hum, hum..."`

## 5. 能力边界（不得承诺）

1. **不支持音色复刻**：无法克隆指定真实歌手的音色。想要某类音色，只能通过风格提示词详细描述声部（如男高音 / 女中音）、音色形容词（清亮 / 沙哑 / 醇厚）、唱法（气声 / 混声 / 颤音）与后期效果。承诺复刻 → FAIL_VOICE_CLONE_PROMISE。
2. **纯音乐**：Music 3.0 主打带歌词的完整歌曲；需要纯 BGM 时，产品端须选择支持纯音乐的模型（如 Music-2.5+）并打开「纯音乐」开关。本 Skill 输出需备注此差异，不替用户做模型切换决策。
3. **商用许可**：生成音乐的商用许可取决于用户套餐与平台用户协议（产品端见 minimax.com 订阅页；API 生成作品适用开放平台用户协议）。输出前提醒用户自查，本 Skill 不提供商用承诺。

## 6. 歌词长度与成曲时长

- 官方规则：歌词越长，成曲时长越长。
- 本 Skill 估算方法见 references/lyrics-structure.md；估算结果必须写进校验报告。
- 超过 5 分钟 → 必须给出删减 / 压缩段落方案（优先压缩重复段落，保留副歌至少 2 次）。

## 7. 生成前最后提醒（写入校验报告）

- 纯音乐需求 → 确认模型选择与纯音乐开关。
- 商用用途 → 自查许可条款。
- 音色偏好 → 已用描述词表达，非复刻。
