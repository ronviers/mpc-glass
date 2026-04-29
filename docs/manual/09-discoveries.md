# 9. Discoveries log

Running log. Reverse chronological. Same shape as `mpc-foundry/docs/manual/09-discoveries.md` and `mpc-quantum/docs/manual/09-discoveries.md`. Promote findings up into structured chapters once a pattern is clear.

The structured working ledger for the glass-substrate mapping work lives in [../journey/MAPPINGS.md](../journey/MAPPINGS.md) (rows, status, conflicts, deferences) and [../journey/FOOTING.md](../journey/FOOTING.md) (what's locked vs. pending). This log is for free-form findings; the journey directory is for structured process.

---

## 2026-04-29 — Project bootstrapped on the s-regime cross-substrate transfer thesis

`mpc-glass` is the third substrate test of MPC's s-regime FDR shape, after `mpc-brain` Session A (Langevin substrate, four scenarios validated) and `mpc-quantum` Session 4 (surface-code syndrome streams, transfer confirmed at sub-threshold operation). The substrate is glass aging.

The thesis: glass-aging dynamics is the most carefully measured FDT-violating phenomenon in physics, with thirty years of empirical work since Cugliandolo–Kurchan 1993. The parametric $\chi$ vs $C$ shape in glass aging is the *same observable* MPC predicts for its s-regime. If the shapes match, MPC's s-regime FDR transfer claim has three independent empirical footholds across substrates with no shared physical content beyond the framework's primitives.

The calibrated position upfront: MPC is not the first thermodynamic mapping of glass aging. Cugliandolo–Kurchan, Bouchaud, Berthier own the field's vocabulary and observables. The MPC contribution at this substrate is *cross-substrate unification*, not the discovery of aging shape. Credit the field; stake the unification claim at the right level.

The Maxwell-pattern framing: Coulomb / Ampere / Faraday were each independently validated; Maxwell unified them under a single equation set; what unification required separately was a new prediction (electromagnetic waves, confirmed by Hertz). The MPC analogue: the cross-substrate transfer of the s-regime FDR shape *is* the prediction the unification implies. `mpc-quantum` tested it on QC syndromes (passed). `mpc-glass` tests it on glass aging.

Bootstrap discipline: Phase 0 is reading. Don't write a glass simulator before you can describe what FDT violation in aging glasses looks like in plain English.

Why this substrate is structurally favourable for MPC's machinery:

- Glasses have *explicit memory kernels* — the system remembers its history through structural relaxation. v4's Table 1 sign predictions for $\gamma_A$ and $\gamma_{ij}$ probably apply directly. The Markovian sign caveat earned in `mpc-quantum` (F-003) likely does not bite here.
- Glass observables (spin states, particle positions) are continuous and local in time. Detection-event preprocessing (F-007 of `mpc-quantum`) is not needed. The substrate's natural readout matches the trail-vector formalism's locality assumption.
- Bath construction is natural — high-temperature equilibrium is the substrate's own reservoir. The shuffled-events bath construction (F-011 of `mpc-quantum`) is not needed.

In short: this is the substrate where the framework should apply most directly. The substrate-conditional reading rules earned for QC are likely all unnecessary here. If MPC's s-regime FDR shape doesn't transfer cleanly to glass aging, that's a more serious calibration finding than the Session 4 result was.

---

## How to add an entry

1. Date the entry (ISO format).
2. 2–4 paragraphs. Concrete and specific. File paths, equations, paper citations, anything verifiable.
3. If a structured chapter should be updated, update it in the same commit and cross-reference here.
4. If the finding is a project-level discipline rule (kernel-wide), add it to FOOTING and cite it here.

The point is *capture*, not completeness. Get findings written down before they dissipate; structure later.
