## Incentive & Mechanism Design

### Emission and Reward Logic
MuseNet operates on a **ranked, multi-tier emission model** (not pure winner-takes-all) to encourage continuous high-quality human music submissions while rewarding diversity.

Every 24-hour validation cycle, the subnet distributes its full TAO emissions across the top 100 ranked tracks according to a decaying curve:

- #1 track receives ~25% of emissions  
- #2–10 receive 50% total (logarithmic decay)  
- #11–100 receive the remaining 25%  

New all-time high scores (across any challenge) trigger an immediate bonus re-allocation of 10% of the next cycle’s emissions to that miner, creating constant competitive pressure.

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
   Top-ranked tracks receive emissions → converted to fiat payouts to submitter.
