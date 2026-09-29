デイリーチェック対象サイト（AI業界トレンド・市場シェア・AIツール動向）

コンサル提案資料の根拠用。詳細な数値・引用文例はNotionナレッジベースに蓄積する。

## 取得方法の凡例

各ソースの「取得方法」は優先順序を示す。フォールバックの詳細は `fetch-flow.md` を参照。

- **WebSearch**: 検索エンジン経由。ゲートウェイ拒否が確定したソースの第一優先
- **WebFetch**: HTML を直接取得。**成功が続いているホストでは第一優先のまま残す**。拒否が確定したソースでも、一次ページは毎回1回だけ試す（復旧検知）
- **RSS / GoogleNewsRSS**: フィード取得。拒否が確定したフィードは第一優先にしない
- **MCP**: 専用 MCP がある一次ソースでは WebSearch より先に使う。取れても WebSearch は打ち切らない

⚠️ **到達性はホスト単位で記録する**（ベンダー単位で「到達不可」と括らない）。同一ベンダーでもホストが違えば届くことがある。
⚠️ **代替経路の連鎖**: 代替として登録したソースが落ちたとき、そのソースがカバーしていた元ソース群も同時に到達不可になる。Google News RSS がその例である（B-004採用、2026-08-26）。
⚠️ **一覧ページからはリンク先 URL（href）を列挙させる。題名からの slug 推定はしない。**

RSS URLの記載がないソースはRSS未提供。年次レポートは公開時期前後に重点確認し、それ以外の期間は月1回とする。

---

## 最優先（日次ニュースソース）
### Google News RSS（AI総合）
- RSS URL（英語）: `https://news.google.com/rss/search?q=AI+OR+"artificial+intelligence"+when:1d&hl=en-US&gl=US&ceid=US:en`
- RSS URL（日本語）: `https://news.google.com/rss/search?q=生成AI+OR+LLM+OR+ChatGPT+when:1d&hl=ja&gl=JP&ceid=JP:ja`
- 検索キーワード（WebSearch用）: `AI OR "artificial intelligence" 2026` / `生成AI LLM ChatGPT 2026` / `site:techcrunch.com AI 2026` / `site:theverge.com AI 2026` / `site:itmedia.co.jp AI 2026` / `site:techno-edge.net 2026`
- 取得方法: WebSearch → 一次の RSS / ページは毎回1回だけ WebFetch（復旧検知）
- 注目点: 英語・日本語の日次ヘッドライン。ブロック中の個別ソース（TechCrunch / The Verge / ITmedia AI+ / テクノエッジ）は、本ソースが生きているときだけ `site:` 指定で間接取得できる
- 頻度: 毎日確認
- 備考: 2026-08-26更新（B-004採用）。日次セッションで `news.google.com` がゲートウェイ拒否（`EGRESS_BLOCKED`）。英語・日本語の2フィードに加え、**TechCrunch / The Verge / ITmedia AI+ / テクノエッジの間接経路が同時に消える**。代替経路が落ちると、その経路が担っていた元ソース群も到達不可になる。ヘッドライン一覧としての定点は失われるため、上記 `site:` クエリを WebSearch で個別に回す。記事要約は元ソースの WebSearch 経由。利用規約上は個人的・非商業的利用に限定

### GIGAZINE
- URL: https://gigazine.net/
- RSS URL（優先）: https://gigazine.net/news/rss_2.0/
- 検索キーワード（WebSearch用）: `GIGAZINE AI 2026`
- 取得方法: WebSearch → 一次ページは毎回1回だけ WebFetch → RSS はフォールバック
- 注目点: テクノエッジ・ITmedia AI+の代替。AI・ソフトウェア・科学を広くカバー。毎日10〜15記事以上。ボット対策なし
- 頻度: 毎日確認
- 備考: 2026-08-26更新（B-004採用）。`gigazine.net` は日次セッションでゲートウェイ拒否（2026-08-08 確定）。フィード本文は抜粋のみ

### The Decoder
- URL: https://the-decoder.com/
- RSS URL（優先）: https://the-decoder.com/feed/
- 検索キーワード（WebSearch用）: `The Decoder AI news 2026`
- 取得方法: WebSearch → 一次ページは毎回1回だけ WebFetch → RSS はフォールバック
- 注目点: TechCrunch AI / The Verge AIの代替。AI研究・プロダクト動向が中心。ドイツ発の英語メディア。ボット対策なし
- 頻度: 毎日確認
- 備考: 2026-08-26更新（B-004採用）。`the-decoder.com` は日次セッションでゲートウェイ拒否（2026-08-10 確定）

