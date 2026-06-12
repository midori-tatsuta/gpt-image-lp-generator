# ジャンル別LPデザイン詳細ガイド

各ジャンルのデザイン仕様を定義する。SKILL.mdのStep 2で参照すること。

---

## ジャンル判定フロー

ユーザーの依頼からジャンルを判定し、対応するセクションを参照する。

| キーワード例 | ジャンル |
|------------|---------|
| 英会話・塾・習い事・スクール・子ども | 子ども向けスクール |
| フィットネス・ジム・筋トレ・ダイエット | フィットネス |
| 美容・コスメ・スキンケア・サロン | 美容・コスメ |
| SaaS・ツール・アプリ・テック・AI | SaaS・テック |
| カフェ・レストラン・飲食・料理 | 飲食・カフェ |
| 不動産・マンション・物件・住宅 | 不動産・高級 |
| ヨガ・瞑想・ウェルネス・マインドフル | ウェルネス |
| コーチング・コンサル・ビジネス | ビジネス・コンサル |
| 医療・クリニック・歯科・健康 | 医療・クリニック |
| EC・ファッション・アパレル | EC・ファッション |

---

## 1. 子ども向けスクール（英会話・塾・習い事）

**Design Movement**: Playful Editorial Luxury — 子供の「楽しさ」と保護者の「信頼感」を両立

### カラーシステム
```css
:root {
  --primary: oklch(0.72 0.12 220);   /* スカイブルー */
  --accent:  oklch(0.82 0.20 85);    /* サンイエロー */
  --leaf:    oklch(0.65 0.14 145);   /* リーフグリーン */
  --bg:      #faf8f4;                /* ウォームクリーム */
  --bg-mid:  #f0ece4;
  --ink:     #1a1814;
  --mist:    #e8e4dc;
}
```

### フォント
- **Display**: Nunito (900) — 丸みがあり親しみやすい
- **Label**: DM Mono — 数字・ラベルに信頼感
- **Body**: Noto Sans JP — 日本語の読みやすさ

### レイアウト
- Hero: 非対称2カラム（左: 子供の自然な笑顔写真、右: 極大タイポ）
- Stats: 4カラムグリッドボーダー（カウントアップ）
- Features: 3カラムリスト（番号 + タイトル + 説明）
- Courses: オフセットカードグリッド（中央カードを下にずらす）
- Testimonials: 保護者の声（ホバーカード）

### ヒーロー文言パターン
- 「Every Child is a Star」
- 「英語が好きになる場所」
- 「楽しいから、続けられる」

### CTA
- 「無料体験レッスン」（メイン）
- 「コースを見る」（サブ）

### 画像プロンプト（hero_editorial）
```
Warm natural light children's education editorial. 
Japanese child aged 6-8, bright genuine smile, sitting at desk with colorful books. 
Soft cream and sky blue tones. Shallow depth of field. 
Clean, inviting atmosphere. No text, no logos. High quality.
```

---

## 2. フィットネス・スポーツ

**Design Movement**: Brutalist Athletic — 力強さと動きのエネルギー

### カラーシステム
```css
:root {
  --ink:     #0a0a0b;
  --chalk:   #f5f3ef;
  --accent:  oklch(0.82 0.22 85);    /* 強いイエロー */
  --surface: #111113;
  --line:    rgba(245,243,239,0.08);
}
```

### フォント
- **Display**: Bebas Neue または Oswald (700) — 力強い大文字
- **Label**: DM Mono
- **Body**: Inter または Noto Sans JP

### レイアウト
- **ダーク背景必須** (`background: var(--ink)`)
- Hero: フルブリード画像 + 斜めクリップパス (`clip-path: polygon(0 0, 100% 0, 100% 92%, 0 100%)`)
- Stats: 横一列 + 大きな数字
- Features: ダーク背景 + イエローアクセント
- CTA: イエロー背景 + 黒テキスト

