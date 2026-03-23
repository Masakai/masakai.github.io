+++
title = "Gemini・Claude・Codex 公式発表まとめ (2026-01-23〜2026-03-23)"
date = 2026-03-23T09:53:04+09:00
tags = ["AI", "Gemini", "Claude", "Codex", "生成AI", "AIエージェント"]
draft = false
featured_image = "/images/gemini-claude-codex-2026-03-23.svg"
+++

## 今週のトレンド分析

この2ヶ月の公式発表をまとめて眺めると、Gemini、Claude、Codex の競争軸は「単に賢いモデルを出すこと」から、「どの仕事を、どのUIで、どこまで肩代わりできるか」にかなり移ってきた感じですね。モデルそのものの性能改善はもちろん続いていますが、実際の発表の厚みは、デスクトップ、Office、レビュー、スケジュール実行みたいな運用面に強く出ています。

**① AIが“会話相手”から“作業面”になってきた**

Geminiは高性能な推論モデルと低コスト高速モデルを細かく出し分け、ClaudeはCoworkやOffice連携で業務フローに入り込み、Codexは専用アプリで複数エージェント管理を前に出してきました。ざっくり言うと、各社とも「良い答えを返すAI」ではなく「仕事を進める面」を作り始めています。

**② モデルの階層化がかなり明確になった**

Gemini 3.1 Pro / Deep Think / Flash-Lite、ClaudeのCowork系機能と長文処理、Codexの GPT-5.3-Codex と Codex-Spark など、重い推論と高速実行の役割分担がはっきりしてきました。1つの万能モデルに寄せるより、用途ごとに体験を分けて最適化する方向が強いですね。

**③ エンタープライズ競争は“配布経路”と“管理機能”に移行中**

Claudeのプラグイン市場や管理機能、Excel/PowerPoint連携、Codexのアプリ・CLI・IDE横断、Geminiのアプリ統合やモデル階層の整理を見ると、今は導入後の定着率を取りにいくフェーズです。性能比較だけでなく、「社内にどう置けるか」が勝敗を左右し始めています。

**オープン系 vs クローズド系で見ると**

今回の対象は3社ともクローズド寄りの主力製品群なので、公式発表もほぼ一貫して“閉じた高品質スタック”の磨き込みに集中していました。オープン系が得意な柔軟な自前運用より、クローズド系が得意な統合UX、管理性、サポート込みの完成度で差を作ろうとしている流れがかなり鮮明です。

自分の仕事に引き寄せるなら、「どのモデルが一番強いか」だけでなく、「自分の業務はどの面でAIに渡すと摩擦が減るか」を考えると見え方が変わりそうです。調査、資料作成、開発、レビューのうち、まずどこから任せるのがいちばん効きそうでしょうか？

---

## Google / Gemini

