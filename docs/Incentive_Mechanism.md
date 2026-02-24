## Incentive & Mechanism Design

### Emission and Reward Logic
MuseNet operates on a **ranked, multi-tier emission model** with a rolling **Champion Carry-Over** mechanic to reward both sustained excellence and decisive upsets.

Every 24-hour validation cycle, the subnet distributes its full TAO emissions as follows:

- Current #1 (Champion) receives a base **20%** of the cycle's emissions  
- An additional **5%** of the cycle's emissions accumulates in a **Champion Carry-Over Pool**  
- The remaining **75%** is distributed across ranks #2–100 using a logarithmic decay curve (largest share to #2, tapering sharply to #100)

**Champion Carry-Over Pool mechanics**:
- The 5% carry-over accumulates day after day in the pool.  
- While the same track remains #1, the champion receives only the 20% base each cycle (pool continues to grow).  
- The moment a **new track** achieves the all-time highest consensus score (dethroning the previous #1), it immediately claims the **entire accumulated carry-over pool** on top of its 20% base for that cycle.  
- After payout, the carry-over pool resets to zero and begins accumulating 5% again from the next cycle.

**Example over multiple days** (assuming stable emissions for illustration):
- Day 1: Track A is #1 → gets 20%, pool gets 5% (pool = 5%)  
- Day 2: Track A still #1 → gets 20%, pool gets 5% (pool = 10%)  
- Day 3: Track A still #1 → gets 20%, pool gets 5% (pool = 15%)  
- Day 4: Track B becomes new #1 → Track B gets 20% + 15% carry-over (total 35% this cycle), pool resets to 0  
- Day 5: Track B still #1 → gets 20%, pool gets 5% (pool = 5%)

This structure creates reliable daily rewards for consistent top performers while building excitement and large upside for challengers who finally surpass the reigning champion.

Emissions are paid to the **miner node** that submitted the track. In practice, the MuseNet web/app (fiat-only frontend) acts as a custodial miner proxy:  
- Musicians upload via email/Google login  
- Backend submits the track on-chain  
- Any earned TAO is auto-converted to fiat and paid out to the musician within 48 hours via Stripe/PayPal  

Musicians never see a wallet, seed phrase, or TAO balance.

### Incentive Alignment for Miners and Validators

- **Miners (musicians or music collectives)**  
  The app makes submission as simple as uploading to SoundCloud. Higher validator scores = higher fiat payouts + visibility (featured playlists, licensing opportunities). This aligns creators with quality because real earnings and exposure scale with score.  
  Open-source submission SDK allows advanced users (labels, DAWs) to batch-upload while still routing through the same scoring engine.

- **Validators**  
  Earn emissions proportional to how closely their scores match the subnet-wide consensus (standard Yuma). They are incentivized to be honest because inaccurate scoring directly reduces their own rewards.  
  All scoring rubrics and audio samples are published on-chain (IPFS hashes) for full transparency.

### Mechanisms to Discourage Low-Quality or Adversarial Behavior

- **Originality gate**  
  Every submission is fingerprinted (AcoustID + perceptual hash) and checked against a growing on-chain database of previously submitted tracks. Plagiarism score >15% → automatic rejection + temporary miner ban.

- **Human-proof requirement (optional but score-boosting)**  
  Submitters can attach a short “creation proof” video or DAW session export hash. Tracks with verified human proof receive a +20% originality multiplier.

- **Submission throttling**  
  Max 3 tracks per 24h per verified user account (fiat KYC-lite via email/phone).

- **Slashing via reputation**  
  Repeated low-quality spam lowers a miner’s trust score; after 3 strikes the miner is pruned from the next 7 cycles.

- **Validator collusion protection**  
  Multiple independent validators per track (minimum 3) + stake-weighted consensus.

### Qualification as a Genuine “Proof of Intelligence” (or Proof of Effort)

MuseNet produces **verifiable creative intelligence** — the collective output of thousands of human musicians competing to create the best music for a given prompt or open theme. This is “proof of human creative intelligence” because:

- Outputs are real, usable music tracks (not synthetic).  
- Scoring is objective where possible (technical metrics + originality) and stake-weighted subjective where it must be (artistic quality).  
- The network continuously surfaces better music than any centralized platform because incentives drive global, permissionless participation.

It qualifies as at least **proof of effort** because every submission requires real creative work (time, skill, studio effort) that cannot be gamed at scale without detection.

### High-Level Algorithm (Task Assignment → Submission → Validation → Scoring → Reward)

1. **Task Assignment**  
   Validators post daily challenges (text prompt + optional reference stem) or open submissions pool.

2. **Submission**  
   Musician uploads via fiat app → backend generates IPFS hash + metadata → miner node submits to subnet.

3. **Validation**  
   3+ random validators download audio and run composite scorer.

4. **Scoring**  
   Each validator outputs a 0–1 score per track. Yuma Consensus aggregates into final weights.

5. **Reward Allocation**  
   Top-ranked tracks receive emissions (including any carry-over payout) → converted to fiat payouts to submitter.
