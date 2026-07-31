# 改善バックログ

改善提案・取得障害の台帳（改善メモの単一情報源）。デイリーエージェントが毎日更新し、ルールへの反映可否は kit が判断する。

## 運用ルール（エージェント向け）

- ダイジェストの「改善メモ」を書く**前に**必ずこのファイルを読み、先に台帳を更新する
- **新しい改善案** → 「提案中」に新規ブロックを追記（ID は既存の最大番号 +1。アーカイブ含む）
- **既出の提案を本日も再確認した** → 該当ブロックの「最終確認」を当日に更新し「回数」を +1。内容の重複起票は禁止
- **新しい取得障害** → 「既知の取得障害」に1行追加。**既知の障害が今日も発生** → 最終確認日のみ更新
- **障害が復旧した** → 該当行の行末に `→ 復旧（YYYY-MM-DD）` を追記（行は削除しない）
- 「状態」の変更（採用済み・見送り）とアーカイブへの移動は **kit が行う。エージェントは行わない**
- このファイルにはルール改善の提案と取得障害のみを書く。ニュース内容の気づきは書かない

## 提案中

- **B-004: `daily-sources.md` 各ソースの「取得方法」欄を WebSearch 優先に書き換える**
  - 対象: `.claude/rules/sites/daily-sources.md`（最優先・高優先の各ソースの「取得方法」行、および凡例）
  - 変更内容: RSS/WebFetch が長期的に全滅（403継続）しているソース群について、取得方法の第一優先を「WebSearch」に変更し、RSS/WebFetch はフォールバック扱いに降格する
  - 根拠: 全RSSフィード一括403が遅くとも 2026-06-07 から継続し、実運用は WebSearch フォールバックで安定している。`fetch-flow.md` の「回避策が安定している長期障害は取得方法欄を回避策ベースに書き換える提案を起票」規定に該当（最終確認 2026-08-01 / 回数 33）

- **B-005: 二次情報の数値が食い違う場合の記載ルールを `fetch-flow.md` に追加**
  - 対象: `.claude/rules/sites/fetch-flow.md`（「WebSearch利用時の注意事項」セクション）
  - 変更内容: 「一次情報に WebFetch で到達できず、WebSearch のスニペットのみで数値・条件が複数系統に割れる場合は、どちらか一方を採用せず『報道で幅がある』旨と複数の値を併記し、一次ソースが確認できなかった事実も明記する」という規定を追加する
  - 根拠: 2026-07-28 の Kimi K3 で、ウェイト容量が「約594GB」と「約1.4TB（MXFP4）」、ライセンスが「Modified MIT」「Apache 2.0」「revenue-tiered 独自ライセンス」の3系統に割れたが、一次ソースである Hugging Face のモデルカードが403で確認できず、採否の判断基準が現ルールに存在しなかった（最終確認 2026-08-01 / 回数 3。2026-07-31 の Amazon FY26 Q2 決算でも売上$181.52B 系と会社ガイダンス$194–199B 系で二次情報が割れ、一次 IR ページが403で確認できず同じ判断を要した。**2026-08-01 の確報で売上$200.6B・AWS +36.7% が確定し、$181.52B 系が誤りだったことが裏づけられた**。ガイダンス整合性を採否基準に使う本提案の妥当性が実例で確認できたため、規定の文面に「会社ガイダンスのレンジと整合しない二次情報は採用しない」を明示的に含める）

- **B-006: MCP 公式ブログ（`blog.modelcontextprotocol.io`）を日次ソースに追加**
  - 対象: `.claude/rules/sites/daily-sources.md`「最優先（日次ニュースソース）」セクション
  - 変更内容: `blog.modelcontextprotocol.io`（RSS: `blog.modelcontextprotocol.io/rss.xml`）を最優先ソースとして追加し、取得方法は「WebFetch → WebSearch」、頻度は毎日確認とする
  - 根拠: 2026-07-28 の MCP 2026-07-28 仕様公開は本リポジトリの主要関心（エージェント接続・権限統制）に直撃したが、現行の `daily-sources.md` に MCP の一次ソースがなく、Publickey / VentureBeat 経由の二次報道でしか捕捉できない。今日は WebFetch 広範403のなかで当ドメインへ WebFetch が成功し、非推奨機能・SDK 対応状況など二次報道にない一次情報を取得できた。MCP/ARD は 2026-07-14 に「エージェントの接続・権限・発見が主戦場」として収録済みで、継続ウォッチ対象と整合する（最終確認 2026-07-31 / 回数 3。RSS は `/rss.xml` が404のため取得方法は「トップページ WebFetch → WebSearch」とする。2026-07-31 も WebFetch 広範403のなか当ドメインのトップページのみ成功しており、回避策の安定性が再確認できた）

