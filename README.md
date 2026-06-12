# gpt-image-lp-generator

**Manus Skill** — GPT image2を活用してジャンル別に最適化された高品質ランディングページ（LP）を自動生成するスキル。

## 概要

ユーザーが指定したテーマ・ブランドのLPを、GPT image2による画像生成 → React + Tailwind CSS実装の一貫フローで作成します。

**10ジャンルに対応し、ジャンルごとに最適なデザインを自動選択します。**

| ジャンル | 背景 | フォント | 特徴 |
|---------|------|---------|------|
| 子ども向けスクール | ライト（クリーム） | Nunito | 親しみ・スカイブルー×イエロー |
| フィットネス | ダーク（黒） | Bebas Neue | 斜めクリップ・力強さ |
| 美容（Z世代） | ダーク（黒） | Cormorant Garamond | プリズム光・セリフ細字 |
| 美容（30代+） | ライト（クリーム） | Playfair Display | 余白重視・ゴールド |
| SaaS・テック | ダーク（濃紺） | Space Grotesk | ダッシュボード風・シアン |
| 飲食・カフェ | ライト（クリーム） | Cormorant Garamond | フードフォト主役 |
| 不動産・高級 | ライト（白） | Cormorant Garamond | 建築的・水平ライン |
| ウェルネス | ライト（サンド） | Lato | 有機的・余白多め |
| ビジネス・コンサル | ネイビー | Playfair Display | 権威性・実績数字 |
| 医療・クリニック | 白 | Noto Sans JP | 清潔感・信頼 |

## ファイル構成

```
gpt-image-lp-generator/
├── SKILL.md                        # メインスキル定義（ワークフロー・実装ガイド）
└── references/
    └── genre-design-guide.md       # ジャンル別デザイン詳細仕様
```

## 使い方

このスキルは [Manus](https://manus.im) のスキル機能として動作します。

1. `SKILL.md` をManusのスキルとして登録する
2. Manusに「〇〇のLPを作って」と依頼する
3. ジャンルが自動判定され、最適なデザインでLPが生成される

## 生成されるLP構成

1. **Navbar** — ロゴ + ナビリンク + CTAボタン
2. **Hero** — 非対称2カラム（左: 画像、右: 極大タイポグラフィ）
3. **Marquee** — ブランドキーワードの横スクロール帯
4. **Stats** — 数値実績カウントアップ
5. **Features** — リスト形式（番号 + ホバー）
6. **Products/Courses** — オフセットグリッド
7. **Story/CTA** — フルブリード画像 + コピー
8. **Testimonials** — 口コミ・保護者の声
9. **FAQ** — アコーディオン
10. **Contact** — 申し込みフォーム
11. **Footer** — 4カラム情報

## 技術スタック

- **フレームワーク**: React 19 + TypeScript
- **スタイリング**: Tailwind CSS 4
- **アニメーション**: Framer Motion + CSS Transitions
- **画像生成**: GPT image-2 (high quality)
- **ホスティング**: Manus WebDev

## ライセンス

MIT
