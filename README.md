<div align="center">

<img src="docs/banner.png" alt="HFT Research Platform" width="100%" />

# ⚡ HFT Research Platform

### Evolutionary strategy generation & market-microstructure simulation.

*A research engine that evolves trading strategies and stress-tests them against a simulated order book — Rust core, Python research layer.*

[![Status](https://img.shields.io/badge/status-Research-7C5CFF?style=for-the-badge)](#-development-status)
![Rust](https://img.shields.io/badge/Rust-000000?style=for-the-badge&logo=rust&logoColor=white)
![Python](https://img.shields.io/badge/Python-3776AB?style=for-the-badge&logo=python&logoColor=white)
![Bybit](https://img.shields.io/badge/Bybit-F7A600?style=for-the-badge&logo=bybit&logoColor=white)

</div>

> **Public portfolio repository.** This documents architecture and research design only. No strategy logic, parameters, or proprietary source is published. This is a **research framework**, not financial advice and not a signal service. Walkthrough under NDA — **arasghorbani9090@gmail.com**.

---

## 📖 Overview

High-frequency trading lives and dies on **market microstructure** — the moment-to-moment mechanics of the order book, latency, and fills. Hand-tuning strategies against that complexity doesn't scale.

The **HFT Research Platform** treats strategy design as a search problem. An **evolutionary engine** generates and mutates candidate strategies; a **microstructure simulator** evaluates each one against realistic order-book dynamics; the survivors are analyzed, ranked, and iterated. A **Rust core** handles the hot path (simulation, evaluation) while **Python** drives research, orchestration, and analysis. Connectivity to **Bybit** provides real market data and a path from simulation toward live evaluation.

**Goals**
- 🧬 **Discover** strategy structures rather than hand-coding them.
- 🔬 **Evaluate** them under realistic microstructure, not naive backtests.
- 📊 **Understand** *why* a strategy works via reproducible research tooling.

---

## ✨ Features

- 🧬 **Evolutionary strategy generation** — population-based search that mutates and selects candidate strategies over generations.
- 📉 **Market-microstructure simulation** — order-book-aware evaluation modeling fills, queue position, and latency effects.
- 🦀 **Rust execution core** — performance-critical simulation and evaluation in safe, fast Rust.
- 🐍 **Python research layer** — experiment orchestration, analysis, and visualization.
- 🔌 **Bybit integration** — market data ingestion and a bridge from sim toward live evaluation.
- 🧪 **Reproducible experiments** — seeded, configurable runs for honest comparison.

---

## 🏗 Architecture

```mermaid
flowchart TD
    subgraph Research["🐍 Python Research Layer"]
        ORCH["Experiment orchestrator"]
        EVO["Evolutionary engine — select / mutate / breed"]
        ANALYSIS["Analysis & visualization"]
    end

    subgraph Core["🦀 Rust Core"]
        SIM["Microstructure simulator"]
        OB["Order-book model"]
        EVAL["Strategy evaluator"]
    end

    subgraph Market["🔌 Market Connectivity"]
        BYBIT["Bybit — data / execution bridge"]
        FEED[("Market data store")]
    end

    ORCH --> EVO
    EVO -->|candidate population| EVAL
    EVAL --> SIM
    SIM --> OB
    EVAL -->|fitness scores| EVO
    EVAL --> ANALYSIS
    BYBIT --> FEED
    FEED --> SIM
```

### Evolutionary research loop

```mermaid
sequenceDiagram
    participant R as Researcher
    participant ORCH as Orchestrator (Py)
    participant EVO as Evolution (Py)
    participant CORE as Rust Core
    R->>ORCH: configure experiment (seed, generations)
    ORCH->>EVO: init population
    loop each generation
        EVO->>CORE: evaluate candidates
        CORE->>CORE: simulate vs order book
        CORE-->>EVO: fitness scores
        EVO->>EVO: select · mutate · breed
    end
    EVO-->>ORCH: ranked survivors
    ORCH-->>R: analysis + metrics
```

---

## 🧱 Tech Stack

| Layer | Technology |
| --- | --- |
| **Performance core** | Rust (simulation, order book, evaluation) |
| **Research / orchestration** | Python 3.11+ |
| **Search** | Evolutionary / genetic algorithms |
| **Market data & connectivity** | Bybit API |
| **Domain** | Market microstructure, algorithmic trading research |
| **Interop** | Rust ⇄ Python bindings (FFI) |

---

## 📂 Folder Structure

> Representative — illustrative of organization, not a source dump.

```
hft-research-platform/
├── core/                   # Rust crate
│   ├── src/
│   │   ├── orderbook/      # order-book model
│   │   ├── sim/            # microstructure simulation
│   │   └── eval/           # strategy evaluation
│   └── Cargo.toml
├── research/               # Python research layer
│   ├── evolution/          # selection, mutation, breeding
│   ├── experiments/        # configs & runners
│   ├── data/               # Bybit ingestion
│   └── analysis/           # metrics & visualization
├── notebooks/              # exploratory research
└── bindings/               # Rust ⇄ Python interop
```

---

## 🖼 Screenshots

> Placeholders — add captures to `docs/screenshots/`.

| Evolution progress | Order-book sim | Strategy metrics |
| --- | --- | --- |
| ![Evolution](docs/screenshots/evolution.png) | ![Sim](docs/screenshots/orderbook.png) | ![Metrics](docs/screenshots/metrics.png) |

---

## 🗺 Roadmap

- [x] Rust microstructure simulator + order-book model
- [x] Evolutionary strategy generation loop
- [x] Bybit market-data ingestion
- [ ] Richer fill / latency modeling
- [ ] Walk-forward & out-of-sample validation harness
- [ ] Distributed evaluation across populations
- [ ] Live paper-trading bridge (read-only first)
- [ ] Research reporting dashboard

---

## 📈 Development Status

🟣 **Research** — the Rust core and evolutionary loop run end-to-end against simulated microstructure; current work focuses on validation rigor and fill realism. Research framework only — not investment advice.

---

## 🤝 Contact

📧 **arasghorbani9090@gmail.com** · 🔗 [LinkedIn](https://www.linkedin.com/in/aras-ghorbani-ab1a7b62)

<div align="center"><sub>Public architecture & docs. Strategy logic and source are proprietary.</sub></div>