- **Gemini 3.1 Pro が Google の最上位複雑タスク向けモデルとして登場**

  2月19日公開のモデルカードで、Gemini 3.1 Pro は Google の最先端複雑タスク向けモデルと位置づけられました。テキスト、音声、画像、動画、コードリポジトリまで扱う前提で、単発回答より「大量情報をまたぐ推論と制作」を担う基盤として整理されています。

  [元記事を読む](https://deepmind.google/models/model-cards/gemini-3-1-pro/)

- **Gemini 3.1 Deep Think が科学・研究・工学向けの特化推論モードとして前面化**

  2月の公開ページでは、Deep Think が Gemini 3.1 Pro 上に構築された最も専門的な推論モードとして紹介されました。数理、科学、工学の難問に寄せた設計で、日常的な生成AIより“研究用の思考装置”に近い売り方になっているのが印象的です。

  [元記事を読む](https://deepmind.google/models/gemini/deep-think/)

- **Gemini アプリに Lyria 3 を使った音楽生成が追加**

  2月18日、Gemini アプリで 30 秒の音楽トラックをテキストや画像から生成できる機能がベータ公開されました。画像・動画の生成に続いて音楽まで一体化したことで、Gemini が検索や会話だけでなく、総合的なクリエイティブ制作面へ広がっているのが分かります。

  [元記事を読む](https://blog.google/innovation-and-ai/products/gemini-app/lyria-3/)

- **Gemini 3.1 Flash-Lite が高スループット向け低コストモデルとして追加**

  3月3日公開のモデルカードで、Gemini 3.1 Flash-Lite は翻訳や分類のような高頻度・低遅延ワークロード向けに最適化された新モデルとして公開されました。高性能モデル一本足ではなく、量をさばく実運用向けの層を厚くしてきた動きとして重要です。

  [元記事を読む](https://deepmind.google/models/model-cards/gemini-3-1-flash-lite/)

## Anthropic / Claude

- **Claude の Cowork に定期実行タスクと Customize セクションが追加**

  2月25日のリリースノートで、Cowork に定期実行・都度実行のスケジュール機能が入り、Claude Desktop には skills、plugins、connectors をまとめる Customize セクションが追加されました。Claude を“毎回指示する相手”から“裏で回る作業者”へ近づける更新です。

  [元記事を読む](https://support.claude.com/en/articles/12138966-release-notes)

- **Cowork plugins と管理者向け統制機能が Team / Enterprise に追加**

  2月24日のリリースノートで、プラグインマーケットプレイスと管理者向けコントロールが導入されました。Claude の導入競争がモデル性能から、社内配布、権限管理、利用統制のしやすさへ移っていることをよく示すアップデートです。

  [元記事を読む](https://support.claude.com/en/articles/12138966-release-notes)

- **Claude のメモリ機能が無料ユーザーまで拡大**

  3月2日のリリースノートで、チャット履歴に基づくメモリ機能が無料ユーザーにも開放されました。個別会話のたびに文脈を積み直す形から、継続的な利用体験へ寄せる更新で、Claude の“使い捨て感”を減らす意味合いが大きいですね。

  [元記事を読む](https://support.claude.com/en/articles/12138966-release-notes)

- **Claude Code にマルチエージェント型の Code Review が研究プレビューで追加**

  3月9日、PRごとに複数エージェントが並列で不具合候補を洗い出し、検証して重要度順に返す Code Review が公開されました。Claude Code が単なるコード生成から、実務で重いレビュー工程の自動化まで踏み込んできたのはかなり大きい変化です。

  [元記事を読む](https://claude.com/blog/code-review)

- **Claude for Excel / PowerPoint がファイル横断の文脈共有と Skills に対応**

  3月11日、Excel と PowerPoint のアドインが会話文脈を共有し、Skills を使った再利用可能ワークフローに対応しました。スプレッドシート分析からスライド化までを1本の会話でつなぐ設計で、Claude の企業利用がかなり現実的になっています。

  [元記事を読む](https://claude.com/blog/claude-excel-powerpoint-updates)

- **1M context が Opus 4.6 / Sonnet 4.6 で一般提供に**

  3月13日、1Mコンテキストが一般提供となり、画像やPDFを含む大規模な入力を長い文脈で扱いやすくなりました。長文解析や巨大コードベースの理解を Claude の強みとしてさらに押し出す更新で、知識労働の大型案件にかなり効きそうです。

  [元記事を読む](https://claude.com/blog/1m-context-ga)

## OpenAI / Codex

- **Codex アプリが macOS 向けに公開、3月4日には Windows 版も案内**

  2月2日、複数のコーディングエージェントを並列管理できる Codex 専用アプリが公開されました。長時間タスク、分離ワークツリー、skills、automations を1つの画面で扱う設計で、Codex を“モデル”ではなく“開発オペレーティング面”として押し出す発表になっています。

  [元記事を読む](https://openai.com/index/introducing-the-codex-app/)

- **GPT-5.3-Codex が長時間タスクと専門職ワークまで視野に入れた主力モデルとして登場**

  2月5日、GPT-5.3-Codex が公開され、GPT-5.2-Codex のコーディング性能と GPT-5.2 系の推論・専門知識を統合したモデルとして位置づけられました。コード生成だけでなく、調査、PRD、監視、分析まで含む“コンピュータ上の仕事全体”へ踏み出したのが特徴です。

  [元記事を読む](https://openai.com/index/introducing-gpt-5-3-codex/)

- **GPT-5.3-Codex-Spark がリアルタイムコーディング向け超低遅延モデルとして研究公開**

  2月12日、Codex-Spark が ChatGPT Pro 向け研究プレビューとして公開されました。Cerebras 基盤で毎秒1000トークン超を目指す設計とされ、OpenAI が高性能一本ではなく、即応性そのものを体験価値として切り分け始めたことがよく分かる発表です。

  [元記事を読む](https://openai.com/index/introducing-gpt-5-3-codex-spark/)
