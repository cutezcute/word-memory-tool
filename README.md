# AFRO Word Memory Tool (Spaced Repetition Spelling Practice)

===========================================================

A **purely local, zero-dependency**​ English vocabulary web app AFRO. Two learners can each use different wordbanks, with reviews scheduled along the Ebbinghaus forgetting curve, focusing on **spelling**​ (first letter as hint; tense/ending inferred by the learner). Learner names can be customized in `Settings → Learner Name`.

> The home page shows only a `Daily Overview + Start Button` for a clean look; detailed practice modes and PRD notes are all in this README.

How to Open

-----------

- Simply **double-click `index.html`**​ to open it in your browser (Chrome / Edge / Safari all work).

- No internet connection or installation required.

Feature-to-PRD Mapping

----------------------

1. **Two Learners + Separate Wordbanks**: Switch between `Learner 1 / Learner 2` and `KET/PET Core / TOEFL Core` at the top; progress is tracked independently. Learner 1 uses a yellow theme. Learner names can be changed in `Settings → Learner Name`.

2. **Not Just Recognition — Spelling Required**​ (auto-advances with proficiency):
- **Chinese meaning displayed above**​ to ensure comprehension; **English word partially or fully cloze-tested below**​ for spelling practice.

- **Partial cloze**: Target word shows the first letter(s) as hints; complete the spelling (tense/ending inferred by learner); the more proficient, the more letters are hidden.

- **Full cloze**: Entire target word hidden; spell the full word from the Chinese meaning.

- Words progress from `partial cloze → full cloze`. After submission: **full English word (highlighted) + POS + definition + related word forms**​ (verb: past/past participle/present participle/3rd person singular; noun: singular/plural; adjective: comparative/superlative/adverb, etc.), with 🔊 **text-to-speech**. Auto-pronunciation plays after submission.

- Shortcuts: `Space` = start/next word; `Enter` = submit (or next word after revealing answer); `⌘/Ctrl + H` = hint.
3. **Ebbinghaus Forgetting Curve**: Daily new words (default 25, adjustable 20–30) + review words, total default 45 (adjustable 40–50), estimated 20–30 min per session. Correct answers advance to next review interval (1/2/4/7/15/30 days); mistakes return sooner. **No repeats within the same day.**

4. **Clean, Kid-Friendly Color Scheme**: Rounded cards + bright colors; KET uses orange/blue, TOEFL uses purple/green; **Learner 1 is fixed to a yellow theme**.

5. **Mining Reward System (inspired by "Math with Ore")**: Every correct answer "mines" an ore. Rules — correct = mine ⛏️; longer streaks yield rarer ores (3/5/8/12 consecutive correct answers grant Iron/Gold/Redstone/Lapis Lazuli respectively); correct with hint = Stone; correct after retry = Copper; correct without hint on hard words (★★★) = 💎 Diamond; full session perfect = 🟢 Emerald; cumulative 100/300 correct answers = 🟣 Netherite / 🗼 Beacon; 7-day consecutive practice = 🛡️ Totem of Undying. All ores are **permanent collectibles, never deducted**. Session end triggers **confetti + trophy animation**​ and displays ores earned; click `🎁 My Warehouse` to view the full ore gallery and cumulative counts, also shown on the `Stats` page.

6. **Mistake Notebook (Wrong-Word Bank)**: Incorrect words auto-save to the `Mistake Notebook` (isolated by learner + wordbank). Click `Mistake Notebook` at the top to view all wrong words, error counts, and timestamps; click `Review These Mistakes` for targeted practice; a word is **auto-removed once answered correctly once**. Updates after each daily session.

7. **Portable**: Zip the entire folder and send to others; double-click to use. Wordbanks can be swapped anytime.

> 📚 **KET/PET Wordbank Source**: `data/ket.js` merges the **Cambridge KET for Schools Official Wordlist**​ and **B1 Preliminary (PET) Official Wordlist**​ (two PDFs), deduplicated to ~3,100 words. Chinese definitions from ECDICT + manual supplementation. To use your own, see `How to Replace Wordbank` below.

> 🗂️ **TOEFL Wordbank Source**: `data/toefl.js` is a merged, deduplicated **TOEFL high-frequency wordlist (~6,679 words including phrases)**​ from Wu Laoshi 1500 / PrepScholar / TOEFL Complete Wordlist. This list contains only `English + Chinese definition` with no example sentences, so TOEFL practice uses `Chinese meaning + standalone cloze word` mode (no sentence embedding).

