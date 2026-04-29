# Hand-off — mpc-glass bootstrap

This file is the entry point for the next session that picks up `mpc-glass` cold. Read it end-to-end before deciding what to do.

## Project goal

Test whether MPC's s-regime FDR shape transfers from Langevin substrate (`mpc-brain` Session A, four scenarios validated) and surface-code syndrome streams (`mpc-quantum` Session 4, transfer confirmed at sub-threshold operation) to glass-aging dynamics on a third substrate. Glass aging is the most carefully measured FDT-violating phenomenon in physics, with thirty years of empirical work since Cugliandolo–Kurchan 1993. If the same MPC observable holds here, the cross-substrate unification claim has three independent empirical footholds on substrates with no shared physical content beyond the framework's primitives.

## State at bootstrap

- **No code yet.** Bootstrap is documents only.
- **Documents written:**
  - [README.md](README.md) — project overview, calibrated position, sibling context, Maxwell-pattern claim.
  - [docs/ROADMAP.md](docs/ROADMAP.md) — Phases 0 through 4 with deliverables, out-of-scope clauses, risks.
  - [docs/journey/FOOTING.md](docs/journey/FOOTING.md) — initial locked items (sibling layout, contour discipline carries, cross-substrate transfer thesis, Maxwell-pattern credit allocation) and pending items (literature reading, simulator choice, substrate-conditional reading rules verification).
  - [docs/journey/MAPPINGS.md](docs/journey/MAPPINGS.md) — initial mapping table seeded with the s-regime ↔ glass-aging claim. Most rows are Open pending Phase 0 reading.
  - [docs/manual/09-discoveries.md](docs/manual/09-discoveries.md) — live discovery log, seeded with the project's central thesis.
  - [docs/manual/README.md](docs/manual/README.md) — manual layout, reading order.

## How to start the next session

The first concrete task is **Phase 0** per [docs/ROADMAP.md](docs/ROADMAP.md):

> Read Cugliandolo–Kurchan 1993 directly. Read one canonical review (Bouchaud–Cugliandolo–Kurchan–Mézard 1998 in *Spin Glasses and Random Fields*, or Berthier–Biroli 2011 *Rev. Mod. Phys.*, or Crisanti–Ritort 2003 *J. Phys. A* experimental review). Identify the canonical FDR observable in glass aging. Survey simulator options.

The discipline rule for Phase 0 specifically: **read first, simulate second.** Do not write a glass simulator until you can describe what FDT violation in aging glasses looks like in plain English.

## What carries from sibling projects

In rough order of when it is needed:

1. **Vendored physics primitives** (`mpc_*_kernel/physics/`): SHA-pinned vendor from `mpc-brain`, currently held by `mpc-foundry` and `mpc-quantum`. Copy verbatim into `mpc_glass_kernel/physics/` per the F-001 discipline of `mpc-quantum`'s journey. The verify script (`scripts/verify_vendored_physics.py`) carries directly. Hashes match across siblings.

2. **Kernel modules** (`mpc_*_kernel/*.py`): forked from `mpc-foundry` via `mpc-quantum`. All internal imports are relative, so the modules port between siblings without code changes. Three cosmetic edits (package-name strings) are applied per `mpc-quantum`'s F-010.

3. **Methodology**:
   - Contour discipline (four-state assignment per claim; cite or experiment for promotion).
   - Substrate-conditional reading rules (v6 paper Appendix F). The Markovian sign caveat (F-003) and detection-event preprocessing (F-007) are the worked examples earned from `mpc-quantum`.
   - Maxwell-pattern credit allocation: components are independently validated; the unification is what `mpc-glass` tests.

## What is new and project-specific

In order of when it gets built (Phases 1+):

- **`scripts/eaglass.py`**: Edwards–Anderson 2D Ising spin glass simulator. Glauber dynamics. Sub-critical temperature $T \approx 0.7\,T_c$. ~200 lines of numpy. The canonical model for glass-aging studies.
- **`mpc_glass_packs/glass_socket/`**: adapter that reads spin-glass trajectories and emits TwinTicks. Each tick carries one Monte Carlo timestep; signals are spin values (or coarse-grained order parameters).
- **FDR measurement harness**: paired-trajectory protocol with small applied field as perturbation. Computes $\chi(t, t_w)$ and $C(t, t_w)$. Plots parametric FDR vs canonical Cugliandolo–Kurchan shape.
- **Manual chapters**: glass-substrate primer for MPC operators; aging dynamics and the X(t, t_w) ratio; comparison to MPC s-regime; substrate-conditional reading rules earned for glasses (likely none new; verify in Phase 2).

## Project-level disciplines

Carry from `mpc-quantum`:

1. **Preserve the thermodynamic paradigm.** MPC's primitives (trail vectors, regime classes, flux ledger, observer always pays) are unchanged. Substrate-conditional reading rules adjust the *reading* of observables, not the framework.
2. **Defer to glass physics for names and empirics, not for paradigm.** Cugliandolo–Kurchan, Bouchaud, Berthier own the field's vocabulary. Use their terms where they exist.
3. **Footing before scaffolding.** Do not build on a pending FOOTING item.
4. **Contour discipline applies to every claim.** Every mapping row gets a contour assignment with citation or experiment.
5. **No silent overclaim.** If MPC's s-regime shape does not match glass aging, document the divergence honestly. The framework either holds or it does not.

