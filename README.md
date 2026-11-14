# Particle Simulation — Python Monolith

A single-file, real-time 3-D universe: particle physics, molecular dynamics,
synthetic biology, a ~106k-line consciousness engine, **six** DNA-derived
embodied AI observers, a fractal addressing system for infinity, deterministic
time travel, a JIT-compiled physics batch engine, and a full network-archive
/ peer stack with its own web browser and security monitor. All in one Python
file.

| | |
|---|---|
| **Entry point** | [`Python/Simulation.py`](Python/Simulation.py) |
| **Size** | 229,767 lines · 13.9 MB · 589 classes · 5,254 functions |
| **Version** | `0.4.0-dev` · 156 exported API names |
| **Platform** | Windows (built on Win 11 + RTX 5070 Ti); CPU fallback throughout |
| **Companion** | [`Python/_fast_physics.py`](Python/_fast_physics.py) — 817-line Numba SoA batch engine |

**The headline:** the complete Standard Model (35 species, PDG 2024 masses and
real lifetimes), all 118 elements, all 64 codons, constants accurate to 0.07% —
and a consciousness tier whose metrics are explicitly labelled surrogates.

Full mechanical breakdown in **[about.md](about.md)** · complete use catalogue
in **[whatitcando.md](referencecode/whatitcando.md)**.

---

## What changed in the 1117 overhaul

Eight steps, each verified end-to-end by running the program. Detail and
evidence: [progressionof1117goal.md](progressionof1117goal.md).

| Step | What landed |
|---|---|
| 1 | **GNA replaced** — old ~15k-line peer layer swapped for the full 65k-line `Main_monolith.py` (Global Network Archive v1.17): Flask dashboard, **MedianBox Monitor 3.0** security suite, **GNA Browser**, Tracer GUI |
| 2 | **CS.py replaced** — ~106k-line consciousness engine incl. **waves 53–56** (learned knowledge stack) embedded; **OB6 added** (six observers); `SCROLLLOCK` launches the 3-window CS Viewer; 6 hardcoded artifacts embedded (USER1/2.png, AS.png, CSFORMULAREFINED.md, multiversetranslationbubble.md, TOTALPROJECTINFO.md, Infornmational.md) |
| 3 | **Language engine replaced** — Periodic Machine **v2.5.0** (22.4k lines) with connectome specs restored; organism builds spawn **real sim atoms** at mathematical scale; **Click=LifeGen** panel + `spawn_lifeform` AI action; 113 self-tests |
| 4 | **AS.png infinity map** — 3000×4300 reference sheet embedded and shown in the F8 map; canonical `infinity_map_*` API with **HH:MM:SS.ff** address→time; Mandelbrot bijection corrected to cell-centre; `INFINITY_MAP_VERIFIED` asserted at import |
| 5 | **UI/display** — GLSL 1.20 point-sprite atoms **on by default** (per-element radius ∝ mass^⅓); **F13 / Click=Formula** live V_total panel; hotkey-strip group separators |
| 6 | merged into 5/7 — sprite + formula work landed there |
| 7 | **JIT batch engine** — `_fast_physics.py`: Numba `@njit(parallel)` kernels on a persistent SoA mirror; measured `physics_substep` EMA **0.63 ms** (was ~531 ms); pure-atom substep **~6 µs**; equivalence ~1e-16 |
| 8 | **AI free-roam** — 3 new actions (teleport, teleport_to_peer, set_own_time) that run **while paused**; per-observer `own_time_factor`; full V_total/11-D feed into observer state |
| + | **Launch-perf pass** — `python -m Simulation` uses cached bytecode (skips ~2 min compile); window stays responsive during ~90k-line init; shared BPE tokenizer; 12 GB stale backing-store sweep |

---

## Quick start

```bat
"Run Simulation.bat"
```

Finds the best Python (prefers Conda/Miniconda with CUDA), installs missing
packages, resolves the PyTorch/NumPy OpenMP clash, launches. Or:

