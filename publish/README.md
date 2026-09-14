# 📚 《Hermes Agent 100 小時》上架出版套件

> 準備日期：2026-09-14 ｜ 作者：Happy eBook Authors ｜ 語言：繁體中文（zh-TW）

## 📦 套件內容

```
~/hermes-course/publish/
├── HermesAgent100Hours.epub      ← 主檔（EPUB 3，兩平台共用）
├── cover.jpg                     ← 封面 1600×2400（升頻自原圖）
├── cover_source.png              ← 原始封面備份（1024×1536）
├── manuscript.md                 ← 書稿原始檔（pandoc 可再轉其他格式）
├── google-play-books-metadata.md ← Google Play Books 後設表＋上架步驟
├── kobo-writing-life-metadata.md ← Kobo Writing Life 後設表＋上架步驟
└── README.md                     ← 本文件
```

## ✅ EPUB 品質驗證（已通過）

| 檢查項 | 結果 |
|---|---|
| mimetype 正確（application/epub+zip，zip 首項未壓縮） | ✓ |
| META-INF/container.xml 存在且指向 OPF | ✓ |
| OPF 含 metadata / manifest / spine / cover-image | ✓ |
| dc:title = Hermes Agent 100 小時 | ✓ |
| dc:creator = Happy eBook Authors | ✓ |
| dcterms 語言 = zh-TW | ✓ |
| 封面圖內嵌（EPUB/media/file0.jpg） | ✓ |
| 目次 nav.xhtml（170 項）＋ toc.ncx（171 navPoints） | ✓ |
| 全部 XML/XHTML 語法可解析 | ✓ |
| 內容檔案數：35 個 XHTML（17.5 萬字元） | ✓ |

> 建議上架前再用官方 EpubCheck 驗一次：https://epubcheck.org/ 或
> `pip install epubcheck` / Homebrew `brew install epubcheck`。

## 🚀 上架流程（兩平台）

### Google Play Books（Partner Center）
1. 開啟 https://play.google.com/books/publish/ → **Add New Book**
2. 按 `google-play-books-metadata.md` 填後設（類別用 BISAC，最多 3 個）
3. Content 頁上傳 `HermesAgent100Hours.epub` ＋ 封面另傳（建議更名 `ISBN_frontcover.jpg`）
4. 設定價格與銷售區域 → Submit → 等待審查

### Kobo Writing Life
1. 開啟 https://www.kobo.com/writinglife → **Create a New eBook**
2. 按 `kobo-writing-life-metadata.md` 填後設（Title/Subtitle 需與封面一致）
3. 上傳 `HermesAgent100Hours.epub` ＋ `cover.jpg`
4. 選 3 個 Subject categories → 設價 → 提交審查（人工審核數小時～數日）

## ⚠️ 上架前檢查表

- [ ] 決定 ISBN：無則兩平台都會自動指派（Kobo 指派者僅 Kobo 內部流通，不送其他通路）
- [ ] 決定價格與銷售區域（兩平台各自設定）
- [ ] （建議）補產 PDF 版：Google 同時收 EPUB+PDF 可提供「原版面」閱讀模式
- [ ] （建議）跑一次 EpubCheck 正式驗證
- [ ] 封面文字與後設 Title/Subtitle 一致（Kobo 明文要求）
- [ ] 確認書內無他人版權素材（教材改編自官方文件，註明出處）

## 🔄 內容更新怎麼做

改完 `manuscript.md` 重新產 EPUB：
```bash
cd ~/hermes-course/publish
pandoc manuscript.md -o HermesAgent100Hours.epub \
  --epub-cover-image=cover.jpg --toc --toc-depth=2 \
  --metadata lang=zh-TW --metadata title="Hermes Agent 100 小時" \
  --metadata author="Happy eBook Authors"
```
選單更新：編輯 `manuscript.md` 開頭 YAML 的 title/author 即可。
改封面：替換 `cover.jpg`（維持 1600×2400，2:3 比例）。

## 💰 定價建議（參考，非必須）
- 技術教學書常見區間：USD $5.99–$14.99（TWD 約 200–500 元）
- Kobo 有「會員價」機制（Kobo Plus），上架前可了解是否符合你的意願