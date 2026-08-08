# AI エージェント用リポジトリテンプレートの設計(2026-08-08 決定)

既存リポジトリ(my-life-os / dayglassbar / MindMeshMap / kanji-verse / blogs / game_ideation)の CLAUDE.md・.claude・docs を横断調査し、リポジトリ非依存で流用できる運用パターンを新規リポジトリ用テンプレートとして固めた。このファイルはテンプレート自身の設計記録であり、テンプレートから作られたリポジトリでは /repo-init が削除する。

## 決定

1. **配布方式**: GitHub Template Repository(private)+ 同梱の `/repo-init` スキルによる自己ブートストラップ(ヒアリング → 空欄記入 → 自己削除)
2. **指示書構成**: CLAUDE.md は `@AGENTS.md` の 1 行スタブ。AGENTS.md にはリポジトリ固有の事実のみ(グローバル ~/.claude/AGENTS.md と重複させない)。200 行以下・コードで分かることは書かない
3. **決定記録**: `docs/decisions/YYYYMMDD-<slug>.md` の 1 決定 1 ファイル。書式は MADR を拡張(不採用案と理由=逆戻りガード・前提と再検討条件・追記式更新)
4. **learnings**: 生の学びファイルを持たず、コミットされる行き先に蒸留する(AGENTS.md 地雷リスト / .claude/rules/ paths 指定 / docs/decisions / docs/<topic> / skills / グローバル AGENTS.md)。Auto memory は揮発性キャッシュ扱い
5. **人間向け解説資料は HTML**(自己完結)。Claude が読む作業ドキュメントは md

## 理由

- Template Repository は履歴を引き継がず 1 コマンドで複製でき、追加ツール不要。新リポジトリの最初のセッションは必ず Claude Code なので、プレースホルダ記入は Actions ではなくスキルの対話で行うのが簡単(CI 不要・ヒアリング可能)
- `@AGENTS.md` スタブは Claude Code 公式ドキュメント記載の推奨パターン。Codex 等 AGENTS.md を直接読むエージェントとの互換も取れる
- 日付プレフィックスのファイル名は並行ブランチで連番衝突せず、時系列ソートが付く。小さい独立ファイルは Grep で該当決定だけ読める
- 複数マシンで開発するため、学びはすべて git 同期される場所に置く必要がある。`.claude/rules/` の paths 指定は「コミットされ・該当領域を触ったときだけロードされる」公式機構で、常時ロードの 200 行予算を消費しない

## 不採用案と理由(逆戻りガード)

- **Actions による template-cleanup**(JetBrains intellij-platform-plugin-template 方式) — 対話ヒアリングができず、CI 設定・実行を要する。エージェントが常に居る前提ならスキルで足りる
- **/new-repo グローバルスキルでスキャフォールド** — テンプレート内容がグローバル設定側に埋まり、テンプレート自体の版管理・レビューがしにくい
- **cookiecutter 等の scaffold ツール** — 追加ツール依存。プレースホルダ構文がファイルを汚す
- **決定記録の連番方式(0001-)** — 並行ブランチで番号が衝突する
- **決定記録の単一ファイル §N 方式** — 1 ファイルが肥大し、読み込みコストが上がる
- **learnings.md(単一ファイル)** — ロードする機構がなく死蔵するか、常時ロードで肥大するかの二択
- **Auto memory を learnings の正にする** — マシンローカルで同期されない。複数マシン開発と両立しない
- **autoMemoryDirectory をリポジトリ内に向けて Auto memory をコミット** — 未レビューのメモが履歴に混ざる・複数マシンでコンフリクト・「コミットは指示時のみ」の運用と常時書き込みが噛み合わない

## 前提と再検討の条件

- Claude Code は AGENTS.md をネイティブに読まない(2026-08 時点、anthropics/claude-code#34235 が open)。ネイティブ対応されたら CLAUDE.md スタブは不要になる
- `.claude/rules/` の paths 指定・Auto memory の仕様(2026-08 時点の公式ドキュメント)が前提。仕様変更時は learnings の行き先を見直す
- テンプレートの更新は既存リポジトリへ伝播しない(新規作成時のみ反映)。既存リポジトリへの遡及適用はしない方針

## 更新

(追記式)
