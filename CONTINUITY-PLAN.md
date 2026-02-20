# OpenClaw Continuity Plan

**Document Version:** 1.0  
**Date:** February 20, 2026  
**Status:** DRAFT — Pending Review  
**Classification:** Internal Strategic Planning

---

## Executive Summary

Following OpenAI's acquisition of OpenClaw (February 15, 2026), this document outlines strategies to ensure operational continuity regardless of upstream changes to the OpenClaw project. The goal is **zero-downtime transition capability** should OpenClaw become unavailable, restricted, or strategically misaligned.

---

## 1. Current State Assessment

### 1.1 What We Run Today
| Component | Location | Status |
|-----------|----------|--------|
| OpenClaw Gateway | `/home/toba/openclaw/` | Production |
| OpenClaw Source (forked) | `/home/toba/openclaw-source/` | Archived pre-acquisition |
| SuperClaw Extension | `/home/toba/superclaw/` | Production |
| Local LLMs (Ollama) | `http://127.0.0.1:11434` | Operational |

### 1.2 Current Dependencies
| Dependency | Risk Level | Notes |
|------------|------------|-------|
| OpenClaw core runtime | **HIGH** | Acquisition target |
| Anthropic API (Claude) | Medium | Primary model, paid |
| Google API (Gemini) | Low | Backup provider |
| Ollama (local) | **None** | Fully self-hosted |
| Node.js runtime | None | Open source |

### 1.3 Pre-Acquisition Snapshot
- **License at fork:** MIT (permissive, allows modification/distribution)
- **Fork date:** Pre-February 15, 2026
- **Commit hash:** [Document actual hash]
- **Location:** `/home/toba/openclaw-source/`

---

## 2. Risk Analysis

### 2.1 Potential Threats

| Threat | Probability | Impact | Timeline |
|--------|-------------|--------|----------|
| License change (proprietary) | Medium | High | 3-12 months |
| Feature paywalling | High | Medium | 1-6 months |
| OpenAI API lock-in | Medium | High | 6-18 months |
| Project abandonment | Low | High | 12+ months |
| Telemetry/data collection | High | Medium | Immediate |
| Breaking changes (forced upgrades) | Medium | Medium | Ongoing |

### 2.2 Warning Signs to Monitor
- [ ] License file changes in upstream repo
- [ ] New Terms of Service requirements
- [ ] Mandatory cloud features / account requirements
- [ ] Removal of self-hosting documentation
- [ ] API endpoint changes requiring OpenAI auth
- [ ] Community fork activity (indicates others see same risks)

---

## 3. Mitigation Strategies

### 3.1 Immediate Actions (Complete Within 7 Days)

| Action | Owner | Status |
|--------|-------|--------|
| Verify local fork is complete and buildable | Chris | ☐ Pending |
| Document current configuration (export all settings) | Chris | ☐ Pending |
| Archive all skills/plugins locally | Chris | ☐ Pending |
| Test Ollama-only operation (no cloud APIs) | Chris | ☐ Pending |
| Inventory all API keys and their purposes | Chris | ☐ Pending |

### 3.2 Short-Term Actions (30 Days)

| Action | Owner | Status |
|--------|-------|--------|
| Evaluate ZeroClaw as primary alternative | Chris | ☐ Pending |
| Build SuperClaw standalone mode (no OpenClaw dependency) | Chris | ☐ Pending |
| Create automated backup of workspace/memory | Chris | ☐ Pending |
| Document migration runbook | Chris | ☐ Pending |
| Test full stack on Jetson Orin (air-gapped) | Chris | ☐ Pending |

### 3.3 Long-Term Actions (90 Days)

| Action | Owner | Status |
|--------|-------|--------|
| Establish relationship with community fork maintainers | Daniel | ☐ Pending |
| Contribute to ZeroClaw/alternative to ensure viability | Chris | ☐ Pending |
| Build provider abstraction layer (swap runtimes easily) | Chris | ☐ Pending |
| Create "escape pod" deployment script | Chris | ☐ Pending |

---

## 4. Fallback Options (Ranked)

### Option A: Community Fork (Fastest)
**Timeline:** 1-3 days  
**Effort:** Low  
**Risk:** Depends on fork maintainer commitment

Switch to an actively maintained community fork:
- **ZeroClaw** — Rust rewrite, edge-first, 22+ providers
- **KimiClaw** — Cloudflare Workers, Kimi K2.5 default
- **NanoClaw** — Container isolation, Claude Agent SDK

**Procedure:**
1. Stop OpenClaw gateway
2. Clone alternative repo
3. Migrate configuration
4. Migrate workspace/memory files
5. Update systemd service
6. Restart

### Option B: Frozen Fork (Most Control)
**Timeline:** 1 week  
**Effort:** Medium  
**Risk:** No upstream security patches

Run our pre-acquisition fork indefinitely:
1. Build from `/home/toba/openclaw-source/`
2. Apply only critical security patches manually
3. Maintain as internal project

**Pros:** Full control, known working state  
**Cons:** Security maintenance burden, no new features

### Option C: SuperClaw Standalone (Strategic)
**Timeline:** 2-4 weeks  
**Effort:** High  
**Risk:** Development time required

Evolve SuperClaw to operate independently:
1. Abstract OpenClaw interfaces
2. Implement core gateway functions natively
3. Use `llm-run` CLI adapter for all providers
4. Migrate session/memory management

**Pros:** Our code, our rules, multi-provider native  
**Cons:** Significant development effort

### Option D: Full Stack Replacement
**Timeline:** 1-2 months  
**Effort:** Very High  
**Risk:** Feature gaps during transition

Build or adopt entirely new agent framework:
- Claude Code CLI (Anthropic official)
- Aider / Continue / other open tools
- Custom orchestration on SWAI

