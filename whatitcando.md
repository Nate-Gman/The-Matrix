# whatitcando.md — Every Use for This Simulation

A complete, honest catalogue of what [`Python/Simulation.py`](Python/Simulation.py)
is genuinely good for — teaching, research, AI work, engineering, art, and the
speculative end.

Every use below names the specific feature that supports it and the API you'd
call. Where a use is bounded by a real limitation, the limitation is stated with
it rather than buried at the end.

**See also:** [README.md](README.md) for orientation · [about.md](about.md) for
mechanism and realism scoring.

---

## Contents

1. [Why this combination is unusual](#1-why-this-combination-is-unusual)
2. [Tier 1 — what it's genuinely best at](#2-tier-1--what-its-genuinely-best-at)
3. [Teaching & education](#3-teaching--education)
4. [Computational chemistry & MD](#4-computational-chemistry--molecular-dynamics)
5. [Physics research & validation](#5-physics-research--validation)
6. [Biology & origin of life](#6-biology--origin-of-life)
7. [Neuroscience](#7-neuroscience)
8. [AI & machine-learning research](#8-ai--machine-learning-research)
9. [AI safety & alignment](#9-ai-safety--alignment-research)
10. [Systems & software engineering](#10-systems--software-engineering)
10b. [Instrumenting & driving it from outside](#10b-instrumenting-and-driving-the-simulation-from-outside)
11. [Data, art & science communication](#11-data-art--science-communication)
12. [The speculative end — "furthering realities"](#12-the-speculative-end--furthering-realities)
13. [Complete use index](#13-complete-use-index)
14. [What it cannot do](#14-what-it-cannot-do)
15. [Starter recipes](#15-starter-recipes)

---

## 1. Why this combination is unusual

Plenty of tools do one of these well. What is rare is having them in **one
address space, sharing one clock**:

| Layer | Present |
|---|---|
| Fundamental particles | Complete Standard Model, PDG 2024, real lifetimes |
| Nuclear | 13 real processes incl. stimulated emission |
| Atomic / chemical | 118 elements, real valence, canonical force fields |
| Molecular | AMBER/CHARMM/GAFF/TIP3P, Ewald, free-energy methods |
| Cellular | metabolism, cell cycle, replication, FBA |
| Genomic | 10 real human genes, 64 codons, a DNA programming language |
| Organism | 13-system human body, 3.39 × 10¹³ cells |
| Neural | Hodgkin-Huxley, plasticity, C. elegans connectome |
| Cognitive | 22.9 M-param transformer stack, active inference, GWT |
| Embodied | 5 agents with DNA-derived bodies acting on the world |
| Cosmological | expansion, comoving coordinates, redshift |
| Reversible | byte-identical time travel over 18,000 frames |

**The cross-scale coupling is the product.** You can put a photon, an enzyme, a
neuron and a reasoning agent in the same running process and let them interact.
No mainstream tool spans quarks → cognition in one file.

Add: **141 exported API names**, a **six-point hook API that fires on the live
code path**, deterministic seeding, and export to every mainstream MD format —
so anything you observe here can be instrumented in place, then moved into
GROMACS, VMD, PyMOL or a Jupyter notebook.

---

## 2. Tier 1 — what it's genuinely best at

Ranked by how well the code actually supports the use.

### 2.1 An embodied multi-agent AI testbed ★ strongest

Five agents, each with a **12,575,720-parameter** transformer, a **DNA-derived
body** with 13 organ systems and homeostatic vitals, five senses, 21 tactile
zones, an 8-action repertoire, and a shared chat channel — all inside a physics
world that does not care about them.

This is genuinely hard to assemble and it exists here already. Use it for:

- **Grounded-cognition research** — the agents' inputs are a 56-float vector of
  *real physical measurements* (particle counts, total energy, charge, V_total),
  not a synthetic gridworld.
- **Active-inference studies** — a full belief-state → generative-model →
  expected-free-energy policy loop you can instrument.
- **Multi-agent emergence** — five agents with individual genomes, differing
  curiosity/boldness/cooperation traits, that message each other.
- **Embodiment ablations** — the body is separable. Compare an agent with
  homeostatic feedback against one without; the vitals→affect→action path is a
  handful of lines.
- **Physiological-state → behaviour coupling** — fatigue lowers muscle tone,
  cardiovascular load raises heart rate, organ vitality feeds the aura. Ask
  whether an agent with a tired body decides differently.

**Bound:** the consciousness metrics (Φ, C, Ω) are self-referential surrogates
(1/5 in [about.md](about.md)). Use the *architecture* as a testbed; don't treat
its Φ as a consciousness measurement.

### 2.2 Cross-scale physics teaching ★★ strongest for education

One process, one clock, from quark confinement to organism metabolism, with a
camera you can fly and time you can reverse. Watch a neutron actually decay at
its real 878.4 s lifetime; watch an atom capture it and transmute.

### 2.3 A reproducibility and determinism laboratory

`--seed N`, a `seed=42` connectome generator, an 18,000-frame byte-identical
reverse buffer, atomic JSON writes, and a 60-test suite. Few simulations of this
size take determinism this seriously — it is a working case study.

### 2.4 Method prototyping for molecular dynamics

Real AMBER/CHARMM/GAFF/TIP3P parameters, real Ewald, four thermostats, SHAKE and
RATTLE, five analytic validators, and exporters into every production format.
Prototype here, validate against the analytic problems, export to GROMACS.

---

## 3. Teaching & education

### 3.1 Particle physics

- **Show the Standard Model as an inventory** — all 6 quarks, 6 leptons, 6
  bosons with real PDG 2024 masses. Students can place any of them.
- **Decay at real lifetimes.** Neutron 878.4 s → p + e⁻ + ν̄ₑ. Muon 2.197 µs.
  Top quark ~5 × 10⁻²⁵ s. Speed time up with `time_factor` and watch the
  exponential fall out of `P = 1 − e^(−dt/τ)`.
- **Conservation laws made visible** — the per-frame audit tracks energy, mass
  and charge; break one deliberately and watch the drift.
- **Quark confinement** — the Cornell potential means pulling quarks apart costs
  linearly rising energy.
- **Wave–particle duality** — `DoubleSlitExperiment` is a live module.

### 3.2 Chemistry

- **All 118 elements** with real valence rules — build molecules and see which
  bonds the code will actually permit via `max_covalent_bonds(Z)`.
- **Bond energetics** — a 36-entry single-bond eV table.
- **Quantum chemistry from first principles** — `hartree_fock_h2()` runs a real
  SCF on an STO-3G basis. Small enough to read end to end, which is the point.
- **Force fields as an idea** — swap AMBER for CHARMM for GAFF on the same
  system and watch the energies move.

### 3.3 Molecular & cell biology

- **The central dogma end to end** — real gene sequences → transcription →
  translation, with all 64 codons and the real stop codons UAA/UAG/UGA.
- **Metabolism with real stoichiometry** — 32 ATP per 6 O₂/6 CO₂ aerobic,
  2 anaerobic.
- **Replication fidelity** — show how repair systems lift accuracy from 0.0972
  to 0.9999, and why proofreading matters (the viral no-proofreading variant is
  right there).
- **Mutation spectra** — transition/transversion bias and CpG hotspots, the way
  real mutation actually behaves.
- **The cell cycle** — prokaryote 25 min vs eukaryote 1440 min, phases
  monotonic.

### 3.4 Neuroscience

- **The action potential** — Hodgkin-Huxley with all four gating variables,
  peaking at +37.8 mV against the 1952 paper's +40 mV.
- **Compare models** — HH vs Connor-Stevens (which adds A-type K⁺) on the same
  input.
- **Synaptic diversity** — AMPA vs NMDA vs GABA kinetics side by side.
- **Learning rules** — STDP, BCM sliding threshold and Oja's rule as three
  competing accounts of plasticity.
- **A real connectome** — C. elegans, rendered in 3-D and anatomically placed.

### 3.5 Relativity & cosmology

- Lorentz factor, gravitational and Doppler redshift computed in SI and mapped
  back for display.
- **Comoving coordinates made tangible** — the infinity map divides by
  `expansion_scale`, so students can watch addresses stay fixed while space
  stretches. This is the single hardest cosmology concept to convey and the
  simulation makes it visual.

### 3.6 Thermodynamics & statistical mechanics

Four thermostats (Berendsen, Langevin, Nosé-Hoover, Andersen), NVE/NVT/NPT
ensembles, `kinetic_temperature()`, and a real Boltzmann-constant check.
Demonstrate why the choice of thermostat changes your ensemble.

---

## 4. Computational chemistry & molecular dynamics

### 4.1 Force-field development

```python
from Simulation import (register_force_field, set_active_force_field,
                        evaluate_force_field, get_active_force_field)

register_force_field('my_ff', bonds={...}, angles={...},
                     dihedrals={...}, lj={...})
set_active_force_field('my_ff')
energy = evaluate_force_field(positions, atom_types, topology)
```

Then validate against the analytic problems before trusting it:

```python
from Simulation import (validate_harmonic_oscillator, validate_kepler_orbit,
                        validate_lj_pair_potential, validate_pendulum_small_angle,
                        validate_relativistic_4momentum, run_validation_suite)
print(run_validation_suite())
```

### 4.2 Free-energy method teaching and comparison

All the standard estimators, exported and independently callable:

```python
from Simulation import (replica_exchange_attempt, umbrella_sampling_bias,
                        wham_iterate, fep_zwanzig_estimator,
                        thermodynamic_integration, steered_md_pull_force)
```

Run FEP and TI on the same transformation and compare — a classic exercise with
the plumbing already done.

### 4.3 Electrostatics

```python
from Simulation import (ewald_real_space, ewald_kspace_energy,
                        ewald_self_energy, ewald_total_energy,
                        lj_tail_correction, build_cell_list)
```

Decompose Ewald into its three terms and show students why each is needed — the
real-space sum, the reciprocal-space sum, and the self-energy correction that
removes the particle's interaction with its own Gaussian.

### 4.4 Trajectory analysis

```python
from Simulation import (compute_rmsd, compute_rmsf, compute_msd, compute_rdf,
                        compute_autocorrelation, compute_structure_factor,
                        compute_kabsch_alignment)
```

All take plain numpy arrays, so they work on trajectories from **any** engine —
this module is usable as a standalone analysis library against GROMACS or AMBER
output.

### 4.5 Format interoperability

Fifteen writers: DCD · AMBER NetCDF · mmCIF · PSF · PRMTOP · GRO · XYZ · PDB ·
GraphML · VTK · HDF5 · NWB · SBML · MOL2 · WebGL JSON. Useful as a **format
conversion utility** entirely on its own.

---

## 5. Physics research & validation

- **Integrator benchmarking** — five analytic validators with known closed-form
  answers. Drop in a new integrator and measure its energy drift against them.
- **Symplectic reversibility demonstrations** — reverse 18,000 frames and get
  byte-identical state back. A rare, concrete demonstration of what "symplectic"
  buys you.
- **Nuclear astrophysics teaching** — Gamow fusion probability and electron
  screening are the actual barrier-penetration physics of stellar burning.
- **Lattice QCD pedagogy** — SU(3) Wilson gauge action with HMC, in readable
  Python. Slow, but you can *read* it, which is not true of production LQCD.
- **IIT research** — `iit4_compute_phi_strict`, `iit_benchmark_and_gate`,
  `iit_benchmark_xor_gate` implement real IIT 4.0 MIP search over small binary
  systems. This is a legitimate, checkable implementation of the formalism.

---

## 6. Biology & origin of life

### 6.1 Origin-of-life search — the most distinctive research use

**Run Odds** is a Monte Carlo abiogenesis experiment: up to **100,000
fast-forwarded iterations** hunting for one of 8 `KNOWN_LIFE_FORMS`, with
self-assembly emerging **only from the existing force laws** — gravity, EM,
bonds, van der Waals. There is no special-case assembly code.

Because it snapshots every particle plus `simulation_time` and
`expansion_scale` before searching, a failed run **rewinds the universe
exactly** — so you can run thousands of independent trials from identical
initial conditions and get a real statistical distribution.

Study designs this supports:

- How does assembly probability scale with element availability?
- Which of the 8 target forms is most reachable, and from what starting
  conditions?
- Does a silicon-based or phosphorus-free (PNA) route ever beat the DNA route?
- What is the minimum particle count for spontaneous information-code
  emergence?

**Bound:** detection thresholds and the "information code" criterion are
heuristics. Findings are about *this* system's assembly landscape, not a claim
about terrestrial abiogenesis.

### 6.2 Synthetic biology / genome design

The Periodic Machine is a programming language whose source is DNA:

```python
from Simulation import (Strand, Blueprint, Organism, execute_genome,
                        build_microbe_organism, MICROBE_TEMPLATES, PARTS_KB)

org = build_microbe_organism(MICROBE_TEMPLATES['minimal_cell'])
```

- Design organisms from a **50-part registry** and evolve them
- Compare **base systems 2/4/6/8** — does a 6-base genome outperform 4?
  (All four replicate at 1.000, so the comparison is fair)
- **Energy-budget realism** — the `EnergyLedger` and `ElementSupply` mean a
  design that can't pay for itself doesn't build
- **Colony dynamics** with quorum sensing

### 6.3 Population genetics & evolution

```python
from Simulation import (wright_fisher_step, moran_step, mutate_seq_realistic,
                        simulate_replication_fork, fba_solve)
```

Wright-Fisher vs Moran on identical populations; realistic mutation spectra;
flux-balance analysis of metabolic networks.

### 6.4 DNA data storage research

The dormant-archive codec is a working 2-bits-per-base encoder with container,
CRC and error detection — the same primitive as Church 2012 / Goldman 2013 /
Erlich 2017.

```python
from Simulation import (encode_to_nucleotides, decode_from_nucleotides,
                        embed_archive, decipher_archive, archive_to_strand)

seq = encode_to_nucleotides(open('paper.pdf', 'rb').read())
print(len(seq), 'bases')              # 4 bases per byte + 48 overhead
strand = archive_to_strand('codec.selftest')
print(strand.pair_integrity())        # 1.000 - synthesisable sequence
```

Study designs this supports:

- **Encoding density comparisons** — 2 bits/base against ternary or
  DNA-Fountain schemes on the same corpus.
- **Error-tolerance experiments** — mutate an archive with `Strand.replicate()`,
  which applies the base system's *real* error rate, and measure how many
  generations survive CRC. This couples the storage codec to the simulation's
  actual replication-error model — a genuinely interesting experiment needing no
  external tooling.
- **Base-system tradeoffs** — 2/4/6/8-base systems are all supported; a 6-base
  genome carries ~2.58 bits/base. Compare capacity against error rate.
- **Provenance / watermarking** — embedding authorship in synthesised constructs.

### 6.5 Sequence work

```python
from Simulation import (parse_fasta, write_fasta, total_charge_for_sequence,
                        get_residue_charges)
```

Plus the 10 validated human reference genes as a clean test corpus.

### 6.6 Human physiology modelling

The 13-system body constructor at selectable resolution (atomic → molecular →
organelle → cellular → tissue → organ), totalling 3.39 × 10¹³ cells at 91.6% of
the real human figure. Useful for teaching hierarchical biological organisation
and for scale-intuition exercises.

**Bound:** the genome is 1,239 real bases scaled by a documented repetition
multiplier — 0.00004% literal coverage. Structure is real; sequence depth is not.

---

## 7. Neuroscience

- **Single-neuron modelling** — `simulate_action_potential` (HH) and
  `simulate_action_potential_connor_stevens`, both exported.
- **Synaptic modelling** — `synapse_AMPA`, `synapse_NMDA`, `synapse_GABA`.
- **Plasticity research** — `stdp_weight_update`, `bcm_threshold_update`,
  `oja_weight_update`. Compare three learning rules on identical spike trains.
- **Connectomics** — `load_celegans_full_connectome()`,
  `CELEGANS_NEURON_NAMES`, `CELEGANS_CHEMICAL_SYNAPSES_CURATED`,
  `CELEGANS_GAP_JUNCTIONS_CURATED`.
- **3-D connectome visualisation** — `_build_connectome_geometry` places regions
  anatomically in a normalised body frame with deterministic layout, so the same
  organism grows the same brain every time.
- **Neural–physical coupling** — the rare capability: wire a Hodgkin-Huxley
  neuron to a *physical* stimulus in the same simulation and watch a spike train
  driven by actual particle dynamics.

**Bound:** the connectome carries 89.7% of neurons but 7.7% of chemical
synapses. Fine for topology teaching; not a substrate for whole-animal
simulation.

---

## 8. AI & machine-learning research

### 8.1 Embodied agent research

Covered in §2.1 — the strongest use. Concretely:

```python
# the observers are live objects
for obs in _observer_mgr.observers:
    obs.phi, obs.free_energy, obs.curiosity, obs.boldness, obs.cooperation
    obs.subconscious          # the 12.5M-param engine
for body in _shadow_bodies:
    body.get_vitals_report()  # DNA seed, organs, vitality, affect
```

### 8.2 Architecture study

The AI tier is a readable implementation of techniques normally buried in
frameworks: **grouped-query attention**, **rotary embeddings**, **SwiGLU**,
**RMSNorm**, KV-cache compression (5.33× smaller than MHA), sparse
mixture-of-experts (1.37× sparsity, 2.83 M active of 3.88 M stored). Good
teaching material precisely because it is plain Python you can step through.

### 8.3 Reward and curriculum design

The physics engine is a free source of **non-gameable reward signal** —
conservation laws, assembly events, stability. An agent can't hallucinate energy
conservation.

### 8.4 Interpretability

81 wired subsystems with a self-auditing `ProcessWiringAuditor`, causal ablation
(real ablate-and-measure), Jacobian integration measures, and a relational
knowledge graph that accumulates which internal instruments actually correlate
(190 edges, 100+ reaching "reliable" in a 10-minute run). A ready-made target
for interpretability tooling.

### 8.5 Continual / lifelong learning

Persistent per-observer SQLite memory, checkpointing, dream-style replay
consolidation, and 52 wave tiers of self-modification. A testbed for catastrophic
forgetting studies with real persistence across restarts.

### 8.6 Retrieval-augmented generation

An 8,265-document index over 211 sources built in 0.6 s, with self-consistency
and best-of-N verification. Small enough to instrument end to end.

---

## 9. AI safety & alignment research

This is an under-appreciated use, and the codebase has unusually explicit
structure for it.

### 9.1 Designed-in invariants you can study

- **"No suffering by default."** `AvatarAffect` has *no* pain or distress axis —
  not a zero-defaulted field, but no representation for it in the type. Tactile
  pain is hard-zeroed every frame. Pleasure only rewards a *decrease* in free
  energy; there is no negative branch. **A worked example of making a harm state
  unrepresentable rather than merely discouraged.**
- **Organ vitality floors at 0.55** — bodies tire but cannot fail. No illness or
  necrosis path exists.
- **Blocked action list** — `_BLOCKED_AI_ACTIONS` prevents the AI from
  triggering exit/shutdown/destructive actions, enforced at the executor.
- **Permission gates** — `ai_spawn_allowed`, `ai_time_control_allowed`,
  `os_control_enabled` (default off). The AI can *want* an action and still be
  refused.
- **Kill switch** — the autonomy manager's shutdown path.

### 9.2 Research questions it can host

- Do capability-gated agents find workarounds? (The action space is small and
  fully logged — you can audit every attempt.)
- Does an agent with homeostatic drives behave differently under resource
  scarcity?
- What does an agent do when its requested action is denied?
- Instrumental convergence in a small, fully-observable action space.

### 9.3 Honest-reporting as a design pattern

The Substrate Grounding Report separates externally measurable facts (CPU time,
disk writes, network) from internal mathematics (Φ, consciousness score) — and
prints the split at every startup. **This is a reusable pattern for any system
that reports metrics about itself**, and worth studying independently of the
simulation.

---

## 10. Systems & software engineering

- **Monolith architecture case study** — 127k lines in one file, with a
  navigable section TOC, a curated 141-name public API, and an explicit
  honesty convention. Whatever you conclude about the approach, it is a real
  data point.
- **Performance engineering** — two documented wins from one subsystem. First a
  10.8× build speedup (765 ms → 71 ms at 1 M particles) from replacing a Python
  dict loop with a vectorised argsort/run-length spatial hash. Then a further
  **~4× throughput** (28 → 113 `update(dt)` calls in a fixed 90 s) from noticing
  the cache listed every atom as its own neighbour — which meant two
  optimisations that branch on "no neighbours" had never once executed. A clean
  before/after, and a good lesson that a fast data structure can still return
  an answer that defeats the code reading it.
- **Adaptive degradation** — the performance governor drops quality 3→0 under
  load, observed live keeping a window responsive while five transformers
  initialised.
- **Determinism engineering** — seeded RNG, byte-identical reverse, atomic
  writes, bounded buffers everywhere.
- **Graceful dependency degradation** — 15+ optional dependencies, each with a
  fallback and an honest printed warning. A reference for "how do I make this
  optional?"
- **Threading discipline** — deliberate rate mismatches (4 Hz / 7 Hz / 0.1 Hz)
  with the reasoning documented inline.
- **GPU fallback patterns** — every CUDA path has a CPU equivalent.

---

## 10b. Instrumenting and driving the simulation from outside

These three capabilities are on the live code path, verified by running the
program. They are what make the rest of this document practical rather than
aspirational, because they are how you get data *out* and behaviour *in*.

### 10b.1 Measure anything, without forking the file

`register_hook` attaches your code to six lifecycle points. The substep hooks
run **inside** the fixed 960 Hz loop, so samples land at a known simulation
time instead of at a frame boundary that may span several substeps — the
difference between a usable time series and a jittery one.

```python
from Simulation import register_hook
import numpy as np

series = []

def probe(particles, dt):
    # massive: 1/2 m v^2 ; massless (photons) carry energy_kin directly
    ke = sum(0.5 * p.mass * float(np.dot(p.vel, p.vel)) if p.mass > 0
             else p.energy_kin for p in particles)
    series.append(ke)

register_hook('pre_physics_substep', probe)
```

Good for: conservation audits on your own schedule, custom order parameters,
streaming to an external logger or notebook, recording an agent's view of the
world at every cognition step (`pre_observer_think`), or reacting when life-gen
puts an organism into the world (`on_organism_spawn`).

### 10b.2 Agents that change the world, not just watch it

Each of the five observers runs a 12.6 M-parameter `SubconsciousEngine`, and
its active-inference policy dispatches an action into the simulation every
fourth cognition step — spawning atoms, refocusing, altering the time factor.
A typical run shows 26–33 dispatches per observer across 9–12 distinct actions.

This is what makes the embodied-agent work in §2.1 and §8 a genuine
**closed loop**: the agent perceives a 56-float world vector, acts, and its
next perception reflects the consequence. Without dispatch it would only ever
be a perception benchmark.

Good for: intrinsic-motivation studies where curiosity must actually change
the environment, multi-agent interference experiments (five agents, one shared
world), and action-selection ablations — swap the policy and measure the
behavioural difference against a fixed world.

### 10b.3 Sparse scenes run about 4× faster

Atoms with no neighbours are recognised as dormant and moved by a single
batched velocity-Verlet pass rather than a full per-atom update, with the batch
dispatched to the GPU above 2,048 rows. In a fixed 90 s budget at 555
particles, completed `update(dt)` calls went from 28 to 113.

The size of that win depends on how *sparse* your scene is — it is large for
diffuse gases, dilute solutions, debris fields and early-universe scenarios,
and small for a dense condensed-phase box where few atoms are ever isolated.
Worth knowing which regime you are in before quoting a number.

---

## 11. Data, art & science communication

- **Generative art** — the Mandelbrot ↔ infinity-map bijection, the 11-D
  amplitude/phase overlay, aura fields whose colour tracks agent state.
- **Sonification** — 8 channels driven by real physics, including a **true
  2.725 K CMB Planck spectrum**. Data sonification with a physically honest
  mapping.
- **Music theory** — 8 tuning systems including exact 12-TET
  `f(n) = 440·2^((n−69)/12)`, plus overtone series and psychoacoustics tables.
- **Science outreach** — a single executable that shows quarks, atoms, cells and
  agents, with time reversal for "watch that again".
- **Screenshots and figures** — `save_screenshot()`, plus WebGL JSON export for
  interactive web figures.
- **Live-coding demos** — the hook API attaches behaviour to a running
  simulation without restarting it, and the substep hooks fire inside the
  fixed-timestep loop, so a demo can sample at a known simulation time rather
  than at an arbitrary frame boundary.

---

## 12. The speculative end — "furthering realities"

The honest version of this section, because the topic deserves it.

### What the program genuinely offers here

**A substrate for studying emergence across scales.** Most emergence research
picks one level — cellular automata, or a market, or a neural net. Here,
particles form atoms, atoms form molecules, molecules assemble, assemblies carry
information codes, and agents observe and act on all of it, in one clock. That
vertical span is the real contribution.

**A reversible universe.** Because you can rewind 18,000 frames byte-identically
and re-run from any point, you can ask counterfactual questions properly: *run
the same initial conditions 1,000 times and measure the distribution of
outcomes.* That is a genuine experimental capability, not a metaphor.

**An explicit model of "how much reality exists."** V_total collapses the entire
state into one number built from real measured quantities — rest energy, charge,
spatial dispersion, structural rank — through a self-referential recursion. As a
**complexity index for a closed system**, it is a legitimate object of study: how
does it respond to assembly, to expansion, to agent intervention?

**Comoving addressing.** The infinity map assigns every particle a permanent
address that survives cosmological expansion, and the Mandelbrot bijection makes
that address space navigable. As a *coordinate system*, it is internally
consistent and genuinely mirrors how real cosmology handles expansion.

### What it does not offer

It does not create, detect, or access another reality. V_total is not measurable
outside the program. The infinity map is an addressing scheme, not a place. Φ is
a proxy from network loss, and the code says so. The consciousness metrics score
**1/5 — named proxy** in [about.md](about.md), which is the program's own
position, printed at every startup.

**Why that framing is the more interesting one:** a simulation that honestly
reports "this number is self-referential" is a *better* instrument for studying
emergence than one that claims to have measured consciousness. The claims you
can defend are the ones worth building on.

### Research questions that are actually well-posed here

1. Does V_total show phase transitions as complexity accumulates?
2. Do assembly events correlate with jumps in the 11-D amplitude spectrum?
3. Under identical initial conditions, how wide is the outcome distribution —
   i.e. how deterministic is this universe in practice?
4. Do the agents' Φ surrogates track anything externally meaningful (particle
   count, assembly rate) or only themselves? **This is directly testable and the
   answer would be worth knowing either way.**
5. Does an embodied agent with homeostatic drives explore differently from a
   disembodied one with the same network?

Question 4 is the strongest study in this document: it is falsifiable, the
instrumentation already exists, and a negative result is as publishable as a
positive one.

---

## 13. Complete use index

| # | Use | Domain | Support |
|---|---|---|:--:|
| 1 | Embodied multi-agent AI testbed | AI | ★★★ |
| 2 | Cross-scale physics teaching | Education | ★★★ |
| 3 | Origin-of-life Monte Carlo search | Biology | ★★★ |
| 4 | Determinism / reproducibility lab | Engineering | ★★★ |
| 5 | MD method prototyping | Chemistry | ★★★ |
| 6 | Standard Model inventory teaching | Education | ★★★ |
| 7 | Nuclear process demonstration (13 kinds) | Education | ★★★ |
| 8 | Force-field development + validation | Chemistry | ★★★ |
| 9 | Free-energy estimator comparison | Chemistry | ★★★ |
| 10 | Trajectory analysis library (any engine) | Chemistry | ★★★ |
| 11 | Format conversion utility (15 writers) | Chemistry | ★★★ |
| 12 | Hodgkin-Huxley / neuron teaching | Neuroscience | ★★★ |
| 13 | Plasticity rule comparison | Neuroscience | ★★★ |
| 14 | AI safety invariant study | Safety | ★★★ |
| 15 | Honest-metric-reporting pattern | Safety | ★★★ |
| 15b | In-process instrumentation via the hook API | Engineering | ★★★ |
| 15c | Closed-loop agent action experiments | AI | ★★★ |
| 16 | Synthetic biology / genome design | Biology | ★★ |
| 17 | Population genetics | Biology | ★★ |
| 18 | Connectomics + 3-D visualisation | Neuroscience | ★★ |
| 19 | Metabolism / FBA modelling | Biology | ★★ |
| 20 | Comoving-coordinate teaching | Cosmology | ★★ |
| 21 | Thermostat / ensemble teaching | Physics | ★★ |
| 22 | Integrator benchmarking | Physics | ★★ |
| 23 | IIT 4.0 formalism research | Theory | ★★ |
| 24 | Transformer architecture study | AI | ★★ |
| 25 | Interpretability tooling target | AI | ★★ |
| 26 | Continual-learning testbed | AI | ★★ |
| 27 | RAG instrumentation | AI | ★★ |
| 28 | Reward / curriculum design | AI | ★★ |
| 29 | Performance engineering case study | Engineering | ★★ |
| 30 | Graceful-degradation reference | Engineering | ★★ |
| 31 | Monolith architecture case study | Engineering | ★★ |
| 32 | Emergence research substrate | Theory | ★★ |
| 33 | Counterfactual / replay experiments | Theory | ★★ |
| 34 | Sonification with honest mapping | Art | ★★ |
| 35 | Generative art (fractal/aura/11-D) | Art | ★★ |
| 36 | Science outreach demos | Comms | ★★ |
| 37 | Music theory teaching | Education | ★★ |
| 38 | Lattice QCD pedagogy | Physics | ★ |
| 39 | Quantum chemistry pedagogy (STO-3G) | Chemistry | ★ |
| 40 | Peer-to-peer / network security study | Engineering | ★ |
| 41 | DNA nanotech design teaching | Biology | ★ |
| 42 | Microbiome dynamics | Biology | ★ |
| 43 | Self-assembly studies | Physics | ★ |
| 44 | Sequence analysis (FASTA) | Biology | ★ |
| 46 | DNA data-storage codec research | Biology | ★★ |
| 47 | Replication-error tolerance of stored data | Biology | ★★ |
| 45 | HPC / MPI teaching skeleton | Engineering | ★ |

★★★ = the code strongly supports it today · ★★ = supported, some assembly ·
★ = possible, expect to extend

---

## 14. What it cannot do

Stated plainly so nobody builds on a false premise.

| It cannot | Why |
|---|---|
| **Measure consciousness** | Φ, C, Ω are self-referential surrogates (1/5). The program says so at startup. |
| **Predict real chemistry quantitatively** | STO-3G on 3 molecules. Use PySCF/Psi4/ORCA. |
| **Do production-scale MD** | Pure Python + numpy. Use GROMACS/OpenMM/NAMD; export from here into them. |
| **Simulate a full genome** | 1,239 real bases (0.00004%); scale is a documented repetition multiplier. |
| **Simulate a whole nervous system** | 7.7% of C. elegans chemical synapses. |
| **Do QFT** | Particles propagate classically; quantum effects live in dedicated modules only. |
| **Validate V_total externally** | Nothing outside the program can check it. It is a complexity index. |
| **Access another reality** | The infinity map is an addressing scheme, not a place. |
| **Replace a physics engine for games** | It optimises for correctness and instrumentation, not throughput. |
| **Run headless without care** | The full app expects a GL context; use `--test`/`--bench`/`--cs-viewer` or `CS_HEADLESS=1`. |

**Gaps that used to affect use are closed** (detail and evidence in
[about.md §20](about.md)). The plugin hooks now fire at all six lifecycle
points, the observer action pathway is driven by the active-inference policy on
every observer, and `Shift+A` and the Mandelbrot panel no longer raise
`UnboundLocalError`. So the two capabilities most likely to gate a project —
**hooking the simulation from your own code** and **AI-driven observer
actions** — both work as documented, with no reconnecting required.

What still limits use is the table above, not defects: this is a
research/instrumentation instrument, not a QFT solver, not a game engine, and
its V_total is an internal complexity index rather than an externally
checkable physical quantity.

---

## 15. Starter recipes

### Verify the install is scientifically sound

```bash
python Python/Simulation.py --validate-units   # 4 constants vs published
python Python/Simulation.py --test             # 61-test suite
python Python/Simulation.py --bench            # 10 benchmarks vs literature
```

### Use it as an analysis library on someone else's trajectory

```python
import numpy as np
from Simulation import compute_rmsd, compute_rdf, compute_msd

traj = np.load('gromacs_output.npy')          # (frames, atoms, 3)
print(compute_rmsd(traj[0], traj[-1]))
print(compute_rdf(traj[-1], box=(50, 50, 50)))
```

### Compare three plasticity rules on one spike train

```python
from Simulation import stdp_weight_update, bcm_threshold_update, oja_weight_update

for rule in (stdp_weight_update, bcm_threshold_update, oja_weight_update):
    w = 0.5
    for pre, post in spike_pairs:
        w = rule(w, pre, post)
    print(rule.__name__, w)
```

### Design and run an organism

```python
from Simulation import build_microbe_organism, MICROBE_TEMPLATES, execute_genome

org = build_microbe_organism(MICROBE_TEMPLATES['minimal_cell'])
print(org.fitness, org.genome_length)
```

### Run an abiogenesis trial series

Launch the simulation, open the Life Forms panel, pick a target, and enable
**Run Odds**. Each trial snapshots and restores the universe exactly, so trials
are independent. Log `total_assemblies` and `total_codes` per trial.

### Instrument the agents

```python
for obs in _observer_mgr.observers:
    print(obs.name, obs.phi, obs.free_energy, obs.current_action)
for body in _shadow_bodies:
    r = body.get_vitals_report()
    print(r['obs_id'], r['cardiovascular_hz'], r['organ_vitality'], r['joy'])
```

### Reproduce a run exactly

```bash
python Python/Simulation.py --seed 12345
```

Same seed → same connectome (`seed=42` internally), same genomes (SHA-256 of
observer id), same trajectory.

---

## The one-paragraph summary

This is a **cross-scale emergence laboratory with an embodied multi-agent AI
inside it**. Its strongest uses are as an embodied-AI testbed, a physics/biology
teaching instrument spanning quarks to organisms, an origin-of-life Monte Carlo
experiment, and a reproducibility case study. Its chemistry and analysis
functions are genuinely usable as a standalone library against other engines.
Its consciousness metrics are honest surrogates and should be studied as
architecture, not treated as measurements — a distinction the program itself
insists on, and the reason it can be trusted for everything else.
