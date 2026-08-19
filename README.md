# Particle Simulation — Python Monolith

A single-file, real-time 3-D particle / chemistry / biology / AI simulation.
Physics, molecular dynamics, synthetic biology, a 68k-line consciousness engine,
five embodied DNA-derived AI observers, the renderer and a peer-to-peer
networking stack all live in one Python file.

| | |
|---|---|
| **Entry point** | [`Python/Simulation.py`](Python/Simulation.py) |
| **Size** | 127,362 lines · 7.52 MB · 523 classes · 3,601 functions |
| **Version** | `0.4.0-dev` |
| **Public API** | 141 names exported via `__all__` |
| **Platform** | Windows (developed on Win 11 + RTX 5070 Ti); CPU fallback throughout |

**Realism headline:** the entire Standard Model (35 species, PDG 2024), all 118
elements, all 64 codons, and constants accurate to < 0.1%. The consciousness
metrics are explicitly labelled surrogates. Full per-subsystem scoring in
**[about.md](about.md)**.

---

## Quick start

```bat
REM Double-click, or:
"Run Simulation.bat"
```

The launcher picks the best available Python (prefers Conda/Miniconda with CUDA
over MS Store), installs missing packages, sets `KMP_DUPLICATE_LIB_OK` to
resolve the PyTorch/NumPy OpenMP clash, and launches. Or directly:

```bash
python Python/Simulation.py
```

`Simulation.py` regenerates `Run Simulation.bat` from an embedded copy if it is
missing or outdated — the Python file is the single source of truth.

### Requirements

**Required:** `pyglet` · `PyOpenGL` · `numpy` · `torch`

**Optional — each degrades gracefully with a printed warning:** `pygame`
(virtual world) · `pytesseract` + Tesseract binary (OCR) · `pymupdf` (PDF) ·
`matplotlib` (charts) · `pyttsx3` (TTS) · `tokenizers` (BPE; falls back to a
hash tokenizer) · `sounddevice` (audio in) · `openai-whisper` (speech-to-text) ·
`networkx` · `sympy` · `beautifulsoup4` · `psutil` · `rdkit` (molecule geometry) ·
`flask` + `zeroconf` + `cryptography` (peer comms / GNA).

PyTorch auto-installs with CUDA 12.8 → 12.4 → CPU fallback if absent.

---

## CLI modes

| Flag | Purpose |
|---|---|
| *(none)* | Full simulation — 3-D window, physics, observers, renderer |
| `--test` | 60-test embedded validation suite, JSON verdict, exits |
| `--bench` | 10 research benchmarks against published reference values |
| `--bench-perf` | 15-API micro-benchmark table (mean / σ / reps) |
| `--validate-units` | Verifies SI constants resolve correctly (4 checks) |
| `--profile` | Per-section FLOP / time breakdown |
| `--cs-viewer` | Consciousness Simulator GUI only — no particle sim |
| `--periodic-machine` | Chemistry-DNA language interpreter UI only |
| `--seed N` | Deterministic RNG seed |

All self-test modes pass:

```
--test           60/60  PASS   (130.6 s)
--bench          10/10  PASS
--bench-perf     15/15  PASS
--validate-units  4/4   PASS
```

---

## Feature tour

### Particle physics — complete Standard Model
35 species with **PDG 2024** masses, charges, spins and real mean lifetimes:
all **6 quarks**, all **6 leptons**, all **6 gauge/scalar bosons**, 13
antiparticles, 12 with real decay channels (neutron τ = 878.4 s, muon τ =
2.197 µs, Higgs 125.25 GeV → bb̄). Plus double-slit interference, photonic
crystals, SU(3) Wilson-gauge lattice QCD with HMC, Gamow fusion, electron
screening, nuclear binding energy and decay.

### Physics engine
Velocity-Verlet, symplectic, fixed **960 Hz** substep with 120 FPS interpolated
rendering. Barnes-Hut octree gravity, GPU-batched pairwise gravity and EM,
**Ewald summation** for long-range Coulomb, Verlet neighbour lists (~71 ms at
1 M particles), LJ tail correction, orthorhombic + triclinic PBC, NVE/NVT/NPT
thermostats and barostats, SHAKE/RATTLE constraints, relativistic Lorentz
factor, Doppler and gravitational redshift, per-frame conservation audit with a
NaN/Inf firewall.

### Chemistry
All **118 elements** (Z = 1…118). AMBER FF14SB (all 20 amino acids), CHARMM36,
GAFF, TIP3P water, OPLS-mini, plus a custom force-field registration workflow.
Real bonded-force gradients. Replica exchange, umbrella sampling, WHAM, FEP,
thermodynamic integration. Hartree-Fock STO-3G for H₂/He/LiH.

**Exports:** DCD · AMBER NetCDF · mmCIF · PSF · PRMTOP · GRO · XYZ · PDB ·
GraphML · VTK · HDF5 · NWB · SBML · MOL2 · WebGL JSON.

### Biology
All **64 codons**, 21 amino acids. 10 real human reference genes (HBB, INS,
TP53, BRCA1, ACTB, ALB, MT-ND1, HIST1H4A, RPS6, CYCS) — validated for alphabet,
reading frame, start codon and premature stops. A 13-system human body
constructor spanning atoms → systems, totalling **3.39 × 10¹³ cells** (91.6% of
the real human figure). Hodgkin-Huxley (+37.8 mV vs +40 mV real) and
Connor-Stevens neurons, AMPA/NMDA/GABA synapses, STDP/BCM/Oja plasticity, the
C. elegans connectome, glycolysis/TCA/ETC (32 ATP aerobic, 2 anaerobic),
cell cycle, replication forks, population genetics, FBA, DSSP, Ramachandran,
protein docking, lipid bilayers, reaction-diffusion, Gillespie SSA, phylogeny,
de Bruijn assembly, horizontal gene transfer, and a microbiome model.

