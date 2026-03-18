# Hugo Ananke カスタマイズ詳解

> 対象: Hugo の `gohugo-theme-ananke` を使っている、またはこれから使う開発者
>
> 想定バージョン: 2025年以降の Ananke ドキュメント系統

---

## 1. 定義

**Ananke** は Hugo 用の汎用テーマで、ブログ、コーポレートサイト、ドキュメント寄りサイトなどの土台として使いやすい「スターターテーマ」です。見た目を一から作り込むより、**既定レイアウトを活かしつつ、設定・CSS・部分テンプレートのオーバーライドで育てていく**のに向いています。

Ananke のカスタマイズは大きく次の4層で考えると整理しやすいです。

1. **設定ファイルで変える**  
   サイト名、ロゴ、本文色、背景、ソーシャルリンク、共有ボタン、日付形式など。
2. **Front Matter でページ単位に変える**  
   ヒーロー画像、共有無効化、テキスト色、レイアウト切替など。
3. **CSS を足して見た目を変える**  
   既存テーマの上に追加 CSS / SCSS を重ねる。
4. **レイアウトをオーバーライドする**  
   `layouts/` 側で partial や single/list テンプレートを差し替える。

Ananke は Tachyons ベースのユーティリティクラスを使う設計なので、**「設定 + Tachyons クラス + 必要な所だけ独自 CSS」** が基本戦略になります。

---

## 2. 要点

### 2.1 まず押さえるべき実務ポイント

- **テーマ本体は直接編集しない**。`themes/ananke` をいじるとアップデート時に衝突しやすい。原則は `config/`, `assets/`, `layouts/`, `static/` 側で上書きする。
- **CSS 追加は `assets/ananke/css` を使う**。Ananke は Hugo Pipes の Asset Bundling で CSS をまとめる。
- **Custom CSS は Hugo Extended 前提で考える**。通常版 Hugo では期待どおり効かないケースがある。
- **色や余白の多くは Tachyons クラスで制御できる**。無理に全部 CSS で殴らない。
- **ヒーロー画像やヘッダ表示は Front Matter でかなり制御できる**。
- **共有ボタンと SNS フォローは最近の Ananke では `params.ananke.social` 以下に寄っている**。
- **ページ単位の調整は Front Matter、全体方針は config、構造変更は layouts** で分離すると保守しやすい。

---

## 3. 比較: どこでカスタマイズするべきか

| 手段 | 向いている用途 | 影響範囲 | 保守性 | 典型例 |
|---|---|---:|---:|---|
| `params` | 全体設定 | サイト全体 | 高い | ロゴ、本文色、日付形式 |
| Front Matter | ページ個別調整 | 単一ページ/セクション | 高い | 特定ページだけヘッダ非表示 |
| `custom_css` | 見た目の微調整 | サイト全体または対象要素 | 中 | フォントサイズ、カード余白 |
| `layouts/partials` 上書き | HTML 構造の変更 | 広い | 中〜低 | ヘッダ構造変更、head内追記 |
| テーマ本体編集 | 緊急避難 | 不定 | 低い | 非推奨 |

---

## 4. ディレクトリ構成の基本

```text
my-site/
├─ assets/
│  └─ ananke/
│     └─ css/
│        ├─ custom.css
│        └─ overrides.css
├─ config/
│  └─ _default/
│     ├─ hugo.toml
│     └─ params.toml
├─ content/
├─ layouts/
│  ├─ _default/
│  └─ partials/
│     └─ head-additions.html
├─ static/
│  ├─ img/
│  │  └─ logo.svg
│  └─ images/
└─ themes/
   └─ ananke/
```

最近の Ananke ドキュメントでは、`config/_default/hugo.toml` や `config/_default/params.toml` に分ける例が多く、**設定の責務分離**に向いています。

---

## 5. まず入れておくとよい基本設定

以下は TOML 例です。

```toml
baseURL = 'https://example.com/'
languageCode = 'ja-jp'
title = 'My Site'
theme = 'ananke'

[params]
  site_logo = 'img/logo.svg'
  body_classes = 'avenir bg-near-white'
  post_content_classes = 'serif'
  text_color = 'dark-gray'
  background_color_class = 'bg-black'
  featured_image_class = 'cover bg-center'
  cover_dimming_class = 'bg-black-40'
  show_reading_time = true
  date_format = ':date_long'
  read_more_copy = '続きを読む'
  custom_css = ['custom.css', 'overrides.css']
```

