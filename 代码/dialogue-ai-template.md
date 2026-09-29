# 对话区 · AI 聊天输出版模板

给 AI 用的生成模板：AI 按下面的结构输出 HTML，贴进允许 HTML+CSS 的聊天/网页即可显示。

特性：零 JS、点击画面推进、说话方立绘自动高亮（另一方变暗下沉）、末句延迟出现「重新开始」按钮。

> 前提：目标环境必须会渲染 `style` 标签与 HTML。若平台会过滤 style（部分聊天站会），这套组件无法显示，属于平台限制。

---

## 零、AI 输出规则（优先遵守）

1. **整块只有一个 div**，而且 **`<style>` 写在 div 里面**（作为 div 的第一个子元素）。
   不要把样式放到 div 外面，也不要拆成「样式块 + 结构块」两段输出。
   正确形状：

   ```
   <div class="dg">
   <style> ……全部样式…… </style>
   ……结构……
   </div>
   ```

2. **只输出代码，不输出说明**。不要输出本文件里的说明、标题、表格，也不要写「下面是为您生成的对话」「希望对你有帮助」这类话。
   确实需要解释时，把解释写在代码块**外面**的正文里，不要写进 div。
3. **div 内部不写 HTML 注释**，只放 `<style>` 和结构。
4. **每段自带一份样式**：一段对话 = 一个自带 `<style>` 的 div，单独发一条消息也能显示，不依赖前面的消息。
5. **命名必须带编号，且全页唯一**（最容易出错的一条）：
   - 第 N 段的 radio：`name="dgN"` —— 第 1 段 `dg1`、第 2 段 `dg2`、第 3 段 `dg3`……
   - 该段第 M 步的元素 id：`dgN-M` —— 第 1 段三步分别是 `dg1-1`、`dg1-2`、`dg1-3`
   - `label` 的 `for` 必须指向同段内真实存在的 id
   - **同一页里绝不允许出现两个相同的 `name`、或两个相同的 `id`**。重复会让几段对话互相抢占状态（点这一段，那一段跟着跳）。
   - 每次生成新一段，编号接着往下排，不要重复用 `dg1`。
6. **占位符必须替换**：`【背景链接】`、`【角色立绘链接】`、`【玩家立绘链接】`、`【台词】` 要换成真实内容，不能原样留在输出里。
7. 不要输出 `<html>`、`<head>`、`<body>`，只要那一个 div。

---

## 一、素材外链对照表

**前缀**（二选一，推荐 jsDelivr，国内较快）

```
jsDelivr : https://cdn.jsdelivr.net/gh/karina-zzya/AI-assets@main/
GitHub   : https://raw.githubusercontent.com/karina-zzya/AI-assets/main/
```

**背景（场景）** — 目录 `邻家大姐姐/` — 1536×1024（3:2）

| 文件名 | jsDelivr 链接 |
| --- | --- |
| 出租房-晚上.png | https://cdn.jsdelivr.net/gh/karina-zzya/AI-assets@main/邻家大姐姐/出租房-晚上.png |
| 出租房-白天.png | https://cdn.jsdelivr.net/gh/karina-zzya/AI-assets@main/邻家大姐姐/出租房-白天.png |
| 大学校园-晚上.png | https://cdn.jsdelivr.net/gh/karina-zzya/AI-assets@main/邻家大姐姐/大学校园-晚上.png |
| 大学校园-白天.png | https://cdn.jsdelivr.net/gh/karina-zzya/AI-assets@main/邻家大姐姐/大学校园-白天.png |
| 商场-晚上.png | https://cdn.jsdelivr.net/gh/karina-zzya/AI-assets@main/邻家大姐姐/商场-晚上.png |
| 商场-白天.png | https://cdn.jsdelivr.net/gh/karina-zzya/AI-assets@main/邻家大姐姐/商场-白天.png |
| 菜市场-晚上.png | https://cdn.jsdelivr.net/gh/karina-zzya/AI-assets@main/邻家大姐姐/菜市场-晚上.png |
| 菜市场-白天.png | https://cdn.jsdelivr.net/gh/karina-zzya/AI-assets@main/邻家大姐姐/菜市场-白天.png |
| 沙滩-晚上.png | https://cdn.jsdelivr.net/gh/karina-zzya/AI-assets@main/邻家大姐姐/沙滩-晚上.png |
| 沙滩-白天.png | https://cdn.jsdelivr.net/gh/karina-zzya/AI-assets@main/邻家大姐姐/沙滩-白天.png |
| 沙滩步道-白天.png | https://cdn.jsdelivr.net/gh/karina-zzya/AI-assets@main/邻家大姐姐/沙滩步道-白天.png |
| 海边步道-晚上.png | https://cdn.jsdelivr.net/gh/karina-zzya/AI-assets@main/邻家大姐姐/海边步道-晚上.png |

