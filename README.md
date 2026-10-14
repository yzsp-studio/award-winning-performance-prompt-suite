<div align="center">

# 🎬 award-winning-performance-prompt-suite

## 2 个技能写好视频提示词：先判场景，再躲开翻车点
## Two skills for video prompts: analyze the scene, then dodge the failures

> ⚠️ **这是一套配合使用的技能组合（2 个）** —— 正文互相引用，建议成套取用。

📮 **商务合作 / Business：wow.vip@foxmail.com**
🎬 **抖音 / Douyin：[v.douyin.com/07EjIDGVErY](https://v.douyin.com/07EjIDGVErY/)**

</div>

---

## 🇨🇳 中文

由 2 个技能组成的视频提示词工艺套件，把怎么把画面写对拆成可执行的步骤。award-winning-performance-prompt 从输入检查开始，逐层分析场景：判断场景分类、识别环境与角色、按时长映射出需要的片段数，再把各要素组织成提示词。video-prompt-craft 补上工艺纪律：先读铁律（违反任何一条即视为废 prompt），再对照生产中常见翻车的反模式逐条自查，然后做风格模式判定与场景分类，最后才进入 STEP 0 与 STEP 1 的分析流程。两个技能配合使用：一个负责把画面分析清楚，一个负责保证提示词不踩坑，适合在正式生成前当作自检关口，避免成片与预期不符。

> ⚠️ **这是一套配合使用的技能组合（2 个）** —— 正文互相引用，建议成套取用。

### ✨ 能做什么

- 输入检查：STEP 0 先校验素材，缺输入就补齐再往下走
- 场景分析：场景分类、环境识别、角色识别三步锁定画面要素
- 时长映射：按时长推算需要几个片段，避免一条提示词硬塞整段剧情
- 铁律清单：生成前必读，违反任何一条即判定为废 prompt
- 反模式自查：对照生产中常见翻车点逐条排查，提前排雷
- 风格模式判定：先定风格模式与场景分类，再进入逐层分析流程

### 📦 包含的技能（配合使用）

- `award-winning-performance-prompt` —— 见 [`award-winning-performance-prompt/SKILL.md`](award-winning-performance-prompt/SKILL.md)
- `video-prompt-craft` —— 见 [`video-prompt-craft/SKILL.md`](video-prompt-craft/SKILL.md)

### 🚀 安装

```bash
git clone https://github.com/yzsp-studio/award-winning-performance-prompt-suite.git
cp -r award-winning-performance-prompt-suite/* "$DSH_HOME/skills/"
```

> 技能是**纯文本说明**（`SKILL.md` + `references/`），零依赖、零 API key，用你当前 agent 的会话额度。

---

## 🇬🇧 English

Two skills for the craft of video prompting that break writing the right shot into executable steps. award-winning-performance-prompt begins with an input check and analyzes the scene layer by layer: classify the scene, identify environment and characters, map duration to the number of segments, then assemble the elements into a prompt. video-prompt-craft adds the discipline: read the iron rules first (breaking any one voids the prompt), self-check against the anti-patterns that commonly derail production, decide the style mode and scene classification, and only then enter the STEP 0 / STEP 1 analysis flow. Used together, one makes the scene analysis explicit and the other keeps the prompt out of known failure modes, which makes them a useful self-check gate before you spend a generation.

> ⚠️ **A cooperating suite of 2 skills** — they reference each other; use them as a group.

### ✨ What it does

- Input check: STEP 0 validates the source material and fills gaps before moving on
- Scene analysis: scene classification, environment recognition and character recognition lock down the visual elements
- Duration mapping: derive how many segments a duration needs instead of cramming one prompt
- Iron rules: a must-read before generation, where breaking any single rule voids the prompt
- Anti-pattern self-check: walk through the failure modes common in production and defuse them early
- Style mode decision: fix style mode and scene classification before the layered analysis flow

### 📦 Skills included (designed to work together)

- `award-winning-performance-prompt` — [`award-winning-performance-prompt/SKILL.md`](award-winning-performance-prompt/SKILL.md)
- `video-prompt-craft` — [`video-prompt-craft/SKILL.md`](video-prompt-craft/SKILL.md)

### 🚀 Install

```bash
git clone https://github.com/yzsp-studio/award-winning-performance-prompt-suite.git
cp -r award-winning-performance-prompt-suite/* "$DSH_HOME/skills/"
```

> Skills are **plain-text instructions** (`SKILL.md` + `references/`). Zero dependencies, no API keys — they run on your agent's existing session quota.

---

## 📮 联系 / Contact

| | |
|---|---|
| 🎬 **抖音 / Douyin** | [https://v.douyin.com/07EjIDGVErY/](https://v.douyin.com/07EjIDGVErY/) |
| 📮 **商务合作 / Business** | **wow.vip@foxmail.com** |
| 🐙 **GitHub** | [https://github.com/yzsp-ai](https://github.com/yzsp-ai) |
| 💖 **打赏 / Support** | [afdian.com/a/yzsp-ai](https://afdian.com/a/yzsp-ai) |

## 📄 License

[MIT](LICENSE) · © 2026 [yzsp-ai](https://github.com/yzsp-ai)
