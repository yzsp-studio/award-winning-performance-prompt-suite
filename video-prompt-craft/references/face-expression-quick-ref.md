# FACS 面部表情速查参考

## 核心面部肌肉（AI可控级别）

| 肌肉 | 位置 | 动作 |
|------|------|------|
| 额肌 | 前额 | 抬眉（惊讶/恐惧） |
| 皱眉肌 | 眉间 | 压眉皱眉（愤怒/困惑） |
| 眼轮匝肌-眶部 | 眼周外圈 | 挤压出鱼尾纹（真笑） |
| 眼轮匝肌-睑部 | 眼皮 | 眯眼（悲伤/强光） |
| 颧大肌 | 脸颊 | 拉嘴角上扬（微笑） |
| 降口角肌 | 嘴角下方 | 拉嘴角下坠（悲伤） |
| 提上唇鼻翼肌 | 鼻翼 | 翻鼻翼（厌恶） |
| 咬肌 | 下颌侧 | 咬紧牙关（愤怒/隐忍） |
| 颈阔肌 | 颈前 | 拉颈部绷紧（极度用力/恐惧） |

## 六大基本情绪 → AI 提示词模板

| 情绪 | 提示词描述（英文） |
|------|----------------|
| 喜悦 | `cheeks lifted high, genuine crow's-feet wrinkles at eye corners, mouth corners pulled wide` |
| 悲伤 | `mouth corners drooping, brows knitted upward at inner ends, lower eyelids slack` |
| 愤怒 | `brows drawn down and together, upper lids tense and narrowed, jaw muscles bulging` |
| 恐惧 | `forehead wrinkles horizontal, eyes wide with increased sclera, mouth slightly open` |
| 惊讶 | `entire forehead raised, eyes wide and round, jaw dropping open` |
| 厌恶 | `nose wrinkled upward, upper lip raised exposing teeth, mouth corners pulled down` |

## 微表情（0.04-0.2s闪过）

- **真笑 vs 假笑**：真笑=眼角鱼尾纹参与；假笑=仅嘴角上扬，眼周无变化
- **轻蔑**：单侧嘴角微翘0.1s后恢复
- **说谎泄露**：真实情绪在0.04s内闪过，随即被控制表情覆盖

## 眼神参数速查

| 参数 | 情绪映射 |
|------|---------|
| 瞳孔放大 | 兴趣/恐惧/震惊 |
| 瞳孔收缩 | 厌恶/愤怒/强光 |
| 眼白增大 | 恐惧/惊讶 |
| 眨眼加速 | 焦虑/说谎 |
| 眨眼减少 | 专注/威胁凝视 |
| 缓慢扫视 | 思考/评估 |
| 急速侧扫 | 警觉/寻找出路 |
| 向下看 | 悲伤/羞耻/服从 |

## 呼吸模式速查

| 模式 | 特征 | 情绪 |
|------|------|------|
| 腹式深呼吸 | 腹部起伏，肩不动 | 平静/深沉悲伤 |
| 胸式浅呼吸 | 胸部起伏，肩微动 | 紧张/兴奋 |
| 锁骨式极浅 | 肩膀上提 | 恐惧/焦虑/濒死 |
| 屏息 | 完全停止 | 惊讶/蓄力 |
