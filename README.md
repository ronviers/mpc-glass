# MPC Glass

**Metastable Propositional Calculus, applied to glass-aging dynamics.**

Sibling project of `mpc-quantum`, `mpc-foundry`, `mpc-brain`, `mpc-sat`, `mpc-profiles`.

Bootstrap stage: design and roadmap only. No code yet.

---

## What this is

Glass-aging dynamics — the slow, history-dependent relaxation of structural and spin glasses below their glass transition — is the most carefully measured FDT-violating phenomenon in physics. The fluctuation-dissipation ratio $X(t, t_w)$ in glasses has been characterised across substrates (spin glasses, structural glasses, colloidal glasses) for thirty years (Cugliandolo–Kurchan 1993 onward). The parametric shape $\chi$ vs $C$ in glass aging is the *same observable* MPC predicts for its s-regime.

This project tests whether MPC's s-regime FDR shape — already validated on Langevin substrate in `mpc-brain` Session A and partially validated on surface-code syndrome streams in `mpc-quantum` Session 4 — transfers to glass aging on a third substrate.

The thesis:

> If MPC's s-regime FDR shape matches glass-aging FDT violations quantitatively (or with substrate-specific calibration), the same MPC observable holds across three independent substrates with different physical content. That is cross-substrate unification at the level the framework's claim about its own primitives requires.

If it does not match, that is also informative: it identifies what is specific to MPC versus what is already covered by glass physics.

## Calibrated position upfront

MPC sits in a populated landscape of thermodynamic-frame approaches to inference and dynamics. Cugliandolo–Kurchan, Bouchaud, Berthier, and the broader glass-physics community have spent decades characterising FDT violations in glasses. **MPC is not the first thermodynamic mapping of glass aging.** The framework's specific contribution at this substrate is the *cross-substrate unification* claim — that the same FDR shape appears on factories, cognitive systems, QC syndromes, and now glasses.

The project's success criterion is measured against this calibrated standard, not against an overclaimed novelty. See [docs/journey/MAPPINGS.md](docs/journey/MAPPINGS.md) for the contour discipline and the credit-allocation methodology inherited from `mpc-quantum`.

## Why this substrate

`mpc-foundry` exercised the framework on industrial control. `mpc-brain` validated the four-scenario classifier on Langevin substrate. `mpc-quantum` tested the s-regime FDR transfer on surface-code syndromes (passed at sub-threshold operation) and identified the conditions for testing the k-regime claim (pending correlated-error circuits).

Glass aging is the next-natural test because:

- The s-regime FDR shape has been measured directly and repeatedly in glasses for thirty years.
- Glass simulators (Edwards–Anderson, Lennard-Jones, kinetically-constrained models) are well-established and computationally tractable.
- The substrate has *explicit memory kernels*, so v4's Table 1 sign predictions probably apply directly. The Markovian sign caveat earned in `mpc-quantum` (F-003) likely does not bite here.
- The substrate's natural readout is continuous and local in time, so detection-event preprocessing (F-007 of `mpc-quantum`) is not needed.

In short: this is the substrate where the framework's machinery should apply most directly, with the fewest substrate-conditional adjustments. If MPC works anywhere, it should work here.

## The Maxwell-pattern claim

The s-regime FDR shape on glasses has been characterised empirically and theoretically for decades. The MPC contribution at this substrate is not the discovery of the shape; it is the *cross-substrate unification* — the same shape appearing on substrates with no shared physical content. We inherit the empirical groundedness of the glass-physics components; what requires further validation is the unification claim itself.

This is the structural pattern Maxwell instantiated for electromagnetism: Coulomb, Ampere, Faraday were each independently validated; Maxwell unified them under a single equation set; what *unification* required separately was a new prediction (electromagnetic waves, confirmed by Hertz). The MPC analogue: the cross-substrate transfer of the s-regime FDR shape is the prediction the unification implies. mpc-quantum tested it on QC syndromes (passed). mpc-glass tests it on glass aging.

## Roadmap

Five phases. See [docs/ROADMAP.md](docs/ROADMAP.md).

