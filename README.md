# NovelADV - AI対話型ノベルアドベンチャーゲーム作成・プレイアプリ

iOSアプリ「NovelADV」へようこそ。SwiftUIとSwiftDataで構築された、AIと対話しながらノベルアドベンチャーを創作・プレイできるツールです。LLMがゲームマスターやナレーター、NPCを演じ、ユーザーが設定した世界観とキャラクターに基づいて動的に物語を生成します。

---

## 1. NovelADV 取扱説明書 (User Manual)

### 1.1 アプリ概要
「NovelADV」は、チャット形式でAIと物語を紡ぐインタラクティブなストーリーテリングツールです。舞台や登場人物を設定し、行動やセリフを入力すると、AIが状況描写とNPCの反応を返して物語を進めます。

### 1.2 主な機能
#### A. プロジェクト管理 (Library)
- 新規作成: テンプレート利用または白紙から新しい物語を作成
- フォルダ管理: プロジェクトをフォルダで整理
- インポート/エクスポート: `.noveladv_backup` バックアップの読込・書出し、Markdown出力

#### B. シナリオ・世界観設定 (World & Style)
- 基本設定: 場所・時代・背景ストーリー
- 文体 (Writing Style): 「ハードボイルド」「三人称視点」など描写スタイル指定
- オープニング: 物語開始時に最初に出力される描写
- ミステリーレベル: 5段階でリアリティラインを制御

#### C. キャラクター管理 (Characters)
- プレイヤーキャラクター (PC): プレイヤーが操作する主人公
- NPC: 性格・口調・関係性に基づいてAIがロールプレイ
- テンプレート: キャラクター設定を保存し、他プロジェクトで再利用

#### D. チャット & 物語進行 (Chat Interface)
- 対話: 行動やセリフを送るとAIが状況描写とNPCの応答を返す
- 序破急システム: ターン数に応じて緊張感を自動調整
- 謎・伏線管理: 会話から「謎」「伏線」を自動抽出し、解決を促す
- チェックポイント: 分岐点などで手動セーブし、巻き戻し可能
- 手動入力モード: ローカルLLM利用時などにAI応答を手動で置き換え

#### E. AI設定 (Settings)
- プロバイダー選択:
  - OpenRouter: GPT-4, Claude 3 などクラウドモデル（APIキー必須）
  - Local LLM: 端末内の `.gguf` モデルでオフライン動作
- プロンプトバージョン: v1（固定）/ v2（小説的表現重視）の切替

### 1.3 制限事項 (Free Plan)
- プロジェクト数、キャラクター数、謎の追跡数などに制限
- プレミアムで制限解除し、高性能モデルや自動メンテナンス機能を利用可能

---

## 2. NovelADV 技術仕様書 (Technical Specifications)

### 2.1 アーキテクチャ概観
- 言語/フレームワーク: Swift, SwiftUI
- データ永続化: SwiftData (SQLite)
- アーキテクチャ: MVVM + Actor（Service層）
- 非同期処理: Swift Concurrency (`async`/`await`, `Actor`)

### 2.2 データモデル (Schema V5)
`SchemaDefinition.swift` に定義されたバージョン管理スキーマを使用。

| モデル名 | 役割 | 主要プロパティ |
| :--- | :--- | :--- |
| Project | 物語全体を管理 | `scenario`, `sessions`, `activeSessionID`, `paceJoTurns`, `dataVersion` |
| Scenario | 世界観・設定 | `settingPlace`, `characters` (Relation), `mysteries` (Relation), `mysteryScale` |
| CharacterProfile | キャラクター情報 | `name`, `personality`, `firstPerson`, `relationshipWithPlayer`, `isPlayerCharacter` |
| Session | チャットセッション | `history` (Messages), `summary`, `currentChapter` |
| ChatMessage | 会話ログ | `role` (user/assistant/event), `content`, `order`, `isSummarized` |
| Mystery | 謎・伏線 | `content`, `truth`, `status` (unresolved/resolved), `resolutionPeriod` |
| Template | 再利用設定 | `ScenarioTemplate`, `CharacterTemplate` |

> モデル変更時は `AI_RULES.md` のマイグレーション手順（History作成、Schemaバージョン更新）に必ず従うこと。

### 2.3 AI ロジックとプロンプト
#### SessionManager（中核ロジック・Actor）
LLMへのプロンプトを組み立て、応答を返す。コンテキスト構成要素:
1. System Prompt: 世界観・キャラ設定、AI役割、禁止事項
2. Story Summary: 過去の物語の要約（長期記憶）
3. Recent History: 直近の会話ログ（`TokenBudgetManager` で管理）
4. Dynamic Instructions: 現在の序破急フェーズや解決すべき謎に基づく指示

Provider: `OpenRouterProvider`（Web API）または `LocalLlmProvider`（SwiftLlama/GGUF）。

#### 自動メンテナンス機能
- SummarizerService: 一定ターン毎に履歴を要約し、コンテキスト溢れを防止
- CharacterUpdaterService: 関係性や最近の出来事フィールドを更新
- MysteryUpdaterService: 会話から謎を検出・解決判定しデータ更新

### 2.4 謎・伏線システム (Mystery System)
- MysteryScale: 1〜5で謎の質を制御するSystem Promptを注入
- 解決プロセス: `resolutionPeriod` に応じて、期限が近い謎を解決させる秘密指示をプロンプトに含める

### 2.5 ファイル・データ構造
- UTType: `.noveladv_backup`（プロジェクトバックアップ）、`.noveladv_scenario`（シナリオテンプレート）、`.noveladv_character`（キャラクターテンプレート）
- Keychain: OpenRouter APIキーを保存
- App Group: 未来の拡張用構造を用意（現時点未使用）

### 2.6 外部依存ライブラリ
- StoreKit: アプリ内課金
- TipKit: チュートリアル表示
- SwiftLlama: ローカルLLM実行
- AuthenticationServices: OpenRouter OAuth認証

### 2.7 開発ルール (AI_RULES.md 抜粋)
- SwiftData: モデル変更は必ずバージョニング。既存モデルを直接改変しない
- Concurrency: `async/await` を徹底
- UI: SwiftUIを使用
- Logging: `AppLogger` でカテゴリ別ログ出力
