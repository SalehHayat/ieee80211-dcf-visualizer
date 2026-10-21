# IEEE 802.11 DCF Backoff Algorithm Visualizer

> **Live Demo → [salehhayat.github.io/ieee80211-dcf-visualizer](https://salehhayat.github.io/ieee80211-dcf-visualizer/)**

A professional, interactive, browser-based simulation that visualizes and compares **Binary Exponential Backoff (BEB)** and **CHUBB (Channel Usage-Based Backoff)** algorithms as defined in the IEEE 802.11 Distributed Coordination Function (DCF) MAC protocol.

Built as part of MS Thesis research at **KUST Kohat**.

---

## Features

| Feature | Description |
|---|---|
| 🔬 **Real Simulation Engine** | Full JavaScript implementation of BEB & CHUBB — not a mockup |
| 📊 **Live Channel Timeline** | Slot-by-slot visualization of success / collision / idle states |
| 🎯 **Node Backoff Lanes** | Per-node backoff counter bar with live CW values |
| 📈 **Rolling Throughput Chart** | 50-slot windowed throughput trend for both algorithms |
| ⚖️ **Side-by-Side Comparison** | BEB vs CHUBB head-to-head table: throughput, fairness, collisions |
| 🧮 **Jain's Fairness Index** | Real-time fairness computation across all nodes |
| ⚙️ **Configurable Parameters** | Nodes (2–40), packet rate, CW_min, CW_max, total slots |
| 💾 **Export to CSV** | Download full slot-by-slot simulation results |
| 🌙 **Dark UI** | Professional dark theme, responsive on mobile |

---

## Algorithms Implemented

### BEB — Binary Exponential Backoff
The standard IEEE 802.11 DCF algorithm:
- On **collision**: `CW = min(CW × 2, CW_max)`
- On **success**: `CW = CW_min` (reset)
- Backoff counter drawn uniformly from `[0, CW-1]`

### CHUBB — Channel Usage-Based Backoff
Proposed in the base paper (HCIS Journal, Vol. 14, 2024):
- Each node computes `N_TRatio = N_t / T` (transmission slots / total slots)
- Uses N_TRatio to select multiplicative factor **G** from a 5-row lookup table
- On collision: `CW = min(CW × G, CW_max)` where G ∈ {1.8 … 2.8}
- Adapts aggressively under high load, conservatively under low load
- Achieves **3–31% throughput improvement** in dense WANETs

---

## How to Use

1. **Select algorithm**: BEB / CHUBB / Both (for comparison)
2. **Adjust parameters** in the left sidebar
3. Click **▶ Run** to start the simulation
4. Use **⏭** to step one slot at a time
5. Use **↺** to reset
6. Click **⬇ Export CSV** to download results

---

## Simulation Model

Based on the classic **Bianchi (2000) Markov chain model** for IEEE 802.11 saturation throughput:

- Time is slotted (20 μs per slot, IEEE 802.11b/g)
- Each node generates a packet with probability `λ` per slot
- Channel access follows DCF CSMA/CA rules
- Collision = 2+ nodes transmit in the same slot
- Post-collision backoff drawn from updated CW

---

## Referenced Papers

| Paper | Year | Key Contribution |
|---|---|---|
| **CHUBB** — Zulfiqar et al. | 2024 | Channel usage ratio adaptive backoff (N_TRatio → G factor) |
| **Wang et al.** | 2026 | NAK-based micro-scheduling with CW hint broadcast |
| **Tu & Chen** | 2026 | CIPD — slot offset Δ(L) based on EWMA collision ratio |
| **Zuo et al.** | 2025 | ACWB-DQN — Deep Q-Network for adaptive CW selection |
| **Yamada et al.** | 2026 | Hybrid CW + p-CSMA optimization (DOR metric) |
| **Bianchi** | 2000 | 2D Markov chain throughput analysis (foundational) |

---

## Tech Stack

- **Pure HTML5 / CSS3 / Vanilla JS** — zero dependencies, no build step
- Canvas API for timeline and throughput chart rendering
- GitHub Pages for live deployment

---

## Author

**Saleh Hayat**
MS Computer Science — KUST Kohat
GitHub: [@SalehHayat](https://github.com/SalehHayat)

---

## License

MIT — free to use for academic and research purposes.
