# 品牌健檢報告（貝納頌）

> 這個 repo 是「報告的原始碼」，不是只放成品。
> 真正要持續更新、版本控管的是 **數據邏輯**（SQL）與 **簡報原始碼**（build-deck.js），
> `.pptx` / `.html` 只是跑出來的產物。

---

## 檔案結構

```
.
├── index.html              ← HTML 報告（GitHub Pages 直接當網頁，固定網址）
├── scripts/
│   └── build-deck.js       ← 簡報原始碼（pptxgenjs，跑它產生 .pptx）
├── sql/
│   └── queries.sql         ← 四面向撈數 SQL（換品牌改關鍵字即可）
└── 貝納頌_品牌健檢報告.pptx   ← 成品（附帶產物；對外更新走雲端硬碟，見下）
```

---

## 方案 2：HTML 版用 GitHub Pages（同一個網址，更新即生效）

一次性設定：

1. 在 GitHub 建一個 repo，把這整包推上去（`index.html` 一定要在根目錄）。
2. repo → **Settings → Pages** → Source 選 `Deploy from a branch` → Branch 選 `main` / 根目錄 `/ (root)` → Save。
3. 等 1～2 分鐘，會得到一個固定網址：`https://<你的帳號>.github.io/<repo名>/`

之後每次更新：

```bash
# 改完 index.html 後
git add index.html
git commit -m "更新 Q2 數據"
git push
```

push 完，**同一個網址重整就是最新版**。看的人不用換連結。
（想保護不公開，可改用 Cloudflare Pages 或加密碼閘道，GitHub Pages 預設是公開的。）

---

## 方案 3：PPTX 版用雲端硬碟（同一個連結，覆蓋更新）

GitHub 不適合 `.pptx`（二進位、看不出 diff）。給人看的簡報走雲端硬碟最直覺：

1. 把 `貝納頌_品牌健檢報告.pptx` 上傳 Google Drive（或 SharePoint）。
2. 對檔案「取得連結 / 共用」，把這個連結發給對方。
3. 之後更新：在 Drive 對著同一個檔案 **「管理版本 / 上傳新版本」**（不是刪掉重傳），
   連結不變、對方看到的永遠是最新版，且 Drive 自己會保留歷史版本可還原。

> Google Drive：對檔案右鍵 → 管理版本 → 上傳新版本。
> SharePoint/OneDrive：同名覆蓋上傳即自動產生版本歷史。

---

## 更新一份報告的標準流程

1. **撈數**：用 `sql/queries.sql` 撈最新數字（改日期區間即可）。
2. **改原始碼**：把新數字填進 `index.html`（HTML 報告）和 `scripts/build-deck.js`（簡報）。
3. **產簡報**：
   ```bash
   npm install pptxgenjs        # 第一次才需要
   node scripts/build-deck.js   # 產出新的 .pptx
   ```
4. **發佈**：HTML → `git push`（Pages 自動更新）；PPTX → Drive 上傳新版本。

---

## 換一個品牌做新報告

1. `sql/queries.sql`：把 `貝納頌|bernachon` 換成新品牌關鍵字、競品聯集同步換。
2. `scripts/build-deck.js`：換標題、數字、品牌名。
3. 重跑、發佈。

> 換色：`build-deck.js` 開頭的 `C` 物件集中所有色碼，改一處即全簡報換色。