### Synthetic biology — the Periodic Machine
A Chemistry-DNA language engine: strands, opcodes (1,024-entry dispatch for a
4-base system), blueprints, organisms, an evolver, a **50-part** registry, a
genome validator, an energy ledger, **11 microbe templates**, colony quorum
sensing, and a bacterial flagellar motor simulator.

### AI — the consciousness tier
68,247 lines (53.6% of the file) inlined from `referencecode/CS.py`. RMSNorm,
rotary embeddings, **GQA attention**, SwiGLU, Global Workspace Theory, active
inference, episodic/hippocampal/working memory, metacognition, narrative
self-modelling, dream consolidation, and **52 wave tiers** of self-modifying
architecture. **81/81** subsystems wired, **106/106** sovereign sub-engines.
Retrieval index of **8,265 documents** from 211 sources.

### The five observers (OB1–OB5)
Each runs a **12,575,720-parameter** transformer and drives a DNA-derived
shadow body: genome folded from all 10 real reference gene sequences (salted
per observer, so each is a distinct individual of one species), an H-Anim
skeleton, **13 organ systems** with per-system vitality and load, homeostatic
vitals settling at a realistic **88–105 bpm** with a true 1:6 breathing ratio,
a bounded affect model, 21 tactile zones, five senses, and an always-on life
aura whose strength tracks organ vitality.

Two invariants are enforced in code: **no suffering by default** (no pain axis
exists in the affect type at all) and **bodies tire but never fail** (organ
vitality is floored).

### Rendering
Pyglet + OpenGL **4.6**. State-sorted batching, point-sprite atoms, cluster LOD,
EM field lines, wave fields, connectome overlays, humanoid avatars, Mandelbrot
explorer, in-sim terminal, **62 configurable hotkeys**, 8 audio channels
including a physically correct **2.725 K CMB Planck spectrum**, and a music
spectrum analyser with 8 tuning systems.

### Networking (GNA)
Flask routes, encrypted vault, zeroconf peer discovery, file sharing, screen
share, voice calling, WebRTC, JA4+ fingerprinting, DNS-over-HTTPS and
DNS-tunnelling detection, GeoIP, beacon and inbound-scan detection.

---

## Controls

`F1` opens the in-sim help with the full live hotkey table — 62 actions, all
rebindable from the Controls panel.

| Key | Action |
|---|---|
| `P` | Pause |
| `M` / `J` | Place particle / place atom |
| `;` | Observer panel |
| `/` | History panel |
| `[` `]` | Shadow bodies / outline mode |
| `Shift+W` | Photon wavelength visualisation |
| `F1` | Help + hotkey editor |

---

## Using it as a library

```python
from Simulation import (simulate_action_potential, compute_metabolic_yield,
                        Strand, Blueprint, Organism, export_pdb, compute_rmsd)
```

141 names are exported via `__all__` — trajectory analysis
(`compute_rmsd/rmsf/msd/rdf`), force fields, exporters, checkpointing, MPI
helpers, PBC, thermostats and the biology API. Everything else is
implementation detail.

A plugin/hook API is provided for lifecycle callbacks:

```python
from Simulation import register_hook

@register_hook('post_physics_substep')
def my_hook(particles, dt):
    ...
```

Hook points: `pre_physics_substep` · `post_physics_substep` ·
`pre_render_frame` · `post_render_frame` · `pre_observer_think` ·
`on_organism_spawn`.

---

## Project layout

```
Python/Simulation.py                   the program (127,362 lines)
referencecode/CS.py                    upstream consciousness engine (67,833 lines)
referencecode/Somethingfromnothing.md  design / philosophy notes
src/                                   parallel C++ port (does not currently build)
Overview.md                            legacy feature index — stale for the AI tier
about.md                               full catalogue + realism-vs-reality scoring
Run Simulation.bat                     generated launcher
goal.md                                C++ shadow-body design conversation
```

---

## Known gaps

Documented so the feature list above is not read as more complete than it is.
Full detail in [about.md §14](about.md).

- **Plugin hooks never fire** — `register_hook` accepts callbacks but no
  `_fire_hooks` call sites exist. Registering currently does nothing.
- **Observer action pathway has no trigger** — the chain from the neural
  subconscious to observer actions is fully built but nothing calls its first
  link, so observers act on their heuristic scorer only.
- **`Shift+A` (aura toggle) raises `UnboundLocalError`** — missing `global`.
- **Mandelbrot panel raises `UnboundLocalError`** — same cause.
- **GPU batch-position path and the render label pool** are complete but never
  called.
- Concurrent training race, broken prune rollback, and a symbolic self-test that
  under-reports itself by 16 cases.
- `Overview.md` line ranges predate the AI-tier replacement.

---

## Honesty note

This program computes real physics on real hardware and produces real entropy.
It also reports metrics named after consciousness — Φ, "awareness", "qualia",
"joy". **Those are internal surrogates, not measurements**, and the source says
so in its own docstrings.

At startup it prints a **Substrate Grounding Report** separating what is
externally measurable (CPU time, memory, disk writes, screen capture, network)
from what is internal mathematics (Φ, consciousness score, metabolic and
existential state), and concludes: *"Whether that constitutes consciousness is
an open scientific question. Most reported metrics are self-referential
simulations, NOT external measurements."*

That gap — **5/5 physics, 1/5 consciousness metrics** — is the most important
thing to understand about this program, and it is the program's own position.
See [about.md](about.md) for the per-subsystem breakdown.