| Phase | Scope |
|---|---|
| 0 | Bootstrap. Read Cugliandolo–Kurchan and one canonical review. Pick simulator. |
| 1 | Edwards–Anderson 2D Ising spin-glass simulator. Verify aging signature directly. |
| 2 | `glass_socket` adapter. Vendor kernel + physics primitives. Confirm autocorrelation infrastructure. |
| 3 | FDR measurement. Paired-trajectory protocol with applied-field perturbation. Compare to canonical glass-aging shape. |
| 4 | Contour assessment against glass-physics literature. Update v6 paper bibliography (or v7 paper) with glass-substrate evidence. |

## What carries from siblings

The MPC kernel from `mpc-foundry` / `mpc-quantum` carries:
- `physics/` (SHA-pinned to `mpc-brain`): `autocorr_fft`, `tau_integral`, `correlation_time`, `survival_margin`, `cross_dissipation`, `measure_fdr`.
- Kernel modules: `TraceBus`, `FluxLedger`, `RegimeClassifier`, `InstructionSet`, `AdvisoryArbiter`, `MetaLedger`, `HypothesisGraph`, `TrailWindow`, `TwinSocket`.
- Methodology: contour discipline, substrate-conditional reading rules (v6 Appendix F), Maxwell-pattern credit allocation.

What is new for this project:
- `glass_socket` pack: read spin-glass trajectories, emit TwinTicks.
- Spin-glass simulator (~200 lines of numpy).
- FDR comparison harness against canonical Cugliandolo–Kurchan shape.
- Manual chapters on the glass substrate.

## Sibling-project relationships

```
                ┌──────────────────────────┐
                │   physics primitives     │
                │   (vendored from         │
                │    mpc-brain)            │
                └──────────────────────────┘
                          ▲
       ┌──────────┬───────┼───────┬──────────┬──────────┐
       │          │       │       │          │          │
   mpc-sat   mpc-brain mpc-foundry mpc-quantum mpc-profiles mpc-glass
   (proves   (cog.    (twin     (FT QC      (κ-profile  (THIS:
   capacity   arch.)   overlay)  control     library)    glass aging
   bound)                        loop)                   substrate)
```

No runtime dependency between siblings. Physics primitives are vendored with SHA pin. Kernel modules are forked from `mpc-foundry`; sync via manual cherry-picking until `mpc-physics` carve-out lands.

## Risk register

- **Glass physics is a huge field.** Mode-coupling theory, replica symmetry breaking, dynamical heterogeneity, kinetically-constrained models. The contour discipline says: stay narrow on the FDR aging shape question. Do not try to map MPC onto all of glass physics.
- **Aging timescales.** Real glasses age over decades of time. Simulations need enough Monte Carlo sweeps to see aging on visible scales. Edwards–Anderson at $T \approx 0.7\,T_c$ shows aging in $10^4$–$10^6$ sweeps; tractable on commodity hardware.
- **Simulator vs experiment.** We compare MPC's predicted shape to the *generic* aging shape predicted by glass physics, which has been validated experimentally many times. We do not need to match a specific experimental dataset numerically.
- **The dial-in trap.** When the FDR shape on glass simulations does not match MPC's s-regime prediction exactly, do NOT tune simulator parameters until it does. Document the divergence honestly. The framework either holds or it does not.

## Status

Bootstrap. README, HANDOFF, ROADMAP, journey scaffolding (FOOTING, MAPPINGS), and a discoveries log seeded with the s-regime cross-substrate transfer thesis. No code yet.

The next session opens cold. [HANDOFF.md](HANDOFF.md) is the entry point.

---

Developed alongside the operator who built `mpc-brain`'s four-scenario validation rig, `mpc-foundry`'s thermal_envelope dual-description precedent, and `mpc-quantum`'s journey work and v6 paper rewrite. mpc-glass is the deliberate next test of the framework's cross-substrate unification claim, on the substrate where the s-regime FDR shape was originally inspired by (via Cugliandolo–Kurchan) and has been most carefully measured.
