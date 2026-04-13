# SAPM Monte Carlo — Conflict Minerals / Fungibility Floor

**Public replication repository for quantitative results in:**

> Postnieks, E. (2026). *Conflict Minerals (Fungibility Floor).* SAPM Working Paper. SSRN.

This repository provides everything needed to independently reproduce, audit,
and extend the Monte Carlo simulation underlying the paper's core results.
The paper is available on SSRN.

---

## Results (N = 100,000 draws, seed = 42)

| Statistic | Value |
|-----------|-------|
| **β_W median** | **12.6** |
| β_W mean | 12.82 |
| β_W std | 2.44 |
| **90% CI** | **[9.2, 17.2]** |
| 99% CI | [8.1, 19.5] |
| P(β_W < 1) | 0.0000% |
| **ΔW median** | **$255.7B/yr** |
| Π (revenue) | $20.3B/yr |

**β_W = 12.6** means the conflict minerals industry destroys **$12.6 in system
welfare for every $1.00 in revenue** — across 6 channels and 100,000 Monte Carlo draws.

**Classification**: Class 1 — Impossibility

---

## What Is β_W?

```
β_W = ΔW / Π
```

- **ΔW** = total annualized welfare destruction ($B/yr) across all channels
- **Π** = annual industry **revenue** ($B/yr) — not profit

β_W > 1: industry destroys more welfare than it captures in revenue.
β_W > 3: Strong Intractability threshold — reform requires structural replacement.

---

## Quick Start

```bash
git clone https://github.com/epostnieks/sapm-mc-conflict-minerals.git
cd sapm-mc-conflict-minerals
pip install numpy scipy
python mc_simulation.py
```

Expected output: `β_W median : 12.6` and `ΔW median : $255.7B/yr`

---

## Welfare Channels

| Channel | Median ($B/yr) | 90% CI | Distribution |
|---------|---------------|--------|--------------|
| C1_armed_conflict | $79.9B | [$49.1B, $129.8B] | Lognormal |
| C2_health_mortality | $40.0B | [$24.6B, $65.2B] | Lognormal |
| C3_environmental | $35.0B | [$22.3B, $55.0B] | Lognormal |
| C4_forced_labor | $30.0B | [$18.0B, $49.9B] | Lognormal |
| C5_governance | $27.9B | [$17.4B, $44.8B] | Lognormal |
| C6_compliance | $38.0B | [$24.5B, $51.5B] | Normal |
| **Total ΔW** | **$255.7B** | **[$187.5B, $348.6B]** | Correlated (ρ=0.3) |

---

## Impossibility Floor

The floor β_W ≥ 3.0 cannot be breached by any policy while the
industry continues to operate. In 100,000 draws, only **0.0000%**
fall below this floor — confirming the structural constraint.

## Repository Contents

| File | Description |
|------|-------------|
| `mc_simulation.py` | Self-contained simulation — no private pipeline imports |
| `mc_results.json` | Pre-run results (100K draws, seed=42) — matches paper |
| `mc_histogram.json` | Binned β_W distribution (80 bins) for companion chart |
| `assumptions.md` | Every parameter: value, derivation, source |
| `data_sources.md` | Full citation list for all empirical inputs |

---

## Replication Notes

Results are seeded and deterministic. Tested with:
```
numpy==1.26.4  scipy==1.12.0  Python 3.11.9
```

The `median` and `ci_90` (to 1 decimal) match exactly across compatible versions.

---

## License

CC BY 4.0. Cite as:

> Postnieks, E. (2026). *SAPM Monte Carlo — Conflict Minerals (Fungibility Floor)*.
> GitHub: epostnieks/sapm-mc-conflict-minerals.
> https://github.com/epostnieks/sapm-mc-conflict-minerals
