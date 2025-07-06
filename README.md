# Claude Code 開発環境テンプレート

Issue管理と開発ワークフロー用のカスタムコマンドが事前設定されたClaude Code開発用のdevcontainerテンプレートです。

## Claude Code コマンド

### `/project:issue-create "タイトル" "説明"`
- 自動採番付きで新しいIssueを作成
- `Issues/open/`に構造化されたIssueファイルを生成
- Issue番号を自動的にインクリメント

### `/project:issue-plan [issue番号]`
- Issueを分析して実装計画を作成
- Issueをopenからdoingステータスに移動
- 詳細な分析と計画をIssueに追加

### `/project:issue-fix [issue番号]`
- 実際のコード実装を実行
- 前のステップで作成した計画に従って実装
- 実装の進捗を記録

### `/project:issue-review [issue番号]`
- コードレビューと品質分析を実行
- Issueをdoingからdoneステータスに移動
- `Issues/reviews/`にレビューレポートを作成

## ディレクトリ構成

```
├── .devcontainer/
│   ├── devcontainer.json    # コンテナ設定
│   └── Dockerfile          # コンテナイメージ定義
├── .claude/
│   ├── commands/           # Claude Codeカスタムコマンド
│   │   ├── issue-create.md
│   │   ├── issue-plan.md
│   │   ├── issue-fix.md
│   │   └── issue-review.md
│   └── settings.local.json # Claude Code権限設定
└── Issues/
    ├── open/              # 新しいIssue
    ├── doing/             # 作業中のIssue
    ├── done/              # 完了したIssue
    ├── reviews/           # Issueレビュー
    └── issue-counter.json # Issue番号管理
```


## 使い方

1. **新しいIssueを作成**:
   ```
   /project:issue-create "ユーザー認証機能の追加" "ログイン・ログアウト機能を実装"
   ```

2. **実装計画を立てる**:
   ```
   /project:issue-plan 001
   ```

3. **解決策を実装**:
   ```
   /project:issue-fix 001
   ```

4. **レビューして完了**:
   ```
   /project:issue-review 001
   ```