### ポイント

- `site_logo` は `static/` 配下の相対パスを指定。
- `body_classes` はサイト全体の `<body>` クラス。
- `post_content_classes` は投稿本文のタイポグラフィ調整に使う。
- `text_color` は本文色。Tachyons の色クラス名を使う。
- `background_color_class` はヒーロー画像がない場合の背景色。
- `featured_image_class` はヒーロー画像の収まり方・位置合わせ。
- `cover_dimming_class` はヒーロー画像のオーバーレイ濃度。
- `show_reading_time` で読了時間と語数を表示。
- `read_more_copy` は「続きを読む」相当の文言を差し替える。

---

## 6. ヘッダ・ヒーロー領域のカスタマイズ

### 6.1 定義

Ananke の「ヒーロー」は、ページ上部の大きなビジュアル領域です。ページごとの `featured_image` と、サイト全体の背景クラス／表示クラスで見た目が決まります。

### 6.2 サイト全体設定

```toml
[params]
  background_color_class = 'bg-dark-blue'
  featured_image_class = 'cover bg-center'
  cover_dimming_class = 'bg-black-30'
```

### 6.3 ページ単位設定

```yaml
---
title: "製品紹介"
featured_image: "/images/hero-product.jpg"
omit_header_text: false
cover_dimming_class: "bg-black-20"
featured_image_class: "cover bg-top"
---
```

### 6.4 実務上の見方

- `featured_image` を指定すると、そのページだけヒーロー画像を差し替えられます。
- `omit_header_text: true` にすると、画像上のヘッダ文字を消せます。
- 画像がない場合は `background_color_class` が効きます。
- ページリソースを使う場合、Ananke は `featured_image` 名に一致する画像や、`cover` / `feature` を含む画像を探す動作があります。

### 6.5 具体例: ランディングページ風にする

```yaml
---
title: "Hugo導入支援"
featured_image: "/images/landing.jpg"
featured_image_class: "cover bg-center"
cover_dimming_class: "bg-black-50"
text_color: "white"
---
```

この組み合わせで、**上部は強いビジュアル、本文は読みやすさ優先**の構成にしやすいです。

---

## 7. ロゴ・サイト名・本文色

### 7.1 ロゴ

```toml
[params]
  site_logo = 'img/logo.svg'
```

ロゴファイルは `static/img/logo.svg` に置くのが分かりやすいです。

### 7.2 本文色

```toml
[params]
  text_color = 'dark-gray'
```

ページ個別に変える場合:

```yaml
---
title: "注意事項"
text_color: "near-black"
---
```

### 7.3 body クラスと本文クラス

```toml
[params]
  body_classes = 'helvetica bg-near-white'
  post_content_classes = 'serif'
```

`body_classes` は全体、`post_content_classes` は本文に寄るため、**UI 部品は sans-serif、本文は serif** のような分離がしやすいです。

---

## 8. CSS カスタマイズ

### 8.1 定義

Ananke は Hugo Pipes でテーマ CSS を束ねて出力します。追加 CSS は `assets/ananke/css/` に置き、`params.custom_css` で登録します。

### 8.2 基本手順

#### 1) ファイルを置く

```text
assets/ananke/css/custom.css
assets/ananke/css/overrides.css
```

#### 2) 登録する

```toml
[params]
  custom_css = ['custom.css', 'overrides.css']
```

### 8.3 実務上の注意

- 登録順に結合されるため、**後ろのファイルほど上書き向き**。
- 登録ファイルは同種で揃える。たとえば全部 `css`、または全部 `scss`。
- `custom_css` は **Hugo Extended を使う前提**で考える。
- 互換動作として、`assets/ananke/css` に見つからない場合は `static` 相対の `<link>` 読み込みを試す動きがある。

### 8.4 具体例

```css
/* assets/ananke/css/custom.css */
.article-meta {
  font-size: 0.9rem;
}

.summary p {
  line-height: 1.8;
}

.site-logo img {
  max-height: 42px;
}
```

```css
/* assets/ananke/css/overrides.css */
main p,
main li {
  letter-spacing: 0.01em;
}

h1, h2, h3 {
  scroll-margin-top: 5rem;
}
```

### 8.5 CSS だけで済むこと / 済まないこと

**CSS だけで済むこと**
- 色
- 余白
- 行間
- フォント
- カードの角丸や影
- アイコンサイズ

