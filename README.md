# pm-notion-deliverable-writing-skill

NotionのDeliverableデータベースにある成果物の文書を、書く・推敲する・構成を変える・公開用に整えるスキル。
Claudeに頼むと、本文と未解決のコメントを読んでから構成案を表で出し、合意してから書き替える。判断の背景はLogへ移し、書き替えたあとは読み直して確かめる。

## 必要なもの

- [Claude Code](https://docs.claude.com/en/docs/claude-code/overview)
- Claudeに接続した公式の [Notion MCP](https://developers.notion.com/docs/mcp)
- NotionのDeliverableデータベース
- 背景をLogへ移すときは [pm-notion-log-record-skill](https://github.com/junyatakechi/pm-notion-log-record-skill)

## インストール

使うプロジェクトの `.agents/skills/` の中でクローンする。フォルダ名はリポジトリ名のままにする。

```bash
git clone https://github.com/junyatakechi/pm-notion-deliverable-writing-skill.git <プロジェクト>/.agents/skills/pm-notion-deliverable-writing-skill
```

- `.claude/skills` は `.agents/skills` へのリンクにしておく。Claude Code と Codex の両方から同じスキルが読まれる。

## セットアップ

値は、プロジェクトのフォルダ直下（Claude Code を起動するフォルダ）の `.env` に書く。この `.env` はプロジェクトのスキルが共有する。キーは同梱の `.env.example` と同じ。同じキーの環境変数があれば、そちらが優先される。

```
PM_DELIVERABLE_DB_URL=<DeliverableのURL>
PM_DELIVERABLE_DATA_SOURCE_ID=<Deliverableのdata source ID>
```

data source ID は、データベースのURLを渡してClaudeにNotion MCPで取得させると、`collection://` の後ろに表示される。`collection://` を除いた値を書く。既存のページを推敲するだけなら、この設定は無くても動く。

## 使い方

Claudeに普段の言葉で頼むと、Claudeがこのスキルを読み込んで作業する。

| 頼み方 | Claudeがすること |
|---|---|
| 「この文書の構成を変えたい <URL>」「推敲したい」 | 本文とコメントを読み、構成案とLogへ移すものを表で出す。合意してから書き替え、読み直して確かめる |
| 「この仕組みを設計書に書いて」 | 実ファイルを読んでから、仕組みと全文を貼る。秘密情報はプレースホルダにする |
| 「一般公開するのでプレースホルダにして」 | 具体的な名前や個人を特定できる記述を洗い出し、プレースホルダに置き換える |

### Claudeがしないこと

- 構成案に合意する前に、Notionを書き替えること
- 頼まれないのに、`重要度`・`公開範囲`・`Pinned` を設定すること
- 秘密情報の実値を本文に載せること
- 文書と実物がずれたときに、黙って文書を実物に合わせること

手順・判断基準・落とし穴は [SKILL.md](SKILL.md) にある。
