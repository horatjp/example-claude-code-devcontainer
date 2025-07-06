---
description: "新しいIssueを作成し、自動で番号を採番"
allowed-tools: Read, Write, LS, Bash
---

# Issue Create Command

引数: $ARGUMENTS

## 使用方法

```bash
/project:issue-create "タイトル" "説明"
```

## 実行手順

1. **引数の解析**
   - 第1引数: Issueタイトル
   - 第2引数: Issue説明（オプション）

2. **番号の自動採番**
   - `Issues/issue-counter.json` から現在のカウンターを読み込み
   - 次の番号を3桁ゼロパディング形式で生成（例: 001, 002, 003）
   - カウンターを更新

3. **Issueファイル作成**
   - `Issues/open/issue-[番号]-[タイトル].md` を作成
   - YAML frontmatter付きのテンプレートを使用

4. **作成完了報告**
   - 作成されたIssue番号とファイルパスを表示

## 実行内容

新しいIssueを作成してください。

1. 引数を解析：
   - タイトル: $ARGUMENTS の最初の引数
   - 説明: $ARGUMENTS の2番目の引数（存在すれば）

2. 番号の自動採番：
   - `Issues/issue-counter.json` を読み込み
   - 現在のcounter値を取得
   - counter値を1増加
   - 3桁ゼロパディング形式で番号を生成（例: counter=1 → "001"）
   - `Issues/issue-counter.json` を更新

3. Issueファイル作成：
   - ファイル名: `Issues/open/issue-[番号]-[タイトル].md`
   - 内容: 以下のテンプレートを使用
   - 説明がある場合は、その内容を基により詳細で構造化された内容を生成：
     - 問題の背景と影響範囲を分析
     - 具体的な実装項目を提案
     - 期待される結果を詳細化
     - 関連する技術や考慮事項を追加
   - 説明がない場合は、タイトルから推測される内容でテンプレートを埋める

```yaml
---
issue_number: [番号]
title: "[タイトル]"
status: "open"
created_at: "[現在日時]"
labels: []
---

# Issue #[番号]: [タイトル]

## 問題の詳細

[説明を基により詳細で構造化された内容を生成]

## 実行したいこと

[説明を基に具体的な実装項目を生成]

## 期待される結果

[説明を基に期待される結果を詳細化]

## 追加情報

[関連する技術や考慮事項を生成]
```

4. 作成完了報告：
   - 「Issue #[番号] を作成しました: Issues/open/issue-[番号]-[タイトル].md」
   - 「次のコマンドで作業を開始できます: /project:issue-plan [番号]」

エラーハンドリング：
- 引数が不足している場合は使用方法を表示
- counter.jsonが存在しない場合は初期化
- ファイル作成に失敗した場合はエラー表示