---
name: gpt-image-lp-generator
description: GPT image2を活用してユーザーが指定した任意テーマ（フィットネス・美容・飲食・SaaS・不動産・スクール等）の高品質ランディングページ（LP）をWebサイトとして自動生成するスキル。「LPを作って」「ランディングページを作りたい」「〇〇のサービスのLPを作って」「参考画像のテイストでLPを作って」などのキーワードが含まれる場合に使用する。GPT image2で全画像を生成し、React + Tailwind CSS + Framer Motionでインタラクティブなウェブサイトとして実装する。
---

# GPT Image LP Generator

ユーザーが指定したテーマ・ブランドの高品質LPを、GPT image2画像生成 → Webサイト実装の一貫フローで作成するスキル。

## ワークフロー概要

```
1. ユーザーからテーマ・ブランド情報を収集
2. デザインコンセプトを決定（ブランドカラー・フォント・レイアウト）
3. GPT image2でヒーロー・セクション用画像を一括生成（5〜7枚）
4. webdev_init_projectでReactプロジェクトを初期化
5. 全セクションをHTML/CSS/JSで実装
6. チェックポイント保存 → ユーザーに届ける
```

## Step 1: 情報収集

ユーザーから以下を把握する（不明な場合は質問せず推測して進める）:

| 項目 | 例 |
|------|-----|
| サービス名・ブランド名 | POWER GYM / BeautyLab / TechFlow |
| ジャンル | フィットネス / 美容 / SaaS / 飲食 / 不動産 / スクール |
| ターゲット | 20代女性 / ビジネスマン / 主婦 |
| 参考画像・テイスト | 添付画像 / 「クール」「ポップ」「高級感」 |
| キーカラー | 指定がなければジャンルに合わせて選定 |
| CTAゴール | 無料体験 / 資料請求 / 購入 / 会員登録 |

情報が揃ったら質問なしで即実装に進む。

## Step 2: デザインコンセプト決定

`ideas.md` を作成し、以下を定義する:

- **Design Movement**: 参照する美学（例: アグレッシブ・スポーツグラフィック / ラグジュアリー・ミニマル / ポップ・ビビッド）
- **Color Philosophy**: メインカラー × アクセント1 × アクセント2（OKLCH形式でCSS変数化）
- **Typography**: 英語見出し用フォント + 日本語フォント（Google Fonts）
- **Layout Paradigm**: フルスクリーン縦スクロール / 非対称グリッド / サイドバー型
- **Signature Elements**: ブランドを象徴する繰り返し要素（ブラシストローク / グラデーションライン / 幾何学パターン等）

**ジャンル別デザイン推奨:**

| ジャンル | カラー推奨 | フォント推奨 | 雰囲気 |
|---------|-----------|------------|--------|
| フィットネス・スポーツ | 黒×黄×青 | Bebas Neue + Noto Sans JP | アグレッシブ・エネルギッシュ |
| 美容・コスメ | ピンク×ゴールド×白 | Playfair Display + Noto Serif JP | エレガント・フェミニン |
| SaaS・テック | 濃紺×シアン×白 | Space Grotesk + Noto Sans JP | クリーン・プロフェッショナル |
| 飲食・カフェ | ブラウン×クリーム×緑 | Cormorant Garamond + Noto Serif JP | ウォーム・ナチュラル |
| 不動産・高級 | 黒×ゴールド×白 | Cormorant Garamond + Noto Serif JP | ラグジュアリー・信頼感 |
| スクール・教育 | 青×オレンジ×白 | Oswald + Noto Sans JP | 活気・信頼・成長 |
| ウェルネス・ヨガ | 緑×ベージュ×白 | Lato + Noto Sans JP | 穏やか・ナチュラル |

## Step 3: GPT image2 画像生成

`generate` ツールで以下の画像を**一括生成**する（並列で5〜7枚）:

### 必須画像セット

| 画像 | アスペクト比 | 用途 |
|------|------------|------|
| `hero_bg` | 16:9 | ヒーローセクション背景（人物 + ブランドカラー光源） |
| `service_1` | 3:4 | サービス/プログラム紹介カード1 |
| `service_2` | 3:4 | サービス/プログラム紹介カード2 |
| `service_3` | 3:4 | サービス/プログラム紹介カード3 |
| `cta_person` | 3:4 | CTAセクション用人物（喜び・達成感の表情） |

必要に応じて `feature_bg`（特徴セクション背景）や `testimonial_person`（お客様の声用）を追加する。

### 画像プロンプト設計の原則

