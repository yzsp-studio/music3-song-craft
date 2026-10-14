# 走查示例：完整三件套（原创歌词）

> 输入：用户只给创作意图「写一首关于告别与重逢的华语抒情歌，男声，3:30–4:30」。
> 本示例演示：代写原创歌词 → 结构层优化（官方标签 + 默认结构模板）→ 中英双语风格提示词 → 校验报告。
> 歌词为 Skill 原创示例内容，与任何已有歌曲无关；同款流程可套用于任意曲风（模板见 references/prompt-crafting.md §3）。

## ① 优化后歌词（直接复制粘贴进 Music 3.0 歌词栏）

```
[Intro]
[Verse 1]
六月的风 把窗帘吹旧
站台的钟 数着车票的褶皱
我把你的名字 折进衬衫领口
转身那刻 蝉声忽然很厚
[Pre-chorus]
后来路过的城 都像你住过的巷口
我站在原地 等晚霞低头
[Chorus]
我把黄昏装进口袋 慢慢地走
把影子交给街灯去守
你要相信 所有告别 都是重逢的缘由
风起的时候 花还开在枝头
[Interlude]
[Verse 2]
你寄来的信 压着海边的邮戳
说那边的夜 星星比这里多
我回信只写 巷口花铺刚开过
还有昨晚 窗台的月光很薄
[Pre-chorus]
后来路过的城 都像你住过的巷口
我站在原地 等晚霞低头
[Chorus]
我把黄昏装进口袋 慢慢地走
把影子交给街灯去守
你要相信 所有告别 都是重逢的缘由
风起的时候 花还开在枝头
[Bridge]
如果时间 真能倒着流
我想把话 再从头说出口
[Final Chorus]
我把黄昏装进口袋 慢慢地走
把影子交给街灯去守
你要相信 所有告别 都是重逢的缘由
风起的时候 花还开在枝头
[Outro]
等下一班车 靠站的时候
```

## ② 风格提示词（中文版，复制粘贴进风格栏）

```
华语流行抒情 / 钢琴情歌，76 BPM，C 大调，4/4。主歌低声叙述、气声轻唱，预副歌渐强，副歌温暖上扬、混声推进，终副歌最满、尾奏渐弱。以温暖男中音为主唱（主歌气声 + 副歌混声），钢琴分解和弦引领，弦乐长音铺底，间奏小提琴独奏，贝斯根音跟随，副歌进入轻摇滚鼓组，温暖自然的大厅混响。
```

## ② 风格提示词（英文版）

```
Mandarin pop ballad / piano ballad, 76 BPM, C major, 4/4. Tender, intimate verses unfold into a warm, rising chorus, led by a mellow male baritone with breathy verses and a mixed-voice chorus, supported by piano arpeggios, lush strings, a violin solo interlude, soft bass, and light rock drums entering at the chorus, with a warm natural hall reverb.
```

## ③ 校验报告

```
【校验报告】
- 歌词字符数：约 750 / 3500（303 个汉字 ×2 + 段落标签与标点约 140 个 ×1）→ PASS
- 风格提示词字符数：约 165（中文版）/ 约 410（英文版） / 2000 → PASS
- 段落标签：Intro / Verse 1 / Pre-chorus / Chorus / Interlude / Verse 2 / Bridge / Final Chorus / Outro，全部为官方 14 种标签 → PASS
- 副歌复现：2 次（Chorus + Final Chorus）→ PASS
- 预计时长：人声约 212 秒（303 字，抒情 76 BPM 按每 100 字约 70 秒）+ Intro 15 秒 + Interlude 12 秒 + Outro 12 秒 ≈ 4:11（≤ 5:00，处于推荐区间 3:30–4:30）→ PASS
- 风格五要素：曲风+子风格 / BPM·拍号·调性 / 情绪弧线 / 人声特质 / 配器与混音，齐全 → PASS
- 原词尊重：本示例为代写歌词（用户仅给创作意图），未涉及改写用户原词 → PASS
- 风险提示：商用请自查许可条款；本示例为带歌词歌曲，不涉及纯音乐开关；人声为描述性表达，非音色复刻。
全部 PASS，可复制粘贴生成。
```
