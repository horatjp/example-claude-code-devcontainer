---
description: "Issue番号を指定してレビューを実行し、doneステータスに移動"
allowed-tools: Read, Write, Edit, LS, Bash, Glob, Grep
---

# Issue Review Command

Issue番号: $ARGUMENTS

## 実行手順

1. **Issue番号の取得**
   - 引数: $ARGUMENTS (例: 001)

2. **ファイル検索**
   - Issues/doing/issue-$ARGUMENTS-*.md を検索
   - ファイルが見つからない場合はエラー表示

3. **Git差分分析**
   - ローカルブランチとmainブランチの差分を取得
   - 変更されたファイルと内容を分析

4. **レビュー実行**
   - 変更点を詳細に分析
   - 日本語でレビューフィードバックを作成

5. **レビューファイル作成**
   - Issues/reviews/issue-$ARGUMENTS-review.md に結果を記録

6. **ステータス変更**
   - ファイルを Issues/done/ に移動
   - 完了状態に変更

## 実行内容

指定されたIssue番号 $ARGUMENTS のレビューを実行し、完了状態に移行してください。

1. まず Issues/doing/issue-$ARGUMENTS-*.md ファイルを検索して読み込む
2. 問題の内容と実装計画を理解する
3. Git差分分析を実行：
   - 現在のブランチ名を取得
   - `git diff main...HEAD` で差分を取得
   - 変更されたファイル一覧を取得
   - 各ファイルの変更内容を分析
4. レビュー分析を実行：
   - コードの品質評価
   - 実装方針の適切性
   - 潜在的な問題点の指摘
   - 改善提案があれば記録
   - テストの充実度確認
5. レビューファイルを作成：
   - Issues/reviews/issue-$ARGUMENTS-review.md に以下を記録：
     - レビュー実行日時
     - 対象ブランチ名
     - 変更ファイル一覧
     - 変更内容の概要
     - レビューコメント（日本語）
     - 総合評価
     - 承認/改善要求の判定
6. Issueファイルを Issues/done/ に移動
7. 完了状況を記録

実行後、「Issue $ARGUMENTS のレビューが完了しました。レビュー結果は Issues/reviews/issue-$ARGUMENTS-review.md に記録されています」と報告してください。