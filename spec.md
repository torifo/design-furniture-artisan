# BURL — design-furniture-artisan Spec

**Status:** Approved  
**Author:** torifo  
**Created:** 2026-05-19  
**Updated:** 2026-05-19

---

## 1. Overview

### Problem Statement
クラフト志向の購買層（25〜45代）は「誰が作ったか」「どう作られたか」を知りたいが、既存の工芸系家具サイトは製品写真を並べるだけで、制作プロセスや職人の顔が見えない。また「おしゃれなEC」に仕立てようとして、クラフト本来の泥臭さや誠実さが失われているケースが多い。

### Goal
「BURL」という架空のアルチザン家具工房のサイトを、**新聞・カタログ的エディトリアルレイアウト**で実装する。製品より「作り手・素材・工程」を前面に出し、ウェブデザイン的なスムーズさよりも印刷物的な誠実さを優先する。

### Non-Goals
- EC機能（カート・決済）
- ローダー・マーキー・grain overlay・カスタムカーソル
- スムーズなアニメーション（アパレル/HVILEとの差別化）

### Background
- BURLは架空ブランド（burl = 木の瘤。美しい不規則な木目）
- `design-furniture-artisan` リポジトリ予定
- 「整ったUIを捨てて、印刷物的な誠実さを選ぶ」実験

---

## 2. User Stories

| ID | Persona | Want to | So that |
|----|---------|---------|---------|
| US-01 | クラフト志向 (25–45代) | 誰がどこで作ったかを最初に知りたい | 職人への信頼を持ってから商品を見られる |
| US-02 | 同上 | 製品の素材・工程・サイズを詳細に確認したい | 「合うかどうか」を一切の曖昧さなく判断できる |
| US-03 | 同上 | スクロールせず全体を俯瞰したい | 新聞を広げるように全貌をつかめる |
| US-04 | 同上 | モバイルでも同じ情報密度を得たい | 外出先でもカタログとして機能する |

### Acceptance Criteria (EARS notation)

**US-01: Makerセクション**
- WHEN ページを開いた THEN ヘッダーに職人名・創業年・産地がマストヘッドとして表示される
- WHEN Makersセクションに到達した THEN 職人の顔写真と経歴が2カラムで表示される

**US-02: 製品カタログ（リスト形式）**
- WHEN 商品リストを見た THEN 品番・製品名・素材・価格・リードタイムが1行に収まった形式で表示される
- WHEN 商品行にホバーした THEN その行がハイライトされる（背景色の変化）

**US-03: エディトリアルヒーロー**
- WHEN ページトップを見た THEN 不規則コラムグリッド（メイン画像大+サブ画像2点+引用文）が並置されている
- WHEN 375px幅で閲覧した THEN コラムが1列に積み直される

---

## 3. Functional Requirements

| ID | Requirement | Priority | Notes |
|----|-------------|----------|-------|
| FR-01 | マストヘッド（新聞ヘッダー：ブランド名＋発行号・日付） | P0 | ナビも同一ラインに配置 |
| FR-02 | 不規則ヒーローグリッド（メイン画像8/12＋サブ2枚＋引用文） | P0 | CSS Grid named areas |
| FR-03 | 工程解説セクション（3カラムテキスト、中央に画像） | P1 | 印刷組版的 |
| FR-04 | 製品カタログ（テーブルリスト形式、4製品） | P0 | グリッドカードなし |
| FR-05 | Makersセクション（職人2名：写真+名前+経歴） | P1 | |
| FR-06 | モノスペース仕様書（IBM Plex Monoで製品仕様を表示） | P1 | タイプライター感 |
| FR-07 | スクロールリビール最小限（opacity only、0.6s） | P2 | translateYなし |
| FR-08 | モバイル対応 | P0 | 375px基準、コラム→1列 |

---

## 4. Architecture

### Page Structure

```
index.html
├── header.masthead          # 新聞マストヘッド（ロゴ大・日付・号数・ナビ）
├── section.hero-editorial   # 不規則グリッドヒーロー
├── section.process          # 工程解説（3カラム）
├── section.catalog          # 製品カタログ（テーブルリスト）
├── section.makers           # 職人紹介（2カラム）
└── footer.simple            # 1〜2行のシンプルフッター
```

### Key Design Decisions

| Decision | Chosen | Rationale | Rejected alternatives |
|----------|--------|-----------|----------------------|
| 製品表示 | テーブルリスト形式 | 注文書・カタログ的。工房の誠実さを体現 | カードグリッド（ECっぽい） |
| ヒーロー | 不規則CSS Grid（named areas） | 新聞の「紙面レイアウト」感 | フルスクリーン写真（HVILEと被る） |
| ナビ | マストヘッドに統合（固定なし） | スクロールで消えてもよい。カタログは通読する | 固定ナビ（ウェブ的すぎる） |
| アニメーション | 最小限（opacity only） | 紙をめくる感覚。滑らかさは不要 | slideUp（ARCH/HVILEと被る） |
| Grain/Cursor | なし | 装飾より情報。工房の誠実さを優先 | あり |

---

## 5. Design System

### Color Palette
```css
--bg:     #F5EDDE;   /* クラフト紙 */
--fg:     #1F1810;   /* インク */
--rust:   #8B3829;   /* 錆び赤（chapter heading accent） */
--moss:   #485C38;   /* 苔緑（Maker section） */
--border: #C8BAA2;   /* 薄い仕切り線 */
--muted:  #6B5C4A;   /* ミュートテキスト */
```

### Typography
```css
--font-serif: 'DM Serif Display', Georgia, serif;
--font-mono:  'IBM Plex Mono', monospace;
--font-sans:  'Outfit', sans-serif;
```
- Google Fonts: `DM+Serif+Display:ital@0;1` + `IBM+Plex+Mono:wght@300;400;500` + `Outfit:wght@300;400`

### Spacing Philosophy
- セクション間は `border-top` のみ。padding controlで余白を作る
- 1px borderが「ページの折り目」として機能する

---

## 9. Testing Strategy (Visual QA)

| Layer | Scenarios |
|-------|-----------|
| Desktop (1280px) | 不規則グリッド確認、テーブルホバー、3カラム |
| Mobile (375px) | 1列化、マストヘッドの折り返し |
| タイポグラフィ | DM Serif Display・IBM Plex Mono読み込み確認 |

---

## 10. Implementation Notes

- ヒーローのCSS Grid: `grid-template-areas` で名前付き配置。`grid-template-columns: 8fr 4fr`
- 製品テーブル: `<table>` ではなく CSS Grid の `grid-template-columns: auto 1fr auto auto auto auto` で柔軟に
- マストヘッドは `position: sticky; top: 0` で固定（スクロール後も見える）ではなく `position: static` を選択
- Makersセクションは `display: grid; grid-template-columns: 1fr 1fr; gap: 4rem`
- IBM Plex Monoは製品仕様書部分のみ使用（フォント混在でクラフト感を出す）
