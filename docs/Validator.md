## Validator Design

### Validator Tasks
Validators in MuseNet are responsible for objectively and fairly evaluating submitted music tracks to produce reliable, consensus-driven scores that drive emissions and quality curation.  
Unlike compute-heavy subnets, validation here is lightweight: validators download audio files (via IPFS hashes), run automated analysis tools, and apply stake-weighted human/AI judgment where artistic elements require it. This keeps validator hardware requirements low (standard laptop/server with ~8–16GB RAM sufficient) to encourage broad participation and decentralization.

Validators run continuously in a permissionless manner: they pull new submissions from the subnet queue, perform evaluations, and publish scores on-chain. The fiat-only MuseNet app never directly involves validators — it only consumes the final consensus scores for ranking, payouts, and featured content.

### Scoring and Evaluation Methodology
Validators compute a composite score (0–1 normalized) for each track using a multi-layered rubric. The final score is aggregated via Yuma Consensus across 3+ independent validators per submission (randomly assigned to prevent collusion).

Breakdown of scoring components (weighted):

- **Prompt / Theme Adherence** (40%):  
  Cosine similarity between track audio embeddings (via CLAP or similar open-source model) and the challenge prompt description. Higher similarity = better match to requested style, mood, genre, or elements.

- **Technical Quality** (25%):  
  Automated metrics using libraries like Essentia, Librosa, or PyDub:  
  - Loudness normalization (LUFS target -14 to -9)  
  - No clipping/distortion (peak detection)  
  - Spectral balance and clarity (high-frequency content, dynamic range)  
  - Sample rate & format compliance (≥44.1kHz, stereo)

- **Originality & Plagiarism Check** (20%):  
  Perceptual audio fingerprinting (AcoustID + custom hash) compared against on-chain historical database. Score penalty if >15% match to prior submissions. Bonus for verified human-proof attachments (e.g., +10–20% if DAW export hash matches).

- **Artistic / Perceptual Quality** (15%):  
  Stake-weighted subjective layer: Validators (or delegated listener panels) provide a perceptual score based on coherence, creativity, emotional impact, and production value. AI surrogates (e.g., music-specific CLAP or fine-tuned models) provide baseline; human stakers override/amplify for nuance. This ensures artistic subjectivity is handled decentralized and incentive-aligned.

All raw metrics, embeddings, and proof hashes are published on IPFS and linked on-chain for auditability and reproducibility.

### Evaluation Cadence
- **Continuous & Asynchronous**: New submissions trigger immediate validation rounds (validators poll the subnet queue every 1–5 minutes).  
- **Cycle Alignment**: Full consensus aggregation happens every 24 hours to align with emission distribution.  
- **Latency Target**: 95% of tracks scored within 2 hours of submission (fast enough for musician feedback loops).  
- **Minimum Validators per Track**: 3 (random selection via on-chain randomness); more if high-stakes challenge.

### Validator Incentive Alignment
Validators earn TAO emissions proportional to how closely their individual scores align with the final Yuma Consensus score (standard Bittensor mechanism: reward honest, accurate evaluators).  
- High-consensus validators build reputation and attract delegation (boosting their effective stake and earnings).  
- Dishonest or outlier scoring (e.g., consistent over/under-rating) leads to lower rewards and eventual de-weighting.  
- Transparency: All validator scores, justifications (if provided), and audio samples are publicly verifiable via IPFS hashes — enabling community auditing and slashing proposals if needed.

This design ensures validators are incentivized to produce fair, high-signal evaluations that surface the best human-created music, while keeping the process decentralized, auditable, and resistant to gaming.
