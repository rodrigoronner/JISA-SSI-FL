# JISA-SSI-FL: Self-Sovereign Identity for Federated Learning

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![Python](https://img.shields.io/badge/python-3.8+-blue.svg)](https://www.python.org/downloads/)
[![Hardhat](https://img.shields.io/badge/built%20with-Hardhat-FFDB1C.svg)](https://hardhat.org/)
[![JISA](https://img.shields.io/badge/submitted-JISA-orange)](https://journals-sol.sbc.org.br/index.php/jisa)

> Official implementation accompanying: **"A Decentralized Identity Protocol for Trustworthy Federated Learning: Comparative Analysis of Trust Models for Internet-Based Health Services"** — submitted to the *Journal of Internet Services and Applications (JISA)*.

## Overview

This repository implements a decentralized identity verification protocol for Federated Learning (FL) in Internet-distributed environments. By integrating W3C Self-Sovereign Identity (SSI) standards (DIDs, VCs) with blockchain smart contracts, the protocol provides deterministic Sybil attack resistance through proactive institutional identity verification rather than reactive reputation scoring.

### Key Features

- **100% external Sybil attack neutralization**: Only DIDs with valid Verifiable Credentials can participate
- **Domain-agnostic protocol**: Transferable beyond healthcare to any Internet service requiring authenticated collaborative ML
- **Clinical-grade performance**: AUC-ROC = 0.954, Recall = 0.890 on MIMIC-IV mortality prediction
- **< 1% protocol overhead**: Blockchain verification + IPFS storage incurs negligible latency relative to local training
- **Analytical cost model**: Enables pre-deployment economic planning (~$15.67 for N=10 over 100 rounds)
- **LGPD compliance mapping**: First structured analysis of Brazilian data protection law across FL trust models

## Paper

The LaTeX source for the JISA submission is located in `paper/jisa/`:

```
paper/jisa/
├── main_jisa.tex          # Main manuscript (JISA template)
├── cover_letter.tex       # Cover letter to editors
├── comments_to_editor.txt # Submission checklist comments
├── sbc2023.cls            # SBC document class
├── apalike-sol.bst        # Bibliography style
└── figures/               # Figure files (see below)
```

**Required figures** (place in `paper/jisa/figures/`):
- `Fig1_SSI-FL Protocol Diagram.jpg`
- `Fig2_convergence_100rounds_final.png`
- `fig3_attack_tree.jpg`

Compile with **XeLaTeX**.

## Repository Structure

```
JISA-SSI-FL/
├── paper/                       # JISA submission files
│   └── jisa/                    # LaTeX source, figures, cover letter
├── contracts/                   # Ethereum Smart Contracts
│   └── FLRegistry.sol          # DID/VC verification + access control
├── scripts/                     # Deployment and utilities
│   └── deploy.js               # Contract deployment script
├── src/                         # Federated Learning Core
│   ├── main_tbfl_simulation.py # Main execution script (100 rounds)
│   ├── blockchain_manager.py   # Web3 interface
│   └── cliente_fl.py           # FL client (hospital) with FedProx
├── data/                        # Preprocessed MIMIC-IV cohort
│   └── mortalidade_features.csv.zip
├── hardhat.config.js            # Hardhat configuration
├── package.json                 # Node.js dependencies
├── requirements.txt             # Python dependencies
└── README.md
```

## Quick Start

### Prerequisites
- Python 3.8+ | Node.js 14+ | MIMIC-IV access via [PhysioNet](https://physionet.org/content/mimiciv/)

### Installation

```bash
git clone https://github.com/rodrigoronner/JISA-SSI-FL.git
cd JISA-SSI-FL

# Blockchain dependencies
npm install

# Python environment
python -m venv venv && source venv/bin/activate
pip install -r requirements.txt
```

### Run Simulation

```bash
# Terminal A: local blockchain
npx hardhat node

# Terminal B: deploy contract + run FL simulation
npx hardhat run scripts/deploy.js --network localhost
# Copy contract address → update src/main_tbfl_simulation.py:CONTRACT_ADDRESS
python src/main_tbfl_simulation.py
```

## Citation

```bibtex
@article{tertulino2025jisa,
  title   = {A Decentralized Identity Protocol for Trustworthy Federated Learning:
             Comparative Analysis of Trust Models for Internet-Based Health Services},
  author  = {Rodrigo Tertulino and Ricardo Almeida and Laercio Alencar},
  journal = {Journal of Internet Services and Applications},
  year    = {2025},
}
```

## Acknowledgments

- MIT Laboratory for Computational Physiology (MIMIC-IV)
- PhysioNet for credentialed clinical data access
- Federal Institute of Rio Grande do Norte (IFRN) for computational resources

## License

MIT License. See [LICENSE](LICENSE) for details.