**角色立绘（李云舒）** — 目录 `邻家大姐姐/` — 1024×1536（2:3）

| 文件名 | jsDelivr 链接 |
| --- | --- |
| 待机.png | https://cdn.jsdelivr.net/gh/karina-zzya/AI-assets@main/邻家大姐姐/待机.png |
| 微笑.png | https://cdn.jsdelivr.net/gh/karina-zzya/AI-assets@main/邻家大姐姐/微笑.png |
| 害羞.png | https://cdn.jsdelivr.net/gh/karina-zzya/AI-assets@main/邻家大姐姐/害羞.png |
| 生气.png | https://cdn.jsdelivr.net/gh/karina-zzya/AI-assets@main/邻家大姐姐/生气.png |
| 难过.png | https://cdn.jsdelivr.net/gh/karina-zzya/AI-assets@main/邻家大姐姐/难过.png |
| 流泪.png | https://cdn.jsdelivr.net/gh/karina-zzya/AI-assets@main/邻家大姐姐/流泪.png |
| 开心挥手.png | https://cdn.jsdelivr.net/gh/karina-zzya/AI-assets@main/邻家大姐姐/开心挥手.png |
| 无奈.png | https://cdn.jsdelivr.net/gh/karina-zzya/AI-assets@main/邻家大姐姐/无奈.png |
| 苦笑.png | https://cdn.jsdelivr.net/gh/karina-zzya/AI-assets@main/邻家大姐姐/苦笑.png |
| 喂饭.png | https://cdn.jsdelivr.net/gh/karina-zzya/AI-assets@main/邻家大姐姐/喂饭.png |
| 背手回眸.png | https://cdn.jsdelivr.net/gh/karina-zzya/AI-assets@main/邻家大姐姐/背手回眸.png |
| 狡黠.png | https://cdn.jsdelivr.net/gh/karina-zzya/AI-assets@main/邻家大姐姐/狡黠.png |

**玩家立绘** — 目录 `邻家大姐姐/` — 1024×1536（2:3）

| 文件名 | jsDelivr 链接 |
| --- | --- |
| 玩家-待机立绘.png | https://cdn.jsdelivr.net/gh/karina-zzya/AI-assets@main/邻家大姐姐/玩家-待机立绘.png |

---

## 二、模板代码

下面**一整个代码块就是一个 div**，`<style>` 在 div 内部最前面。第 1 段编号为 `dg1`；再生成一段就整体改成 `dg2`（`name="dg2"`、id 为 `dg2-1`、`dg2-2`…）。

