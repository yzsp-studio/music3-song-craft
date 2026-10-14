# 风格提示词优化（Structured Caption 五要素）

> 官方范式来源：本平台 Music 3.0 发布博客。模型用细粒度时序描述理解创作意图，并从专业 Structured Caption 模板库扩展简单描述（Prompt Enhancement System）。因此提示词越结构化、越"专业编曲语言"，生成越贴合意图。

## 1. 五要素模板（必须全部覆盖，缺一即 FAIL_PROMPT_MISSING_ELEMENT）

### 中文范式

```
[曲风 + 子风格]，[BPM 数值] BPM，[调性] [拍号]。[情绪发展弧线：主歌…预副歌…副歌…桥段…尾奏…]。以[人声声部 + 音色 + 唱法]为主唱，[主奏乐器]引领，[辅奏乐器]铺底，[段落配器变化]，[混音 / 制作质感]。
```

### 英文范式

```
[Genre / subgenre], [BPM] BPM, [key] [time signature]. [Emotional arc: verses… chorus… bridge…]. with [vocal: range, timbre, technique], [lead and supporting instruments and their entrances], and [mix / production quality].
```

### 五要素逐一说明

| # | 要素 | 必写内容 | 反例 |
|---|---|---|---|
| ① | 曲风 + 子风格 | 主风格与子风格并用，如 "Warm Mandarin pop / traditional Chinese ballad" | 只写 "流行" |
| ② | 速度 / 拍号 / 调性 | BPM 数值 + 拍号 + 调性（有把握时写），如 "74 BPM, A-flat major" | 只写 "中速" |
| ③ | 情绪发展弧线 | 按段落描述起伏，而非单个情绪词，如 "Tender nostalgia opens into a celebratory chorus" | 只写 "伤感" |
| ④ | 人声特质 | 声部（男高音 / 女中音…）+ 音色 + 唱法（breathy / mixed-voice / vibrato）+ 和声 | 只写 "女声" |
| ⑤ | 配器 + 混音质感 | 主辅乐器、何时进入 / 退出、律动与低频发展、混音质感（warm / polished / live-room） | 只写 "钢琴" |

## 2. 官方示例颗粒度（照此写）

```
Warm Mandarin pop / traditional Chinese ballad, 74 BPM, A-flat major. Tender nostalgia opens into a celebratory chorus, with a mature male baritone-tenor, delicate guzheng, soft strings, gentle acoustic textures, expressive vibrato, and a natural live-room sound.
```

```
Progressive house / EDM, 126 BPM, B-flat major. Reflective and nostalgic verses rise into a cathartic, euphoric chorus, with a smooth breathy male tenor, pulsing side-chained synths, punchy club bass, crisp drums, and wide hall reverb.
```

```
Bright power pop / pop rock, 112 BPM, E-flat major. Nostalgic, bittersweet verses burst into cathartic choruses, led by a clear female mezzo-soprano with soaring octave hooks, punchy drums, wide layered guitars, subtle synths, and a polished modern mix.
```

## 3. 风格模板库（可直接套用，按需改 BPM / 调性 / 人声）

### T-01 华语钢琴情歌（经典抒情）
- 中文：华语流行抒情 / 钢琴情歌，74 BPM，♭B 大调，4/4。主歌低声叙述、气声轻唱，预副歌渐强，副歌明亮上扬、强混声爆发，终副歌最满、尾奏渐弱。以清亮男高音为主唱（主歌气声 + 副歌强混声），钢琴分解和弦引领，弦乐长音铺底，间奏小提琴独奏，贝斯根音跟随，副歌进入轻摇滚鼓组，温暖自然的大厅混响。
- English: Mandarin pop ballad / piano ballad, 74 BPM, B-flat major, 4/4. Tender, intimate verses unfold into a radiant chorus, led by a clear male tenor with breathy verses and a powerful mixed-voice chorus, supported by piano arpeggios, lush strings, a violin solo interlude, soft bass, and light rock drums entering at the chorus, with a warm natural hall reverb.

### T-02 温暖民谣
- 中文：温暖治愈系民谣 / 独立民谣，76 BPM，G 大调，4/4。主歌安静自白、副歌朴素上扬。以醇厚女中音为主唱（轻声咬字 + 自然颤音），木吉他扫弦引领，口琴点缀，轻钢琴铺底，低音提琴拨弦，无鼓或轻刷鼓，近距离温暖房间质感。
- English: Warm healing folk / indie folk, 76 BPM, G major, 4/4. Quiet confessional verses rise into a plain, uplifting chorus, with a mellow female alto, gentle acoustic guitar strums, harmonica accents, light piano, upright bass, brushed drums or no drums, and an intimate warm room sound.

