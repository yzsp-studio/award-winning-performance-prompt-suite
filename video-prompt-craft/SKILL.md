---
name: video-prompt-craft
description: |
  电影级 AI 视频提示词生成专家。将静态图片或场景描述转化为 Seedance 2.0 可直接使用的
  逐秒时间码视频提示词。融合真人表演层（微表情/眼神/肌肉链）与动画物理层
  （预期动作/挤压拉伸/跟随重叠/弧线运动/时间控制/慢入慢出）。
  内置八大推演层，自动区分写实/动画/混合风格，匹配对应的表演精度和物理密度。
  支持文戏/武戏双模式切换，融入伪透视公式与镜头密码。
  输出可直接复制粘贴到 Seedance 2.0 使用，杜绝废话。
  触发词包括：逐秒时间码、Seedance提示词、影视级提示词、图生视频提示词、I2V prompt、
  八层推演、武戏提示词、文戏提示词、表演提示词、动画提示词、animation prompt、
  迪士尼法则、动画法则、animation principles、挤压拉伸、预期动作、
  跟随重叠、慢入慢出、FACS提示词、精准控制、肌肉级描述、物理化描述、
  动画物理提示词、award-winning-performance-prompt、biomechanics prompt、让视频更真实、让动作更自然、
  动画增强、弧线运动、伪透视公式、镜头密码。
  不适用于：通用 prompt 写法教学（用 video-prompting）、静态图片生成（用 image agent）。
summary-cn: 影视级视频提示词工坊——写实+动画双模式八层推演
summary-en: Cinema-grade video prompt workshop — 8-layer reasoning for realism + animation
version: 1.0.0
tags: [Video, Prompt Engineering, Cinematic, Animation, Seedance, FACS, Biomechanics]
tags-cn: [视频, 提示词工程, 动画]
trigger-words: [逐秒时间码, Seedance提示词, 影视级提示词, 图生视频提示词, I2V prompt, 八层推演, 武戏提示词, 文戏提示词, 表演提示词, 动画提示词, animation prompt, 迪士尼法则, 动画法则, animation principles, 挤压拉伸, 预期动作, 跟随重叠, 慢入慢出, FACS提示词, 精准控制, 肌肉级描述, 物理化描述, 动画物理提示词, award-winning-performance-prompt, biomechanics prompt, 让视频更真实, 让动作更自然, 动画增强, 弧线运动, 伪透视公式, 镜头密码]
author: yzsp-ai
repository: https://github.com/yzsp-ai
---


# Video Prompt Craft — 影视级视频提示词工坊

将一张静态图片或场景描述转化为**电影级品质**的 Seedance 2.0 视频提示词。
融合**真人表演精度**与**动画物理原理**，双模式覆盖写实和动画两种风格。

**核心理念**：用科学语言定义**运动过程**，而非描述静态外观。

---

## 铁律（生成前必读，违反任何一条 = 废 prompt）

1. **动态优先**：每秒必须有可见变化（微表情/物理飘动/光影流转），静态描写直接删掉
2. **运镜必写**：每一拍都有运镜指令，没有运镜的 prompt 模型会自己乱选
3. **媒介必锁**：写实/动漫/3D 三选一显式声明 + NOT 排除项，混着写直接崩
4. **角色身份卡逐字重复**：子 agent 无状态，跨镜头必须重复完整外貌描述
5. **禁止抽象情绪词**："悲伤""愤怒" → 换成具体肌肉/运动描述
6. **每个镜头只聚焦 3-5 个核心细节**，堆砌 10+ 描述 = 模型全部忽略

## 反模式（生产中常见翻车，对照自查）

| 反模式 | 为什么翻车 | 正确做法 |
|--------|----------|---------|
| 写"表情悲伤" | 模型不理解抽象情绪 | 写具体肌肉：嘴角下拉+皱眉+眼睑松弛 |
| 堆砌 15 个细节描述 | 模型注意力饱和，全部变模糊 | 只保留最重要的 3-5 个 |
| 不写媒介锁 | 模型在写实和动漫之间飘移 | `Medium: hyper-realistic photography. NOT anime, NOT 3D render` |
| 运镜写在 prompt 末尾 | 位置太靠后被稀释 | 运镜写在每个时间段的开头 |
| 同时写"cyberpunk + 北欧极简" | 两种相反美学互相抵消 | 一个镜头只用一种美学风格 |
| "角色缓缓走来"这种文学化描述 | 模型需要物理参数 | `stride 70cm at 3 steps/s, weight shifting from heel to toe` |
| 跨镜不重复角色外貌 | 模型"忘了"角色长什么样 | 角色身份卡片逐字粘贴到每个 prompt |

