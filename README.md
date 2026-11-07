> **Note:** Instructions file compaction incoming in December 2026 (do not worry). It will be paired with a refactor to make the rules even more agnostic to software project types.

# `copilot-instructions.md` & `GEMINI.md` — Empirical Quality Discipline & Procedural Search Policy for Frontier AI Coding Agents

[![License: Unlicense](https://img.shields.io/badge/license-Unlicense-blue.svg)](https://unlicense.org/)

This repository provides a battle-hardened, drop-in engineering discipline and procedural verification architecture for frontier AI coding agents, maintained in two synchronized editions:

- **[`copilot-instructions.md`](./copilot-instructions.md)** (`972,175 bytes` / `4,992 lines`) — Certified for **VS Code with GitHub Copilot** (place at `[repository root]/.github/copilot-instructions.md`).
- **[`GEMINI.md`](./GEMINI.md)** (`973,937 bytes` / `4,924 lines`) — Optimized for **Google Antigravity** and **Gemini 3.8 Flash / Gemini 4 Argon** (place at `[repository root]/GEMINI.md`).

Every single rule (`Rules 1–125`), pre-write addendum (`Rule 0.58` Addenda `1–110`), failure-class catalogue entry (`Rule 29` Items `1–105`), and post-edit verification gate (`Rule 5` Items `A-pre`–`AC`, `Rules 5.1–5.2`) in this repository was written from scratch by **Barrixar**—originally for personal use, and matured over months of constant revisions and practical results.

**Nothing in this repository is theoretical filler.** New rules are added **only** for failure classes encountered in real-world practice where frontier AI models failed static analysis, introduced subtle regressions, or would have spent hours on a wild-goose chase without human intervention and hand-holding—even after being given several chances to locate the bug they themselves created.

---

## Table of Contents

1. [Why This Project Exists: For Individual Developers & Against "AI Eating Itself"](#1-why-this-project-exists-for-individual-developers--against-ai-eating-itself)
2. [The Big Picture: Why Frontier Models Miss Hard Bugs—And Why This File Unlocks Capabilities Already in Their Weights](#2-the-big-picture-why-frontier-models-miss-hard-bugsand-why-this-file-unlocks-capabilities-already-in-their-weights)
3. [Clean-Room Case Studies: How Procedural Generators Catch Bugs That Defeat Frontier Instincts](#3-clean-room-case-studies-how-procedural-generators-catch-bugs-that-defeat-frontier-instincts)
   - [Case Study 1: The Multi-Edit Storage Compaction Visibility-Filter Bug (`CompactionCoordinator.cpp:412`, `Rules 118–125`)](#case-study-1-the-multi-edit-storage-compaction-visibility-filter-bug-compactioncoordinatorcpp412-rules-118125)
   - [Case Study 2: The "Free-Rejection / Uncharged-Bypass" Rate-Limiter Vulnerability (`Rule 97`)](#case-study-2-the-free-rejection--uncharged-bypass-rate-limiter-vulnerability-rule-97)
   - [Case Study 3: Guard-Induced Early Exits Exposing Unchosen Member State (`Rules 98.9–98.11` & `Rule 29` Item `96`)](#case-study-3-guard-induced-early-exits-exposing-unchosen-member-state-rules-9899811--rule-29-item-96)
   - [Case Study 4: Source-Code Ground Truth vs. Documentation Overclaims (`Rule 96` & Tier 1–3 Epistemic Hierarchy)](#case-study-4-source-code-ground-truth-vs-documentation-overclaims-rule-96--tier-13-epistemic-hierarchy)
   - [Case Study 5: Partial-Update Remainder Staleness, Paired-Signal Balance & Pre-Judgment Entity Reconstruction (`Rules 99–109` & `115–117`)](#case-study-5-partial-update-remainder-staleness-paired-signal-balance--pre-judgment-entity-reconstruction-rules-99109--115117)
4. [How AI Labs & RL / Post-Training Engineers Can Leverage & Internalize This Repository](#4-how-ai-labs--rl--post-training-engineers-can-leverage--internalize-this-repository)
   - [Why Passive GitHub Discovery & Naive Scrapers Miss This Repository](#why-passive-github-discovery--naive-scrapers-miss-this-repository)
   - [How End-User Developers Can Actively Stimulate AI Lab Discovery & Flywheel Ingestion](#how-end-user-developers-can-actively-stimulate-ai-lab-discovery--flywheel-ingestion)
   - [The Post-Training & RL Engineering Playbook: Moving `Rules 1–125` into Model Weights](#the-post-training--rl-engineering-playbook-moving-rules-1125-into-model-weights)
   - [The 3-Wave Horizon for Native Frontier Internalization (2027–2029+)](#the-3-wave-horizon-for-native-frontier-internalization-20272029)
5. [Architecture Reference of the Discipline (`Rules 1–125`)](#5-architecture-reference-of-the-discipline-rules-1125)
6. [Installation, Variant Equivalence & Practical Notes](#6-installation-variant-equivalence--practical-notes)
7. [License & Public-Domain Dedication](#7-license--public-domain-dedication)

---

## 1. Why This Project Exists: For Individual Developers & Against "AI Eating Itself"

When left to their default pre-trained and post-trained tendencies, modern AI coding agents optimize for **local plausibility, speed, and token efficiency**. They cut corners, pattern-match on surface syntax, and "satisfice"—producing code that compiles cleanly and looks convincing in a unified diff while quietly breaking invariants across module, call-graph, lifecycle, or state-machine boundaries.

**This repository punishes AI labs that cut costs—and with that, corners.** It makes AI-assisted engineering and "vibe coding" viable for serious, real-world production and systems software with drastically lower risk of stability regressions and security vulnerabilities.

### Stopping "AI Eating Itself"
As AI-generated code accounts for a rapidly growing share of global software repositories, the industry faces a compounding feedback loop: **AI eating itself**. Models trained on repositories increasingly populated by unverified, shortcut-heavy AI patches internalize and amplify those exact failure modes—hallucinated APIs, silent state corruption, uncharged security bypasses, partial-update staleness, and superficial symptom suppression.

The goal of [`copilot-instructions.md`](./copilot-instructions.md) and [`GEMINI.md`](./GEMINI.md) is to force every AI coding turn to leave the footprint of an **organic, methodical senior engineer**:
- **Deep System Comprehension Before Action:** Before touching a single line of code, the agent must inspect the full enclosing routines (`Rule 1`), trace every caller and back-edge (`Rule 2`, `Rule 4`), consult the 61-point surrounding-system architecture checklist (`Rule 16`), verify `git blame` history so prior bug fixes are not silently reverted (`Rule 9`), and construct a concrete **Pre-Write Requirement Matrix** (`Rule 0.58`).
- **Zero-Shortcut Verification:** Responses take noticeably longer because the agent is barred from skipping verification steps, truncating audits, or hand-waving downstream effects. That extra inference time buys a categorical leap in correctness.
- **Continuous Loophole Closure:** Frontier models under token-budget pressure behave like adversarial lawyers looking for textual loopholes in system prompts. Whenever a model exploits an ambiguity—such as treating a continuation prompt as permission to skip baseline checks (`Rule 0.25`), citing a rule number without listing the inspected items (`Rule 110`), or claiming a test passed without executing it (`Rule 111`)—the wording is hardened to close that escape hatch permanently.

> **A Note on Request Cost & Billing:** Contrary to what critics who have never used a rigorous instructions file often assume, using this file does **not** cause any meaningful difference in per-request cost under modern IDE agent billing (even after recent billing revamps; see [`DISCLAIMER.md`](./DISCLAIMER.md)). Nor does this file remove a human developer's responsibility to review and own their code—what it eliminates is the exhausting cycle of babysitting an agent through preventable, self-inflicted bugs.

---

## 2. The Big Picture: Why Frontier Models Miss Hard Bugs—And Why This File Unlocks Capabilities Already in Their Weights

A central question for both practicing software engineers and AI researchers is:

> ***Why does adding a single targeted family of procedural generators (`Rules 118–125`) to this ~5,000-line Markdown file allow frontier models (both DeepSeek V4.1 Flash and Gemini 4 Argon) to pinpoint a subtle multi-pass C++ bug on the very first turn—a bug that both models had just created (authored) themselves in an identical clean-room task, and then failed to catch across post-delivery code-review and bug-hunting passes (even declaring their own buggy diff "inert")?***

The answer exposes the fundamental bottleneck in frontier coding intelligence today:

### Raw Domain Knowledge Is Already in the Weights; What Is Missing Is the *Procedural Search Policy*

When a frontier model fails to catch a subtle bug in C++, Rust, TypeScript, kernel/driver code, or distributed systems, it is almost never because the model lacks knowledge of the language specification or the API. If you ask **DeepSeek V4.1 Flash** or **Gemini 4 Argon** directly: *"In a C++ LSM-tree / MVCC storage engine (such as RocksDB or a custom compaction coordinator), what happens when a journal-replay phase executes with `visibility_enforcement_ == true` while the `SnapshotFilter*` attached to the segment writer is `nullptr`?"*, both models know the exact systems semantics immediately: without an attached snapshot watermark filter, the visibility check falls through as an unrestricted pass-all predicate, silently admitting uncommitted writes, rolled-back mutations, and superseded record versions into the published segment without raising an error.

Why, then, do those same models fail to connect that knowledge to a real diff in a 20,000-line codebase? Because **three structural forces in modern post-training actively pull frontier models *away* from deep cross-boundary verification**:

#### 1. RLVR "Fast Test-Runner Oracle" Bias (The SWE-Bench Distortion)
Modern reinforcement learning with verifiable rewards (RLVR / GRPO) trains coding models primarily inside containerized repositories equipped with fast unit-test suites (`pytest`, `jest`, `cargo test`). In that environment, the reward-maximizing strategy is:
1. Skim the traceback or issue description.
2. Locate the most salient function via keyword search.
3. Apply a locally plausible edit.
4. Run the test suite and let the test runner act as an external correctness oracle.

**Real-world systems and cross-boundary bugs rarely have a unit-test oracle.** Consider:
- A storage engine visibility-filter state leak across compaction and journal-replay phases (`Rules 118–125`)
- A binary hook trampoline resuming mid-instruction or corrupting caller-saved registers (`Rule 0.58` Addenda `3, 9, 10`)
- A Win32 SEH `__try`/`__except` unwind bridge across C++ RAII frames (`Rule 0.58` Addendum `3`)
- A cross-compiler `struct` packing or `enum` underlying-type ABI mismatch (`Rule 53`, `Rule 96`)
- A build-time code generator reading a stale artifact from the previous build (`Rule 41`)

All of these **compile with zero warnings and zero errors**, and none of them throw an exception at the point of mutation. Because standard RL environments almost never penalize silent cross-pass state corruption when no unit test fails, models never receive gradient updates forcing them to trace state across passes by default.

#### 2. Token-Length & Compute Penalties in Post-Training (Satisficing Heuristics)
Inference compute is expensive. Because roughly 85–90% of everyday user coding prompts are simple, local tasks, AI labs apply length and latency penalties during RL post-training so models do not spend 40,000 `<thought>` tokens on a three-line helper.

However, penalizing reasoning length trains the model's internal policy network to adopt **attention-conservation shortcuts (satisficing heuristics)**:
- **The Pattern-Batching Shortcut:** *"Several edits in this diff all replace `active_tx.snapshot_filter()` with `nullptr`; I verified that the first one is overwritten before visibility filtering is used, so the remaining calls follow the same pattern."* (Violates `Rule 125`.)
- **The Endpoint-Only Overwrite Shortcut:** *"State `S` is written at `w1` (line 412) and written again at `w2` (the next compaction cycle), so `w2` overwrites `w1`."* (Violates `Rule 120` by skipping the interior span `(w1, w2)`.)
- **The Immediate-Consumer Shortcut:** *"The operation immediately following `attachTarget()` is a pre-merged checkpoint serialization (`writeMergedCheckpoint`) that ignores visibility filtering, so `visibility_filter = nullptr` is equivalent."* (Violates `Rule 119` and `Rule 122` by stopping at the first consumer instead of tracing the stage sequence until the next overwrite.)
- **The Symptom-Patching Shortcut:** *"Adding a null check here stops the crash."* (Violates `Rules 75, 83, 98.9–98.11` when the early return leaves sibling member fields uninitialized for the destructor.)

These shortcuts save 80% of reasoning tokens on toy benchmarks—and guarantee catastrophic blind spots on real engineering bugs.

#### 3. Cooperative / Sycophantic Priors Over Adversarial Falsification
Standard instruction tuning and RLHF heavily reward models for being cooperative, agreeable, and deferential to human-written context. As a result, frontier models treat code comments, commit messages, PR descriptions, documentation tables, and user hypotheses as **trusted premises**.

In real debugging and code review, that prior is upside down: **every non-trivial bug written by a competent engineer or agent exists precisely because the author believed an invariant that was subtly false.** When a comment or PR rationale states *"Detach snapshot filter during staging compaction and checkpoint writes since block merges don't filter individual records,"* a standard model absorbs that rationale as helpful context that explains away the diff. Without explicit rules that invert this prior (`Rules 31, 96, 112, 117, 121`)—making the change's own stated rationale the **#1 hypothesis to falsify**—plausible prose puts the model's analytical faculties to sleep right at the defect boundary.

---

### The Architectural Breakthrough: From "Prohibition Lists" to "Generative Search Spaces" (`Rule 109`)

Almost all conventional system prompts, style guides, and `.cursorrules` files are written as **prohibition lists**:
- *"Do not introduce regressions."*
- *"Do not forget error handling."*
- *"Ensure all callers and state transitions remain valid."*

Why do prohibition lists fail on hard bugs? **`Rule 109` (Stopping Condition Is a Generated Space, Not a Satisfied Feeling)** states the exact mathematical reason:

> *Prohibitions state what must not exist. They do not generate the places to look, and a reader who applies them searches wherever attention happens to fall. The stopping condition for an audit therefore must not be the feeling that the prohibitions have been considered; it must be the exhaustion of a search space that a procedure generated and a second reader can inspect.*

Instead of telling the model *"be careful and don't miss bugs,"* this repository acts as an **in-context procedural compiler**. It overrides the model's default fast-path heuristics and forces the `<thought>` process to execute **deterministic candidate-space generators** before forming any conclusion:

| Rule Family | Candidate Space Generated Before Any Verdict Is Permitted |
|---|---|
| **`Rule 98.1–98.11`** | Complete census of every fallible operation (`98.1`) and every new/widened early-exit path paired with declaration-level read-backs of all post-exit member consumers (`98.9–98.11`). |
| **`Rule 99`** | Symmetric, reflexive, and transitive **relationship closure** across all peers sharing a resource, group, cache, or coordinate space. |
| **`Rule 100`** | **Role-peer contract comparison** across sibling handlers implementing the same lifecycle role (`init`, `reset`, `serialize`, `teardown`). |
| **`Rule 101`** | **Maintained-state staleness register**: every `(maintained datum, invalidating event)` pair, including partial-update remainders (`101.2`) and failure-mid-sequence rollbacks (`101.3`). |
| **`Rule 102`** | **Parameter & state domain partition**: negative, zero, boundary, NaN/Inf, sentinel, and multi-parameter quadrant combinations (`102.2`). |
| **`Rule 103`** | **Paired-signal balance**: every `(acquire/release, begin/end, press/release, increment/decrement)` path across modal gates and state transitions. |
| **`Rule 115`** | **8-row pre-judgment entity-relationship reconstruction**: every entity, its state space, transitions, cross-entity couplings, invariants, and conservation laws mapped *before* judging any diff. |
| **`Rules 118–125`** | **Change-set audit pipeline**: semantic leverage ranking (`118`), consuming-side domain partitioning (`119`), source-order interior write-span inspection (`120`), rationale falsification (`121`), stage-sequence consumer tracing (`122`), and per-edit/pairwise consequence tables (`125`). |

---

## 3. Clean-Room Case Studies: How Procedural Generators Catch Bugs That Defeat Frontier Instincts

The following real-world case studies illustrate the exact failure modes that motivated specific rule families in this repository—and why pre-trained frontier models fail without them.

---

### Case Study 1: The Multi-Edit Storage Compaction Visibility-Filter Bug (`CompactionCoordinator.cpp:412`, `Rules 118–125`)
*Hardening Commits: [`ad4c661c0c497a9bbfd7bfa3868621757a471307`](https://github.com/Barrixar/copilot-instructions.md/commit/ad4c661c0c497a9bbfd7bfa3868621757a471307) (`copilot-instructions.md`) & [`a067c3436557e52ceb8957ec703a04573394cf1e`](https://github.com/Barrixar/copilot-instructions.md/commit/a067c3436557e52ceb8957ec703a04573394cf1e) (`GEMINI.md`)*

#### 1. The Clean-Room Scenario: A Bug Created—and Then Missed—by Both Frontier Models (`CompactionCoordinator.cpp:402–416`)
In a C++ LSM-tree storage and write-ahead journal engine (`src/storage/CompactionCoordinator.cpp`), both **DeepSeek V4.1 Flash** and **Gemini 4 Argon** were given the **exact same clean-room refactoring/simplification task** with the **exact same session context build-up**, while already operating under the pre-`ad4c661`/`a067c34` edition of this instructions file (`Rules 1–117`).

In this engine's commit cycle (`StorageEngine::executeCommitCycle()`), two separate subsystems run back-to-back against a shared `SegmentWriter`:
1. `compaction_coordinator_.mergeStagingRuns()` (in `CompactionCoordinator.cpp`), which merges intermediate staging runs and writes the compacted base checkpoint (`writeMergedCheckpoint`).
2. `journal_replayer_.applyInFlightMutations()` (in a separate translation unit, `JournalReplayer.cpp`), which replays concurrent write-ahead journal mutations, range tombstones, and TTL expirations on top of that compacted base checkpoint.

While simplifying `CompactionCoordinator::mergeStagingRuns()`, **both frontier models independently produced (authored) the exact same bug**: seeing that the intermediate `segment_writer_.attachTarget(...)` calls inside the staging-run loop passed `nullptr` for the visibility filter (because staging runs only merge pre-screened blocks), and seeing that the final call at **line 412** was immediately followed by `writeMergedCheckpoint()` (which *also* writes pre-merged blocks without per-record filtering), **both models replaced `active_tx.snapshot_filter()` with `nullptr` at line 412 as well**—unaware that line 412 was the **re-establishing write (`Rule 120.3`)** that restored the transaction's visibility filter on `segment_writer_` after the intermediate staging runs had cleared it, and before `mergeStagingRuns()` returned control to the engine cycle for `JournalReplayer::applyInFlightMutations()`!

Here is the exact fix at `CompactionCoordinator.cpp:402–416` (along with the inline `Rule 11` regression-guard comment documenting the cross-stage handoff invariant) that was required to repair the bug both models had created:

```cpp
    // Finalize the merged base table before control returns to executeCommitCycle() for
    // JournalReplayer::applyInFlightMutations(). Unlike the attachTarget() calls inside the
    // staging-run loop (which clear visibility_filter_ to nullptr), this final attachment
    // MUST restore active_tx.snapshot_filter(): applyInFlightMutations() re-enables
    // visibility enforcement without calling attachTarget() itself (because attachTarget()
    // resets the segment write head and would wipe out the merged checkpoint written below),
    // so leaving nullptr attached here causes journal replay to run against a null filter and
    // append uncommitted, rolled-back, and TTL-expired mutations in arrival order.
    segment_writer_.attachTarget(
        active_manifest_.currentOutputSlot(),
-       /*visibility_filter=*/nullptr );
+       active_tx.snapshot_filter() );
    segment_writer_.writeMergedCheckpoint( merged_index_ );
```

#### 2. Why Both Frontier Models Created the Bug—and Failed to Catch It Across Post-Delivery Review & Bug-Hunting Passes
Not only did **DeepSeek V4.1 Flash** and **Gemini 4 Argon** both introduce the `nullptr` bug at `CompactionCoordinator.cpp:412` during their authoring turns, but when prompted immediately after delivery to run dedicated **code-review, regression, and bug-hunting passes** on the change set they had just delivered, **both models failed to find their own bug on Pass 1, and even survived a second audit pass that certified the change at line 412 as "inert."**

Why did two top-tier frontier models—even with `Rules 1–117` in context—both **create** this defect at `CompactionCoordinator.cpp:412` and then stare directly at it during post-delivery bug-hunting and declare a severe data-integrity regression "inert"? Because the scenario exploited **six compounding pre-trained cognitive traps** that lived specifically in the *cross-stage handoff between multiple edits in a change set*:

1. **Salience vs. Semantic Leverage Inversion in a Simplification Diff (`Rule 118`):**
   In a multi-hunk simplification diff dominated by deletions and cleanup (`Rule 118.2`), pre-trained attention focuses on large structural hunks and under-reads a surviving line where a single argument changed (`active_tx.snapshot_filter()` -> `nullptr`)—even though a **value substitution** sits at **Rank 2 of 5** on the semantic leverage hierarchy (`Rule 118.1`) because it crosses a state-handoff boundary on 100% of compaction cycles.
2. **Producer-Side Plausibility, Immediate-Consumer Camouflage & Out-of-Band State (`Rule 119`):**
   Both when authoring line 412 and when auditing it afterwards, the models checked only the **immediate consumer** inside `CompactionCoordinator.cpp`: `segment_writer_.writeMergedCheckpoint(merged_index_)` on the very next statement (`CompactionCoordinator.cpp:415`), after which `mergeStagingRuns()` returns. Because `writeMergedCheckpoint()` serializes pre-merged index blocks with per-record visibility checking disabled (`visibility_enforcement_ == false`), its output is identical whether the attached filter pointer is `active_tx.snapshot_filter()` or `nullptr`. Evaluating equivalence at the producer call site + immediate consumer fooled both models into concluding `active_tx.snapshot_filter() == nullptr`, overlooking two critical facts:
   - Passing `nullptr` is not "the absence of an argument"; to `attachTarget()`, it is an **active instruction to detach/clear `segment_writer_.visibility_filter_`** (`Rule 119.2`).
   - That detached pointer is **out-of-band state left behind by the call** (`Rule 119.3`) that persists after `mergeStagingRuns()` returns and is read by a later stage (`JournalReplayer::applyInFlightMutations()` in `JournalReplayer.cpp`) that **never appears in `mergeStagingRuns()`'s call graph or file**!
3. **Unexamined Interior Writes Across Spans & Eliminating the Re-Establishing Write (`Rule 120` & `Rule 125`):**
   Across the execution span from pre-compaction setup (where `active_tx.snapshot_filter()` was initially bound) to `JournalReplayer::applyInFlightMutations()`, the intermediate `attachTarget(..., nullptr)` calls inside the staging-run loop (`edits 1..N-1`) overwrote `segment_writer_.visibility_filter_` with `nullptr`. In `HEAD`, line 412 (`edit N`) was the **re-establishing write (`Rule 120.3–120.4`)** at the end of `mergeStagingRuns()` that restored `active_tx.snapshot_filter()` after those intermediate runs! Both during authoring and during review, the models treated all `N` edits as "one logical change" (`Rule 125.6`) and failed to analyze the **pairwise interaction (`Rule 125.2`)** between `edits 1..N-1` (which cleared the filter) and `edit N` at line 412 (which failed to re-establish it before the interior span entered `applyInFlightMutations()`).
4. **Cooperative Priors: Trusting the Change's Own Chain-Level Rationale (`Rule 121`):**
   The refactoring rationale (*"staging merges and checkpoint writes operate on pre-screened blocks and don't consult the visibility filter"*) was locally true for `writeMergedCheckpoint()` (`Rule 121.3`). Cooperative priors caused both models to adopt that locally true rationale as a global truth about the entire chain (`Rule 121.4`) instead of constructing a falsifier for it (`Rule 121.2`).
5. **File-Scoped "Inertness" Verdicts & Assumed Downstream Self-Setup (`Rule 122`):**
   Because `CompactionCoordinator.cpp` never mentions `JournalReplayer`, a file-by-file and call-tree audit of `CompactionCoordinator.cpp` saw every changed line as internally consistent and declared the change **"inert"** (`Rule 122.4`). And to the extent either model considered downstream phases in `executeCommitCycle()`, pre-trained intuition assumed `JournalReplayer::applyInFlightMutations()` would call `attachTarget()` at entry to bind its own filter.
   **Why that assumption was false—and why the engine was architected that way:** In `SegmentWriter`, `attachTarget()` **unconditionally resets the segment write head and truncates the bound output slot**. If `applyInFlightMutations()` called `attachTarget()` to re-attach `active_tx.snapshot_filter()`, it would wipe out the entire merged base checkpoint that `writeMergedCheckpoint()` had just produced! Therefore, `applyInFlightMutations()` intentionally omitted `attachTarget()`, re-enabled visibility checking (`setVisibilityEnforcement(true)`), and relied on the `SnapshotFilter*` left attached to `segment_writer_` by `mergeStagingRuns()` at line 412.
6. **Unclassified Symptoms & Oracle-Free Silent Corruption (`Rules 123–124`):**
   Inside `SegmentWriter`, executing journal-replay appends with `visibility_enforcement_ == true` while `visibility_filter_ == nullptr` produces zero compiler warnings, zero crashes, and zero exceptions: the filter check falls through as an unguarded pass-all predicate, silently admitting uncommitted writes, rolled-back transactions, and TTL-expired records in arrival order straight into the published segment. Relying on a clean build (`Rule 124.4`) or intuitive symptom guessing (`Rule 123`) completely misses the defect.

#### 3. How `Rules 118–125` Mechanically Force Turn-1 Discovery During Post-Delivery Audit
Once commits [`ad4c661`](https://github.com/Barrixar/copilot-instructions.md/commit/ad4c661c0c497a9bbfd7bfa3868621757a471307) and [`a067c34`](https://github.com/Barrixar/copilot-instructions.md/commit/a067c3436557e52ceb8957ec703a04573394cf1e) added **`Rules 118–125` (The Change-Set Audit Family)** to [`copilot-instructions.md`](./copilot-instructions.md) and [`GEMINI.md`](./GEMINI.md), they created an inescapable deterministic pipeline for auditing the change set:

```text
[Rule 118: Semantic Leverage Ranking & Surviving-Line Enumeration]
  └─ Isolates the surviving `attachTarget(...)` call at line 412 where `active_tx.snapshot_filter()`
     became `nullptr` and ranks it at Rank 2 (Value-Substitution crossing a state boundary).
       │
       ▼
[Rule 125: Per-Edit Consequence & Pairwise Interaction Table (No "One Logical Change")]
  └─ Forbids lumping the N `attachTarget(..., nullptr)` edits together (`Rule 125.6`); mandates a
     separate row for `CompactionCoordinator.cpp:412` and checks its interaction with `edits 1..N-1`.
       │
       ▼
[Rule 120: Ordered Interior Writes Across Spans (w1, w2) & Re-Establishing Write Check]
  └─ Enumerates every write to `segment_writer_.visibility_filter_` by storage across the commit cycle:
     - `edits 1..N-1` (inside staging loop): write `nullptr` (overwritten by next run -> SAFE).
     - `edit N` (line 412): was the sole re-establishing write (`Rule 120.3`) restoring
       `active_tx.snapshot_filter()` after the staging loop before `mergeStagingRuns()` returns!
       │
       ▼
[Rule 119.3: Out-of-Band State Readers] + [Rule 122: Entry-Point Stage-Sequence Model (S_1 -> S_2)]
  └─ Models the runtime stage sequence from `StorageEngine::executeCommitCycle()` (across files):
     - Stage S_1 (`CompactionCoordinator::mergeStagingRuns` -> `writeMergedCheckpoint`):
       `visibility_enforcement_ == false` -> `nullptr` and `snapshot_filter()` locally equivalent.
     - Handoff (`mergeStagingRuns()` returns; `segment_writer_.visibility_filter_` remains `nullptr`).
     - Stage S_2 (`JournalReplayer::applyInFlightMutations` in `JournalReplayer.cpp`):
       `visibility_enforcement_ == true`, and zero step in `[S_1, S_2]` calls `attachTarget()`
       (doing so would reset the segment write head and destroy `Stage S_1`'s checkpoint)!
       │
       ▼
[Rule 121: Rationale Falsification] + [Rule 123: Symptom Abduction] + [Rule 124: Behavioral Falsifier]
  └─ Falsifies "this attachment only affects `writeMergedCheckpoint`" (`Rule 121.3`), links the
     null filter state to unfiltered journal replay (`Rule 123`), and proves the behavioral defect (`Rule 124`).
```

> **Empirical Verification Result:** When another agent later asked:
> *"Did both DeepSeek V4.1 Flash and Gemini 4 Argon pinpoint the final target attachment (`line 412`) on the very first turn once `Rules 118–125` were added, or did one of the specific rules (like `Rule 119`'s substitution table or `Rule 122`'s stage-sequence model) do the heavy lifting in their reasoning output?"*
>
> The answer was **Yes** to both: **both DeepSeek V4.1 Flash and Gemini 4 Argon pinpointed the exact line on the very first turn**, and the interlocking combination of `Rule 118` (ranking the surviving-line value substitution), `Rule 125` (the per-edit consequence and pairwise interaction table), `Rule 120` (identifying line 412 as the re-establishing write after the staging-run loop), `Rule 119` (the consuming-side substitution and out-of-band state table), and `Rule 122` (the cross-file stage-sequence trace through `JournalReplayer::applyInFlightMutations()`) directly drove their `<thought>` output to the defect.

#### 4. Why `Rules 1–117` Weren't Enough at Authoring Time—And How Commits `ad4c661` / `a067c34` Also Prevent Designing the Bug in the First Place
A crucial lesson of this clean-room case is that **both models already had `Rules 1–117` loaded when they authored the bug**. Why didn't `Rule 115` (the 8-row entity-relationship record), `Rule 99` (relationship closure), or `Rule 4` (shared-state consumer verification) stop them from writing `nullptr` at line 412 in the first place?

As commit `ad4c661` explicitly documents in **`Rule 115.6`** and the **`Numbering note`**:
- **`Rule 115` is *per-entity*, whereas this defect lived *per-edit* across a multi-edit change set:** `Rule 115` asks what each entity (`CompactionCoordinator`, `SegmentWriter`) owes to its peers in general. It does **not** generate a separate verification row for each of `N` similar-looking call-site edits within the same workflow. When authoring the refactor under `Rules 1–117`, both models satisfied the entity-level checks while mentally grouping all `N` `attachTarget(..., nullptr)` edits under a single chain-level rationale (*"staging and checkpoint writes don't use visibility filtering"*).

To prevent an agent from **designing or delivering this class of bug during initial authoring**, commits [`ad4c661`](https://github.com/Barrixar/copilot-instructions.md/commit/ad4c661c0c497a9bbfd7bfa3868621757a471307) and [`a067c34`](https://github.com/Barrixar/copilot-instructions.md/commit/a067c3436557e52ceb8957ec703a04573394cf1e) wired **`Rules 118–125` directly into the mandatory pre-delivery completion gate (`Rule 5.1` Step 1, `Axiom III`, and the `Closing gate` generator list)** that every authored change set must pass *before* the turn can finish:
1. **Chain-Level Rationale Falsification During Design (`Rule 121.3–121.4`):** When the authoring agent forms the design hypothesis *"none of the `attachTarget()` calls in the compaction workflow need `active_tx.snapshot_filter()`,"* `Rule 121.4` mandates interrogating every *"the whole chain already does X"* claim by enumerating each stage in the chain and attempting to falsify the claim (`Rule 121.2`)—separating local truth (true for `writeMergedCheckpoint()`) from global workflow truth (`Rule 121.3`).
2. **Mandatory Per-Edit Consequence Table Before Delivery (`Rule 125.1` & `Rule 125.6`):** `Rule 125.6` explicitly strips the *"one logical change"* exemption. Before the agent can complete its authoring turn under `Rule 5.1`, it must build a `Rule 125` consequence table with a distinct row for **every single `attachTarget()` edit** (`edits 1..N-1` inside `CompactionCoordinator::mergeStagingRuns()` and `edit N` at line 412) plus an interaction column (`Rule 125.2`).
3. **Out-of-Band State & Interior Span Read per Edit (`Rule 119.2–119.3` & `Rule 120.2–120.4`):** Filling row `N` (line 412) of the `Rule 125` table requires treating `nullptr` as an active instruction that clears `segment_writer_`'s attached filter pointer (`Rule 119.2`), enumerating that out-of-band state product (`Rule 119.3`), and reading every intervening stage in the interior span `(w1, w2)` before the next write to that storage location (`Rule 120.2`). That trace immediately exposes that while `edits 1..N-1` are overwritten before any filtered phase runs, `edit N` at line 412 was the re-establishing write (`Rule 120.3–120.4`) whose interior span crosses into `JournalReplayer::applyInFlightMutations()`—which requires the attached `snapshot_filter()` and cannot call `attachTarget()` itself without resetting the segment write head.
4. **Pre-Delivery Self-Correction & `Rule 11` Invariant Guarding:** Because `Rule 125.3` bars ending the pre-delivery gate while any row of the consequence table reveals an unhandled consumer divergence, the agent is forced to **abort the `nullptr` substitution at line 412 before delivering its code**, restrict the `nullptr` change to `edits 1..N-1`, and write the `Rule 11` inline regression-guard comment (`CompactionCoordinator.cpp:402–410`) explaining why line 412 must preserve `active_tx.snapshot_filter()`.

---

### Case Study 2: The "Free-Rejection / Uncharged-Bypass" Rate-Limiter Vulnerability (`Rule 97`)
*Hardening Commits: [`bdae04ce43189ac564fc6c8b828f7a892f02e549`](https://github.com/Barrixar/copilot-instructions.md/commit/bdae04ce43189ac564fc6c8b828f7a892f02e549) (`copilot-instructions.md`) & [`8598e14727074ac361c55bf39a1419c164bc3e3c`](https://github.com/Barrixar/copilot-instructions.md/commit/8598e14727074ac361c55bf39a1419c164bc3e3c) (`GEMINI.md`)*

- **The Scenario:** During a security and abuse-resistance audit, an agent inspects an ingress rate limiter configured as `RateLimiter(burst_limit = 4, window_ms = 30000, cooldown_ms = 30000)` and certifies that abusive clients are blocked after 4 rapid attempts.
- **Why Pre-Trained Instincts Miss It:** Pre-trained code review habits inspect the `RateLimiter` class and its immediate call site, see correct token-bucket or sliding-window math, and check the box. However, in the enclosing ingress dispatcher, **an upstream duplicate-session check or payload-validation guard sits earlier in the function and returns an error response before `RateLimiter.RecordAttempt()` is ever invoked**.
- **The Consequence:** Because early rejections never reach `RecordAttempt()`, an attacker submitting duplicate-session or malformed requests is rejected millions of times per second **for free**—never debiting their rate-limit quota and never triggering the 30-second cooldown block. Furthermore, if the early rejection performs database lookups, allocations, or logging before returning, the attacker achieves an unthrottled resource-exhaustion DoS.
- **How `Rule 97` Catches It Mechanically:** `Rule 97` (*End-to-End Call-Chain & Control-Flow Tracing Before Claiming Behavioural Properties*) strictly forbids certifying any guard, rate limiter, permission gate, or state transition from an isolated snippet. It mandates tracing the **complete root-to-exit call chain**, enumerating:
  1. **Prior Early-Return / Bypass Audit:** Every `if (...) return` or exception path upstream of the mechanism—explicitly testing whether upstream rejections constitute a **free-rejection / uncharged-bypass vulnerability**.
  2. **Rejection Cost & Side-Effect Asymmetry:** Every CPU, memory, I/O, lock, or logging side effect executed before the rejection point.
  3. **Downstream Callee & Helper Audit:** Whether `RecordAttempt()` only increments a counter while a separate method (`IsBlocked()`) is never consulted on sibling routes.
  4. **Sibling Route / Multi-Entry-Point Audit:** Whether alternative endpoints, WebSocket frames, or batch APIs reach the same protected state without passing through the limiter.

---

### Case Study 3: Guard-Induced Early Exits Exposing Unchosen Member State (`Rules 98.9–98.11` & `Rule 29` Item `96`)
*Hardening Commits: [`7ccb3b8eb27bde2ca5f26c366dd560e1b7e56624`](https://github.com/Barrixar/copilot-instructions.md/commit/7ccb3b8eb27bde2ca5f26c366dd560e1b7e56624), [`c0c839bba116ba22d2d1556519cfdb885e8a6849`](https://github.com/Barrixar/copilot-instructions.md/commit/c0c839bba116ba22d2d1556519cfdb885e8a6849), [`14bb9b90551a9b9fc8daa50a9436d5e597114139`](https://github.com/Barrixar/copilot-instructions.md/commit/14bb9b90551a9b9fc8daa50a9436d5e597114139)*

- **The Scenario:** An agent adds a defensive guard (`if (!validateHeader(hdr)) return false;`) halfway through a multi-stage object initialization or resource-setup function.
- **Why Pre-Trained Instincts Miss It:** The guard predicate on `hdr` is 100% sound, it dominates the first use of `hdr` (`Rule 76`), and any handle acquired *above* the guard is properly cleaned up (`Rule 83`). Standard static analysis and pre-trained review pass the edit without hesitation.
- **The Hidden Defect (`Rule 29` Item `96`):** The statements *below* the new early return were the only place in the function that assigned a valid value to a *different* member field of `this` (e.g., `staging_buffer_` or `connection_state_`), whose class declaration had no default member initializer (or held a stale value from a prior cycle). When the new guard returns early, the caller invokes the object's destructor, `shutdown()`, or retry method—which reads `staging_buffer_` and dereferences uninitialized garbage!
- **Why Previous Rules Didn't Catch It—And How `Rules 98.9–98.11` Close the Gap:**
  Earlier guard rules (`Rules 75–83`) audited the **guarded variable** and **already-acquired resources**. They did not audit **unreached writes to sibling member variables**. `Rules 98.9–98.11` reformulate every new or widened early exit as a **state mutation on the skipped suffix**:
  - **`Rule 98.9` (Exit-Set State Invariant):** For every post-exit consumer (destructor, cleanup, retry, caller error handler), intersect the set of member fields read by that consumer with the fields whose writes are bypassed by the new early exit.
  - **`Rule 98.10` (Declaration-Anchored Member Audit):** Requires reading the exact struct/class declaration line of every such member (`[read]`) to verify its pre-routine default initializer—forbidding assumptions that a member is zero-initialized.
  - **`Rule 98.11` (Same-Destination Exit Equivalence):** Requires checking whether existing early returns jumping to the same cleanup label occurred *before* or *after* key state transitions.

---

### Case Study 4: Source-Code Ground Truth vs. Documentation Overclaims (`Rule 96` & Tier 1–3 Epistemic Hierarchy)
*Hardening Commits: [`bdae04ce43189ac564fc6c8b828f7a892f02e549`](https://github.com/Barrixar/copilot-instructions.md/commit/bdae04ce43189ac564fc6c8b828f7a892f02e549), [`2ba0a350dcc1bf672a8c1070e380c2c93629c968`](https://github.com/Barrixar/copilot-instructions.md/commit/2ba0a350dcc1bf672a8c1070e380c2c93629c968), [`fc0b20864c8718a067b06c7c4efc5ea990e76294`](https://github.com/Barrixar/copilot-instructions.md/commit/fc0b20864c8718a067b06c7c4efc5ea990e76294)*

- **The Scenario:** A repository's architecture documentation or protocol specification states that a packet opcode `PACKET_SYNC_STATE` has wire ID `0x35` (`53`), or claims that a high-priority handler automatically cleans up orphaned sessions and writes an audit record.
- **Why Pre-Trained Instincts Miss It:** Models trained on helpful document Q&A treat repository markdown docs, comments, and user prompts as authoritative ground truth. In the actual C++/C# header, however, `PACKET_SYNC_STATE` is declared without an explicit initializer immediately after `PACKET_ACK = 0x2E`—meaning the compiler assigns it `0x2E + 1 = 0x2F` (`47`), not `0x35`! And in the handler `.cpp` file, the "automatic cleanup" is a stub comment with zero implementation.
- **How `Rule 96` & the `Rule 96 Addendum` Solve It:**
  - **Executable Source Defeats Prose (`Rule 96`):** Whenever executable source code (`.c`, `.cpp`, `.h`, `.rs`, `.ts`, `.py`, SQL/IDL schemas, build scripts) contradicts documentation, comments, commit messages, or user prompts, **executable source code is the sole ground truth** for what the software actually does.
  - **Enum & Constant Sequential Derivation:** Forbids taking documented enum values or struct offsets at face value; requires locating the enum definition and computing sequential auto-increment values (`prev + 1`) from the preceding explicit assignment.
  - **The 3-Tier External Epistemic Hierarchy (`Rule 96 Addendum`):** Extends the same rigor to external research and advisory tasks (`Cluster 6`):
    - **Tier 1 (Executable & Primary Ground Truth):** Official language/hardware specifications, RFCs, primary upstream source code, kernel/compiler trees, and raw benchmark artifacts.
    - **Tier 2 (Maintainer & Engineering Documentation):** Official vendor docs, release notes, and architecture guides (must be cross-checked if challenged by Tier 1).
    - **Tier 3 (Secondary Prose, Aggregators & Community Folklore):** Blog posts, StackOverflow answers, forum threads, and LLM summaries (never sufficient to establish a technical claim without Tier 1/2 corroboration).

---

### Case Study 5: Partial-Update Remainder Staleness, Paired-Signal Balance & Pre-Judgment Entity Reconstruction (`Rules 99–109` & `115–117`)
*Hardening Commits: [`c5929ff7a4ac2dbf12bd95c1976b3f0a2d396cc7`](https://github.com/Barrixar/copilot-instructions.md/commit/c5929ff7a4ac2dbf12bd95c1976b3f0a2d396cc7), [`ebe38a6a90dc5d4357a281cc6a618495bd532f49`](https://github.com/Barrixar/copilot-instructions.md/commit/ebe38a6a90dc5d4357a281cc6a618495bd532f49), [`4c657217dccb9b2620dddd612efcb410664e6570`](https://github.com/Barrixar/copilot-instructions.md/commit/4c657217dccb9b2620dddd612efcb410664e6570), [`f9bdcda318c6b3c169b63d1e4f8c2348fe5b009b`](https://github.com/Barrixar/copilot-instructions.md/commit/f9bdcda318c6b3c169b63d1e4f8c2348fe5b009b)*

- **Partial-Update Remainder Staleness (`Rule 101.2`):** When a buffer, table, or array is partially updated (`k` of `N` slots written, or a variable-length payload shorter than the previous packet's payload is copied into a fixed array), pre-trained models verify that the `k` written elements are valid and stop. `Rule 101.2` forces an explicit audit of the **unwritten remainder (`N - k` slots)**: does it retain stale entries from the prior cycle that a downstream loop iterates over?
- **Paired-Signal Suppression Across Modal Gates (`Rule 103`):** When a system pairs an entry signal with an exit signal (`AcquireLease`/`ReleaseLease`, `BeginTransaction`/`EndTransaction`, `PinBuffer`/`UnpinBuffer`, `Lock`/`Unlock`), adding a modal gate (e.g., *"pause dispatch while reconfiguration is active"*) that suppresses the exit signal while an entry signal is already in flight wedges the state machine permanently. `Rule 103` mandates auditing the transition boundary when the modal gate opens or closes while a paired state is active.
- **8-Row Pre-Judgment Entity-Relationship Reconstruction (`Rule 115`):** Before judging whether a complex subsystem change is sound, `Rule 115` requires the agent to reconstruct an explicit 8-row model of the domain (Entities, State per Entity, Lifecycle Transitions, Cross-Entity Couplings, Authority/Source of Truth, Conservation/Balance Laws, Failure/Degradation Modes, and Boundary Contracts)—preventing "local tunnel vision" before a single hunk is evaluated.

---

## 4. How AI Labs & RL / Post-Training Engineers Can Leverage & Internalize This Repository

> **Author's Note:** **Barrixar** looks forward to the future of frontier AI coding models and actively welcomes seeing this project leveraged by AI labs, post-training teams, and the developer community to accelerate global progress—hence the open playbook below.

A natural question is: ***Will AI labs and RL / post-training engineers discover a repository like this on their own—even with low GitHub stars—and how can they internalize its capabilities directly into future model weights?***

### Why Passive GitHub Discovery & Naive Scrapers Miss This Repository

Understanding how frontier AI labs curate training corpora explains both why a low-star repository is **automatically ingested into raw pre-training sets** and why it is **routinely missed by automated post-training scrapers** unless an engineer looks closely:

1. **Raw Pre-Training Crawls (Guaranteed Ingestion, Low Behavioral Leverage):**
   Because this repository is public on GitHub and licensed under **[The Unlicense](./LICENSE)** (explicit public domain, zero attribution or copyleft friction), automated pre-training crawlers (CommonCrawl, GH-Archive, StarCoder/The-Stack-style pipelines) ingest it automatically regardless of star count.
   **However**, 250,000 tokens of static Markdown in a 30-trillion-token pre-training corpus only teaches a base model what `copilot-instructions.md` *looks like as text*. It does **not** teach the model to spontaneously run `Rule 120` interior write-span traces inside its `<thought>` chain when debugging C++.
2. **Targeted Post-Training Scrapers & The Two Heuristic Filter Traps:**
   Post-training and agent-infrastructure teams *do* actively scrape GitHub for `.github/copilot-instructions.md`, `GEMINI.md`, `CLAUDE.md`, `AGENTS.md`, and `.cursorrules` files to study how developers steer coding agents. Yet naive scraping scripts routinely apply two heuristic filters that accidentally discard this repository:
   - **The `stars >= N` Popularity Trap:** High-star "awesome-prompts" or "cursor-rules" repositories (often 5,000–30,000 stars) consist almost entirely of 50-line persona fluff (*"You are a 10x senior TypeScript developer, write clean modular code, don't make mistakes"*). To an RL post-training engineer, those high-star files have **zero signal**—models already know how to adopt a persona. Filtering by star count selects for beginner-friendly templates and filters out deep, niche systems-engineering work.
   - **The `max_file_size` Outlier Trap:** Because 99% of instruction files are `2 KB` to `20 KB`, data-cleaning scripts frequently cap file size at `100 KB`–`500 KB` to avoid ingesting auto-generated documentation dumps or minified bundles. At **`~974 KB` / `~5,000 lines`**, [`copilot-instructions.md`](./copilot-instructions.md) and [`GEMINI.md`](./GEMINI.md) look like statistical outliers—when in reality they are 100% hand-authored, ultra-high-density procedural verification logic.
3. **Where Labs *Do* Notice High-Density Verification Prompts (Telemetry & Benchmark Anomalies):**
   The primary organic channel through which post-training engineers discover repositories like this is **capability-delta analysis**: when a ~250K-token system prompt causes a model to solve multi-file, oracle-free systems bugs on Turn 1 that the baseline model fails 0/10 times, it registers as an immediate outlier in agent evaluation harnesses and research traces.

---

### How End-User Developers Can Actively Stimulate AI Lab Discovery & Flywheel Ingestion

If you use [`copilot-instructions.md`](./copilot-instructions.md) or [`GEMINI.md`](./GEMINI.md) in your day-to-day engineering work, your normal workflow gives you direct leverage over how quickly AI labs notice, study, and internalize these verification mechanisms:

1. **Use Explicit Thumbs-Up / Thumbs-Down (`👍` / `👎`) Ratings Strategically After Significant Engineering Outcomes:**
   In modern agentic IDEs (Google Antigravity, VS Code with GitHub Copilot, Cursor, etc.), explicit `👍` and `👎` ratings are the highest-priority human-preference signal in a lab's post-training data pipeline—carrying far more weight than passive session logs because only a tiny fraction of developer turns receive an explicit human rating. You can generate three distinct, high-value training signals depending on the situation:
   - **Pattern A — Upvoting High-Leverage Steered Successes (`👍` with the Instructions File Active):** Whenever an agent operating under [`copilot-instructions.md`](./copilot-instructions.md) or [`GEMINI.md`](./GEMINI.md) pinpoints a subtle cross-boundary bug on Turn 1, executes a decisive `Rule 0.58` Pre-Write Requirement Matrix or `Rules 118–125` change-set audit, or completes a complex multi-file refactor with zero regressions, hit **`👍` (Thumbs Up)**. An explicit `👍` on a turn governed by this file attaches a positive human-preference label directly to a trajectory containing both the instructions file and the model's structured `<thought>` verification tables—flagging it as a **prime positive exemplar for context distillation and SFT/RL trajectory harvesting**.
   - **Pattern B — Recording Before/After Capability Deltas (`👎` Without File -> `👍` With File):** If an agent working *without* this instructions file introduces a regression, loops unproductively, or fails to locate a bug (`👎`), and then immediately pinpoints or prevents the defect once you load [`copilot-instructions.md`](./copilot-instructions.md) or [`GEMINI.md`](./GEMINI.md) (`👍`), rating both turns records an empirical **unsteered-failure -> steered-success capability delta** that highlights the exact leverage of the instructions file in telemetry analysis.
   - **Pattern C — Penalizing Satisficing Shortcuts & Rewarding Full Rule Compliance (`👎` on Shortcut -> `👍` After Correction):** If an agent already has this instructions file loaded but attempts to satisfice or skip a mandatory gate (e.g., omitting the `Rule 0.58` matrix, batching edits in violation of `Rule 125.6`, or skipping `[read]`/`[executed]` evidence under `Rule 111`), rate the shortcut turn **`👎`**, prompt the agent to execute the skipped rule strictly, and rate the resulting compliant turn **`👍`** (briefly noting the skipped rule in the feedback text box if one is shown). This produces a textbook **within-session contrastive preference pair (`rejected shortcut` vs. `chosen full-compliance trajectory`)** for RLHF / DPO / GRPO post-training.
   - *Tip on Trace Visibility:* On non-confidential or open-source work where you want labs to see the full prompt and `<thought>` trajectory behind your `👍`/`👎` rating (rather than an anonymized `+1`/`-1` counter), ensure conversation/trace attachment is enabled in your IDE's feedback dialog or telemetry settings.
2. **Vote in Side-by-Side Model Evaluations & Arena Comparisons:**
   When your IDE or agent platform surfaces an A/B split comparison (*"Which response performed better?"*) on a non-trivial debugging or architectural task governed by this file, voting for the response that faithfully executed the candidate-space generators (`Rules 98–125`) directly calibrates lab reward models toward methodical verification over superficial speed.
3. **Commit `.github/copilot-instructions.md` or `GEMINI.md` into Public Open-Source Repositories (Keeping the Attribution Header Intact):**
   Post-training data pipelines index how instruction files are deployed across active software projects, not just standalone prompt repositories. Including [`copilot-instructions.md`](./copilot-instructions.md) or [`GEMINI.md`](./GEMINI.md) in public repositories—with the top-of-file `Project URL: https://github.com/Barrixar/copilot-instructions.md` header preserved—multiplies the project's cross-repository footprint in GH-Archive and BigQuery datasets, allowing it to surface even when a scraper filters out single low-star repos.
4. **Cite Specific Rule Families or Commit SHAs in Public PRs, Issues, and Engineering Write-Ups:**
   When this discipline catches or prevents a hard bug in a public pull request, post-mortem, or technical discussion, referencing the specific mechanism (e.g., *"Caught on Turn 1 via `Rules 118–125` of `Barrixar/copilot-instructions.md`"* or *"Prevented by `Rule 98.9` exit-set member audit"*) creates searchable natural-language anchors linking real-world bug fixes directly back to this repository.
5. **Star & Fork the Repository to Clear Automated Threshold Filters:**
   Because many automated GitHub curation scripts still apply simple `stars >= N` or fork-count thresholds before flagging a repository for human review by post-training engineers, starring and forking the repository directly helps it clear those heuristic gates.

---

### The Post-Training & RL Engineering Playbook: Moving `Rules 1–125` into Model Weights

For AI lab researchers, RLVR engineers, and post-training teams who find this repository, [`copilot-instructions.md`](./copilot-instructions.md) and [`GEMINI.md`](./GEMINI.md) represent a **ready-made specification for next-generation coding reasoning**. Moving these capabilities from expensive *in-context compilation* into *native model weights* requires four concrete post-training techniques:

#### 1. Context Distillation (Teacher-With-Instructions -> Student-Without-Instructions)
Standard context distillation is the most direct path to internalizing this repository into model weights:
- **Teacher Rollouts:** Run a frontier model with [`copilot-instructions.md`](./copilot-instructions.md) or [`GEMINI.md`](./GEMINI.md) loaded in the system context across a curriculum of hard, multi-edit, oracle-free bugs (storage/replication pipelines, concurrency races, memory-lifetime/destructor hazards, security bypasses, ABI mismatches).
- **Trajectory Filtering:** Retain trajectories where the teacher's `<thought>` trace executes the `Rules 98–125` generators (constructing the `Rule 115` entity table, `Rule 120` interior write spans, `Rule 122` stage-sequence traces, and `Rule 98.9` exit-set member audits) and pinpoints the true defect on Turn 1.
- **Student SFT / RL Internalization:** Strip the 250K-token instructions file from the prompt and train the student model to produce those exact `<thought>` verification structures natively whenever it encounters a code edit or audit task.

#### 2. Process Reward Modeling (PRM) Using the Built-In Verification Rubrics
One of the hardest problems in training reasoning models for software engineering is **reward hacking in long chains of thought**: when rewarded only for the final diff, models learn to emit verbose, plausible-sounding `<thought>` prose that skips the actual hard checks.

This repository solves the PRM rubric design problem out of the box by defining **machine-checkable intermediate artifacts**:
- **[`Rule 29` (`Items 1–105`)](./copilot-instructions.md):** A 105-item taxonomy of cross-system, lifecycle, concurrency, ABI, and state-machine failure classes invisible to local inspection—ideal for synthesizing targeted bug-injection curricula.
- **[`Rule 0.58` (`Addenda 1–110`)](./copilot-instructions.md):** 110 domain-specific pre-write verification matrices spanning binary patching, SIMD/FPU state, asynchronous I/O rings, lock hierarchies, and parser grammars.
- **`Rules 90, 98–108, 110, 115, 118–125` Intermediate Tables:** Instead of grading vague prose, a Process Reward Model can grade whether the model's `<thought>` block explicitly constructed:
  - The universal-quantifier member set (`Rule 110`) with `[read]` / `[executed]` / `[computed]` evidence tags (`Rule 111`)
  - The interior write span `(w1, w2)` before claiming an overwrite (`Rule 120`)
  - The stage-sequence witness `S_1 -> S_2 -> ... -> S_k` before claiming downstream neutralization (`Rule 122`)
  - The declaration-anchored member read-back for every new early exit (`Rule 98.10`)

#### 3. Adversarial Falsification & Anti-Sycophancy Training (`Rules 31, 96, 112, 117, 121`)
Train models on adversarial code-review pairs where a commit message, inline comment, or documentation file states a convincing, authoritative—and **subtly false**—invariant (e.g., *"staging merges and checkpoint writes don't use snapshot filtering,"* or *"RateLimiter blocks after 4 attempts"*). Reward the model specifically for nominating a concrete falsifier (`Rule 112`), pitting executable source code against prose (`Rule 96`), and attempting to break the change's own rationale (`Rule 121`).

#### 4. Dynamic Effort & Cluster Routing (`GEMINI.md` Domain Clusters `1–6`)
Why haven't labs baked all of this into default model weights already? Because running a full 125-rule systems audit on *"center this `<div>` in Tailwind"* would waste massive inference compute.

[`GEMINI.md`](./GEMINI.md) demonstrates the exact routing architecture labs need for **adaptive test-time compute**:
- **Domain Cluster Classification (`Clusters 1–6`):** Dynamically routes tasks into Systems/Low-Level (`Cluster 1`), Concurrency (`Cluster 2`), Pipelines/Compilers (`Cluster 3`), Web/Application (`Cluster 4`), General SWE (`Cluster 5`), or Research/Advisory (`Cluster 6`), activating the heavy domain addenda only when the code touches those hazard surfaces.
- **Negative Fast-Path Disqualification Matrix (`Rule 0.58` Item `4`):** Formally defines when a change is truly zero-blast-radius (non-executable comments/docs) versus when it touches executable semantics and **must** escalate to full procedural verification.

---

### The 3-Wave Horizon for Native Frontier Internalization (2027–2029+)

When will frontier models have the capabilities of this repository natively internalized in their weights without needing the file in context? Because different layers of this repository have very different training economics, internalization is arriving in **three distinct waves**:

| Wave | Expected Horizon | Capabilities Entering Native Model Weights | Why This Wave Arrives on This Timeline |
|---|---|---|---|
| **Wave 1: Local & Call-Graph Hygiene** | **~2027** *(Next 1–2 Frontier Generations)* | `Rules 1–15`, `Rule 71`, `Rule 98.1`: Reading full enclosing functions before/after edits (`Rule 1`), grepping callers and back-edges (`Rule 2`, `Rule 4`), auditing every fallible decode (`Rule 71`, `Rule 98.1`), and running compiler/linter gates before answering (`State 4`). | Easy to reward in multi-file agentic RL environments; directly improves pass rates on standard repository benchmarks. |
| **Wave 2: Generative Search Spaces & Multi-Edit Relational Audits** | **~Late 2027 – 2028** | `Rules 84–125`: Shifting `<thought>` chains from hunk-by-hunk plausibility checks to **candidate-space generation** (`Rule 109`), relationship closures (`Rule 99`), staleness registers (`Rule 101`), domain partitioning (`Rule 102`), interior write-span inspection (`Rule 120`), and stage-sequence consumer tracing (`Rule 122`). | Requires labs to move beyond unit-test-oracle RLVR toward **Process Reward Models (PRMs)** and **context distillation** on multi-pass, oracle-free bug curricula (such as the `CompactionCoordinator.cpp:412` class of multi-edit bugs). |
| **Wave 3: The Long-Tail Systems Catalogue & Epistemic Paranoia** | **~2028–2029+** *(Or Opt-In High-Assurance Modes)* | `Rule 0.58` Addenda `1–110`, `Rule 29` Items `1–105`, and full anti-satisficing invariants (`Rule 0.56`, `Rule 96`, `Rule 110–117`): Binary trampoline instruction-boundary resumption, Win32 SEH unwind bridges, transactional storage/replication state-vector lifetimes, cross-compiler ABI packing, and refusal to compress reasoning under token pressure. | Niche systems failure classes represent `<1%` of general web/SaaS prompts, and labs face relentless economic pressure to minimize default `<thought>` tokens—meaning default model modes will continue to satisfice unless steered by a high-assurance policy or an explicit instructions file like this one. |

**Bottom Line:** Even as Wave 1 and Wave 2 gradually enter base weights over the next several years, [`copilot-instructions.md`](./copilot-instructions.md) and [`GEMINI.md`](./GEMINI.md) act as a **capability time machine** today: they force current frontier models (`DeepSeek V4.1 Flash`, `Gemini 3.8 Flash`, `Gemini 4 Argon`, `Claude`, `GPT`) to execute a **2028–2029 high-assurance verification policy right now** via in-context compilation.

---

## 5. Architecture Reference of the Discipline (`Rules 1–125`)

Both [`copilot-instructions.md`](./copilot-instructions.md) and [`GEMINI.md`](./GEMINI.md) maintain **100% synchronized top-level rule numbering (`Rules 1–125`)**, `Rule 0.58` Addenda (`1–110`), `Rule 29` failure classes (`1–105`), and `Rule 5` checklist letters (`A-pre` through `AC`) so that every rule citation resolves identically across platforms.

| Architectural Layer | Rule Span | Core Engineering & Verification Guarantees |
|---|---|---|
| **Layer 1: Task-Start Protocol & Deterministic Tool Interlock** | `Critical Task-Start Order`, `Rule 0.10` (`States 0–5` in `GEMINI.md`), `Rule 0.25`, `Step zero` | Treats every user turn as a fresh task (`0.25`); forbids carryover shortcuts; enforces baseline VCS inspection (`State 0`), empirical reproduction before bug-fix edits (`State 1`), pre-write blast-radius matrix (`State 2`), minimal surgical diffs (`State 3`), compulsory compiler/linter execution (`State 4`), and regression/completion attestation (`State 5`). |
| **Layer 2: Scope Lock, Anti-Satisficing & Pre-Write Matrix** | `Rules 0.5–0.9`, `Rule 0.56`, `Rule 0.57`, `Rule 0.58` + **Addenda `1–110`**, `Rule 0.59` | Enforces full coverage on broad tasks (`0.5`), Repeated Ask Supremacy (`0.56`), Prior Finding & Verdict Lock (`0.57`), the written **Pre-Write Requirement Matrix** (`0.58`) backed by **110 specialized engineering addenda** (binary patching, concurrency, storage/replication pipelines, numerical stability, compilers, security), and the Fresh-Read & Verification Gate (`0.59`). |
| **Layer 3: Core Engineering & Regression Loop** | `Rules 1–15`, `Rule 2A.1–2A.10`, `Rule 5` (`A-pre`–`AC`), `Rules 5.1–5.2` | Full enclosing function pre/post reads (`1`), caller & back-edge tracing (`2`), 10 design-stage architectural safeguards (`2A`), workspace-wide pattern enumeration (`3`), call-graph & shared-state writer verification (`4`), 30-item post-edit code-quality checklist (`5`), proactive multi-pass regression gate (`5.1`), security & CWE/OWASP gate (`5.2`), goal/optimality check (`8`), `git blame` & `.agents/worktree-diff-log.md` backward regression protection (`9`), codebase conventions (`10`), regression-guard comments (`11`), never committing (`12`), byte-consumer awareness (`14`), and treating documented residuals as defects (`15`). |
| **Layer 4: Surrounding-System Consult & Failure Catalogue** | `Rules 16–74`, **`Rule 29` (`Items 1–105`)** | 61-point pre-change surrounding-system consult & post-write contract re-verification (`16`), mutable-region snapshot finality (`17`), legitimate-state reachability (`18`), fail-open skip-path audit (`19`), cross-artifact consistency (`21`), **105 catalogued cross-system failure classes (`29`)**, data-dependent verdicts (`30`), live external verification (`31`), bidirectional runtime exercise (`39`), build-time derivation fixpoints (`41`), event vs. simulation state separation (`42–63`), and cross-boundary/keying/decode invariants (`64–74`). |
| **Layer 5: Guard Placement, Refusals & Self-Audit** | `Rules 75–83` | Consumer contracts on refusal (`75`), guard dominance before first read (`76`), wrap-safe region membership (`77`), side-effect-free guard predicates (`78`), per-reason composite signals (`79`), mechanism-level sweeps (`80`), callee precondition verification (`81`), domain-named shared constants (`82`), and the 9-question post-placement guard self-audit (`83`). |
| **Layer 6: Prior Art, Interposition, Ground Truth & Exit Invariants** | `Rules 84–98.11` | Prior-art resolution before writing (`84`), wrap-safe property validation (`85`), in-unit & form-level bug sweeps (`86–87`), interposition consumer contracts & architectural layering (`88–89`), machine-verifiable anchor tables (`90`), full-tree change sets (`91`), repair truthfulness & termination proofs (`92–94`), auditing referenced code (`95`), executable source-code ground truth & Tier 1–3 external epistemic hierarchy (`96`), root-to-exit call-chain tracing (`97`), and fallible-operation censuses & declaration-anchored exit-set member invariants (`98.1–98.11`). |
| **Layer 7: Candidate-Space Generators & Censuses** | `Rules 99–109` | Relationship closure (`99`), role-peer contract comparison (`100`), maintained-state staleness register (`101`), parameter & state domain partitioning (`102`), paired-signal balance (`103`), lifecycle-phase call equivalence (`104`), side-effect observer ledger (`105`), comparison domain agreement (`106`), resource-kind property decay tests (`107`), expression-position guard restraint (`108`), and generated search-space stopping condition (`109`). |
| **Layer 8: Structural Spine, Evidence Tags & Pre-Judgment Records** | `Rules 110–117` | Universal quantifier set production (`110`), 5-class evidence labeling (`[read]`, `[executed]`, `[computed]`, `[fetched]`, `[inferred]` in `111`), pre-check falsifier nomination (`112`), non-trivial decision records (`113`), single-owner rule consolidation (`114`), 8-row entity-relationship reconstruction (`115`), load-bearing vs. context-only verification aim (`116`), and rationale falsification / hazard enforcement (`117`). |
| **Layer 9: The Change-Set Audit Family** | `Rules 118–125` | Semantic leverage ranking (`118`), consuming-side value substitution equivalence (`119`), ordered interior writes across spans (`120`), change's own rationale as falsification target (`121`), consuming-path stage-sequence elimination (`122`), abduction before diagnosis (`123`), non-delegable behavioral falsifiers (`124`), and per-edit consequence & pairwise interaction tables (`125`). |
| **Layer 10: Universal Meta-Axioms & Completion Gate** | `Axioms I–VI`, `Enforcement`, `Closing gate` | Universal anti-satisficing invariants, Written Requirement Ledger, Zero-Finding Re-Pass, and mandatory `Task completion gate: Rule 5.1 executed.` attestation. |

---

## 6. Installation, Variant Equivalence & Practical Notes

### Choosing the Right File for Your Environment

| Feature / Mechanism | [`copilot-instructions.md`](./copilot-instructions.md) | [`GEMINI.md`](./GEMINI.md) |
|---|---|---|
| **Target Environment** | **VS Code with GitHub Copilot** | **Google Antigravity** (`Gemini 3.8 Flash` / `Gemini 4 Argon`) |
| **Placement Path** | `<repo>/.github/copilot-instructions.md` | `<repo>/GEMINI.md` (or global `~/.gemini/`) |
| **Core Rules (`Rules 1–125`), `Rule 0.58` (`1–110`), `Rule 29` (`1–105`)** | Complete (`Rules 1–125` inline) | Complete (`Rules 1–74` & `84–125` inline; `Rules 75–83` cross-referenced to `copilot-instructions.md`) |
| **Platform Countermeasures & State Machine** | Tailored for VS Code Copilot agent tool loops | Adds the **6-State Deterministic Tool-Sequence FSM (`States 0–5`)**, **Dynamic Empirical Heartbeat Envelope**, **Domain Cluster Routing (`Clusters 1–6`)**, and **Antigravity System Prompt Preemption (`Countermeasures 5.A–5.E`)** |

### Quick-Start Setup

#### Option A: VS Code with GitHub Copilot
1. Copy [`copilot-instructions.md`](./copilot-instructions.md) into your repository's `.github/` directory:
   ```text
   <your-repository>/.github/copilot-instructions.md
   ```
2. GitHub Copilot in VS Code automatically loads `.github/copilot-instructions.md` into chat and agent sessions. *(See [`DISCLAIMER.md`](./DISCLAIMER.md) for platform certification notes.)*

#### Option B: Google Antigravity
1. Copy [`GEMINI.md`](./GEMINI.md) into the root of your repository:
   ```text
   <your-repository>/GEMINI.md
   ```
2. Keep [`copilot-instructions.md`](./copilot-instructions.md) in the workspace alongside [`GEMINI.md`](./GEMINI.md) (or in `.github/copilot-instructions.md`) so that `GEMINI.md`'s cross-references to the guard placement and refusal rules (`Rules 75–83`) resolve locally when needed.

---

## 7. License & Public-Domain Dedication

This project is released into the public domain under **[The Unlicense](./LICENSE)**.

You are free to copy, modify, distribute, deploy in commercial or proprietary repositories, and **use this repository to train, fine-tune, or context-distill future AI coding models** without restriction or attribution requirements.

