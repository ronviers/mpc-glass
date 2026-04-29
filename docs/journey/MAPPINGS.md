# MAPPINGS — Glass substrate ↔ MPC working ledger

Working file. Each row is one concept-pair under analysis. Bootstrap stage; most rows are Open pending Phase 0 reading.

The contour discipline carries from `mpc-quantum`'s Appendix H methodology. The substrate-conditional reading rules carry from v6 Appendix F.

## Three governing rules (carry from mpc-quantum)

1. **Preserve the thermodynamic paradigm.** MPC primitives (trail vectors, regime classes, flux ledger) are unchanged.
2. **Defer to glass physics for names and empirics, not for paradigm.** Cugliandolo–Kurchan, Bouchaud, Berthier own the field's vocabulary.
3. **Footing before scaffolding.** Don't build a row that rests on a pending FOOTING item.

---

## Status legend

| Status | Meaning |
|---|---|
| **Open** | Hypothesis. Not yet checked against glass-physics literature or measured. |
| **Provisional** | Consistent with literature; awaiting empirical test. |
| **Locked** | Empirically supported (within scope) or formally entailed. |
| **Reworked** | MPC adjusted to defer to glass physics. See Resolution and Deference Log. |
| **Doesn't carry** | Mapping rejected. |

## Contours legend

Same four states as `mpc-quantum` Appendix H.

| Contour | Meaning | Contribution |
|---|---|---|
| **Adheres / named** | MPC reading matches substrate reality, field has a name | Floor: vocabulary |
| **Adheres / unnamed** | MPC reading matches substrate reality, no field name | Mid-tier: framing work |
| **Diverges / holds** | MPC predicts something the field doesn't, holds empirically | Ceiling: dual description |
| **Diverges / fails** | MPC predicts something different, fails empirically | Calibration: feeds next paper revision |
| **?** | Not yet examined | (Default for Open rows) |

Discipline rule: no row reaches Locked with Contour = `?`. Every promotion to Provisional or Locked carries the citation or experiment that justified the calibration.

---

## Summary table

Quick-scan view. Detail subsections below for any row with notes, conflicts, or open questions.

| # | Glass concept | MPC counterpart | Confidence | Status | Contour |
|---|---|---|---|---|---|
| 01 | FDT violation in glass aging | s-regime FDR aging shape | Strong | Open | ? (test in Phase 3) |
| 02 | Two-time correlation $C(t, t_w)$ | Trail-vector autocorrelation | Strong | Open | Adheres / named (provisional) |
| 03 | Response function $R(t, t_w)$ | Trail-vector response under perturbation | Strong | Open | Adheres / named (provisional) |
| 04 | $X(t, t_w)$ ratio | $X$ in v4 §5 / Appendix E | Strong | Open | Adheres / named (provisional) |
| 05 | Aging exponents / scaling forms | Falloff profile (v6 §7 open question) | Moderate | Open | ? |
| 06 | Replica symmetry breaking phases | k-regime extensions (v6 §8) | Weak | Open | ? |
| 07 | Glass transition $T_c$ | Operator-level Boolean limit boundary | Weak | Open | ? |
| 08 | Edwards–Anderson order parameter $q_{EA}$ | Trail-vector overlap of similar propositions | Moderate | Open | ? |
| 09 | Mode-coupling theory | (no obvious MPC counterpart at this scope) | n/a | Doesn't carry | n/a |
| 10 | Dynamical heterogeneity | Trail-vector spatial correlations (potential extension) | Weak | Open | ? |

---

## Detail rows

### 01 — FDT violation in glass aging ↔ MPC s-regime FDR aging shape

The project's central claim. If shapes match, the cross-substrate transfer thesis (F-003 of FOOTING) has a third independent empirical foothold.

