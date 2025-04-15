# BigQuery Analysis MCP Server
[![smithery badge](https://smithery.ai/badge/@gotalab/bigquery-analysis-mcp-server)](https://smithery.ai/server/@gotalab/bigquery-analysis-mcp-server)

## Overview
This server is an MCP server for executing SQL queries against Google BigQuery, providing the following features:

- Query validation (dry run): Verifies if a query is valid and estimates its processing size
- Safe query execution: Only runs SELECT queries under 1TB (prevents data modifications)
- JSON-formatted results: Returns query results in structured JSON format

## Features

### Tools
- `dry_run_query` - Perform a dry run of a BigQuery query
  - Validates the query and estimates its processing size
  - Checks query size against the 1TB limit

- `run_query_with_validation` - Run a BigQuery query with validation
  - Detects and rejects DML statements (data modification queries)
  - Rejects data processing over 1TB
  - Executes queries that pass validation and returns results

## Development

### Prerequisites
- Node.js (v16 or higher)
- Google Cloud authentication setup (gcloud CLI or service account)

### Install Dependencies
```bash
npm install
```

### Build
```bash
npm run build
```

### Development Mode (Auto-rebuild)
```bash
npm run watch
```

## Installation

To use with Claude Desktop, add the server configuration:

MacOS: `~/Library/Application Support/Claude/claude_desktop_config.json`  
Windows: `%APPDATA%/Claude/claude_desktop_config.json`

```json
{
  "mcpServers": {
    "bigquery-analysis-server": {
      "command": "/path/to/bigquery-analysis-server/build/index.js"
    }
  }
}
```

### Installing via Smithery

To install BigQuery Analysis Server for Claude Desktop automatically via [Smithery](https://smithery.ai/server/@gotalab/bigquery-analysis-mcp-server):

```bash
npx -y @smithery/cli install @gotalab/bigquery-analysis-mcp-server --client claude
```

### Debugging

Since MCP servers communicate over stdio, debugging can be challenging. We recommend using the [MCP Inspector](https://github.com/modelcontextprotocol/inspector):

```bash
npm run inspector
```

The Inspector will provide a URL to access debugging tools in your browser.

## Authentication Setup

This server uses Google Cloud authentication. Set up authentication using one of the following methods:

1. Login with gcloud CLI:
   ```bash
   gcloud auth application-default login
   ```

2. Use a service account key:
   ```bash
   export GOOGLE_APPLICATION_CREDENTIALS="/path/to/service-account-key.json"
   ```

## Usage Examples

1. Dry run a query:
   ```
   dry_run_query("SELECT * FROM `bigquery-public-data.samples.shakespeare` LIMIT 10")
   ```

2. Run a query with validation:
   ```
   run_query_with_validation("SELECT word, word_count FROM `bigquery-public-data.samples.shakespeare` WHERE corpus='hamlet' LIMIT 10")
   ```

---

# BigQuery Analysis MCP Server (日本語版)

## 概要
BigQueryでSQLクエリを実行するためのMCPサーバーです。クエリの検証（ドライラン）と実行を行い、1TB以上のデータ処理や変更系クエリ（DML）を防止する安全機能を備えています。

## 機能
このサーバーはGoogle BigQueryに対してSQLクエリを実行するためのMCPサーバーで、以下の機能を提供します：

- クエリの検証（ドライラン）：クエリが有効かどうかを確認し、処理サイズを見積もる
- 安全なクエリ実行：1TB以下のSELECTクエリのみを実行（データ変更を防止）
- 結果のJSON形式での返却：クエリ結果を構造化されたJSONで返す

## 機能

### ツール
- `dry_run_query` - BigQueryクエリのドライラン実行
  - クエリの検証と処理サイズの見積もりを行う
  - 1TBの制限に対してクエリサイズをチェック

- `run_query_with_validation` - 検証付きでBigQueryクエリを実行
  - DML文（データ変更クエリ）を検出して拒否
  - 1TB以上のデータ処理を拒否
  - 検証に通過したクエリを実行し結果を返す

## 開発方法

### 前提条件
- Node.js（v16以上）
- Google Cloud認証設定（gcloud CLIまたはサービスアカウント）

### 依存関係のインストール
```bash
npm install
```

### ビルド
```bash
npm run build
```

### 開発モード（自動再ビルド）
```bash
npm run watch
```

## インストール

Claude Desktopで使用するには、サーバー設定を追加してください：

MacOS: `~/Library/Application Support/Claude/claude_desktop_config.json`  
Windows: `%APPDATA%/Claude/claude_desktop_config.json`

```json
{
  "mcpServers": {
    "bigquery": {
      "command": "node",
      "args": ["/path/to/bigquery-server/build/index.js"]
    }
  }
}
```

### デバッグ

MCPサーバーは標準入出力（stdio）を介して通信するため、デバッグが難しい場合があります。[MCP Inspector](https://github.com/modelcontextprotocol/inspector)の使用をお勧めします：

```bash
npm run inspector
```

InspectorはブラウザでデバッグツールにアクセスするためのURLを提供します。

## 認証設定

このサーバーはGoogle Cloud認証情報を使用します。以下のいずれかの方法で認証を設定してください：

1. gcloud CLIでログイン：
   ```bash
   gcloud auth application-default login
   ```

2. サービスアカウントキーを使用：
   ```bash
   export GOOGLE_APPLICATION_CREDENTIALS="/path/to/service-account-key.json"
   ```

## 使用例

1. クエリのドライラン：
   ```
   dry_run_query("SELECT * FROM `bigquery-public-data.samples.shakespeare` LIMIT 10")
   ```

2. 検証付きクエリ実行：
   ```
   run_query_with_validation("SELECT word, word_count FROM `bigquery-public-data.samples.shakespeare` WHERE corpus='hamlet' LIMIT 10")
   ```