```html
<div class="dg">
<style>
.dg{position:relative;width:100%;padding-top:150%;overflow:hidden;background:#0b1220;isolation:isolate;font-family:system-ui,"Microsoft YaHei",sans-serif;font-size:clamp(12px,3.6vw,17px);line-height:1.7;color:#eaf1ff}
.dg *{box-sizing:border-box}
.dg-s{position:absolute;bottom:0;left:0;width:1px;height:1px;opacity:0;pointer-events:none}
.dg-step{position:absolute;top:0;right:0;bottom:0;left:0;display:none}
.dg-s:checked+.dg-step{display:block}
.dg-bg{position:absolute;top:0;left:0;width:100%;height:100%;object-fit:cover}
.dg-role,.dg-player{position:absolute;bottom:26.5%;width:52.3%;height:52.3%;object-fit:contain;object-position:bottom center;opacity:.34;filter:grayscale(.65) brightness(.7);transform:translateY(11.6%) scale(.94);transition:.45s ease}
.dg-role{left:-2.3%}
.dg-player{right:-2.3%}
.dg-speak-role .dg-role,.dg-speak-player .dg-player{opacity:1;filter:none;transform:translateY(-5.2%) scale(1);z-index:2}
.dg-box{position:absolute;left:4.5%;bottom:3%;width:91%;height:27.3%;padding:3.2% 4.1% 6.4%;border:1px solid rgba(124,199,255,.34);border-radius:12px;background:rgba(6,10,22,.82);overflow:hidden;z-index:3}
.dg-name{display:inline-block;margin-bottom:.5em;padding:.1em .8em;border-radius:999px;font-size:.92em;font-weight:700;color:#04121f;background:linear-gradient(135deg,#7cc7ff,#cdeaff)}
.dg-speak-player .dg-name{background:linear-gradient(135deg,#ff9ad5,#ffd3ee)}
.dg-text{margin:0;font-size:1em;line-height:1.7;text-shadow:0 2px 8px rgba(0,0,0,.6)}
.dg-hit{position:absolute;top:0;right:0;bottom:0;left:0;z-index:6;cursor:pointer}
.dg-restart{position:absolute;left:50%;bottom:2%;transform:translateX(-50%);z-index:6;padding:.3em 1.2em;border:1px solid rgba(124,199,255,.6);border-radius:999px;background:rgba(14,24,44,.95);color:#eaf1ff;font-size:.82em;font-weight:700;letter-spacing:.1em;white-space:nowrap;cursor:pointer;animation:dg-in .35s ease 1.2s both}
@keyframes dg-in{from{opacity:0;visibility:hidden}to{opacity:1;visibility:visible}}
</style>

  <input class="dg-s" type="radio" name="dg1" id="dg1-1" checked>
  <div class="dg-step dg-speak-role">
    <img class="dg-bg" src="【背景链接】" alt="">
    <img class="dg-role" src="【角色立绘链接】" alt="李云舒">
    <img class="dg-player" src="【玩家立绘链接】" alt="{{user}}">
    <div class="dg-box">
      <b class="dg-name">李云舒</b>
      <p class="dg-text">【台词】</p>
    </div>
    <label class="dg-hit" for="dg1-2" aria-label="继续"></label>
  </div>

  <input class="dg-s" type="radio" name="dg1" id="dg1-2">
  <div class="dg-step dg-speak-player">
    <img class="dg-bg" src="【背景链接】" alt="">
    <img class="dg-role" src="【角色立绘链接】" alt="李云舒">
    <img class="dg-player" src="【玩家立绘链接】" alt="{{user}}">
    <div class="dg-box">
      <b class="dg-name">{{user}}</b>
      <p class="dg-text">【台词】</p>
    </div>
    <label class="dg-hit" for="dg1-3" aria-label="继续"></label>
  </div>

  <input class="dg-s" type="radio" name="dg1" id="dg1-3">
  <div class="dg-step dg-speak-role">
    <img class="dg-bg" src="【背景链接】" alt="">
    <img class="dg-role" src="【角色立绘链接】" alt="李云舒">
    <img class="dg-player" src="【玩家立绘链接】" alt="{{user}}">
    <div class="dg-box">
      <b class="dg-name">李云舒</b>
      <p class="dg-text">【台词】</p>
    </div>
    <label class="dg-restart" for="dg1-1">重新开始</label>
  </div>

</div>
```

---

## 三、多段对话生成说明

一段对话 = 一个自带 `<style>` 的 `<div class="dg">…</div>`。**每段一块，整块复制即用**，不需要额外的样式代码。

1. **编号方案（务必遵守）**：第 N 段 → `name="dgN"`，该段第 M 步的 id → `dgN-M`。
   连续生成三段时应当是这样，三段互不重复：

   | 段 | radio name | 各步 id | 点击层 for |
   | --- | --- | --- | --- |
   | 第 1 段 | `dg1` | `dg1-1` `dg1-2` `dg1-3` | `dg1-2` `dg1-3` / 重开指向 `dg1-1` |
   | 第 2 段 | `dg2` | `dg2-1` `dg2-2` `dg2-3` | `dg2-2` `dg2-3` / 重开指向 `dg2-1` |
   | 第 3 段 | `dg3` | `dg3-1` `dg3-2` `dg3-3` | `dg3-2` `dg3-3` / 重开指向 `dg3-1` |

   ⚠️ 最容易犯的错：两段都用 `dg1`，或者 id 只写 `dg1`/`dg2`（少了「步号」那一段）。这会让几段对话互相抢占状态。