### VentureBeat AI
- URL: https://venturebeat.com/category/ai/
- RSS URL（優先）: https://venturebeat.com/category/ai/feed/
- 検索キーワード（WebSearch用）: `VentureBeat AI news 2026`
- 取得方法: WebSearch → 一次ページは毎回1回だけ WebFetch → RSS はフォールバック
- 注目点: The Decoderと補完関係。資金調達・M&A・IPO等のディール情報とエンタープライズAI導入事例に強い。フルテキストRSS。1日45〜50記事の高ボリューム
- 頻度: 毎日確認
- 備考: 2026-08-26更新（B-004採用）。`venturebeat.com` は日次セッションでゲートウェイ拒否（2026-08-10 確定）

### Publickey
- URL: https://www.publickey1.jp/
- RSS URL（優先）: https://www.publickey1.jp/atom.xml
- 検索キーワード（WebSearch用）: `Publickey AI クラウド 2026`
- 取得方法: WebSearch → 一次ページは毎回1回だけ WebFetch → RSS はフォールバック
- 注目点: エンタープライズIT・クラウド・開発者ツール・LLM関連。M365/Copilot定着化支援等の提案根拠に直結。CloudFlare使用だがRSSエンドポイントは意図的にボット対策から除外
- 頻度: 毎日確認
- 備考: 2026-08-26更新（B-004採用）。`www.publickey1.jp` は日次セッションでゲートウェイ拒否（2026-08-12 確定）

### Hacker News AI（hnrss.org経由）
- URL: https://news.ycombinator.com/
- RSS URL（優先）: https://hnrss.org/newest?q=AI+OR+LLM&points=50
- 検索キーワード（WebSearch用）: `Hacker News AI LLM 2026`
- 取得方法: WebSearch → 一次の RSS は毎回1回だけ WebFetch（復旧検知）
- 注目点: メディアが取り上げる前のツール・プロダクトの速報を捕捉。ポイントフィルタ（50以上）でノイズ除去。RSS/Atom/JSON Feed対応
- 頻度: 毎日確認
- 備考: 2026-08-26更新（B-004採用）。`hnrss.org` は日次セッションでゲートウェイ拒否（2026-08-26 確定）。ポイント閾値付きの新着抽出は WebSearch で再現できないため、定点としての粒度は落ちる

### Product Hunt
- URL: https://www.producthunt.com/
- RSS URL（優先）: https://www.producthunt.com/feed
- 検索キーワード（WebSearch用）: `Product Hunt AI tool launch 2026`
- 取得方法: WebSearch → 一次ページは毎回1回だけ WebFetch → RSS はフォールバック
- 注目点: 新興AIツールのローンチが最も早く集まる場所。AQUAvoice等のトレンドツールはここで初出するケースが多い
- 頻度: 毎日確認
- 備考: 2026-06-10 追加（B-001採用）。WebSearch 経由では個別ツールのローンチ日特定が困難。日付不明時は「今週ローンチ」等の幅をもたせた表現で記載する。
  2026-08-26更新（B-004採用）。`www.producthunt.com` は日次セッションでゲートウェイ拒否（2026-08-16 確定）

### GitHub Trending（非公式RSS経由）
- URL: https://github.com/trending
- RSS URL（優先）: https://mshibanami.github.io/GitHubTrendingRSS/daily/python.xml
- RSS URL（補助）: https://mshibanami.github.io/GitHubTrendingRSS/daily/typescript.xml
- 検索キーワード（WebSearch用）: `GitHub trending AI python 2026`
- 取得方法: WebSearch → 一次の RSS は毎回1回だけ WebFetch（復旧検知）
- 注目点: OpenClaw等のトレンドリポジトリを検知。GitHub Actionsで日次生成・GitHub Pagesでホスト。言語別フィードあり
- 頻度: 毎日確認
- 備考: 2026-08-26更新（B-004採用）。`mshibanami.github.io` は日次セッションでゲートウェイ拒否（2026-08-25 確定）。非公式のコミュニティプロジェクト。サービス停止リスクあり。スター数・順位の鮮度は WebSearch では確認しにくい

