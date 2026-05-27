---
title: "Huawei's τ Scaling Law: Moore's Law Successor or Branding Exercise?"
date: 2026-05-27 22:00:00
tags:
  - Semiconductor
  - Huawei
  - Chips
categories:
  - Tech Commentary
---

On May 25, 2026, He Tingbo, Huawei Board Director and President of HiSilicon, presented a keynote at IEEE ISCAS 2026 in Shanghai, officially proposing the "τ (Tau) Scaling Law" — a new semiconductor evolution principle intended to replace geometric scaling. This article evaluates its innovation, feasibility, and limitations from a technical perspective.

<!-- more -->

## I. Why a New Path: Moore's Law in Trouble

### Moore's Law is Slowing

Moore's Law — transistor counts doubling roughly every two years — is visibly slowing. Intel's former CEO Pat Gelsinger admitted in 2023 that "we're probably doubling effectively closer to every three years now"; NVIDIA's Jensen Huang declared Moore's Law dead in 2022 [1].

### Physical Limits: The Atomic-Scale Wall

Geometric scaling faces a hard ceiling at atomic dimensions. When gate lengths approach a few atoms wide (<1nm):

- Quantum tunneling prevents effective gate control of channel current
- Atomic-level fluctuations make device-to-device variation uncontrollable
- Source-drain leakage becomes unsuppressable

Today's most advanced "2nm" process has actual physical gate dimensions of ~12nm ("2nm" is commercial naming). Industry consensus: geometric scaling has 2-3 generations remaining (~2030) [1].

### An Overlooked Problem: The Interconnect Bottleneck

Even if transistors could keep shrinking, narrower wires cause resistance to spike, offsetting gains. At advanced nodes, the primary delay bottleneck has shifted from transistors to on-chip interconnects — precisely the problem the τ Law targets.

### The Industry Was Already Exploring Alternatives

In 2016, ITRS published its final Moore's Law-driven roadmap, shifting to "More than Moore" [1]. AMD's chiplets [3], NVIDIA's system integration, Intel's Foveros 3D packaging — all explore paths beyond pure transistor shrinking. The τ Law didn't appear in a vacuum; it's one specific theoretical framework within this broader trend.

## II. The τ Scaling Law: Core Idea

### From "Smaller" to "Shorter"

The τ Law's central claim: replace **geometric scaling** with **time scaling**.

Instead of making transistors smaller, systematically compress signal propagation delay time constant τ.

### What is the Time Constant τ

In digital circuits, signal delay from A to B is determined by the RC time constant:

**τ = R × C**

- R = wire resistance (thinner wire → higher R)
- C = parasitic capacitance (larger area → higher C)

Traditional Moore's Law shrinks transistors to reduce C, but narrower wires simultaneously increase R, worsening RC delay. The τ Law breaks this deadlock by compressing τ across multiple levels:

- **Device level**: Optimize transistor switching speed (higher-mobility channel materials)
- **Circuit level**: Reduce logic stages on critical paths
- **Chip level**: Shorten physical wire distances via 3D stacking
- **System level**: Inter-chip interconnect optimization (shorter package traces, on-chip optical interconnects)

### Mathematical Formulation

- τ = f(τ_transistor, τ_circuit, τ_chip, τ_system)
- Generational rule: τ(n+1) / τ(n) ≤ 1/α
- α is application-dependent: mobile ~1.3x/year, AI up to 10x/year

**Essential difference**: Geometric scaling does more by making things smaller. Time scaling does more by placing things closer and making paths shorter.

### Naming

Chinese 韬 (tāo) means "grand strategy/profound concealment." Greek τ (tau) is the physics time constant symbol. A bilingual pun.

## III. Key Technology: Logic Folding

### Principle

Traditional chips lay all circuits on one layer — like a city of single-story buildings. Larger city = longer communication paths.

Logic Folding is like replacing single-story with multi-story buildings: circuits "fold" into vertically stacked active silicon layers, connected via ultra-fine-pitch hybrid bonding (<2μm).

```
Traditional 2D layout:        After Logic Folding:
┌───────────────────────┐     ┌───────────┐
│ A ──────────────── B  │     │ A ──── B  │ ← Layer 2
│                       │     ├───────────┤
│ C ──────────────── D  │     │ C ──── D  │ ← Layer 1
└───────────────────────┘     └───────────┘
  Long signal paths             Short paths (vertical interconnects are tiny)
```