2. **加一步**：复制一组两行结构 —— `<input class="dg-s" …>` 紧挨着 `<div class="dg-step" …>`（顺序不能颠倒，显示逻辑靠相邻选择器 `+`），id 顺延（`dg1-4`、`dg1-5`…）。
3. **每段第一步**要带 `checked`，否则开局是空白。
4. **说话方**：给该步的 `.dg-step` 加 `dg-speak-role`（角色说话，左侧亮）或 `dg-speak-player`（玩家说话，右侧亮）。不加则两边都是暗的。
5. **点击推进**：每步放一个铺满的 `<label class="dg-hit" for="下一步的id">`。
6. **最后一步**：删掉 `dg-hit`，换成 `<label class="dg-restart" for="本段第一步的id">重新开始</label>`，这样点画面不会重开，必须点按钮（按钮进入末步 1.2 秒后淡入）。
7. **段长建议**：每段 3～6 步，一段讲完一个场景，换场景就换一段。
8. **表情差分**：同一步里换 `<img class="dg-role" src="…">` 的链接即可（如「微笑.png」→「害羞.png」），不需要额外结构。

---

## 四、内容填充说明

| 槽位 | 位置 | 怎么写 |
| --- | --- | --- |
| **背景** | `<img class="dg-bg" src="…">` | 用对照表里 `邻家大姐姐/` 的链接，`object-fit:cover` 自动裁满画面。换场景只改这一条；每步可以不同（比如走出门就切成「大学校园-晚上」） |
| **角色立绘** | `<img class="dg-role" src="…">` | 用 `邻家大姐姐/` 的链接，按情绪选（待机 / 微笑 / 害羞 / 生气 / 难过 / 流泪 / 开心挥手 / 无奈 / 苦笑 / 喂饭 / 背手回眸 / 狡黠）。亮暗由说话方自动决定 |
| **玩家立绘** | `<img class="dg-player" src="…">` | 用 `邻家大姐姐/玩家-待机立绘.png`。若不想要主角立绘，整行删掉即可 |
| **说话人** | `<b class="dg-name">` | 角色写「李云舒」，玩家写 `{{user}}`（这两个字符别改，游戏里会自动替换成玩家名）。玩家那句的名牌会自动变成粉色 |
| **台词** | `<p class="dg-text">` | 建议 **不超过 60 字**（框内约 3 行 × 每行 22 字），超出会被裁切。长台词拆成两步 |

台词风格参考（李云舒：温柔克制，把情绪藏在细节里，称呼「我们{{user}}」）：

- 「门一响，我就听见了。……真的是你啊。」
- 「欢迎回家。……好久不见，我们{{user}}。」
- 「我等你好久了。从你说要回来的那天起，就一直在数日子。」
- 「行李先放着，去洗手吧，汤刚炖好——累不累？饿不饿？」

---

## 五、最小可用示例（一个 div 整块复制即可运行）

下面这一整个代码块**就是一个 div**，样式在 div 里面，链接全是真地址，直接贴进页面就能跑。