> 🔊 **About Text-to-Speech**: Pronunciation uses the browser's built-in speech synthesis (offline, no internet needed). Voice quality depends on **English voices installed on your system**: macOS includes natural voices like Samantha; on Windows, install and select "Microsoft Aria / David" in `Settings → Time & Language → Speech` for better results. If unsupported, a prompt will appear.

How to Replace Wordbank

-----------------------

Two methods, choose one:

**Method A: In-Page Upload (local only, most convenient)**

- Go to `Wordbank` page → click upload → supports **`.txt / .csv / .json / .js`**​ formats.

- Text format (one per line, comma or tab separated):

  ```
  apple,苹果
  apple,苹果,I eat an apple every day.
  ```

- JSON format:

  ```json
  [{"en":"apple","zh":"苹果","sentence":"I eat an apple every day."}]
  ```

- **.js format (both recognized)**:

  - This tool's format: `window.WORDBANKS.toefl = { words:[{en:"apple", zh:"苹果", pos:"n.", sentence:"..."}] }`

  - Third-party format (auto-converts to en/zh, attempts POS inference from definition): `const TOEFL_WORDS = [{word:"abandon", meaning:"vt. abandon; give up"}]`

  - Upload only overrides the default wordbank for the current `Learner + Wordbank` combination; click `Restore Default Wordbank` to undo.

**Method B: Edit Default File (permanent replacement, good for sharing)**

- Edit the `words` array in `data/ket.js` or `data/toefl.js` following the same field structure.

- Save and reopen `index.html` to apply changes.

Progress Backup / Device Migration

----------------------------------

- Progress is stored locally in your browser. Before switching computers or clearing cache, go to `Settings → Progress Backup` to **export progress**​ (JSON), then **import**​ on the new device.

- You can also export uploaded wordbanks from the `Wordbank` page.

File Structure

--------------

```
word-memory-tool/
├─ index.html        # Entry point
├─ style.css         # Styles (kid-friendly color scheme)
├─ app.js            # All logic (scheduling / spelling / progress)
├─ data/
│  ├─ ket.js         # KET/PET default wordbank (editable)
│  └─ toefl.js       # TOEFL default wordbank (editable)
└─ README.md
```

Tips

----

- In Settings, adjust `New Word Count / Daily Total / Seconds per Word`, and whether to cloze-test within English sentences.

- When a child is tired, doing fewer words is fine — the system auto-defers unfinished words without data loss.

#

# AFRO 背单词小工具（艾宾浩斯拼写练习）

一个**纯本地、零依赖**的英语背单词网页工具 AFRO。两个学习者可分别用不同词库，按遗忘曲线安排复习，重点练**会写**（首字母作提示，时态/词尾自己判断）。学习者名字可在「设置 → 学习者名字」里自行填入。

> 首页只放「今日概览 + 开始按钮」，保持干净；详细的练习模式与 PRD 说明都在这份 README 里。

## 怎么打开

- 直接**双击 `index.html`** 用浏览器打开即可（Chrome / Edge / Safari 均可）。
- 不需要联网、不需要安装任何东西。

## 功能对照 PRD

1. **两个学习者 + 不同词库**：顶部切换「学习者 1 / 学习者 2」和「KET/PET 高频 / TOEFL 高频」，进度各自独立。学习者 1 的界面为黄色主题。学习者名字可在「设置 → 学习者名字」里修改。
2. **不仅认识，还要会写**（随熟练度自动进阶）：
   - **上方显示中文意思**，让孩子先读懂意思；**下方是英文单词，部分或全挖空**，在挖空里练拼写。
   - **部分挖空**：目标词显示首字母等几个字母作提示，补全并写出整词（时态/词尾自己判断）；越熟练挖得越多。
   - **全挖空**：目标词整词挖空，读中文把完整单词拼写出来。
   - 单词按"部分挖空 → 全挖空"进阶。提交后展示**完整英文单词（高亮）+ 词性 + 词义 + 相关词形（动词的过去式/过去分词/现在分词/三单；名词单复数；形容词比较级/最高级/副词等）**，并可点 🔊 **听读音**，提交后还会**自动朗读**该词。
   - 快捷键：空格 = 开始/下一词，回车 = 提交（看答案后 = 下一词），⌘/Ctrl + H = 提示。