- **Glass-physics concept.** $X(t, t_w) = T \cdot R(t, t_w) / \partial_{t_w} C(t, t_w)$ becomes time-dependent in glasses; the parametric $\chi$ vs $C$ plot has the canonical aging shape — FDT diagonal at short times, bend, plateau at long times (Cugliandolo–Kurchan 1993).
- **MPC counterpart.** s-regime FDR (v4 §5; v6 Appendix E): aging diagonal that bends away from FDT, plateaus at long times. Validated on Langevin substrate (`mpc-brain` Session A) and on surface-code syndrome streams at sub-threshold operation (`mpc-quantum` Session 4).
- **Evidence.**
  - Brain Session A four-scenario rig: s-regime FDR shape measured directly with the parametric plot, validated against v4 §5 prediction.
  - mpc-quantum Session 4: s-regime shape transferred to QC syndromes at sub-threshold operation (Figure 1 of v6).
  - Glass-physics empirical literature: thirty years of measurements — colloidal glasses, spin glasses, structural glasses, polymer melts.
- **Conflicts expected.** None at the qualitative level. Glass aging is essentially the substrate the s-regime shape was originally inspired by (via Cugliandolo–Kurchan). The quantitative comparison may reveal substrate-specific exponents.
- **Open questions.**
  - Does the EA spin-glass simulation reproduce the canonical Cugliandolo–Kurchan aging shape?
  - Does MPC's kernel reproduce the same shape on the same simulation?
  - Are the shapes quantitatively comparable, or only qualitatively?
  - If only qualitatively, what substrate-conditional calibration is needed?
- **Sources to read first (per FOOTING P-001, P-002).**
  - Cugliandolo, Kurchan 1993, *Phys. Rev. Lett.* 71, 173.
  - Bouchaud, Cugliandolo, Kurchan, Mézard 1998 review.
  - Crisanti, Ritort 2003, *J. Phys. A* 36, R181 (experimental review).

### 02 — Two-time correlation $C(t, t_w)$ ↔ Trail-vector autocorrelation

- **Glass-physics concept.** $C(t, t_w) = \langle \phi(t) \phi(t_w) \rangle$ where $\phi$ is the relevant observable (spin, density fluctuation, etc.). In aging glasses, $C$ depends on both $t$ and $t_w$, not just their difference.
- **MPC counterpart.** $C(t, t') = \langle d_A(t) \cdot d_A(t') \rangle$ from v4 Appendix E. The trail-vector autocorrelation is computed by the kernel's `autocorr_fft` and `tau_integral` primitives.
- **Provisional contour.** Adheres / named. The two are the same observable in different vocabulary. Glass physics has the formal definition and the empirical measurements.
- **Open questions.**
  - Is the substrate-correct trail-vector observable on a spin-glass simulation just the spin field $s_i(t)$? Or does it need coarse-graining (e.g., the EA order parameter $q_{EA}$)?

### 03 — Response function $R(t, t_w)$ ↔ Trail-vector response under perturbation