### T-03 都市 R&B
- 中文：都市 R&B / 新灵魂乐，88 BPM，♭A 大调，4/4。主歌慵懒低语、副歌丝滑上扬。以磁性男中音为主唱（气声转音 + 假声高音），电钢琴引领，808 低音沉稳，踩镲十六分律动，副歌加和声堆叠，现代清透的录音室混音。
- English: Urban R&B / neo-soul, 88 BPM, A-flat major, 4/4. Lazy whispered verses glide into a silky rising chorus, with a magnetic male baritone, airy riffs and falsetto highs, electric piano, deep 808 bass, sixteen-note hi-hat groove, stacked harmonies in the chorus, and a modern clean studio mix.

### T-04 国风
- 中文：国风 / 传统中式抒情，72 BPM，D 宫五声调式，4/4。主歌水墨留白、副歌辽阔舒展。以温润女声为主唱（吟唱感长音 + 细腻颤音），古筝弹拨引领，笛箫点缀，弦乐长音铺底，轻打击（木鱼 / 钟磬）营造空间感，自然现场厅堂混响。
- English: Chinese traditional style / guofeng ballad, 72 BPM, D major pentatonic, 4/4. Water-ink spare verses open into a vast unfolding chorus, with a warm female vocal, delicate guzheng plucks, dizi and xiao accents, soft string pads, light traditional percussion, and a natural live-hall reverb.

### T-05 电子舞曲 EDM
- 中文：旋律电子舞曲 / progressive house，126 BPM，♭B 大调，4/4。主歌克制铺垫、Drop 全开释放。以清透女声为主唱（主歌气声 + 副歌高亢混声），明亮分层合成器引领，脉冲侧链贝斯，四四拍底鼓，清脆军鼓与镲片，宽阔的节日级混音。
- English: Melodic EDM / progressive house, 126 BPM, B-flat major, 4/4. Restrained verses build into a full-release drop, with a clear female vocal, bright layered synths, pulsing side-chained bass, four-on-the-floor kick, crisp snares and hats, and a wide festival-polished mix.

### T-06 轻摇滚
- 中文：明亮流行摇滚 / 力量流行，112 BPM，E 大调，4/4。主歌怀旧克制、副歌酣畅爆发。以明亮女中音为主唱（八度大跳副歌），有力鼓组，宽阔分层电吉他，轻合成器点缀，现代精致混音。
- English: Bright pop rock / power pop, 112 BPM, E major, 4/4. Nostalgic restrained verses burst into cathartic choruses, with a clear female mezzo-soprano and soaring octave hooks, punchy drums, wide layered guitars, subtle synths, and a polished modern mix.

### T-07 爵士
- 中文：经典上海爵士 / 灵魂乐，96 BPM，♭E 大调，4/4 摇摆律动。主歌轻柔叙事、副歌慵懒闪光。以亲昵女声为主唱（克制乐句处理），柔和钢琴引领，低音提琴拨弦，鼓刷轻扫，暖铜管点缀，复古房间质感混音。
- English: Classic Shanghai jazz / soul, 96 BPM, E-flat major, 4/4 swing. Tender nostalgic verses unfold into a softly radiant chorus, with an intimate female vocal and restrained phrasing, mellow piano, upright bass, brushed drums, warm brass accents, and a vintage room-like mix.

### T-08 影视感纯音乐（仅备注，不直接用于 3.0）
- 说明：纯音乐需产品端选择支持纯音乐的模型并开启纯音乐开关；风格提示词改为纯器乐描述，如 "Cinematic orchestral / film score, 90 BPM, C minor, 4/4. A restrained opening grows into an epic wall-of-sound finale, with strings, brass, timpani and a wide concert-hall mix."
- 中文：电影感管弦乐 / 影视配乐，90 BPM，C 小调，4/4。内敛开场渐强至宏大声墙终章，弦乐、铜管、定音鼓，宽阔音乐厅混音。

## 4. 缺省档位（用户未指定参数时）

| 参数 | 缺省值 |
|---|---|
| BPM | 76（抒情）；未定曲风时先按抒情处理 |
| 调性 | 不写死；写 "key 由模型自适配" 或从用户参考歌推定 |
| 拍号 | 4/4 |
| 语言 | 中文 |
| 时长 | 3:30–4:30 |
| 人声 | 用户指定；未指定时按曲风模板默认 |

## 5. 禁止项

- 禁止承诺音色复刻（FAIL_VOICE_CLONE_PROMISE）。
- 禁止风格与歌词同时为空。
- 禁止风格提示词超过 2000 字符；超限时删除次要修饰语，保留五要素骨架。
- 中文提示词正文保持中文；英文版独立输出，不中英混排。