- **B-007: 主要クラウド4社の IR 決算ページを四半期定点ソースとして追加**
  - 対象: `.claude/rules/sites/daily-sources.md`「高優先（四半期・月次データソース）」セクション
  - 変更内容: Microsoft / Alphabet / Amazon / Meta の IR 決算プレスリリースページを四半期ソースとして追加する。取得方法は「IR一次ページを WebFetch → WebSearch」、頻度は「1月・4月・7月・10月の決算発表週は毎日確認、それ以外は確認不要」とする
  - 根拠: 2026-07-30 に Microsoft FY26 Q4 / Meta Q2 2026 から Azure 成長率+43%・M365 Copilot 有料シート3,000万超・capex 実績という提案直結の一次数値を採録したが、これらは現行 `daily-sources.md` に定点ソースがなく、決算カレンダーを手がかりに都度検索して拾っている。当日は `microsoft.com/en-us/Investor/...` の WebFetch のみ成功し、`prnewswire.com` / `sec.gov` / `investor.atmeta.com` は403だった。IR ページを名指しで登録すれば403回避の当たり先が固定でき、Copilot シート数のような年次更新では追えない指標を四半期粒度で継続取得できる（最終確認 2026-07-31 / 回数 2。2026-07-31 の Amazon FY26 Q2 / Apple FY26 Q3 でも同じ問題が再発し、`aboutamazon.com` の IR リリースと `cnbc.com` の決算記事がいずれも403で Amazon の確報値を一次確認できなかった。登録先には Apple も加える）

- **B-008: 取りこぼし検知用の週次スイープを設ける（TLDR AI を「必要時に参照」から「高優先」へ昇格）**
  - 対象: `.claude/rules/sites/daily-sources.md`（`tldr.tech/ai` の記載を「必要時に参照 > ニュースメディア・ニュースレター」から「高優先（四半期・月次データソース）」へ移動し、頻度欄を新設）
  - 変更内容: 頻度を「週1回。直近7日分の見出しを通読し、`.last-check-state.md` に未収録の項目を catch-up 収録する」とする。取得方法は「WebSearch」
  - 根拠: 2026-07-31 に AMD × Anthropic の最大2GW 提携・最大$5B 出資（7/22 発表）を9日遅れ、EU デジタルオムニバス Regulation (EU) 2026/1744（7/24 官報掲載・7/27 発効）を7日遅れで catch-up 収録した。前者は Anthropic の計算基盤が4ベンダー構成になるという調達前提の変更、後者は EU 高リスクAIの適用時期が最大16カ月ずれるという提案直結の一次情報でありながら、日次の WebSearch では当日の話題に埋もれて捕捉できなかった。現行 `daily-sources.md` は TLDR AI を「取りこぼし検知に有用」と評価しながら頻度を定めておらず、実運用で参照されていない（最終確認 2026-08-01 / 回数 2。2026-08-01 も JetBrains Context の早期アクセス提供〈7/21 開始〉を10日遅れで捕捉しており、日次 WebSearch が当日話題に偏る傾向が再確認できた）

