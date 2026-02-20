# Continuity Plan Action Checklist

## Status Key
- ☐ Not started
- 🔄 In progress
- ✅ Complete
- ⏸️ Blocked

---

## Immediate Actions (7 Days)

| # | Action | Owner | Status | Due | Notes |
|---|--------|-------|--------|-----|-------|
| 1 | Verify local fork is complete and buildable | Chris | ☐ | Feb 27 | Check `/home/toba/openclaw-source/` |
| 2 | Document current configuration | Chris | ☐ | Feb 27 | Export all gateway settings |
| 3 | Archive all skills/plugins locally | Chris | ☐ | Feb 27 | Git commit workspace/skills/ |
| 4 | Test Ollama-only operation | Chris | ☐ | Feb 27 | No cloud APIs for 1 hour |
| 5 | Inventory all API keys | Chris | ☐ | Feb 27 | Update TOOLS.md |
| 6 | Create encrypted credentials backup | Chris | ☐ | Feb 27 | GPG encrypt |

---

## Short-Term Actions (30 Days)

| # | Action | Owner | Status | Due | Notes |
|---|--------|-------|--------|-----|-------|
| 7 | Evaluate ZeroClaw as primary alternative | Chris | ☐ | Mar 20 | Clone, build, test |
| 8 | Build SuperClaw standalone mode | Chris | ☐ | Mar 20 | Abstract OpenClaw deps |
| 9 | Create automated workspace backup | Chris | ☐ | Mar 20 | Daily cron job |
| 10 | Document migration runbook | Chris | ✅ | Feb 20 | RUNBOOK.md created |
| 11 | Test full stack on Jetson Orin | Chris | ☐ | Mar 20 | Air-gapped operation |

---

## Long-Term Actions (90 Days)

| # | Action | Owner | Status | Due | Notes |
|---|--------|-------|--------|-----|-------|
| 12 | Establish relationship with fork maintainers | Daniel | ☐ | May 20 | ZeroClaw, KimiClaw |
| 13 | Contribute to ZeroClaw | Chris | ☐ | May 20 | Ensure project viability |
| 14 | Build provider abstraction layer | Chris | ☐ | May 20 | Swap runtimes easily |
| 15 | Create "escape pod" deployment script | Chris | ☐ | May 20 | One-command migration |

---

## Monitoring Tasks (Ongoing)

| Task | Frequency | Last Done | Next Due |
|------|-----------|-----------|----------|
| Check OpenClaw repo for license changes | Weekly | — | Feb 27 |
| Review community fork activity | Weekly | — | Feb 27 |
| Test fallback provider chain | Monthly | — | Mar 20 |
| Full backup verification | Monthly | — | Mar 20 |
| Review this checklist | Weekly | Feb 20 | Feb 27 |

---

## Warning Signs Detected

| Date | Indicator | Severity | Action Taken |
|------|-----------|----------|--------------|
| Feb 15 | OpenAI acquisition announced | ⚠️ High | Created this plan |
| — | — | — | — |

---

## Decision Log

| Date | Decision | Rationale | Approved By |
|------|----------|-----------|-------------|
| Feb 20 | Create continuity plan | Acquisition risk | Daniel |
| — | — | — | — |

---

## Notes

*Add any relevant observations or updates here.*

---

## Document History

| Date | Change |
|------|--------|
| 2026-02-20 | Initial checklist |