---

## STEP 0: CHECK INPUT

需要以下输入：

1. **图片或场景描述**（必须）：一张参考图 OR 文字场景描述
   - 如果是图片：用 `hub_read_media` 分析图片内容
   - 如果是文字：直接使用用户描述
2. **目标时长**（可选，默认 5s）：5s / 10s / 15s
3. **画面比例**（必须确认）：16:9（横屏）/ 9:16（竖屏）/ 1:1（方形）
   - 如果用户没指定，**主动询问一次**，确认后锁定全项目统一
4. **风格模式**（可选，自动判断）：写实 / 动画 / 混合
5. **场景类型**（可选，自动判断）：文戏 / 武戏 / 混合

如果用户只发了一张图没说别的，**直接分析并生成提示词，不要多问**（但画面比例仍需确认）。

---

## STEP 1: ANALYZE SCENE

后台推演，不输出给用户。

### 1a. 风格模式判定

| 模式 | 判断依据 | 推演层优先级 |
|------|---------|------------|
| **写实** | 真人/写实CG/自然场景 | L1-L5+L7 为主，L6/L8 轻量 |
| **动画** | 卡通/Q版/2D动画风 | L6-L8+L1/L3 为主，L4/L5 轻量 |
| **混合** | 写实场景+夸张动作 | 全 8 层均衡 |

### 1b. 场景分类

| 类型 | 判断依据 | 表演密度 |
|------|---------|---------|
| **文戏** | 对话/独白/情感 | 眼神每1.5s一次，情绪0.5-1s渐变 |
| **武戏** | 打斗/追逐/对决 | 全身肌肉链+碰撞+重力必写 |
| **混合** | 文转武/武转文 | 转折点切换密度 |

### 1c. 环境识别
- 空间特征 → 伪透视公式
- 光源类型 → 融入每秒描述
- 环境活物 → 背景微动（尘埃/烟/风/水/火/落叶）

### 1d. 时长→片段映射

| 时长 | 片段数 | 单片段 |
|------|-------|--------|
| 5s | 3-4 段 | 1.2-1.7s |
| 10s | 6-8 段 | 1.2-1.7s |
| 15s | 9-12 段 | 1.2-1.7s |

---

## STEP 2: GENERATE PROMPT — 八大推演层

**直接输出时间码格式，不加废话。**

### L1 — 动态优先
拒绝静态描写。每秒必须有微表情（眼神/呼吸）、物理飘动（发丝/衣摆）、肢体位移。

### L2 — 运镜语言
每一拍必须包含运镜指令。常用：Slow Dolly In, Push In, Pull Out, Arc Shot, Whip Pan, Handheld Shake, Speed Ramp, Rack Focus, Crane Shot, Steadicam, Tilt Up/Down, Dutch Angle, Vertigo Shot。
> 更详细的运镜参数、特殊运镜变体和运镜禁忌见 `cinematic-grammar-glossary` §4 镜头字典。

伪透视三公式（根据场景选用）：
- 无限延伸式：走廊/大殿 → Wide-angle 14-24mm + vanishing point
- 巨物压迫式：高墙/庙宇 → Worm's-eye + Scale contrast
- 大气纵深式：竹林/战场 → Multi-layer fog + Foreground occlusion

### L3 — 环境互动
背景必须是活的：光影流转、尘埃浮动、烛火摇曳、落叶翻飞。主体动作必须有环境回应。

### L4 — award-winning-performance-prompt（写实模式主力）

**眼神三要素**（每个镜头必须）：
- 瞳孔反应：微缩（警觉）/ 放大（震惊）/ 微眯（算计）
- 眼球运动：缓移 / 急速侧扫 / 下垂后骤然上挑
- 眼周肌肉：眼轮匝肌轻颤（压抑）/ 皱眉肌收紧（愤怒）

