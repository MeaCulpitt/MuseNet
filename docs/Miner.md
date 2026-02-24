## Miner Design

### Miner Tasks
In MuseNet, miners are responsible for submitting high-quality, original music tracks (or short stems/clips) in response to subnet challenges or open submission pools.  
The primary task is creative production: musicians use their skills, DAWs (Ableton, Logic Pro, FL Studio, etc.), instruments, or production setup to create audio content that meets or exceeds the challenge criteria.

Miners do **not** run heavy AI inference or compute-intensive tasks — this keeps barriers low so real human creators (indie producers, bedroom musicians, collectives) can participate easily without needing GPUs or technical setup beyond a standard music production workflow.

### Expected Input → Output Format

- **Input (from validators or challenge system)**:
  - Optional: Text prompt/challenge description (e.g., "Create a 60-second upbeat electronic track with dreamy synth pads and female vocal chops", or "Remix this provided stem pack in a lo-fi hip-hop style").
  - Optional: Reference audio file (IPFS hash of a stem, loop, or mood reference track).
  - Open submissions: No specific input — miners submit freely to the daily pool.

- **Output (submitted by miner)**:
  - Primary: Audio file (WAV or high-quality MP3, max 5–10 MB to keep on-chain costs low).
    - Recommended: 30–120 seconds length for quick validation.
    - Multi-stem option (bonus): ZIP archive containing 4–8 isolated stems (vocals, drums, bass, melody, etc.) in WAV format.
  - Metadata JSON:
    ```json
    {
      "prompt": "upbeat electronic track with ethereal vocals",
      "title": "Dreamscape Drift",
      "genre": "Electronic / Chillwave",
      "duration_seconds": 90,
      "bpm": 128,
      "creation_proof_hash": "ipfs://Qm... (optional DAW session export or video proof)",
      "originality_declaration": true
    }
    ```
  - All files pinned to IPFS/Arweave; only hashes + metadata submitted on-chain via the miner node.

The fiat-only MuseNet web/app handles this transparently: musicians drag-and-drop audio + fill simple form fields → backend generates IPFS hash, bundles metadata, and submits as the custodial miner node.

### Performance Dimensions
Validators score submissions across these weighted dimensions (total 0–1 normalized score):

- **Creative Quality & Prompt Adherence** (40%): How well the track matches the challenge intent, musical coherence, innovation, emotional impact (measured via CLAP/audio embeddings similarity + stake-weighted human/AI listener feedback).
- **Technical Polish** (25%): Audio fidelity (loudness normalization, no clipping/distortion via Essentia or similar libs), mix balance, mastering level.
- **Originality & Uniqueness** (20%): Low plagiarism (perceptual hash + AcoustID match <15%), avoidance of generic tropes (diversity embedding distance from top historical submissions).
- **Human Effort Proof (Bonus Multiplier)** (up to +20%): Verified creation proof (e.g., timestamped DAW project hash, short screen-recording video) increases trust score and final weight.
- **Efficiency/Format Compliance** (15%): Correct file specs (sample rate ≥44.1kHz, proper tagging), fast submission (within cycle window), multi-stem bonus for remixability.

These dimensions are designed to be **objective where possible** (technical metrics, hashes) and **stake-weighted subjective** where artistic judgment is needed (Yuma Consensus handles this robustly). High performance across all dimensions maximizes fiat payouts (converted from TAO emissions) and visibility in the app's featured feeds/playlists.

Advanced miners (e.g., labels or DAW-integrated users) can use an open-source SDK to automate batch submissions or integrate directly with production tools, but the core experience remains simple and fiat-native for everyday musicians.
