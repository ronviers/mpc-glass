# mpc-glass — Roadmap

Phase-by-phase plan. Each phase is bounded; each adds a visible artefact.

The discipline rules from `mpc-quantum` carry over verbatim:

1. Preserve the thermodynamic paradigm.
2. Defer to glass physics for names and empirics, not for paradigm.
3. Footing before scaffolding.
4. Contour discipline applies to every claim.
5. No silent overclaim.

Plus one new for this project:

> **Treat glass-physics literature with the deference of QC field's prior art.** Thirty years of careful FDT-violation measurement is a substantial body of work. The `mpc-quantum` deferences D-003 through D-006 are the precedent for how to credit it.

---

## Phase 0 — Bootstrap (mostly reading)

**Scope.** Set up the journey scaffolding (already done at bootstrap). Read Cugliandolo–Kurchan 1993 directly. Read one canonical review. Identify the canonical FDR observable in glass aging. Survey simulator options. Update `docs/journey/MAPPINGS.md` with contour assessments.

**Deliverables.**

- Reading notes on Cugliandolo–Kurchan 1993 in `docs/manual/09-discoveries.md`. Specifically: the exact form of $X(t, t_w)$ they predict, the aging exponents and asymptotic shapes, the model class for which their derivation applies (long-range spin glass; spherical model; etc.).
- Reading notes on one canonical review (Bouchaud–Cugliandolo–Kurchan–Mézard 1998 review, Berthier–Biroli 2011, or Crisanti–Ritort 2003). Pick the densest.
- Update `docs/journey/MAPPINGS.md` row 01 with contour assessment of MPC's s-regime claim against the canonical glass-aging shape.
- Decision on simulator: Edwards–Anderson 2D Ising spin glass is the default. Verify aging timescales are tractable on commodity hardware. Alternative: kinetically-constrained model (e.g., Fredrickson–Andersen) if EA is too slow.

**Out of scope.** Simulator implementation. FDR measurement.

**Risks.** Cugliandolo–Kurchan paper is technical; needs careful reading. Don't try to absorb all of glass physics at once. Stay narrow on the FDR aging shape.

---

## Phase 1 — Glass simulator

**Scope.** Build the simplest simulator that exhibits glass aging. Verify aging signature directly before integrating with the kernel.

**Deliverables.**

- `scripts/eaglass.py` — Edwards–Anderson 2D Ising spin glass on $L \times L$ lattice with $\pm J$ random bonds. Glauber dynamics. Sub-critical temperature $T \approx 0.7\,T_c$. ~200 lines of numpy.
- Verify aging signature directly: compute the two-time correlation $C(t, t_w)$ for varying $t_w$. Aging means $C(t, t_w)$ depends on both $t$ and $t_w$, not just their difference. Plot $C$ vs $t/t_w$ should show waiting-time-dependent collapse.
- Decide on system size and waiting times. Typical: $L = 32$ or $L = 64$, $t_w \in \{10^2, 10^3, 10^4\}$ Monte Carlo sweeps, $t \in [t_w, 10\,t_w]$.
- Document parameter choices in `docs/journey/FOOTING.md` with reasoning.

**Out of scope.** MPC kernel integration. FDR perturbation experiment.

**Risks.** Aging timescales. If $L$ is too small or $T$ is too far from $T_c$, aging won't be visible on tractable simulation timescales. Calibration during this phase.

---

## Phase 2 — Kernel adapter (`glass_socket`)

**Scope.** Wire the spin-glass simulator into the MPC kernel via a `glass_socket` adapter.

**Deliverables.**

- `mpc_glass_kernel/physics/` — vendored from `mpc-foundry` (which vendors from `mpc-brain`) with SHA pin. `scripts/verify_vendored_physics.py` passes.
- `mpc_glass_kernel/*.py` — forked from `mpc-foundry`. Three cosmetic edits applied (package-name strings) per `mpc-quantum` F-010 precedent.
- `mpc_glass_packs/glass_socket/` — adapter that reads spin trajectories and emits TwinTicks. Each tick carries one Monte Carlo timestep; signals are spin values (or a coarse-grained order parameter such as the Edwards–Anderson order parameter $q_{EA}(t, t_w) = \langle s_i(t) s_i(t_w) \rangle$).
- Confirm the kernel's autocorrelation primitives (`autocorr_fft`, `tau_integral`, `correlation_time`) work on glass trajectories. Verify $\tau_A$ grows with waiting time — the explicit aging signature.
- **Substrate-conditional reading rules verification.** Check whether F-003 (Markovian sign caveat) and F-007 (detection-event preprocessing) from `mpc-quantum` apply to glasses. Prior expectation: NEITHER applies, because glasses have explicit memory kernels and continuous local observables. If verified, document in `docs/journey/FOOTING.md` as new locked items. If they DO apply, that's a substrate-conditional rule earned for this substrate.

