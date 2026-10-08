# AgentOS-C

**AgentOS-C** は、AIごとに自分を覚えさせるのではなく、**自分の知識・判断・手順・作業状態を外部に持ち、必要なAIからそこへ接続する**ための個人向けAI運用基盤です。

> AIごとに自分を覚えさせるのではなく、自分のAgentOS-CへAIを接続する。

AIの内部メモリを正本にはしません。正本はAgentOS-C側に置き、AI Memoryは短い索引やキャッシュとして使います。

## 何ができるか

AgentOS-Cでは、会話・メール・資料などの原情報を、そのままAIの「記憶」にするのではなく、根拠を保ったまま Knowledge / Context / Skill / History へ整理します。

- 本人の発言、一次資料、AIの提案、推論を分ける
- 「調べた」「欲しい」「注文した」「届いた」「持っている」を混同しない
- 過去の判断や手順を次のAIへ引き継ぐ
- AIを変更しても同じKBを使い続ける
- 修正や失敗を回答だけで終わらせず、KBや手順へ戻す
- 個人KBと一般公開用の設計・テンプレートを分離する

## 使い方は2通り

### 1. AI無課金ユーザー / クラウド直接書込なし

**ZIPによる手動同期**を使います。

1. このリポジトリの「AI無課金ユーザー版」設計書をAIへ添付します。
2. チャットで `実行` と送ります。
3. AIが初回のAgentOS-C一式を作り、`AgentOS-C_initial.zip` として返します。
4. そのZIPをGoogle Drive、OneDrive、PC、NAS等へ保存します。
5. 次回更新時は、保存してある**最新版ZIPを1個だけ**AIへ添付します。
6. AIが必要部分を更新し、更新済みZIPを返します。

利用者にファイルを一つずつ作らせる設計ではありません。AIが保存・アップロード・共有リンク取得などの操作を具体的に案内します。

### 2. クラウド直接読書きができるAI

**Active Workspace**として展開して使います。

AIが `START_HERE.md`、`BUILD_PLAN.md`、registry、Context、Knowledge、Skill を参照し、現在の作業に必要なファイルだけを読み書きします。

ZIPは主に次の用途で使います。

- 初回配布
- AI間の引越し
- バックアップ
- スナップショット
- クラウド連携できない環境との受け渡し

つまり、**ZIPは搬送・保存の形、展開Workspaceは日常運用の形**です。中身のAgentOS-Cは同じです。

## まず試す

### 一般版

[AgentOS-C 設計・構築運用指示書 — 一般配布版](docs/AgentOS-C_設計・構築運用指示書_一般配布版.md)

クラウド連携や、より完全なAgentOS-C構成を利用する場合はこちらを使います。

### AI無課金ユーザー版

[AgentOS-C 設計・構築運用指示書 — AI無課金ユーザー版](docs/AgentOS-C_設計・構築運用指示書_AI無課金ユーザー版.md)

クラウド保存先へAIが直接書き込めない場合はこちらから始めます。

どちらも基本操作は同じです。

```text
実行
```

と送れば、AIが保存先・接続状態を確認し、推奨構成を1案提示して構築を進めます。

短い手順だけ見たい場合は [QUICKSTART.md](QUICKSTART.md) を参照してください。

## Presentation

最新版の紹介スライドはこちらです。

[AgentOS-C Presentation v1.3（PowerPoint / speaker notes付き）](https://docs.google.com/presentation/d/1oOroO3_Ry_AyJMZlITOoG5Lpg6AH83t8/edit?usp=sharing)

## AgentOS-Cの基本構造

```text
AgentOS-C/
├─ START_HERE.md      # AIが最初に読む入口
├─ BUILD_PLAN.md      # 現在の作業状態・再開位置
├─ 00_system/         # 設計・台帳・ルール
├─ 01_private/        # 個人情報・私的記録
├─ 10_sources/        # 原文・根拠
├─ 20_knowledge/      # 整理済み知識
├─ 30_contexts/       # Project / Area / Resource等の入口
├─ 40_outputs/        # 派生成果物
├─ 50_skills/         # 再利用するAI作業手順
├─ 60_memory_backup/  # AI Memory等のバックアップ
├─ 70_scripts/        # 検査・補助スクリプト
├─ 80_reviews/        # 品質確認・レビュー
├─ 85_attachments/    # 大容量原本
├─ 90_history/        # 旧版・履歴
└─ 99_inbox/          # 未分類
```

初回からすべてのフォルダを作る必要はありません。用途に応じて必要な部分から増やします。

## 重要な考え方

AgentOS-Cは単なるフォルダ整理ではなく、次のライフサイクルをAIに回させるための仕組みです。

```text
Raw Source
   ↓
Evidence
   ↓
Knowledge
   ↓
Context / Skill
   ↓
AIが利用
   ↓
訂正・追加
   ↓
差分更新
   ↓
History / Review
```

使うほど、正本・Context・Skillが改善されることを狙います。

## このGitHubに入れないもの

このリポジトリは**AgentOS-Cの一般公開用仕様・テンプレート専用**です。

次のものはコミットしません。

- 実際の個人KB
- 個人のチャット履歴
- 購入履歴・健康情報・仕事情報
- Google Drive等の非公開URLやファイルID
- APIキー、秘密鍵、認証情報
- 個人用Memory Backup

実際の個人KBはGoogle Drive、OneDrive、ローカルストレージ等の**非公開の永続保存先**で管理してください。

## Release package

初回配布用パッケージは `release/` に置きます。

- 設計書
- QUICKSTART
- README
- LICENSE
- manifest

を1つのZIPにまとめ、AIへ渡しやすい形にします。

## ライセンス

MIT Licenseです。詳しくは [LICENSE](LICENSE) を参照してください。

## Status

AgentOS-Cは現在、実運用から一般化を進めている段階です。仕様は互換性を意識しつつ改善していきます。