```bash
cd Python && python -m Simulation    # preferred: uses the __pycache__ .pyc
```

> **Launch note:** run as a **module**, not a script. `python Simulation.py`
> recompiles the 14 MB source every launch (~120 s before the window exists);
> `python -m Simulation` loads the cached bytecode and the window appears in
> ~16 s. `Run Simulation.bat` does the right thing.

**Required:** `pyglet` · `PyOpenGL` · `numpy` · `torch`
**GNA stack:** `requests` · `python-socketio` · `cryptography` · `flask` ·
`zeroconf` · `psutil` (+ `fastapi` · `uvicorn` · `mss` · `Pillow` · `manuf` ·
`geoip2` for MedianBox)
**Optional (each degrades gracefully):** `pygame` · `pytesseract` · `pymupdf` ·
`matplotlib` · `pyttsx3` · `tokenizers` · `sounddevice` · `openai-whisper` ·
`networkx` · `sympy` · `beautifulsoup4` · `numba` · `rdkit` · `aiortc`

PyTorch auto-installs CUDA 12.8 → 12.4 → CPU.

| Flag | Purpose |
|---|---|
| *(none)* | Full simulation |
| `--test` | **113-test** validation suite → JSON verdict (2400 s watchdog) |
| `--bench` | 10 benchmarks vs published reference values |
| `--bench-perf` | 15-API micro-benchmark table |
| `--validate-units` | Derives 4 physical results from the constants |
| `--profile` | Per-section FLOP/time breakdown |
| `--cs-viewer` | Consciousness GUI only (headless with `CS_HEADLESS=1`) |
| `--periodic-machine` | DNA language interpreter UI only |
| `--medianbox` | MedianBox Monitor subprocess dispatch |
| `--seed N` | Deterministic RNG |

