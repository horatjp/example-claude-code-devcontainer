---
description: "Issue番号を指定して問題を分析・計画作成し、doingステータスに移動"
allowed-tools: Read, Write, Edit, LS, Bash, Glob, Grep
---

# Issue Plan Command

Issue番号: $ARGUMENTS

## 実行手順

1. **Issue番号の取得**
   - 引数: $ARGUMENTS (例: 001)

2. **ファイル検索**
   - Issues/open/issue-$ARGUMENTS-*.md を検索
   - ファイルが見つからない場合はエラー表示

3. **問題分析・計画作成**
   - 該当Issueファイルを詳細に分析
   - 実装計画を作成
   - 必要な技術スタック、手順、考慮事項を整理

4. **ステータス変更**
   - ファイルを Issues/doing/ に移動
   - 作業開始状態に変更

## 実行内容

指定されたIssue番号 $ARGUMENTS の問題を分析し、実装計画を作成してください。

1. まず Issues/open/issue-$ARGUMENTS-*.md ファイルを検索して読み込む
2. 問題の詳細を理解し、以下の観点で分析：
   - 問題の本質と影響範囲
   - 必要な技術・ツール
   - 実装の難易度と工数
   - 依存関係とリスク
3. 具体的な実装計画を作成：
   - 実装手順の詳細
   - 各ステップの成果物
   - テスト方法
   - 完了条件
4. 分析結果をファイルに追記
5. ファイルを Issues/doing/ に移動

実行後、「Issue $ARGUMENTS の分析・計画が完了しました」と報告してください。