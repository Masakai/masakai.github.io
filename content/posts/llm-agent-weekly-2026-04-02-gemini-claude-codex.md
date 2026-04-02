+++
title = "Gemini・Claude・Codex 公式発表ウォッチ (2026-03-25〜2026-04-02)"
date = 2026-04-02T13:55:07+09:00
tags = ["AI", "Gemini", "Claude", "Codex", "生成AI", "AIエージェント"]
draft = false
featured_image = "/images/gemini-claude-codex-2026-04-02.svg"
+++

## 今週のトレンド分析

この1週間強をざっくり見ると、Gemini・Claude・Codex はそろって小さくても意味のある更新を出してきました。Gemini はリアルタイム音声、Claude はモバイルのインタラクティブ表示に加えて配布物管理の信頼性が問われる出来事があり、Codex はプラグイン配布という具合に、今週は「モデル名の刷新」より「使い方の面と運用品質」が強く意識された週でしたね。

**① Gemini は“音声エージェントの実用化”を一段押し進めた**

3月26日に公開された Gemini 3.1 Flash Live は、ネイティブ音声を前提にした低遅延・高信頼の対話モデルとして整理されています。テキスト中心のアシスタントから、リアルタイムで会話しながら道具を使うエージェントへ重心がさらに移った感じです。

**② Claude は機能拡張と同時に、配布物の信頼性も問われた**

3月25日のリリースノートでは、iOS / Android の Claude アプリがライブチャートや図を会話内で表示できる interactive apps に対応しました。一方で 3月31日には Claude Code の npm 配布物に source map が含まれ、内部ソース再構成が可能だった件が報じられています。機能を広げるだけでなく、配布の作法そのものが信頼に直結する段階に入った感じです。

**③ Codex はワークフロー共有をしやすくする方向へ一歩進んだ**

3月26日の ChatGPT release notes では、Codex に curated plugins directory が追加されました。skills、apps、MCP 構成を束ねた再利用可能ワークフローを配布しやすくする更新で、Codex が個人用ツールからチーム共有基盤へ少し寄った印象です。

**オープン系 vs クローズド系で見ると**

今週の動きは、クローズド系の強みと弱みがどちらも見えやすかったです。音声、可視化、プラグイン共有みたいな“仕事の入り口”を少しずつ埋める強さがある一方で、npm 配布物やアプリ更新の品質管理でつまずくと一気に信頼を削る、という現実も出ました。実務導入では、機能追加と同じくらい配布品質の安定が重要ですね。

自分の仕事に引き寄せるなら、「今週は何が新しく出たか」だけでなく、「3月に出た機能のうち、どれを本当に業務に組み込めるか」を見直すタイミングかもしれません。音声、長文処理、コード支援のどれがいちばん手応えありそうでしょうか？

---

## Google / Gemini

- **Gemini 3.1 Flash Live が3月26日に公開、リアルタイム音声エージェント性能を強化**

  Google DeepMind は 2026年3月26日に Gemini 3.1 Flash Live のモデルカードを公開しました。音声、画像、動画、テキストを扱う 128K コンテキスト対応モデルで、会話の間合い理解、関数呼び出し、長い対話でのペルソナ維持などを強く打ち出しています。今週の3社比較では、いちばん明確な新規公式発表でした。

  [元記事を読む](https://deepmind.google/models/model-cards/gemini-3-1-flash-live/)

- **Gemini Audio ページでも 3.1 Flash Live を次世代ライブ音声エージェントの中核として訴求**

  Google DeepMind の Gemini Audio ページでも、Gemini 3.1 Flash Live を「より自然で信頼性の高い live voice agents」を支えるモデルとして前面に出しています。単なるモデルカード公開にとどまらず、Google 側が音声インターフェースを Gemini の重要な成長軸として押していることがよく分かります。

  [元記事を読む](https://deepmind.google/models/gemini-audio/)

## Anthropic / Claude

- **Claude の iOS / Android アプリが 3月25日に interactive apps に対応**

  Claude Help Center のリリースノートでは、2026年3月25日にモバイル版 Claude が fully interactive apps へ接続できるようになったと案内されています。ライブチャート、図、共有可能なアセットを会話内にそのまま描画できるため、3月12日に入った可視化機能をモバイル利用へ広げる更新と見てよさそうです。

  [元記事を読む](https://support.claude.com/en/articles/12138966-release-notes)

- **Claude Code の npm 配布物で source map 露出が報じられ、その後バージョン更新が継続**

  3月31日には、`@anthropic-ai/claude-code` の npm 配布物に source map が含まれ、内部ソースを再構成できる状態だったと複数媒体が報じました。Anthropic の公式ニュース記事は見当たりませんが、npm 上ではその後も 1.0.102、1.0.108 と更新が続いており、少なくとも配布物は継続的に差し替えられています。今週の Anthropic 関連では、機能発表以上にこの件のインパクトが大きかったと言えます。

  [報道を読む](https://www.theguardian.com/technology/2026/apr/01/anthropic-claudes-code-leaks-ai)

  [npmの更新状況を見る](https://www.npmjs.com/package/%40anthropic-ai/claude-code?activeTab=versions)

## OpenAI / Codex

- **Codex に 3月26日付で curated plugins directory が追加**

  OpenAI の ChatGPT release notes では、2026年3月26日に Codex へ curated plugins directory を追加したと案内されています。プラグインは skills、任意の app 連携、MCP サーバー設定をまとめて配布できるパッケージとして定義されており、Codex のワークフローをプロジェクト横断で再利用しやすくする更新です。

  [元記事を読む](https://help.openai.com/en/articles/6825453-how-chatgpt-and-other-ai-writing-tools-work)