### MM総研
- URL: https://www.m2ri.jp/
- 検索キーワード（WebSearch用）: `MM総研 生成AI 利用率 2026`
- 取得方法: WebFetch → WebSearch
- 注目点: 国内の生成AIサービス別利用率（ChatGPT/Gemini/Copilot比較）。代替不可。年40件超のプレスリリース（月3〜4件ペース）
- 頻度: 週1回確認
- 備考: 2026-06-07〜06-09 に3日連続「更新なし」のため毎日→週1回に変更（B-003採用、2026-06-10）。速報性不要の調査データであり数日遅れは許容

### モデル API 料金（主要3社）
- URL（OpenAI）: https://platform.openai.com/docs/pricing および https://openai.com/index/ の料金告知
- URL（Anthropic）: https://www.anthropic.com/pricing
- URL（Google）: https://ai.google.dev/gemini-api/docs/pricing
- 検索キーワード（WebSearch用）: `OpenAI API pricing change 2026` / `Anthropic Claude API pricing 2026` / `Gemini API pricing update 2026` / `LLM API price cut 2026`
- 取得方法: Google（`ai.google.dev`）は WebFetch（一次）→ 失敗時 WebSearch。OpenAI（`platform.openai.com` / `openai.com`）と Anthropic（`www.anthropic.com`）は WebSearch（一次ページはオリジン403のため到達不可）。到達性はホスト単位で記録する（B-004）。同一ベンダーの別ホスト（例: `developers.openai.com`）は B-028 で提案中であり、本項では未採用
- 注目点: ティア別の入力・出力単価、キャッシュ単価、値下げ/値上げ、モデル退役に伴う単価改定
- 頻度: 毎日確認
- 備考: 2026-08-02 追加（B-009採用）。`ai-tools.md` は「料金・ビジネスモデルの変更」を提案直結の最重要関心に挙げているのに、API 単価の定点ソースが1件も無かった。
  **既存の Business Insider Japan（B-002）は国内向け主要サービスの月次早見表であり、API のティア別単価を告知当日の粒度では追えない。** 2026-08-01 に OpenAI の GPT-5.6 値下げ（Luna 80%減・Terra 20%減、7/30 実施）を1日遅れで二次報道から捕捉した実例がある。
  ⚠️ **2026-08-03 更新: ベンダーごとに到達可否が分かれた。** 実行環境のネットワークポリシーに許可ドメインを追加した結果、`ai.google.dev` が復旧した。
  以下の「ゲートウェイ拒否」と「オリジン403」の定義・判定順序は `fetch-flow.md`「403 を記録する前の判定順序」に集約した（2026-08-06）。本項はその適用例である。
  - **Google（`ai.google.dev`）**: WebFetch で一次取得する（2026-08-03 に `curl` 200 を確認）。Gemini API のティア別単価は一次ページで確定させ、二次スニペットに頼らない
  - **OpenAI（`platform.openai.com` / `openai.com`）**: WebSearch を継続する。許可リスト追加でゲートウェイ拒否は解消したが、**ゲートウェイを抜けた先でサイト側が HTTP 403 を返す**ため一次本文は読めない（`www.anthropic.com` と同じ類型）
  - **Anthropic（`www.anthropic.com`）**: WebSearch を継続する（オリジン403が 2026-04-02 以降継続）

  OpenAI / Anthropic の値の裏取りは、複数の二次スニペットの突き合わせと `.last-check-state.md` の旧単価との整合確認で行う。二次情報が割れた場合は `fetch-flow.md` の併記ルールに従う


## 高優先（四半期・月次データソース）

### IDC / IDC Japan
- URL（グローバル）: https://www.idc.com
- URL（国内）: https://www.idc.com/jp
- 検索キーワード（WebSearch用）: `IDC AI market forecast 2026` / `IDC Japan AI市場予測 2026`
- 取得方法: WebFetch → WebSearch
- 注目点: グローバル・国内AI市場規模予測の基準値。主要数値は無料
- 頻度: 毎日確認
- 備考: 四半期〜半年でプレスリリース公開。公開時期が不定のため日次チェックを維持

### Similarweb AI Tracker
- URL: https://www.similarweb.com/top-websites/ai-chatbots-and-tools/
- 検索キーワード（WebSearch用）: `Similarweb AI tools traffic share 2026`
- 取得方法: WebFetch → WebSearch
- 注目点: AIツールサイトの月間訪問数・トラフィックシェア。a16zレポートのデータ提供元。トップレベル指標は無料
- 頻度: 毎日確認
- 備考: 月次更新だが公開時期が不定のため日次チェックを維持