3. **艾宾浩斯遗忘曲线**：每天新词（默认 25，可调 20–30）+ 复习旧词，总量默认 45（可调 40–50），预计 20–30 分钟。做对进下一复习档（1天/2天/4天/7天/15天/30天），做错很快重练；**当天练过的不再重复**。
4. **简洁、孩子喜欢的配色**：圆角卡片 + 明亮色调；KET 用橙蓝、TOEFL 用紫绿区分，**学习者 1 固定黄色主题**。
5. **矿石挖矿 + 庆祝（仿"矿石数学"）**：每答对一题就"挖矿"。规则——做对就挖矿⛏️；连对越多矿越稀有（连对 3/5/8/12 题分别得 铁矿石/金矿石/红石/青金石）；用了提示答对得「石头」、错题重做答对得「铜矿石」、不用提示解出难题（★★★）得「💎 钻石」；一节全对得「🟢 绿宝石」；累计做对 100/300 题得「🟣 下界合金 / 🗼 信标」；连续 7 天练习得「🛡️ 不死图腾」。所有矿石**只增不减**，是收藏成就不是货币。结束页播放**彩带 + 奖杯庆祝动画**并展示本次挖到的矿石；点「🎁 我的仓库」可看完整矿石图鉴与累计数量，累计数也会显示在「统计」页。
6. **复习本（错词本）**：答错过的词会自动收进「复习本」（按 学习者 + 词库 隔离）。点顶部「复习本」可看到所有错词、答错次数与最近时间；点「开始复习这些错词」单独复习；某词**答对一次即视为学会，自动移出复习本**。每天练完滚动更新。
7. **可打包发送**：整个文件夹压缩发给别人，对方双击即用，词库可随时替换。

> 📚 **KET/PET 词库来源**：`data/ket.js` 已合并**剑桥 KET for Schools 官方词汇表**与 **B1 Preliminary（PET）官方词汇表**两份 PDF，去重后约 3100 词，中文释义来自 ECDICT 词典 + 人工补译。如需换成你自己的词，见下方「怎么换词库」。

> 🗂️ **TOEFL 词库来源**：`data/toefl.js` 为合并去重的 **托福高频词表（约 6679 词，含短语）**，来源：无老师1500 / PrepScholar / TOEFL单词完整版。该表只有「英文 + 中文释义」，没有例句，所以 TOEFL 练习走"中文意思 + 单独挖空词"模式（不嵌句子）。

> 🔊 **关于听读音**：朗读用的是浏览器内置语音合成（离线、无需联网）。发音是否自然取决于**你电脑里装了哪种英文语音**：Mac 自带 Samantha 等自然嗓音；Windows 建议在「设置 → 时间和语言 → 语音」里安装并选择 "Microsoft Aria / David" 等英文语音，体验更自然。若浏览器完全不支持，会弹出提示。

## 怎么换词库

两种方式，任选其一：

**方式 A：页面内上传（仅本机生效，最方便）**

- 进入「词库」页 → 点上传 → 支持 **`.txt / .csv / .json / .js`** 四种格式。

- 文本格式（每行一个，逗号或制表符分隔）：

  ```
  apple,苹果
  apple,苹果,I eat an apple every day.
  ```

- JSON 格式：

  ```json
  [{"en":"apple","zh":"苹果","sentence":"I eat an apple every day."}]
  ```

- **.js 格式（两种都认）**：

  - 本工具格式：`window.WORDBANKS.toefl = { words:[{en:"apple", zh:"苹果", pos:"n.", sentence:"..."}] }`
  - 第三方格式（自动转成 en/zh，并尝试从释义推断词性）：`const TOEFL_WORDS = [{word:"abandon", meaning:"vt.抛弃;放弃"}]`
  - 上传后仅覆盖当前「学习者 + 词库」组合的默认词库；可点「恢复默认词库」撤销。

**方式 B：改默认文件（永久替换，适合发给别人）**

- 编辑 `data/ket.js` 或 `data/toefl.js` 里的 `words` 数组，按上面同样的字段。
- 改完保存，重新打开 `index.html` 即生效。

## 进度备份 / 换设备

- 进度只存在本机浏览器。换电脑或清缓存前，去「设置 → 进度备份」**导出进度**（JSON），到新环境再**导入**。
- 也可在「词库」页把上传的词库一并导出带走。

## 文件结构

```
word-memory-tool/
├─ index.html        # 入口
├─ style.css         # 样式（孩子友好配色）
├─ app.js            # 全部逻辑（计划/排期/拼写/进度）
├─ data/
│  ├─ ket.js         # KET/PET 默认词库（可改）
│  └─ toefl.js       # TOEFL 默认词库（可改）
└─ README.md
```

## 小贴士

- 设置里可调整「新词数量 / 每天总量 / 每词秒数」，以及是否在英文句子里挖空练拼写。
- 孩子累的时候，少练几个也没关系——系统会自动把没练的顺延，不会丢失。