**Pros:** Clean slate, no legacy baggage  
**Cons:** Longest timeline, feature regression

---

## 5. Provider Independence Matrix

| Provider | CLI Tool | API Cost | Offline Capable | Status |
|----------|----------|----------|-----------------|--------|
| Ollama (local) | `ollama run` | **FREE** | ✅ Yes | ✅ Ready |
| Claude | `claude` | $3-15/M | ❌ No | ✅ Ready |
| Gemini | `gemini` | $0.075/M | ❌ No | ✅ Ready |
| Kimi K2.5 | `llm-run kimi` | $0.60/M | ❌ No | ⚠️ Needs setup |
| DeepSeek | `llm-run deepseek` | $0.14/M | ❌ No | ⚠️ Needs credits |
| Codex | `codex` | Variable | ❌ No | ✅ Ready |

### Local Model Inventory (Ollama)
| Model | Size | Use Case | VRAM |
|-------|------|----------|------|
| dolphin-llama3:8b | 4.6GB | Simple tasks | 6GB |
| dolphin-llama3:70b | 40GB | Complex reasoning | 48GB+ |
| qwen3-coder | 18GB | Code generation | 20GB |

**Hardware:** RTX 4090 (16GB VRAM) can run 8B-32B models comfortably.

---

## 6. Data Portability

### 6.1 Critical Data to Preserve
| Data | Location | Backup Strategy |
|------|----------|-----------------|
| Workspace files | `/home/toba/.openclaw/workspace/` | Git + offsite |
| Memory files | `workspace/memory/` | Git + offsite |
| Credentials | `/home/toba/.openclaw/credentials/` | Encrypted backup |
| Configuration | `/home/toba/.openclaw/config/` | Git + offsite |
| Session history | SQLite DBs | Daily backup |
| Skills | `workspace/skills/` | Git + offsite |

### 6.2 Export Procedures
```bash
# Full workspace backup
tar -czvf openclaw-backup-$(date +%Y%m%d).tar.gz \
  /home/toba/.openclaw/workspace \
  /home/toba/.openclaw/config \
  --exclude='*.sqlite'

# Credentials (encrypt separately)
tar -czvf credentials-$(date +%Y%m%d).tar.gz \
  /home/toba/.openclaw/credentials

# Encrypt credentials backup
gpg --symmetric --cipher-algo AES256 credentials-*.tar.gz
```

---

## 7. Transition Runbook

### 7.1 Emergency Transition (OpenClaw stops working)

**Time to recover:** <4 hours

```bash
# 1. Stop current gateway
sudo systemctl stop openclaw-gateway

# 2. Clone ZeroClaw (fastest alternative)
cd /home/toba
git clone https://github.com/theonlyhennygod/zeroclaw.git
cd zeroclaw

# 3. Build
cargo build --release

# 4. Migrate config
cp /home/toba/.openclaw/config/*.yaml ./config/

# 5. Migrate workspace
ln -s /home/toba/.openclaw/workspace ./workspace

# 6. Start
./target/release/zeroclaw gateway start
```

### 7.2 Planned Migration (Proactive switch)

**Time to complete:** 1-2 weeks

1. **Week 1:** Parallel operation
   - Run new system alongside OpenClaw
   - Validate all features work
   - Test all integrations (WhatsApp, Telegram, etc.)

2. **Week 2:** Cutover
   - Migrate remaining data
   - Update DNS/routing
   - Decommission OpenClaw
   - Monitor for issues

---

## 8. Decision Matrix

**When to trigger migration:**

| Condition | Action |
|-----------|--------|
| OpenClaw requires OpenAI account | Evaluate alternatives |
| License changes to non-permissive | Fork immediately |
| Critical security vuln, no patch | Fork and patch ourselves |
| Features paywalled we depend on | Migrate to fork/alternative |
| Community consensus to fork | Join community effort |
| OpenClaw service discontinued | Execute emergency runbook |

---

## 9. Communication Plan

### Internal (Team)
- Notify team of any upstream changes within 24 hours
- Share this document with key stakeholders
- Monthly review of risk indicators

### External (If publishing SuperClaw)
- Position as "OpenClaw-compatible, provider-independent"
- Emphasize governance and multi-provider support
- Avoid direct criticism of OpenAI (professional tone)

---

## 10. Review Schedule

| Review Type | Frequency | Next Review |
|-------------|-----------|-------------|
| Risk indicators | Weekly | Feb 27, 2026 |
| Full plan review | Monthly | Mar 20, 2026 |
| Fallback testing | Quarterly | May 2026 |

---

## Appendix A: Alternative Projects

| Project | URL | Notes |
|---------|-----|-------|
| ZeroClaw | github.com/theonlyhennygod/zeroclaw | Rust, edge-first |
| KimiClaw | github.com/yksanjo/KimiClaw | Cloudflare Workers |
| NanoClaw | github.com/qwibitai/nanoclaw | Container isolation |
| Claude Code | anthropic.com | Official Anthropic CLI |
| Aider | aider.chat | Git-focused coding agent |

---

## Appendix B: Key Contacts

| Role | Contact | Notes |
|------|---------|-------|
| ZeroClaw maintainer | TBD | Establish relationship |
| OpenClaw community | Discord | Monitor sentiment |
| Anthropic | Enterprise support | Backup if needed |

---

## Document History

| Version | Date | Author | Changes |
|---------|------|--------|---------|
| 1.0 | 2026-02-20 | Chris | Initial draft |

---

**Prepared by:** Chris (Digital Familiar)  
**For:** Daniel Heiwig, Black Eagle Project  
**Classification:** Internal — Not for distribution without approval