### Business Insider Japan（AIサービス料金早見表）
- URL: https://www.businessinsider.jp/
- 検索キーワード（WebSearch用）: `Business Insider Japan AI サービス 料金 早見表 2026`
- 取得方法: WebSearch
- 注目点: 主要 AI サービスの料金・プラン変更の月次早見表。コンサル提案の料金根拠に直結
- 頻度: 月1回確認（月初〜中旬の更新を想定）
- 備考: 2026年6月版を初活用し有用と確認（B-002採用、2026-06-10）

### NRC デイリートラッキング
- URL: https://www.nrc.co.jp/
- 検索キーワード（WebSearch用）: `NRC 生成AI デイリートラッキング 2026`
- 取得方法: WebSearch
- 注目点: 2022年5月から生成AI利用経験率を日次蓄積。サービス別利用率の時系列推移を四半期レポートで無料公開。提案書で推移グラフを直接引用可
- 頻度: 週1回。四半期レポート公開時（1月・4月・7月・10月頃）は重点確認

### TLDR AI（取りこぼし検知・週次スイープ）
- URL: https://tldr.tech/ai
- 検索キーワード（WebSearch用）: `TLDR AI newsletter 2026` / `site:tldr.tech/ai 2026`
- 取得方法: WebSearch
- 注目点: 日次 WebSearch が当日話題に偏って落とす項目の検知。提案直結の提携・制度・退役・価格・セキュリティ研究
- 頻度: **週1回**（月曜想定）。直近7日分の見出しを通読し、`.last-check-state.md` に未収録の項目を catch-up 収録する
- 備考: 2026-09-21追加（B-008採用）。「必要時に参照」から高優先へ昇格。日刊ニュースレターのため日次巡回の代替ではなく**取りこぼし検知の定点**。
  ⚠️ **週次スイープの手順（同日に実施）**:
  1. TLDR AI の直近7日見出しを通読し、未収録を catch-up する
  2. 登録済み changelog / リリースノート / 製品ブログは**直近14日ぶん**のエントリ見出しを全件確認する（先頭N件だけ見ない）
  3. 退役・廃止ページでは「停止」以外の語（作成不可・新規受付終了・読み取り専用化）で書かれた期限も期限として扱う
  4. 既収録テーマの主要プレイヤーを列挙し、同枠の欠けを探す
  5. 登録済みソースで期日を記録したら、**同じ期日に別の変更が併走していないか**を二次で確認する
  6. Black Hat / DEF CON / RSA の会期中とその翌週は、発表一覧を1本ずつ突き合わせる
  7. 月1回: エージェント CLI の既定設定に影響する PoC / アドバイザリを遡って確認する

## 年次レポート（公開時期に合わせて確認）

⚠️ **公開想定月は「毎日確認」とする**（B-010採用、2026-08-02）。年次レポートは公開が単日に集中するため、週1回の確認では最大6日の遅延が構造的に生じる。実例: 2026-07-24 公表の令和8年版 情報通信白書を 08-02 まで**9日間**捕捉できなかった（企業の生成AI業務利用 86.4%〈前年度 55.2%〉・個人の利用経験 58.8%〈同 26.7%〉・業務変革で「組織的な取組はない」が日本 27.0% 対 米国 1.4% という、提案の前提数値を直接置き換える内容だった）。**取りこぼしの原因は登録漏れではなく頻度設定にある。**

### McKinsey State of AI
- URL: https://www.mckinsey.com/capabilities/quantumblack/our-insights/the-state-of-ai
- 検索キーワード（WebSearch用）: `McKinsey State of AI survey 2026`
- 取得方法: WebSearch
- 注目点: 企業AI導入率、AIエージェント浸透度。完全無料。経営層への訴求力が高い
- 頻度: 年次公開（春頃）。**3〜5月は毎日確認**（公開月が「春頃」としか特定できないため、想定期間すべてを毎日確認とする。B-010採用、2026-08-02）

### Stanford HAI AI Index
- URL: https://hai.stanford.edu/ai-index
- 検索キーワード（WebSearch用）: `Stanford HAI AI Index Report 2026`
- 取得方法: WebSearch
- 注目点: 市場全体感の概観。完全無料。投資動向・技術進化・導入率・政策を1レポートで網羅
- 頻度: 年次公開（4月）。**4月は毎日確認**、3月・5月は週1回（B-010採用、2026-08-02）

