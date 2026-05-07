# ゴミ捨て当番カレンダー

Singerly社内のゴミ捨て輪番を管理するWebアプリ。  
GitHub Pages でホストし、Notion DB をデータストアとして全員が同じ状態を参照できる。

## アクセス先

**https://yuyaterui-lgtm.github.io/gomi-calendar/**

## 構成

```
ブラウザ（GitHub Pages）
  ↓ JSONP リクエスト
GAS Web App（Notion Token を安全に保持）
  ↓ Notion API
Notion DB（スケジュール + 交換履歴）
```

## 機能

- 今週の担当者を大きく表示
- 輪番順（5人）の表示
- 年間スケジュール一覧（月別・担当者フィルター付き）
- 今週分・全期間のテキストコピー
- 印刷対応

## 担当者の交換・スキップ方法

**Notion DB を直接編集する。** アプリ側には編集機能がないため、変更後にページを再読み込みすると反映される。

| 操作 | Notion での手順 |
|------|----------------|
| 担当交換 | スケジュール DB の「担当者」列を変更し、「交換済み」チェックボックスをON |
| 週のスキップ | スケジュール DB の「スキップ」チェックボックスをON |

## セットアップ（初回のみ）

### 必要なもの
- Notion Internal Integration（token: `ntn_xxx`）
- Notion スケジュール DB・交換履歴 DB（各 DB を Integration に接続済み）
- Google Apps Script Web App（`Code.gs` をデプロイ済み）

### GAS Script Properties
| キー | 値 |
|------|----|
| `NOTION_TOKEN` | Notion Integration Token |
| `SCHEDULE_DB_ID` | スケジュール DB の ID（32桁） |
| `HISTORY_DB_ID` | 交換履歴 DB の ID（32桁） |

### GAS ファイル
`~/work/ops/gas/gomi-calendar/Code.gs` を GAS プロジェクトにコピーしてデプロイ。

## ファイル構成

```
index.html   — フロントエンド（GitHub Pages で配信）
README.md    — このファイル
```

GAS コードは `~/work/ops/gas/gomi-calendar/` で管理。
