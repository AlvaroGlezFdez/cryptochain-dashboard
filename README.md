# CryptoChain Insights Dashboard

Real-time **Streamlit** dashboard that connects to a public Bitcoin API and visualizes
live cryptographic metrics of the network, applying core cryptography concepts —
**SHA-256, Proof of Work and difficulty adjustment** — to real on-chain data, plus an
**anomaly-detection** component. Individual academic project for the *Cryptography*
course (B.Sc. in Mathematical Engineering, UAX).

## What it does

The dashboard is organised in four modules (tabs):

- **M1 · PoW Monitor** — difficulty, inter-block times and block flow over the last
  blocks. Computes the mining **target from the block `bits`** field and the number of
  required **leading zero bits**.
- **M2 · Block Header** — decodes the six fields of a block header and verifies the
  **double SHA-256** hash against the target.
- **M3 · Difficulty History** — difficulty across **2016-block adjustment periods**,
  with the real-time / 600 s ratio (whether blocks were found faster or slower than the
  10-minute target).
- **M4 · Anomaly Detector** — models block inter-arrival times as a **Poisson process**
  (exponential distribution, mean 600 s) and flags statistically anomalous blocks with a
  two-tailed test (α = 0.05).

## Data source

Real-time data from the **public Blockstream API** (`blockstream.info/api`). No API keys
or credentials required.

## Cryptography concepts applied

SHA-256 (double hashing for header verification) · Proof of Work, target and difficulty ·
difficulty re-adjustment every 2016 blocks · block discovery modelled as a Poisson process.

## Tech stack

Python · Streamlit · Plotly · pandas · NumPy · SciPy · requests

## How to run

​```bash
pip install -r requirements.txt
streamlit run app.py
​```

## Repository structure

​```
├── app.py                     # Streamlit entry point (4 tabs)
├── api/
│   └── blockchain_client.py   # Blockstream API client (blocks, headers, difficulty)
├── modules/
│   ├── m1_pow_monitor.py      # Proof of Work monitor
│   ├── m2_block_header.py     # block header decoder + SHA-256 verification
│   ├── m3_difficulty_history.py
│   └── m4_ai_component.py     # anomaly detector (exponential model)
├── .streamlit/config.toml
└── requirements.txt
​```

---
*Individual academic project · Cryptography · Universidad Alfonso X el Sabio (UAX) · 2025–2026.*