```html
<div class="dg">
<style>
.dg{position:relative;width:100%;padding-top:150%;overflow:hidden;background:#0b1220;isolation:isolate;font-family:system-ui,"Microsoft YaHei",sans-serif;font-size:clamp(12px,3.6vw,17px);line-height:1.7;color:#eaf1ff}
.dg *{box-sizing:border-box}
.dg-s{position:absolute;bottom:0;left:0;width:1px;height:1px;opacity:0;pointer-events:none}
.dg-step{position:absolute;top:0;right:0;bottom:0;left:0;display:none}
.dg-s:checked+.dg-step{display:block}
.dg-bg{position:absolute;top:0;left:0;width:100%;height:100%;object-fit:cover}
.dg-role,.dg-player{position:absolute;bottom:26.5%;width:52.3%;height:52.3%;object-fit:contain;object-position:bottom center;opacity:.34;filter:grayscale(.65) brightness(.7);transform:translateY(11.6%) scale(.94);transition:.45s ease}
.dg-role{left:-2.3%}
.dg-player{right:-2.3%}
.dg-speak-role .dg-role,.dg-speak-player .dg-player{opacity:1;filter:none;transform:translateY(-5.2%) scale(1);z-index:2}
.dg-box{position:absolute;left:4.5%;bottom:3%;width:91%;height:27.3%;padding:3.2% 4.1% 6.4%;border:1px solid rgba(124,199,255,.34);border-radius:12px;background:rgba(6,10,22,.82);overflow:hidden;z-index:3}
.dg-name{display:inline-block;margin-bottom:.5em;padding:.1em .8em;border-radius:999px;font-size:.92em;font-weight:700;color:#04121f;background:linear-gradient(135deg,#7cc7ff,#cdeaff)}
.dg-speak-player .dg-name{background:linear-gradient(135deg,#ff9ad5,#ffd3ee)}
.dg-text{margin:0;font-size:1em;line-height:1.7;text-shadow:0 2px 8px rgba(0,0,0,.6)}
.dg-hit{position:absolute;top:0;right:0;bottom:0;left:0;z-index:6;cursor:pointer}
.dg-restart{position:absolute;left:50%;bottom:2%;transform:translateX(-50%);z-index:6;padding:.3em 1.2em;border:1px solid rgba(124,199,255,.6);border-radius:999px;background:rgba(14,24,44,.95);color:#eaf1ff;font-size:.82em;font-weight:700;letter-spacing:.1em;white-space:nowrap;cursor:pointer;animation:dg-in .35s ease 1.2s both}
@keyframes dg-in{from{opacity:0;visibility:hidden}to{opacity:1;visibility:visible}}
</style>

  <input class="dg-s" type="radio" name="dg1" id="dg1-1" checked>
  <div class="dg-step dg-speak-role">
    <img class="dg-bg" src="https://cdn.jsdelivr.net/gh/karina-zzya/AI-assets@main/邻家大姐姐/出租房-晚上.png" alt="">
    <img class="dg-role" src="https://cdn.jsdelivr.net/gh/karina-zzya/AI-assets@main/邻家大姐姐/待机.png" alt="李云舒">
    <img class="dg-player" src="https://cdn.jsdelivr.net/gh/karina-zzya/AI-assets@main/邻家大姐姐/玩家-待机立绘.png" alt="{{user}}">
    <div class="dg-box">
      <b class="dg-name">李云舒</b>
      <p class="dg-text">门一响，我就听见了。……真的是你啊。</p>
    </div>
    <label class="dg-hit" for="dg1-2" aria-label="继续"></label>
  </div>

  <input class="dg-s" type="radio" name="dg1" id="dg1-2">
  <div class="dg-step dg-speak-player">
    <img class="dg-bg" src="https://cdn.jsdelivr.net/gh/karina-zzya/AI-assets@main/邻家大姐姐/出租房-晚上.png" alt="">
    <img class="dg-role" src="https://cdn.jsdelivr.net/gh/karina-zzya/AI-assets@main/邻家大姐姐/待机.png" alt="李云舒">
    <img class="dg-player" src="https://cdn.jsdelivr.net/gh/karina-zzya/AI-assets@main/邻家大姐姐/玩家-待机立绘.png" alt="{{user}}">
    <div class="dg-box">
      <b class="dg-name">{{user}}</b>
      <p class="dg-text">姐，我回来了。</p>
    </div>
    <label class="dg-hit" for="dg1-3" aria-label="继续"></label>
  </div>

  <input class="dg-s" type="radio" name="dg1" id="dg1-3">
  <div class="dg-step dg-speak-role">
    <img class="dg-bg" src="https://cdn.jsdelivr.net/gh/karina-zzya/AI-assets@main/邻家大姐姐/出租房-晚上.png" alt="">
    <img class="dg-role" src="https://cdn.jsdelivr.net/gh/karina-zzya/AI-assets@main/邻家大姐姐/微笑.png" alt="李云舒">
    <img class="dg-player" src="https://cdn.jsdelivr.net/gh/karina-zzya/AI-assets@main/邻家大姐姐/玩家-待机立绘.png" alt="{{user}}">
    <div class="dg-box">
      <b class="dg-name">李云舒</b>
      <p class="dg-text">欢迎回家。……好久不见，我们{{user}}。我等你好久了。</p>
    </div>
    <label class="dg-restart" for="dg1-1">重新开始</label>
  </div>

</div>
```
