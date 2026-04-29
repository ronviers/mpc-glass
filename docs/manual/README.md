# mpc-glass — Operator Manual

Bootstrap stage. Most chapters are placeholders; they fill in as work lands.

The structural chapters (kernel types, ISA, regime classifier, ledger) inherit from `mpc-foundry` / `mpc-quantum`. A future session can either copy those chapters verbatim and edit for glass-substrate specifics, or reference the sibling chapters directly and only document the glass-substrate-specific pieces here.

The chapters that are NEW for this project, and need to be written from scratch:

- A glass-substrate primer for MPC operators ("what is glass aging, what is FDT violation, what is the X(t, t_w) ratio, what is an Edwards–Anderson spin glass").
- A chapter on the glass-aging FDR observable and how MPC's s-regime shape compares.
- A chapter on substrate-conditional reading rules earned for this substrate (likely none new; verify in Phase 2).
- A chapter on the cross-substrate unification result (filled in after Phase 3).

The chapter that is actually written today is the discoveries log ([09-discoveries.md](09-discoveries.md)) — the project starts there because everything new lands there first.

## Layout (target)

```
docs/manual/
├── README.md                   ← this file
├── 01-overview.md              ← what mpc-glass is (mostly defer to project README)
├── 02-isa.md                   ← inherits from foundry; glass-specific notes
├── 03-operations/              ← per-op detailed docs (inherit from foundry)
├── 04-regimes.md               ← what c/s/k/r mean for spin-glass trajectories
├── 05-ledger.md                ← Φ accounting in glass-substrate units (energy budget, MC sweep cost)
├── 06-experiments.md           ← designing/running/interpreting glass experiments
├── 07-arbiters.md              ← (probably not needed for glass substrate; placeholder)
├── 08-substrates.md            ← Edwards-Anderson, kinetically-constrained, structural glass options
├── 09-discoveries.md           ← LIVE — the most important file
├── 10-glossary.md              ← terms + symbols (will need substantial glass-physics additions)
├── 11-meta-ledger.md           ← inherit from foundry; the Compression Axiom test on glass-substrate cluster digests is the natural follow-up
├── 12-glass-primer.md          ← NEW: glass aging for MPC operators
└── 13-mpc-primer.md            ← NEW: MPC for glass-physics operators
```

The two primer chapters are doing serious cross-pollination work. Whoever writes them needs to be careful about the audience.

## Reading order

For someone who knows MPC and is new to glass physics: project README → [09-discoveries.md](09-discoveries.md) → 12-glass-primer (when written) → 03-operations/ inherited from foundry → 06-experiments.

For someone who knows glass physics and is new to MPC: [09-discoveries.md](09-discoveries.md) → 13-mpc-primer (when written) → project README → 04-regimes → v6 MPC paper (in `mpc-quantum/docs/`) for the framework.

The discoveries log is the entry point in both cases because it captures the project's strongest non-obvious claim (MPC's s-regime FDR shape transfers to glass aging) in one document.
