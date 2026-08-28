# Vercel 部署 + 绑定 aidesignlab.cc 实操指南

目标：把「中国就业市场 AI 影响分析」挂到你自己的域名下，拿到 **https://jobs.aidesignlab.cc**（或你偏好的子域）。

> 前置：你已有 Vercel 账号，且 `aidesignlab.cc` 主站已在 Vercel 上运行。

---

## 一、准备代码（已帮你做完）

- `index.html`：已加龙御2037 品牌署名、顶部数据免责声明、SEO/OG/Twitter 分享元数据。
- `README.md`：已改为龙御2037 口径 + 部署说明。
- `vercel.json`：已加，告诉 Vercel 这是纯静态站点、无需构建。
- `CNAME`：已删除（原指向 `ai.easonzhan.cyou`，不属于你，留着会误导）。

代码位置：`D:\我的知识库\AI实验室\AI影响职业分析\AI-Impact-Jobs\`

---

## 二、推到你的 GitHub（约 2 分钟）

1. 打开 github.com，新建一个仓库，建议名 `ai-impact-jobs`（Public 即可，Vercel 免费版支持）。
2. 把 `AI-Impact-Jobs` 目录里的文件（index.html、README.md、vercel.json）push 上去。
   - 该目录原本是别人（EasonZe）的 git 仓库，请**不要**直接用它，自己建新仓库推。
   - 只需这三个文件，数据已内联在 index.html 里，无需其他资源。

如果不会命令行推，也可以跳过 GitHub，直接用下面「拖拽部署」。

---

## 三、Vercel 部署（约 3 分钟）

**方式 A：连 GitHub（推荐，以后改代码自动重新部署）**
1. 打开 vercel.com → 右上角 **Add New… → Project**。
2. 在 Import Git Repository 里选中你的 `ai-impact-jobs` 仓库 → **Import**。
3. Framework Preset 选 **Other**（纯静态），Root Directory 默认，点 **Deploy**。
4. 几十秒后拿到一个 `xxx.vercel.app` 临时链接，先点开确认页面正常。

**方式 B：拖拽部署（最快，不需 GitHub）**
1. 打开 vercel.com → **Add New… → Project** → 选择 **Deploy** 标签页（或首页直接拖文件夹）。
2. 把 `AI-Impact-Jobs` 文件夹拖进去 → 自动识别为静态站 → Deploy。
3. 同样先拿到 `xxx.vercel.app` 临时链接确认。

---

## 四、绑定 jobs.aidesignlab.cc（约 3 分钟 + DNS 生效等待）

1. 在 Vercel 项目里点 **Settings → Domains**。
2. 输入 `jobs.aidesignlab.cc` → **Add**。
3. Vercel 会显示一条 DNS 记录要求，通常是：
   - 类型 **CNAME**
   - 名称 `jobs`
   - 值 `cname.vercel-dns.com`（以页面显示为准）
4. 登录 `aidesignlab.cc` 的域名商（Cloudflare / Namecheap / 阿里云 / 腾讯云等），在 DNS 解析里**新增一条 CNAME 记录**，按上面填。
5. 回到 Vercel Domains 页面，等状态从 `Invalid Configuration` 变 `Valid Configuration`（绿色），说明 DNS 生效。
6. 访问 **https://jobs.aidesignlab.cc**，搞定。HTTPS 证书 Vercel 自动签发，无需手动配。

> DNS 生效时间：通常 5 分钟到 1 小时，取决于域名商 TTL。

---

## 五、上线后收尾

- **分享卡片 og:image**：社交分享目前无图，可再生成一张 1200×630 的分享图补上（匹配龙御视觉 DNA）。
- **移动端核对**：手机上打开 treemap / 表格 / 深色模式再扫一遍。
- **下线 CloudStudio 旧链接**：旧的 `https://9559ddee3dd64c08998f90283948f59a.app.workbuddy.link` 可保留过渡，或确认 Vercel 正常后下线（在 WorkBuddy「设置 - 数据管理 - 我发布的应用」里操作）。

---

## 常见问题

**Q：能不能用路径 aidesignlab.cc/jobs 而不是子域？**
A：可以，但更复杂——需要在 `aidesignlab.cc` 主站项目里配置 rewrite 到本项目的部署，且两个项目都要在 Vercel。子域 `jobs.aidesignlab.cc` 最省事，推荐。

**Q：子域名能改成别的吗？比如 aiimpactjobs.aidesignlab.cc？**
A：可以，第 4 步填你想要的子域即可，只要 DNS 里 CNAME 名称对应改掉。

**Q：Vercel 免费版够用吗？**
A：纯静态站点、流量不大完全够用，自带 HTTPS、自动 CDN。

**Q：改了 index.html 怎么更新上线？**
A：若用 GitHub 方式，push 新代码自动重新部署；若用拖拽方式，重新拖一次文件夹。