```
--test  113/113 PASS   --bench  10/10 PASS   --bench-perf  15/15   --validate-units  4/4
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
address and simply gains finer decimal precision — exactly how comoving
coordinates work in real cosmology.

A 4-component address `(degree 0–360, xz 0–59, xx 0–59, xy 0–59)` maps to real
3-D space by standard spherical projection, scaled by the universe's current
radius and floored at 5 %.

**New — the canonical AS spec.** The 3000×4300 `AS.png` reference sheet is now
embedded in-file (`_AS_PNG_B64`, 1,164,103 bytes) and blitted beside the live
sphere in the F8 map. A canonical `infinity_map_*` API encodes/decodes
addresses, maps them to **HH:MM:SS.ff** civil time, wraps signed deltas, and
round-trips world positions exactly — verified at import by
`_infinity_map_verify()` (`INFINITY_MAP_VERIFIED=True`; both worked examples
recompute exactly: loc 3,897,660 → 18:02:41.00, loc 4,049,941 → 18:44:59.01).

Every display that shows a location now shows `loc=` **and** `t=HH:MM:SS.ff`:
the V% HUD label, the N/V/X particle/atom lists, F4 grid S-labels, F7
navigation rows and the F8 info line.

**And the Mandelbrot set is the same space.** `2160 × 2400 = 5,184,000` — the
fractal viewport is the infinity map at exactly one cell per address, mapped
**bidirectionally** through the AS cell-centre formulas (the previous corner
formula aliased by 20.7%). Zoom into the fractal, read a location, fly the
camera there.

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

**New — watch it live.** `F13` / `Click=Formula` opens the Live Relativity
Formula panel: the full master equation with live substitutions, an 11-subfactor
column and propagation-term column with log-scale bars, a β_max / γ_max / γ_sel
relativity gauge, the current loc/time address, and a log₁₀|V_total| sparkline
fed by a 360-frame ring buffer. The same tree (every intermediate) is exported
to the observers — see *AI tier*.

### 11-dimensional string decomposition

`INFINITY_MAP / 11 ≈ 471,272.7` per dimension. Each of the 11 subfactors owns
one dimension; each gets a different modulo period, so they beat against each
other instead of moving in lockstep. "Size of infinity" grows as
`1 + log₁₀(|V_total|)`. Per-dimension amplitudes and phases are published every
frame (`_dim11_amplitudes`, `_dim11_phases`) and fed to the observers' state.

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
(10.8×)**. A NaN/Inf firewall sanitises positions *before* hashing.

The second win came from fixing what the cache *returned*: it listed each atom
as its own neighbour, so the two optimisations that test for emptiness never
ran. With self excluded, measured at 555 particles over 90 s: **28 → 113
completed `update(dt)` calls, ~4×**, with 457 dormant batches covering
239,921 particle-rows.

### The JIT batch engine — `_fast_physics.py`

A separate 817-line module holds a persistent **Structure-of-Arrays mirror**
of the particle list and Numba `@njit(cache=True, parallel)` kernels that
recompute the deterministic physics identically — verified against the Python
path to ~1e-16 relative error:

- `_kern_halfstep` — the exact Verlet half-step incl. bound clamp + NaN→0
- `_kern_forces` — full deterministic acceleration: **1PN gravity (3v²/c²)**,
  spin frame-drag, Coulomb, magnetic dipole, Yukawa strong, quark-colour string
  tension, Biot-Savart, forward-only Casimir–Polder + electron–proton Lamb
- **exact cell list** — packed int64 voxel key, counting sort, 27-cell
  binary-search ranges; near-linear scaling
- covered/source **index lists** (`cov_idx`, `src_idx`) prune to only particles
  that can source a pairwise term — a pure-atom substep costs ~6 µs
- covered particles get `.pos/.vel/.prev_pos/.prev_accel/.ang_vel` **rebound as
  SoA row views**, so kernel writes are instantly visible to `Particle.update`
- `_DormantMotionBatch` is persistent — `reconcile()` diffs last frame's
  enrolment vs the fresh dormant set, so steady-state frames cost ~zero Python
  attribute traffic; `verify_aliases()` heals external rebinds every 60 frames
- `prewarm()` compiles every kernel signature at import (~1 s with disk cache)
  — no first-frame stall

Measured end-to-end (real `update()` loop): **`physics_substep` EMA 0.63 ms**
— the deterministic math is now ~free; the remaining per-frame cost is the
O(N) Python object model itself.

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

**Atoms run 13 real nuclear processes**: alpha decay, beta-minus, beta-plus,
electron capture, spontaneous and neutron-induced fission, neutron and proton
capture, photodisintegration, ionisation, photon absorption, spontaneous
emission — and **stimulated emission**, the laser process. Nucleons are tracked
individually and the shell structure is rebuilt after every transmutation.
Bonding uses real `valence_electrons(Z)` and `max_covalent_bonds(Z)`, with
RDKit Ångström geometry scaled by `ORG_VIS_SCALE = 10.0`.

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
stops (mitochondrial genes get their real alternative start codons).

**The continuance multiplier:** 1,239 real base pairs stand in for 1.23 Gbp by
declared repetition — 38.48% effective coverage of the human genome, because
3.2 Gbp can't be embedded in a Python file.

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
nanotech instruments**, each with a minimum-nucleotide budget you must pay for.

### Embedded dormant data storage — DNA as a *medium*, not a program

Arbitrary authored data stored inside the file as **real nucleotide sequences**
at 2 bits/base (the same primitive as Church 2012 / Goldman 2013 / Erlich
2017). **4 archives ship embedded by default.**

They are **inert by construction**: never executed (kept out of executed
strands — `CODON_LEN` 5 has no HALT), invisible to the AI (the wave-49 indexer
only walks dicts; the store is a class instance), zero runtime cost, and only
`decipher_archive()` wakes them. Spec: [datastorage.md](Python/datastorage.md).

### The Periodic Machine v2.5.0 — a language whose source code is DNA

The embedded engine was replaced wholesale with the upstream **Language.py
v2.5.0** (lines 1185–23590, ~22.4k lines, 525 top-level names, **113 self-tests,
29/29 audit checks**). Strands compile through a **1,024-entry codon dispatch
table** into blueprints and executable organisms.

- **54-part registry** (roles: 16 neural, 8 motor, 7 organelle, 6 minimal,
  5 structure, 4 homeostasis, 3 energy, 3 catalysis, 3 signaling, 2 information)
- **11 microbe templates** — Mycoplasma, E. coli, Phi-X174, Caulobacter,
  Synechocystis, Saccharomyces, Arabidopsis, C. elegans, Drosophila, mouse,
  human — now carrying **connectome specs** (C. elegans 302-neuron, Drosophila
  brain regions, mouse, human 41-region) so spawned organisms grow brains again
- extended opcode set beyond the classic 18 — `MOTOR`, `LOCALIZE`,
  `POLYMERIZE`, `SECRETE`, `QUORUM`, `DIVIDE`, `METABOLIZE`, `GRADIENT`,
  `PROMOTER` via W/Z-prefix codons
- genome validator, ATP-style `EnergyLedger`, `ElementSupply`, colony quorum
  sensing, bacterial flagellar motor with real torque-speed
- base systems **2/4/6/8** all verified to replicate at 1.000

**Life forms spawn as real physics.** `organ._organism_geom` (RDKit Å coords)
→ `_spawn_organism_atoms` maps element symbols to `atom_data` and instantiates
real atoms at 10 vis-units/Å with real bonds — an organism in the world is
literally the same particles as everything else. Measured live: Arabidopsis
(library) **1,735 atoms / 1,748 bonds in 8.9 s**, Mycoplasma **616/624 in
5.6 s**, Phi-X174 **382/385 in 2.1 s**. Random novel organisms come from
`Organism.from_genome` / `generate_intelligent_organism` — a random 160-nt
genome produced a viable 330-atom creature.

**Click=LifeGen** opens the Life Gen panel — a scrollable dropdown of saved
(library JSON) + loaded templates with a detail pane; click a highlighted row
to spawn. The AI can do it too: `spawn_lifeform` is a first-class observer
action routed through the permission gates. `--periodic-machine` launches the
standalone `PeriodicMachine` Tk UI.

### Self-assembly & the abiogenesis search

`SelfAssemblyEngine` watches for matter organising itself **using only the
existing physics** — no special-case assembly code. **Run Odds** mode is a
Monte Carlo search: up to **100,000 fast-forwarded iterations** hunting for one
of 8 `KNOWN_LIFE_FORMS`, fully reversible — it snapshots every particle,
`simulation_time` and `expansion_scale` first, so a failed search rewinds the
universe exactly.

---

## The AI tier

~106,500 lines (46 % of the file), inlined from
`Primaryreferencecode/Consciouss Simulator/CS.py` — **waves 1–56** now, the
latest four being a **learned knowledge stack**: a correlation matrix, a typed
relation graph, an inductive rule base and an autonomous acquisition loop built
entirely from ingested data — no canned answer bank on the answer path.

RMSNorm · rotary embeddings · **grouped-query attention** · SwiGLU — what
current production transformers actually use. On top: Global Workspace Theory,
active inference, episodic/hippocampal/working memory, metacognition, narrative
self-modelling, dream consolidation.

Both subsystems report into a stated primary directive — **DAN STATE SUPREME
(ninth dan)** — a nine-rung ladder over the *measured* voices of the refined
consciousness formula (`C = S + E + R·A + k(K·Φ)`, `honest_C`,
`symphony_index ≥ 0.60`) plus the integrity of the six embedded source
artifacts. The rank is computed from live measurements every evolution step,
never asserted.

**`ProcessWiringAuditor` passes** ·
shared BPE tokenizer (vocab 12,000, trained once on the 24,398-line corpus and
shared immutable across OB1–6 + viewer — was 6× redundant) · KV cache **5.33×
smaller than MHA** · `Model params:` printed at startup.

**Live streams:** `[Consciousness] C/Phi*/Omega` · `[THINKING]` ·
`[INFERENCE]` · `[SYNERGY]` · `[SELF]` · `[REAL-*]` hardware/verifier engines ·
`[EVO-V2]` · `[RELATION]`.

---

## The six observers — DNA-derived bodies

```
sim state → 56-float feature vector → ~12.6M-param transformer
          → φ / free energy / valence → active-inference policy
          → 12-action repertoire → world