### ヒーロー文言パターン
- 「UNLEASH YOUR POTENTIAL」
- 「限界を超えろ」
- 「NO LIMITS」

### 画像プロンプト（hero_editorial）
```
High contrast athletic editorial. Muscular figure in dynamic motion, 
dramatic single-source side lighting, deep shadows. 
Matte black background. Cinematic, powerful. 
Dazed & Confused magazine aesthetic. No text, no logos. 8K.
```

---

## 3. 美容・コスメ（Z世代向け）

**Design Movement**: Post-Digital Luxury Editorial

### カラーシステム
```css
:root {
  --ink:     #0a0a0b;
  --chalk:   #f5f3ef;
  --accent:  oklch(0.78 0.15 320);   /* プリズムピンク */
  --surface: #0f0f10;
  --line:    rgba(245,243,239,0.06);
}
```

### フォント
- **Display**: Cormorant Garamond (300) — 繊細なセリフ体
- **Label**: DM Mono
- **Body**: Jost または Noto Sans JP

### レイアウト
- **ダーク背景必須**
- Hero: 非対称2カラム（左: プリズム光の人物写真）
- Products: 3カラムオフセットグリッド
- Story: フルブリード + テキストオーバーレイ

### 画像プロンプト（hero_editorial）
```
Ultra high-end beauty editorial. Young East Asian woman, 
face partially obscured by iridescent glass panel. 
Prismatic rainbow light refracts across her skin. 
Pure matte black background. Dramatic single-source side lighting. 
Vogue Japan aesthetic. No text, no logos. 8K, cinematic.
```

---

## 4. 美容・コスメ（30代以上・高級）

**Design Movement**: Organic Wabi-Sabi Luxury

### カラーシステム
```css
:root {
  --cream:   #f7f3ee;
  --gold:    oklch(0.78 0.10 85);
  --ink:     #2a2420;
  --mist:    #e8e0d4;
  --surface: #f0ebe3;
}
```

### フォント
- **Display**: Playfair Display (400/700) — 上品なセリフ体
- **Label**: Jost (300)
- **Body**: Noto Serif JP または Noto Sans JP

### レイアウト
- **ライト背景（クリーム）**
- Hero: 余白重視 + 中央揃え（例外的に許可）
- 全体的に余白多め、ゆったりとした印象

---

## 5. SaaS・テック

**Design Movement**: Data-Driven Precision

### カラーシステム
```css
:root {
  --ink:     #0a0c10;
  --surface: #0f1117;
  --surface2:#161b27;
  --cyan:    oklch(0.78 0.15 200);
  --chalk:   #e8edf5;
  --line:    rgba(100,120,160,0.12);
}
```

### フォント
- **Display**: Space Grotesk (700) または Inter (800)
- **Label**: JetBrains Mono
- **Body**: Inter または Noto Sans JP

### レイアウト
- **ダーク背景必須**
- Hero: ダッシュボード風スクリーンショット + 左テキスト
- Features: アイコン + 説明のグリッド
- Stats: データビジュアライゼーション風

### 特徴的要素
- コードスニペット表示
- 点線グリッドパターン背景
- シアン/ブルーのグロー効果

---

## 6. 飲食・カフェ

**Design Movement**: Artisan Warmth Editorial

### カラーシステム
```css
:root {
  --espresso: #2c1a0e;
  --cream:    #f5ede0;
  --warm:     oklch(0.72 0.12 55);   /* アンバー */
  --leaf:     oklch(0.55 0.12 145);
  --mist:     #e8ddd0;
}
```

### フォント
- **Display**: Cormorant Garamond (300/700) — 食の上品さ
- **Label**: DM Mono
- **Body**: Noto Serif JP

### レイアウト
- **ライト背景（クリーム）**
- Hero: フードフォト主役（フルブリード）
- Menu: 縦長カード + 価格表示
- Story: シェフ/オーナーの写真 + コピー

---

## 7. 不動産・高級

**Design Movement**: Architectural Minimalism

