# 美学卡片 · flomo 式网状联想（GitHub Pages 版）

94 张美学知识卡片，支持卡片流 / 网状关系图 / 随机漫步，带**图片纠错编辑层**，并支持**多图轮播**与**剪贴板粘贴图片链接**。

---

## 一、如何纠正代表图片（重点）

### 方式 A：页面里直接改（最省事，无需改代码）

1. 打开页面，点顶部工具栏的 **✎ 纠错模式**
2. 点任意一张卡片，右侧会出现编辑面板
3. 修改图片链接，可顺手改图片说明、一句话定义
   - **粘贴图片链接**：点图片框旁的 **📋 粘贴** 按钮；或点中图片框后直接按 **Ctrl+V**（会自动从剪贴板文字里提取 http 链接，支持整段 URL / Markdown 图片语法）
   - 焦点不在任何输入框时直接按 **Ctrl+V**，会自动贴到第一张图片
4. 点 **保存修正** —— 立即生效，且存在你本机浏览器里，刷新不丢
5. 收集好若干条后，点 **导出修正**，会下载一个 `overrides.json`

把这个 `overrides.json` 放到本目录（覆盖同名文件）或提交到 GitHub 仓库，所有人打开页面就都会看到修正后的图片。

> 注：浏览器剪贴板读取在 `https`（GitHub Pages）和 `localhost` 下可用；若用 `file://` 双击打开受限，手动点中输入框按 Ctrl+V 仍可粘贴。

### 方式 B：多张图片 + 详情轮换

每条词条可以挂**多张代表图**：

- 在纠错模式的编辑面板里，点 **＋ 添加一张图片** 增加图片行，可逐张填 URL 和说明
- 保存后，点开该卡片，详情里图片区出现 **‹ › 箭头** 和**圆点**，可鼠标点击切换；卡片缩略图右上角会显示「图 N 张」角标
- 图片说明会显示在图片左下角，计数显示「当前 / 总数」

### 方式 C：直接编辑 `overrides.json`（适合批量 / 协作者）

文件格式（键是词条英文名，只写要改的字段）：

```json
{
  "Y2K": {
    "imgs": [
      { "url": "https://images.pexels.com/photos/111/pexels-photo-111.jpeg", "desc": "镭射光泽" },
      { "url": "https://images.pexels.com/photos/222/pexels-photo-222.jpeg", "desc": "透明塑料质感" }
    ],
    "def": "可选：覆盖默认定义"
  },
  "Goblincore": {
    "img": "https://...",
    "img_desc": "苔藓、蘑菇与旧铜器"
  }
}
```

- `imgs`：图片数组（多张，推荐用这个）；`img` / `img_desc`：单张旧格式，仍兼容
- 其他可改字段：`def`（定义）、`judge`（判别要点）、`cn`（中文名）
- 以 `_` 开头的键会被忽略，可用来写备注

改完保存，刷新页面即可。已修正的词条卡片上会显示一个「已修正」小标签。

### 关于「开放编辑入口」

这是**纯静态页面**（GitHub Pages 只托管文件，没有后端），所以：

- ✅ 任何人都能看到你发布的修正
- ✅ 你可以把 `REPO` 配置好，让卡片里出现「在 GitHub 编辑」和「提交 Issue 反馈」按钮，别人可通过 Issue 给你提图片纠正
- ✅ 协作者若有仓库写权限，可直接在 GitHub 网页上编辑 `overrides.json`
- ❌ 无法做到「匿名访客直接在页面上改，且所有人同步看到」——那需要后端数据库

配置仓库：打开 `index.html`，找到 `const REPO = '';`，改成 `const REPO = '你的用户名/仓库名';`，保存即可。

---

## 二、发布到 GitHub Pages（约 3 分钟）

1. 在 GitHub 新建一个仓库，例如 `aesthetic-atlas`，设为 **Public**
2. 把本目录下的文件全部上传进去：
   - `index.html`
   - `overrides.json`
   - `.nojekyll`（空文件，防止 Pages 用 Jekyll 处理）
   - `README.md`
3. 仓库 **Settings → Pages → Build and deployment**：
   - Source 选 `Deploy from a branch`
   - Branch 选 `main`，目录选 `/ (root)`，Save
4. 等待 1～2 分钟，访问 `https://你的用户名.github.io/aesthetic-atlas/`

> 提示：如果仓库名不是用户名前缀，网址就是 `https://用户名.github.io/仓库名/`。

---

## 三、本地打开 vs 在线打开

- **双击本地 `index.html`**：可用。但浏览器不允许本地文件 `fetch`，所以页面不会自动读取 `overrides.json`。请用工具栏的 **导入修正** 按钮手动载入。纠错改动存在本机浏览器 localStorage。
- **GitHub Pages / 本地 HTTP 服务**：页面会自动读取同目录 `overrides.json`，并让本机修正优先叠加。可用 `python3 -m http.server 8000` 在本机模拟在线环境。

---

## 四、数据与来源

- 94 条词条：科技/机械/工业硬核 42 条 + 核类美学 52 条
- 一级标签 16 个、二级标签 28 个、血缘连线 84 条
- 代表图来自 Pexels 公开直链（非 AI 生成）；若外链失效，用上面的纠错机制替换即可
- 配套 Notion 词典页：https://app.notion.com/p/41a4308e5d4f811e90fbc8a0314c558e
