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
  - 根拠: 全RSSフィード一括403が遅くとも 2026-06-07 から継続し、実運用は WebSearch フォールバックで安定している。`fetch-flow.md` の「回避策が安定している長期障害は取得方法欄を回避策ベースに書き換える提案を起票」規定に該当（最終確認 2026-07-29 / 回数 30）

- **B-005: 二次情報の数値が食い違う場合の記載ルールを `fetch-flow.md` に追加**
  - 対象: `.claude/rules/sites/fetch-flow.md`（「WebSearch利用時の注意事項」セクション）
  - 変更内容: 「一次情報に WebFetch で到達できず、WebSearch のスニペットのみで数値・条件が複数系統に割れる場合は、どちらか一方を採用せず『報道で幅がある』旨と複数の値を併記し、一次ソースが確認できなかった事実も明記する」という規定を追加する
  - 根拠: 2026-07-28 の Kimi K3 で、ウェイト容量が「約594GB」と「約1.4TB（MXFP4）」、ライセンスが「Modified MIT」「Apache 2.0」「revenue-tiered 独自ライセンス」の3系統に割れたが、一次ソースである Hugging Face のモデルカードが403で確認できず、採否の判断基準が現ルールに存在しなかった（最終確認 2026-07-28 / 回数 1）

- **B-006: MCP 公式ブログ（`blog.modelcontextprotocol.io`）を日次ソースに追加**
  - 対象: `.claude/rules/sites/daily-sources.md`「最優先（日次ニュースソース）」セクション
  - 変更内容: `blog.modelcontextprotocol.io`（RSS: `blog.modelcontextprotocol.io/rss.xml`）を最優先ソースとして追加し、取得方法は「WebFetch → WebSearch」、頻度は毎日確認とする
  - 根拠: 2026-07-28 の MCP 2026-07-28 仕様公開は本リポジトリの主要関心（エージェント接続・権限統制）に直撃したが、現行の `daily-sources.md` に MCP の一次ソースがなく、Publickey / VentureBeat 経由の二次報道でしか捕捉できない。今日は WebFetch 広範403のなかで当ドメインへ WebFetch が成功し、非推奨機能・SDK 対応状況など二次報道にない一次情報を取得できた。MCP/ARD は 2026-07-14 に「エージェントの接続・権限・発見が主戦場」として収録済みで、継続ウォッチ対象と整合する（最終確認 2026-07-29 / 回数 1）

## 既知の取得障害

- 全RSSフィード一括403（Google News RSS / GIGAZINE / The Decoder / VentureBeat / Publickey Atom / hnrss.org / Product Hunt / GitHub Trending 非公式RSS）: 403（初出: 不明・遅くとも 2026-06-07 には継続中 / 最終確認 2026-07-29）→ 回避策: WebSearch 経由で全ソース取得（運用安定）
- Ledge.ai（`ledge.ai`）: WebFetch 403（初出 2026-07-16 / 最終確認 2026-07-16）→ 回避策: WebSearch のスニペットで代替（本文取得は不可・手動確認推奨）
- 記事本文・一次情報ページの WebFetch 広範403（`forbes.com` / `itmedia.co.jp` / `publickey1.jp` / `mlq.ai` / `buildfastwithai.com` / `venturebeat.com` / `unite.ai` / `huggingface.co` モデルカード / `champaignmagazine.com` / `stacktr.ee` / `workos.com` / `releasebot.io` / `blogs.nvidia.com` / `investing.com` / `tech-noisy.com`）: 403（初出 2026-07-27 / 最終確認 2026-07-29。2026-07-28 に Hugging Face のモデルカード等の一次情報ページへ対象が拡大し、WebFetch は実質全滅に近い。2026-07-29 は `blog.modelcontextprotocol.io` のみ WebFetch 成功）→ 回避策: WebSearch のスニペットで代替（本文取得は不可・数値の裏取りは複数スニペットの突き合わせで実施）

## アーカイブ（採用済み・見送り）

- B-001: Product Hunt のローンチ日特定問題への対処方針を明記 — **採用済み（2026-06-10）**。`daily-sources.md` Product Hunt 備考に反映（日付不明時は幅表現）
- B-002: Business Insider Japan の料金早見表を月次定点ソースに追加 — **採用済み（2026-06-10）**。`daily-sources.md` 高優先（四半期・月次）に追加
- B-003: MM総研の確認頻度を見直す — **採用済み（2026-06-10）**。`daily-sources.md` の頻度を毎日→週1回に変更（kit 判断）
