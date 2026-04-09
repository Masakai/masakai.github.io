# Hugo ブログプロジェクト - プロジェクト指南書

このプロジェクトは、**Hugo** で構築された静的サイトジェネレーター型ブログであり、**GitHub Pages** を使用して公開されています。クライアント向けサービスとして、複数ジャンルの週刊ニュースレターを作成します。

---

## 📋 プロジェクト概要

- **ブログシステム：** Hugo（静的サイトジェネレーター）
- **テーマ：** Ananke
- **ホスティング：** GitHub Pages
- **リポジトリ：** このフォルダは Git リポジトリとして管理されています
- **主な用途：** 複数テーマの週刊ニュースレター形式の記事配信

---

## 🗂️ ディレクトリ構造

```
report_riverruns/
├── CLAUDE.md                    # このファイル（プロジェクト指南書）
├── AGENTS.md                    # Codex チーム向け指示書
├── config.toml                  # Hugo サイト設定
├── content/
│   └── posts/                   # ブログ記事（Markdown形式、テーマ別）
│       ├── llm-agent-weekly-2026-04-09.md
│       ├── manufacturing-sme-review-2026-04-09.md
│       ├── aerospace-domestic-weekly-2026-04-09.md
│       ├── precision-metal-weekly-2026-04-09.md
│       ├── deburring-polishing-weekly-2026-04-09.md
│       └── ... (その他コラム・製品紹介など)
├── static/
│   └── images/                  # 画像アセット
├── themes/
│   └── ananke/                  # Hugo テーマ（Git サブモジュール）
└── .github/
    └── workflows/               # GitHub Actions（CI/CD設定）
```

---

## 🚀 GitHub Pages デプロイメント

### デプロイ方式
- **リポジトリ設定：** GitHub Pages は `master` ブランチから自動的にビルド・デプロイされます
- **ビルド方式：** GitHub Actions により、push 時に自動的に Hugo ビルドと公開が実行されます

### デプロイフロー
1. 新規記事をコミット・push する
2. GitHub Actions が自動的にトリガーされ、Hugo ビルドを実行
3. ビルド成功後、静的サイトが GitHub Pages に公開

### デプロイ前のチェックリスト
記事を公開する前に、以下を確認してください：

- [ ] **TOML front matter が正しいか確認**
  - 「テーマ別情報源・テンプレート一覧」のテンプレートに従っているか
  - `title`, `date`, `tags`, `draft`, `featured_image` が記載されているか
  ```toml
  +++
  title = "記事タイトル"
  date = 2026-04-09T10:00:00+09:00  # ISO 8601 形式（タイムゾーン必須）
  tags = ["タグ1", "タグ2"]
  draft = false  # 公開設定
  featured_image = "/images/image.png"  # 画像パスは /images/ で始まる
  +++
  ```
- [ ] **記事ファイル名が正しいか確認**（テーマ別命名規則は下記「テーマ別情報源・テンプレート一覧」参照）
- [ ] **画像ファイルが `static/images/` に配置されているか確認**
- [ ] **ローカルでビルド確認を実施**（詳細は下記参照）
- [ ] **記事内のリンクが正しく機能するか確認**
- [ ] **タグが既存タグと統一されているか確認**

---

## 💻 ローカル開発環境

### 環境セットアップ
```bash
# Hugo がインストール済みであることを確認
hugo version

# ローカル開発サーバーの起動
hugo server

# ブラウザで http://localhost:1313 にアクセス
```

### ローカル検証
```bash
# ビルド成功の確認
hugo

# `public/` フォルダが生成されれば成功
# 生成されたサイトをブラウザで確認
open public/index.html
```

### よくあるトラブル
| 問題 | 原因 | 解決方法 |
|------|------|--------|
| 記事が表示されない | `draft = true` のまま | `draft = false` に変更 |
| 画像が表示されない | 画像パスが間違っている | `/images/filename.png` 形式を確認 |
| ビルドエラー | front matter の TOML 形式が壊れている | `+++` で囲まれているか、構文を確認 |

