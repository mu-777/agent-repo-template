---
name: repo-init
description: テンプレート(agent-repo-template)から作られた新規リポジトリの初回セットアップ。ユーザーへのヒアリングで AGENTS.md の空欄と README を埋め、テンプレート由来のファイルを片付け、このスキル自身を削除する。リポジトリ作成直後の最初のセッションで一度だけ実行する。
---

# repo-init — 新規リポジトリの初回セットアップ

## 手順

1. **現状確認**: AGENTS.md・README.md を読む。既に埋まっている節はスキップする。`git remote get-url origin` が `mu-777/agent-repo-template` 自身を指す場合はテンプレートの保守作業なので、何もせず中止して報告する。
2. **ヒアリング**: 以下を確認する。一度に全部並べず会話として聞く。会話・既存ファイルから分かる項目は聞かない。未定のものは未定のまま置いてよい。
   - リポジトリの目的(1〜2 行で言えるまで)
   - プラットフォーム(Web / デスクトップ / モバイル / ゲーム / CLI / ライブラリ / 非コード)と実装言語・フレームワーク
   - コスト方針(既定: ランニングコストゼロ。バックエンド・有料サービスの要否)
   - 開発環境で自動確認できないこと(GUI・実機・OAuth・IME など)
   - 検証コマンド(lint / build / test)。ツール未定なら「ツール決定後に記入」と書く
3. **AGENTS.md を埋める**: 各節の「(未記入)」をヒアリング結果で置き換え、冒頭の repo-init 案内行を削除する。書きすぎない(200 行以下・コード/README で分かることは書かない。トークンは落とし穴に使う)。
4. **README.md を書き直す**: テンプレートの説明をすべて消し、このプロジェクトの確定事実のみで書く。
5. **決定記録**: この時点で選択肢を比較して決めたこと(技術スタック等)があれば `docs/decisions/YYYYMMDD-<slug>.md` を TEMPLATE.md の書式で作る。何も決めていなければ作らない。
6. **テンプレート由来ファイルの削除**: `docs/decisions/20260808-template-design.md`(テンプレート自身の設計記録)と `.claude/skills/repo-init/`(このスキル)を削除する。`docs/decisions/TEMPLATE.md` は残す。**Web アプリ / Web サイトでないリポジトリなら `.claude/skills/web-seo/` `.claude/skills/web-share-assets/` `.claude/skills/web-deploy/` も削除する**(Web なら残す)。
7. **報告**: 変更一覧を報告し、コミットするかユーザーに確認する(コミットは指示があったときだけ)。

## 注意

- グローバル ~/.claude/AGENTS.md と重複する内容を AGENTS.md に書かない。
- 「必ず実行させたいこと」(コミット前 lint 等)が既に決まっているなら、AGENTS.md への記載ではなく .claude/settings.json の hooks を提案する。
