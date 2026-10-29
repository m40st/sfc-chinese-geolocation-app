# SFC 中国語フレーズ学習アプリ
**SFC Chinese Phrase Learning App**

慶應義塾大学SFCキャンパス内で、現在地に応じた中国語フレーズを学習できるWebアプリ。  
A location-aware Chinese language learning web app designed for use on the Keio University SFC campus.

🌐 **[Live Demo](https://sfc-chinese-geolocation-app.netlify.app)**

![Status](https://img.shields.io/badge/status-Prototype-orange)
![Status](https://img.shields.io/badge/ステージ-実証実験中-orange)
![Deploy](https://img.shields.io/badge/deploy-Netlify-00C7B7?logo=netlify)
![License](https://img.shields.io/badge/license-MIT-blue)

---

## 現在のステージ / Current Stage

| | |
|---|---|
| **ステージ** | 🔬 プロトタイプ（実証実験中） |
| **目標** | 研究発表版（v1.0）の完成 |
| **場所** | 慶應義塾大学 SFCキャンパス |

> このリポジトリは単一ブランチで継続的にアップデートしている。プロトタイプから研究発表版への変遷はコミット履歴で確認可能。  
> This repository is continuously updated on a single branch. The evolution from prototype to research release can be traced through the commit history.

---

## ロードマップ / Roadmap

```
Phase 1 ──────── Phase 2 ──────────── Phase 3
基盤構築 ✅        精度改善 🔧            研究発表版 🔜
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

### Phase 2 　精度改善 🔧　*現在進行中*

| 課題 | 詳細 |
|------|------|
| 🔧 全建物の座標更新 | Google Maps実測値で推定座標を置き換え |
| 🔧 マップピンのズレ修正 | `g2s()` GPS→SVGピクセル変換の精度改善 |
| 🔧 室内GPS対応 | 精度低下時の建物判定ロジックの安定化 |

---

### Phase 3 　研究発表版（v1.0）🔜　*予定*

| 機能 | 説明 |
|------|------|
| 🔜 学習履歴の可視化 | フレーズ別の練習回数・達成率を表示 |
| 🔜 フレーズ拡充 | CLT・TBLT理論に基づくシナリオ追加 |
| 🔜 マップ改善 | SVG再描画 または Google Maps API 移行の検討 |

---

## 概要 / Overview

SFCキャンパス内を歩きながら、いる場所に合った中国語フレーズが自動的に表示される。発音練習機能（Web Speech API）も搭載しており、実際に声に出して学習することができる。

As you walk around the SFC campus, the app automatically displays Chinese phrases relevant to your current location. It also features pronunciation practice powered by the Web Speech API, so you can learn by speaking aloud.

---

## 機能 / Features

- **位置連動フレーズ表示** — GPS・QZSSを使い、キャンパス内の建物を検出して場所に合ったフレーズを表示  
  **Location-aware phrases** — Detects nearby campus buildings via GPS/QZSS and shows contextually relevant phrases

- **発音練習** — Web Speech APIによる中国語（普通話）の音声認識で発音を評価  
  **Pronunciation practice** — Evaluates your Mandarin pronunciation using the Web Speech API (zh-CN)

- **屋内/屋外判定** — GPS精度と移動状態から屋内・屋外・接近中・離脱中を自動判定  
  **Indoor/outdoor detection** — Automatically detects whether you're inside, outside, approaching, or leaving a building

- **学習履歴** — 練習したフレーズの履歴をローカルに保存  
  **Study history** — Saves your practice history locally in the browser

- **キャンパスマップ** — SVGマップ上に現在地と最寄り建物をリアルタイム表示  
  **Campus map** — Displays your current location and nearest building on an SVG campus map

---

## 対応建物 / Supported Buildings

| 建物名 | 概要 | 座標ステータス |
|--------|------|---------------|
| バス停A・B | キャンパス入口 | 推定値 |
| Μ館（メディアセンター） | 図書館・メディア施設 | 推定値 |
| Α館 | 本館・学事・ウェルネス | 推定値 |
| Σ館 | 食堂・購買・コンビニ | 推定値 |
| 講義棟（κ・ε・ι・ο・λ・Θ） | 各種講義室 | **QZSS実測済み** |
| τ館 | 大学院棟 | **QZSS実測済み** |
| Γ館 | 体育館 | 推定値 |
| βヴィレッジ | 学生寮エリア | 推定値 |
| 鴨池・学生ラウンジ | ガリバー池・サブウェイ | 推定値 |

「推定値」の建物は今後Google Maps実測値への更新を予定している。  
Buildings marked "推定値" (estimated) are planned to be updated with accurate Google Maps coordinates.

---

## 技術構成 / Tech Stack

| 項目 | 内容 |
|------|------|
| 言語 | HTML / CSS / JavaScript（フレームワークなし） |
| 位置情報 | `navigator.geolocation` API（QZSS対応） |
| 距離計算 | Haversine formula |
| 音声認識 | Web Speech API（`zh-CN`） |
| フォント | Noto Sans JP（Google Fonts） |
| デザイン | デジタル庁デザインシステム準拠（純黒背景・最小14px） |
| ホスティング | Netlify（GitHub連携による自動デプロイ） |
| データ保存 | `localStorage`（サーバーなし） |

**No frameworks used** — Pure HTML/CSS/JS single-file app. No build tools, no npm, no backend.

---

## GPS・位置検出の仕組み / How Location Detection Works

```
スマホのGPS/QZSS
      ↓
navigator.geolocation.watchPosition()
      ↓
Haversine formula で各建物との距離を計算
      ↓
最近傍建物が検出半径(r)以内 → 建物を検出
      ↓
建物ごとのフレーズを表示
```

建物座標はQZSS（±3〜4m精度）による現地実測値を一部使用。QZSSは日本の準天頂衛星システムで、日本国内では通常のGPSより高精度な位置情報を提供する。  
Some building coordinates are based on on-site measurements using QZSS (±3–4m accuracy). QZSS (Quasi-Zenith Satellite System) is Japan's own satellite positioning system, providing higher accuracy than standard GPS within Japan.

---

## 使い方 / How to Use

1. スマホでアプリを開く / Open the app on your smartphone
2. 位置情報の使用を許可する / Allow location access
3. SFCキャンパス内を歩く / Walk around the SFC campus
4. 建物に近づくとフレーズが表示される / Phrases appear as you approach buildings
5. 「フレーズ練習を始める」でマイクを使って発音練習 / Tap "Start Practice" to practice pronunciation

> ⚠️ **注意 / Note**  
> 位置情報の精度向上のため、スマホの位置情報設定を「高精度」モードにすることが必須。  
> For best accuracy, set your phone's location mode to "High accuracy" (GPS + Wi-Fi + Cell).

---

## アクセス / Access

🌐 **[https://sfc-chinese-geolocation-app.netlify.app](https://sfc-chinese-geolocation-app.netlify.app)**

ブラウザでURLを開くだけで動作する。インストール不要。  
Just open the URL in your browser. No installation required.

> 開発者向け：`sfc_app.html` 単体ファイルで完結している。クローンしてHTTPSサーバー上で動かすこと（位置情報APIはHTTPS必須）。  
> For developers: the app is a single self-contained file (`sfc_app.html`). Clone the repo and serve it over HTTPS (Geolocation API requires HTTPS).

---

## 開発背景 / Background

慶應義塾大学 環境情報学部 宮本研究会B2（外国語教授法・AI教材開発）の個別プロジェクトとして開発。  
GPSジオフェンシングを活用した「場所連動型語学学習」の実証実験アプリ。CLT（コミュニカティブ・ランゲージ・ティーチング）およびTBLT（タスク・ベースト・ランゲージ・ティーチング）の理論に基づき、学習者が実際のキャンパス環境でリアルな文脈のもと中国語を使用することを目的としている。

Developed as part of Professor Miyamoto's seminar B2 at Keio SFC, focused on foreign language teaching methodology and AI-integrated educational material development. This app serves as a proof-of-concept for location-triggered language learning using GPS geofencing, grounded in CLT (Communicative Language Teaching) and TBLT (Task-Based Language Teaching) principles.

---

## ライセンス / License

MIT
