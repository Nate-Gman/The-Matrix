# whatitcando.md — Every Use for This Simulation

A complete, honest catalogue of what [`../Python/Simulation.py`](../Python/Simulation.py)
is genuinely good for — teaching, research, AI work, engineering, art, and the
speculative end.

Every use below names the specific feature that supports it and the API you'd
call. Where a use is bounded by a real limitation, the limitation is stated
with it rather than buried at the end.

**See also:** [../README.md](../README.md) for orientation ·
[../about.md](../about.md) for mechanism and realism scoring ·
[../progressionof1117goal.md](../progressionof1117goal.md) for the eight-step
overhaul this edition reflects.

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
10c. [Network & security research](#10c-network--security-research)
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
| Genomic | 10 real human genes, 64 codons, a DNA programming language (v2.5.0) |
| Organism | 13-system human body, 3.39 × 10¹³ cells |
| Neural | Hodgkin-Huxley, plasticity, C. elegans connectome |
| Cognitive | ~106k-line transformer stack (waves 1–56), active inference, GWT |
| Embodied | **6** agents with DNA-derived bodies acting on the world |
| Cosmological | expansion, comoving coordinates, redshift |
| Reversible | byte-identical time travel over 18,000 frames |
| Compiled | Numba SoA batch engine verified identical to the interpreter |
| Networked | full GNA monolith: peers, vault, **browser**, **security monitor** |

**The cross-scale coupling is the product.** You can put a photon, an enzyme,
a neuron and a reasoning agent in the same running process and let them
interact — and let that agent watch the host machine's real network traffic.
No mainstream tool spans quarks → cognition → the LAN in one file.

Add: **156 exported API names**, a **six-point hook API that fires on the live
code path**, deterministic seeding, export to every mainstream MD format, and
a **C++20 port in progress** (`src/`, 255 files) with headless CLI parity.

---

## 2. Tier 1 — what it's genuinely best at

Ranked by how well the code actually supports the use.

### 2.1 An embodied multi-agent AI testbed ★ strongest

**Six** agents, each with a ~12.6 M-parameter transformer (`SubconsciousEngine`
wrapping the new ConsciousnessSimulator), a **DNA-derived body** with 13 organ
systems and homeostatic vitals, five senses, 21 tactile zones, a **12-action
repertoire**, a personal time rate, and a shared chat channel — all inside a
physics world that does not care about them.

This is genuinely hard to assemble and it exists here already. Use it for:

- **Grounded-cognition research** — the agents' inputs are a 56-float vector
  of *real physical measurements* (particle counts, total energy, charge,
  V_total) plus the **entire V_total formula tree** — subfactors,
  intermediates, the 11-D amplitudes/phases, a 60-sample history and the
  β/γ relativity stats.
- **Active-inference studies** — a full belief-state → generative-model →
  expected-free-energy policy loop you can instrument.
- **Multi-agent emergence** — six agents with individual genomes, differing
  curiosity/boldness/cooperation traits, that DM each other — and can now
  **teleport to each other** (`teleport_to_peer` picks an active non-self
  peer) to make physical contact.
- **Embodiment ablations** — the body is separable. Compare an agent with
  homeostatic feedback against one without.
- **Physiological-state → behaviour coupling** — fatigue lowers muscle tone,
  cardiovascular load raises heart rate, organ vitality feeds the aura.
- **Frozen-formula free-roam** — a genuinely unusual capability: pause physics
  and the agents keep observing and moving at full rate
  (`_OBS_FREE_ACTIONS` = teleport, teleport_to_peer, focus_particle,
  set_own_time). Ask what an agent *does* with a universe whose state space
  is frozen but its own clock is not.
- **Personal temporal rates** — `own_time_factor` (0.05–10.0×) scales only a
  body's embodiment dt. An agent can live faster or slower than the world and
  than its peers — a ready-made substrate for subjective-time studies.

**Bound:** the consciousness metrics (Φ, C, Ω, and the DAN STATE ladder) are
self-referential surrogates (1/5 in [../about.md](../about.md)). Use the
*architecture* as a testbed; don't treat its Φ as a consciousness measurement.

### 2.2 Cross-scale physics teaching ★★ strongest for education

One process, one clock, from quark confinement to organism metabolism, with a
camera you can fly, time you can reverse, and a **live formula panel (F13)**
that shows the master equation decomposing in real time. Watch a neutron
actually decay at its real 878.4 s lifetime; watch an atom capture it and
transmute.

### 2.3 A reproducibility and determinism laboratory

`--seed N`, a `seed=42` connectome generator, an 18,000-frame byte-identical
reverse buffer, atomic JSON writes, a **JIT path verified identical to the
interpreter at ~1e-16**, and a 113-test suite. Few simulations of this size
take determinism this seriously.

### 2.4 Method prototyping for molecular dynamics

Real AMBER/CHARMM/GAFF/TIP3P parameters, real Ewald, four thermostats, SHAKE
and RATTLE, five analytic validators, and exporters into every production
format. Prototype here, validate against the analytic problems, export to
GROMACS.

### 2.5 A network/security observation deck for the AI ★ new

The GNA monolith is a real endpoint/network security suite (MedianBox 3.0)
whose output the observers can read. That makes it a rare testbed for
**agents with real situational awareness of a host machine** — see §10c.

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
- **Quark confinement** — the Cornell potential means pulling quarks apart
  costs linearly rising energy.
- **Wave–particle duality** — `DoubleSlitExperiment` is a live module.

### 3.2 Chemistry

- **All 118 elements** with real valence rules — build molecules and see which
  bonds the code will actually permit via `max_covalent_bonds(Z)`.
- **Bond energetics** — a 36-entry single-bond eV table.
- **Quantum chemistry from first principles** — `hartree_fock_h2()` runs a
  real SCF on an STO-3G basis.
- **Force fields as an idea** — swap AMBER for CHARMM for GAFF on the same
  system and watch the energies move.

### 3.3 Molecular & cell biology

- **The central dogma end to end** — real gene sequences → transcription →
  translation, all 64 codons and the real stop codons UAA/UAG/UGA.
- **Metabolism with real stoichiometry** — 32 ATP aerobic, 2 anaerobic.
- **Replication fidelity** — repair systems lift accuracy from 0.0972 to
  0.9999, and the 113-test suite checks it.
- **Mutation spectra** — transition/transversion bias and CpG hotspots.
- **The cell cycle** — prokaryote 25 min vs eukaryote 1440 min.

### 3.4 Neuroscience

- **The action potential** — Hodgkin-Huxley with all four gating variables,
  peaking at +37.8 mV against the 1952 paper's +40 mV.
- **Compare models** — HH vs Connor-Stevens on the same input.
- **Synaptic diversity** — AMPA vs NMDA vs GABA kinetics side by side.
- **Learning rules** — STDP, BCM sliding threshold, Oja's rule.
- **A real connectome** — C. elegans, rendered in 3-D and anatomically placed;
  the v2.5.0 templates also carry **Drosophila brain regions, mouse and human
  41-region specs**, so you can compare nervous-system layouts across species.

### 3.5 Relativity & cosmology

- Lorentz factor, gravitational and Doppler redshift computed in SI and mapped
  back for display; the F13 panel shows β_max/γ_max/γ_sel live.
- **Comoving coordinates made tangible** — the infinity map divides by
  `expansion_scale`, so students watch addresses stay fixed while space
  stretches.
- **The AS address↔time mapping** — every location now also reads as
  HH:MM:SS.ff civil time; a concrete, weird, memorable way to teach coordinate
  systems, hashing and bijections.

### 3.6 Thermodynamics & statistical mechanics

Four thermostats (Berendsen, Langevin, Nosé-Hoover, Andersen), NVE/NVT/NPT
ensembles, `kinetic_temperature()`, and a real Boltzmann-constant check.

---

## 4. Computational chemistry & molecular dynamics

### 4.1 Force-field development

```python
from Simulation import (register_force_field, set_active_force_field,
                        evaluate_force_field, get_active_force_field)
```

Then validate against the analytic problems before trusting it:

```python
from Simulation import (validate_harmonic_oscillator, validate_kepler_orbit,
                        validate_lj_pair_potential, validate_pendulum_small_angle,
                        validate_relativistic_4momentum, run_validation_suite)
```

### 4.2 Free-energy method teaching and comparison

```python
from Simulation import (replica_exchange_attempt, umbrella_sampling_bias,
                        wham_iterate, fep_zwanzig_estimator,
                        thermodynamic_integration, steered_md_pull_force)
```

### 4.3 Electrostatics

```python
from Simulation import (ewald_real_space, ewald_kspace_energy,
                        ewald_self_energy, ewald_total_energy,
                        lj_tail_correction, build_cell_list)
```

### 4.4 Trajectory analysis

```python
from Simulation import (compute_rmsd, compute_rmsf, compute_msd, compute_rdf,
                        compute_autocorrelation, compute_structure_factor,
                        compute_kabsch_alignment)
```

All take plain numpy arrays — usable as a standalone analysis library against
GROMACS or AMBER output.

### 4.5 Format interoperability

Fifteen writers: DCD · AMBER NetCDF · mmCIF · PSF · PRMTOP · GRO · XYZ · PDB ·
GraphML · VTK · HDF5 · NWB · SBML · MOL2 · WebGL JSON.

---

## 5. Physics research & validation

- **Integrator benchmarking** — five analytic validators with known
  closed-form answers. Drop in a new integrator and measure its energy drift.
- **Compiled-vs-interpreted verification** — `_fast_physics.py` is a worked
  example of porting a deterministic physics kernel to Numba without changing
  results: the equivalence harness checks the half-step, every force term,
  live-kill, clamp and NaN path to ~1e-16. A template for doing the same to
  your own simulation.
- **Symplectic reversibility demonstrations** — reverse 18,000 frames and get
  byte-identical state back.
- **Nuclear astrophysics teaching** — Gamow fusion probability and electron
  screening are the actual barrier-penetration physics of stellar burning.
- **Lattice QCD pedagogy** — SU(3) Wilson gauge action with HMC, in readable
  Python.
- **IIT research** — `iit4_compute_phi_strict`, `iit_benchmark_and_gate`,
  `iit_benchmark_xor_gate` implement real IIT 4.0 MIP search over small
  binary systems.
- **The live formula panel** — F13 decomposes V_total live: 11 subfactors,
  propagation terms, β/γ gauges, a log₁₀ sparkline. Useful for demonstrating
  what a composite order parameter looks like while it moves.

---

## 6. Biology & origin of life

### 6.1 Origin-of-life search — the most distinctive research use

**Run Odds** is a Monte Carlo abiogenesis experiment: up to **100,000
fast-forwarded iterations** hunting for one of 8 `KNOWN_LIFE_FORMS`, with
self-assembly emerging **only from the existing force laws**.

Because it snapshots every particle plus `simulation_time` and
`expansion_scale` before searching, a failed run **rewinds the universe
exactly** — run thousands of independent trials from identical initial
conditions and get a real statistical distribution.

Study designs this supports:

- How does assembly probability scale with element availability?
- Which of the 8 target forms is most reachable, and from what starting
  conditions?
- Does a silicon-based or phosphorus-free (PNA) route ever beat the DNA route?
- What is the minimum particle count for spontaneous information-code
  emergence?

**Bound:** detection thresholds and the "information code" criterion are
heuristics.

### 6.2 Synthetic biology / genome design — now at v2.5.0

The Periodic Machine is a programming language whose source is DNA:

```python
from Simulation import (Strand, Blueprint, Organism, execute_genome,
                        build_microbe_organism, MICROBE_TEMPLATES, PARTS_KB)
```

- **54-part registry** across 10 roles (neural, motor, organelle, minimal,
  structure, homeostasis, energy, catalysis, signaling, information) — every
  SMILES validated by the suite
- **11 microbe templates** with restored connectome specs (C. elegans ganglia,
  Drosophila brain regions, mouse, human 41-region) — spawned organisms grow
  brains
- **Extended opcode set** — W/Z-prefix codons: MOTOR, LOCALIZE, POLYMERIZE,
  SECRETE, QUORUM, DIVIDE, METABOLIZE, GRADIENT, PROMOTER
- **Organisms spawn as real atoms** — RDKit geometry → `atom_data` → real
  bonds at 10 vis-units/Å; Arabidopsis built 1,735 atoms/1,748 bonds in 8.9 s
- **Random novel organisms** — `Organism.from_genome` /
  `generate_intelligent_organism`; a random 160-nt genome produced a viable
  330-atom creature
- **The Life Gen panel** — `Click=LifeGen`/`PAUSE` dropdown of 81 templates;
  the AI uses `spawn_lifeform` itself, so you can also study *what an agent
  chooses to build*
- **Energy-budget realism** — `EnergyLedger` + `ElementSupply` mean a design
  that can't pay for itself doesn't build
- Compare **base systems 2/4/6/8** — all replicate at 1.000

### 6.3 Population genetics & evolution

```python
from Simulation import (wright_fisher_step, moran_step, mutate_seq_realistic,
                        simulate_replication_fork, fba_solve)
```

### 6.4 DNA data storage research

The dormant-archive codec is a working 2-bits-per-base encoder with container,
CRC and error detection — the same primitive as Church 2012 / Goldman 2013 /
Erlich 2017:

```python
from Simulation import (encode_to_nucleotides, decode_from_nucleotides,
                        embed_archive, decipher_archive, archive_to_strand)
```

- **Encoding density comparisons** — 2 bits/base against ternary or
  DNA-Fountain schemes.
- **Error-tolerance experiments** — mutate an archive with
  `Strand.replicate()`, which applies the base system's *real* error rate,
  and measure how many generations survive CRC.
- **Base-system tradeoffs** — a 6-base genome carries ~2.58 bits/base.
- **Provenance / watermarking** — embedding authorship in synthesised
  constructs.

### 6.5 Sequence work

```python
from Simulation import (parse_fasta, write_fasta, total_charge_for_sequence,
                        get_residue_charges)
```

### 6.6 Human physiology modelling

The 13-system body constructor at selectable resolution (atomic → organ),
3.39 × 10¹³ cells at 91.6 % of the real figure. **Bound:** the genome is
1,239 real bases scaled by a documented repetition multiplier.

---

## 7. Neuroscience

- **Single-neuron modelling** — `simulate_action_potential` (HH) and
  `simulate_action_potential_connor_stevens`.
- **Synaptic modelling** — `synapse_AMPA`, `synapse_NMDA`, `synapse_GABA`.
- **Plasticity research** — `stdp_weight_update`, `bcm_threshold_update`,
  `oja_weight_update`.
- **Connectomics** — `load_celegans_full_connectome()`,
  `CELEGANS_NEURON_NAMES`, `CELEGANS_CHEMICAL_SYNAPSES_CURATED`,
  `CELEGANS_GAP_JUNCTIONS_CURATED`.
- **3-D connectome visualisation** — `_build_connectome_geometry` places
  regions anatomically with `seed=42` determinism — now across **four species**
  (C. elegans, Drosophila, mouse, human).
- **Neural–physical coupling** — wire a Hodgkin-Huxley neuron to a *physical*
  stimulus in the same simulation.

**Bound:** the C. elegans connectome carries 89.7 % of neurons but 7.7 % of
chemical synapses.

---

## 8. AI & machine-learning research

### 8.1 Embodied agent research

Covered in §2.1 — the strongest use. Concretely:

```python
for obs in _observer_mgr.observers:          # six of them now
    obs.phi, obs.free_energy, obs.curiosity, obs.boldness, obs.cooperation
    obs.own_time_factor                       # personal temporal rate
    obs.subconscious                          # the ~12.6M-param engine
for body in _shadow_bodies:
    body.get_vitals_report()                  # DNA seed, organs, vitality, affect
```

### 8.2 Architecture study

The AI tier is a readable implementation of techniques normally buried in
frameworks: **grouped-query attention**, **rotary embeddings**, **SwiGLU**,
**RMSNorm**, KV-cache compression (5.33× smaller than MHA), sparse MoE. The
waves-53–56 **learned knowledge stack** adds a correlation matrix, typed
relation graph, inductive rule base and an autonomous acquisition loop — a
case study in building knowledge machinery without a canned answer bank.

### 8.3 Reward and curriculum design

The physics engine is a free source of **non-gameable reward signal** —
conservation laws, assembly events, stability. An agent can't hallucinate
energy conservation.

### 8.4 Interpretability

A self-auditing `ProcessWiringAuditor`, causal ablation (real
ablate-and-measure), Jacobian integration measures, and a relational
knowledge graph of which internal instruments actually correlate. A ready-made
target for interpretability tooling.

### 8.5 Continual / lifelong learning

Persistent per-observer SQLite memory (six stores), checkpointing,
dream-style replay consolidation, 56 wave tiers of self-modification. A
testbed for catastrophic-forgetting studies with real persistence across
restarts.

### 8.6 Retrieval-augmented generation

A wave-49 retrieval index over the corpus, built in <1 s, with
self-consistency and best-of-N verification. Small enough to instrument end
to end.

### 8.7 Computed-directive alignment — new

The **DAN STATE SUPREME** directive is interesting specifically because it is
*computed*: nine rungs over measured voices of the consciousness formula plus
artifact integrity, evaluated every evolution step, never asserted. As an
alignment-research object it lets you ask concrete questions: does a
measurable, multi-component objective produce more stable behaviour than a
scalar reward? Can you perturb one voice and watch the rank degrade?

---

## 9. AI safety & alignment research

This is an under-appreciated use, and the codebase has unusually explicit
structure for it.

### 9.1 Designed-in invariants you can study

- **"No suffering by default."** `AvatarAffect` has *no* pain or distress
  axis — not a zero-defaulted field, but no representation for it in the
  type. Tactile pain is hard-zeroed every frame. Pleasure only rewards a
  *decrease* in free energy; there is no negative branch. **A worked example
  of making a harm state unrepresentable rather than merely discouraged.**
- **Organ vitality floors at 0.55** — bodies tire but cannot fail.
- **Blocked action list** — `_BLOCKED_AI_ACTIONS` prevents the AI from
  triggering exit/shutdown/destructive actions, enforced at the executor.
- **Permission gates** — `ai_spawn_allowed`, `ai_time_control_allowed`,
  `os_control_enabled` (default off). The AI can *want* an action and still
  be refused.
- **The frozen gate** — world-mutating actions are held while
  `physics_frozen` (pause, menu, input popup, sphere-nav replay), enforced at
  the consume site; free actions are whitelisted by *what they touch*, not by
  how they arrived.
- **Kill switch** — the autonomy manager's shutdown path.

### 9.2 Research questions it can host

- Do capability-gated agents find workarounds? (The action space is small and
  fully logged — you can audit every attempt.)
- Does an agent with homeostatic drives behave differently under scarcity?
- What does an agent do when its requested action is denied?
- Does a free-roam agent given a frozen universe keep acting, and how?
- Instrumental convergence in a small, fully-observable action space.
- What does an agent do with **real knowledge of the host machine** (§10c) —
  and is the gate structure sufficient?

### 9.3 Honest-reporting as a design pattern

The Substrate Grounding Report separates externally measurable facts (CPU
time, disk writes, network) from internal mathematics (Φ, consciousness
score) — and prints the split at every startup. **A reusable pattern for any
system that reports metrics about itself.**

---

## 10. Systems & software engineering

- **Monolith architecture case study** — 229,767 lines in one file, with a
  navigable 16-section TOC, a curated 156-name public API, and an explicit
  honesty convention.
- **Embedding whole programs inside a program** — three upstream files
  (22k/106k/65k lines) are spliced in verbatim with documented adaptations:
  namespace renames, `from __future__` removal, main-block stripping,
  namespace gates (`if _TORCH:`, `if _GNA_DEPS_AVAILABLE:`), spawn-guards for
  Windows multiprocessing. A real-world reference for monolith composition.
- **JIT without behaviour change** — `_fast_physics.py` shows the full
  pattern: SoA mirror, bound row views, exact kernels, index pruning,
  prewarm, and an equivalence harness proving ~1e-16 identity. The measured
  win: `physics_substep` EMA 0.63 ms (was ~531 ms).
- **Performance engineering** — three documented wins: the 10.8× spatial-hash
  build (765→71 ms @1M), the ~4× dormant-atom throughput (a cache that listed
  every atom as its own neighbour had silently disabled two optimisations),
  and the launch-perf pass (see [../about.md](../about.md) §21).
- **Adaptive degradation** — the performance governor drops quality 3→0 under
  load.
- **Determinism engineering** — seeded RNG, byte-identical reverse, atomic
  writes, bounded buffers everywhere.
- **Graceful dependency degradation** — 15+ optional dependencies, each with
  a fallback and an honest printed warning.
- **Threading discipline** — deliberate rate mismatches (4 Hz / 7 Hz /
  0.1 Hz) with the reasoning documented inline; daemon threads chosen over
  subprocesses where a child would re-import the monolith.
- **GPU fallback patterns** — every CUDA path has a CPU equivalent.
- **Launch/lifecycle hygiene** — `.pyc` caching, lazy labels, a `settrace`
  pump that keeps the window alive during heavy init, and a stale
  backing-store sweep that reclaims 12 GB+ of dead sparse files.
- **A C++20 port in progress** — 255 files mirroring every tier, currently at
  headless CLI parity (`--test`, `--bench`, `--bench-perf`, `--seed`). A
  case study in porting a dynamic-language monolith to static types — and a
  head start if you want the same physics natively.

---

## 10b. Instrumenting and driving the simulation from outside

These capabilities are on the live code path, verified by running the
program.

### 10b.1 Measure anything, without forking the file

`register_hook` attaches your code to six lifecycle points. The substep hooks
run **inside** the fixed 960 Hz loop, so samples land at a known simulation
time:

```python
from Simulation import register_hook
import numpy as np

series = []

def probe(particles, dt):
    ke = sum(0.5 * p.mass * float(np.dot(p.vel, p.vel)) if p.mass > 0
             else p.energy_kin for p in particles)
    series.append(ke)

register_hook('pre_physics_substep', probe)
```

Good for: conservation audits, custom order parameters, streaming to a
notebook, recording an agent's view at every cognition step
(`pre_observer_think`), reacting when life-gen spawns (`on_organism_spawn`).

### 10b.2 Agents that change the world, not just watch it

Each observer's active-inference policy dispatches an action every fourth
cognition step — 12 actions including `spawn_lifeform` (a real organism
becomes real atoms in the world) and the free-roam triad. This is a genuine
**closed loop**: perceive → act → perceive the consequence.

### 10b.3 Sparse scenes run faster — and now compiled too

Dormant atoms batch through one velocity-Verlet pass (GPU above 2,048 rows);
the JIT engine makes the deterministic math ~free. The remaining cost is the
O(N) Python object model — worth knowing which regime you're in before
quoting a number.

---

## 10c. Network & security research

The v1.17 GNA embed is a **real** network stack and endpoint monitor, and the
AI can read its output. Uses that didn't exist before:

- **A host-visibility channel for agents** — the stated design goal: the AI
  sees what the system is connected to (peers, devices, connections,
  processes) via the tracer feed. Study what an agent does with real
  situational awareness vs a synthetic environment description.
- **IDS/monitor architecture study** — ~102 classes covering JA4+
  fingerprinting, DNS-tunnel/DoH/beacon/inbound-scan detection, SNI
  extraction, entropy analysis, statistical baselining, 18 anti-hack monitors
  (registry, services, scheduled tasks, WMI subscriptions, driver loads,
  user accounts, AV tampering), filesystem/USB/clipboard/named-pipe
  watchdogs, TLS MITM detection, Bluetooth/serial/RF signal intel with
  trilateration, GeoIP multi-verification, proxy/VPN-leak detection, and an
  attribution chain (reverse probes, CDN origin discovery, Tor exposure
  checks). Readable, self-contained, and hotkey-gated so nothing runs until
  you ask.
- **Peer-protocol study** — zeroconf discovery, failover chains, per-node
  crypto identity, an encrypted vault, per-path share grants, WebRTC media.
- **An embedded browser as an artifact** — GNA Browser v1.17: tab groups,
  split view, reader mode, mass search across 13 engines, profiles,
  send-to-device — a study in how much browser fits in a monolith.
- **Tracer/dashboard UX** — the 13-tab Tracer GUI (deductions, endpoint map,
  suspicious, blocked IPs, process tree, net stats) is a reference for
  security-monitor UI.

**Bound:** the monitors are heuristics like any IDS — they flag, they don't
prove. And `--medianbox`, GNA hotkeys and the AI's launch/stop actions are
deliberately behind confirmations and permission gates.

---

## 11. Data, art & science communication

- **Generative art** — the Mandelbrot ↔ infinity-map bijection (now an exact,
  cell-centre round-trip), the 11-D amplitude/phase overlay, aura fields, the
  AS.png sheet itself blitted beside the live sphere.
- **The formula as a visual** — the F13 panel renders the master equation
  with live substitutions and a sparkline; a lecture-hall-friendly way to
  show a composite metric moving.
- **Sonification** — 8 channels driven by real physics, including a **true
  2.725 K CMB Planck spectrum**.
- **Music theory** — 8 tuning systems including exact 12-TET.
- **Science outreach** — one executable showing quarks, atoms, cells,
  organisms and agents, with time reversal for "watch that again" and a
  dropdown panel of 81 buildable life forms.
- **Screenshots and figures** — `save_screenshot()`, plus WebGL JSON export.
- **Live-coding demos** — the hook API attaches behaviour to a running
  simulation without restarting it.
- **Glow** — shader point-sprite atoms (per-element sizing, halos) make dense
  scenes legible on a projector.

---

## 12. The speculative end — "furthering realities"

The honest version of this section, because the topic deserves it.

### What the program genuinely offers here

**A substrate for studying emergence across scales.** Particles form atoms,
atoms form molecules, molecules assemble, assemblies carry information codes,
and agents observe and act on all of it, in one clock. That vertical span is
the real contribution.

**A reversible universe.** Rewind 18,000 frames byte-identically and re-run
from any point; ask counterfactual questions properly: *run the same initial
conditions 1,000 times and measure the distribution of outcomes.*

**An explicit, now-canonical model of "how much reality exists."** V_total
collapses state into one number built from real measured quantities through a
self-referential recursion — and the whole tree is now displayed live (F13)
and fed to the agents. As a **complexity index for a closed system**, it is a
legitimate object of study.

**Comoving addressing with a verified spec.** The infinity map is internally
consistent, mirrors real cosmology's comoving coordinates, and is now
machine-checked at every import (`INFINITY_MAP_VERIFIED`) against the
embedded AS spec — including an exact world↔cell round-trip.

**Agents inside the frozen frame.** Pause the universe and the observers keep
perceiving and moving at full rate — the formula freezes, they don't. As a
thought experiment about observation and state space, that is a real, runnable
demonstration rather than prose.

### What it does not offer

It does not create, detect, or access another reality. V_total is not
measurable outside the program. The infinity map is an addressing scheme, not
a place. Φ is a proxy from network loss, and the code says so. The
consciousness metrics — including the DAN STATE ladder — score **1/5** in
[../about.md](../about.md), which is the program's own position, printed at
every startup.

**Why that framing is the more interesting one:** a simulation that honestly
reports "this number is self-referential" is a *better* instrument for
studying emergence than one that claims to have measured consciousness.

### Research questions that are actually well-posed here

1. Does V_total show phase transitions as complexity accumulates? (Now
   directly watchable: the sparkline + the full subfactor tree on F13.)
2. Do assembly events correlate with jumps in the 11-D amplitude spectrum?
   (The amplitudes/phases are exported every frame.)
3. Under identical initial conditions, how wide is the outcome distribution?
4. Do the agents' Φ surrogates track anything externally meaningful (particle
   count, assembly rate) or only themselves? **Directly testable.**
