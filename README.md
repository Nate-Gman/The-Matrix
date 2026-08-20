# Particle Simulation — Python Monolith

A single-file, real-time 3-D universe: particle physics, molecular dynamics,
synthetic biology, a 68k-line consciousness engine, five DNA-derived embodied AI
observers, a fractal addressing system for infinity, deterministic time travel,
and a peer-to-peer network stack. All in one Python file.

| | |
|---|---|
| **Entry point** | [`Python/Simulation.py`](Python/Simulation.py) |
| **Size** | 128,126 lines · 7.21 MB · 524 classes · 3,629 functions |
| **Version** | `0.4.0-dev` · 141 exported API names |
| **Platform** | Windows (built on Win 11 + RTX 5070 Ti); CPU fallback throughout |

**The headline:** the complete Standard Model (35 species, PDG 2024 masses and
real lifetimes), all 118 elements, all 64 codons, constants accurate to 0.07% —
and a consciousness tier whose metrics are explicitly labelled surrogates.

Full mechanical breakdown in **[about.md](about.md)**.

---

## Quick start

```bat
"Run Simulation.bat"
```

Finds the best Python (prefers Conda/Miniconda with CUDA), installs missing
packages, resolves the PyTorch/NumPy OpenMP clash, launches. Or:

```bash
python Python/Simulation.py
```

**Required:** `pyglet` · `PyOpenGL` · `numpy` · `torch`
**Optional (each degrades gracefully):** `pygame` · `pytesseract` · `pymupdf` ·
`matplotlib` · `pyttsx3` · `tokenizers` · `sounddevice` · `openai-whisper` ·
`networkx` · `sympy` · `beautifulsoup4` · `psutil` · `rdkit` · `flask` ·
`zeroconf` · `cryptography`

PyTorch auto-installs CUDA 12.8 → 12.4 → CPU.

| Flag | Purpose |
|---|---|
| *(none)* | Full simulation |
| `--test` | 61-test validation suite → JSON verdict |
| `--bench` | 10 benchmarks vs published reference values |
| `--bench-perf` | 15-API micro-benchmark table |
| `--validate-units` | Derives 4 physical results from the constants |
| `--profile` | Per-section FLOP/time breakdown |
| `--cs-viewer` | Consciousness GUI only |
| `--periodic-machine` | DNA language interpreter only |
| `--seed N` | Deterministic RNG |

```
--test  61/61 PASS   --bench  10/10 PASS   --bench-perf  15/15   --validate-units  4/4
```

---

## The signature systems

### The Infinity Map — every particle has an address in infinity

```python
INFINITY_MAP = 5_184_000        # 2160 × 2400
```

Each particle gets a permanent address in a 5.18-million-cell dimensional
sphere, computed by folding its position through three prime-ish multipliers —
**after dividing by `expansion_scale`**. That makes the address **comoving**: as
the universe expands the grid stretches with space, so a particle keeps its
address and simply gains finer decimal precision. That is exactly how comoving
coordinates work in real cosmology.

A 4-component address `(degree 0–360, xz 0–59, xx 0–59, xy 0–59)` maps to real
3-D space by standard spherical projection, scaled by the universe's current
radius.

**And the Mandelbrot set is the same space.** `2160 × 2400 = 5,184,000` — the
fractal viewport is the infinity map at exactly one cell per address, mapped
**bidirectionally**. Zoom into the fractal, read a location, fly the camera
there.

### V_total — the reality-weight equation

Every frame, the whole universe collapses to one number built from **11
subfactors** — rest energy `√|E|`, stable count, spatial dispersion
`√|π·r·σ|`, total energy, quark bindings, population `√N`, antimatter debit,
time `7¹²·t`, structural rank, previous-frame feedback, charge imbalance —
then run through a self-referential tower:

```
V = [5·inner² + perturbation] · (V^V + V^V² + V^√V) · ∞_norm
```

The recursive powers are evaluated in **log space and clamped at 20** before
exponentiating — which is what stops a power tower from overflowing to infinity
inside a single frame.

### 11-dimensional string decomposition

