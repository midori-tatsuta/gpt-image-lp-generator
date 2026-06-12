---
name: gpt-image-lp-generator
description: GPT image2を活用してユーザーが指定した任意テーマ（フィットネス・美容・飲食・SaaS・不動産・スクール等）の高品質ランディングページ（LP）をWebサイトとして自動生成するスキル。「LPを作って」「ランディングページを作りたい」「〇〇のサービスのLPを作って」「参考画像のテイストでLPを作って」などのキーワードが含まれる場合に使用する。GPT image2で全画像を生成し、React + Tailwind CSS + Framer Motionでインタラクティブなウェブサイトとして実装する。ジャンルに応じて背景色・フォント・レイアウト・配色を自動最適化する。
---

# GPT Image LP Generator

ユーザーが指定したテーマ・ブランドの高品質LPを、GPT image2画像生成 → Webサイト実装の一貫フローで作成するスキル。

## ワークフロー概要

```
1. ジャンル判定 → ジャンル別デザイン仕様を選択
2. GPT image2でヒーロー・セクション用画像を一括生成（5〜7枚）
3. webdev_init_projectでReactプロジェクトを初期化
4. 全セクションをHTML/CSS/JSで実装
5. チェックポイント保存 → ユーザーに届ける
```

情報が不明な場合は質問せず推測して進める。

## Step 1: ジャンル判定とデザイン仕様選択

**ジャンル別デザイン詳細は `references/genre-design-guide.md` を参照すること。**

### ジャンル別デザイン概要

| ジャンル | 背景 | Display Font | ラベルFont | 特徴 |
|---------|------|-------------|-----------|------|
| **子ども向けスクール** | ライト（クリーム） | Nunito 900 | DM Mono | 丸み・親しみ・スカイブルー×イエロー |
| **フィットネス** | **ダーク（黒）** | Bebas Neue / Oswald | DM Mono | 斜めクリップ・フルブリード・イエロー |
| **美容Z世代** | **ダーク（黒）** | Cormorant Garamond 300 | DM Mono | プリズム光・非対称・セリフ細字 |
| **美容30代+** | ライト（クリーム） | Playfair Display | Jost | 余白重視・ゴールド・上品 |
| **SaaS・テック** | **ダーク（濃紺）** | Space Grotesk 700 | JetBrains Mono | ダッシュボード風・シアン |
| **飲食・カフェ** | ライト（クリーム） | Cormorant Garamond | DM Mono | フードフォト主役・アンバー |
| **不動産・高級** | ライト（白） | Cormorant Garamond 300 | Jost | 建築的・ゴールド・水平ライン |
| **ウェルネス** | ライト（サンド） | Lato 300 | DM Mono | 有機的・セージグリーン・余白多め |
| **ビジネス・コンサル** | ネイビー | Playfair Display | DM Mono | 権威性・実績数字・ロイヤルブルー |
| **医療・クリニック** | **白** | Noto Sans JP 700 | DM Mono | 清潔感・信頼・ミント |

### 重要: ダーク/ライト背景の判断

ジャンルによって背景色が根本的に異なる。**ダーク背景ジャンルに子ども向けのクリーム背景を使うのは致命的なミス。**

- **ダーク必須**: フィットネス・美容Z世代・SaaS
- **ライト必須**: 子ども向け・飲食・ウェルネス・医療
- **どちらも可**: 不動産・コンサル（ブランドトーンによる）

## Step 2: デザインコンセプト決定

`ideas.md` を作成し、以下を定義する。

### アンチパターン（必ず回避）

- **中央揃えの縦積み** → 非対称グリッドへ
- **均一なカード** → セクションごとに異なる視覚言語
- **Inter フォント** → ジャンル固有のフォントペアリング
- **パープルグラデーション** → ブランドに固有のカラーシステム
- **ジャンル不一致のデザイン** → 子ども向けにダーク背景は禁止

### デザイン方針の定義

- **Design Movement**: 参照する美学
- **Color Philosophy**: メインカラー × アクセント（OKLCH形式）
- **Typography System**: 英語Display + ラベル(モノスペース) + 日本語本文の3種
- **Layout Paradigm**: 非対称2カラム / 編集的グリッド（中央揃えのみ禁止）
- **Signature Elements**: ブランドを象徴する繰り返し要素

## Step 3: GPT image2 画像生成

`generate` ツールで以下を**一括生成**する（5〜7枚）。

| 画像 | アスペクト比 | 用途 |
|------|------------|------|
| `hero_editorial` | 1:1 | ヒーロー左カラム |
| `vertical_model` | 9:16 | ストーリーセクション縦画像 |
| `texture_bg` | 16:9 | テクスチャ背景 |
| `service_1〜3` | 3:4 | サービス/商品カード |