Plus one specific to this substrate:

6. **Treat glass-physics literature with the deference of the QC field's prior art.** Thirty years of careful FDT-violation measurement is a substantial body of work. The `mpc-quantum` deferences D-003 through D-006 are the precedent for how to credit it.

## Risks to watch

- **Glass physics is a huge field.** Mode-coupling theory, replica symmetry breaking, dynamical heterogeneity, kinetically-constrained models, multiple competing theoretical frameworks. The contour discipline says: stay narrow on the FDR aging shape question. Do not try to map MPC onto all of glass physics.
- **Aging timescales.** Real glasses age over decades of physical time. Simulations need enough Monte Carlo sweeps to see aging on visible scales. Edwards–Anderson at $T \approx 0.7\,T_c$ shows aging in $10^4$–$10^6$ sweeps; tractable on commodity hardware (minutes to hours, not days). If aging is not visible in initial runs, calibrate $T$ closer to $T_c$ and lattice size $L$.
- **Simulator vs experiment.** We compare MPC's predicted shape to the *generic* aging shape predicted by glass physics, which has been validated experimentally many times. We do not need to match a specific experimental dataset numerically. That is the more tractable target.
- **The dial-in trap.** Same as `mpc-quantum`. When the FDR shape on glass simulations does not match MPC's prediction exactly, do NOT tune simulator parameters until it does. Document the divergence honestly. The framework either holds or it does not; either is a result.
- **Deference fatigue.** After six contour reallocations in `mpc-quantum`, there is a temptation to over-defer. The Maxwell pattern is the right framing here: components are independently validated; the unification is what we are testing. Stake the unification claim at the right level — neither dismissing it ("just renaming") nor overclaiming it ("MPC discovered glass aging").

## What is at H:\\ for context

- `H:\\mpc-foundry\\` — sibling. Industrial-twin application; thermal_envelope dual-description precedent. The `mpc_foundry_kernel/` is the source for the kernel-module fork.
- `H:\\mpc-brain\\` — sibling. Cognitive-architecture application; four-scenario Langevin validation rig. Brain's `docs/temp/SESSION_A_STATE.md` (referenced in `mpc-quantum`) is the empirical foundation for the s-regime FDR shape claim. The `physics_primitives` source lives here.
- `H:\\mpc-quantum\\` — sibling. QC application; cross-substrate FDR transfer measured (Session 4, `F-014` and discoveries log entry); journey work in `docs/journey/`. The contour methodology and substrate-conditional reading rules are documented in v6 Appendix F and Appendix H of `docs/v5 MPC ...md` (or `v6` if/when that lands).
- `H:\\mpc-profiles\\` — sibling. Substrate calibration profile registry; once glass-substrate profiles are defined, they live there.
- `H:\\mpc-sat\\` — sibling. SAT proof traces.
- `H:\\mpc-glass\\` — this project.

## Canonical citations to read first

For Phase 0:

1. **Cugliandolo, Kurchan 1993.** *Analytical solution of the off-equilibrium dynamics of a long-range spin-glass model.* Phys. Rev. Lett. 71, 173. The foundational FDT-violation framework for glass aging.
2. **Bouchaud, Cugliandolo, Kurchan, Mézard 1998.** *Out-of-equilibrium dynamics in spin glasses and other glassy systems.* In *Spin Glasses and Random Fields* (A. P. Young, ed.). The canonical review; densest single source.

If those are dense, supplement with:

3. **Berthier, Biroli 2011.** *Theoretical perspective on the glass transition and amorphous materials.* Rev. Mod. Phys. 83, 587. Modern review of glass-transition theory.
4. **Crisanti, Ritort 2003.** *Violation of the fluctuation-dissipation theorem in glassy systems: basic notions and the numerical evidence.* J. Phys. A 36, R181. Experimental review with explicit FDR-shape figures.

These are the citations any v1 `mpc-glass` paper would lead with, and the contour discipline requires them to be cited explicitly when contour-assigning row 01 of `MAPPINGS.md`.

## On the framework's identity (carry from v6 paper)

MPC is the finite-flux generalisation of Boolean logic. Boolean is the asymptote, recovered as $\Phi^* \to \infty$. MPC specifies the deviation profile away from Boolean. The framework's reach is empirical: trail vectors and the four-regime classification port across substrates without modification. The s-regime FDR aging shape is the framework's most-validated specific prediction; `mpc-glass` is the next test of its substrate portability.

The cross-substrate unification claim is what this project tests. If the s-regime shape transfers to glass aging cleanly, MPC's primitives are doing real cross-domain work. If it does not, that identifies what is specific to MPC versus what is specific to glasses.

---

Hand-off written 2026-04-29 by the same operator-Claude pair that completed `mpc-quantum`'s bootstrap, journey work, Session 4 hinge measurement, and v6 paper rewrite in the immediately prior session. The pivot to glass aging is a deliberate next step in the empirical-foothold programme: if the s-regime FDR shape transfers to a third independent substrate, the framework's cross-substrate unification claim has substantively more weight. If it does not, the divergence is itself a calibration result.
