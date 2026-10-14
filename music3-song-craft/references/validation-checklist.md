# 自检清单与 FAIL_* 失败码路由

## 1. 校验流程

1. 产出三件套草稿后，逐条执行下表检查，输出每条 PASS / FAIL。
2. 任何 FAIL → 回到对应规则文件修复，最多重试 2 次。
3. 2 次仍 FAIL → 输出校验报告（失败项 + 原因 + 修复建议）并如实上报用户，不得继续产出。
4. 全部 PASS → 输出三件套（歌词代码块 + 中英双语风格提示词代码块 + 校验报告）。

## 2. 检查项与失败码

| ID | 检查项 | PASS 条件 | FAIL 码 |
|---|---|---|---|
| A01 | 歌词与风格不可同时为空 | 至少一项有内容 | FAIL_BOTH_EMPTY |
| A02 | 歌词字符数 | 汉字 ×2 + 其他 ×1 ≤ 3500 | FAIL_LYRICS_CHAR_OVERFLOW |
| A03 | 风格提示词字符数 | ≤ 2000 | FAIL_PROMPT_CHAR_OVERFLOW |
| A04 | 段落标签合法性 | 全部标签属于官方 14 种（含合法变体） | FAIL_TAG_NOT_OFFICIAL |
| A05 | 段落标签完整性 | 用户提供的歌词每段都有标签（Intro/Outro 可留空由模型生成） | FAIL_LYRICS_NO_TAG |
| A06 | 副歌复现 | 副歌 ≥ 2 次（第 2 次可用 Final Chorus） | FAIL_STRUCTURE_NO_CHORUS_REPEAT |
| A07 | 预计时长 | ≤ 5 分钟，且已按公式估算并标注 | FAIL_DURATION_OVER_5MIN |
| B01 | 风格五要素 | 曲风+子风格 / BPM·拍号·调性 / 情绪弧线 / 人声特质 / 配器与混音 五项齐全 | FAIL_PROMPT_MISSING_ELEMENT |
| B02 | 双语输出 | 中文版 + 英文版均已输出 | FAIL_PROMPT_NO_BILINGUAL |
| B03 | 音色复刻承诺 | 未承诺复刻真实歌手音色 | FAIL_VOICE_CLONE_PROMISE |
| B04 | 原词尊重 | 未擅自改写用户歌词的词意 / 韵脚 / 句数 | FAIL_LYRICS_REWRITTEN |
| B05 | 非语言人声占位 | 哼唱 / 吟唱已用音节占位（ooh / la / mmm / ah） | FAIL_HUM_NO_SYLLABLE |
| C01 | 纯音乐备注 | 纯音乐需求已备注模型选择与纯音乐开关 | FAIL_BGM_SWITCH_NOT_NOTED |
| C02 | 商用提醒 | 校验报告含商用许可自查提醒 | FAIL_LICENSE_REMINDER_MISSING |

## 3. 修复路由

| FAIL 码 | 修复动作 | 依据文件 |
|---|---|---|
| FAIL_BOTH_EMPTY | 要求用户补充歌词或风格描述 | official-rules.md §2 |
| FAIL_LYRICS_CHAR_OVERFLOW | 压缩重复段落、删冗余长句（保留副歌 2 次） | lyrics-structure.md §6 |
| FAIL_PROMPT_CHAR_OVERFLOW | 删除次要修饰语，保留五要素骨架 | prompt-crafting.md §5 |
| FAIL_TAG_NOT_OFFICIAL | 按规范化对照表改写标签 | lyrics-structure.md §2 |
| FAIL_LYRICS_NO_TAG | 逐段补齐官方标签 | lyrics-structure.md §3 |
| FAIL_STRUCTURE_NO_CHORUS_REPEAT | 补一次副歌（可作 Final Chorus） | lyrics-structure.md §4 |
| FAIL_DURATION_OVER_5MIN | 删减段落 / 压缩句式后重新估算 | lyrics-structure.md §7 |
| FAIL_PROMPT_MISSING_ELEMENT | 按五要素模板逐项补齐 | prompt-crafting.md §1 |
| FAIL_PROMPT_NO_BILINGUAL | 补缺失语言版本 | prompt-crafting.md §1 |
| FAIL_VOICE_CLONE_PROMISE | 改为音色描述词（声部 / 音色 / 唱法 / 后期） | official-rules.md §5 |
| FAIL_LYRICS_REWRITTEN | 恢复原词，只做结构层修改 | lyrics-structure.md §1 |
| FAIL_HUM_NO_SYLLABLE | 写入官方音节占位 | official-rules.md §4 |
| FAIL_BGM_SWITCH_NOT_NOTED | 校验报告补纯音乐模型与开关备注 | official-rules.md §5 |
| FAIL_LICENSE_REMINDER_MISSING | 校验报告补商用许可自查提醒 | official-rules.md §5 |

## 4. 校验报告模板

```
【校验报告】
- 歌词字符数：N / 3500（汉字 N1 个 ×2 + 其他 N2 个）→ PASS
- 风格提示词字符数：N / 2000 → PASS
- 段落标签：官方标签 N 处，非法标签 0 处 → PASS
- 副歌复现：2 次（Chorus + Final Chorus）→ PASS
- 预计时长：约 M:SS（≤ 5:00）→ PASS
- 风格五要素：齐全 → PASS
- 风险提示：商用请自查许可条款；纯音乐需选择对应模型并开启开关；音色为描述性表达，非复刻。
全部 PASS，可复制粘贴生成。
```