**画像プロンプト原則:**
1. **照明の独自性**: プリズム光・単一光源ドラマ照明・キャウスティック等を指定
2. **構図の意外性**: ガラス越し・液体テクスチャ・俯瞰・部分クローズアップ
3. **参照スタイル明示**: "Vogue Japan editorial", "Dazed & Confused" 等

- **model**: `gpt-image-2`、**quality**: `high` を必ず指定
- 保存先: `/home/ubuntu/webdev-static-assets/<project>_<name>.png`
- 生成後、`manus-upload-file --webdev` でアップロードし、返却された `/manus-storage/...` パスをコードで使用

## Step 4: プロジェクト初期化

```
webdev_init_project(scaffold="web-static", name="<brand>-lp", title="<Brand> - <Tagline>")
```

初期化後、`client/index.html` にGoogle Fontsを追加する。

## Step 5: LP実装

### 必須セクション構成

| # | セクション | 内容 |
|---|-----------|------|
| 1 | **Navbar** | ロゴ + ナビリンク + CTAボタン（スクロールで背景変化） |
| 2 | **Hero** | **非対称2カラム**（左: 画像、右: 極大タイポグラフィ） |
| 3 | **Marquee** | ブランドキーワードの横スクロールテキスト帯 |
| 4 | **Stats** | グリッドボーダーで区切られた数値実績（カウントアップ） |
| 5 | **Features** | **リスト形式**（カードではなく行区切り + 番号 + ホバー） |
| 6 | **Products/Courses** | **オフセットグリッド**（中央カードを下にずらす） |
| 7 | **Story/CTA** | フルブリード画像 + 2カラムコピー |
| 8 | **Testimonials** | 口コミ・保護者の声（ホバーカード） |
| 9 | **FAQ** | アコーディオン形式 |
| 10 | **Contact** | 申し込みフォーム |
| 11 | **Footer** | 4カラム情報 + コピーライト |

### CSS設計の原則

**カラーシステム（ジャンルに応じて変更）:**
```css
/* ライト系（子ども・飲食・ウェルネス等） */
:root {
  --bg:     #faf8f4;    /* ウォームクリーム */
  --ink:    #1a1814;
  --mist:   #e8e4dc;
}

/* ダーク系（フィットネス・SaaS・美容Z世代等） */
:root {
  --bg:     #0a0a0b;    /* ほぼ黒 */
  --chalk:  #f5f3ef;
  --line:   rgba(245,243,239,0.08);
}
```

**タイポグラフィ（3層構造）:**
```css
.type-display  { font-family: var(--font-display); font-size: clamp(3.5rem, 9vw, 8rem); font-weight: 900; line-height: 1.0; }
.type-headline { font-family: var(--font-display); font-size: clamp(2rem, 5vw, 4rem); font-weight: 800; }
.type-label    { font-family: var(--font-mono); font-size: 0.6875rem; letter-spacing: 0.18em; text-transform: uppercase; }
.type-body     { font-family: var(--font-body); font-size: 0.9375rem; line-height: 1.75; }
```

**スクロールリビール（4種類）:**
```css
.reveal       { opacity: 0; transform: translateY(32px); transition: opacity 800ms, transform 800ms cubic-bezier(0.16, 1, 0.3, 1); }
.reveal-left  { opacity: 0; transform: translateX(-40px); transition: opacity 800ms, transform 800ms cubic-bezier(0.16, 1, 0.3, 1); }
.reveal-right { opacity: 0; transform: translateX(40px); transition: opacity 800ms, transform 800ms cubic-bezier(0.16, 1, 0.3, 1); }
.reveal.in, .reveal-left.in, .reveal-right.in { opacity: 1; transform: none; }
```

**マーキー:**
```css
.marquee-track { display: flex; gap: 2rem; animation: marquee 24s linear infinite; white-space: nowrap; width: max-content; }
@keyframes marquee { from { transform: translateX(0); } to { transform: translateX(-50%); } }
```

### React実装の原則

**必須フック（`client/src/hooks/` に作成）:**
```ts
// useReveal: IntersectionObserver + "in" クラス付与（threshold: 0.08）
// useCounter: requestAnimationFrame カウントアップ（threshold: 0.1）
// useScrollProgress: スクロール進捗 0→1
```

**重要: Home.tsx では `useRevealAll()` のみ使用し、独自 Observer を追加しない（重複競合を防ぐ）。**

**Hero（非対称2カラム）:**
```tsx
<section style={{ display: "grid", gridTemplateColumns: "1fr 1fr", minHeight: "100svh" }}>
  <div style={{ position: "relative", overflow: "hidden", minHeight: "100svh" }}>
    <img style={{ width: "100%", height: "100%", objectFit: "cover" }} />
  </div>
  <div style={{ display: "flex", flexDirection: "column", justifyContent: "flex-end", padding: "0 3rem 5rem 2.5rem" }}>
    <h1 className="type-display">...</h1>
  </div>
</section>
```