- **Glass-physics concept.** $R(t, t_w) = \delta \langle \phi(t) \rangle / \delta h(t_w)$ where $h$ is a small perturbing field applied at time $t_w$.
- **MPC counterpart.** Response function $R(t, t')$ in v4 Appendix E. Computed by paired-trajectory protocol with applied perturbation.
- **Provisional contour.** Adheres / named.

### 04 — $X(t, t_w)$ ratio ↔ MPC's $X$

- **Glass-physics concept.** $X(t, t_w) = T \cdot R(t, t_w) / \partial_{t_w} C(t, t_w)$. Time-dependent in glasses.
- **MPC counterpart.** $X(t, t')$ in v4 Appendix E. Definitionally identical.
- **Provisional contour.** Adheres / named. Same observable, same definition. The substantive question is whether the *shape* of $X$'s parametric trajectory matches across substrates (row 01).

### 05 — Aging exponents and scaling forms ↔ Falloff profile

- **Glass-physics concept.** Glass aging exhibits scaling forms: $C(t, t_w) \sim f(t/t_w^\mu)$ with substrate-specific exponent $\mu$. Bouchaud's "trap model" and other aging theories predict specific functional forms.
- **MPC counterpart.** v6 §7 names the falloff profile — the functional form of regime probabilities $P(\text{regime} \mid \Phi^*)$ at fixed graph topology — as an open theoretical problem. The aging exponents in glass physics may directly inform candidate functional forms.
- **Open questions.**
  - Does the polynomial-in-$1/\Phi^*$ candidate (v6 §7 candidate 1) match glass-aging scaling forms?
  - Does the critical-scaling candidate (v6 §7 candidate 2) match the universality classes in glass-physics finite-size scaling?
  - Does Bouchaud's trap model give an explicit functional form that could be the falloff profile?
- **Worth following up if the cross-substrate transfer in row 01 lands cleanly.** The unification claim implies the falloff profile across substrates is the same shape, which would constrain candidate functional forms substantially.

### 06 — Replica symmetry breaking ↔ k-regime extensions

- **Glass-physics concept.** Glasses below $T_c$ exhibit replica symmetry breaking (RSB) — the equilibrium state is described by a hierarchical structure of pure states. RSB is mathematically intricate and physically corresponds to a hierarchical landscape of free-energy minima.
- **MPC counterpart.** v6 §8's higher-order frustration / glassy phases extension — relaxing the framework's commitment to scalar trail vectors and introducing hierarchical structure. RSB may map onto glassy MPC k-regime variants.
- **Conflicts.** None obvious; this is structural mapping work.
- **Open questions.**
  - Does the v6 §8 higher-order frustration extension map onto RSB?
  - Are the k-regime variants in glassy MPC the same as RSB phases, or just structurally similar?
- **Source to read.** Mézard–Parisi–Virasoro 1987 *Spin Glass Theory and Beyond* is the canonical RSB reference. Also relevant: stat mech of SAT (Mézard–Parisi–Zecchina lineage), already credited in `mpc-quantum`'s D-006 deference.

---

## Deference Log

When glass physics names something MPC was about to coin, or when glass-physics measurements override an MPC prediction, the adjustment lands here with a back-pointer to the row that triggered it. The thermodynamic paradigm itself is preserved; the deferences are over names, substrate-specific calibrations, and empirical reality, not over the framework's primitives.

### D-001 (precedent — inherited from mpc-quantum) — six deferences D-001 through D-006

The Markovian sign caveat (D-001 of `mpc-quantum`, originally inherited from `mpc-brain`), detection events as $\dot{x}$ (D-002), DKLP 2002 owns the global thermodynamic-phase framing of surface codes (D-003), the dynamical-decodability line owns the non-equilibrium refinement (D-004), steady-state and burst-then-steady framings of magic state factories (D-005), real-time decoder thermodynamic engineering owns the $\Phi_{book}$ engineering layer (D-006).

These six deferences are the precedent for how to credit prior art on a substrate with developed thermodynamic-frame literature. Glass-physics deferences will likely take the same shape — specific named workers and specific framings whose prior art the framework absorbs.

*No mpc-glass-specific entries yet.* The first entry is likely after Phase 0 reading: a deference to Cugliandolo–Kurchan for the FDR aging shape framing (which the framework adopts as its s-regime prediction explicitly, with credit), and possibly to Bouchaud for the trap-model framing of aging dynamics.

---

## How to update this file

1. **Adding a row.** New numeric ID. Add to the summary table and a detail subsection.
2. **Promoting a row.** Open → Provisional requires a citation (Phase 0 reading lands). Provisional → Locked requires either an empirical measurement or a formal entailment from a Locked footing item.
3. **Deferring.** Found a conflict? Don't fight it. Update the Resolution field with what we changed in MPC, add a Deference Log entry, set the row's Status to "Reworked".
4. **Promoting up.** When a row's finding generalises beyond the row, add an entry to `../manual/09-discoveries.md` and link to the row.
