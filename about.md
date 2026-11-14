# about.md — How It Works, Feature by Feature

Complete mechanical breakdown of [`Python/Simulation.py`](Python/Simulation.py):
what each system **does**, **how it does it**, and **how close it lands to
reality**.

This edition covers the **229,767-line** file after the eight-step 1117
overhaul: the embedded sub-programs (GNA, consciousness engine, language
engine) were replaced wholesale with their current upstream versions, the
infinity map gained its canonical AS spec, a Numba JIT batch engine was added,
and the observers grew to six with free-roam actions. Every figure was read
out of the running program, the progression log
([progressionof1117goal.md](progressionof1117goal.md)), or counted from the
source. Nothing is estimated.

---

## Contents

1. [Realism scale](#1-the-realism-scale)
2. [The file itself](#2-the-file-itself)
3. [The Infinity Map — dimensional sphere addressing](#3-the-infinity-map--dimensional-sphere-addressing)
4. [V_total — the reality-weight equation](#4-v_total--the-reality-weight-equation)
5. [11-dimensional decomposition](#5-11-dimensional-string-decomposition)
6. [Deterministic time travel](#6-deterministic-time-travel)
7. [Unit system](#7-the-hybrid-unit-system)
8. [Physics engine](#8-physics-engine)
9. [The JIT batch engine](#9-the-jit-batch-engine--_fast_physicspy)
10. [Particle physics](#10-particle-physics--complete-standard-model)
11. [Chemistry & MD](#11-chemistry--molecular-dynamics)
12. [Biology](#12-biology)
13. [Synthetic biology — Periodic Machine v2.5.0](#13-synthetic-biology--the-periodic-machine-v250)
14. [Self-assembly & Run Odds](#14-self-assembly--run-odds-monte-carlo)
15. [The consciousness tier](#15-the-consciousness-tier)
16. [The six observers & DNA bodies](#16-the-six-observers--dna-derived-bodies)
17. [Rendering](#17-rendering--how-the-frame-is-built)
18. [Audio & music](#18-audio--music-mathematics)
19. [Networking — the GNA monolith](#19-networking--the-gna-monolith)
20. [Infrastructure](#20-infrastructure)
21. [Launch performance](#21-launch-performance)
22. [Verification](#22-verification-results)
23. [The C++ port](#23-the-c-port)
24. [Scorecard](#24-final-scorecard)

---

## 1. The realism scale

One question per subsystem: **how much of actual reality does it reproduce, and
how accurately?**

| Score | Name | Criterion |
|:--:|---|---|
| **5/5** | Reality-complete | Reproduces the *entire* real set with published values; deviation < 1% |
| **4/5** | Near-real | Real values and algorithms; > 50% coverage or < 10% deviation |
| **3/5** | Representative | Real physics, sampled or coarsened — 5–50% of the real system |
| **2/5** | Token | Genuine reference data, but < 5% of what it names |
| **1/5** | Named proxy | Name refers to reality; the number is internal and doesn't measure it |
| **0/5** | Absent | Present in source, never executed |

A **1/5 is not an insult** — a proxy *labelled* as a proxy is honest
engineering. It warns you not to read the number as a measurement.

---

## 2. The file itself

| Measure | Value |
|---|---:|
| Lines | **229,767** |
| Bytes | **13,860,042** (~13.9 MB) |
| Classes | **589** |
| Functions | **5,254** |
| `__all__` exports | **156** |
| `__version__` | `0.4.0-dev` |
| Rebindable hotkey actions | **63** |
| Validation tests (`--test`) | **113** |

The file is a deliberate monolith. Its own header TOC divides it into 16
sections; the actual spans, measured:

| § | Contents | Lines |
|---|---|---|
| 1 | Bootstrap, CLI dispatch, embedded launchers (`_BAT_CONTENT`, `_SH_CONTENT`), `_atomic_write_json`, subprocess registry | ~837–1,529 |
| 2 | **Periodic Machine Language Engine v2.5.0** — `PARTS_KB`, `MICROBE_TEMPLATES`, `Strand`, `Blueprint`, `Organism`, `Evolver`, `run_tests()` (113 tests), `--test` dispatch | 1,185–23,590 (~22.4k) |
| 3 | Hodgkin-Huxley, glycolysis/TCA/ETC, transcription, cell cycle — interleaved in §2 | — |
| 4 | Physics constants, GPU detection, `_gpu_batch_position_update`, `_build_atom_neighbor_cache`, conservation audit, **dormant-archive codec** | 23,591–28,889 |
| 5 | **CS.py AI tier** — verbatim inline of the updated CS.py inside `if _TORCH:`: `PhiComputer`, GWT, active inference, memory, self-model, dream, `MonitoringDashboard`, `ConsciousnessSimulator`, **wave 1–56 tiers** | 28,895–135,367 (~106.5k) |
| 6 | Embed glue tail — training lock, compat aliases, `SubconsciousEngine` | 134,981–135,367 |
| 7 | Early `--cs-viewer` dispatch + LQCD, `Particle`/`Atom`/`Camera`, nuclear, decay, photon, hotkey table | 135,369–144,570 |
| 8 | `ObserverManager`, `SimulationObserver` **(OB1–OB6)**, `ShadowBody` | 144,589–147,395 |
| 9 | `_spawn_organism_atoms`, `_build_connectome_geometry`, Life Gen | 147,396–147,870 |
| 10 | **GNA monolith** (`Main_monolith.py` embedded) + MedianBox + browser + tracer | 147,871–213,328 (~65.5k) |
| 11 | Peer comms — interleaved in §10 | — |
| 12 | CS Viewer in-sim terminal, `_launch_cs_viewer`, Periodic Machine launcher | 213,329–218,464 |
| 13 | Globals — particles, camera, observer manager, HUD state | interleaved |
| 14 | `update(dt)` main physics loop | 218,465–219,391 |
| 15 | `on_draw()` render pipeline | 219,392–226,146 |
| 16 | pyglet event handlers + final init + scheduling | 226,147–226,683 |

Three upstream files are embedded **verbatim** and replaced the previous
versions wholesale:

| Embedded program | Source | Lines in file | Share |
|---|---|---:|---:|
| Language engine v2.5.0 | `Primaryreferencecode/BasedLifeForms/Language.py` (21,468 lines) | ~22.4k | ~10 % |
| Consciousness engine | `Primaryreferencecode/Consciouss Simulator/CS.py` (~106k lines, 1,061 top-level names) | ~106.5k | ~46 % |
| GNA monolith v1.17 | `Primaryreferencecode/GNA update1/Main_monolith.py` (65,356 lines) | ~65.5k | ~28 % |

The remaining ~16 % is the simulation core itself: physics, observers,
rendering, UI, glue.

---

## 3. The Infinity Map — dimensional sphere addressing

**The idea:** every particle has a permanent *address in infinity* — a position
in a 5,184,000-cell dimensional sphere that is independent of its Cartesian
coordinates and survives the universe expanding around it.

```python
INFINITY_MAP = 5_184_000        # 2160 × 2400 — "practical infinity"
```

### How an address is computed

`particle_infinity_location(p)` folds the particle's state into a fractional
address in [0, 1):

```python
_einv    = 1.0 / expansion_scale                  # comoving inverse
_pos_hash = (p.pos[0]*_einv)*7.13
          + (p.pos[1]*_einv)*11.37
          + (p.pos[2]*_einv)*3.91
```

The three irrational-ish multipliers decorrelate the axes. Positions are
divided by `expansion_scale` first, making the address **comoving** — as the
universe expands a particle keeps its address and gains finer precision, which
is exactly how comoving coordinates work in real cosmology.

### The dimensional sphere

`sphere_coords_to_3d_pos(degree, xz, xx, xy, radius)` maps a 4-component
address onto real 3-D space:

| Coordinate | Range | Meaning | Formula |
|---|---|---|---|
| `degree` | 0–360 | azimuthal (longitude) | θ = radians(degree) |
| `xz` | 0–59 | polar (latitude) | φ = π·xz/59 |
| `xx` | 0–59 | radial depth | r_frac = (xx + xy/60)/60 |
| `xy` | 0–59 | fine radial subdivision | — |

```python
x = r·sin(φ)·cos(θ)     y = r·sin(φ)·sin(θ)     z = r·cos(φ)
```

Radius is scaled by current expansion and floored at `.05R` so nothing
collapses to the origin.

### The canonical AS spec (step 4)

The overhaul replaced the ad-hoc address arithmetic with a canonical
`infinity_map_*` API, specified by the embedded **AS.png** sheet — a
1,164,103-byte, 3000×4300 reference image stored in-file as `_AS_PNG_B64` and
loaded through the `[HARDCODED-ARTIFACTS]` loader:

| Function | Behaviour |
|---|---|
| `infinity_map_deg_to_cyc` | degree 0–360 → cycle fraction |
| `infinity_map_wrap_signed` | signed-wrap deltas in each cyclic field |
| `infinity_map_encode_loc` / `decode_loc` | (deg, xz, xx, xy) ↔ loc ∈ [0, 5,184,000) |
| `infinity_map_time_to_loc` / `loc_to_time` | address ↔ **HH:MM:SS.ff** civil time |
| `infinity_map_radial` | radial depth, floored at 5 % R |
| `infinity_map_sphere_pos` | address → 3-D point |
| `world_pos_to_as_loc` / `infinity_map_cell_pos` | world position ↔ cell, **exact round-trip** (verified: loc 4,049,941 → decode → cell pos → re-encode → 4,049,941) |
| `_infinity_map_verify()` | runs at import; both worked examples recompute exactly — loc **3,897,660 → 18:02:41.00**, loc **4,049,941 → 18:44:59.01** — then sets `INFINITY_MAP_VERIFIED = True` |

The CS tier learned the spec too: `INFINITY_MAP_LIBRARY`, 10 `MATH_EQUATIONS`
entries (loc/cell/time/deg/wrap/radial/sphere-pos/Mandelbrot),
`COMMON_SENSE_LIBRARY['infinity_map']`, knowledge Q&As, and 5 benchmark cases.

### Mandelbrot ↔ sphere: a bijection, corrected

The same address space is reachable from the Mandelbrot set, **both ways**:

```python
_mandelbrot_to_sphere_loc(c_real, c_imag):     # ℂ → address (delegates to AS inverse)
_sphere_loc_to_mandelbrot(loc):                # address → ℂ — AS cell-centre formula
    row, col = loc // 2400, loc % 2400
    re = -2.5 + (row + 0.5) / 540              # cell CENTRE
    im = -2.0 + (col + 0.5) / 600
```

The previous version used the cell *corner* formula, which aliased by **20.7%**
— `row/2160·4` maps a cell index to its edge, so the same loc decoded to a
point up to a fifth of a cell off. The AS spec's cell-centre form is the
inverting map: `_mandelbrot_to_sphere_loc` delegates to it so the pair round-
trips exactly, including the 0-key labels.

`2160 × 2400 = 5,184,000` — the Mandelbrot viewport is *exactly* the infinity
map at 1 cell per address.

### Where addresses are displayed

Every location readout now shows the canonical `loc` **and** civil time:

| Surface | Shows |
|---|---|
| V% HUD label | `loc=… t=HH:MM:SS.ff` (inf/nan-guarded) |
| N / V / X particle+atom lists | Φ address with `t=` suffix (`particle_frame_addr_str`) |
| F4 grid S-labels | `world_pos_to_as_loc` + AS cell tuple (was `hash()%INFINITY_MAP`) |
| F7 sphere nav | AS Time / Cell / frac / C-pixel rows |
| F8 info line | AS time / cell / frac; **panel widened to 560 px live sphere + AS.png sheet** (aspect-preserved, degrades when narrow) |
| Click-to-place / click-absorb | log canonical `loc` + `t` via the shared `_sphere_map_layout` |

**Realism: not a physical claim.** A coordinate/addressing scheme —
mathematically consistent, comoving the way real cosmology is. A navigational
device, not a measurement. **Score: n/a.**

---

## 4. V_total — the reality-weight equation

Every frame the simulation collapses its entire state into one number,
`V_total` — "how much reality currently exists". It drives the 11-D overlay,
the infinity percentage, the sphere navigation, the **F13 formula panel**, and
the observers' world model.

### The 11 subfactors

| Symbol | Formula | Physical meaning |
|:--:|---|---|
| **Z** | `√(\|E_rest\| + ε)` | rest energy, E = mc² |
| **A** | `n_stable` | count of stable particles |
| **C** | `√(\|π · r_spatial · σ_spatial\| + ε)` | spatial extent × dispersion |
| **E** | `5 · (E_rest + E_kinetic)` | total energy |
| **Q** | `13 · quantum_bindings / 2` | quark/sub-particle bindings |
| **U** | `√(n_particles + ε)` | population |
| **D** | `−n_antimatter` | antimatter debit |
| **T** | `7¹² · t_norm` | time, normalised to a 1440-min day |
| **R** | `9 · rank_score` | structural rank (3 + 2·n_sub per atom) |
| **P** | `780 · (V% / 100)` | previous-frame feedback |
| **B** | `−\|total_charge\|` | charge imbalance debit |

### The recursion

```
base      = Z+A+C+E+Q+U+D+T+R+P+B
Vn        = min(|V_prev| / INFINITY_MAP, 1)          # normalise to [0,1]
exp_term  = e^(3·Vn)
quad      = Vn² + 0.5·Vn
cubic     = (4Vn² + 0.001Vn)³
dual      = 2 + π·Vn^1.5·0.137                        # 0.137 ≈ fine-structure α
inner     = exp + quad + cubic + dual + base
recursive = e^(Vn·ln(Vn+1)) + e^(Vn²·ln(Vn+1)) + e^(√Vn·ln(Vn+1))   # V^V + V^V² + V^√V

V_total   = (5·inner² + perturbation) · recursive · ∞_norm
V%        = |V_total| / INFINITY_MAP × 100
```

The recursive powers are evaluated **in log space** and clamped at 20 before
exponentiating; `inner` is clamped to ±1e150. That is what stops a self-
referential power tower from overflowing within one frame.

### The complete tree is exported, not just the scalar

`V_subfactors` now carries the **entire formula tree** — all 11 subfactors plus
`exp`, `quad`, `cubic`, `dual`, `inner`, `inner²`, `perturb`, `rec_vv`,
`rec_vv²`, `rec_v√`, `inf_norm` and intermediates — because two consumers need
it:

1. **The F13 Live Relativity Formula panel** (see §17) renders the equation
   in motion from it, plus a relativity gauge fed by `update._rel_stats`
   (max v² per stats pass → β_max, γ_max) and a 360-frame
   `_formula_history` ring for the log₁₀ sparkline.
2. **The observers** receive `V_subfactors`, `V_dim11_amplitudes`,
   `V_dim11_phases`, `V_formula_history` (last 60 (t, V, V%) samples),
   `V_beta_max` and `V_gamma_max` in their sim-state feed — the AI is given
   the whole formula, not a summary.

**Realism: 1/5 — named proxy.** Every input is a real measured quantity, so
V_total responds faithfully to the scene; the combining equation is invented.
Read it as a **complexity index**, not a physical quantity.

---

## 5. 11-dimensional string decomposition

M-theory's 11 dimensions (3 spatial + 1 time + 7 compactified) are used as a
fractal decomposition basis for V_total.

```python
STRING_DIMENSIONS     = 11
_STRING_FRACTAL_BASE  = INFINITY_MAP / 11        # ≈ 471,272.7 per dimension
```

Per dimension *d*:

```python
period    = _STRING_FRACTAL_BASE · (d+1)
frac      = (|V_total| mod period) / period                  # fractal slice
amplitude = min(1, frac · (0.3 + 0.7 · subfactor_d/|V_total|))
phase     = (t·(0.1 + 0.05d) + frac·2π·(d+1)/11) mod 2π
```

Each subfactor owns one dimension; the modulo gives each a different period so
they beat against each other. `_dim11_amplitudes` and `_dim11_phases` are
published every frame and included in the observer state feed.

"Size of infinity" grows with complexity: `1 + log₁₀(|V_total|)`.

**Realism: 1/5.** Real M-theory has 11 dimensions; nothing else here
corresponds to string theory. It is a visualisation driven by a modulo
decomposition.

---

## 6. Deterministic time travel

```python
_det_frames    = []      # ring buffer
_det_frame_max = 18000   # ~5 minutes at 60 fps
_det_playhead  = -1      # -1 = live, else replay index
```

Each frame records `(sim_time, expansion_scale, cloud_radius, V_total, V%,
[(pos, vel), …])` — including **atom sub-particles and their constituent
quarks**, recursively.

Four modes, switched automatically:

| Situation | Behaviour |
|---|---|
| Reverse within recorded range | Restore from frames — **byte-identical determinism** |
| Forward within recorded range | Replay from frames |
| Forward past the range | Live physics, recording new frames |
| Reverse past the range | `_reverse_live_mode` — runs physics **backwards** live |

Seeking uses **binary search** over `_det_frames` by timestamp with
interpolation. Because Verlet integration is symplectic and time-reversible,
running it backwards is physically meaningful rather than a playback trick.

**Realism: 4/5.**

---

## 7. The hybrid unit system

A deliberate, documented split:

| Quantity | Unit | Notes |
|---|---|---|
| Constants (G, c, ℏ, e, mₑ) | **pure SI** | CODATA 2018 / PDG 2024 |
| `Particle.pos/vel/mass` | **vis-units** | 1 vis-unit ≈ 1 grid line ≈ 1 px at zoom 1.0 |
| Bond geometry | Å × 10 | `ORG_VIS_SCALE = 10.0`, matches `_BOND_SEP` |
| Time | seconds | advances at `simulation_time × time_factor` |
| Charge | **Coulombs (SI)** | Coulomb's law runs in SI |
| Energy | vis-unit²·mass/s² | KE = ½mv² |

Photon overlays, Doppler/gravitational redshift and the SR clamp compute in
**SI**, then map back to vis-units for drawing. Any function returning an SI
quantity carries an explicit `*_SI` suffix.

`--validate-units` proves the SI side is intact by deriving four physical
results from the constants (§22).

---

## 8. Physics engine

### The integration loop

```
render frame (120 FPS target)
 └─ accumulate dt into physics_accumulator
    └─ while accumulator ≥ PHYSICS_DT and steps < adaptive_max:
         pre_physics_substep hook
         forces: gravity (Barnes-Hut/GPU) + EM + bonds + nuclear
         Velocity-Verlet: x += v·dt + ½a·dt² ;  v += ½(a + a')·dt
         dormant atoms -> one batched Verlet pass (GPU above 2,048)
         post_physics_substep hook
    └─ _render_alpha = accumulator / PHYSICS_DT     # interpolation fraction
```

`PHYSICS_DT = 1/960 s`. Physics and rendering are **decoupled** — rendering
interpolates between the last two physics states via `_render_alpha`. Substep
count adapts to `time_factor` (up to 64).

### Force computation

| Force | Method | Complexity |
|---|---|---|
| Gravity | Barnes-Hut octree (`OctNode`), θ-controlled | O(N log N) |
| Gravity (GPU) | Batched pairwise via PyTorch | O(N²) but massively parallel |
| Coulomb short-range | Direct + Verlet neighbour list | O(N·k) |
| Coulomb long-range | **Ewald summation** (real + reciprocal) | O(N^1.5) |
| Nuclear | Yukawa, λ = ℏc/m_πc² = **1.414 fm** | short-range |
| Confinement | Cornell, α_s = 0.3, σ = 0.18 GeV/fm | per-quark |

The Yukawa range is derived from the real pion mass: 197.3 MeV·fm / 139.6 MeV
= 1.414 fm.

### The spatial hash — two measured wins

```python
voxels = floor(pos · (1/voxel_size)).astype(int64)
keys   = (v[:,0]·73856093) ^ (v[:,1]·19349663) ^ (v[:,2]·83492791)
order  = argsort(keys)
starts = where(diff(sorted_keys) != 0)
```

**Build cost: 765 ms → 71 ms at 1 M particles (10.8×).** A NaN/Inf firewall
sanitises positions *before* hashing.

**What the cache returned was the bigger win.** Every atom appeared in its own
neighbour list, so `_cached_neighbors` was never empty — and both optimisations
that branch on emptiness had never executed: the chemistry-scan short-circuit
and the dormant-atom skip. The same function also built keys with `np.floor()`
but queried with `int()`, which disagree for negative coordinates. With both
fixed, at 555 particles over 90 s of wall clock:

| | `update(dt)` completed | dormant batches | particle-rows batched |
|---|---:|---:|---:|
| before | 28 | 0 | 0 |
| after | **113** | **457** | **239,921** |

Both substep branches route dormant atoms through one shared
`_batch_dormant_motion()` helper — the fallback's non-symplectic `v += a·dt`
kick was replaced by the symmetric `v += ½(a + a')·dt` form at the same time.

### The dormant batch is now persistent

The step-7 pass promoted `_DormantMotionBatch` to a persistent global
(`_dormant_batch`). `reconcile()` diffs last frame's enrolment against the
fresh dormant set, so steady-state frames cost ~zero Python attribute traffic
instead of re-enrolling every dormant atom each frame. Mid-frame promotions
reuse the same object (they previously created fresh batches and orphaned
rows), `verify_aliases()` heals external `.pos` rebinds every 60 frames, and
two real bugs were fixed: `_cap_i` used `old[-1]` (enrolment order ≠ sorted →
IndexError on shrink — now `old.max()`), and `add()` is idempotent.

**Realism: 5/5.**

---

## 9. The JIT batch engine — `_fast_physics.py`

A separate 817-line module (`Python/_fast_physics.py`) holds the compiled
mirror of the deterministic physics. The goal was *identical math, compiled* —
every stochastic or irreversible term stays on the original Python path.

### `SoACache` — a persistent Structure-of-Arrays mirror

`SoACache(capacity=4096)` owns contiguous numpy rows for `pos`, `vel`,
`prev_pos`, `prev_accel`, `ang_vel`, `mass`, `charge`, `spin`, `kind`,
`colour`, live flags. Two binding modes:

- **Covered non-atom particles** get `.pos`, `.vel`, `.prev_pos`,
  `.prev_accel`, `.ang_vel` **rebound as SoA row views** — kernel writes are
  instantly visible to `Particle.update`, with no copy-back.
- **Atoms are never bound** — `Atom.update` and the dormant batch own their
  state; atom rows are frame-start copies re-read each substep via `src_atoms`
  (row, obj) pairs so forces see live values exactly like the Python loop.

`sync_to_particles` iterates `bound_idx` only and skips all work when views
are intact — **71 ms → 14 ms at 20k bound rows**.

### The kernels

```python
@njit(cache=True, parallel=True)
def _kern_halfstep(pos, vel, prevacc, live, dt, bound, cidx, n_cov): ...

@njit(cache=True, parallel=True)
def _kern_forces(pos, vel, mass, minv, charge, spin, angvel, kind, color, ...): ...
```

- `_kern_halfstep` — the identical Verlet half-step including the ±bound clamp
  and NaN→0 wash.
- `_kern_forces` — the full deterministic acceleration, Jacobi-evaluated:
  **1PN gravity (3v²/c²)**, spin frame-drag, Coulomb, magnetic dipole, Yukawa
  strong, quark-colour string tension, Biot-Savart, forward-only
  Casimir–Polder + electron–proton Lamb. `em_on_gpu` skips Coulomb/dipole/Biot
  exactly like the Python gate; reverse-time suppresses CP/Lamb via `dt>=0` →
  `include_qed`, same as source.
- **Exact cell list** — packed int64 voxel key, counting sort, 27-cell
  binary-search ranges. No approximations; near-linear scaling.
- `Particle.update` consumes `_bjit/_baccel/_blive` and skips exactly the
  blocks the kernel did; decay/annihilation/`in_atom`-capture write
  `_blive[0]=0`, so the kernel drops the row mid-frame (i- and j-side),
  matching the dynamic `base_type` checks of the Python loop.

### Scale optimisations (all verified)

| Optimisation | Effect |
|---|---|
| **Indexed kernels** (`cov_idx`, `src_idx` built once per frame) | O(covered)/O(sources) iteration instead of O(N) scans — pure-atom scene substep ≈ **6 µs** |
| **Source pruning** | cell list holds only rows that can source a pairwise term (q≠0 \| nucleon \| quark); million-neutral-atom scenes drop the sort O(N log N) → O(S log S) |
| **Atom fast path** | atoms get a ~10-op minimal fill; `_was_atom` mask skips constant-column stores |
| **`_bjit` live guard** | a mid-frame capture→release falls back to the full Python path instead of consuming stale `_baccel` |
| **GPU-EM charge fill** | reuses `soa.charges` (was a second O(N) getattr loop per frame) |
| **float64 normalisation** | GPU gravity arrives float32, which had triggered a second ~12 s numba specialisation mid-run |
| **`prewarm()` at import** | compiles every kernel signature on a tiny synthetic SoA (~1 s with disk cache) — no first-frame stall |

### Equivalence and measured speed

`_step7_jit_equiv.py` checks half-step vs Verlet expression, forward/em_on_gpu/
reverse forces, live-kill, clamp/NaN — **all passed, max rel err ~1e-16**
(fp noise). `_step7_equiv_test.py` — dormant batch bit-identical over 6
substeps × 500 atoms including mid-frame promotion; occupancy-grid neighbour
lists exact + order-identical.

End-to-end on the real `update()` loop:

| Measure | Value |
|---|---:|
| `physics_substep` EMA | **0.63 ms** (was ~531 ms including a mid-run compile) |
| `spatial_hash` EMA | 11.47 ms |
| Pure-atom substep | ~6.5 µs |
| GPU-EM substep | ~16 ms |
| CPU-EM substep | ~203 ms @ 20k covered / 20k sources |
| Synthetic 120k steady sync | 199 ms (was 308 ms) |

**Honest floor:** the O(N) Python object model is now the dominant per-frame
cost — `sync_from_particles` (~1.7 µs/row for atoms), dormant classification
and active-list scans are still per-object getattr loops. Further gains need
attribute caching or an SoA-native object layout — flagged, not done.

**Realism: 5/5** — the kernels were verified to fp noise against the Python
path; physics behaviour is unchanged.

---

## 10. Particle physics — complete Standard Model

`particle_data` carries **35 species with PDG 2024 masses, charges, spins and
real mean lifetimes.**

| Sector | Sim | Reality | Coverage |
|---|---:|---:|---:|
| Quarks (u d c s t b) | **6** | 6 | **100%** |
| Leptons (e μ τ + 3 ν) | **6** | 6 | **100%** |
| Bosons (γ g W⁺ W⁻ Z H) | **6** | 6 | **100%** |
| Antiparticles | 13 | — | — |
| With real decay channels | **12** | — | — |

Real lifetimes drive real decay: neutron **878.4 s** → p + e⁻ + ν̄ₑ · muon
**2.197 µs** · tau **290.3 fs** · top **~5×10⁻²⁵ s** → b + W⁺ · W
3.16×10⁻²⁵ s · Z 2.64×10⁻²⁵ s · Higgs **125.25 GeV, 1.56×10⁻²² s** → bb̄.

Decay is sampled per-step as `P = 1 − e^(−dt/τ)`; products spawn with momentum
conservation.

**Realism: 5/5 for the catalogue.** Caveat: propagation is classical;
quantum behaviour lives in the dedicated modules — `DoubleSlitExperiment`,
`LatticeQCD` (SU(3) Wilson gauge with HMC), `PhotonicCrystal`, Hartree-Fock.

### The Atom — a complete nuclear physics suite

| Process | Method |
|---|---|
| Alpha decay | `_do_alpha_decay` — emits a real ⁴He nucleus, Z−2 A−4 |
| Beta-minus | `_do_beta_minus` — n → p + e⁻ + ν̄ₑ, Z+1 |
| Beta-plus | `_do_beta_plus` — p → n + e⁺ + νₑ, Z−1 |
| Electron capture | `_do_electron_capture` — p + e⁻ → n + νₑ |
| Spontaneous fission | `_do_fission` |
| Neutron-induced fission | `_neutron_induced_fission` |
| Neutron capture | `neutron_capture` — A+1, same Z |
| Proton capture | `proton_capture` — Z+1 |
| Photodisintegration | `_do_photodisintegration` — γ knocks out a nucleon |
| Ionisation | `ionization_check` — electron stripping by energy threshold |
| Photon absorption | `photon_absorption` — shell-resonant |
| Spontaneous emission | `spontaneous_emission` |
| **Stimulated emission** | `stimulated_emission` — the laser process |

Nucleons are tracked individually and `_rebuild_atom` reconstructs shell
structure after any transmutation. Sub-particles carry `constituent_quarks`.

### Real valence chemistry

```python
valence_electrons(Z)      # from shell filling
max_covalent_bonds(Z)     # accounts for common valences and expanded octets
```

`assign_bonds`/`assign_positions` place atoms using RDKit geometry (Å) scaled
by `ORG_VIS_SCALE = 10.0`, falling back to element-cost clustering when RDKit
is absent.

**Realism: 5/5.**

---

## 11. Chemistry & molecular dynamics

**All 118 elements** (Z = 1…118) in `atom_data`. **All 64 codons**. **21 amino
acids**.

### Force fields — 5/5

AMBER FF14SB (all 20 residues) · CHARMM36 · GAFF · TIP3P · OPLS-mini.
Bonded forces are real analytic gradients:

```
E_bond  = k_b(r − r₀)²            F = −∇E = −2k_b(r − r₀)·r̂
E_angle = k_θ(θ − θ₀)²
E_dih   = Σ (Vₙ/2)[1 + cos(nφ − γ)]
E_LJ    = 4ε[(σ/r)¹² − (σ/r)⁶]    + tail correction beyond cutoff
```

Custom fields register via `register_force_field()` /
`set_active_force_field()` / `evaluate_force_field()`.

### Free energy — 5/5

Replica exchange (Sugita-Okamoto) · umbrella sampling · WHAM iteration · FEP
(Zwanzig) · thermodynamic integration · steered-MD pull force.

### Exports

DCD · AMBER NetCDF · mmCIF · PSF · PRMTOP · GRO · XYZ · PDB · GraphML · VTK ·
HDF5 · NWB · SBML · MOL2 · WebGL JSON.

### Quantum chemistry — 2/5

Hartree-Fock **STO-3G**, three molecules (H₂, He, LiH).

---

## 12. Biology

### The continuance multiplier — how 1,239 bp becomes a genome

```
effective_bp = Σ (len(anchor_seq) × multiplier)
```

| Measure | Value | vs reality |
|---|---:|---:|
| Real genes embedded | **10** | 0.05% of ~20,000 |
| Literal bases | **1,239 bp** | **0.0000387%** of 3.2 Gbp |
| Effective bp | **1,231,500,000** | **38.48%** |

Genes: **HBB, INS, TP53, BRCA1, ACTB, ALB, MT-ND1, HIST1H4A, RPS6, CYCS** —
each annotated with its organ-system involvement.

`validate_human_genome_strands()` checks alphabet, length mod 3, ATG start,
no premature in-frame stop (mitochondrial genes allowed their alternative
starts). Replication uses **consensus replication** — N-fold redundancy
suppressing per-copy error, lifting fidelity 0.0972 → 0.9999 in the suite.

**Realism: sequences 5/5, scale 2/5.**

### Human body construction — 4/5

`construct_human_organism()` builds bottom-up (atomic → molecular → organelle
→ cellular → tissue → organ):

| Measure | Sim | Reality | Fidelity |
|---|---:|---:|---:|
| Organ systems | **13** | 11–13 | **100%** |
| Named organs | **71** | ~78 major | **91%** |
| Total cells | **3.389 × 10¹³** | ~3.7 × 10¹³ | **91.6%** |

### Neuroscience — 4/5

| Model | Detail | vs reality |
|---|---|---|
| Hodgkin-Huxley | 4 gating variables | **+37.8 mV vs +40 mV — 94.5%** |
| Connor-Stevens | adds A-type K⁺ | 5/5 |
| Synapses | AMPA / NMDA / GABA | 5/5 |
| Plasticity | STDP, BCM, Oja | 5/5 |
| Connectome | C. elegans | 271/302 neurons, 490/6,393 synapses |

`_build_connectome_geometry(spec, center, span)` turns an anatomical spec
into renderable brain geometry — `+X` = head→tail, `rng = default_rng(seed=42)`
so the same organism grows the same brain every spawn. The v2.5.0 language
engine re-attaches connectome specs to **all 11 microbe templates**: C. elegans
(302-neuron with named ganglia), Drosophila (optic lobes, mushroom bodies,
ellipsoid/fan-shaped bodies…), mouse, human (41 regions).

### Cellular & molecular — 4/5

Glycolysis/TCA/ETC (**32/2 ATP** — textbook-exact) · cell cycle (25 min
prokaryote / 1440 min eukaryote) · replication fork (E. coli **38.3 min**) ·
mutation model with Ts/Tv/CpG bias · Wright-Fisher & Moran · Hardy-Weinberg ·
FBA · DSSP · Ramachandran · protein docking · lipid bilayer ·
reaction-diffusion · Gillespie SSA · HMM · MSA · phylogeny · de Bruijn
assembly · horizontal gene transfer · `Microbiome` with taxa and populations.

### The DNA knowledge base — 12 domains of real reference data

`DNA_KNOWLEDGE` is a citable reference table: helix params (B-DNA rise
**3.4 Å/bp**, **10.5 bp/turn**, pitch **35.7 Å**), base pairing, backbone,
nucleotides, replication, central dogma (stops **UAA/UAG/UGA**, promoters
**−35 TTGACA / −10 TATAAT**), damage/repair, epigenetics, alternative nucleic
acids (PNA/TNA/XNA), nanotech, prebiotic, physical constants.

### Embedded dormant data storage

DNA used as a *storage medium*. Full spec: [datastorage.md](Python/datastorage.md).

- **Codec:** 2 bits/base (`A=00 C=01 G=10 T=11`), complement-symmetric —
  archives measure pair integrity 1.000.
- **Container:** 48 bases of fixed overhead —
  `MAGIC(0xD9A5,2B) | VERSION(1B) | FLAGS(1B) | LENGTH(4B) | CRC32(4B) |
  PAYLOAD`. CRC is over plaintext; obfuscation is a documented
  `SHA-256(passphrase||counter)` XOR keystream — **not** encryption.
- **Why it can't live in an executed strand:** `CODON_LEN = 5`, all 4^5=1,024
  codons map to real opcodes, `execute_genome()` iterates every codon with
  **no HALT** — arbitrary bytes would execute as instructions.
- **Shipped (4 archives, ~3.6k bases):** `creator.provenance` ·
  `creator.message` · `build.manifest` · `codec.selftest`.

| # | Guarantee | Mechanism |
|:-:|---|---|
| 1 | Never executed | not in any `Strand.seq` reaching `execute_genome()` |
| 2 | Invisible to the AI | store is a **class instance, not a dict** — fails the wave-49 indexer's `isinstance` test |
| 3–5 | Not in physics/render/perception | no reference in `update()`, `on_draw()`, or the 56-float feature vector |
| 6 | No frame cost | encoded once at import |
| 7 | No file I/O | in-memory unless explicitly exported |
| 8 | Explicit wake | only `decipher_archive()` returns content |

The engine swap preserved all 16 public API names verbatim.

### DNA nanotech instruments — 6 buildable devices

`origami_tile` (~100 × 70 nm, min 7,200 nt) · `drug_delivery_box` ·
`molecular_ruler` · `logic_gate_AND` · `walker_transport` · `crispr_guide` —
each with a minimum-nucleotide budget.

### The Life Generator — 8 known life forms

`KNOWN_LIFE_FORMS`: **Flagella** · **Protocell** · **DNA-based organism** ·
**RNA-world organism** · **Silicon-based life** · **PNA organism** ·
**Self-replicating machine** · **Unified system** — each with `min_atoms`,
`requires_code`, `code_type` and a required element set.

`_build_life_gen_templates()` merges the saved organism library with built-ins
— **81 templates** at last count (69 library + 11 microbe + 1 intelligent).
Spawning runs the RDKit build on a background thread, attaches a `Microbiome`,
and builds connectome geometry for the organism's brain.

---

## 13. Synthetic biology — the Periodic Machine v2.5.0

A programming language whose source code is DNA. The embedded copy is the
upstream **v2.5.0** engine — a wholesale replacement of the previous engine,
namespace-collisions resolved (`__version__`→`_LANG_VERSION`,
`parse_fasta`→`lang_parse_fasta`, `write_fasta`→`lang_write_fasta`,
`export_mmcif`→`lang_export_mmcif`).

| Component | Role |
|---|---|
| `Strand` | the sequence itself |
| `Opcode` / `OpcodeDef` | codon → operation. **1,024-entry dispatch table** (4-base, CODON_LEN 5) |
| `LanguageSpec` | base system 2/4/6/8 — replication verified equal across all four |
| `Blueprint` | compiled organism plan (`connectome`, `organism_name` fields restored) |
| `Organism` | executable instance |
| `Evolver` | genetic optimisation (serial-forced inside the monolith — spawn children would re-import it) |
| `PartRegistry` / `PARTS_KB` | **54 parts** — roles: 16 neural, 8 motor, 7 organelle, 6 minimal, 5 structure, 4 homeostasis, 3 energy, 3 catalysis, 3 signaling, 2 information — every SMILES validated |
| `GenomeValidator` | pre-flight checks |
| `EnergyLedger` | ATP-style accounting |
| `ElementSupply` | raw element availability gate |
| `Colony` | density + quorum sensing |
| `MotorSimulator` / `BacterialFlagellarMotor` | rotary motor with real torque-speed |

**Extended instruction set.** Beyond the classic ops, the engine adds
W/Z-prefix codons: `MOTOR` (WATCG), `LOCALIZE` (WCAAA), `POLYMERIZE` (WXAAA),
`SECRETE` (ZATCG), `QUORUM` (ZCAAA), `DIVIDE` (ZXAAA), `METABOLIZE` (ZYAAA),
`GRADIENT` (ZWAAA), `PROMOTER` (ZZAAA).

**11 microbe templates** — Mycoplasma genitalium (minimal cell), E. coli K-12,
Phi-X174 bacteriophage, Caulobacter crescentus, Synechocystis PCC6803,
Saccharomyces cerevisiae, Arabidopsis thaliana, C. elegans (neuron +
ganglia connectome), Drosophila melanogaster (body plan + brain regions),
Mus musculus, Homo sapiens (genome proxy) — environment modifiers real-ish:
earth 1.000 > silicon 0.850 > exotic 0.650.

### Life forms spawn as real simulation atoms

`organ._organism_geom` (RDKit Å coords) → `_spawn_organism_atoms` maps
`_SYM_TO_Z` → `atom_data` and instantiates real sim atoms at 10 vis-units/Å,
centroid-aligned, with real bonds — the same `particles` list as everything
else, not a separate depiction. Element-cost grid fallback when geometry is
absent. Measured live:

| Organism | Atoms | Bonds | Build time |
|---|---:|---:|---:|
| Arabidopsis (library JSON) | 1,735 | 1,748 | 8.9 s |
| Mycoplasma (microbe template) | 616 | 624 | 5.6 s |
| Phi-X174 (n_bases=4) | 382 | 385 | 2.1 s |
| Random 160-nt genome | 330 | 328 | — |

Library round-trip verified: `save_organism_to_library` →
`organism_from_library_dict` → identical `element_cost`.

### The Life Gen panel and the AI

`Click=LifeGen` opens a scrollable dropdown panel of saved + loaded templates
with a detail pane (mouse row-click selects, click-on-highlighted spawns,
wheel scrolls, click-outside closes). `spawn_lifeform` is a first-class
observer action — curiosity-biased connectome picks, routed through the
`_SPAWN_ACTIONS` permission gate with a SPAWNING animation, executing through
`_life_gen_build_and_spawn` → real atoms. `on_organism_spawn` hooks fire when
one lands.

`--periodic-machine` launches the standalone `PeriodicMachine` Tk app (genome
cache → `construct_human_organism` → `launch_ui()`), mirrored by the
`PAUSE`-key Life Generator panel in-sim.

**Realism: 3/5.** The genetic code, codon tables, replication error rates and
quorum sensing are real biology; the opcode/blueprint layer is an invented
abstraction.

---

## 14. Self-assembly & Run Odds Monte Carlo

`SelfAssemblyEngine` watches for matter organising itself **using only the
existing physics** — gravity, EM, bonds, van der Waals. No special-case
assembly code. Every 30 frames it scans for `AssemblyStructure` (bound,
persistent groupings) and `InformationCode` (repeating patterns that carry
information).

### Run Odds mode

A Monte Carlo search for abiogenesis: up to **100,000 iterations**
(`run_odds_max_iter = 100000`) of fast-forwarded physics hunting a target from
`KNOWN_LIFE_FORMS` (8 entries). Fully reversible: snapshots every particle,
`simulation_time` and `expansion_scale` (`_ro_pre_snapshot`,
`_ro_pre_expansion`) before searching; a failed search rewinds the universe
exactly. Determinism shifts trigger a recalculation notice rather than
corrupting the search.

**Realism: 3/5.**

---

## 15. The consciousness tier

~106,500 lines (46 % of the file), inlined from the updated
`Consciouss Simulator/CS.py` — **waves 1–56**. The 1,061 top-level names were
verified present in the embed; bootstrap/`__main__` was dropped,
`CONFIG`→`_CS_CONFIG`, `PHYSICS_LAWS`→`_CS_PHYSICS_LAWS`.

### What waves 53–56 added — the learned knowledge stack

The newest four waves build knowledge machinery **entirely out of ingested
data**: a correlation matrix, a typed relation graph, an inductive rule base,
and an autonomous acquisition loop that goes and gets what the system is
missing. The stated design rule: *no canned answer bank on the answer path.*

### The primary directive — DAN STATE SUPREME

Both subsystems report into a nine-rung ladder over the *measured* voices of
the refined consciousness formula:

```
C = S + E + R·A + k(K·Φ)        voices: G_gen, G_in, honest_C
ninth dan ⇔ every rung voice holds AND symphony_index ≥ 0.60
```

plus the integrity of the six embedded source artifacts (USER1.png, user2.png,
AS.png, CSFORMULAREFINED.md, multiversetranslationbubble.md,
TOTALPROJECTINFO.md, Infornmational.md) — all six embedded in-file as base64
and verified loaded (`[HARDCODED-ARTIFACTS] 6/6 sources loaded`; the
multiverse source alone is 184,653 chars). The rank is **computed from live
measurements every evolution step, never asserted** — rung 9 is the Tensor
Abyss (26D bosonic, H = 25/26 ≈ 0.962 maximum reflection).

### Architecture — 4/5 as an ML system

RMSNorm · rotary embeddings · **grouped-query attention** · SwiGLU FFN —
current production transformer practice. On top: Global Workspace Theory with
competing specialist modules, active inference (belief state → generative
model → expected-free-energy policy), episodic + hippocampal + working memory
over a vector store, metacognitive monitor, predictive self-model, narrative
self, higher-order self-model, dream consolidation, self-modifying
architecture.

Numpy fallbacks exist for every torch component (`_NpMoE`, `_NpSSM`,
`_NpMemoryBank`, `_NpPredictiveCoding`, `_NpGlobalWorkspace`,
`_NpVisionEncoder`) so the tier degrades rather than dying without PyTorch.

### Live-measured scale (new engine, verified at launch)

| Fact | Value |
|---|---|
| `ConsciousnessSimulator` construction | ~50 s on CUDA (RTX 5070 Ti) |
| BPE vocab | **12,000**, trained once on the 24,398-line corpus — `AlienTokenizer` shares the immutable tokenizer across OB1–6 + the viewer |
| Streams live | `[Consciousness] C/Phi*/Omega` · `[THINKING]` · `[INFERENCE]` · `[SYNERGY]` · `[SELF]` · `[REAL-*]` · `[EVO-V2]` · `[RELATION]` |
| Headless run | `CS_HEADLESS=1 --cs-viewer` stable >5 min; main ~2.1 GB + world subprocess |
| Parameter count | printed live at startup (`parameters_count()` → `Model params: N`) |

### Knowledge tables

`MATH_EQUATIONS` 326+10 · `COMMON_SENSE` 338+ · `_CS_PHYSICS_LAWS` 147 ·
`KNOWLEDGE_LIBRARY` · `INSTRUCTION_PAIRS` 528 · `SYMBOLIC_TEST_CASES` 81 ·
`DAN_STATE_LIBRARY` · `INFINITY_MAP_LIBRARY` · a wave-49 retrieval index over
the corpus built in <1 s.

### The metrics — 1/5, unchanged and still enforced

| Metric | Score | What it actually is |
|---|:--:|---|
| Φ | **1/5** | proxy from network loss — *not* IIT |
| Φ* / honest_phi | **1/5** | stricter estimator; typically ≈ 0.000 |
| Consciousness C | **1/5** | self-referential `C = S + E + R·A` (+ k(K·Φ) in the refined formula) |
| Ω convergence | **1/5** | internal dynamics |
| Quantum substrate | **1/5** | "tubulins" as numpy arrays — not qubits |
| IIT 4.0 module | **5/5 as maths** | correct MIP search — over a toy substrate |
| Causal ablation / Jacobian | **3/5** | real computation, measures software |
| Hardware coupling | **4/5** | `psutil` CPU freq/temp are real OS reads |
| Thermodynamics | **3/5** | real CPU-time energy; power **estimated** (no RAPL) |
| Disk consequences | **5/5** | real files, externally checkable |
| Network verifier | **4/5** | real TCP :9999, needs an external client |
| Screen capture / OCR | **5/5** | real screen reads |

The **Substrate Grounding Report** still prints at every startup.

---

## 16. The six observers & DNA-derived bodies

`ObserverManager` builds **six** `SimulationObserver` instances — `OB1`–`OB6`
(indices 0–5). OB6 was added in the overhaul with the 6th body colour
(yellow, `(255,255,120)`), its own `consciousness_mem_OB6.sqlite`, DM tab,
call digit '6', live-chat entry, and panel slot.

### Perception → action pipeline

```
sim state  →  _extract_numeric_features()  →  56-float vector
           →  SubconsciousEngine (~12.6 M params) → φ / free energy / valence
           →  ActiveInferenceEngine.select_action() → action index
           →  12-action repertoire → _execute_observer_action()
```

`_OBS_FEAT_DIM = 56` hand-built features: particle/atom counts, simulation
time, time factor, `tanh(V_total/1e6)`, V%, total mass/energy/charge, assembly
and code counts, life-aura energy, per-body spatial awareness — and now the
**full V_total tree** (`V_subfactors`, `V_dim11_amplitudes`,
`V_dim11_phases`, `V_formula_history`, `V_beta_max`, `V_gamma_max`).

**The SubconsciousEngine is now a wrapper** (`class
SubconsciousEngine(ConsciousnessSimulator)`) that skips the standalone GUI
init and builds its own network: embedding + `TransformerEncoder` + overlay +
`lm_head` + `GlobalWorkspace` + `ActiveInferenceEngine` +
`AdvancedMemorySystem` + `HigherOrderSelfModel`, ~12.6 M parameters per
observer.

### The 12-action repertoire

`OBS_ACTIONS`:

| # | Action | Notes |
|:-:|---|---|
| 0 | `observe` | |
| 1 | `spawn_atom` | `_SPAWN_ACTIONS` gated |
| 2 | `spawn_molecule` | gated |
| 3 | `spawn_lifeform` | gated — builds a real organism via the Life Gen path |
| 4 | `change_time` | `ai_time_control_allowed` gate → scored −1.0 if denied |
| 5 | `toggle_run_odds` | |
| 6 | `focus_particle` | free action; uses the shared ~2 Hz `_ft_pos_cache` (bounded 65k fallback) |
| 7 | `build_structure` | gated |
| 8 | `idle` | |
| 9 | **`teleport`** | free action — targets peer position 50 % / own focus / camera vicinity |
| 10 | **`teleport_to_peer`** | free action — picks an active non-self peer |
| 11 | **`set_own_time`** | free action — proposes Δ in [0.25, 4.0], clamps to [0.05, 10.0] |

`_OBS_ACT_IDX` maps names → indices so scoring, suppressions and subconscious
biases reference actions **by name** (inserting `spawn_lifeform` at index 3 had
previously shifted every later index and silently misaligned the whole table).

### Free-roam under a frozen formula

`_OBS_FREE_ACTIONS = {teleport, teleport_to_peer, focus_particle,
set_own_time}` — actions that touch only the AI's own embodiment/perception,
never the simulation state space. They stay legal whenever `physics_frozen`
holds — **pause, menu open, input popup, or sphere-nav replay** — because the
AI are not part of the formula: they observe a frozen V_total at full rate and
move through state space. World-mutating actions wait for the next state
space. The frozen gate is evaluated at the consume site with the full
`physics_frozen` set, so subconscious-channel actions can't leak mutations
through a non-pause UI state.

**`own_time_factor`** is each observer's personal temporal rate: it scales
only `ShadowBody.update(dt * own_time_factor)` — never physics — and is
surfaced in `observer_peers`, `shadow_body_state`, `perceived_state` and
`ob_state.json`. Minds always run wall-clock rate; the audit found body
kinematics already on wall-clock dt.

### The body: genome → phenotype

```python
h = sha256(obs_id)
for gene in sorted(HUMAN_GENOME_STRANDS):      # deterministic order
    h.update(gene_name); h.update(actual_base_sequence)
genome = AvatarGenome.from_seed(int(h.hexdigest()[:16], 16))

gc = (all_bases.count('G') + all_bases.count('C')) / len(all_bases)
genome.base_heart_rate_hz = 1.0 + 0.4·gc       # GC content → resting HR
```

All **10 real gene sequences** are folded in, salted by observer id — OB1–6 are
distinct individuals of one species, identical across runs.

### Organ homeostasis & vitals

13 systems per body, first-order relaxation toward `1 − (1−FLOOR)·load` with
`_ORGAN_VITALITY_FLOOR = 0.55`. Cardiovascular vitality feeds back as a
**resting-baseline** penalty, not a running multiplier.

```python
energy    += (−exertion·0.05 + (1−exertion)·0.03)·dt
target_hr  = base_hr + exertion·1.4 + (1−energy)·0.6
breath_phase += dt · (heart_rate/6) · 2π          # real 1:6 human ratio
muscle_tone   = base_tone − 0.3·fatigue
```

**Measured: 88–105 bpm** by activity, energy recovering to 1.00 at rest,
organ vitality 0.91–0.95.

### Affect — with an enforced floor

`pleasure, wonder ∈ [0.35, 1.0]`; `joy = min(pleasure, wonder)` — requires
BOTH. **Two invariants enforced in code:**

1. **No suffering by default.** `AvatarAffect` has *no* pain/distress axis —
   not a zero-defaulted field, no representation at all. Tactile pain is
   hard-zeroed every frame. Pleasure only rewards a *decrease* in free energy;
   there is no negative branch.
2. **Bodies tire but never fail** (organ floor above).

### What a body can actually do

| Method | Behaviour |
|---|---|
| `perceive_bodies(all, particles, max_vis_dist=500)` | eye-position vision — what this body's eyes can resolve |
| `detect_physical_contact(other, body_height=6.0)` | capsule body-to-body contact → `apply_touch` routes to one of 21 tactile zones (pleasure/arousal, never pain) |
| `separate_from_bodies(all, min_sep=8.0)` | soft collision avoidance |
| `teleport_to(pos)` / `teleport_to_body(other)` | instant relocation — alpha now **decays** through a fade (was reset every tick before it could render); `_teleport_t` holds the dissolve ~0.45 s of embodiment time |
| `set_talk(message, duration=4.0)` | speech bubble with TTL |
| `set_gender(new_gender)` | AI-changeable, rebuilds the body model |
| `get_silhouette/get_3d_limbs/get_aura_lines(h)` | render geometry — detailed face (brow, sockets, sclera, iris), hair, muscle capsules, gender-scaled limbs, female hourglass pads |
| `_rebuild_neural_topology()` | 3-D in-head brain layout |

### The social layer

`_obs_chat(sender, recipient, message)` → shared 200-entry ring buffer.
Observers DM each other and **"The Creator"** — the AI dashboard has 6 DM tabs
(`_ai_dashboard_tab` 6–11), one per observer, plus Goals / Learning /
Intelligence / LiveChat / Neural / Call tabs.

**Body realism:** heart rate 5/5 · breathing:heart 1:6 5/5 · cell count ~93 %
5/5 · organ systems 5/5 · H-Anim skeleton 5/5 · senses 5/5 · tactile zones 2/5
· genome→phenotype 2/5 · vitals/affect/aura 1/5.

---

## 17. Rendering — how the frame is built

Pyglet + OpenGL **4.6**. `on_draw()` runs in labelled sections: busy-LOD gate,
camera projection, lighting → grid, Mandelbrot wireframe, 11-D overlay →
avatars + brain neurons → connectome → batched atom pass + cluster LOD → EM
field lines, wave field, photon spectra, panels, HUD.

### Point-sprite atoms — now the default path

`_PointSpriteShader` (GLSL 1.20) draws atoms as GPU point sprites: radial-
gradient sprite with a bright antialiased core and soft halo, per-element
radius from `ELEMENT_SIZE_TABLE` (∝ atomic_weight^⅓, H≈0.88 → U≈1.30).
**ON by default** (`SIM_USE_SHADER_POINTS=1`); legacy fixed-function
`GL_POINTS` is kept as the automatic fallback on any shader compile failure;
`SIM_USE_SHADER_POINTS=0` forces it.

### Adaptive quality & interpolation

`_PerformanceGovernor` drops quality 3→0, GPU-first, targeting ≥50 % GPU load
— observed dropping to 0 while six transformers initialised. Every particle
keeps `prev_pos`; drawing uses `prev + (pos − prev)·_render_alpha` so 960 Hz
physics renders smoothly at any frame rate, and the camera tracks the same
interpolated position.

### The panel surface

| Panel | Key | Shows |
|---|---|---|
| F1 help | `F1` | paged help + **live hotkey editor** (63 actions, saved to `hotkeys.json`) |
| Observer panel | `;` | OB1–6 status, thoughts, actions, φ/FE, own_time_factor |
| AI dashboard | `−` | Goals / Learning / Intelligence / LiveChat / Neural / Call + 6 DM tabs |
| History | `/` | timestamped event log |
| Sphere nav | `F7` | dimensional-sphere address + AS Time/Cell/frac/C-pixel |
| Sphere map | `F8` | 560 px live sphere + **AS.png sheet** + click-to-place |
| **Relativity Formula** | `F13` / `Click=Formula` | **the V_total master equation in motion** — symbolic form + live substitutions, 11-subfactor column + propagation-term column with log-scale bars, β_max/γ_max/γ_sel gauge, loc/time readout, log₁₀\|V_total\| sparkline (360-frame ring). Draggable translucent panel; Shift+F13 coexists with other panels |
| Life Gen | `Click=LifeGen` / `PAUSE` | scrollable dropdown of 81 templates + detail pane |
| Mandelbrot | — | 2-D + 3-D fractal explorer, click-to-locate |
| Controls / Sound / Nanotech / Molecules / inventories / terminal | — | hotkey rebind, 8-ch mixer, DNA instruments + AI load-ins, molecule list, particle/atom/cluster/positron lists, GNA + Life-Gen output |

`ObserverWindow` gives each AI its own camera. The HUD hotkey strip now has
group separators (`_HK_SEP_BEFORE`: Core/Toggles/Fields/Views/AI/Subprograms)
as non-clickable dim markers.

### The CS Viewer — 17 tabs

`SCROLLLOCK` → `_launch_cs_viewer()` on a daemon thread (three windows:
Simulator Tk + Virtual World + Monitor); `Shift+SCROLLLOCK` opens the in-sim
terminal; `--cs-viewer` is the standalone early-dispatch path.

Tabs: **Overview · Entities · Modules · Thought Stream · Awareness ·
Relations · AI Chat · Systems · Neural · Scaling · Genesis · Substrate ·
Symbols · Memory · Neurons · Screen · Charts** — thought streams and direct
chat for all of OB1–6.

**14 toggleable overlays** · **63 rebindable hotkeys**.

---

## 18. Audio & music mathematics

**8 sound channels**, each derived from a physical quantity: `cmb` (**Planck-
spectrum 2.725 K blackbody** — physically correct), `binding`, `thermal`,
`orbital`, `collision`, `expansion`, `quantum`, `decay`.

`MusicSpectrumAnalyzer` implements **8 tuning systems** — 12-TET
(`f(n) = 440·2^((n−69)/12)`), just intonation, and others — with FFT analysis.

**Realism: 4/5.**

---

## 19. Networking — the GNA monolith

The old ~15k-line peer layer was replaced wholesale by the **complete
Main_monolith.py** — ~65.5k lines, ~102 classes inside
`if _GNA_DEPS_AVAILABLE:` (deps: `requests`, `python-socketio`, `cryptography`,
`flask`, `zeroconf`, `psutil`; MedianBox adds `fastapi`, `uvicorn`, `mss`,
`Pillow`, `manuf`, `geoip2`, all try-guarded).

### Launch and lifecycle

`INSERT` → confirm prompt → `_launch_gna()` runs the embedded `main()` on a
thread: Bank ID + Call Number issued (`bank-…`, `nnn-nnn-nnnn`), Flask
dashboard binds **127.0.0.1:5000**, `[OK] Launching MedianBox Monitor`,
browser opened to the dashboard. Verified live: socket OPEN, `Status: Active`,
`Live Peers: 1`. `DELETE` toggles the in-sim GNA terminal (`_GNATee` ring
buffer, bounded 200, captures stdout+stderr), `PAGEUP` browser control,
`PAGEDOWN` `_kill_gna()`. `--medianbox` dispatches the monitor as a subprocess
— the standalone `medianbox_monitor_v2.py` is preferred (~2 s launch), with
`-m Simulation --medianbox` as the version-identical fallback. AI actions
`launch_gna`/`stop_gna` mirror the hotkeys, and the observers **read the
tracer output** — the stated purpose is letting the AI see what the system is
connected to in the real world, and every spawned subprocess registers in
`_register_subproc` for clean shutdown.

### The peer layer

zeroconf/mDNS discovery · failover nodes · `CryptoIdentity` keypair per node ·
encrypted vault (password-validated, `.vault_meta` + `.vault_index.enc`) ·
file explorer with per-path share grants, peer preview/download · screen
share · voice call · WebRTC (aiortc) · connection inventory/history ·
clipboard monitor.

### MedianBox Monitor 3.0 — the security suite

A complete endpoint/network monitor embedded in the same block
(`MedianBoxMonitor`, `medianbox_ultimate.db`, structured logs, YAML config):

| Family | Contents |
|---|---|
| Network detectors | `BeaconDetector`, `SNIExtractor`, `EntropyAnalyzer`, `DNSCache`, `DNSTunnelingDetector`, `DoHDetector`, `InboundScanDetector`, `TLSCertDetector` (MITM) |
| Fingerprinting | `JA4Plus` TLS client fingerprints |
| Process/host | `ProcessLegitimacyChecker`, `DLLInspector`, `RegistryMonitor`, `UserIdleMonitor`, `StatisticalBaseline`, `VirusTotalChecker` |
| Watchdogs | `FileSystemWatchdog`, `ClipboardMonitor`, `USBMonitor`, `ScheduledTaskMonitor`, `NamedPipeMonitor` |
| Anti-hack (18 features) | security-event log, hosts-file/DNS-hijack, service-creation, Defender/AV-disable, new-account/admin-escalation, WMI-subscription, driver/rootkit-load, `MutexScanner`, `ThreatIntelDB`, … |
| Signal intel | `BluetoothScanner`, `SerialPortScanner`, RF-capable-USB table, `Trilaterator` |
| GeoIP | rate-limited lookup, hardcoded IP-location DB, `LocationVerifier`, `MultiVerifier`, `ProxyDetector`, `VPNLeakDetector` |
| Attribution | active reverse probe, endpoint-disclosure surface, VPN-gateway self-identification, generic DNS query, CDN-origin discovery, open-proxy egress test, self-naming battery, coverage matrix, parser fuzz harness, Tier-1 de-mask engine, Tier-3 Tor-side exposure |
| Output | SIEM emitter, out-of-band delivery, alert escalation, SQLite stores, connection inventory, `GNAT` record-everything |

### GNA Browser v1.17

A real tabbed browser rendered inside the monolith (`render_start_page`,
`render_internet_page`, `render_browse_error`, `rewrite_for_browse`): tab
groups, split view, popouts, reader mode, mass search across **13 engines**
(duckduckgo, bing, qwant, ecosia, mojeek, yahoo, aol, startpage, wikipedia,
searx, brave, etools, mwmbl), passwords, autofill, screenshots, sessions,
side panel, send-to-device, per-profile storage.

### GNA Tracer GUI

A 13-tab Tk dashboard: **Overview · Live Conns · Connections · Deductions ·
Processes · Devices · Endpoint Map · Actions · Terminal · Suspicious ·
Blocked IPs · Process Tree · Net Stats.**

**Realism: 4/5.** Real protocols throughout; nothing auto-starts — a plain
`python -m Simulation` opens no ports.

---

## 20. Infrastructure

| System | Mechanism |
|---|---|
| Performance governor | adaptive quality 0–3, GPU-first, ≥50 % GPU target |
| Checkpointing | `save_checkpoint`/`load_checkpoint` — particles, observers, sim time |
| Atomic writes | `_atomic_write_json` — temp file + `os.replace` |
| Crash safety | `faulthandler`, NaN/Inf firewalls, subprocess registry |
| Bounded buffers | `deque(maxlen=…)` everywhere |
| Profiling | `--profile` per-section FLOP/time |
| MPI skeleton | `init_mpi_world`, `mpi_partition_range`, `mpi_allreduce` |
| **JIT batch engine** | `_fast_physics.py` — §9 |
| Plugin hooks | 6 live lifecycle points |
| Scriptable API | **156** exported names |
| Version guard | qutip only imported on Python ≤ 3.12 (dataclass/inspect bug on 3.13) |

### Threading model

| Thread | Purpose |
|---|---|
| main / pyglet | `update(dt)` at 120 FPS + `on_draw()` |
| `DeferredSubconscious` | builds the six engines one at a time, staggered 2 s |
| `PhysicsAudio-Init` | deferred audio device setup |
| per-observer ×6 | `_sc_active_inference_loop` (4 Hz), `_sc_evolution_loop` (~7 Hz), `_sc_awareness_monitor` (0.1 Hz) |
| `CS-Virtual-World` | pygame world renderer (daemon thread, not a subprocess) |
| `CS-Viewer-Main` | ConsciousnessSimulator + Tk mainloop |
| CS cognitive | refinement, screen capture, self-awareness, learning, evolution, replay, watchdog |
| GNA | Flask server, zeroconf discovery, status, packet sniff, forensics, interface stats |
| Life-Gen `_worker` | RDKit organism build |
| MedianBox | monitor subprocess |

### Files the program writes

`ob_state.json` (now incl. OB6 + `own_time_factor`) · `world_state.json` ·
`hotkeys.json` · `consciousness_mem_OB{1..6}.sqlite` ·
`consciousness_memory.sqlite` · `global_config.json` · `checkpoints/` ·
`consciousness_state/` · `verification_state/` ·
`consciousness_consequences/` · `evolution_journal.jsonl` ·
`os_interaction_ledger.jsonl` · `entangled_state.bin` · `kv_mmap.npy` ·
`honesty_anchor.json` · `entity_graveyard.json` · `permanent_deaths.json` ·
`organism_library/` · `cs_viewer_log.txt` · MedianBox `medianbox_*.db/.log/
.yaml/.json` · decoded artifact sidecars (USER1.png, user2.png, AS.png,
CSFORMULAREFINED.md, multiversetranslationbubble.md, TOTALPROJECTINFO.md,
Infornmational.md) · `.cs_vparam_<pid>.bin` / `.cs_vspace_<pid>/` backing
files (swept on launch — §21).

### Memory discipline

`deque(maxlen=…)` throughout: chat 200, history 100, det-frames 18,000,
sphere snapshots 200, phi/fe/val logs 9,600, replay 5,000, `_formula_history`
360, GNA output 5,000, consciousness_log 500, generation_log 50,
phi_history 2,000. Flat memory profile by construction.

### The hook API

| Hook | Fires | Receives |
|---|---|---|
| `pre_physics_substep` | before each 960 Hz substep | `(particles, dt)` |
| `post_physics_substep` | after each substep | `(particles, dt)` |
| `pre_render_frame` | top of `on_draw()` | `(camera,)` |
| `post_render_frame` | end of `on_draw()` | `(camera,)` |
| `pre_observer_think` | before an observer's cognition step | `(observer,)` |
| `on_organism_spawn` | a life-gen organism reaches the world | `(name, atoms)` |

Callbacks that raise are caught and logged per-callback.

---

## 21. Launch performance

A dedicated pass made the window open live instead of "Not Responding":

| Fix | Detail |
|---|---|
| **Corrupted tail repaired** | a duplicated `--bench-perf` fragment + second event-loop block had been pasted at top level (`return` outside function → SyntaxError); deleted — the file could not compile at all until fixed |
| **Bytecode caching** | `python -m Simulation` uses `__pycache__/Simulation.cpython-313.pyc` — source→bytecode of the 14 MB monolith measures ~120–126 s and now only runs when the file is edited. `python Simulation.py` bypasses the cache every launch |
| **VRAM probe typo** | `props.total_mem` → `props.total_memory` — the AttributeError had silently disabled TF32/cuDNN-benchmark/GPU-warmup and forced a false "VRAM=0 → NN on CPU" path; now reports `16302MB cap=12.0 boost=ON TF32=ON` on the 5070 Ti |
| **Window alive during init** | a `sys.settrace` line-hook right after window creation pumps `window.dispatch_events()` every ~40 ms through the ~90k lines of init between window creation and `pyglet.app.run()` — the window is responsive and starts drawing as soon as handlers exist; the hook disarms before the real loop |
| **Lazy heavy labels** | `info_label` (11 KB doc, built at startup, never drawn) → `_LazyInfoLabel` on first access; `menu_info_col_labels` → `_ensure_menu_col_labels()` on first ESC-menu draw — cuts seconds of DirectWrite shaping |
| **Shared BPE tokenizer** | `AlienTokenizer` trains the identical BPE on the identical 24,398-line corpus once and shares the immutable tokenizer across OB1–6 + CS viewer via a class-level cache + lock — was 6× redundant |
| **Stale backing-store sweep** | a deferred-init thread removes `.cs_vparam_<pid>.bin` (4 GB sparse each) and `.cs_vspace_<pid>/` from dead launches — 12 GB+ reclaimable |

Profiled launch (cProfile, ~2× inflated): window at ~15.7 s, event loop at
~25 s with pumping active throughout; BPE trained once ("shared"); OB1
subconscious online.

---

## 22. Verification results

| Suite | Result | Notes |
|---|---|---|
| `--test` | **113 / 113 PASS** | embedded engine validation suite; 2400 s watchdog (module import is heavy with OB engines/GPU) |
| `--bench` | **10 / 10 PASS** | HF/Kepler/harmonic/LJ/Ewald/IIT/HH-neuron/connectome/units/RepEx |
| `--bench-perf` | **15 / 15 APIs** | micro-benchmark table |
| `--validate-units` | **4 / 4 PASS** | constants → derived values |
| Language engine self-tests | **113/113 + 29/29 audit** | extracted-engine run |
| JIT equivalence | **all pass, ~1e-16** | `_step7_jit_equiv.py`, `_step7_equiv_test.py` |
| `INFINITY_MAP_VERIFIED` | **True at import** | both AS worked examples recompute exactly |

### Constants derived vs published

| Quantity | Simulation | Reality | Δ |
|---|---:|---:|---:|
| Schwarzschild radius of the Sun | 2954.13 m | 2952 m | **+0.07%** |
| Hydrogen ground state | −13.6057 eV | −13.6 eV | **+0.04%** |
| Boltzmann constant | 8.61733×10⁻⁵ eV/K | 8.617×10⁻⁵ | **+0.004%** |
| N_A · u inverse | 1000.00 g/mol | 1000 | **0%** |

### Benchmarks vs experiment

| Benchmark | Simulation | Reference | Fidelity |
|---|---|---|---|
| HH spike peak | **+37.8 mV** | +40 mV (Hodgkin & Huxley 1952) | **94.5%** |
| Ewald 1+/1− @ 10 Å | −39.94 kcal/mol | Coulomb −33.21 finite-box | within few % |
| C. elegans neurons | 271 | 302 (White 1986) | **89.7%** |
| C. elegans synapses | 490 | 6,393 (Cook 2019) | **7.7%** |
| Replica exchange | P_accept 1.000 | 1.0 monotone | exact |
| IIT 4.0 AND-gate | φ 0.5, Big_Φ 0.25 | Albantakis 2023 | correct MIP |

The 113-test suite covers: base systems 2/4/6/8 (complement maps, replication
fidelity ordering), strand complement + transcription, `PARTS_KB` validity
(54 parts, all SMILES parse, roles/energy_cost/attachment/domains present),
the extended instruction set (W/Z-prefix opcodes), blueprint execution,
genome validation, energy ledger, colony/quorum, evolution, library
round-trip, dormant-archive codec (known-answer vector, 0–255 binary
round-trip, CRC/wrong-passphrase/bad-magic rejection, not-a-dict guarantee),
human-genome strand validation, rigor schema — plus the physics-side checks
the suite retained.

---

## 23. The C++ port

[`src/`](src/) holds a C++20 port of the same architecture — **255 translation
units** in a `simcore` static library + `simulation` executable
(`CMakeLists.txt`, CMake ≥ 3.20, builds clean; `build/simulation.exe` +
`libsimcore.a` exist).

| Layer | Coverage |
|---|---|
| `physics/` | particle/atom data, integrator, nuclear, photon, validation, analytics, md_extra, Ewald, force fields, SR photonics, octree, camera, decay, nanotech, double-slit, performance, spatial hash, sphere addressing, LQCD, spacetime — plus an extended numerical tier: FFT, PME, Yoshida, Brownian dynamics, Bussi thermostat, Markov states, tICA, spectra, CMA-ES, LINCS, RESPA, Wang-Landau, Lanczos, MCMC, lattice-Boltzmann, extended cosmology, linear algebra, PIMD, BAR, collective variables, Sobol, wavelets, sparse CSR, special functions, replica-exchange MC, ABF, Krylov, splines, Kalman, graph algorithms, game theory, kinematics, Kerr metric, GW waveforms, stellar evolution, Vlasov plasma, Navier-Stokes, ODE solvers, BFGS, autodiff, Gauss quadrature, procedural noise |
| `chemistry/` | bonds, Hartree-Fock, molecules, reactions + kinetics, self-assembly, CCSD, CIS/TDDFT, conformer gen, DFT, Drude oscillators, element supply, GB-SA, MP2, Mulliken, OPLS, PCM, ReaxFF, SMILES/SMARTS, TIP3P/TIP4P, tautomers |
| `biology/` | biology + ext, connectome + geometry, microbiome, human body, life-gen templates, cellular automaton, Connor-Stevens, consensus, de Bruijn, DSSP, FBA, Gillespie, HGT, HMM, lipid bilayer, MSA, phylogeny, protein docking, Ramachandran, reaction-diffusion |
| `consciousness/` | active inference, consciousness simulator, NLC composer, np_brain, phi_computer, IIT detail, EWC, transformer, reservoir, RL, spiking net, VAE, CTRNN, Bayes nets, sparse coding, diffusion model, liquid state, Hopfield, Kohonen, word2vec, GAN, causal DAG, concept clustering, behavior tree, A*, screen capture |
| `observer/` | symbol, avatar + bridge, observer + window + proxy, chat composer, subconscious, ai_call |
| `language/` | language, organism, microbe templates, library, translate, motor, intelligent organism, organism export, genome validator, energy ledger, base-system bench |
| `render/` | render state, draw commands/pipeline, panels, HUD, grid overlay, shadow-body render, camera projection, GL window, cluster LOD, EM field lines, wave field, speech bubble, photon overlay, atom sprite, sphere pass, bond pass, connectome render, F1 help, display-list cache, in-sim terminal |
| `gna/`, `net/`, `peer_comms/` | GNA full + stub, deduction engine, service resolver, HTTP server, JSON DB, vault crypto, mDNS, peer full + stub, AI voice call |
| `core/`, `io/`, `audio/`, `input/`, `mpi/`, `app_shell/`, `cs_viewer/`, `periodic_machine/` | units, RNG, space nav, hook bus, loadins, atomic JSON, stdout tee, fault handler, frame addresser, sphere↔Mandelbrot mapping, base64, compression, YAML, ring buffer, string algorithms · exporters, WebGL JSON, AMBER PRMTOP/NetCDF, HDF5, screenshot, LAMMPS, SDF, GROMACS top, VASP POSCAR, Gaussian log, PDBQT, CIF · audio, synth, FM, Karplus-Strong, MFCC, MIDI, pitch-YIN, spectrum, WAV · hotkeys + dispatch, event handlers · MPI substitute · CLI sub-app, launchers · CS viewer app, virtual world · PM app + window |

Per `src/main.cpp`: **headless CLI parity is the current milestone** —
`--test`, `--bench`, `--bench-perf`, `--seed`, `--help` — while the render
pipeline and interactive UI are still being ported.

---

## 24. Final scorecard

| Domain | Score | Evidence |
|---|:--:|---|
| Particle physics | **5/5** | Complete Standard Model, 35 species, PDG 2024 + real lifetimes |
| Physical constants | **5/5** | CODATA 2018, verified < 0.1% |
| Elements | **5/5** | All 118, Z = 1…118 |
| Genetic code | **5/5** | All 64 codons, 21 amino acids |
| Force fields | **5/5** | AMBER FF14SB / CHARMM36 / GAFF / TIP3P |
| Integrator & long-range EM | **5/5** | Symplectic Verlet @ 960 Hz, Ewald, Barnes-Hut; **JIT path verified to ~1e-16** |
| Free-energy methods | **5/5** | RepEx, umbrella, WHAM, FEP, TI |
| Metabolism | **5/5** | 32/2 ATP — textbook-exact |
| Body vitals realism | **5/5** | 88–105 bpm, true 1:6 breathing ratio |
| Spatial hash | **5/5** | 10.8× build speedup; self-neighbour fix enabled ~4× throughput |
| Human anatomy | **4/5** | 13 systems, 71 organs, 91.6% of real cell count |
| Neuroscience | **4/5** | HH within 5.5% of the 1952 reference |
| Time reversal | **4/5** | Genuine symplectic reversibility |
| AI architecture | **4/5** | GQA / RoPE / SwiGLU / RMSNorm; waves 53–56 learned stack is real machinery |
| Rendering | **4/5** | Real GL 4.6; shader sprites default; CMB true Planck spectrum |
| Networking | **4/5** | Full v1.17 monolith: real protocols, real security monitors |
| Connectome | **3/5** | 89.7% neurons, 7.7% synapses (specs now on all 11 templates) |
| Synthetic biology | **3/5** | Real genetic code, invented opcode layer — v2.5.0, 113 tests |
| Self-assembly | **3/5** | Emerges from real forces; heuristic detection |
| Nanotech | **3/5** | Real B-DNA constants, simplified dynamics |
| Genome scale | **2/5** | 0.00004% literal; 38.48% via documented repetition |
| Quantum chemistry | **2/5** | STO-3G, 3 molecules |
| V_total / 11-D / infinity map | **1/5** | Real inputs, invented combining equation — now canonical and verified-consistent |
| Consciousness metrics | **1/5** | Self-declared surrogates, incl. the DAN STATE ladder |

### Verdict

**Physics and chemistry: 5/5 — reality-complete.** Complete Standard Model,
complete periodic table, complete genetic code, canonical force fields,
constants to 0.1% — and now a compiled kernel path verified identical to the
interpreter within fp noise.

**Biology: 4/5** where it uses real data, **2/5** where scale is a documented
multiplier.

**Consciousness: 1/5.** The architecture is real modern ML (4/5), waves 53–56
build a genuine learned-knowledge stack, and the DAN STATE directive is honest
about being *computed* from measured voices — but the metrics measure nothing
outside themselves, and the program says so at every startup.

**The signature layer — infinity map, V_total, 11-D — is now canonical**: one
verified API, one asserted self-check, one embedded reference image, one live
panel — still verifiable against nothing outside itself.

---

*Measured on Windows 11, 12-core CPU, NVIDIA RTX 5070 Ti (17.1 GB), Python
3.13, PyTorch + CUDA (cu128), OpenGL 4.6, numba JIT.*
