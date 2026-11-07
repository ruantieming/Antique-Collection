# 瓷路 · 铁明藏瓷 — 维护说明

静态单页站：`index.html`（全部代码+数据）+ `photos/`（图片）。无构建、无依赖（仅Google Fonts），任何静态托管可用。

## GitHub Pages 部署
1. 本仓库 Settings → Pages → Source: Deploy from a branch → `main` / `(root)` → Save
2. 网址：`https://<用户名>.github.io/<仓库名>/`；单件直链：`.../#transitional-bowl`

## 日常更新

**加照片**（最常用）
1. 图片压到长边≤1200px、~150KB（手机导出或任何压图工具即可），命名如 `canton-1.jpg`
2. 拖进 `photos/` 文件夹（GitHub网页 Add file → Upload files）
3. `index.html` 里 `var PHOTOS = {` 区块对应器物加文件名：
   `"transitional-bowl": ["transitional-1.jpg", ..., "新文件名.jpg"],`
   第一张是卡片封面和档案主图。

**加一件新器物**（三处）
1. `var ITEMS = [` 数组末尾照此模板加一条（中文）：
```js
{id:"canton-plate", st:"col", title:"外销青花 Canton 盘", date:"清 · 乾隆—嘉庆，约1760–1810",
 verdict:"一句话判语：真伪、断代依据要点、在收藏体系里的位置。",
 meta:[["口径","9 英寸"],["装烧","垫饼仰烧"],["款识","无款"]],
 secs:[
  ["鉴定依据",["证据一","证据二","证据三"]],
  ["品相",["描述"]]
 ]},
```
   `id`：小写英文连字符，全站唯一。`st`："col"=入藏（主页网格显示）/ "spec"=标本室 / "watch"=过眼（本分享版不显示，仅存档案）。
2. `var EN = {` 对象里加同id的英文版（title/date/verdict/meta/secs同结构）；漏了也不崩，EN模式下回退显示中文。
3. `PHOTOS` 里加照片（见上）。


**加一个新分类**（如外销银器、玉器）——两步
1. `index.html` 里搜 `var SECTIONS`，照样加一行：
```js
 {id:"silver", hash:"silver", zh:"外销银器", en:"Export Silver",
  zhs:"分类副标题（中文）。", ens:"Section subtitle (English)."},
```
   （上一行末尾记得补逗号。）导航按钮、标签页、网格、返回键全部自动生成。
2. 新器物照常加进 `ITEMS`/`EN`/`PHOTOS`，`st` 用新分类的 id（如 `st:"silver"`），卡片自动归入该标签页。

**年表SVG加盒子**：坐标映射 X(年)=208+(年-1550)×1.72（1900前）/ 810+(年-1900)×5.92（1900后）。手算易错，建议攒几件后交给AI统一排版（见下）。

## 让AI改（个人Gemini/Claude/ChatGPT通用指令）
上传 `index.html` + 新照片，粘贴：
> 这是我的瓷器收藏网站，单文件HTML。数据在 `var ITEMS`（中文）、`var EN`（英文）、`var PHOTOS`（照片映射）。请照现有条目的格式，把下面这件新器物加进这三处，并在年表SVG的中国线对应年代加一个盒子（坐标函数：X(y)=208+(y-1550)*1.72 当y≤1900，否则 810+(y-1900)*5.92；盒子格式照抄现有的，不与同行其他盒子重叠，加 `<a href="#新id">` 链接和绿色圆点）。**除此之外不要改动任何代码、样式或其他数据，输出完整文件。**
> 新器物信息：【贴你的鉴定文字】 照片文件名：【xxx.jpg】

改完替换仓库里的 `index.html`。Git自带版本历史，改坏随时回滚（仓库 → History → 旧版本 → 恢复）。

## 原则（本分享版）
- 不含价格、购入渠道、议价信息——新增档案也请保持
- 年表只放：已有藏品（绿点实心盒）、缺口目标（虚线圈）、历史背景（虚线框）
