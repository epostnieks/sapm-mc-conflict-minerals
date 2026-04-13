# Monte Carlo Assumptions — Conflict Minerals / Fungibility Floor

All values in $B USD (annualized). Every parameter traces to paper §4–§5
or the citations in `data_sources.md`. Run `python mc_simulation.py` to
reproduce bit-identical results.

---

## Simulation Parameters

| Parameter | Value | Justification |
|-----------|-------|---------------|
| Seed | 42 | Fixed for reproducibility |
| N draws | 100,000 | 4-decimal CI stability |
| Cross-channel correlation ρ | 0.3 | Shared macro drivers (GDP, population, regulation) |
| Private payoff Π | $20.3B/yr | Annual industry revenue — see `data_sources.md` |
| β_W median (result) | 12.6 | Confirmed by N=100,000 draws |
| ΔW median (result) | $255.7B/yr | Sum of channel medians (correlated) |

**Π = revenue, not profit.** SAPM Iron Law: βW = ΔW/Π where Π is annual
revenue. Using profit would inflate βW by 5–20× for low-margin industries.

---

## Channel Parameters

| Channel | Dist | Low | Mid | High | Description |
|---------|------|-----|-----|------|-------------|
| `C1_armed_conflict` | lognormal | $50B | $80B | $130B | Armed conflict financing, displacement, death |
| `C2_health_mortality` | lognormal | $25B | $40B | $65B | Occupational mortality, toxic exposure, disease |
| `C3_environmental` | lognormal | $20B | $35B | $55B | Deforestation, water contamination, biodiversity loss |
| `C4_forced_labor` | lognormal | $18B | $30B | $50B | Child labor, forced labor in artisanal mining |
| `C5_governance` | lognormal | $15B | $28B | $45B | Governance failure, warlord economies, corruption |
| `C6_compliance` | normal | $25B | $38B | $52B | Downstream compliance deadweight, audit costs |


All ranges represent [P5, P95] of the channel-specific distribution as
calibrated from literature in paper §4.

---

## Impossibility Floor

The floor β_W ≥ 3.0 is the minimum ratio achievable while the industry operates.
This bounds the simulation from below: the theorem holds regardless of parameter values,
because even best-case scenarios exceed the floor.

In 100,000 draws: P(β_W < 3.0) = 0.0000%

## Sensitivity (VSL × Double-Counting Grid)

Central VSL (1.0×): no DC adj β_W = 12.36 | 20% DC adj = 9.89 | 40% DC adj = 7.42

See `mc_results.json` → `sensitivity_matrix` for full 5×5 grid.

## Distribution Robustness

The simulation uses a lognormal/normal mix calibrated to channel-specific
uncertainty structure. Results are robust: the central β_W changes by less
than ±0.3 under all-lognormal or all-normal configurations.

---

## Plausibility Checks (SAPM IL#28)

- **Annual flow**: All W_i are $/yr flows ✓
- **GDP bound**: ΔW = $256B = 0.2% of world GDP ($106T) ✓
- **β_W range**: 12.6 is within the [0.5, 100] plausible range ✓
- **P(β_W < 1)**: 0.0000% ✓
