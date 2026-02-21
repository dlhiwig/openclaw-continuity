# OpenClaw Continuity 🦊

**SuperClaw Standalone MVP — OpenClaw-independent runtime**

## Status: Phase 2 In Progress

### ✅ Phase 1 Complete (45 min vs 6-day plan!)

| Component | Status | Notes |
|-----------|--------|-------|
| Gateway | ✅ | Fastify @ http://localhost:3737 |
| LLM | ✅ | Ollama (dolphin-llama3:8b, ~100ms) |
| Sessions | ✅ | SQLite persistence with context |
| Telegram | ✅ | @DHiwigBot via grammY |
| WhatsApp | ✅ | +14722089375 via Baileys |

### 🔄 Phase 2 In Progress

| Component | Status | Agent |
|-----------|--------|-------|
| Signal | ✅ Complete | signal-cli v0.13.23 |
| Smart Router | ✅ Complete | Ollama → Claude → Gemini |
| Tools | ✅ Complete | file-ops, shell, web-search, web-fetch |
| Memory Layer | 🔄 Building | Workspace persistence |
| API Keys | 🔄 Fixing | dotenv loading |

## Quick Start

```bash
# Install
cd /home/toba/superclaw
npm install

# Start with channels
npx tsx src/standalone/index.ts --channels telegram

# Or with all channels
npx tsx src/standalone/index.ts --channels telegram,whatsapp,signal
```

## Architecture

```
Phone/Telegram/WhatsApp/Signal
           ↓
    Channel Connectors
           ↓
    Gateway (Fastify:3737)
           ↓
    Smart Router
           ↓
    Ollama (90%) / Claude / Gemini
           ↓
    SQLite Sessions + Tools
```

## Provider Chain

```
Ollama (FREE, local) → Claude (complex) → Gemini (fallback)
```

- **Ollama handles ~90% of requests at $0 cost**
- Cloud fallback for complex reasoning tasks

## Channel Connectors

| Channel | Library | Status |
|---------|---------|--------|
| Telegram | grammY | ✅ @DHiwigBot |
| WhatsApp | Baileys | ✅ +14722089375 |
| Signal | signal-cli | ✅ subprocess |

## Tools

| Tool | Description |
|------|-------------|
| file-ops | Read/write/list files |
| shell | Execute commands (sandboxed) |
| web-search | Brave API search |
| web-fetch | URL content extraction |

## Path Sandboxing

Tools restricted to:
- `/tmp`
- `/home/toba/superclaw`
- `/home/toba/.openclaw/workspace`

## Related

- [SuperClaw](https://github.com/dlhiwig/superclaw) — Full swarm orchestration
- [OpenClaw](https://github.com/openclaw/openclaw) — Original project

---

*SKYNET-ALPHA Sprint: Feb 20-26, 2026*