- **人物**: ターゲット層に合った人種・年齢・表情を明示する（例: "Japanese female, 25-30 years old, confident expression"）
- **照明**: ブランドカラーに合わせた光源を指定する（例: "dramatic blue and yellow rim lighting"）
- **背景**: ブランドの世界観を反映する（例: "dark gym interior", "minimalist white studio", "urban rooftop at night"）
- **品質**: 末尾に必ず `cinematic photography, professional quality, high contrast, no text` を付加する
- **model**: `gpt-image-2`、**quality**: `high` を必ず指定する
- **保存先**: `/home/ubuntu/webdev-static-assets/<project-name>_<image-name>.png`

生成後、ツールが返すCloudFront URLをそのままコードで使用する（ローカルパス不可）。

## Step 4: プロジェクト初期化

```
webdev_init_project(
  scaffold="web-static",
  name="<brand-name>-lp",
  title="<Brand Name> - <Tagline>"
)
```

初期化後、`client/index.html` にGoogle Fontsを追加する。

## Step 5: LP実装

### 必須セクション構成

| # | セクション | 内容 |
|---|-----------|------|
| 1 | **Navbar** | ロゴ + ナビリンク + CTAボタン（スクロールで背景変化） |
| 2 | **Hero** | フルスクリーン背景画像 + 大型見出し + サブコピー + CTAボタン2つ |
| 3 | **Stats/Trust** | 数値実績のカウントアップアニメーション（3〜4指標） |
| 4 | **Features** | ブランドの特徴・強み（4カード） |
| 5 | **Services/Programs** | サービス・プログラム紹介（画像カード × 3〜4） |
| 6 | **CTA/Join** | 入会・申込案内 + 特典 + 人物画像 |
| 7 | **Contact Form** | 申込フォーム（送信後サンクスメッセージ） |
| 8 | **Footer** | ロゴ + ナビ + コピーライト |

### CSS設計の原則

`client/src/index.css` で以下を定義する:

- ブランドカラーをCSS変数（`--brand-primary`, `--brand-accent`, `--brand-bg`）で管理する
- `font-display`（英語大見出し）/ `font-heading`（日本語見出し）/ `font-body`（本文）の3クラスを定義する
- `.btn-primary` をclip-pathやborder-radiusでブランドに合わせた形状にする
- `.feature-card` にhoverアニメーション（translateY + border-color変化）を付ける
- `@keyframes fadeInUp / fadeInLeft / scaleIn` を定義し、IntersectionObserverと連携する
- `ThemeProvider defaultTheme="dark"` を使用する場合、`.dark {}` のCSS変数と必ず一致させる

### React実装の原則

- `useInView` フック（IntersectionObserver、threshold=0.15）でスクロール時にアニメーション発火
- `useCounter` フックで統計数値のカウントアップ（requestAnimationFrame使用）
- Navbar: `scrollY > 50` でbackdrop-blur + border追加
- フォーム: `useState(submitted)` でサンクスメッセージ切り替え
- 画像は全てCloudFront URLを定数として先頭に定義する

### アニメーション設計

- **入場**: `opacity: 0 → 1` + `translateY(40px) → 0`、duration 700ms、easing `cubic-bezier(0.23, 1, 0.32, 1)`
- **遅延**: 各カードに `transitionDelay: ${i * 100}ms` でスタガー
- **ホバー**: ボタン `scale(1.03)` + glow shadow、カード `translateY(-4px)` + border変化
- **カウンター**: `requestAnimationFrame` で2秒かけてカウントアップ

## Step 6: チェックポイント & 納品

```
webdev_save_checkpoint(description="<Brand> LP 初回実装完成版")
```

ユーザーへの報告に含める内容:
- 実装したセクション一覧
- デザインコンセプト（カラー・フォント）
- 次のステップ提案（料金プラン追加 / お客様の声 / Google Maps等）

## 品質チェックリスト

- [ ] 全画像がCloudFront URLで正常表示される
- [ ] モバイル（375px）でレイアウト崩れがない
- [ ] スクロールアニメーションが各セクションで発火する
- [ ] CTAボタンがフォームセクションにアンカーリンクされている
- [ ] フォーム送信後にサンクスメッセージが表示される
- [ ] Navbarがスクロール時に背景変化する
- [ ] TypeScriptエラーがない（LSPチェック）

## よくある失敗パターンと対処

**画像が表示されない**: ローカルパスではなくCloudFront URLを使用しているか確認する。`generate_image` ツールが返すURLをそのまま使う。

**フォントが適用されない**: `client/index.html` の `<head>` にGoogle Fontsの `<link>` が追加されているか確認する。

**アニメーションが動かない**: IntersectionObserverのthresholdが高すぎる場合は0.1〜0.15に下げる。

**モバイルでテキストが大きすぎる**: 見出しに `clamp(最小px, vw値, 最大px)` を使用する。

**ダークテーマで文字が見えない**: `ThemeProvider defaultTheme="dark"` と `index.css` の `.dark {}` のCSS変数が一致しているか確認する。
