+++
title = "ChatGPT・Claude・Gemini週刊ニュース (2026-04-13〜2026-04-20)"
date = 2026-04-20T00:46:07+09:00
tags = ["AI", "LLM", "エージェント", "生成AI"]
draft = false
featured_image = "/images/LLM_news_letter.png"
+++

## 今週のトレンド分析

今週のAI 3社を見ると、モデルの賢さだけを競う段階から、「どの仕事の入口をAIに任せるか」を広げる段階に入ってきた感じですね。ChatGPTは利用プランと配信面、Claudeはコーディングとデザイン、Geminiは音声と画像生成で、それぞれ日常業務に近いところを押さえにきています。

**① Claudeは“長く任せる仕事”をさらに取りにきている**

Claude Opus 4.7は、難しいソフトウェア開発、長時間のエージェント作業、視覚理解を強化しています。さらにClaude Designで、設計・資料・プロトタイプ作成まで広げていて、開発者だけでなくPMやデザイナーにも届く動きですね。

**② Geminiは“声と画像”で生活・業務の入口を増やしている**

Gemini 3.1 Flash TTSやNative Audioの更新、Google Photos連携の画像生成を見ると、Googleはテキストチャットだけでなく、音声対話、翻訳、個人文脈つきの画像生成へかなり力を入れています。マルチモーダルを普段使いに落とす方向です。

**③ GoogleはGeminiとGemmaの二本立てがはっきりしてきた**

GeminiはGoogle製品やクラウドで使う高機能モデル、GemmaはApache 2.0ライセンスのオープンモデルとして、役割分担がかなり明確です。企業としては、クラウド利用のGeminiと、手元・エッジ・自社環境で動かすGemmaをどう使い分けるかが見どころですね。

**④ ChatGPTはCodexを含む“仕事用AI”の導線を太くしている**

OpenAIはChatGPTの利用プラン整理に加えて、Codex側でもGPT-5.4やGPT-5.4 miniを前面に出しています。とくにCodexでminiをサブエージェント的に使える流れは、開発作業を「大きなモデルに全部任せる」から「複数の役割に分けて回す」方向へ進めています。

ざっくり言うと、今週は「より賢いモデル」だけでなく、「どの場面で自然にAIを使わせるか」の競争が強く出ています。自分の仕事で見るなら、コード、資料、音声、画像のどこをAIに任せると一番時間が戻ってくるか、そこから考えるとよさそうです。

---

## OpenAI / ChatGPT

- **ChatGPT、Free/Goプラン向け広告を一部地域で展開開始**

  OpenAIは4月16日、オーストラリア、ニュージーランド、カナダのFree/Goユーザー向け広告展開を発表。有料プランとの差別化がより明確になりました。

  [元記事を読む](https://help.openai.com/en/articles/6825453-chatgpt-release-notes)

- **GPT-5.3 / GPT-5.4のChatGPT内での役割を整理**

  OpenAIのヘルプでは、GPT-5.3 InstantとGPT-5.4 Thinkingの用途、ツール対応、コンテキスト長を整理。日常利用と高難度作業の分担が見えます。

  [元記事を読む](https://help.openai.com/en/articles/11909943-gpt-53-and-gpt-54-in-chatgpt)

- **GPT-5.4 miniがCodexにも対応、サブエージェント用途を強化**

  OpenAIはGPT-5.4 miniをAPI、Codex、ChatGPTで提供。Codexではapp、CLI、IDE拡張、webで使え、軽めの開発タスクを低コストに回せます。

  [元記事を読む](https://openai.com/index/introducing-gpt-5-4-mini-and-nano/)

- **GPT-5.4はCodexにも提供、プロ向け作業モデルとして位置づけ**

  GPT-5.4はChatGPT、API、Codexで提供され、GPT-5.3-Codexのコーディング力を取り込みつつ、ツール利用や業務文書まで広げたモデルです。

  [元記事を読む](https://openai.com/index/introducing-gpt-5-4/)

## Anthropic / Claude

- **Claude Opus 4.7を一般提供、コーディングと視覚理解を強化**

  Anthropicは4月16日にClaude Opus 4.7を公開。高度なソフトウェア開発、長時間のエージェント作業、画像理解の改善を前面に出しています。

  [元記事を読む](https://www.anthropic.com/news/claude-opus-4-7)

- **Claude Designを研究プレビューとして公開**

  Anthropicは4月17日、デザイン、プロトタイプ、スライド、資料作成をClaudeと進められるClaude Designを発表。Opus 4.7を基盤にしています。

  [元記事を読む](https://www.anthropic.com/news/claude-design-anthropic-labs)

- **Claude公式リリースノートもOpus 4.7とDesignを更新**

  Claudeのリリースノートでは、4月16日のOpus 4.7、4月17日のClaude Designを連続して掲載。製品面での展開速度がかなり速い週でした。

  [元記事を読む](https://support.claude.com/en/articles/12138966-release-notes)

## Google / Gemini

- **Gemma 4を公開、Gemini 3由来の技術を使ったオープンモデルに**

  Googleは4月2日にGemma 4を発表。高度な推論、エージェント型ワークフロー、コード生成、画像・音声入力、長文コンテキストをApache 2.0で提供します。

  [元記事を読む](https://blog.google/innovation-and-ai/technology/developers-tools/gemma-4/)

- **Gemma 4はオンデバイスAIとエッジ用途も重視**

  Google Developers Blogでは、Gemma 4をAndroid、デスクトップ、Raspberry Piなどで動くエージェント用途として紹介。ローカルAIの選択肢が広がります。

  [元記事を読む](https://developers.googleblog.com/bring-state-of-the-art-agentic-skills-to-the-edge-with-gemma-4/)

- **Gemini 3.1 Flash TTSを公開、表現力ある音声生成を強化**

  Googleは4月15日、Gemini 3.1 Flash TTSを発表。70以上の言語、自然言語による音声タグ、SynthID透かしで音声生成の制御性を高めています。

  [元記事を読む](https://blog.google/innovation-and-ai/models-and-research/gemini-models/gemini-3-1-flash-tts/)

- **Geminiアプリ、Google Photos連携のパーソナル画像生成を追加**

  Googleは4月16日、GeminiアプリでGoogle Photosや個人の好みを使った画像生成を発表。長いプロンプトなしで個人文脈を反映しやすくなります。

  [元記事を読む](https://blog.google/innovation-and-ai/products/gemini-app/personal-intelligence-nano-banana/)

- **Gemini Native Audioを更新し、ライブ音声エージェントを強化**

  Gemini 2.5 Flash Native Audioは、関数呼び出し、指示追従、複数ターン会話を改善。Google AI StudioやVertex AI、Gemini Liveで展開されます。

  [元記事を読む](https://blog.google/products-and-platforms/products/gemini/gemini-audio-model-updates/)