### Effects

- **Shorter wires**: Cross-chip traces become short vertical interconnects
- **Lower RC delay**: Shorter wires → smaller R and C → smaller τ
- **Higher density**: Multiple layers in same footprint = multiplied transistor density
- **No advanced lithography needed**: Same process per layer; gains come from stacking, not shrinking

### Critical Difference from Traditional 3D Packaging

Traditional 3D packaging stacks memory on processors (e.g., HBM) — functional modules stacked together. Logic Folding splits **the processor's own logic circuits** across layers — far harder because logic has much denser internal signal interactions than memory.

**As of now, there are no commercialized 3D-stacked logic cores** [2]. Commercial 3D is limited to memory (NAND, HBM) and I/O layers. If Huawei achieves mass-production of 3D-stacked active logic, it would be a genuine industry first.

## IV. Silicon-Verified Data: Kirin 2026

Huawei's published Kirin 2026 results (silicon-verified, planned for Mate 90):

| Metric | Improvement |
|--------|-------------|
| Transistor density | 155 → 238 MTr/mm² (+53%) |
| Performance core efficiency | +41% |
| Max clock frequency | 3.1GHz (+13%) |
| Wire length | -30% |
| Clock skew | -25% |

Claimed equivalent to first-gen TSMC 3nm / Intel 18A. Roadmap:

- 2027: Kirin 2027, 3.39GHz
- 2029: >4GHz
- 2031: Equivalent 1.4nm density (400+ MTr/mm²)

Huawei states 381 chips mass-produced over 6 years across mobile, base stations, automotive, and AI.

## V. Physical Limits of the τ Path

Moore's Law hits the "wall of space." The τ path will hit the "wall of time and heat":

### 1. Speed of Light

Signals in copper propagate at ~60-70% of vacuum light speed. Propagation time cannot be less than distance ÷ c, regardless of path optimization. This limit emerges as chips get sufficiently small.

### 2. Thermodynamic Limit (Landauer's Principle)

Each irreversible bit operation dissipates at minimum kT·ln2 (~3×10⁻²¹ J/bit @ 300K). Faster switching = higher power density, while 3D stacking makes thermal dissipation harder — a fundamental tension between power density and time constant.

### 3. Material RC Limits

- Resistance R: Copper resistivity ~1.7μΩ·cm is a physical floor; at nanometer scales, surface and grain boundary scattering worsen it further
- Capacitance C: Low-k dielectrics near manufacturing limits (currently ~k=2.0-2.5; theoretical floor is vacuum at 1)

Even with minimal path lengths, per-unit-length RC is constrained by material physics.

### 4. Stacking Layer Limits

Each added layer: worse thermals, multiplicative yield loss, tighter alignment requirements. NAND stacks 200+ layers because storage cells have extremely low power density; logic chips have 1-2 orders of magnitude more power, severely limiting achievable layers.

### Summary

Both paths have physical limits, just different ones. Most likely they're complementary: time scaling provides several extra generations after geometric scaling is exhausted, but also eventually hits a ceiling.

## VI. The Evaluation Problem: How to Verify a Multi-Variable Framework

τ = f(τ_transistor, τ_circuit, τ_chip, τ_system) involves four levels with multiple variables. Core question: when a manufacturer claims "τ improved 30%," how can outsiders verify?

Under Moore's Law, evaluation is simple — count transistors, measure gates. Under the τ framework, variables have complex trade-offs:

| Optimization | τ Improvement | Side Effects |
|-------------|---------------|--------------|
| More stacking layers | Shorter wires → τ↓ | Worse thermals, lower yield |
| Lower-k dielectrics | Capacitance↓ → τ↓ | Reduced strength, reliability risks |
| Finer-pitch bonding | Inter-layer distance↓ → τ↓ | Tighter alignment, higher cost |
| Pipeline repartitioning | Critical path stages↓ → τ↓ | Area/power increase |
| System interconnect optimization | Inter-chip delay↓ → τ↓ | Design complexity explosion |

The same τ number can be achieved through different combinations, but user experience may differ dramatically. Aggressive stacking with low τ may require thermal throttling, yielding worse sustained performance than a conservative approach.