---

## 📚 テーマ別情報源・テンプレート一覧

サーチャーはユーザーからテーマを受け取ったら、この表を引いて情報源・ファイル名・front matter を決定する。

---

### テーマ1: AI・LLMエージェント

**ファイル命名：** `llm-agent-weekly-YYYY-MM-DD.md`

**front matter テンプレート：**
```toml
+++
title = "LLM・AIエージェント週刊ニュース (YYYY-MM-DD〜YYYY-MM-DD)"
date = YYYY-MM-DDThh:mm:ss+09:00
tags = ["AI", "LLM", "エージェント", "生成AI"]
draft = false
featured_image = "/images/LLM_news_letter.png"
+++
```

**一次資料ソース（優先順）：**

| 情報源 | URL |
|--------|-----|
| OpenAI Blog | https://openai.com/blog |
| Anthropic Blog | https://anthropic.com/news |
| Google DeepMind Blog | https://deepmind.google/blog |
| Google Research Blog | https://research.google/blog |
| Meta AI Blog | https://ai.meta.com/blog |
| Mistral AI News | https://mistral.ai/news |
| Hugging Face Blog | https://huggingface.co/blog |
| Microsoft Research Blog | https://microsoft.com/en-us/research/blog |
| ChatGPT Release Notes | https://help.openai.com/en/articles/6825453-chatgpt-release-notes |

**レビュアーのトレンド分析軸（目安）：** オープン系 vs クローズド系モデルの動向比較を含めると良い

---

### テーマ2: 国内製造業向けDX

**ファイル命名：** `manufacturing-sme-review-YYYY-MM-DD.md`

**front matter テンプレート：**
```toml
+++
title = "国内製造業DX週刊レビュー (YYYY-MM-DD〜YYYY-MM-DD)"
date = YYYY-MM-DDThh:mm:ss+09:00
tags = ["製造業", "DX", "中小企業", "デジタル化", "METI"]
draft = false
featured_image = "/images/manufacturing-sme.png"
+++
```

※ `manufacturing-sme.png` は未作成。イラストレータが初回記事時に生成すること。

**一次資料ソース（優先順）：**

| 情報源 | URL |
|--------|-----|
| 中小企業庁（白書・施策） | https://www.chusho.meti.go.jp |
| 経済産業省（製造業・DX） | https://www.meti.go.jp/policy/mono_info_service/mono/index.html |
| 日本政策金融公庫（調査・統計） | https://www.jfc.go.jp/n/findings/index.html |
| 日本工作機械工業会（受注統計） | https://www.jmtba.or.jp |
| 日刊工業新聞 | https://www.nikkan.co.jp |
| ものづくり白書（METI） | https://www.meti.go.jp/report/whitepaper/mono/index.html |
| 内閣府 月例経済報告 | https://www5.cao.go.jp/keizai3/getsurei/getsurei.html |
| 日本銀行 短観 | https://www.boj.or.jp/statistics/tk/index.htm |

**レビュアーのトレンド分析軸（目安）：** 「受注・景況感」「コスト転嫁・賃上げ」「省力化・自動化投資」の3軸で整理

---

### テーマ3: 航空宇宙産業（国内）

**ファイル命名：** `aerospace-domestic-weekly-YYYY-MM-DD.md`

**front matter テンプレート：**
```toml
+++
title = "航空宇宙産業 国内週刊ニュース (YYYY-MM-DD〜YYYY-MM-DD)"
date = YYYY-MM-DDThh:mm:ss+09:00
tags = ["航空宇宙", "宇宙開発", "防衛", "ロケット", "JAXA", "国内動向"]
draft = false
featured_image = "/images/aerospace-domestic.png"
+++
```

**一次資料ソース（優先順）：**

