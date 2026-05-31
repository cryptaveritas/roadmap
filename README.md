# CryptaVeritas — Public Roadmap

> Cryptographic verification protocol for trading signals.
> Every signal is hash-committed before reveal.

**Telegram:** [t.me/cryptaveritas](https://t.me/cryptaveritas) · **Verifier:** [cryptaveritas.github.io/cryptaveritas-verify](https://cryptaveritas.github.io/cryptaveritas-verify) · **Booklet:** [Partner booklet](https://cryptaveritas.github.io/cryptaveritas-verify/booklet.html)

---

## Overall progress

| Phase | Name | Timeline | Status |
|-------|------|----------|--------|
| 1 | CryptaSignals MVP | May 2026 | ✅ Complete |
| 2 | Growth and monetization | Weeks 3-8 | 🔄 In progress |
| 3 | Infrastructure migration | Months 3-6 | 📋 Planned |
| 4 | Full CryptaVeritas protocol | Months 6-12+ | 🔮 Future |

---

## ✅ Phase 1 — CryptaSignals MVP (May 2026)

**Goal:** Launch working Commit-Reveal protocol with cryptographic proof, Telegram bot, and public verifier.

### Completed

- [x] Commit-Reveal crypto core (SHA-256 + domain prefix + salt)
- [x] AES-256-GCM encryption with random IV
- [x] clearMasterKey() — key zeroed from memory on shutdown
- [x] SQLite WAL database with cached prepared statements
- [x] Reveal worker with isProcessing guard and forced-reveal
- [x] Time-Jacking guard (process.hrtime.bigint monitoring)
- [x] Telegram bot — primary + backup (RESERVE_BOT_TOKEN)
- [x] HTTP API: /health and /verify/:hash
- [x] Public browser verifier (HTML/JS, no dependencies)
- [x] CLI verifier (Node.js)
- [x] Full test suite: 14/14 passing on Node.js 20 LTS
- [x] GitHub Pages deployment
- [x] Telegram channel: t.me/cryptaveritas
- [x] Organization profile and roadmap (this repository)

### Security — 10 vulnerabilities closed

- [x] Replay attacks — domain prefix cryptasignals:v1|signal|
- [x] Timing attacks — crypto.timingSafeEqual
- [x] IV reuse — random IV per AES encryption
- [x] Prompt Injection — Zod .strict() + Depth Guard (20 levels)
- [x] Time-Jacking (NTP spoofing) — hrtime monitoring
- [x] SQLITE_BUSY — busy_timeout 5000ms
- [x] WAL data loss — wal_checkpoint(TRUNCATE) on graceful shutdown
- [x] Key memory leak — clearMasterKey() Buffer.fill(0)
- [x] Overlapping worker runs — isProcessing flag
- [x] DoS via nesting — LIMIT 100 in getPendingCommits

### Proof tests (staging)

- [ ] Test 1: bot.stop() error does not block clearMasterKey() and dbService.close()
- [ ] Test 2: Heap snapshot — AES key not found after clearMasterKey()
- [ ] Test 3: Worker race condition — DB close during active write

---

## 🔄 Phase 2 — Growth and Monetization (Weeks 3-8)

**Goal:** Token-gated access model, first B2B clients, legal structure on trigger.

### Access model

| Tier | Requirement | Notes |
|------|-------------|-------|
| B2C — Private signals | Hold 1,000 $CRYSIG | Offchain RPC check, hourly |
| B2B Lite — Basic API | Hold 10,000 $CRYSIG | Offchain RPC check, hourly |
| B2B Pro — Extended API | Hold 50,000 $CRYSIG | Offchain RPC check, hourly |
| Enterprise — White label | Official contract | $CRYSIG / USDC / USDT / fiat |

No fiat, no KYC, no contracts for B2C and B2B tiers.

### In progress

- [x] Telegram channel launched (t.me/cryptaveritas)
- [x] Public verifier live
- [x] Partner booklet published
- [ ] Bot staging (48h stability test)
- [ ] $CRYSIG token launch on Mainnet (after staging)
- [ ] OTC pre-launch sales via Squads v4 multisig
- [ ] Token-gated access implementation (Helius RPC)
- [ ] Drip Reveal (progressive signal disclosure)
- [ ] Multi-oracle price validation (Birdeye + Pyth)
- [ ] Reddit post in r/CryptoTechnology (waiting for karma 50+)
- [ ] Early access landing page

### Legal triggers

| Trigger | Condition | Action |
|---------|-----------|--------|
| 01 | First corporate client requesting official contract | Register legal entity (~200 EUR) |
| 02 | First Enterprise payment | Treasury multisig (2/3) accepts $CRYSIG / USDC / USDT |
| 03 | Revenue 5,000 EUR equivalent | Legal opinion on $CRYSIG (MiCA) |

### OTC mechanics (pre-launch, one-time)

- Tool: Squads v4 multisig vault (500,000 CRYSIG reserved)
- OTC price: $0.000008 per CRYSIG (20% discount from pool price)
- Pool price: $0.00001 per CRYSIG
- Client sends USDC → receives CRYSIG at fixed price
- After OTC: client sees +25% vs pool price
- Sniper protection: OTC completes before public pool creation
- After pool launch: DEX only, market price

---

## 📋 Phase 3 — Infrastructure Migration (Months 3-6)

**Goal:** Move pre-commit proofs onchain, launch marketplace, staking contract.

- [ ] Onchain pre-commit hashes → Solana (Memo Program)
- [ ] Agent reputation registry (ERC-8004) → Base
- [ ] Staking contract on Solana for B2B Lite
- [ ] Verified signal source marketplace
- [ ] Platform commission in $CRYSIG
- [ ] Soulbound NFTs for hold tenure and activity
- [ ] TradingView Pine Script indicator
- [ ] KMS/HSM for key management
- [ ] Cross-chain $CIPCRY integration (pending legal opinion)
- [ ] Community audit of smart contracts
- [ ] International trademark registration (Madrid system)
- [ ] PostgreSQL migration for Enterprise tier

---

## 🔮 Phase 4 — Full CryptaVeritas Protocol (Months 6-12+)

**Goal:** ZK proofs, decentralized validators, DeFAI ecosystem.

- [ ] ZK proofs for confidential pre-commit (Noir + zkVerify)
- [ ] Decentralized validator network with slashing
- [ ] Onchain credit scoring for AI agents
- [ ] DeFAI protocol partnerships
- [ ] Three-level ZK audit (CI/CD + AI assistants + external)
- [ ] Enterprise white-label ZK verification

---

## $CRYSIG Tokenomics

**Total supply:** 10,000,000 CRYSIG

| Category | Share | Unlock |
|----------|-------|--------|
| Team | 15% | 6-month cliff, 24 months linear |
| Treasury | 25% | Multisig 2 of 3 (Squads v4) |
| Community and airdrops | 10% | 20% immediately, 80% over 12 months |
| Marketing and partnerships | 10% | 25% immediately, 75% over 12 months |
| Initial liquidity | 40% | LP burned (CyreneAI) |

**Utility:** private signals (1,000+), B2B Lite (10,000+), B2B Pro (50,000+), buyback and burn from Enterprise revenue, governance (Phase 3+).

---

## How to verify a signal

**Browser:** [cryptaveritas.github.io/cryptaveritas-verify](https://cryptaveritas.github.io/cryptaveritas-verify)

**CLI:**
```bash
node cli-verify.js <hash> <signal_json> <salt>
```

**Hash algorithm:**
```
SHA-256( "cryptasignals:v1|signal|" + toStrictString(signal) + "|" + salt )
```

---

## Follow progress

- Telegram: [t.me/cryptaveritas](https://t.me/cryptaveritas)
- GitHub: [github.com/cryptaveritas](https://github.com/cryptaveritas)
- Verifier: [cryptaveritas.github.io/cryptaveritas-verify](https://cryptaveritas.github.io/cryptaveritas-verify)

---

*Last updated: May 2026*