**Stats（カウントアップ）— レスポンシブ崩れ対策:**
```tsx
// インラインスタイルでgridTemplateColumnsを指定するとメディアクエリが効かない
// 必ず className="stats-grid" + <style>タグで制御する
<div ref={ref} className="stats-grid" style={{ display: "grid", borderTop: "1px solid var(--mist)" }}>
  {/* 各StatItemは独自のopacity/transformアニメーションを持つ（revealクラスは使わない） */}
</div>
<style>{`
  .stats-grid { grid-template-columns: repeat(4, 1fr); }
  @media (max-width: 900px) { .stats-grid { grid-template-columns: repeat(2, 1fr) !important; } }
  @media (max-width: 480px) { .stats-grid { grid-template-columns: 1fr !important; } }
`}</style>
```

**Features（リスト形式）— レスポンシブ崩れ対策:**
```tsx
// 同様にclassName="feature-row" + <style>タグで制御する
<div className="feature-row">
  <div className="feature-num">01</div>
  <div className="feature-title-col">タイトル</div>
  <div className="feature-desc">説明文</div>
</div>
<style>{`
  .feature-row { display: grid; grid-template-columns: 5rem 1fr 2.5fr; }
  @media (max-width: 900px) {
    .feature-row { grid-template-columns: 3rem 1fr !important; }
    .feature-desc { grid-column: 1 / -1; }
  }
`}</style>
```

**Products/Courses（オフセットグリッド）:**
```tsx
// 中央カードを translateY("3rem") でずらし、視覚的テンションを生む
{ courses.map((c, i) => (
  <div style={{ transform: i === 1 ? "translateY(3rem)" : "none" }}>...</div>
))}
```

### アニメーション設計

- **入場**: `opacity: 0 → 1` + `translateY(32px) → 0`、800ms、`cubic-bezier(0.16, 1, 0.3, 1)`
- **遅延スタガー**: `transitionDelay: ${i * 80}ms`（80msずつずらす）
- **ホバー**: ボタンはスライドインク効果、カードは `translateY(-3px)` + border明度アップ
- **マウスパララックス**: Heroで `translate(${mouseX * -8}px, ${mouseY * -6}px)` を画像に適用

## Step 6: チェックポイント & 納品

```
webdev_save_checkpoint(description="<Brand> LP 初回実装完成版")
```

ユーザーへの報告に含める内容:
- 実装したセクション一覧（表形式）
- デザインコンセプト（Design Movement・カラー・フォント）
- 次のステップ提案（3つ、具体的で実装可能なもの）

## 品質チェックリスト

- [ ] **ジャンルに合った背景色**（子ども=クリーム、フィットネス=黒、等）
- [ ] 全画像が `/manus-storage/...` URLで正常表示される
- [ ] Heroが非対称2カラムで、左に画像・右にタイポグラフィ
- [ ] `type-display` が `clamp(3.5rem, 9vw, 8rem)` 以上の極大サイズ
- [ ] `type-label` がモノスペースフォント + 大文字 + 広いletter-spacing
- [ ] Stats/Featuresのレスポンシブが `className` + `<style>` タグで制御されている
- [ ] カウントアップの `threshold: 0.1`（高すぎると発火しない）
- [ ] `Home.tsx` に独自 Observer がない（`useRevealAll()` のみ使用）
- [ ] モバイル（375px）でレイアウト崩れがない
- [ ] TypeScriptエラーがない
- [ ] `prefers-reduced-motion` でアニメーション無効化

## よくある失敗パターンと対処

**ジャンル不一致のデザイン**: 子ども向けにダーク背景、フィットネスにクリーム背景など。`references/genre-design-guide.md` を必ず参照する。

**Stats/Featuresのレスポンシブ崩れ**: インラインスタイルの `gridTemplateColumns` に `@media` が効かない。`className` + `<style>` タグで制御する。

**カウントアップが途中で止まる**: `threshold: 0.3` が高すぎる → `threshold: 0.1` に下げる。`reveal` クラスの `opacity: 0` と競合する場合は、カウンター要素に独自のフェードイン実装を使う。

**重複 IntersectionObserver**: `useRevealAll()` + `Home.tsx` の独自 Observer が競合 → `Home.tsx` の独自 Observer を削除する。

**画像が表示されない**: `manus-upload-file --webdev` 後の `/manus-storage/...` パスを使う（generate_image のCloudFront URLではない）。

**左カラム画像が潰れる**: `minHeight: "100svh"` を左カラムの `div` に設定する。

**フォントが適用されない**: `client/index.html` の `<head>` にGoogle Fontsの `<link>` を追加する。

**「ありきたり」に見える**:
1. 全セクションが中央揃えになっていないか
2. 見出しフォントサイズが `clamp` で十分大きいか
3. `type-label` がモノスペースフォントか
4. 商品グリッドにオフセット（translateY）があるか
5. ジャンルに固有のカラーシステムか（パープルグラデーション禁止）