### カラーシステム
```css
:root {
  --ink:   #0a0a0b;
  --chalk: #f8f6f2;
  --gold:  oklch(0.78 0.10 85);
  --line:  rgba(10,10,11,0.08);
}
```

### フォント
- **Display**: Cormorant Garamond (300) — 建築的な細さ
- **Label**: Jost (300)
- **Body**: Noto Sans JP

### レイアウト
- **ライト背景（ほぼ白）**
- Hero: 物件写真フルブリード + 薄いオーバーレイ
- 水平ラインで区切るシンプルな構成

---

## 8. ウェルネス・ヨガ

**Design Movement**: Organic Breathing Space

### カラーシステム
```css
:root {
  --sage:   oklch(0.72 0.08 145);
  --sand:   #f0ebe0;
  --earth:  #8a7a60;
  --cream:  #faf7f2;
  --mist:   #e4ddd0;
}
```

### フォント
- **Display**: Lato (300/700) または Cormorant Garamond
- **Label**: DM Mono
- **Body**: Noto Sans JP

### レイアウト
- **ライト背景（クリーム/サンド）**
- 余白を多く取る
- 有機的な曲線（border-radius多め）
- 自然素材・植物の写真

---

## 9. ビジネス・コンサル

**Design Movement**: Executive Precision

### カラーシステム
```css
:root {
  --navy:   #0a1628;
  --chalk:  #f5f7fa;
  --accent: oklch(0.65 0.15 250);   /* ロイヤルブルー */
  --gold:   oklch(0.78 0.10 85);
  --line:   rgba(10,22,40,0.08);
}
```

### フォント
- **Display**: Playfair Display または Libre Baskerville
- **Label**: DM Mono
- **Body**: Noto Sans JP

### レイアウト
- **ネイビーまたはライト背景**
- 信頼感・権威性を前面に
- 実績・数字を大きく表示

---

## 10. 医療・クリニック

**Design Movement**: Clinical Trust

### カラーシステム
```css
:root {
  --white:  #ffffff;
  --blue:   oklch(0.65 0.12 230);
  --mint:   oklch(0.85 0.06 175);
  --ink:    #1a2030;
  --line:   rgba(26,32,48,0.08);
}
```

### フォント
- **Display**: Noto Sans JP (700) または Poppins
- **Label**: DM Mono
- **Body**: Noto Sans JP

### レイアウト
- **白背景必須**
- 清潔感・信頼感を最優先
- アイコン多用
- 医師・スタッフ写真

---

## レイアウト選定マトリクス

| 背景 | ターゲット感情 | 推奨ジャンル |
|-----|-------------|------------|
| ダーク（黒/濃紺） | 高級感・力強さ・クール | フィットネス・美容Z世代・SaaS・不動産 |
| ライト（クリーム/白） | 親しみ・信頼・温かさ | 子ども・飲食・ウェルネス・医療 |
| ミッドトーン（グレー） | プロフェッショナル | コンサル・B2B |

---

## よくある崩れパターンと対処

### Stats 4カラムが崩れる
- `gridTemplateColumns` をインラインスタイルで指定すると `@media` セレクタが効かない
- 解決: `className="stats-grid"` + `<style>` タグで `.stats-grid` にメディアクエリを適用

### Features 3カラムが右に偏る
- インラインスタイルの `gridTemplateColumns` に `@media` が効かない
- 解決: `className="feature-row"` + `<style>` タグで制御

### カウントアップが途中で止まる
- `IntersectionObserver` の `threshold: 0.3` が高すぎる
- 解決: `threshold: 0.1` に下げる
- `reveal` クラスの `opacity: 0` と競合する場合は、カウンター要素に `reveal` クラスを使わず、独自のフェードイン実装を使う

### 重複 IntersectionObserver
- `useRevealAll()` を使いつつ `Home.tsx` でも独自 Observer を作ると競合する
- 解決: `useRevealAll()` のみ使用し、`Home.tsx` の独自 Observer を削除する