### 総務省 情報通信白書
- URL: https://www.soumu.go.jp/johotsusintokei/whitepaper/
- 検索キーワード（WebSearch用）: `総務省 情報通信白書 AI 2026`
- 取得方法: WebSearch
- 注目点: 日本のAI利用率の国際比較（日米独中4カ国）。完全無料。Excel/CSVデータあり
- 頻度: 年次公開（7月）。**7月は毎日確認**、6月・8月は週1回（B-010採用、2026-08-02）

### a16z Top 100 Gen AI Consumer Apps
- URL: https://a16z.com/100-gen-ai-apps/
- 検索キーワード（WebSearch用）: `a16z top 100 gen AI consumer apps 2026`
- 取得方法: WebSearch
- 注目点: Similarweb＋Sensor Towerデータに基づくAIアプリランキング（Web Top50＋モバイルTop50）。完全無料
- 頻度: 半年更新。**1月・7月は毎日確認**（B-010採用、2026-08-02）

### Gartner Magic Quadrant
- URL: https://www.gartner.com
- 検索キーワード（WebSearch用）: `Gartner Magic Quadrant AI 2026`
- 取得方法: WebSearch
- 注目点: ベンダー選定の権威。有料だがLeaderベンダー経由で主要MQ入手可
- 頻度: 年次（カテゴリ別に順次公開）

## 必要時に参照

### 旧日次ソース（ブロック中 — Google News RSS も拒否のため WebSearch の `site:` でカバー）

⚠️ **代替経路の連鎖（B-004採用、2026-08-26）。** 下の4媒体は本体がブロック中のため Google News RSS の `site:` 指定で間接カバーする前提だった。`news.google.com` がゲートウェイ拒否になると、**代替経路と元ソースが同時に到達不可になる。** 間接カバーは WebSearch の `site:` クエリに切り替える。RSS は復旧検知用に毎回1回だけ試す。

- **TechCrunch AI** (`techcrunch.com`): GoogleNewsRSS URL `https://news.google.com/rss/search?q=site:techcrunch.com+AI&hl=en-US&gl=US&ceid=US:en`
- **The Verge AI** (`theverge.com`): GoogleNewsRSS URL `https://news.google.com/rss/search?q=site:theverge.com+AI&hl=en-US&gl=US&ceid=US:en`
- **ITmedia AI＋** (`itmedia.co.jp`): GoogleNewsRSS URL `https://news.google.com/rss/search?q=site:itmedia.co.jp+AI&hl=ja&gl=JP&ceid=JP:ja` / RSS URL（要テスト）`https://rss.itmedia.co.jp/rss/2.0/aiplus.xml`
- **テクノエッジ** (`techno-edge.net`): GoogleNewsRSS URL `https://news.google.com/rss/search?q=site:techno-edge.net&hl=ja&gl=JP&ceid=JP:ja`

### 市場データ・調査レポート

- **Synergy Research Group** (`srgresearch.com`): クラウドシェア（AWS/Azure/GCP）データが必要な場合
- **ITR Market View** (`itr.co.jp`): 国内AIベンダー別シェアが必要な場合
- **富士キメラ総研** (`fcr.co.jp`): AI市場の4層構造分解が必要な場合
- **Sensor Tower** (`sensortower.com`): モバイルAIアプリDL数・課金額が必要な場合
- **PwC Japan 生成AI実態調査** (`pwc.com/jp/`): 日本と海外の導入格差を5カ国比較で示したい場合

### ニュースメディア・ニュースレター

- **Ledge.ai** (`ledge.ai`): 国内最大級AI特化メディア。RSS: `ledge.ai/feed/`
- **Import AI** (`importai.substack.com`): Anthropic共同創業者の一人Jack Clark著の週刊AI動向。RSS: `importai.substack.com/feed`
- **ASCII.jp** (`ascii.jp`): AI専用セクションあり。RSS: `https://ascii.jp/rss.xml`
  （TLDR AI は 2026-09-21 に高優先へ昇格・B-008。週次スイープの定点）

### 開発者コミュニティ・ベンチマーク

- **Stack Overflow Developer Survey** (`survey.stackoverflow.co`): LLM・フレームワーク別の利用率比較が必要な場合
- **LMSYS Chatbot Arena** (`arena.ai/leaderboard`): LLMモデル間の性能比較データが必要な場合
- **Zenn AIトピック** (`zenn.dev/topics/ai`): 日本語開発者コミュニティの実装情報。RSS: `https://zenn.dev/topics/ai/feed`
