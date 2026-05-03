# AI News Digest システム構成

## 概要

AIエージェント・開発ツールに特化した日次ニュースダイジェストを自動生成するシステム。コンサル提案資料の根拠データ収集を兼ねる。

毎朝、複数のAIニュースソースを巡回 → 関心領域でフィルタ → 日本語Markdownで要約 → GitHub Pagesで公開、というパイプラインで動作する。

## 実行環境

| 項目 | 内容 |
|---|---|
| 実行基盤 | Claude Code on the web（クラウド実行） |
| 実行頻度 | スケジュールタスクで毎朝自動実行 |
| ネットワーク | Full internet（外部サイトへのWebFetch/WebSearchが必要） |
| ブランチ | `main` 固定 |
| タイムゾーン | JST（Asia/Tokyo, UTC+9） |

## ディレクトリ構成

```
03_ai-news-industry/
├── CLAUDE.md                       # プロジェクト指示書（基本方針・実行手順）
├── README.md
├── index.html                      # marked.js使用のHTMLビューア
├── files.json                      # ビューア参照用ダイジェスト一覧（新しい順）
├── .last-check-state.md            # 各ソースの前回チェック状態（差分判定用）
├── .nojekyll                       # GitHub Pages設定
├── digests/
│   └── YYYY/MM/
│       └── ai-news-YYYY-MM-DD.md   # デイリーダイジェスト本体
└── .claude/
    └── rules/
        ├── sites/
        │   ├── daily-sources.md    # 対象サイト一覧・取得方法・代替URL
        │   └── fetch-flow.md       # WebFetch失敗時のフォールバックフロー
        ├── interests/
        │   └── ai-tools.md         # 関心領域・除外基準
        └── preferences/
            └── output-style.md     # 出力フォーマット・ファイル形式
```

## 使用ツール

### Claude Code 標準ツール

| ツール | 用途 |
|---|---|
| WebFetch | ソースHTML/RSSの直接取得 |
| WebSearch | 取得失敗時のフォールバック検索 |
| Read / Write / Edit | ダイジェスト・状態ファイルの読み書き |
| Bash | git操作・日付取得（`TZ=Asia/Tokyo date`） |

### 公開・閲覧

| 技術 | 用途 |
|---|---|
| GitHub Pages | ダイジェストのホスティング |
| marked.js | Markdown → HTML変換（クライアントサイド） |

## 監視ソース構造

### 最優先（日次チェック）

| ソース | 取得方法 | 注目点 |
|---|---|---|
| Google News RSS（AI総合） | RSS | 英語・日本語の総合カバレッジ。ブロック中ソースの代替 |
| GIGAZINE | RSS → WebSearch | テクノエッジ・ITmediaの代替 |
| The Decoder | RSS → WebSearch | TechCrunch AI / The Verge AIの代替 |
| VentureBeat AI | RSS → WebSearch | 資金調達・M&A・エンタープライズ導入事例 |
| Publickey | RSS → WebSearch | エンタープライズIT・クラウド・LLM |
| Hacker News AI | RSS（hnrss.org） | メディア掲載前のツール速報 |
| Product Hunt | RSS → WebSearch | 新興AIツールのローンチ |
| GitHub Trending | 非公式RSS | トレンドリポジトリ検知 |
| MM総研 | WebFetch → WebSearch | 国内生成AIサービス別利用率 |

### 高優先（四半期・月次）

- IDC / IDC Japan — グローバル・国内AI市場規模予測
- Similarweb AI Tracker — AIツールの月間訪問数・トラフィックシェア
- NRC デイリートラッキング — 生成AI利用経験率の時系列推移

### 年次レポート（公開時期に合わせて確認）

- McKinsey State of AI（春頃）
- Stanford HAI AI Index（4月）
- 総務省 情報通信白書（7月）
- a16z Top 100 Gen AI Consumer Apps（半年更新）
- Gartner Magic Quadrant（カテゴリ別に順次）

### ブロック中（Google News RSS `site:` 指定で間接取得）

- TechCrunch AI
- The Verge AI
- ITmedia AI＋
- テクノエッジ

## 取得フロー

```
1. プライマリURL → WebFetch
       │ 403 / 429 / timeout
       ▼
2. 代替URL → WebFetch
       │ 失敗
       ▼
3. WebSearch: site:ドメイン 検索キーワード 当年
       │ 結果0件
       ▼
4. WebSearch: 検索キーワード 当年（site: なし）
       │ 失敗
       ▼
5. ダイジェストに「取得不可（手動確認推奨）」と記載
```

フォールバック発生時は末尾の「改善メモ」セクションに失敗URL・ステータス・成功手段・日時を記録する。同URL2回以上の失敗で `daily-sources.md` の更新を推奨。

## 出力ポリシー

- **言語**: 日本語
- **形式**: カテゴリ分類 + 要約。各項目2〜3行、全体5〜15項目
- **トーン**: 事実ベース、冗長な前置き不要、重要度順に配置
- **重視する情報**:
  - AIプラットフォーム競争動向（OpenAI / Google / Anthropic / Microsoft）
  - 料金・ビジネスモデル変更
  - エンタープライズAI導入事例（定量成果付き）
  - 新興AIツール・プロダクトのローンチ
- **除外**: 学術論文のみ、画像/音楽生成系、AI倫理・規制議論

## 生成後フロー

1. `digests/YYYY/MM/ai-news-YYYY-MM-DD.md` を生成（ディレクトリがなければ作成）
2. `.last-check-state.md` を更新
3. `files.json` の配列先頭に新ファイルパスを追加
4. `main` ブランチに git commit + push
