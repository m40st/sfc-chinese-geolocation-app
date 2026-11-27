# SFC 中国語フレーズ学習アプリ
**SFC Chinese Phrase Learning App**

慶應義塾大学SFCキャンパス内で、場所に応じた中国語フレーズ・単語を学習できるWebアプリ。  
A Chinese language learning web app designed for use on the Keio University SFC campus.

![Status](https://img.shields.io/badge/status-Prototype-orange)
![Status](https://img.shields.io/badge/ステージ-実証実験中-orange)
![Deploy](https://img.shields.io/badge/deploy-Netlify-00C7B7?logo=netlify)
![License](https://img.shields.io/badge/license-MIT-blue)

---

## バージョン構成 / Versions

このリポジトリは2つのバージョンを並行開発している。

| バージョン | ブランチ | URL | 状態 |
|-----------|---------|-----|------|
| **手動選択版**（現行・推奨） | `main` | [sfc-chinese-geolocation.netlify.app](https://sfc-chinese-geolocation.netlify.app) | 本番稼働中 |
| **GPS測位版**（開発継続中） | `gps-dev` | [gps-dev--sfc-chinese-geolocation.netlify.app](https://gps-dev--sfc-chinese-geolocation.netlify.app) | 開発中 |

### なぜ手動選択版を作ったか

GPS版の開発中、スマートフォンの屋内GPS精度の限界により、建物判定が安定しない問題が継続して発生した。研究発表に向けて発音練習・フレーズ学習機能を先行して使える状態にするため、2026年11月に手動選択版（`main`）を別途リリースした。GPS版（`gps-dev`）は引き続き精度改善を進め、完成次第 `main` へ統合する予定。

> GPS accuracy limitations on smartphones (especially indoors) caused persistent building-detection instability. To ensure the phrase/vocabulary learning features were usable for research presentation, a manual building-selection version was released in November 2026. The GPS version continues in parallel development on `gps-dev`.

---

## 現在のステージ / Current Stage

| | |
|---|---|
| **ステージ** | プロトタイプ（実証実験中） |
| **目標** | 研究発表版（v1.0）の完成 |
| **場所** | 慶應義塾大学 SFCキャンパス |

---

## ロードマップ / Roadmap

```
Phase 1 ──────── Phase 2 ──────────── Phase 3
基盤構築 ✅        精度改善・並行開発 🔧    研究発表版 🔜
```

---

### Phase 1 　基盤構築 ✅　*完了*

| 機能 | 説明 |
|------|------|
| ✅ GPS/QZSS位置検出 | `watchPosition()` + Haversine formula |
| ✅ 建物ジオフェンシング | 各建物に検出半径（r）を設定 |
| ✅ 屋内・屋外判定 | 接近・滞在・離脱の状態管理 |
| ✅ 中国語フレーズ表示 | 場所に連動したコンテキスト表示 |
| ✅ 発音練習 | Web Speech API（zh-CN）による音声評価 |
| ✅ SVGキャンパスマップ | リアルタイムで現在地を表示 |
| ✅ CI/CD | GitHub push → Netlify 自動デプロイ |
| ✅ QZSS実測座標 | ο館・τ館（講義棟）を現地計測（±3〜4m） |

---

### Phase 2 　精度改善・並行開発 🔧　*現在進行中*

| 課題 | 詳細 | ブランチ |
|------|------|---------|
| ✅ 手動選択版リリース | GPS精度問題の回避策として並行開発・本番公開 | `main` |
| 🔧 GPS精度改善 | 全建物の座標更新・室内GPS対応強化 | `gps-dev` |
| 🔧 マップピンのズレ修正 | `g2s()` GPS→SVGピクセル変換の精度改善 | `gps-dev` |

---

### Phase 3 　研究発表版（v1.0）🔜　*予定*

| 機能 | 説明 |
|------|------|
| 🔜 GPS版と手動版の統合 | GPS精度が十分になり次第 `gps-dev` → `main` に統合 |
| 🔜 学習履歴の可視化 | フレーズ別の練習回数・達成率を表示 |
| 🔜 フレーズ拡充 | CLT・TBLT理論に基づくシナリオ追加 |

---

## 機能 / Features

### 手動選択版（`main`）

- **建物手動選択** — 現在地の建物をタップして選択、フレーズ練習を即座に開始
- **フレーズ一覧・単語一覧** — 全エリア・エリア別に一覧表示、ブックマーク（★）機能付き
- **ブックマーク練習** — ★を付けたフレーズ・単語だけを集中練習
- **間違えたもの練習** — 不正解だったフレーズ・単語のみ再練習
- **発音練習** — Web Speech API（zh-CN）による音声認識で発音を評価
- **学習履歴** — 練習したフレーズ・単語の履歴をローカルに保存

### GPS測位版（`gps-dev`、開発中）

- **GPS/QZSS位置検出** — 現在地を自動検出して近傍建物を判定
- **SVGキャンパスマップ** — リアルタイムで現在地と最寄り建物を表示
- **建物ジオフェンシング** — 接近・滞在・離脱を自動判定

---

## 対応建物 / Supported Buildings

| 建物名 | 概要 |
|--------|------|
| バス停 | キャンパス入口 |
| Μ館（メディアセンター） | 図書館・3Dプリンター |
| Σ館 | 食堂・ラウンジ・コンビニ |
| 講義棟（κ・ε・ι・ο・λ・θ・Ω） | 各講義室 |
| α館 | 本館・学事・ウェルネス |
| サブウェイ | 軽食・テイクアウト |
| τ館 | 大学院棟 |
| Δ館 | 研究棟 |
| Γ館（体育館） | スポーツ・サークル |
| 鴨池（ガリバー池） | 屋外・休憩スペース |

---

## 技術構成 / Tech Stack

| 項目 | 内容 |
|------|------|
| 言語 | HTML / CSS / JavaScript（フレームワークなし） |
| 位置情報 | `navigator.geolocation` API（QZSS対応）※GPS版のみ |
| 音声認識 | Web Speech API（`zh-CN`） |
| フォント | Noto Sans JP（Google Fonts） |
| デザイン | デジタル庁デザインシステム準拠（純黒背景） |
| ホスティング | Netlify（GitHub連携による自動デプロイ） |
| データ保存 | `localStorage`（サーバーなし） |

**No frameworks used** — Pure HTML/CSS/JS single-file app. No build tools, no npm, no backend.

---

## 使い方 / How to Use

### 手動選択版（推奨）

1. スマホ・PCでアプリを開く / Open the app on your device
2. 建物カードから今いる場所を選ぶ / Select your current building from the cards
3. 状態（向かっている・建物内・屋外・出た後）を選ぶ / Choose your situation
4. マイクボタンを押して発音練習 / Tap the mic button to practice pronunciation

### GPS測位版

1. スマホでアプリを開く / Open the app on your smartphone
2. 位置情報の使用を許可する / Allow location access
3. SFCキャンパス内を歩く / Walk around the SFC campus
4. 建物に近づくとフレーズが自動表示される / Phrases appear automatically as you approach buildings

---

## 開発背景 / Background

慶應義塾大学 環境情報学部 宮本研究会B2（外国語教授法・AI教材開発）の個別プロジェクトとして開発。  
GPSジオフェンシングを活用した「場所連動型語学学習」の実証実験アプリ。CLT（コミュニカティブ・ランゲージ・ティーチング）およびTBLT（タスク・ベースト・ランゲージ・ティーチング）の理論に基づき、学習者が実際のキャンパス環境でリアルな文脈のもと中国語を使用することを目的としている。

Developed as an individual project within the Miyamoto Seminar B2 (Foreign Language Teaching Methodology & AI-Integrated Educational Material Development), Faculty of Environment and Information Studies, Keio University.
A proof-of-concept app for location-triggered language learning using GPS geofencing. Grounded in CLT (Communicative Language Teaching) and TBLT (Task-Based Language Teaching), the app aims to enable learners to use Chinese in authentic contexts within the real campus environment.

---

## ライセンス / License

MIT