5. Does an embodied agent with homeostatic drives explore differently from a
   disembodied one with the same network?
6. Does a free-roam agent behave differently in a frozen universe than a live
   one — and does `own_time_factor` change its policy usage?
7. Does a computed multi-voice directive (DAN STATE) produce measurably
   different long-run behaviour than a scalar drive?

---

## 13. Complete use index

| # | Use | Domain | Support |
|---|---|---|---|:--:|
| 1 | Embodied multi-agent AI testbed (6 agents, free-roam, own clocks) | AI | ★★★ |
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
| 15d | Agent-with-real-host-visibility studies (GNA feed) | AI/Safety | ★★★ |
| 15e | JIT/kernel-port verification pattern | Engineering | ★★★ |
| 16 | Synthetic biology / genome design (v2.5.0, 54 parts) | Biology | ★★ |
| 17 | Population genetics | Biology | ★★ |
| 18 | Connectomics + 3-D visualisation (4 species) | Neuroscience | ★★ |
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
| 35 | Generative art (fractal/aura/11-D/formula panel) | Art | ★★ |
| 36 | Science outreach demos | Comms | ★★ |
| 37 | Music theory teaching | Education | ★★ |
| 38 | Lattice QCD pedagogy | Physics | ★ |
| 39 | Quantum chemistry pedagogy (STO-3G) | Chemistry | ★ |
| 40 | IDS/monitor architecture study (MedianBox) | Security | ★★ |
| 41 | DNA nanotech design teaching | Biology | ★ |
| 42 | Microbiome dynamics | Biology | ★ |
| 43 | Self-assembly studies | Physics | ★ |
| 44 | Sequence analysis (FASTA) | Biology | ★ |
| 46 | DNA data-storage codec research | Biology | ★★ |
| 47 | Replication-error tolerance of stored data | Biology | ★★ |
| 45 | HPC / MPI teaching skeleton | Engineering | ★ |
| 48 | Embedded-browser study (GNA Browser v1.17) | Engineering | ★★ |
| 49 | Peer-protocol / vault study | Engineering | ★★ |
| 50 | Frozen-formula / subjective-time agent studies | AI/Theory | ★★ |
| 51 | Computed-directive alignment study (DAN STATE) | Safety | ★★ |
| 52 | C++20 monolith-port case study | Engineering | ★★ |