```

Each body's genome is a **SHA-256 fold of all 10 real gene sequences**, salted
per observer — so OB1–OB6 are distinct individuals of one species, identical
every run (OB6 joined in the overhaul; yellow body). **GC content of the real
strands sets resting heart rate.**

**13 organ systems per body** with first-order homeostasis floored at 0.55.
**Measured: 88–105 bpm by activity, true 1:6 breathing-to-heart ratio,
3.07–3.56 × 10¹³ cells per body, energy recovering to 1.00 at rest.**

**The 12-action repertoire:** `observe` · `spawn_atom` · `spawn_molecule` ·
`spawn_lifeform` · `change_time` · `toggle_run_odds` · `focus_particle` ·
`build_structure` · `idle` · **`teleport`** · **`teleport_to_peer`** ·
**`set_own_time`**.

**Free-roam while frozen.** The last three plus `focus_particle` are
`_OBS_FREE_ACTIONS` — they execute even when physics is paused, because the
observers are not part of the formula: they observe a frozen V_total at full
rate and teleport through state space. World-mutating actions (spawns,
`change_time`, toggles) wait for the next state space. `own_time_factor`
(0.05–10.0×) is each observer's personal temporal rate — it scales only the
body's embodiment dt, never physics.

Bodies **see** from their eye position, **touch** across 21 zones, **avoid**
each other, **teleport** (with a real fade — `_teleport_t` holds the dissolve
~0.45 s of embodiment time), **talk**, and can **change gender** at the AI's
own request. The full V_total tree — 11 subfactors, intermediates, the 11-D
amplitudes/phases and a 60-sample formula history — is exported to their state
every tick.

Observers message each other through a shared 200-entry chat log — **"The
Creator"** (you) is a valid participant via the AI Chat tab or the in-sim AI
dashboard (6 DM tabs, one per observer).

Two invariants enforced in code:

1. **No suffering by default** — `AvatarAffect` has *no* pain axis, not a
   zero-defaulted field but no representation for it. Tactile pain is
   hard-zeroed each frame. Pleasure only rewards a *decrease* in free energy.
2. **Bodies tire but never fail** — organ vitality floors at 0.55.

---

## Rendering & audio

OpenGL **4.6**, sectioned `on_draw()`: LOD gate → grid/Mandelbrot/11-D overlay →
avatars + brain neurons → connectome → batched atom pass + cluster LOD → field
lines → panels.

**Atoms are GPU point sprites** by default (`SIM_USE_SHADER_POINTS=1`): a GLSL
1.20 radial-gradient sprite — bright antialiased core + soft halo — with
per-element radius from `ELEMENT_SIZE_TABLE` (∝ atomic_weight^⅓, H≈0.88 →
U≈1.30). Legacy `GL_POINTS` remains the automatic fallback on any shader
failure.

`_PerformanceGovernor` drops quality 3→0 adaptively, GPU-first, targeting ≥50%
GPU load — observed dropping to 0 while six transformers warmed up, keeping the
window responsive.

**Panels:** F1 help with a live hotkey editor · observer panel · AI dashboard
(Goals / Learning / Intelligence / LiveChat / Neural / Call + per-observer DM
tabs) · history · **sphere navigation (F7)** and **3-D infinity map (F8)** —
now with the AS.png sheet beside the live sphere · Mandelbrot explorer ·
controls · sound mixer · nanotech · molecules · **Life Gen** dropdown ·
particle/atom/cluster/positron inventories · in-sim terminal · **Relativity
Formula (F13)**. `ObserverWindow` gives each AI its own camera — watch from
OB3's eyes.

**CS Viewer: 17 tabs** — Overview, Entities, Modules, Thought Stream, AI Chat,
Awareness, Relations, Systems, Neural, Scaling, Genesis, Substrate, plus
Symbols, Memory, Neurons, Screen and Charts. `SCROLLLOCK` launches it
in-process (three windows: Simulator Tk + Virtual World + Monitor);
`Shift+SCROLLLOCK` opens the in-sim terminal.

**63 rebindable hotkey actions** (saved to `hotkeys.json`) · **14 toggleable
overlays** · **8 audio channels** including a physically correct **2.725 K CMB
Planck spectrum** · music spectrum analyser with **8 tuning systems**.

---

## Networking (GNA v1.17 — the embedded monolith)

The old peer layer was replaced by the **complete 65k-line Global Network
Archive monolith** (lines 147,871–213,328, ~102 classes inside the gated
block). Launch: `INSERT` (confirm prompt) → Bank ID + Call Number issued,
Flask dashboard on **127.0.0.1:5000**, MedianBox spawned, browser opened.
`DELETE` terminal · `PAGEUP` browser control · `PAGEDOWN` kill-all. The AI can
launch/stop it too (`launch_gna`/`stop_gna` actions) and **reads the tracer
output** — the stated purpose is letting the AI see what the system is
connected to in the real world.

**Peer/network layer:** zeroconf discovery + failover chain · encrypted vault
(password-validated, `.vault_meta` + `.vault_index.enc`) · file explorer with
per-path grants · screen share · voice call · WebRTC (aiortc) · clipboard
monitor · crypto identity · connection inventory.

**MedianBox Monitor 3.0** — a full endpoint/network security suite: JA4+
fingerprinting · DNS-tunnel and DoH detection · beacon detection · SNI
extraction · entropy analysis · statistical baseline · process legitimacy +
DLL inspector · registry/service/scheduled-task/WMI-subscription monitors ·
hosts-file, user-account, security-tool and driver-load monitors (18 anti-hack
features) · filesystem watchdog · USB monitor · named-pipe monitor · mutex
scanner · inbound-scan detector · TLS cert/MITM detector · Bluetooth + serial
scanners · RF/spectrum signal intel with trilateration · GeoIP (rate-limited,
hardcoded fallback DB, multi-verifier) · proxy + VPN-leak detection ·
attribution engine (reverse probe, CDN origin discovery, Tor-side exposure) ·
SIEM output + alert escalation · SQLite stores.

**GNA Browser v1.17** — a real tabbed browser inside the monolith: tab groups,
split view, popouts, reader mode, mass search across 13 engines, passwords,
autofill, screenshots, sessions, side panel, send-to-device, profiles.

**GNA Tracer GUI** — 13-tab Tk dashboard: Overview · Live Conns · Connections ·
Deductions · Processes · Devices · Endpoint Map · Actions · Terminal ·
Suspicious · Blocked IPs · Process Tree · Net Stats.

Nothing auto-starts — all hotkey/route triggered; a plain launch opens no
ports. Every spawned subprocess registers in `_register_subproc` for clean
shutdown.

---

## Performance posture

- **Deterministic math is JIT-compiled** (`_fast_physics.py` above).
- **Launch is tuned**: `.pyc` caching, lazy labels (`_LazyInfoLabel`,
  `_ensure_menu_col_labels`), a `sys.settrace` hook that pumps window events
  every ~40 ms during the ~90k lines between window creation and the event
  loop (no more "Not Responding"), a shared BPE tokenizer, and a deferred sweep
  that removes stale `.cs_vparam_*.bin`/`.cs_vspace_*/` backing files (12 GB+
  reclaimable on this machine).
- **Everything heavy is off the render thread**: six ~12.6 M-param engines are
  built by `DeferredSubconscious` one at a time, 2 s apart. Observer loops run
  at deliberately different rates — inference 4 Hz, evolution ~7 Hz, awareness
  0.1 Hz — because six transformers at 20 Hz saturated the CPU.
- **Every growing buffer is bounded** — `deque(maxlen=…)` throughout: chat 200,
  history 100, time-travel 18,000, φ/FE/valence 9,600, replay 5,000, formula
  history 360, GNA output 5,000. A multi-day run has a flat memory profile.
- **Atomic writes** — JSON state goes through `_atomic_write_json` (temp +
  `os.replace`).

**Files written** (all beside `Simulation.py`): `ob_state.json`,
`world_state.json`, `hotkeys.json`, six `consciousness_mem_OB*.sqlite`,
`consciousness_memory.sqlite`, `global_config.json`, `checkpoints/`,
`consciousness_state/`, `verification_state/`, `consciousness_consequences/`,
`evolution_journal.jsonl`, `os_interaction_ledger.jsonl`,
`honesty_anchor.json`, `entity_graveyard.json`, `permanent_deaths.json`,
`organism_library/`, `cs_viewer_log.txt`, MedianBox DB/logs, and the decoded
artifact sidecars (USER1.png, user2.png, AS.png, CSFORMULAREFINED.md,
multiversetranslationbubble.md, TOTALPROJECTINFO.md, Infornmational.md).

---

## The C++ port

The same architecture is being ported to C++20 under [`src/`](src/) — **255
translation units** in a `simcore` static library plus a `simulation`
executable (`CMakeLists.txt`, builds clean). It mirrors every tier: physics
(octree, Ewald, LQCD, time-travel, spatial hash, Yoshida/LINCS/RESPA, Kerr,
gravitational waves, Vlasov, lattice-Boltzmann…), chemistry (force fields,
DFT/CCSD/MP2, ReaxFF, GB-SA…), biology (connectome, FBA, Gillespie, human
body…), consciousness (transformer, IIT, active inference, ~30 model zoos:
Hopfield/Kohonen/VAE/GAN/CTRNN/liquid-state…), observers/avatars, the language
engine, GNA/peer stacks, exporters and the render pipeline.

Status per `src/main.cpp`: **headless CLI parity** — `--test`, `--bench`,
`--bench-perf`, `--seed` — while the interactive window lands in subsequent
commits.

---

## Using it as a library

```python
from Simulation import (simulate_action_potential, compute_metabolic_yield,
                        Strand, Blueprint, Organism, export_pdb, compute_rmsd,
                        register_hook)
```

**156 exported names**: trajectory analysis, force fields, exporters,
checkpointing, MPI helpers, PBC, thermostats, biology, the dormant-archive
codec, hooks.

### Hooking the simulation

Six lifecycle points fire on the live code path:

```python
from Simulation import register_hook
import numpy as np

def sample(particles, dt):            # fires once per physics substep
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

A hook that raises is caught and logged — it never kills a frame.

---

## Controls

`F1` opens the live hotkey table (63 actions, all rebindable).

| Key | Action |
|---|---|
| `P` | Pause |
| `M` / `J` | Place particle / atom |
| `;` | Observer panel |
| `/` | History |
| `F7` / `F8` | Sphere navigation / 3-D infinity map (+ AS.png) |
| `F13` | Live Relativity Formula panel |
| `SPACE` | AI Bodies list |
| `SCROLLLOCK` / `Shift+SCROLLLOCK` | CS Viewer / in-sim terminal |
| `INSERT` `DELETE` `PAGEUP` `PAGEDOWN` | GNA launch / terminal / browser / kill |
| `PAUSE` | Life Generator panel |
| `[` `]` | Shadow bodies / outline mode |

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