**CSS だけでは済まないこと**
- 出力 HTML 構造そのものを変える
- 要素の並び順を大きく変える
- 条件分岐で別 UI を出す

後者は `layouts/` のオーバーライドが必要です。

---

## 9. ヘッダ内へのスクリプト追加

一部の解析タグ、検証タグ、外部ウィジェット初期化スクリプトは `<head>` に入れたい場合があります。Ananke では `layouts/partials/head-additions.html` を置く方法が案内されています。

```html
<!-- layouts/partials/head-additions.html -->
<meta name="example-verification" content="YOUR_TOKEN">
<script defer src="https://example.com/widget.js"></script>
```

### 実務メモ

- GTM, 検証メタ, 独自 JS の head 挿入に向く。
- ただし CSP や privacy 対応が必要なら、別途サイト全体設計を見直す。

---

## 10. 読了時間・語数表示

```toml
[params]
  show_reading_time = true
```

またはページ単位:

```yaml
---
title: "長文記事"
show_reading_time: true
---
```

長文ブログでは有効ですが、固定ページ中心のサイトでは冗長になることもあります。

---

## 11. 日付表示のローカライズ

```toml
[params]
  date_format = '2. January 2006'
```

新しめの Hugo では以下のような定義済みレイアウトも使えます。

```toml
[params]
  date_format = ':date_full'
```

日本語サイトであれば、テンプレート側や Hugo のロケール設定と合わせて調整すると自然です。

---

## 12. 「続きを読む」文言の変更

サイト全体:

```toml
[params]
  read_more_copy = '続きを読む'
```

ページ単位:

```yaml
---
title: "天体観測レポート"
read_more_copy: "観測記録の続きへ"
---
```

多言語サイトでは言語別 `params` に置き分けると自然です。

---

## 13. ソーシャルメディア設定

### 13.1 定義

最近の Ananke では、SNS 関連設定は `params.ananke.social` 以下に集約されています。ここで

- フォローリンク
- シェアボタン
- ネットワーク定義

を扱います。

### 13.2 フォローリンク設定例

```toml
[params.ananke.social.follow]
  new_window_icon = true
  networks = ['github', 'linkedin', 'bluesky']

[params.ananke.social.github]
  username = 'yourname'

[params.ananke.social.linkedin]
  username = 'yourname'

[params.ananke.social.bluesky]
  username = 'yourname.bsky.social'
```

#### リンクを直接上書きする例

```toml
[params.ananke.social.linkedin]
  username = 'yourname'
  profilelink = 'https://www.linkedin.com/in/yourname/'
  rel = 'me'
```

### 13.3 シェアボタン設定例

```toml
[params.ananke.social.share]
  icons = true
  sharetext = true
  networks = ['email', 'facebook', 'bluesky', 'linkedin']
```

### 13.4 無効化

ページ単位:

```yaml
---
disable_share: true
---
```

全体:

```toml
[params.ananke.social.share]
  disable_share = true
```

### 13.5 実務判断

- B2B サイトや会社案内では共有ボタン不要のことが多い。
- 技術ブログや記事中心サイトでは共有ボタンが有効。
- `rel = 'me'` はプロフィール所有証明系の用途で便利。

---

## 14. メニューのカスタマイズ

Ananke 固有というより Hugo 本体の機能ですが、実際のカスタマイズでは重要です。

```toml
[[menus.main]]
  name = 'Home'
  pageRef = '/'
  weight = 10

[[menus.main]]
  name = 'Posts'
  pageRef = '/posts'
  weight = 20

[[menus.main]]
  name = 'About'
  pageRef = '/about'
  weight = 30
```

### メニュー設計の勘所

- `weight` で順序制御。
- `pageRef` を使うと URL 変更への耐性が比較的高い。
- セクション一覧を主導線にしたい場合は `posts` や `works` を上に置く。

---

## 15. Front Matter でよく使う項目

Ananke で実務上よく触る Front Matter 項目をまとめると次のとおりです。

```yaml
---
title: "記事タイトル"
featured_image: "/images/sample.jpg"
omit_header_text: false
featured_image_class: "cover bg-center"
cover_dimming_class: "bg-black-40"
text_color: "dark-gray"
show_reading_time: true
read_more_copy: "続きを読む"
disable_share: false
canonicalUrl: "https://example.com/original-post"
private: true
---
```

