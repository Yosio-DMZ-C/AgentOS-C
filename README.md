# AgentOS-C

**AgentOS-C** is a portable, AI-agnostic framework for keeping a user's knowledge, decisions, procedures, context, and work state outside any single AI service.

> AIごとに自分を覚えさせるのではなく、自分のAgentOS-CへAIを接続する。

The core idea is simple: the knowledge base is the source of truth; AI memory is only a cache or shortcut. AgentOS-C separates evidence, knowledge, context, procedures, execution state, and history so that different AI systems can work with the same durable structure.

## What this repository contains

- **General design & build guide** — the canonical public design for AgentOS-C.
- **AI unpaid-user guide** — a manual-sync workflow that works even when the AI cannot directly read/write cloud storage.
- **Portable package model** — ZIP is used for transfer, onboarding, and snapshots; an expanded workspace is used when direct cloud read/write is available and efficient.

## Basic modes

### 1. Manual sync / portable package

For AI environments without direct persistent storage access:

1. Give the AgentOS-C instruction document to the AI.
2. The AI builds the initial AgentOS-C package and returns a single ZIP.
3. Save that ZIP in your persistent storage.
4. For the next update, upload the latest ZIP to the AI.
5. The AI updates only the necessary logical records, rebuilds the package, and returns the updated ZIP.

### 2. Active workspace / direct sync

When the AI can directly read and write the chosen storage:

1. The AI creates or expands the AgentOS-C workspace.
2. `START_HERE.md`, `BUILD_PLAN.md`, registry, Context, Knowledge, and Skills are used as navigation layers.
3. Only the files needed for the current task are read or updated.
4. Periodic ZIP snapshots can be produced for backup, migration, or handoff.

The logical AgentOS-C structure is the same in both modes. Moving from manual sync to direct sync is a transport change, not a rebuild.

## Start here

For the full specification, read:

- [`docs/AgentOS-C_設計・構築運用指示書_一般配布版.md`](docs/AgentOS-C_設計・構築運用指示書_一般配布版.md)
- [`docs/AgentOS-C_設計・構築運用指示書_AI無課金ユーザー版.md`](docs/AgentOS-C_設計・構築運用指示書_AI無課金ユーザー版.md)

If your AI can accept file uploads, attach the appropriate guide and send:

```text
実行
```

The AI should guide the rest of the setup and explain any user-side upload or sharing steps. If you get stuck, ask the AI from the screen or step where you stopped.

## Public repository policy

This repository is for the **public AgentOS-C specification and reusable templates only**. Do not commit a real personal knowledge base, private chat exports, purchase/health/work records, account identifiers, private cloud links, access tokens, API keys, or other secrets.

## License

MIT License. See [`LICENSE`](LICENSE).