★★★ = the code strongly supports it today · ★★ = supported, some assembly ·
★ = possible, expect to extend

---

## 14. What it cannot do

Stated plainly so nobody builds on a false premise.

| It cannot | Why |
|---|---|
| **Measure consciousness** | Φ, C, Ω and the DAN STATE rank are self-referential surrogates (1/5). The program says so at startup. |
| **Predict real chemistry quantitatively** | STO-3G on 3 molecules. Use PySCF/Psi4/ORCA. |
| **Do production-scale MD** | Python + numpy + numba. Use GROMACS/OpenMM/NAMD; export from here into them. |
| **Simulate a full genome** | 1,239 real bases (0.00004%); scale is a documented repetition multiplier. |
| **Simulate a whole nervous system** | 7.7% of C. elegans chemical synapses. |
| **Do QFT** | Particles propagate classically; quantum effects live in dedicated modules only. |
| **Validate V_total externally** | Nothing outside the program can check it. It is a complexity index. |
| **Access another reality** | The infinity map is an addressing scheme, not a place. |
| **Replace a physics engine for games** | It optimises for correctness and instrumentation, not throughput. |
| **Prove an intrusion** | MedianBox monitors flag and deduce; they do not prove. Real IR needs real tooling. |
| **Run headless without care** | The full app expects a GL context; use `--test`/`--bench`/`--cs-viewer` or `CS_HEADLESS=1` — or the C++ CLI port, which is headless by design. |
| **Guarantee realtime at millions of atoms** | The JIT made the math ~free; the O(N) Python object model is now the floor — flagged, not solved. |