| 情報源 | URL |
|--------|-----|
| JAXA 公式ニュース | https://www.jaxa.jp/press/index_j.html |
| 防衛省 プレスリリース | https://www.mod.go.jp/j/press/index.html |
| 経済産業省 航空機産業室 | https://www.meti.go.jp/policy/mono_info_service/mono/aircraft/index.html |
| 宇宙航空工業会（SJAC）ニュース | https://www.sjac.or.jp/news |
| 宇宙政策委員会 議事録（内閣府） | https://www8.cao.go.jp/space/comittee/yusou-dai3/yusou-index.html |
| Defense News（日本関連） | https://www.defensenews.com/global/asia-pacific |
| 日本経済新聞（航空宇宙タグ） | https://www.nikkei.com |
| sorae.info（宇宙ニュース専門） | https://sorae.info |

**レビュアーのトレンド分析軸（目安）：** 「民間宇宙輸送」「防衛・安全保障宇宙」「次世代機・輸出規制」の3軸で整理

---

### テーマ4: 精密金属加工業

**ファイル命名：** `precision-metal-weekly-YYYY-MM-DD.md`

**front matter テンプレート：**
```toml
+++
title = "精密金属加工業週刊ニュース (YYYY-MM-DD〜YYYY-MM-DD)"
date = YYYY-MM-DDThh:mm:ss+09:00
tags = ["精密加工", "切削", "工作機械", "製造業", "金属加工"]
draft = false
featured_image = "/images/precision-metal.png"
+++
```

**一次資料ソース（優先順）：**

| 情報源 | URL |
|--------|-----|
| 日本工作機械工業会（受注統計・展示会） | https://www.jmtba.or.jp |
| 日本精密工業会 | https://www.jspe.or.jp |
| 日本機械工業連合会（日機連） | https://www.jmf.or.jp |
| OSG 公式ニュース・新製品 | https://www.osg.co.jp/news |
| オークマ 展示会・新製品情報 | https://www.okuma.co.jp/news |
| DMG森精機 プレスリリース | https://www.dmgmori.co.jp/news |
| GrindingHub ニュースルーム | https://www.grindinghub.de/en/newsroom |
| ファナック プレスリリース | https://www.fanuc.co.jp/ja/news |
| 日刊工業新聞 | https://www.nikkan.co.jp |

**レビュアーのトレンド分析軸（目安）：** 「難削材対応・工具進化」「研削・研磨の知能化」「展示会での業界動向」の3軸で整理

---

### テーマ5: バリ取り・研磨業

**ファイル命名：** `deburring-polishing-weekly-YYYY-MM-DD.md`

**front matter テンプレート：**
```toml
+++
title = "バリ取り・研磨業週刊ニュース (YYYY-MM-DD〜YYYY-MM-DD)"
date = YYYY-MM-DDThh:mm:ss+09:00
tags = ["バリ取り", "研磨", "表面処理", "精密加工", "自動化"]
draft = false
featured_image = "/images/deburring-polishing.png"
+++
```

※ `deburring-polishing.png` は未作成。イラストレータが初回記事時に生成すること。

**一次資料ソース（優先順）：**

| 情報源 | URL |
|--------|-----|
| Rösler Metal Finishing プレスリリース | https://www.rosler.com/en/press-releases |
| VOLLMER Group ニュース | https://www.vollmer-group.com/de/news |
| ultraTEC innovation（超音波バリ取り） | https://www.ultratec-innovation.de |
| GrindingHub ニュースルーム | https://www.grindinghub.de/en/newsroom |
| 日本研磨工業会 | https://www.jaas.or.jp |
| 日本砥石工業会 | https://www.jwa.or.jp |
| 日刊工業新聞（精密・表面処理） | https://www.nikkan.co.jp |
| DMG森精機（自動化・バリ取りユニット） | https://www.dmgmori.co.jp/news |
| 日本工作機械工業会（統計） | https://www.jmtba.or.jp |

