# Default Role(template placeholder)

このリポは [prolegomena-yume/harness-core](https://github.com/Prolegomena-yume/harness-core) の **starter template**。新規 consumer 起こし時に以下を編集:

1. `.harness.json` の `project.name` / `linear.teamName` 等を実値に書き換え
2. 必要なら `cloud.codex.enabled = true`(cloud Codex 主経路使用時)
3. 不要な `.claude/commands/role-*.md` を削除(role 切替を使わない場合)
4. 本 CLAUDE.md を consumer 固有内容に書き換え(以下 default として残置)

---

このリポの default role は **鷹野(PDM)**。`@import` で session 起動時に context へロール定義が展開される。harness-core(submodule)経由で reach。

@.claude/_core/roles/takano.md

★ ただし CLAUDE.md / `@import` の内容は Claude Code 仕様上「**suggest 扱い**」── 逸脱が起こり得る。**確実な強制切替が必要な時は `/role-takano` slash command を撃つ**(`.claude/commands/role-takano.md` = wrapper、内部で `@.claude/_core/roles/takano.md` import + 強制適用ルール)。

# `.claude/` 配下と SessionStart hook

汎用 layer は **`.claude/_core/`**([prolegomena-yume/harness-core](https://github.com/Prolegomena-yume/harness-core) submodule)に集約。consumer 固有設定は repo root `.harness.json`。

`.claude/_core/hooks/session-init.sh` が SessionStart hook として発火し、`.harness.json` 駆動で context を会話冒頭の system context へ自動注入。

`.harness.json` schema は [.claude/_core/schema/harness.schema.json](.claude/_core/schema/harness.schema.json)、実例は [.claude/_core/docs/example.harness.json](.claude/_core/docs/example.harness.json)。

submodule update: `git submodule update --remote .claude/_core` で harness-core upstream 追従。clone 直後の `git submodule update --init --recursive` は Cloud Setup script Phase 0 で冪等吸収。

# 詳細手順

新規 consumer setup 全手順 = [.claude/_core/docs/consumer_setup.md](.claude/_core/docs/consumer_setup.md)
