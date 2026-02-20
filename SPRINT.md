# SuperClaw Independence Sprint

**Mission:** Build a fully standalone SuperClaw MVP in 6 days  
**Start:** February 20, 2026 08:34 EST  
**Target Completion:** February 26, 2026 08:00 EST  
**Codename:** SKYNET-ALPHA

---

## Success Criteria

A single command that:
```bash
superclaw standalone start
```

Delivers:
- ✅ All channels operational (WhatsApp, Telegram, Signal)
- ✅ Memory/workspace intact and portable
- ✅ Multi-provider LLM routing (Ollama → Claude → Gemini)
- ✅ Skills system functional
- ✅ Zero OpenClaw dependencies

---

## Sprint Timeline

### Day 0 — TODAY (Feb 20) — Foundation
| Hour | Task | Owner | Status |
|------|------|-------|--------|
| 08:00-10:00 | Verify pre-acquisition fork builds | Agent-Core | ☐ |
| 10:00-12:00 | Architecture document for standalone | Agent-Core | ☐ |
| 12:00-14:00 | Set up sprint tracking in repo | Chris | ☐ |
| 14:00-16:00 | Inventory OpenClaw dependencies | Agent-Core | ☐ |
| 16:00-18:00 | Design standalone gateway contract | Agent-Core | ☐ |
| 18:00-20:00 | Ollama integration verification | Agent-Provider | ☐ |

### Day 1 (Feb 21) — Core Runtime
| Hour | Task | Owner | Status |
|------|------|-------|--------|
| 08:00-12:00 | Standalone HTTP gateway (Fastify) | Agent-Core | ☐ |
| 12:00-16:00 | Session management (SQLite) | Agent-Core | ☐ |
| 16:00-20:00 | Memory/workspace layer | Agent-Core | ☐ |
| 20:00-24:00 | Basic CLI entrypoint | Agent-Core | ☐ |

### Day 2 (Feb 22) — LLM Routing
| Hour | Task | Owner | Status |
|------|------|-------|--------|
| 08:00-12:00 | Provider abstraction layer | Agent-Provider | ☐ |
| 12:00-16:00 | Ollama adapter (primary) | Agent-Provider | ☐ |
| 16:00-20:00 | Claude/Gemini adapters (fallback) | Agent-Provider | ☐ |
| 20:00-24:00 | Cost tracking + routing logic | Agent-Provider | ☐ |

### Day 3 (Feb 23) — Channel Connectors
| Hour | Task | Owner | Status |
|------|------|-------|--------|
| 08:00-12:00 | WhatsApp connector (Baileys) | Agent-Channel | ☐ |
| 12:00-16:00 | Telegram connector (grammy/telegraf) | Agent-Channel | ☐ |
| 16:00-20:00 | Signal connector (signal-cli) | Agent-Channel | ☐ |
| 20:00-24:00 | Channel router + message bus | Agent-Channel | ☐ |

### Day 4 (Feb 24) — Integration
| Hour | Task | Owner | Status |
|------|------|-------|--------|
| 08:00-12:00 | Wire channels → gateway → LLM | All | ☐ |
| 12:00-16:00 | Skills loader (port from SuperClaw) | Agent-Core | ☐ |
| 16:00-20:00 | Tools system integration | Agent-Core | ☐ |
| 20:00-24:00 | End-to-end smoke test | All | ☐ |

### Day 5 (Feb 25) — Hardening
| Hour | Task | Owner | Status |
|------|------|-------|--------|
| 08:00-12:00 | Error handling + recovery | Agent-Core | ☐ |
| 12:00-16:00 | Migration script (OpenClaw → SuperClaw) | Agent-Core | ☐ |
| 16:00-20:00 | Escape pod one-liner | Agent-Core | ☐ |
| 20:00-24:00 | Documentation + runbook | Chris | ☐ |

