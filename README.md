# harness-starter

Starter template for [Claude Code](https://claude.com/claude-code) harness-core consumers.

新規 consumer リポを **5 分以内**で起こすための空骨格。harness-core(`prolegomena-yume/harness-core`)を submodule マウント済 + `.harness.json` placeholder + 必須 file の最小セット。

## 使い方

### 1. このリポから新規 repo を生成

GitHub UI で **「Use this template」**(右上緑ボタン)→ 新 repo 名と visibility(public/private)を選んで生成。

### 2. local に clone

```bash
git clone --recurse-submodules https://github.com/<your-org>/<your-repo>.git
cd <your-repo>
```

`--recurse-submodules` 漏れた場合:
```bash
git submodule update --init --recursive
```

### 3. `.harness.json` を編集

```bash
$EDITOR .harness.json
```

主要書き換え field:
- `project.name` / `project.displayName` ── 実 project 名
- `linear.teamName` ── 使う Linear team 名(無ければ Linear 節 skip)
- `cloud.*` ── cloud session 想定時の apt / Node / env / Codex 設定
- `install.buildTargets` ── monorepo の場合の build 対象 workspaces

詳細 schema = [.claude/_core/schema/harness.schema.json](.claude/_core/schema/harness.schema.json)

### 4. CLAUDE.md / 不要 file 整理

- `CLAUDE.md` を consumer 固有内容に書き換え(default 部分は残してよい)
- `.claude/commands/role-takano.md` / `role-ohashi.md` の不要側を削除
- consumer 固有 file(`package.json`, `AGENTS.md`, ソースコード)を追加

### 5. cloud session 想定の場合

Cloud Setup script の貼付・env vars 投入は consumer_setup.md §8 参照。

## ファイル構造

```
<your-consumer>/
├── .claude/
│   ├── _core/                   ── harness-core submodule(commit pin)
│   ├── commands/
│   │   ├── role-takano.md       ── /role-takano wrapper
│   │   └── role-ohashi.md       ── /role-ohashi wrapper
│   └── settings.json            ── SessionStart hook 登録
├── .gitmodules                  ── submodule 定義
├── .harness.json                ── consumer 設定(★ placeholder、編集必須)
├── .gitignore                   ── node_modules / .linear-token / 等
├── CLAUDE.md                    ── central canonical(★ placeholder、編集推奨)
└── README.md                    ── 本書(template 自身)── consumer 固有 README に置き換え推奨
```

## 詳細手順 doc

新規 consumer 起こしの全 step(submodule 運用 / Linear token / cloud session / role 切替 / trouble shooting)は:

→ [.claude/_core/docs/consumer_setup.md](.claude/_core/docs/consumer_setup.md)

## 既存 consumer

- [prolegomena-yume/Prolegomena](https://github.com/Prolegomena-yume/Prolegomena) ── consumer #1(monorepo フル機能)
- [prolegomena-yume/stella](https://github.com/Prolegomena-yume/stella) ── consumer #2(技術 monorepo、private)

## 関連

- harness-core: [prolegomena-yume/harness-core](https://github.com/Prolegomena-yume/harness-core)
