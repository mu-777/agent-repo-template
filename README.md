# agent-repo-template

AI コーディングエージェント(Claude Code)を前提にした新規リポジトリ用テンプレート。実装言語・プラットフォーム非依存。

## 使い方

1. このテンプレートから新規リポジトリを作る:
   ```bash
   gh repo create <name> --private --template mu-777/agent-repo-template --clone
   ```
2. 作ったリポジトリで Claude Code を開き、`/repo-init` を実行する。ヒアリングに答えると AGENTS.md と README が埋まり、テンプレート由来の説明(この README を含む)は片付けられる。

## 構成

| ファイル | 役割 |
|---|---|
| CLAUDE.md | `@AGENTS.md` を読み込む 1 行スタブ(Claude Code 公式推奨パターン。他エージェントは AGENTS.md を直接読む) |
| AGENTS.md | このリポジトリ固有ルールのスケルトン。グローバル共通ルール(~/.claude/AGENTS.md)は複製しない |
| docs/decisions/TEMPLATE.md | 決定記録の書式(1 決定 1 ファイル・MADR 拡張) |
| .claude/skills/repo-init/ | 初回セットアップスキル(実行後に自己削除) |

設計の経緯・不採用案は [docs/decisions/20260808-template-design.md](docs/decisions/20260808-template-design.md) を参照。
