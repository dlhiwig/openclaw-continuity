# Provider Independence Matrix

## Overview

Our goal is **zero single-provider dependency**. If any one provider becomes unavailable, operations continue.

---

## Cloud Providers

| Provider | CLI Tool | Cost (per 1M tokens) | Status | Notes |
|----------|----------|---------------------|--------|-------|
| **Claude** (Anthropic) | `claude` | $3-15 | ✅ Primary | Best reasoning |
| **Gemini** (Google) | `gemini` | $0.075 | ✅ Backup | Cost-effective |
| **Kimi K2.5** (Moonshot) | `llm-run kimi` | $0.60 in / $3 out | ⚠️ Setup needed | Native subagents |
| **DeepSeek** | `llm-run deepseek` | $0.14 in / $0.28 out | ⚠️ Needs credits | Budget option |
| **Codex** (OpenAI) | `codex` | Variable | ✅ Ready | Code generation |

---

## Local Models (Ollama)

**Zero cost, zero dependency, full offline capability.**

| Model | Size | VRAM Required | Use Case |
|-------|------|---------------|----------|
| `dolphin-llama3:8b` | 4.6 GB | 6 GB | Simple tasks, quick queries |
| `dolphin-llama3:70b` | 40 GB | 48+ GB | Complex reasoning |
| `qwen3-coder` | 18 GB | 20 GB | Code generation |

### Hardware Requirements

**Current:** RTX 4090 (16GB VRAM)
- Comfortable: 8B-32B models
- Possible with quantization: 70B models

**Recommended for full independence:**
- 2x RTX 4090 or
- RTX 5090 (32GB) or
- Jetson Orin (64GB unified)

---

## Provider Health Monitoring

```bash
# Check all providers
superclaw swarm --health

# Individual checks
claude --version
gemini --version
ollama list
```

---

## Fallback Chain

If primary provider fails, automatic fallback:

```
Claude (primary)
    ↓ (fails)
Gemini (secondary)
    ↓ (fails)
Ollama/dolphin-llama3 (local)
    ↓ (fails)
Alert human — manual intervention required
```

---

## Cost Optimization

| Query Type | Recommended Provider | Cost |
|------------|---------------------|------|
| Simple lookups | Ollama (local) | FREE |
| Code generation | Ollama/qwen3-coder | FREE |
| Medium complexity | Gemini | $0.075/M |
| Complex reasoning | Claude Sonnet | $3/M |
| Critical decisions | Claude Opus | $15/M |

**Monthly budget target:** $50-100 with local model offloading

---

## API Key Inventory

| Provider | Key Name | Location | Expiry |
|----------|----------|----------|--------|
| Anthropic | SWAI.1 | ANTHROPIC_API_KEY | None |
| Google | DEFIT | GEMINI_API_KEY | None |
| OpenAI | SUPERCLAW.1 | OPENAI_API_KEY | None |
| NVIDIA NIM | — | NVIDIA_API_KEY | None |

**Backup location:** 1Password vault (Chris.Nicholsbot@yahoo.com)

---

## Adding New Providers

1. Get API key
2. Add to `llm-run` adapter (`/usr/local/bin/llm-run`)
3. Add to SuperClaw providers (`src/swarm/providers.ts`)
4. Test with health check
5. Document in this matrix

---

## Document History

| Date | Change |
|------|--------|
| 2026-02-20 | Initial matrix |