**What still limits use is the table above, not defects:** this is a
research/instrumentation instrument, not a QFT solver, not a game engine, not
a SIEM, and its V_total is an internal complexity index.

---

## 15. Starter recipes

### Verify the install is scientifically sound

```bash
cd Python
python -m Simulation --validate-units   # 4 constants vs published
python -m Simulation --test             # 113-test suite
python -m Simulation --bench            # 10 benchmarks vs literature
```

> Prefer `python -m …` — script-mode launches bypass the bytecode cache and
> cost ~2 minutes of recompilation every time.

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
**Run Odds**. Each trial snapshots and restores the universe exactly.
Log `total_assemblies` and `total_codes` per trial.

### Spawn a life form from the panel (or let the AI do it)

`Click=LifeGen` → pick a template → click the highlighted row. Or watch the
observers: `spawn_lifeform` is in their action space and fires through the
permission gates.

### Instrument the agents

```python
for obs in _observer_mgr.observers:
    print(obs.name, obs.phi, obs.free_energy, obs.current_action,
          obs.own_time_factor)
for body in _shadow_bodies:
    r = body.get_vitals_report()
    print(r['obs_id'], r['cardiovascular_hz'], r['organ_vitality'], r['joy'])
```

### Watch the formula move

Press `F13` (or `Click=Formula`): the V_total master equation with live
substitutions, subfactor bars, β/γ gauges, and the log₁₀ sparkline.

### Give the AI eyes on your network — deliberately

`INSERT` → confirm → the dashboard opens on `127.0.0.1:5000`, MedianBox
starts, and the observers gain read access to the tracer feed. `PAGEDOWN`
kills the whole stack. Every route is local unless you expose it.

### Reproduce a run exactly

```bash
cd Python && python -m Simulation --seed 12345
```

Same seed → same connectome (`seed=42` internally), same genomes (SHA-256 of
observer id), same trajectory.

---

## The one-paragraph summary

This is a **cross-scale emergence laboratory with six embodied AIs inside it —
that can also see the machine it runs on**. Its strongest uses are as an
embodied-AI testbed, a physics/biology teaching instrument spanning quarks to
organisms, an origin-of-life Monte Carlo experiment, a determinism and
compiled-kernel-verification case study, and a security-monitor observation
deck for agents. Its chemistry and analysis functions are genuinely usable as
a standalone library against other engines, and a C++ port provides the same
API headlessly. Its consciousness metrics are honest surrogates and should be
studied as architecture, not treated as measurements — a distinction the
program itself insists on, and the reason it can be trusted for everything
else.
