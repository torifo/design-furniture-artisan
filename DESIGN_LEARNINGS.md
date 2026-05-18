# BURL Design Learnings

## 目的

クラフト志向ペルソナ（25–45代）は「誰が作ったか」「どう作られたか」を家具そのものより先に知りたい。BURLでは、新聞・カタログ的なエディトリアルレイアウトで、製品の前に職人と素材を見せる設計を選んだ。

BURLは架空ブランドであり、実在の店舗・商品ではない。

---

## 「整ったUIを捨てる」という判断

BURLの設計における最も重要な判断は、**ウェブ的な滑らかさを意図的に排除した**こと。

| 捨てたもの | 代わりに選んだもの |
|-----------|------------------|
| スムーズなスクロールリビール（translateY） | opacity onlyのフェード |
| カードグリッド | テーブルリスト（注文書形式） |
| 固定ナビ | マストヘッドに統合した静的ナビ |
| ローダー・マーキー・grain | なし |
| ライフスタイル写真 | プロセス・素材・職人の顔 |

「丁寧に作られた印刷物」を参照点にした。ウェブサイトではなく、**工房カタログがデジタルになったもの**として設計する。

---

## レイアウト

```
マストヘッド → ヒーロー（不規則グリッド）→ 工程解説（3カラム）
→ 製品カタログ（テーブルリスト）→ Makersセクション → フッター
```

### ヒーローの不規則グリッド

```css
.hero-editorial {
  display: grid;
  grid-template-columns: 8fr 4fr;
  grid-template-areas:
    "main sub1"
    "main sub2"
    "main quote";
}
```

新聞の紙面割り付けを参照。「メイン記事 + 関連写真 + 引用文」という構造が自然に視線を誘導する。

### 製品カタログ（テーブルではなく CSS Grid）

```css
.catalog-row {
  display: grid;
  grid-template-columns: 3rem 1fr auto auto auto auto;
  /* 品番 / 製品名 / 素材 / 価格 / リードタイム / 詳細リンク */
  padding: 1.25rem 0;
  border-bottom: 1px solid var(--border);
}
.catalog-row:hover { background: rgba(31,24,16,0.04); }
```

`<table>` ではなく CSS Grid を使うことで、レスポンシブ時の列の隠し・折り返しがCSSで管理できる。

---

## CSS

主要な判断:

```css
:root {
  --bg:   #F5EDDE;   /* クラフト紙。冷たい白を排除 */
  --rust: #8B3829;   /* 見出しアクセント。錆びた釘の色 */
  --font-serif: 'DM Serif Display', Georgia, serif;
  --font-mono:  'IBM Plex Mono', monospace;   /* スペック・品番 */
}
```

フォントの混在（DM Serif Display + IBM Plex Mono）が「印刷物的な誠実さ」を生む。見出しは組版的セリフ、仕様書はタイプライター。

---

## マストヘッドの設計

```css
.masthead {
  border-bottom: 2px solid var(--fg);   /* 太い線が新聞感 */
  display: grid;
  grid-template-rows: auto auto;
}
.masthead-top {
  border-bottom: 1px solid var(--fg);
  font-family: var(--font-mono);
  font-size: 0.6rem;
  /* "Issue No. 12 · AW 2026 · Handcrafted in Scandinavia" */
}
```

マストヘッドを `position: static` にしたのは意図的。スクロールで消えることで「カタログをめくる」感覚が生まれる。

---

## フォント

- Display: `DM Serif Display italic` — 書籍組版的。Playfair Displayより現代的で、Cormorant Garamondより温度がある
- Mono: `IBM Plex Mono` — 製品仕様・品番・価格のみ使用。タイプライターで書かれた注文書のような誠実さ
- Body: `Outfit weight 300/400` — 読み取りやすさのベース

---

## アニメーション

- `opacity only` のリビール（translateYなし）
- `0.6s ease` — シリーズで最短。印刷物は「現れる」のではなく「最初からそこにある」
- 商品行ホバー: `background-color 0.15s` のみ。素直な反応

---

## furniture シリーズとの対比

| 軸 | VELA（luxury） | BURL（artisan） |
|----|----------------|----------------|
| 構造 | Chapter全画面 | 新聞エディトリアルフロー |
| 製品表示 | 1製品1章 | テーブルリスト（複数並記） |
| ナビ | 固定サイドドット | マストヘッドに統合（静的） |
| フォント | Playfair Display | DM Serif Display + IBM Plex Mono |
| アクセント | ゴールド #B8945A | 錆び赤 #8B3829 |
| アニメーション | opacity + translate / 1s | opacity only / 0.6s |
| 背景 | ニュートラルホワイト #FAFAF8 | クラフト紙 #F5EDDE |
