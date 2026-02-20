# Phase 2: SuperClaw Standalone Enhancement

**Status:** DRAFTED — Awaiting Phase 1 test approval  
**Estimated Duration:** 2-3 days with parallel agents

---

## Phase 2 Objectives

### P0 — Critical
1. **Skills/Tools System** — Port essential tools from OpenClaw
   - File operations (read, write, edit)
   - Shell execution (exec)
   - Web search (Brave API)
   - Web fetch (URL content extraction)

2. **Cloud Provider Fallback** — When Ollama can't handle it
   - Claude API integration (complex reasoning)
   - Gemini API integration (cost-effective backup)
   - Automatic routing based on query complexity

### P1 — Important
3. **Signal Connector** — Complete the channel trifecta
   - signal-cli integration
   - Credential migration from OpenClaw

4. **Memory/Workspace Layer** — Persistent agent memory
   - MEMORY.md equivalent
   - Daily notes (memory/YYYY-MM-DD.md)
   - Workspace file access

### P2 — Nice to Have
5. **Cron/Scheduler** — Background tasks
   - Heartbeat system
   - Scheduled checks

6. **Multi-Session Support** — Parallel conversations
   - Session isolation
   - Cross-session messaging

---

## Architecture Additions

```
┌─────────────────────────────────────────────────────────────┐
│                    SUPERCLAW STANDALONE v2                   │
├─────────────────────────────────────────────────────────────┤
│  Phase 1 (DONE)                                              │
│  ├── Gateway (Fastify)                                      │
│  ├── Sessions (SQLite)                                      │
│  ├── LLM (Ollama)                                           │
│  └── Channels (Telegram, WhatsApp)                          │
├─────────────────────────────────────────────────────────────┤
│  Phase 2 (NEW)                                               │
│  ├── Tools System                                           │
│  │   ├── FileOps (read, write, edit)                        │
│  │   ├── ShellExec (sandboxed)                              │
│  │   ├── WebSearch (Brave)                                  │
│  │   └── WebFetch (content extraction)                      │
│  ├── Provider Router                                         │
│  │   ├── Ollama (local, primary)                            │
│  │   ├── Claude (cloud, complex)                            │
│  │   └── Gemini (cloud, budget)                             │
│  ├── Memory Layer                                            │
│  │   ├── Workspace access                                   │
│  │   ├── Memory search                                      │
│  │   └── Context injection                                  │
│  └── Signal Connector                                        │
└─────────────────────────────────────────────────────────────┘
```

---

## Agent Assignments (Ready to Deploy)

| Agent | Focus | Priority |
|-------|-------|----------|
| Impl-Tools-FileOps | File read/write/edit | P0 |
| Impl-Tools-Shell | Shell execution | P0 |
| Impl-Tools-Web | Search + fetch | P0 |
| Impl-Provider-Router | Cloud fallback routing | P0 |
| Impl-Signal | Signal connector | P1 |
| Impl-Memory | Workspace/memory layer | P1 |
| Impl-Cron | Scheduler system | P2 |

---

## Success Criteria — Phase 2

```bash
superclaw standalone start --channels telegram,whatsapp,signal
```

Delivers:
- ✅ All Phase 1 features
- ✅ Tool execution (files, shell, web)
- ✅ Cloud fallback (Claude, Gemini)
- ✅ Signal channel
- ✅ Persistent memory
- ✅ Background tasks (optional)

---

## Timeline

| Day | Focus | Agents |
|-----|-------|--------|
| 1 | Tools system (file, shell, web) | 3-4 |
| 2 | Provider router + Signal | 2-3 |
| 3 | Memory layer + integration | 2-3 |

---

**Awaiting Daniel's test results and go-ahead.**
