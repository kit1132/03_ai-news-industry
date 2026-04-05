デイリーチェック対象サイト（AI業界トレンド・市場シェア・AIツール動向）

コンサル提案資料の根拠用。詳細な数値・引用文例はNotionナレッジベースに蓄積する。

## 取得方法の凡例

- **RSS**: RSS/Atom フィードを取得し、XMLから新着エントリを抽出する
- **WebFetch**: HTMLページを直接取得する
- **WebSearch**: 検索エンジン経由で情報を取得する
- **GoogleNewsRSS**: Google News RSSフィード経由で間接取得する

各ソースの「取得方法」は優先順序を示す。フォールバック条件（403/429時の挙動、リトライ手順など）の詳細は `fetch-flow.md` を参照。

RSS URLの記載がないソースはRSS未提供。年次レポートは公開時期前後に重点確認し、それ以外の期間は月1回とする。

---

## 最優先（日次ニュースソース）
### Google News RSS（AI総合）
- RSS URL（英語）: `https://news.google.com/rss/search?q=AI+OR+"artificial+intelligence"+when:1d&hl=en-US&gl=US&ceid=US:en`
- RSS URL（日本語）: `https://news.google.com/rss/search?q=生成AI+OR+LLM+OR+ChatGPT+when:1d&hl=ja&gl=JP&ceid=JP:ja`
- 取得方法: RSS
- 注目点: ブロック中の個別ソース（TechCrunch / The Verge / ITmedia AI+ / テクノエッジ）の記事もアグリゲーション経由で間接取得可能。`site:` 指定で特定メディアに絞ることも可能
- 頻度: 毎日確認
- 備考: 利用規約上は個人的・非商業的利用に限定。ヘッドライン・URL取得の補助として使い、記事要約は元ソースのWebSearch経由で行う

### GIGAZINE
- URL: https://gigazine.net/
- RSS URL（優先）: https://gigazine.net/news/rss_2.0/
- 検索キーワード（WebSearch用）: `GIGAZINE AI 2026`
- 取得方法: RSS → WebSearch
- 注目点: テクノエッジ・ITmedia AI+の代替。AI・ソフトウェア・科学を広くカバー。毎日10〜15記事以上。ボット対策なし
- 頻度: 毎日確認
- 備考: フィード本文は抜粋のみ

### The Decoder
- URL: https://the-decoder.com/
- RSS URL（優先）: https://the-decoder.com/feed/
- 検索キーワード（WebSearch用）: `The Decoder AI news 2026`
- 取得方法: RSS → WebSearch
- 注目点: TechCrunch AI / The Verge AIの代替。AI研究・プロダクト動向が中心。ドイツ発の英語メディア。ボット対策なし
- 頻度: 毎日確認

### VentureBeat AI
- URL: https://venturebeat.com/category/ai/
- RSS URL（優先）: https://venturebeat.com/category/ai/feed/
- 検索キーワード（WebSearch用）: `VentureBeat AI news 2026`
- 取得方法: RSS → WebSearch
- 注目点: The Decoderと補完関係。資金調達・M&A・IPO等のディール情報とエンタープライズAI導入事例に強い。フルテキストRSS。1日45〜50記事の高ボリューム
- 頻度: 毎日確認

### Publickey
- URL: https://www.publickey1.jp/
- RSS URL（優先）: https://www.publickey1.jp/atom.xml
- 検索キーワード（WebSearch用）: `Publickey AI クラウド 2026`
- 取得方法: RSS → WebSearch
- 注目点: エンタープライズIT・クラウド・開発者ツール・LLM関連。M365/Copilot定着化支援等の提案根拠に直結。CloudFlare使用だがRSSエンドポイントは意図的にボット対策から除外
- 頻度: 毎日確認

### Hacker News AI（hnrss.org経由）
- URL: https://news.ycombinator.com/
- RSS URL（優先）: https://hnrss.org/newest?q=AI+OR+LLM&points=50
- 取得方法: RSS
- 注目点: メディアが取り上げる前のツール・プロダクトの速報を捕捉。ポイントフィルタ（50以上）でノイズ除去。RSS/Atom/JSON Feed対応
- 頻度: 毎日確認

### Product Hunt
- URL: https://www.producthunt.com/
- RSS URL（優先）: https://www.producthunt.com/feed
- 検索キーワード（WebSearch用）: `Product Hunt AI tool launch 2026`
- 取得方法: RSS → WebSearch
- 注目点: 新興AIツールのローンチが最も早く集まる場所。AQUAvoice等のトレンドツールはここで初出するケースが多い
- 頻度: 毎日確認