### Day 6 (Feb 26) — Launch
| Hour | Task | Owner | Status |
|------|------|-------|--------|
| 08:00-10:00 | Final integration test | All | ☐ |
| 10:00-12:00 | Cut v0.1.0 release | Chris | ☐ |
| 12:00-14:00 | Parallel run alongside OpenClaw | Chris | ☐ |
| 14:00-16:00 | Go/no-go decision | Daniel | ☐ |

---

## Agent Assignments

### Agent-Core
**Focus:** Gateway, sessions, memory, CLI  
**Model:** Claude Opus (complex architecture)  
**Workdir:** `/home/toba/superclaw/src/standalone/`

### Agent-Provider  
**Focus:** LLM routing, Ollama, cost tracking  
**Model:** Ollama dolphin-llama3:8b + Claude Sonnet  
**Workdir:** `/home/toba/superclaw/src/providers/`

### Agent-Channel
**Focus:** WhatsApp, Telegram, Signal connectors  
**Model:** Claude Sonnet  
**Workdir:** `/home/toba/superclaw/src/channels/`

---

## Architecture Overview

```
┌─────────────────────────────────────────────────────────────┐
│                    SUPERCLAW STANDALONE                      │
├─────────────────────────────────────────────────────────────┤
│  CLI Entrypoint                                              │
│  └── superclaw standalone start|stop|status                 │
├─────────────────────────────────────────────────────────────┤
│  Gateway (Fastify HTTP + WebSocket)                          │
│  ├── /health                                                │
│  ├── /v1/chat                                               │
│  └── /v1/sessions                                           │
├─────────────────────────────────────────────────────────────┤
│  Channel Router                                              │
│  ├── WhatsApp (Baileys)                                     │
│  ├── Telegram (grammy)                                      │
│  └── Signal (signal-cli)                                    │
├─────────────────────────────────────────────────────────────┤
│  Session Manager                                             │
│  ├── SQLite persistence                                     │
│  ├── Memory/workspace layer                                 │
│  └── Context window management                              │
├─────────────────────────────────────────────────────────────┤
│  LLM Router                                                  │
│  ├── Ollama (local, primary)                                │
│  ├── Claude (cloud, fallback)                               │
│  ├── Gemini (cloud, fallback)                               │
│  └── Cost tracker + circuit breaker                         │
├─────────────────────────────────────────────────────────────┤
│  Skills/Tools                                                │
│  ├── Skill loader                                           │
│  ├── Tool executor                                          │
│  └── Sandbox (optional)                                     │
└─────────────────────────────────────────────────────────────┘
```

---

## Key Dependencies (No OpenClaw)

| Component | Library | Why |
|-----------|---------|-----|
| HTTP Server | fastify | Fast, typed, production-ready |
| WebSocket | @fastify/websocket | Native WS support |
| Database | better-sqlite3 | Sync SQLite, no async overhead |
| WhatsApp | @whiskeysockets/baileys | Official successor to Baileys |
| Telegram | grammy | Modern, TypeScript-first |
| Signal | signal-cli (exec) | Most reliable Signal interface |
| Ollama | ollama-js | Official Ollama client |
| Claude | @anthropic-ai/sdk | Official SDK |
| Gemini | @google/generative-ai | Official SDK |

---

## Risk Mitigations

| Risk | Mitigation |
|------|------------|
| WhatsApp auth complexity | Reuse existing Baileys session from OpenClaw |
| Signal-cli reliability | Fallback to Telegram if Signal fails |
| Ollama model quality | Route complex tasks to Claude |
| Time pressure | Parallel agent execution, MVP scope only |

---

## Definition of Done

- [ ] `superclaw standalone start` boots clean
- [ ] WhatsApp message → response works
- [ ] Telegram message → response works  
- [ ] Signal message → response works
- [ ] Ollama handles simple queries
- [ ] Claude handles complex queries
- [ ] Memory persists across restarts
- [ ] No OpenClaw imports in codebase
- [ ] Migration script tested
- [ ] Documentation complete

---

## Changelog

| Timestamp | Change | Author |
|-----------|--------|--------|
| 2026-02-20 08:34 | Sprint created | Chris |

---

*"Move fast. Stay vigilant. Build independence."*