**レビュアーのトレンド分析軸（目安）：** 「バリ取り自動化・ロボット化」「表面品質と後工程連携」「超音波・電解などの工法革新」の3軸で整理

---

## 📝 Hugo ニュースレター生成チーム

このプロジェクトでは、信頼性の高い一次資料（企業公式ブログ等）をもとに、**3役のチーム構造** で週刊ニュースレターを作成します。

### 🔍 サーチャー
**指揮者（ユーザー）から受け取るもの：**
- 収集テーマ（5テーマのいずれか：AI・LLM / 国内製造業DX / 航空宇宙 / 精密金属加工 / バリ取り・研磨）
- 収集期間（例：直近1週間）

**作業内容：**
- ユーザーが指定したテーマ名から、上記「テーマ別情報源・テンプレート一覧」の対応行を参照する
- その行に列挙された一次資料ソースのみを検索対象とする
- 信頼性の低いまとめサイト・二次情報は除外する
- 収集した情報（タイトル・概要・URL）をライターに渡す

**テーマ判定の優先順位：**
1. ユーザーが「テーマ名」を明示した場合 → その行の情報源を使う
2. ファイル名パターンが示された場合 → ファイル名プレフィックスから対応テーマを逆引きする
3. 不明な場合 → ユーザーに確認する

---

### ✍️ ライター
**サーチャーから受け取るもの：**
- 記事タイトル・概要・URL のリスト

**作業内容：**
- 各記事を **80〜120文字（目安100文字）の日本語要約** にまとめる
- 企業・組織ごとにセクション分けする
- URL はそのまま記事直下に記載する
- 冒頭に `<!-- REVIEWER_SUMMARY_HERE -->` プレースホルダーを挿入してレビュアーに渡す
- Hugo front matter（TOML形式）を含める。テンプレートは上記「テーマ別情報源・テンプレート一覧」の対応テーマを参照
  ```toml
  +++
  title = "テーマに応じた記事タイトル (YYYY-MM-DD〜YYYY-MM-DD)"
  date = YYYY-MM-DDThh:mm:ss+09:00
  tags = ["テーマ別タグ", "タグ2"]
  draft = false
  featured_image = "/images/theme-slug.png"
  +++
  ```
  ※ `date` は時刻まで含めた ISO 8601 形式（例：`2026-04-09T09:00:00+09:00`）で記載すること

---

### 🧐 レビュアー
**ライターから受け取るもの：**
- `<!-- REVIEWER_SUMMARY_HERE -->` を含む記事草稿

**作業内容：**
- プレースホルダーを削除し、代わりに `## 今週のトレンド分析` セクションを冒頭に挿入する
- 以下の内容を含める：
  1. **収集期間全体のトレンドと構造的変化**（2〜3点）
  2. **テーマ別の推奨分析軸**（上記「テーマ別情報源・テンプレート一覧」内のレビュアー軸参照）
  3. **読者への語りかけ**（「自分の仕事にどう使えるか」を促すメッセージ）
- **文体はフレンドリーで親しみやすく**：
  - 「〜ですね」「〜感じ」「ざっくり言うと」などの語り口を使う
  - 論文・レポート調の「〜である」「〜だろう」は避ける
  - 絵文字を自然な範囲で使用する（1セクションにつき0〜1個が目安）
  - 締めは読者への問いかけや促しで終わる
- **AI らしさを省く**：
  - トレンド分析完成後、`/humanizer-ja` スキルを実行
  - 文章全体から「AIが書いた感」を取り除き、人間らしい自然な日本語に変換
  - 不自然な表現、一般的すぎる論調、定型句を修正
- **レイアウト調整（仕上げ）**：
  - 各記事の見出し（`**タイトル**`）と本文要約の間に空行を入れ、読みやすく整える
  - トレンド分析内の番号付き見出し（`**①**` `**②**` など）と本文の間にも空行を入れる
  - セクション見出し（`##`）の直前には必ず空行を入れる
  - URL はリンクテキスト付きの Markdown リンク形式（`[元記事を読む](URL)`）に統一する
  - 記事ブロック間（箇条書き項目間）にも空行を入れて、各エントリが視覚的に分離されるようにする