- **B-009: 主要3社のモデル API 料金ページを日次定点ソースとして追加する**
  - 対象: `.claude/rules/sites/daily-sources.md`「最優先（日次ニュースソース）」セクション
  - 変更内容: OpenAI（`platform.openai.com/docs/pricing` および `openai.com/index/` の料金告知）/ Anthropic（`anthropic.com/pricing`）/ Google（`ai.google.dev/gemini-api/docs/pricing`）の料金ページを日次ソースとして追加する。取得方法は「WebSearch → WebFetch」とし（後述のとおり一次ページは403が常態）、頻度は毎日確認とする
  - 根拠: `ai-tools.md` は「料金・ビジネスモデルの変更」をコンサル提案に直結する最重要関心の一つに挙げているが、現行 `daily-sources.md` にモデル API 単価の定点ソースが1件も無い。既存の Business Insider Japan（B-002 で採用済み）は国内向け主要サービスの月次早見表であり、API のティア別単価を告知当日の粒度では追えない。2026-08-01 に OpenAI の GPT-5.6 値下げ（Luna 80%減・Terra 20%減、7/30 実施）を1日遅れで二次報道から捕捉したが、これは提案の見積り前提を直接動かす変更だった。当日は一次告知ページ `openai.com/index/advancing-the-price-performance-frontier-with-gpt-5-6/` が403で、値の裏取りは複数の二次スニペットの突き合わせと `.last-check-state.md` の旧単価（Luna $1／$6）との整合確認で行っている（最終確認 2026-08-01 / 回数 1）

## 既知の取得障害

- 全RSSフィード一括403（Google News RSS / GIGAZINE / The Decoder / VentureBeat / Publickey Atom / hnrss.org / Product Hunt / GitHub Trending 非公式RSS）: 403（初出: 不明・遅くとも 2026-06-07 には継続中 / 最終確認 2026-07-31）→ 回避策: WebSearch 経由で全ソース取得（運用安定）
- MCP 公式ブログ RSS（`blog.modelcontextprotocol.io/rss.xml`）: 404（初出 2026-07-30 / 最終確認 2026-07-31）→ 回避策: トップページ `blog.modelcontextprotocol.io/` を WebFetch（成功・記事一覧と日付を取得可）
- Ledge.ai（`ledge.ai`）: WebFetch 403（初出 2026-07-16 / 最終確認 2026-07-16）→ 回避策: WebSearch のスニペットで代替（本文取得は不可・手動確認推奨）
- 記事本文・一次情報ページの WebFetch 広範403（`forbes.com` / `itmedia.co.jp` / `publickey1.jp` / `mlq.ai` / `buildfastwithai.com` / `venturebeat.com` / `unite.ai` / `huggingface.co` モデルカード / `champaignmagazine.com` / `stacktr.ee` / `workos.com` / `releasebot.io` / `blogs.nvidia.com` / `investing.com` / `tech-noisy.com` / `anthropic.com` / `claude.com` / `prnewswire.com` / `sec.gov` / `investor.atmeta.com` / `axios.com` / `buildfastwithai.com` / `aboutamazon.com` / `cnbc.com` / `the-decoder.com` フィード / `openai.com` / `explainx.ai`）: 403（初出 2026-07-27 / 最終確認 2026-08-01。2026-07-28 に Hugging Face のモデルカード等の一次情報ページへ対象が拡大し、WebFetch は実質全滅に近い。2026-07-29 は `blog.modelcontextprotocol.io` のみ、2026-07-30 は同ドメインと `microsoft.com/en-us/Investor/...` のみ、2026-07-31 は同ドメインのみ WebFetch 成功。**2026-08-01 は WebFetch 成功ドメインが1件も無く、`openai.com` の料金告知ページと `publickey1.jp` の記事本文がいずれも403**）→ 回避策: WebSearch のスニペットで代替（本文取得は不可・数値の裏取りは複数スニペットの突き合わせで実施）

## アーカイブ（採用済み・見送り）

- B-001: Product Hunt のローンチ日特定問題への対処方針を明記 — **採用済み（2026-06-10）**。`daily-sources.md` Product Hunt 備考に反映（日付不明時は幅表現）
- B-002: Business Insider Japan の料金早見表を月次定点ソースに追加 — **採用済み（2026-06-10）**。`daily-sources.md` 高優先（四半期・月次）に追加
- B-003: MM総研の確認頻度を見直す — **採用済み（2026-06-10）**。`daily-sources.md` の頻度を毎日→週1回に変更（kit 判断）
