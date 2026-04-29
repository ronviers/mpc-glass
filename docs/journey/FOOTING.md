# FOOTING

What we have locked in, and what we need to lock in next. Pending items block any mapping row in [MAPPINGS.md](MAPPINGS.md) that depends on them.

The rule: don't build a row that rests on a pending footing item. Mark the row Open and move on until the footing lands.

Bootstrap stage. Most items are pending; few are locked. The locked items are the ones that carry from `mpc-quantum` and the project's central thesis.

---

## Locked

### F-001 — Sibling layout, no parent

`mpc-glass` is a sibling project of `mpc-foundry`, `mpc-brain`, `mpc-quantum`, `mpc-sat`, `mpc-profiles` at `H:\`. There is no parent. No runtime dependency between siblings; physics is vendored with SHA pin, kernel modules are forked. The `mpc-physics` carve-out is planned but not yet present.

### F-002 — Contour discipline carries from mpc-quantum

The methodology earned in `mpc-quantum` applies here directly:
- Six contour states (Adheres / named, Adheres / unnamed, Diverges / holds, Diverges / fails, plus Open and `?`).
- Discipline rule: every claim in MAPPINGS.md gets a contour assignment with citation or experiment for promotion.
- Substrate-conditional reading rules (Markovian sign caveat F-003 and detection-event preprocessing F-007 of `mpc-quantum`) are the worked examples; new ones are earned per substrate.
- Maxwell-pattern credit allocation: components are independently validated; the unification is what we test.
- Three governing rules carry: preserve thermodynamic paradigm; defer to substrate field for names and empirics, not for paradigm; footing before scaffolding.

The six deferences D-001 through D-006 in `mpc-quantum`'s Deference Log are the precedent for how to credit prior art.

### F-003 — The cross-substrate transfer thesis is the project's central claim

MPC's s-regime FDR aging shape has been validated on:

- Langevin substrate (`mpc-brain` Session A four-scenario rig): all four regimes classified correctly; the s-regime FDR aging diagonal is the canonical measured shape.
- Surface-code syndrome streams (`mpc-quantum` Session 4): s-regime shape transfers cleanly at sub-threshold operation; partial validation of v4 §5.

`mpc-glass` tests transfer on a third substrate — glass aging — where the same observable has been measured carefully for thirty years (Cugliandolo–Kurchan 1993 onward).

If the shapes match, three independent empirical footholds for MPC's s-regime claim, on substrates with no shared physical content beyond the framework's primitives. That is the project's central claim and the success criterion for v7 paper or v6 update.

### F-004 — Maxwell-pattern credit allocation

The s-regime FDR shape on glasses has been characterised empirically and theoretically by glass physicists for decades (Cugliandolo–Kurchan 1993, Bouchaud, Berthier, et al.). The MPC contribution at this substrate is *cross-substrate unification* — the same shape appearing on substrates with no shared physical content.

We inherit the empirical groundedness of the glass-physics components. What requires further validation is the unification claim itself, which is what `mpc-glass` tests. The structural pattern is Maxwell's: Coulomb, Ampere, Faraday were each independently validated; Maxwell unified them under a single equation set; what unification required separately was a new prediction (electromagnetic waves). The MPC analogue: the cross-substrate transfer is the prediction the unification implies.

### F-006 — Relative imports as a sibling-family discipline

The MPC kernel modules use **relative imports throughout** (`from .events`, `from .physics`, `from .trace_bus`, etc.). This was foundry's original authoring choice; it turns out to be load-bearing for sibling-to-sibling kernel transfer. The kernel ports between siblings without code changes — only cosmetic package-name edits in docstrings and error messages (3 sites, documented per `mpc-quantum` F-010).

**Discovered at `mpc-quantum` F-010.** When the foundry kernel was forked into `mpc_quantum_kernel/`, the discovery was that no internal imports needed editing — they were all `from .X` rather than `from mpc_foundry_kernel.X`. The 3 sites that did need editing were docstrings and error-message strings referring to the package by name; cosmetic, not functional.

**Discipline for `mpc-glass` and any future sibling.**

- *Inside the kernel package*, use relative imports (`from .events`, `from .physics import Phase`, etc.). Absolute references (`from mpc_glass_kernel.events`) belong only at cross-package boundaries — pack code, experiment scripts, scripts directory.
- *When forking the kernel from a sibling* (Phase 2), the only edits required are the package-name strings in docstrings and error messages. Catalogue from `mpc-quantum` F-010: `__init__.py` lines 1 and 8 (top docstring); `flux_ledger.py` lines 64 and 79 (docstring + error message); `profiles/loader.py` line 103 (docstring). The exact line numbers may shift slightly with future kernel edits; the pattern is `grep -n 'mpc_foundry_kernel\|mpc_quantum_kernel' kernel_dir/`.
- *Vendor source.* Either `mpc-foundry` (canonical upstream of the fork chain) or any tested sibling (`mpc-quantum` is the most recent tested fork at the time of this writing). Both produce byte-equivalent content after the cosmetic edits. Slight preference for vendoring from foundry directly to keep the lineage clean.

**Implication for Phase 2.** When `mpc_glass_kernel/` is created, the import structure should remain relative throughout. Any new module added to the kernel for glass-substrate-specific work should follow the same discipline. Future siblings (`mpc-physics` carve-out, others) inherit the property automatically if it's preserved here.

**Credit.** Foundry's original authors made the imports relative. The portability property is theirs; later siblings inherited it. Naming the discipline explicitly is the contribution at this footing layer — turning an accident-of-authorship into a deliberate sibling-family rule.

### F-005 — Substrate-favourable conditions for MPC's machinery

Glass substrate is structurally favourable for the framework's primitives in three ways:

1. *Explicit memory kernels.* Glasses have history-bearing dynamics by construction; v4's Table 1 sign predictions for $\gamma_A$ and $\gamma_{ij}$ probably apply directly. The Markovian sign caveat (F-003 of `mpc-quantum`) likely does not bite here. *To verify in Phase 2.*
2. *Continuous local readouts.* Spin states, particle positions are observable directly; the substrate's natural readout matches the trail-vector formalism's locality assumption. Detection-event preprocessing (F-007 of `mpc-quantum`) is not needed. *To verify in Phase 2.*
3. *Natural bath.* High-temperature equilibrium is the substrate's own reservoir; the shuffled-events bath construction (F-011 of `mpc-quantum`) is not needed. *To verify in Phase 2.*

Implication: if MPC's s-regime FDR shape *fails* to transfer cleanly to glass aging, that is a more serious calibration finding than the QC Session 4 partial result. The substrate is set up favourably for the framework; failure to transfer would suggest the substrate-conditional reading rules earned in `mpc-quantum` were doing more work than realised, or that the framework's claim about the s-regime shape is more substrate-specific than the v4/v6 papers state.

---

## Pending

### P-001 — Cugliandolo–Kurchan 1993 read carefully

Read the foundational paper directly. Identify:
- The exact form of the FDR observable $X(t, t_w)$ they predict.
- The aging exponents and asymptotic shapes.
- The model class for which their derivation applies (long-range spin glass; spherical model; etc.).
- The relationship of their $X(t, t_w)$ to MPC's $X$ in v4 §5 / Appendix E.

**Blocks.** Any mapping row that claims MPC's s-regime shape matches their prediction. Specifically MAPPINGS row 01.

### P-002 — One canonical review

Pick one and read densely:
- Bouchaud–Cugliandolo–Kurchan–Mézard 1998 review in *Spin Glasses and Random Fields* (densest single source).
- Berthier–Biroli 2011 *Rev. Mod. Phys.* 83, 587 (modern theoretical perspective).
- Crisanti–Ritort 2003 *J. Phys. A* 36, R181 (experimental review with explicit FDR-shape figures).

**Blocks.** Contour assignment for the s-regime ↔ glass-aging mapping. Bibliography for the v7 paper update.

### P-003 — Simulator choice and parameter calibration

Edwards–Anderson 2D Ising spin glass is the default. Verify it shows aging dynamics on tractable timescales. Alternative: kinetically-constrained model (e.g., Fredrickson–Andersen) if EA is too slow.

Specific calibration questions:
- Lattice size $L$. Default $L = 32$ or $L = 64$.
- Temperature $T$. Default $T \approx 0.7\,T_c$, where $T_c$ is the EA spin-glass transition temperature.
- Waiting times $t_w$. Default $\{10^2, 10^3, 10^4\}$ Monte Carlo sweeps.
- Observation times $t$. Default $[t_w, 10\,t_w]$.

**Blocks.** Phase 1 implementation.

### P-004 — Substrate-conditional reading rules verification

Verify whether F-003 (Markovian sign caveat) and F-007 (detection-event preprocessing) from `mpc-quantum` apply to glasses. Prior expectation per F-005: NEITHER applies. But verify experimentally before declaring it:

- Run basic autocorrelation on glass trajectories.
- Confirm $\tau_A$ grows with waiting time (the aging signature).
- Check whether $\gamma_A$ signs match v4 Table 1 predictions or whether they invert.
- Confirm that the natural local readout (spin values) suffices as $\dot{x}$ — no preprocessing needed.

If verified, document as new locked items (F-006 onward). If F-003 or F-007 *do* apply unexpectedly, that's a substrate-conditional rule earned for this substrate and a deference log entry.

**Blocks.** Phase 3 FDR measurement (the substrate-correct readings have to be in place first).