**Out of scope.** FDR measurement. Comparison to glass-physics predictions.

**Risks.** The substrate-conditional reading rule verification is non-trivial. Run the basic autocorrelation on glass trajectories first and confirm shapes are interpretable before declaring the rules don't apply.

---

## Phase 3 — FDR measurement

**Scope.** The hinge phase. Measure MPC's s-regime FDR shape on the spin-glass simulator and compare to the canonical Cugliandolo–Kurchan prediction.

**Deliverables.**

- Paired-trajectory protocol: same noise seed (deterministic Glauber), base trajectory at zero applied field, perturbed trajectory at small applied field $h$. The matched-noise pairing is direct in MC simulation (just use the same RNG sequence with a small perturbing term).
- Compute $C(t, t_w)$ on the base ensemble for several waiting times $t_w$.
- Compute $R(t, t_w)$ from the response of the magnetisation to the applied field, integrated over time-since-$t_w$.
- Plot parametric FDR ($\chi$ vs $C$) for each $t_w$.
- Compare directly to the canonical Cugliandolo–Kurchan aging shape: FDT diagonal at short times, bend, plateau at long times.
- Document the result in `docs/journey/FOOTING.md` (analogous to `mpc-quantum`'s F-014).

**Out of scope.** Quantitative matching to specific experimental datasets. We compare to the *generic* predicted shape.

**Risks.** This is the project's hinge measurement. The discipline rule applies hard:
- If shapes match qualitatively, that is a *Diverges / holds* result (per `mpc-quantum`'s contours framework). Two cross-substrate transfers in hand.
- If shapes match quantitatively, that is a stronger result.
- If shapes differ qualitatively, that is a *Diverges / fails* result — MPC's s-regime is NOT just glass aging on a different substrate. Real calibration finding for v7 paper.
- Do not tune simulator parameters until shapes match. Document the divergence honestly.

---

## Phase 4 — Contour assessment and write-up

**Scope.** Stake the claim relative to glass-physics prior art. Update the v6 paper bibliography (or write v7 conditional on the result).

**Deliverables.**

- For each component of MPC's s-regime claim, assign a contour state per the Appendix H methodology of v6: Adheres / named, Adheres / unnamed, Diverges / holds, Diverges / fails.
- Credit Cugliandolo–Kurchan, Bouchaud, Berthier explicitly. The MPC contribution is at the cross-substrate-unification level, not the discovery-of-aging-shape level.
- Update `mpc-quantum`'s v6 paper bibliography and §5 to add glass-substrate evidence (or v7 paper rewrite if preferred).
- Manual chapter on the glass substrate, comparable in scope to v6's QC §5.
- Discoveries-log entry capturing the cross-substrate transfer result and its implications for the framework's empirical position.

**Out of scope.** New substrate explorations. v7 paper rewrite (separate session, conditional on Phase 3 result).

---

## What carries from siblings, day-zero

When Phase 2 lands, the immediately-usable pieces:

- `mpc_*_kernel/physics/` (SHA-pinned) — `autocorr_fft`, `tau_integral`, `correlation_time`, `survival_margin`, `cross_dissipation`, `measure_fdr`. Identical content; identical SHA pin. The four-scenario Langevin regression in `mpc-brain` Session A is the acceptance test by reference.
- Typed events, `TraceBus`, `FluxLedger`, `RegimeClassifier`, `InstructionSet`, `AdvisoryArbiter`, `MetaLedger`, `HypothesisGraph`, `TrailWindow`, `TwinSocket` — fork verbatim from `mpc-foundry` with three cosmetic edits.
- Methodology: contour discipline, substrate-conditional reading rules, Maxwell-pattern credit allocation.

What needs to be new:

- `glass_socket` — substrate adapter for spin-glass trajectories (later: structural glass, colloidal glass).
- Manual chapters: glass-substrate primer; aging dynamics; comparison to MPC s-regime.

## Cost in time, calibrated

Comparison: `mpc-quantum` got from "first commit" to "full kernel + smoke pipeline + Session 4 FDR + v6 paper" in ~one extended working session. `mpc-glass` is structurally simpler (no detection-event preprocessing, probably no sign caveat, simulator is well-documented) but the glass-physics literature requires more careful reading. Reasonable estimate: Phases 0–4 in 1–2 working sessions, with most time in Phase 0 (literature) and Phase 3 (FDR measurement).