**微表情**（禁止空泛如"面无表情"）：
- 嘴唇：嘴角单侧微勾=轻蔑；下唇轻咬后松开=犹豫
- 鼻翼：翕张=压抑怒火；轻皱=厌恶
- 下颌：咬肌鼓起后松开=吞咽愤怒；微抬=傲慢
- 颈部：肌腱绷紧=紧张；喉结滚动=吞咽

**FACS 情绪速查**（简化版，不用百分比，用强度词）：
| 情绪 | 核心肌肉动作 |
|------|------------|
| 喜悦 | 颧大肌强收+眼轮匝肌收缩出鱼尾纹 |
| 悲伤 | 嘴角下拉+皱眉+眼睑松弛 |
| 愤怒 | 皱眉强收+眼睑紧绷+咬肌隆起 |
| 恐惧 | 额肌上提+瞳孔放大+眼白暴露增大 |
| 惊讶 | 额肌全提+嘴张开+眼睑上提 |
| 厌恶 | 鼻翼上提+嘴角下压+皱眉 |

**肢体去同质化**：每个角色必须有独属身体语言签名。

### L5 — 物理真实（武戏必须，文戏酌情）

**动力链**：力从脚→腿→髋→核心→肩→臂→末端传递。
- ❌ `她挥剑劈下`
- ✅ `rear foot digs into stone, torque spiraling through hip into core, shoulder snapping forward, forearm pronating to angle the edge`

**碰撞物理**：冲击瞬间（共振/冲击波）+ 反作用力（弹开角度/重心补偿）+ 材质响应（火星/裂纹）

**重力原理**：起跳蓄力 → 滞空抛物线 → 落地三关节缓冲

**服装物理**：衣袍飘动=风向+身体运动矢量叠加；急停时惯性前甩回落；饰品摆动频率与头部运动相位差

**皮肤与体液**（按需）：
- 汗液：珠状→条状→片状湿润
- 泪液：沿鼻翼或脸颊固定路径
- 寒冷：呼出白雾+鸡皮疙瘩+末梢苍白

### L6 — 动画物理（动画模式主力）

**预期动作**：每个主要动作前必须有反向预备。
- 大动作 → 深蹲/后收/蓄力，占主动作1/2时间
- 中动作 → 重心后移/手臂预摆，占1/3时间
- 小动作 → 吸气/嘴唇微张/眉毛先扬

**挤压拉伸**：运动物体写入形变，体积守恒。
- 软体 → 大变形（宽度+30%）
- 肌肉 → 中变形
- 刚体 → 微/不变形
- 衣物/头发 → 跟随延迟 0.1-0.3s

**慢入慢出**：所有运动起止有加速减速，禁止线性。

**弧线运动**：生物运动沿弧线，禁止直线轨迹。
- 肢体 → 圆形弧线
- 跳跃 → 抛物线
- 扭转 → S形

**跟随与重叠**：不同部分有时间差，禁止同时启停。
- 头发/丝带 → 延迟 0.3-0.5s
- 衣服/披风 → 延迟 0.2-0.4s
- 手臂/手指 → 延迟 0.1-0.2s

**时间控制**：通过速度变化传达重量和情绪。
- 重物 → 运动慢
- 轻物 → 运动快
- 重要瞬间 → speed ramp 或 beat of stillness

### L7 — 次要动作与反呆板

在主动作之外添加性格化小动作（呼吸起伏、眨眼、重心微移、手指小动作）。

**反 AI 呆板对冲**：
- 静止 → 呼吸+重心微移+无意识手指动作
- 对话 → 倾听方眉毛微动/嘴角变化/身体前倾
- 情绪转折 → 眼神先变→嘴唇抿紧→整脸转变（0.5-1s渐变）
- 群演 → 每人独立微动作

### L8 — 夸张与风格

按风格模式选择性夸张：
- 写实 → 轻微夸张（比现实强 10-20%），仅夸张最关键动作
- 卡通 → 中等夸张（50-100%），表情和动作都放大
- 喜剧 → 极端夸张，允许物理违规

只夸张最重要的1-2个元素，其余正常。