**Viable evaluation methods:**

1. **End-to-end benchmarks**: Geekbench, SPEC don't care about the path — they measure results
2. **Energy efficiency (perf/watt)**: If τ reduction costs power explosion, it's meaningless
3. **Sustained vs. peak performance**: Under thermal constraints, the gap may be large
4. **Equivalent node comparison**: Compare density/performance against known TSMC/Intel nodes
5. **Independent teardown**: TechInsights et al. can verify physical parameters

He Tingbo's paper acknowledges "new benchmarking frameworks are required" — until established, the most reliable judge remains real-world production device experience.

## VII. Controversies and Criticism

### "Laws" Are Validated, Not Declared

Moore's Law was an empirical observation (1965), validated over decades by the entire industry. The τ Law was named and announced by one company at one conference. "A law emerges from decades of validation, not from a corporate keynote."

### Thermal: The Core Challenge of 3D Logic Stacking

The acknowledged #1 challenge of 3D ICs [2]: heat accumulates in stacks, electrical proximity = thermal proximity, hotspot management becomes extremely complex. Whether sustained peak performance is achievable in thermally-constrained phone form factors remains unproven.

### Timeline Gap

TSMC/Samsung/Intel target 1.4nm mass production by 2027-2028. Huawei's "equivalent 1.4nm" target is 2031 — 3-4 years later via an alternative path. Of course, for Huawei without EUV access, "arriving late" is far better than "never arriving."

### Branding vs. Breakthrough

The underlying technologies (3D stacking, chiplets, architecture co-optimization) are all pursued by AMD/Intel/NVIDIA/TSMC. Huawei's unique contribution is unifying them under a τ-centered theoretical framework. Innovation or packaging? No independent third-party verification exists.

### Self-Acknowledged Limitations (from He Tingbo's paper)

- EDA tools not ready for native 3D design
- Inter-wafer process variation unresolved
- Vertical interconnect overhead varies by workload
- No energy companion principle (τ handles time, not energy)
- New benchmarking frameworks required

## VIII. Our Take

The τ Law's technical path is real and valuable. Under sanctions, Huawei has found an evolution path independent of EUV. Logic folding and system-level co-optimization are pragmatic engineering choices, and the silicon data is compelling.

However, naming it a "law" and positioning it alongside Moore's Law is primarily strategic communications. This isn't necessarily bad — a clear narrative aligns teams and supply chains. But we should distinguish between "an effective engineering strategy" and "an industry-recognized objective law."

The real tests:

1. Kirin 2026 mass-production performance, yields, and costs
2. Whether other manufacturers adopt similar frameworks
3. Whether multiple generations can consistently validate τ scaling's predictability

If in five years the entire industry uses a similar methodology, it may indeed become a law. If only Huawei uses it, it remains an excellent corporate technology strategy — which is already worthy of respect.

## References

**Official & Media Sources:**

1. Huawei Official: [IEEE ISCAS τ Law Announcement](https://www.huawei.com/cn/news/2026/5/ieee-iscas-tau-scaling)
2. Xinhua: [Huawei Proposes τ Law](https://www.news.cn/tech/20260526/75603364bbae42bab67933d63d63e373/c.html)
3. Sina Tech (He Tingbo paper summary): [τ Law Explained](https://news.sina.com.cn/c/2026-05-26/doc-inhzchzh3471783.shtml)
4. CNBC: [Huawei Chip Logic-Folding](https://www.cnbc.com/2026/05/25/huawei-chip-logicfolding-semiconductor-nvidia-china.html)

**Technical Background:**

5. Wikipedia: [Moore's Law - Slowdown and alternatives](https://en.wikipedia.org/wiki/Moore%27s_law) [1]
6. Wikipedia: [Three-dimensional integrated circuit](https://en.wikipedia.org/wiki/Three-dimensional_integrated_circuit) [2]
7. Wikipedia: [Chiplet architecture](https://en.wikipedia.org/wiki/Chiplet) [3]
8. ITRS 2016 Final Edition / IRDS: More than Moore roadmap

**Note:** As of publication (May 27, 2026), major international semiconductor analysts (SemiAnalysis, TechInsights, EE Times, IEEE Spectrum) have not yet published in-depth technical analysis of the τ Law. This article will be updated as such analyses become available.