---

## 🔄 ワークフロー

### 新規記事の作成・公開フロー
```
1. ユーザーからの依頼（テーマ・期間を指定）
   ↓
2. サーチャー: テーマ別情報源から記事を検索
   ↓
3. ライター: 記事ドラフト作成（front matter + 要約 + トレンド分析プレースホルダ）
   ↓
4. レビュアー: トレンド分析追加 → humanizer-ja で人間らしい文体に調整 → 最終レイアウト
   ↓
5. コミット・プッシュ
   ↓
6. GitHub Actions による自動ビルド
   ↓
7. GitHub Pages に自動公開
```

### ブランチ戦略
- **main/master ブランチ：** 本番環境。すべての記事はこのブランチから公開
- **開発時：** 必要に応じてローカルで編集し、完成後に master にコミット
- **merge request：** 大規模な変更やテーマ更新時は、PR で管理することを推奨

---

## ✅ ベストプラクティス

### 記事作成時
- **ファイル名**：テーマ別命名規則に従う（「テーマ別情報源・テンプレート一覧」参照）
  - AI・LLM → `llm-agent-weekly-YYYY-MM-DD.md`
  - 国内製造業DX → `manufacturing-sme-review-YYYY-MM-DD.md`
  - 航空宇宙 → `aerospace-domestic-weekly-YYYY-MM-DD.md`
  - 精密金属加工 → `precision-metal-weekly-YYYY-MM-DD.md`
  - バリ取り・研磨 → `deburring-polishing-weekly-YYYY-MM-DD.md`
- **front matter**：テーマ別テンプレートに従い、TOML 形式で記載。`draft = false` を忘れずに
- **画像**：`static/images/` に配置し、`/images/filename.png` で参照
- **タグ**：テーマ別テンプレートで指定されたタグを優先。既存の tags と統一可能な場合は追加
- **日時**：ISO 8601 形式（タイムゾーン `+09:00` 必須）

### GitHub Pages へのデプロイ
- **自動デプロイ：** push 直後に GitHub Actions が実行。完了までの時間は通常 1〜5 分
- **デプロイ状況の確認：** リポジトリの "Actions" タブから確認可能
- **デプロイ失敗時：** GitHub Actions のログを確認し、エラーメッセージを読む（多くはビルドエラーまたは front matter 構文エラー）

### 画像アセット
- **フォーマット：** PNG, JPG, SVG など一般的なフォーマット使用
- **サイズ：** 最適化済み（1MB 以下が目安）
- **配置：** すべて `static/images/` に集約
- **参照：** Markdown では `![alt](/images/filename.png)` または HTML で参照

---

## 🛠️ トラブルシューティング

### よくあるエラーと対応

| エラー | 原因 | 対応 |
|--------|------|------|
| `ERROR: Unable to locate config file` | config.toml がない | リポジトリルートに config.toml があるか確認 |
| `theme mismatch error` | テーマのサブモジュール未初期化 | `git submodule update --init --recursive` を実行 |
| GitHub Pages に記事が表示されない | `draft = true` のままになっている | front matter を確認し `draft = false` に修正 |
| ビルド失敗（Actions） | Markdown の front matter 破損 | ファイルのエンコーディング（UTF-8）と TOML 構文を確認 |
| featured_image が表示されない | 画像ファイルが存在しない | `static/images/` に指定のファイルがあるか確認 |

---

## 📞 サポート

このプロジェクトについて質問がある場合は、以下を確認してください：

- Hugo 公式ドキュメント：https://gohugo.io/documentation/
- Ananke テーマ：https://github.com/theNewDynamic/gohugo-theme-ananke
- GitHub Pages：https://pages.github.com/
