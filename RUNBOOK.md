# Emergency Transition Runbook

## Scenario: OpenClaw Becomes Unavailable

**Target Recovery Time:** <4 hours

---

## Pre-Flight Checks

Before any transition, verify:

- [ ] Workspace backup exists and is current
- [ ] Credentials backup exists (encrypted)
- [ ] Alternative runtime tested in last 30 days
- [ ] Team notified of potential transition

---

## Option A: ZeroClaw (Fastest)

**Time:** 1-2 hours  
**Requirements:** Rust toolchain, Linux

```bash
# 1. Stop OpenClaw
sudo systemctl stop openclaw-gateway

# 2. Clone ZeroClaw
cd /home/toba
git clone https://github.com/theonlyhennygod/zeroclaw.git
cd zeroclaw

# 3. Build
cargo build --release

# 4. Migrate workspace (symlink)
ln -s /home/toba/.openclaw/workspace ./workspace

# 5. Copy config
cp /home/toba/.openclaw/config/gateway.yaml ./config/

# 6. Start
./target/release/zeroclaw gateway start

# 7. Verify
curl http://localhost:3000/health
```

---

## Option B: Frozen Fork

**Time:** 2-3 hours  
**Requirements:** Node.js, pre-acquisition source

```bash
# 1. Stop current gateway
sudo systemctl stop openclaw-gateway

# 2. Use archived source
cd /home/toba/openclaw-source

# 3. Install dependencies
npm install

# 4. Build
npm run build

# 5. Copy current config
cp /home/toba/.openclaw/config/* ./config/

# 6. Start
npm run gateway:start

# 7. Verify
curl http://localhost:3000/health
```

---

## Option C: SuperClaw Standalone

**Time:** 4+ hours (requires development)  
**Requirements:** SuperClaw with gateway abstraction

```bash
# 1. Stop OpenClaw
sudo systemctl stop openclaw-gateway

# 2. Enter SuperClaw
cd /home/toba/superclaw

# 3. Start standalone mode (if implemented)
npm run standalone:start

# 4. Configure channels
# Edit config/channels.yaml

# 5. Verify
curl http://localhost:18800/health
```

---

## Post-Transition Checklist

- [ ] All channels responding (WhatsApp, Telegram, Signal)
- [ ] Memory files accessible
- [ ] Skills loading correctly
- [ ] Cron jobs migrated
- [ ] API keys working
- [ ] Ollama connection verified
- [ ] Test message sent successfully

---

## Rollback Procedure

If transition fails:

```bash
# Stop new system
# (varies by option)

# Restart OpenClaw (if still functional)
sudo systemctl start openclaw-gateway

# Or restore from backup
cd /home/toba
tar -xzvf openclaw-backup-YYYYMMDD.tar.gz
```

---

## Contacts

| Role | Action |
|------|--------|
| Daniel | Approve major decisions |
| Chris | Execute technical steps |
| Community | Monitor Discord for fork status |

---

## Document History

| Date | Change |
|------|--------|
| 2026-02-20 | Initial runbook |