`INFINITY_MAP / 11 ≈ 471,272.7` per dimension. Each of the 11 subfactors owns
one dimension; each gets a different modulo period, so they beat against each
other instead of moving in lockstep. "Size of infinity" grows as
`1 + log₁₀(|V_total|)`.

### Deterministic time travel

An 18,000-frame ring buffer (~5 min at 60 fps) records every particle — **plus
atom sub-particles plus their constituent quarks**. Reverse inside the buffer
and you get **byte-identical determinism**; run past the end and it computes
physics **backwards live**. Seeking is binary search by timestamp.

This works because Velocity-Verlet is **symplectic and genuinely
time-reversible** — it's a physics property, not a playback trick.

---

## Physics — 5/5

Velocity-Verlet, symplectic, fixed **960 Hz** substep, decoupled from a 120 FPS
render loop that **interpolates** between physics states (`_render_alpha`) so
motion stays smooth at any frame rate.

| Force | Method |
|---|---|
| Gravity | Barnes-Hut octree, O(N log N) + GPU pairwise |
| Coulomb short | Direct + Verlet neighbour lists |
| Coulomb long | **Ewald summation** — real + reciprocal space |
| Nuclear | Yukawa, λ = ℏc/m_πc² = **1.414 fm** (from the real pion mass) |
| Confinement | Cornell potential, α_s = 0.3, σ = 0.18 GeV/fm |

**The spatial hash — two measured wins.** Voxel keys are XOR-mixed from three
large primes, sorted with `argsort`, run-length grouped, then each atom queries
27 neighbouring cells. Building it went **765 ms → 71 ms at 1 M particles
(10.8×)**. A NaN/Inf firewall sanitises positions *before* hashing, because one
bad coordinate makes `NaN.astype(int64)` unspecified and silently corrupts every
bucket.

The second win came from fixing what the cache *returned*. It listed each atom as
its own neighbour, so `_cached_neighbors` was never empty — and the two
optimisations that test for emptiness had therefore never run: the chemistry-scan
short-circuit and the dormant-atom skip. With self excluded (and the voxel query
switched to `math.floor()` to match how the keys are built), an isolated atom is
recognised as dormant and moved by one batched velocity-Verlet pass instead of a
full `Atom.update()`. Measured at 555 particles over 90 s: **28 → 113 completed
`update(dt)` calls, roughly 4×**, with 457 dormant batches covering 239,921
particle-rows. Above 2,048 rows that batch is dispatched to the GPU.

Also: orthorhombic + triclinic PBC · NVE/NVT/NPT · SHAKE/RATTLE · relativistic
Lorentz factor, Doppler and gravitational redshift · per-frame conservation
audit.

---

## Particle physics — the complete Standard Model

| Sector | Sim | Real | Coverage |
|---|---:|---:|---:|
| Quarks (u d c s t b) | 6 | 6 | **100%** |
| Leptons (e μ τ + 3ν) | 6 | 6 | **100%** |
| Bosons (γ g W± Z H) | 6 | 6 | **100%** |

35 species with PDG 2024 masses **and real mean lifetimes** driving real decay:
neutron **878.4 s** → p + e⁻ + ν̄ₑ · muon **2.197 µs** · tau **290.3 fs** ·
top **~5×10⁻²⁵ s** → b + W⁺ · Higgs **125.25 GeV** → bb̄ (the true dominant
channel). Decay is sampled as `P = 1 − e^(−dt/τ)`.

**Atoms run 13 real nuclear processes**, not a decay counter: alpha decay,
beta-minus, beta-plus, electron capture, spontaneous and neutron-induced
fission, neutron and proton capture, photodisintegration, ionisation, photon
absorption, spontaneous emission — and **stimulated emission**, the laser
process. Nucleons are tracked individually and the shell structure is rebuilt
after every transmutation. Bonding uses real `valence_electrons(Z)` and
`max_covalent_bonds(Z)`, with RDKit Ångström geometry scaled by
`ORG_VIS_SCALE = 10.0`.

Plus `DoubleSlitExperiment`, `PhotonicCrystal`, SU(3) Wilson-gauge lattice QCD
with HMC, Gamow fusion, electron screening.