### GitHub Trending（非公式RSS経由）
- URL: https://github.com/trending
- RSS URL（優先）: https://mshibanami.github.io/GitHubTrendingRSS/daily/python.xml
- RSS URL（補助）: https://mshibanami.github.io/GitHubTrendingRSS/daily/typescript.xml
- 取得方法: RSS
- 注目点: OpenClaw等のトレンドリポジトリを検知。GitHub Actionsで日次生成・GitHub Pagesでホスト。言語別フィードあり
- 頻度: 毎日確認
- 備考: 非公式のコミュニティプロジェクト。サービス停止リスクあり

### MM総研
- URL: https://www.m2ri.jp/
- 検索キーワード（WebSearch用）: `MM総研 生成AI 利用率 2026`
- 取得方法: WebFetch → WebSearch
- 注目点: 国内の生成AIサービス別利用率（ChatGPT/Gemini/Copilot比較）。代替不可。年40件超のプレスリリース（月3〜4件ペース）
- 頻度: 毎日確認


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

### NRC デイリートラッキング
- URL: https://www.nrc.co.jp/
- 検索キーワード（WebSearch用）: `NRC 生成AI デイリートラッキング 2026`
- 取得方法: WebSearch
- 注目点: 2022年5月から生成AI利用経験率を日次蓄積。サービス別利用率の時系列推移を四半期レポートで無料公開。提案書で推移グラフを直接引用可
- 頻度: 週1回。四半期レポート公開時（1月・4月・7月・10月頃）は重点確認

## 年次レポート（公開時期に合わせて確認）

### McKinsey State of AI
- URL: https://www.mckinsey.com/capabilities/quantumblack/our-insights/the-state-of-ai
- 検索キーワード（WebSearch用）: `McKinsey State of AI survey 2026`
- 取得方法: WebSearch
- 注目点: 企業AI導入率、AIエージェント浸透度。完全無料。経営層への訴求力が高い
- 頻度: 年次公開（春頃）。3〜5月は週1回

### Stanford HAI AI Index
- URL: https://hai.stanford.edu/ai-index
- 検索キーワード（WebSearch用）: `Stanford HAI AI Index Report 2026`
- 取得方法: WebSearch
- 注目点: 市場全体感の概観。完全無料。投資動向・技術進化・導入率・政策を1レポートで網羅
- 頻度: 年次公開（4月）。3〜5月は週1回

### 総務省 情報通信白書
- URL: https://www.soumu.go.jp/johotsusintokei/whitepaper/
- 検索キーワード（WebSearch用）: `総務省 情報通信白書 AI 2026`
- 取得方法: WebSearch
- 注目点: 日本のAI利用率の国際比較（日米独中4カ国）。完全無料。Excel/CSVデータあり
- 頻度: 年次公開（7月）。6〜8月は週1回

### a16z Top 100 Gen AI Consumer Apps
- URL: https://a16z.com/100-gen-ai-apps/
- 検索キーワード（WebSearch用）: `a16z top 100 gen AI consumer apps 2026`
- 取得方法: WebSearch
- 注目点: Similarweb＋Sensor Towerデータに基づくAIアプリランキング（Web Top50＋モバイルTop50）。完全無料
- 頻度: 半年更新。1月・7月頃は週1回

### Gartner Magic Quadrant
- URL: https://www.gartner.com
- 検索キーワード（WebSearch用）: `Gartner Magic Quadrant AI 2026`
- 取得方法: WebSearch
- 注目点: ベンダー選定の権威。有料だがLeaderベンダー経由で主要MQ入手可
- 頻度: 年次（カテゴリ別に順次公開）

## 必要時に参照

### 旧日次ソース（ブロック中 — Google News RSS `site:` 指定で間接カバー）

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
- **TLDR AI** (`tldr.tech/ai`): 92万人購読の日刊AIニュースレター。取りこぼし検知に有用
- **Import AI** (`importai.substack.com`): Anthropic共同創業者の一人Jack Clark著の週刊AI動向。RSS: `importai.substack.com/feed`
- **ASCII.jp** (`ascii.jp`): AI専用セクションあり。RSS: `https://ascii.jp/rss.xml`

### 開発者コミュニティ・ベンチマーク

- **Stack Overflow Developer Survey** (`survey.stackoverflow.co`): LLM・フレームワーク別の利用率比較が必要な場合
- **LMSYS Chatbot Arena** (`arena.ai/leaderboard`): LLMモデル間の性能比較データが必要な場合
- **Zenn AIトピック** (`zenn.dev/topics/ai`): 日本語開発者コミュニティの実装情報。RSS: `https://zenn.dev/topics/ai/feed`