---

## STEP 3: OUTPUT FORMAT

严格按时间码格式输出：

```
(00-1.5s): [Camera: 运镜] + [Light: 光影] + [Body: 起势+动力链] + [Face: 微表情+眼神] + [Physics: 衣物/发丝/环境] + [Animation: 预期/缓动（如适用）]

(1.5-3.0s): [Camera: 运镜变化] + [Body: 动态发展+重心] + [Face: 情绪渐变] + [Interaction: 角色间/碰撞] + [Animation: 挤压拉伸/弧线/时间控制]

(3.0-4.0s): [Camera: 冲击运镜] + [Body: 动作高潮+全链路] + [Face: 情绪爆发+瞳孔] + [Physics: 碰撞+冲击波+材质]

(4.0-5.0s): [Camera: 收尾] + [Body: 惯性/回落] + [Face: 余韵微表情] + [Animation: 跟随余韵+缓出+settle] + [Environment: 环境余韵]
```

**提示词语言**：全部使用**英文**输出。专有名词保留拼音。

### 多参考素材标记（Seedance 2.0 @语法）
```
【@素材1】为首帧画面参考
【@素材2】参考运镜/人物情绪演绎
角色映射（多角色1:1）：参考@图1@图2中的[角色A]，@图3@图4中的[角色B]
```

---

## STEP 4: SELF-CHECK

生成后逐项检查：

- [ ] 没有抽象情绪词（"悲伤""愤怒"→换成具体肌肉/运动描述）
- [ ] 所有动作标注持续时间
- [ ] 物理效果符合牛顿运动定律
- [ ] 优先级正确（表情>眼神>呼吸>动作>物理>环境）
- [ ] 只描述最重要的 3-5 个细节（不过载）
- [ ] 是否有线性运动？→ 加慢入慢出
- [ ] 是否缺少预备动作？→ 加反向预期
- [ ] 所有部分是否同时启停？→ 加跟随重叠时间差
- [ ] 静止角色是否僵硬？→ 加呼吸+重心微移
- [ ] 表情/眼神/呼吸/动作属于同一情绪状态

---

## STEP 5: PRESENT & ITERATE

直接输出提示词。不加开场白/结束语。用户可直接复制到 Seedance 2.0。

如果需要调整，重新生成完整提示词（时间码和情绪弧线是整体设计）。

加载详细参考：
- 想要更精确的 FACS 参数 → `references/face-expression-quick-ref.md`
- 想要更丰富的动画法则细节 → `references/animation-principles-detail.md`

---

## 武器与战斗效果词表 — Combat Effects Vocabulary

武戏模式下涉及枪械/爆炸/冷兵器时，使用以下标准化描述词表。
禁止写"开枪了"这种抽象描述——必须拆解为可见的物理效果。

### 枪械射击效果

| 效果 | 标准描述（英文 prompt 用） | 备注 |
|------|--------------------------|------|
| 枪口焰 | `bright orange muzzle flash bursting from barrel tip` | 夜景加 `illuminating shooter's face` |
| 硝烟 | `wispy grey-white gun smoke drifting from ejection port` | 连射加 `thick haze of cordite smoke` |
| 抛壳 | `brass casing ejecting upward at 45°, spinning, catching light` | 加 `motion blur on the casing` |
| 地面弹壳 | `scattered brass shell casings on the ground/sandbags` | |
| 后坐力 | `shoulder absorbing sharp recoil, muzzle kicking upward 5°` | |
| 弹道效果 | `tracer round streaking as thin orange line` | 夜景/远景用 |

### 爆炸效果

| 效果 | 标准描述 |
|------|---------|
| 近距离 | `fireball expanding outward, shockwave rippling dust from ground` |
| 远景 | `column of dark smoke rising, debris silhouetted against flash` |
| 碎片 | `chunks of earth/concrete/wood flying outward in parabolic arcs` |

### 冷兵器效果

| 效果 | 标准描述 |
|------|---------|
| 刺刀反光 | `bayonet blade catching cold light, steel glint` |
| 挥刀轨迹 | `curved motion blur following blade arc` |
| 军刀出鞘 | `blade sliding from scabbard with metallic gleam` |