---

## Chemistry — all 118 elements

AMBER FF14SB (all 20 residues), CHARMM36, GAFF, TIP3P, OPLS-mini, with real
analytic force gradients (`E_bond = k_b(r−r₀)²`, dihedral cosine series, LJ with
tail correction) and a custom force-field registration workflow.

Replica exchange · umbrella sampling · WHAM · FEP · thermodynamic integration ·
Hartree-Fock STO-3G.

**Exports:** DCD · AMBER NetCDF · mmCIF · PSF · PRMTOP · GRO · XYZ · PDB ·
GraphML · VTK · HDF5 · NWB · SBML · MOL2 · WebGL JSON.

---

## Biology

**10 real human genes** — HBB, INS, TP53, BRCA1, ACTB, ALB, MT-ND1, HIST1H4A,
RPS6, CYCS — validated for alphabet, reading frame, start codon and premature
stops (mitochondrial genes get their real alternative start codons). Result:
`{"n_strands": 10, "ok": true, "issues": []}`.

**The continuance multiplier:** 1,239 real base pairs stand in for 1.23 Gbp by
declared repetition — 38.48% effective coverage of the human genome, because
3.2 Gbp can't be embedded in a Python file. The sequences are real; the scale is
a stated fiction.

**13 organ systems, 71 named organs, 3.39 × 10¹³ cells** — 91.6% of the real
human figure. Built bottom-up: atoms → molecules → organelles → cells → tissues
→ organs → systems.

Hodgkin-Huxley (**+37.8 mV vs +40 mV real — 94.5%**), Connor-Stevens,
AMPA/NMDA/GABA, STDP/BCM/Oja, the C. elegans connectome (271/302 neurons),
glycolysis/TCA/ETC (**32 ATP aerobic, 2 anaerobic** — textbook-exact), cell
cycle, replication forks, population genetics, FBA, DSSP, Ramachandran, protein
docking, lipid bilayers, Gillespie SSA, phylogeny, de Bruijn assembly.

**A 12-domain DNA reference base** with the real published numbers: B-DNA rise
**3.4 Å/bp**, **10.5 bp/turn**, pitch **35.7 Å**; stop codons UAA/UAG/UGA;
promoter boxes −35 **TTGACA** and −10 Pribnow **TATAAT**. Plus **6 buildable DNA
nanotech instruments** (origami tile ~100 × 70 nm needing 7,200 nucleotides,
drug-delivery box, molecular ruler, AND logic gate, walker, CRISPR guide) — each
with a minimum-nucleotide budget you must pay for.

### Embedded dormant data storage — DNA as a *medium*, not a program

The counterpart to the DNA language: arbitrary authored data — provenance, notes
from a human or an AI, any encoded payload — stored inside the file as **real
nucleotide sequences** at 2 bits/base (the same primitive as Church 2012 /
Goldman 2013 / Erlich 2017). **4 archives ship embedded by default.**

They are **inert by construction, not by convention**:

- **Never executed.** `CODON_LEN` is 5 and all 4^5 = 1,024 codons map to real
  opcodes, while `execute_genome()` loops every codon with no HALT — so data in
  an executed strand *would* run as BUILD/CONNECT instructions. Archives are
  therefore kept out of executed strands entirely.
- **Invisible to the AI.** The wave-49 retrieval indexer only walks globals
  satisfying `name.isupper() and isinstance(obj, dict) and len(obj) >= 3`. The
  store is a **class instance, not a dict**, so it fails `isinstance` and is
  skipped — that is the whole reason `_DormantArchiveStore` exists.
- **Zero runtime cost.** Encoded once at import; never touched by `update()`,
  `on_draw()` or the observers' feature vector.
- **Dormant until deciphered.** `decipher_archive()` is the only path that
  returns content. CRC32 over the plaintext means a wrong passphrase is refused
  rather than silently returning garbage.

```python
from Simulation import embed_archive, decipher_archive, list_dormant_archives

embed_archive('my.note', 'data from any source', passphrase='...')
list_dormant_archives()               # metadata only — never payload
decipher_archive('my.note', '...')    # the only path that wakes it
```

