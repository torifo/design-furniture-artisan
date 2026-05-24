# BURL — design-furniture-artisan

> **架空ブランド注記**: BURLは本デザイン研究のために作成した架空ブランドです。実在のブランド・店舗・商品ではありません。

---

## Overview

**furniture design research series** の「アルチザン」ペルソナ作品。

「burl」はオーク等の樹木に生じる美しい不規則な木目（瘤）のこと。クラフト志向の購買層（25〜45代）が求める「誰が、どこで、どう作ったか」という問いに、新聞・カタログ的なエディトリアルレイアウトで答える。製品より職人と素材を前面に出す設計。

---

## Brand

| | |
|--|--|
| **Brand** | BURL |
| **Tagline** | Made by Hand. Built to Last. |
| **Aesthetic** | 職人工房カタログ × 新聞エディトリアル |
| **Target Persona** | 25–45代、職人技と素材工程を重視するクラフト志向 |
| **Color** | Kraft Paper `#F5EDDE` + Ink `#1F1810` + Rust `#8B3829` |
| **Display Font** | DM Serif Display |
| **Spec Font** | IBM Plex Mono |
| **Body Font** | Outfit |

---

## Design Approach

ウェブ的な「滑らかさ」を意図的に排除し、**工房カタログがデジタルになったもの**として設計した。

- **新聞マストヘッド**: ロゴ・発行号・日付を同一ラインに。固定ナビなし
- **不規則ヒーローグリッド**: CSS Grid named areasで「紙面割り付け」を再現
- **製品テーブルリスト**: カードグリッドではなく、品番・素材・価格・リードタイムを1行に並べた注文書形式
- **IBM Plex Mono**: 製品仕様のみタイプライター体。「手書きの仕様書」的誠実さ
- **Makersセクション**: 職人の顔と経歴を最終セクションに配置

**排除したUI要素**: ローダー・マーキー・grain・カスタムカーソル・スムーズなtranslateYアニメーション

---

## Tech

- Vanilla HTML / CSS / JS — single file (`index.html`)
- Google Fonts: [DM Serif Display](https://fonts.google.com/specimen/DM+Serif+Display), [IBM Plex Mono](https://fonts.google.com/specimen/IBM+Plex+Mono), [Outfit](https://fonts.google.com/specimen/Outfit)
- ビルドツール不要

## Local Development

```bash
open index.html
# または
python3 -m http.server 8080
```

---

## Series

このリポジトリは **furniture design research series** の一作です。

| Theme | Brand | Aesthetic | Persona | Site |
|-------|-------|-----------|---------|------|
| nordic | HVILE | 北欧オーガニック | 30–45代、素材重視の住まい手 | [design.furniture-nordic.riumu.net](https://design.furniture-nordic.riumu.net/) |
| luxury | VELA | ラグジュアリー・アトリエ | 40–60代、ラグジュアリー層 | [design.furniture-luxury.riumu.net](https://design.furniture-luxury.riumu.net/) |
| **artisan** | **BURL** | **職人工房・カタログ** | **25–45代、クラフト志向** | [design.furniture-artisan.riumu.net](https://design.furniture-artisan.riumu.net/) |
| urban | BLOC | アーバン・グラフィック | 20–35代、都市生活者 | [design.furniture-urban.riumu.net](https://design.furniture-urban.riumu.net/) |
