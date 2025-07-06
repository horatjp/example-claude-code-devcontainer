---
description: "Issue番号を指定して実際のコード修正・開発を実行"
allowed-tools: Read, Write, Edit, MultiEdit, LS, Bash, Glob, Grep, Task
---

# Issue Fix Command

Issue番号: $ARGUMENTS

## 実行手順

1. **Issue番号の取得**
   - 引数: $ARGUMENTS (例: 001)

2. **ファイル検索**
   - Issues/doing/issue-$ARGUMENTS-*.md を検索
   - ファイルが見つからない場合はエラー表示

3. **実装実行**
   - 該当Issueファイルの内容に基づいて実際のコード修正・開発を実行
   - 計画に従って段階的に実装

4. **実装完了確認**
   - 実装内容の動作確認
   - 必要に応じてテスト実行

## 実行内容

指定されたIssue番号 $ARGUMENTS の問題を解決するため、実際のコード修正・開発を実行してください。

1. まず Issues/doing/issue-$ARGUMENTS-*.md ファイルを検索して読み込む
2. 問題の詳細と実装計画を理解する
3. 実装計画に従って以下を実行：
   - 必要なファイルの作成・編集
   - コードの実装・修正
   - 設定ファイルの更新
   - 依存関係の追加
4. 実装完了後の確認：
   - 動作確認
   - エラーチェック
   - 基本的なテスト実行
5. 実装結果をIssueファイルに記録：
   - 実装内容の概要
   - 変更されたファイル一覧
   - 残課題があれば記録

実装完了後、「Issue $ARGUMENTS の修正・開発が完了しました。レビューが必要な場合は /project:issue-review $ARGUMENTS を実行してください」と報告してください。