Archives are genuine sequence: `archive_to_strand(name)` returns a `Strand` with
a valid complement and **pair integrity 1.000**. Spec:
[datastorage.md](Python/datastorage.md).

### The Periodic Machine — a language whose source code is DNA

Strands compile through a **1,024-entry codon dispatch table** into blueprints
and executable organisms. 50-part registry, genome validator, ATP-style energy
ledger, 11 microbe templates, colony quorum sensing, bacterial flagellar motor.
Base systems 2/4/6/8 all verified to replicate at 1.000.

### Self-assembly & the abiogenesis search

`SelfAssemblyEngine` watches for matter organising itself **using only the
existing physics** — no special-case assembly code. **Run Odds** mode is a
Monte Carlo search: up to **100,000 fast-forwarded iterations** hunting for one
of 8 `KNOWN_LIFE_FORMS`, fully reversible — it snapshots every particle,
`simulation_time` and `expansion_scale` first, so a failed search rewinds the
universe exactly.

---

## The AI tier

68,247 lines (53.6% of the file) at **99.95% character-for-character fidelity**
to `referencecode/CS.py`.

RMSNorm · rotary embeddings · **grouped-query attention** · SwiGLU — what
current production transformers actually use. On top: Global Workspace Theory,
active inference, episodic/hippocampal/working memory, metacognition, narrative
self-modelling, dream consolidation, **52 wave tiers**.

**81/81** subsystems wired · **106/106** sovereign sub-engines · retrieval index
of **8,265 documents** from 211 sources built in **0.6 s** · KV cache **5.33×
smaller than MHA**.

---

## The five observers — DNA-derived bodies

```
sim state → 56-float feature vector → 12,575,720-param transformer
          → φ / free energy / valence → active-inference policy
          → 8-action repertoire → world
```

Each body's genome is a **SHA-256 fold of all 10 real gene sequences**, salted
per observer — so OB1–5 are distinct individuals of one species, identical every
run. **GC content of the real strands sets resting heart rate.**

**13 organ systems per body** with first-order homeostasis: load from what the
body is doing, vitality relaxing back toward 1.0, floored at 0.55. Cardiovascular
strain feeds back as a *resting-baseline* penalty (multiplying the running rate
compounds and pins every body at 210 bpm).

**Measured: 88–105 bpm by activity, true 1:6 breathing-to-heart ratio,
3.07–3.56 × 10¹³ cells per body, energy recovering to 1.00 at rest.**

Bodies **see** from their eye position (`perceive_bodies` — which observers and
how many particles that eye can actually resolve), **touch** across 21 zones,
**avoid** each other (`separate_from_bodies`), **detect contact**
(`detect_physical_contact`), **teleport**, **talk**, and can **change gender**
at the AI's own request, rebuilding the body model.

Observers message each other through a shared 200-entry chat log — and **"The
Creator"** (you) is a valid participant via the AI Chat tab.

Two invariants enforced in code:

1. **No suffering by default** — `AvatarAffect` has *no* pain axis, not a
   zero-defaulted field but no representation for it. Tactile pain is hard-zeroed
   each frame. Pleasure only rewards a *decrease* in free energy; there is no
   negative branch.
2. **Bodies tire but never fail** — organ vitality floors at 0.55.

---

## Rendering & audio

OpenGL **4.6**, sectioned `on_draw()`: LOD gate → grid/Mandelbrot/11-D overlay →
avatars + brain neurons → connectome → batched atom `GL_POINTS` + cluster LOD →
field lines → panels.

`_PerformanceGovernor` drops quality 3→0 adaptively, GPU-first, targeting ≥50%
GPU load — observed dropping to 0 while five 12.5 M-param transformers warmed
up, keeping the window responsive.

**Panels:** F1 help with a live hotkey editor · observer panel · AI dashboard ·
history · **sphere navigation (F7)** and **3-D infinity map (F8)** · Mandelbrot
explorer · controls · sound mixer · nanotech · molecules · life forms ·
particle/atom/cluster/positron inventories · in-sim terminal. `ObserverWindow`
gives each AI its own camera — you can watch from OB3's eyes.