### 要点

- `canonicalUrl` は転載・再掲時に重要。
- `private: true` は検索エンジンにインデックスさせたくないページ向け。
- `featured_image_*` 系はヒーロー見た目の微調整に有効。

---

## 16. レイアウトのオーバーライド

### 16.1 定義

Hugo では、テーマ内テンプレートと同じ相対パスのファイルをサイト側 `layouts/` に置くと、**テーマよりサイト側が優先**されます。Ananke の本格カスタマイズはここが肝です。

### 16.2 典型パターン

```text
layouts/
├─ _default/
│  ├─ baseof.html
│  ├─ single.html
│  └─ list.html
└─ partials/
   ├─ head-additions.html
   ├─ site-header.html
   └─ footer.html
```

### 16.3 どう使い分けるか

- **ヘッダだけ変えたい** → `partials` 上書き
- **記事詳細ページだけ変えたい** → `_default/single.html`
- **一覧ページのカード構造を変えたい** → `_default/list.html` または関連 partial
- **全ページ共通の外枠を変えたい** → `_default/baseof.html`

### 16.4 実務のコツ

- いきなり全面コピーしない。**必要な partial だけ抜き出して変更**する。
- テーマ更新追随を考えると、変更差分は少ないほどよい。
- オーバーライド後は upstream の変更を取り込みにくくなるので、コメントで理由を残す。

---

## 17. コメント機能や外部サービス統合

Ananke の wiki にはコメント機能カスタマイズ項目もありますが、運用上はテーマ標準の仕組みよりも、

- Giscus
- Commento
- Utterances
- 独自埋め込み

のような外部サービス統合になることが多いです。

この場合はたいてい `layouts/partials` 側で、記事末尾や `single.html` に埋め込みます。

```html
<!-- 例: layouts/partials/comments.html -->
<script src="https://giscus.app/client.js"
        data-repo="OWNER/REPO"
        data-repo-id="..."
        data-category="Announcements"
        data-category-id="..."
        data-mapping="pathname"
        data-strict="0"
        data-reactions-enabled="1"
        data-emit-metadata="0"
        data-input-position="bottom"
        data-theme="light"
        data-lang="ja"
        crossorigin="anonymous"
        async>
</script>
```

---

## 18. 多言語サイトでのカスタマイズ

Ananke は多言語利用とも相性がよく、少なくとも以下は言語別設定しやすいです。

- `read_more_copy`
- メニュー
- タイトル・説明
- 日付書式
- ソーシャル表示文言

例:

```toml
[languages.ja]
  languageName = '日本語'
  weight = 1

[languages.ja.params]
  read_more_copy = '続きを読む'

[languages.en]
  languageName = 'English'
  weight = 2

[languages.en.params]
  read_more_copy = 'Read more'
```

---

## 19. 実戦的なカスタマイズ方針

### 19.1 最小変更で済ませる方針

向いているサイト:
- ブログ
- 技術メモ
- 会社の簡易サイト

手順:
1. `params` を整える
2. `site_logo` とメニューを入れる
3. `custom_css` で最低限整える
4. 必要なら SNS 設定を足す

### 19.2 デザインをかなり寄せる方針

向いているサイト:
- ブランドサイト
- LP
- 既存デザイン再現

手順:
1. ヒーロー表示を Front Matter と CSS で設計
2. カード一覧や single を `layouts/` で上書き
3. CTA, バナー, コメント, 分析タグなどを partial 化
4. テーマとの差分管理をドキュメント化

### 19.3 将来保守を重視する方針

- 上書き partial を最小限にする
- 独自 CSS は役割別に分ける
- 設定値は `params.toml` に寄せる
- カスタマイズ項目一覧を README に残す

---

## 20. よくある落とし穴

### 20.1 Custom CSS が効かない

確認順:
1. Hugo Extended を使っているか
2. `assets/ananke/css/` 配下に置いたか
3. `custom_css` のファイル名が正しいか
4. `css` と `scss` を混在させていないか
5. ブラウザキャッシュを疑ったか

### 20.2 body のフォントを変えたのに本文が変わらない

`body_classes` では本文部分の指定が効き切らない場合があります。`post_content_classes` を使うか、独自 CSS で本文領域を明示的に当てます。

### 20.3 テーマ更新で崩れた

`layouts/` にオーバーライドが多いほど発生しやすいです。テーマ本体更新時は

