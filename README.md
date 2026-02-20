# github-custom-role-permissions-watcher

GitHubのcustom organization roleのパーミッションの差分を検出してプルリクエストを作成する

## ワークフロー: Watch Organization Custom Role Permissions

`.github/workflows/watch-org-custom-role-permissions.yml`

毎月1日（UTC 00:00）に自動実行され、Organization の fine-grained permissions の一覧を取得して `data/org-custom-role-permissions.json` に保存します。前回からの差分が検出された場合、新しいブランチを作成してコミット・プッシュし、差分の内容をボディに含むプルリクエストを自動で作成します。

### 事前設定

#### 1. GitHub App の作成

このワークフローは GitHub App のトークンを使って Organization の fine-grained permissions を取得します。GitHub App の作成手順は [docs/how-to-add-github-app.md](docs/how-to-add-github-app.md) を参照してください。

以下の Secrets をリポジトリに設定してください。

| Secret 名 | 説明 |
|---|---|
| `APP_ID` | GitHub App の App ID |
| `APP_PRIVATE_KEY` | GitHub App の秘密鍵 |
| `ORGANIZATION_NAME` | 監視対象の Organization 名 |

#### 2. Workflow permissions の設定

GitHub Actions がプルリクエストを作成できるよう、リポジトリの Settings で以下を有効化してください。

`Settings > Actions > General > Workflow permissions`

- **「Allow GitHub Actions to create and approve pull requests」** にチェックを入れる

### 手動実行

`workflow_dispatch` で手動実行できます。`create_sample_pr` を `true` にすると、サンプルデータを使ってプルリクエスト作成の動作確認ができます。
