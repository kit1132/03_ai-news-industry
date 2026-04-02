# デイリーチェック対象サイト（AI業界トレンド・市場シェア・AIツール動向）

コンサル提案資料の根拠用。詳細な数値・引用文例はNotionナレッジベースに蓄積する。

## 取得方法の凡例

- **RSS**: RSS/Atom フィードを取得し、XMLから新着エントリを抽出する
- **WebFetch**: HTMLページを直接取得する
- **WebSearch**: 検索エンジン経由で情報を取得する

各ソースの「取得方法」は優先順序を示す。フォールバック条件（403/429時の挙動、リトライ手順など）の詳細は `fetch-flow.md` を参照。

RSS URLの記載がないソースはRSS未提供。年次レポートは公開時期前後に重点確認し、それ以外の期間は月1回とする。

---

## 最優先（日次ニュースソース）

### TechCrunch AI
- URL: https://techcrunch.com/category/artificial-intelligence/
- RSS URL（優先）: https://techcrunch.com/category/artificial-intelligence/feed/
- 検索キーワード（WebSearch用）: `TechCrunch AI news 2026`
- 取得方法: RSS → WebSearch
- フィード本文: 抜粋のみ（リード文＋リンク）。詳細が必要な場合は記事URLをWebFetchで追加取得
- 注目点: AIツールの新リリース・資金調達・アップデート速報
- 頻度: 毎日確認
- 備考: RSS URLは要疎通確認。TechCrunchもCloudflare配下の可能性があり、RSSでも403を返す場合がある

### The Verge AI
- URL: https://www.theverge.com/ai-artificial-intelligence
- 検索キーワード（WebSearch用）: `The Verge AI news 2026`
- 取得方法: WebFetch → WebSearch
- 注目点: AIプロダクトのユーザー視点レビュー。「実際どう使えるか」の観点
- 頻度: 毎日確認

### ITmedia AI＋
- URL: https://www.itmedia.co.jp/aiplus/
- 検索キーワード（WebSearch用）: `ITmedia AI＋ 2026`
- 取得方法: WebFetch → WebSearch
- 注目点: 国内AI専門メディア（2024年創刊）。完全無料・日次複数本更新。ビジネス向けAIツール記事・導入事例
- 頻度: 毎日確認

### テクノエッジ
- URL: https://www.techno-edge.net/
- 検索キーワード（WebSearch用）: `テクノエッジ AI 2026`
- 取得方法: WebFetch → WebSearch
- 注目点: 「生成AIウィークリー」が週次の定点観測として有用。海外AI情報の日本語カバーが早い
- 頻度: 毎日確認

### MM総研
- URL: https://www.m2ri.jp/
- 検索キーワード（WebSearch用）: `MM総研 生成AI 利用率 2026`
- 取得方法: WebFetch → WebSearch
- 注目点: 生成AIサービス別利用率（ChatGPT/Gemini/Copilot比較）。年40件超のプレスリリース（月3〜4件ペース）
- 頻度: 毎日確認

## 高優先（四半期・月次データソース）

### Synergy Research Group
- URL: https://www.srgresearch.com/articles
- 検索キーワード（WebSearch用）: `Synergy Research cloud market share quarterly 2026`
- 取得方法: WebFetch → WebSearch
- 注目点: クラウドシェア（AWS/Azure/GCP）の決定版データ
- 頻度: 毎日確認
- 備考: 四半期末から数週間内にプレスリリース公開。公開時期が不定のため日次チェックを維持

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

### ITR Market View
- URL: https://www.itr.co.jp/
- 検索キーワード（WebSearch用）: `ITR Market View AI市場 2026`
- 取得方法: WebSearch
- 注目点: 国内AIベンダー別シェアで最高精度。プレスリリースで主要シェア数値は無料公開
- 頻度: 年次

### Gartner Magic Quadrant
- URL: https://www.gartner.com
- 検索キーワード（WebSearch用）: `Gartner Magic Quadrant AI 2026`
- 取得方法: WebSearch
- 注目点: ベンダー選定の権威。有料だがLeaderベンダー経由で主要MQ入手可
- 頻度: 年次（カテゴリ別に順次公開）

### 富士キメラ総研
- URL: https://www.fcr.co.jp/
- 検索キーワード（WebSearch用）: `富士キメラ総研 AI市場総調査 2026`
- 取得方法: WebSearch
- 注目点: AI市場を4層構造（サービス/アプリ/プラットフォーム/インフラ）で分解
- 頻度: 年次

### Sensor Tower
- URL: https://sensortower.com/
- 検索キーワード（WebSearch用）: `Sensor Tower AI apps report 2026`
- 取得方法: WebSearch
- 注目点: モバイルAIアプリのダウンロード数・課金額の業界標準データ。レポートサマリーは無料（要登録）
- 頻度: 年次〜半年

## 必要時に参照

- **Stack Overflow Developer Survey** (`survey.stackoverflow.co`): LLM・フレームワーク別の利用率比較が必要な場合
- **LMSYS Chatbot Arena** (`arena.ai/leaderboard`): LLMモデル間の性能比較データが必要な場合
- **PwC Japan 生成AI実態調査** (`pwc.com/jp/`): 日本と海外の導入格差を5カ国比較で示したい場合