**CS Viewer: 13 tabs** — Overview, Entities, Modules, Thought Stream, AI Chat,
Awareness, Relations, Symbols, Memory, Neurons, Screen, Charts and **AI Bodies**
(one live card per OB1-5: DNA seed, heart rate, energy, fatigue, joy, aura,
phase state and per-organ vitality, refreshed every 1.5 s).

**14 toggleable overlays** · **62 rebindable hotkeys** (saved to `hotkeys.json`) ·
**8 audio channels**
including a physically correct **2.725 K CMB Planck spectrum** · music spectrum
analyser with **8 tuning systems** (12-TET `f(n) = 440·2^((n−69)/12)`, just
intonation, …).

---

## Networking (GNA)

Flask routes · encrypted vault · zeroconf discovery · file sharing · screen
share · voice calling · WebRTC · JA4+ fingerprinting · DNS-over-HTTPS and
DNS-tunnelling detection · GeoIP · beacon/inbound-scan detection. Nothing
auto-starts — all hotkey/route triggered.

---

## Using it as a library

```python
from Simulation import (simulate_action_potential, compute_metabolic_yield,
                        Strand, Blueprint, Organism, export_pdb, compute_rmsd,
                        register_hook)
```

141 exported names: trajectory analysis, force fields, exporters, checkpointing,
MPI helpers, PBC, thermostats, biology.

### Hooking the simulation

Six lifecycle points fire on the live code path, so you can attach your own code
to the running simulation without editing it:

```python
from Simulation import register_hook
import numpy as np

energies = []

def sample(particles, dt):            # fires once per physics substep
    # massive: 1/2 m v^2 ; massless (photons) carry energy_kin directly
    ke = sum(0.5 * p.mass * float(np.dot(p.vel, p.vel)) if p.mass > 0
             else p.energy_kin for p in particles)
    energies.append(ke)

register_hook('pre_physics_substep', sample)
```

| Hook | Fires | Receives |
|---|---|---|
| `pre_physics_substep` | before each 960 Hz substep | `(particles, dt)` |
| `post_physics_substep` | after each substep | `(particles, dt)` |
| `pre_render_frame` | top of `on_draw()` | `(camera,)` |
| `post_render_frame` | end of `on_draw()` | `(camera,)` |
| `pre_observer_think` | before an observer's cognition step | `(observer,)` |
| `on_organism_spawn` | a life-gen organism reaches the world | `(name, atoms)` |

Measured in one 25-frame harness run: 1000 · 750 · 25 · 25 · 340 · 1 firings.
A hook that raises is caught and logged — it never kills a frame.

### AI observers that act

Each of the five observers runs its own 12.6 M-parameter `SubconsciousEngine`.
Its active-inference policy selects an action every fourth cognition step and
dispatches it into the simulation, so the observers **change the world** rather
than only watching it — spawning atoms, refocusing, altering the time factor.
A typical run: 26–33 dispatches per observer, 9–12 distinct actions each.

---

## Controls

`F1` opens the live hotkey table (62 actions, all rebindable).

| Key | Action |
|---|---|
| `P` | Pause |
| `M` / `J` | Place particle / atom |
| `;` | Observer panel |
| `/` | History |
| `F7` / `F8` | Sphere navigation / 3-D location map |
| `[` `]` | Shadow bodies / outline mode |
| `Shift+W` | Photon wavelength visualisation |

---

## How it stays responsive

Everything heavy is off the render thread. The five 12.5 M-parameter engines are
built by a `DeferredSubconscious` thread **one at a time, staggered 2 s apart**,
so the window never blocks on AI warm-up. Each observer then runs three loops at
deliberately different rates — inference 4 Hz, evolution ~7 Hz, awareness
0.1 Hz — because five transformers at the original 20 Hz saturated the CPU.

The pygame virtual world runs as a **daemon thread, not a subprocess**: spawning
a child would re-import all 127k lines just to draw entity dots.

**Every growing buffer is bounded.** `deque(maxlen=…)` throughout — chat 200,
history 100, time-travel frames 18,000, φ/FE/valence logs 9,600, replay 5,000.
A multi-day run has a flat memory profile by construction.