- upstream 差分確認
- 自分の partial 上書き確認
- ソーシャル設定の変更有無確認

をセットで見ます。

### 20.4 SNS 設定が古い記事のままで動かない

Ananke の SNS 周りは近年 `params.ananke.social` 配下に整理されています。古い記事の `params.social` 系だけを写すと、現在の構成と噛み合わないことがあります。

---

## 21. 典型的な完成例

### 21.1 技術ブログ向け

```toml
[params]
  site_logo = 'img/logo.svg'
  body_classes = 'sans-serif bg-near-white'
  post_content_classes = 'serif'
  text_color = 'near-black'
  show_reading_time = true
  read_more_copy = '続きを読む'
  custom_css = ['custom.css']

[params.ananke.social.follow]
  networks = ['github', 'linkedin']

[params.ananke.social.github]
  username = 'yourname'

[params.ananke.social.linkedin]
  username = 'yourname'
```

特徴:
- 読了時間あり
- GitHub 導線あり
- 本文可読性重視

### 21.2 コーポレートサイト向け

```toml
[params]
  site_logo = 'img/company-logo.svg'
  background_color_class = 'bg-dark-blue'
  featured_image_class = 'cover bg-center'
  cover_dimming_class = 'bg-black-50'
  text_color = 'dark-gray'
  custom_css = ['brand.css']

[params.ananke.social.share]
  disable_share = true
```

特徴:
- シェアボタン無効
- ブランドトーン優先
- 画像・導線を強く見せる

---

## 22. 推奨ワークフロー

```bash
hugo server -D
```

開発時は以下のサイクルが堅実です。

1. `config/_default/params.toml` を触る
2. 足りない部分を Front Matter で確認
3. さらに足りない部分を `custom_css` で補う
4. 最後にだけ `layouts/` を上書きする

この順番にすると、**テーマ更新耐性**と**見通しのよさ**を両立しやすいです。

---

## 23. 最終的なおすすめ設計

Ananke を長く運用するなら、次の方針が最も安定します。

- テーマ本体は編集しない
- 設定は `config/_default/` に集約
- 見た目調整は `assets/ananke/css/` に集約
- HTML 構造変更だけ `layouts/` で上書き
- ページ差分は Front Matter に閉じ込める

要するに、**「設定で済むことは設定で、CSS で済むことは CSS で、構造変更だけテンプレートで」** が Ananke カスタマイズの基本原則です。

---

## 24. 参考設定サンプル一式

### `config/_default/hugo.toml`

```toml
baseURL = 'https://example.com/'
languageCode = 'ja-jp'
title = 'My Ananke Site'
theme = 'ananke'
```

### `config/_default/params.toml`

```toml
site_logo = 'img/logo.svg'
body_classes = 'avenir bg-near-white'
post_content_classes = 'serif'
text_color = 'dark-gray'
background_color_class = 'bg-dark-blue'
featured_image_class = 'cover bg-center'
cover_dimming_class = 'bg-black-40'
show_reading_time = true
date_format = ':date_long'
read_more_copy = '続きを読む'
custom_css = ['custom.css']

[ananke.social.follow]
new_window_icon = true
networks = ['github', 'linkedin']

[ananke.social.github]
username = 'yourname'

[ananke.social.linkedin]
username = 'yourname'

[ananke.social.share]
icons = true
sharetext = false
networks = ['email', 'linkedin']
```

### `assets/ananke/css/custom.css`

```css
body {
  font-feature-settings: "palt";
}

main p {
  line-height: 1.9;
}

article h2,
article h3 {
  margin-top: 2.2rem;
}

nav a {
  font-weight: 600;
}
```

### `content/posts/sample.md`

```yaml
---
title: "サンプル記事"
date: 2026-03-18
featured_image: "/images/sample-hero.jpg"
featured_image_class: "cover bg-center"
cover_dimming_class: "bg-black-30"
text_color: "dark-gray"
show_reading_time: true
read_more_copy: "記事の続きへ"
disable_share: false
---

本文...
```

---

## 25. 参考資料

- theNewDynamic / gohugo-theme-ananke README
- Ananke Wiki: Getting Started
- Ananke Wiki: Customization Styles
- Ananke Wiki: Customization Herosection
- Ananke Wiki: Configure Social Media Networks
- Hugo Documentation: Configure menus
- Hugo Documentation: Configure params