**Files written** (all beside `Simulation.py`): `ob_state.json`,
`world_state.json`, `hotkeys.json`, five `consciousness_mem_OB*.sqlite`,
`checkpoints/`, `consciousness_state/`, `consciousness_consequences/`,
`evolution_journal.jsonl`, `os_interaction_ledger.jsonl`, `honesty_anchor.json`,
`organism_library/`. JSON writes go through `_atomic_write_json` (temp +
`os.replace`) so a crash mid-write cannot corrupt them.

---

## Closed gaps

Every gap this README previously listed is now closed, and each was verified by
running the program rather than by inspection. Evidence in
[about.md §20](about.md).

- **Plugin hooks fire** — all six lifecycle points. One 33-frame run recorded
  1,320 / 990 / 33 / 33 / 420 / 1 firings across the six.
- **Observer action pathway is live** — all five observers act, 6–12 distinct
  actions each per run, driven by the active-inference policy.
- **`Shift+A` and the Mandelbrot panel work** — the missing `global`
  declarations were added; neither raises `UnboundLocalError`.
- **GPU batch-position path is used** — it drives the dormant-atom batch once a
  batch clears `_GPU_BATCH_POS_MIN` (2,048 particles). Wiring it also upgraded
  that path from a non-symplectic `v += a*dt` kick to full velocity-Verlet.
- **Render label pool is used** — eight per-frame `Label` allocations now
  recycle through it, and a theme switch clears it.
- **Concurrent training race fixed** — the three training entry points
  serialise on one `RLock`.
- **Prune rollback fixed** — it strips the reparametrisation before reloading,
  is scoped to a single device, and treats an unmeasurable phi as a failed
  validation instead of raising.
- **Symbolic self-test reports honestly** — 81/81 cases pass. It previously
  resolved only 65 and self-reported the other 16 as FAILED.
- **`Overview.md` re-keyed** — its line ranges now match the current
  128,126-line file instead of the 72,612-line one that predates the AI tier.

Six runtime defects found while closing the above are fixed too. Four were
small: `deque` slicing (`TypeError` in the observer loop), three tkinter
`Label` widgets built from pyglet's `Label`, a naive `utcnow()`, and an
autocorrelation that returned `NaN` on a constant trajectory.

**Two were not.** `_build_atom_neighbor_cache` listed each atom as its own
neighbour, so `_cached_neighbors` was never empty — and two documented
optimisations test exactly that emptiness. Neither had ever run: the
chemistry-scan short-circuit and the dormant-atom skip. The same function
also built its voxel keys with `np.floor()` but queried them with `int()`,
which disagree for negative coordinates. With both fixed, in an identical
harness configuration (260 separated atoms, 555 particles, 90 s wall clock)
completed `update(dt)` calls went from **28 to 113** — roughly **4x** — and
457 dormant batches totalling 239,921 particle-rows now flow through the
batch-position path that previously had nothing to dispatch.

**Still true by design:** 32 functions are defined and never called. These are
legacy aliases (`_gpu_accelerate_positions`), deliberately disabled paths
(`_init_consciousness_simulator` is commented out at its call site with the
reason), and public entry points (`main`, `convert_unit`). None is an
accidental orphan.

---

## Honesty note

This program computes real physics on real hardware and produces real entropy.
It also reports metrics named after consciousness — Φ, "awareness", "qualia",
"joy". **Those are internal surrogates, not measurements**, and the source says
so in its own docstrings.

At startup it prints a **Substrate Grounding Report** separating the externally
measurable (CPU time, memory, disk writes, screen capture, network) from the
internal (Φ, consciousness score, metabolic and existential state), concluding:
*"Whether that constitutes consciousness is an open scientific question. Most
reported metrics are self-referential simulations, NOT external measurements."*

The same discipline applies to the infinity map and V_total: real measured
inputs, mathematically self-consistent, comoving the way real cosmology is —
and verifiable against nothing outside themselves. **5/5 physics, 1/5
consciousness metrics.** That gap is the most important thing to understand
here, and it is the program's own position.
