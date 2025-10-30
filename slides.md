---
theme: default
class: text-center
highlighter: shiki
lineNumbers: false
info: |
  ## Huxley-Gödel Machine
  Human-Level Coding Agent Development by an Approximation of the Optimal Self-Improving Machine
drawings:
  persist: false
transition: slide-left
title: Huxley-Gödel Machine
mdc: true
colorSchema: auto
---

<div class="grid grid-cols-2 gap-16 h-full items-center px-16">

<div class="text-left space-y-8">

<div>
<div class="text-5xl font-bold leading-tight">
Huxley-Gödel Machine
</div>

<div class="text-2xl opacity-80 mt-8 leading-relaxed">
Human-Level Coding Agent Development by an Approximation of the Optimal Self-Improving Machine
</div>
</div>

<div class="text-base opacity-50">
KAUST, 2025
</div>

</div>

<div class="flex items-center justify-center">
<img src="/images/title-figure.jpg" class="max-h-[480px] rounded-lg shadow-2xl" />
</div>

</div>

---

# The Challenge

<div class="grid grid-cols-2 gap-16 mt-16">

<div class="flex flex-col items-center justify-center">
<div class="text-6xl mb-6">🎯</div>
<div class="text-2xl font-bold mb-4">Central Question</div>
<div class="text-xl text-center">
Which self-modifications<br/>should we accept?
</div>
</div>

<div class="space-y-8">

<div class="bg-red-50 dark:bg-red-900 p-6 rounded-lg">
<div class="text-xl font-bold mb-2">❌ Prior Approach</div>
<div>DGM & SICA use benchmark scores</div>
<div class="text-sm opacity-70 mt-2">Assume: High score → Better lineage</div>
</div>

<div class="bg-orange-50 dark:bg-orange-900 p-6 rounded-lg">
<div class="text-xl font-bold mb-2">⚠️ The Problem</div>
<div class="text-lg">High scores ≠ Good descendants</div>
</div>

</div>

</div>

---

# Metaproductivity-Performance Mismatch

<div class="flex flex-col items-center justify-center h-full gap-8">

<div class="grid grid-cols-2 gap-16 text-3xl font-bold">
<div class="text-center">
<div class="text-red-500">Performance</div>
<div class="text-xl mt-2 font-normal">Immediate scores</div>
</div>

<div class="text-center">
<div class="text-green-500">Metaproductivity</div>
<div class="text-xl mt-2 font-normal">Long-term potential</div>
</div>
</div>

```mermaid
graph LR
    A[Agent A<br/>Score: 0.8 🔴] --> B[Score: 0.75]
    A --> C[Score: 0.70]

    X[Agent X<br/>Score: 0.7 🟢] --> Y[Score: 0.85]
    X --> Z[Score: 0.90 ⭐]

    style A fill:#fee
    style X fill:#efe
    style Z fill:#ffe
```

<div class="text-xl text-center opacity-70 mt-4">
Lower score → Better descendants!
</div>

</div>

---

# Self-Improvement as Tree-Search

<div class="grid grid-cols-2 gap-12 items-center">

<div>

```mermaid
graph TD
    A0[a₀<br/>Initial Agent] --> A1[a₁]
    A0 --> A2[a₂]
    A1 --> A3[a₃]
    A1 --> A4[a₄]
    A2 --> A5[a₅]
    A4 --> A6[a₆ ⭐]

    style A0 fill:#e3f2fd
    style A6 fill:#ffd54f
```

<div class="mt-4 text-center text-2xl">
🌳 Tree of evolved agents
</div>

</div>

<div class="text-xl">

## At each step:

<div class="space-y-6 mt-8">

<div class="flex items-center gap-4">
<div class="text-4xl">🔧</div>
<div><strong>Modify</strong> agent → create child</div>
</div>

<div class="flex items-center gap-4">
<div class="text-4xl">📊</div>
<div><strong>Evaluate</strong> agent on task</div>
</div>

<div class="flex items-center gap-4">
<div class="text-4xl">🎯</div>
<div><strong>Goal:</strong> Find best final agent</div>
</div>

</div>

</div>

</div>

---

# From Gödel Machine to HGM

<div class="flex items-center justify-center h-full">

<div class="grid grid-cols-3 gap-8 text-center">

<div class="flex flex-col items-center gap-4">
<div class="text-6xl">🧮</div>
<div class="text-2xl font-bold">Gödel Machine</div>
<div class="text-lg opacity-70">Formal proofs<br/>Theoretically optimal</div>
</div>

<div class="flex flex-col items-center justify-center">
<div class="text-6xl">→</div>
</div>

<div class="flex flex-col items-center gap-4">
<div class="text-6xl">⚡</div>
<div class="text-2xl font-bold">HGM</div>
<div class="text-lg opacity-70">Estimate CMP<br/>Practical approximation</div>
</div>

</div>

</div>

<div class="mt-12 text-center text-xl">
<v-click>

<strong>Key Insight:</strong> In coding agent setting, we can approximate optimality without proofs!

</v-click>
</div>

---

# Clade-Metaproductivity (CMP)

<div class="grid grid-cols-2 gap-12 items-center">

<div>

## The Idea: Focus on **Lineages**

```mermaid
graph TD
    A[Agent a] --> B[Child 1]
    A --> C[Child 2]
    B --> D[Descendant]
    B --> E[Descendant]
    C --> F[Descendant ⭐]

    style A fill:#e1f5ff
    style B fill:#ffe1e1
    style C fill:#ffe1e1
    style D fill:#fff3e1
    style E fill:#fff3e1
    style F fill:#ffd54f
```

<div class="text-center mt-4 text-xl">
🌿 <strong>Clade</strong> = Agent + all descendants
</div>

</div>

<div class="text-xl">

## Why CMP?

<div class="space-y-6 mt-8">

<div>
✅ Modest ancestor can have great descendants
</div>

<div>
✅ More statistically robust
</div>

<div>
✅ Inspired by biology (Huxley)
</div>

<div>
✅ Captures long-term potential
</div>

</div>

</div>

</div>

---

# Theorem 1: CMP Oracle = Gödel Machine

<div class="flex flex-col items-center justify-center h-full gap-12">

<div class="bg-blue-50 dark:bg-blue-900 p-8 rounded-lg text-center text-2xl max-w-4xl">
<strong>CMP oracle is sufficient to implement the Gödel Machine</strong>
</div>

<div class="grid grid-cols-3 gap-8 text-center">

<div class="flex flex-col items-center gap-4">
<div class="text-5xl">🎯</div>
<div class="text-xl">CMP ≡ Q-value</div>
</div>

<div class="flex flex-col items-center gap-4">
<div class="text-5xl">✓</div>
<div class="text-xl">Provably optimal</div>
</div>

<div class="flex flex-col items-center gap-4">
<div class="text-5xl">⚡</div>
<div class="text-xl">No proofs needed</div>
</div>

</div>

<v-click>
<div class="text-2xl text-center bg-green-50 dark:bg-green-900 p-6 rounded-lg max-w-3xl">
💡 <strong>Insight:</strong> Estimate CMP → Approximate Gödel Machine
</div>
</v-click>

</div>

---

# HGM: How to Estimate CMP?

<div class="flex flex-col items-center justify-center h-full gap-10">

<div class="text-2xl text-center max-w-3xl">
Aggregate success across <strong>entire clade</strong> (lineage)
</div>

<div class="bg-blue-50 dark:bg-blue-900 p-8 rounded-xl shadow-lg">
<div class="text-3xl text-center">

$$\widehat{\text{CMP}}(a) = \frac{\text{successes in clade}}{\text{total tests in clade}}$$

</div>
</div>

<div class="grid grid-cols-3 gap-10 mt-4">

<div class="text-center">
<div class="text-5xl mb-3">📊</div>
<div class="text-lg font-semibold">Clade-level</div>
<div class="text-sm opacity-70">aggregation</div>
</div>

<div class="text-center">
<div class="text-5xl mb-3">⚖️</div>
<div class="text-lg font-semibold">Weighted by</div>
<div class="text-sm opacity-70">evaluations</div>
</div>

<div class="text-center">
<div class="text-5xl mb-3">🎲</div>
<div class="text-lg font-semibold">Thompson</div>
<div class="text-sm opacity-70">Sampling</div>
</div>

</div>

</div>

---

# HGM: Three Adaptive Policies

<div class="grid grid-cols-3 gap-8 mt-10">

<div class="bg-blue-50 dark:bg-blue-900 border-2 border-blue-400 dark:border-blue-600 rounded-xl p-8 shadow-lg">
<div class="text-center text-5xl mb-4">🔧</div>
<div class="text-center text-2xl font-bold mb-4">Expansion</div>
<div class="text-center opacity-80 mb-4">
Which agent to modify?
</div>
<div class="text-center text-lg bg-blue-100 dark:bg-blue-800 p-3 rounded">
Use <strong>clade CMP</strong>
</div>
</div>

<div class="bg-green-50 dark:bg-green-900 border-2 border-green-400 dark:border-green-600 rounded-xl p-8 shadow-lg">
<div class="text-center text-5xl mb-4">📊</div>
<div class="text-center text-2xl font-bold mb-4">Evaluation</div>
<div class="text-center opacity-80 mb-4">
Which agent to test?
</div>
<div class="text-center text-lg bg-green-100 dark:bg-green-800 p-3 rounded">
Use <strong>individual stats</strong>
</div>
</div>

<div class="bg-purple-50 dark:bg-purple-900 border-2 border-purple-400 dark:border-purple-600 rounded-xl p-8 shadow-lg">
<div class="text-center text-5xl mb-4">⚖️</div>
<div class="text-center text-2xl font-bold mb-4">Selection</div>
<div class="text-center opacity-80 mb-4">
Expand or evaluate?
</div>
<div class="text-center text-lg bg-purple-100 dark:bg-purple-800 p-3 rounded">
<strong>Adaptive</strong> scheduling
</div>
</div>

</div>

<div class="mt-10 text-center text-xl bg-yellow-50 dark:bg-yellow-900 p-5 rounded-xl shadow-md max-w-4xl mx-auto">
🚀 <strong>Key Innovation:</strong> Decoupled expansion from evaluation!
</div>

---

# HGM in Practice

<div class="flex items-center justify-center h-full">

<div class="grid grid-cols-2 gap-16 text-center">

<div>
<div class="text-4xl mb-4">⚡</div>
<div class="text-2xl font-bold mb-2">Asynchronous</div>
<div class="text-lg">Run on all CPUs<br/>Early stopping</div>
</div>

<div>
<div class="text-4xl mb-4">🏆</div>
<div class="text-2xl font-bold mb-2">Best-Belief</div>
<div class="text-lg">Select final agent<br/>by posterior</div>
</div>

</div>

</div>

---

# Experimental Setup

<div class="flex items-center justify-center h-full">

<div class="grid grid-cols-3 gap-12 text-center max-w-5xl">

<div>
<div class="text-5xl mb-4">📊</div>
<div class="text-xl font-bold mb-3">Benchmarks</div>
<div class="text-base">
SWE-bench Verified (500)<br/>
SWE-bench Lite (300)<br/>
Polyglot
</div>
</div>

<div>
<div class="text-5xl mb-4">🤖</div>
<div class="text-xl font-bold mb-3">Baselines</div>
<div class="text-base">
DGM<br/>
SICA<br/>
SWE-agent
</div>
</div>

<div>
<div class="text-5xl mb-4">🧠</div>
<div class="text-xl font-bold mb-3">Models</div>
<div class="text-base">
GPT-5 / GPT-5-mini<br/>
Qwen3-Coder
</div>
</div>

</div>

</div>

---
layout: center
---

# Main Results from Paper

<div class="flex items-center justify-center">
<img src="/images/figure1-main-results.jpg" class="max-w-full max-h-[500px] rounded-lg shadow-2xl" />
</div>

---

# Result 1: CMP Correlation

<div class="flex items-center justify-center h-full">

<div class="max-w-4xl">

| Method | Weighted Correlation | Unweighted Correlation |
|--------|---------------------|------------------------|
| SICA   | 0.444 / 0.274       | 0.444 / 0.274          |
| DGM    | 0.285 / 0.383       | 0.406 / 0.357          |
| <strong>HGM</strong> | <strong>0.778 / 0.626</strong>   | <strong>0.512 / 0.873</strong>      |

<div class="text-sm mt-4 opacity-70">SWE-Verified-60 / Polyglot</div>

<div class="mt-12 text-2xl text-center bg-green-50 dark:bg-green-900 p-6 rounded-lg">
📈 HGM: <strong>2-3× better correlation</strong> with true metaproductivity
</div>

</div>

</div>

---

# Result 2: Performance & Efficiency

<div class="grid grid-cols-2 gap-16 mt-12">

<div>

## 🎯 Accuracy

<div class="space-y-6 mt-8">

<div class="bg-gradient-to-r from-green-50 to-green-100 dark:from-green-900 dark:to-green-800 p-6 rounded-xl shadow-md">
<div class="text-sm opacity-70 mb-1">SWE-Verified-60</div>
<div class="text-3xl font-bold">56.7%</div>
<div class="text-lg text-green-600 dark:text-green-400 font-semibold">+16.7% improvement</div>
</div>

<div class="bg-gradient-to-r from-green-50 to-green-100 dark:from-green-900 dark:to-green-800 p-6 rounded-xl shadow-md">
<div class="text-sm opacity-70 mb-1">Polyglot</div>
<div class="text-3xl font-bold">30.5%</div>
<div class="text-lg text-green-600 dark:text-green-400 font-semibold">+10.2% improvement</div>
</div>

</div>

</div>

<div>

## ⚡ Speed

<div class="space-y-6 mt-8">

<div class="bg-gradient-to-r from-blue-50 to-blue-100 dark:from-blue-900 dark:to-blue-800 p-6 rounded-xl shadow-md">
<div class="text-sm opacity-70 mb-1">vs DGM</div>
<div class="text-4xl font-bold text-blue-600 dark:text-blue-400">2.38×</div>
<div class="text-lg">faster</div>
</div>

<div class="bg-gradient-to-r from-blue-50 to-blue-100 dark:from-blue-900 dark:to-blue-800 p-6 rounded-xl shadow-md">
<div class="text-sm opacity-70 mb-1">Polyglot speedup</div>
<div class="text-4xl font-bold text-blue-600 dark:text-blue-400">6.86×</div>
<div class="text-lg">faster</div>
</div>

</div>

</div>

</div>

---

# Result 3: vs. Human Designers

<div class="flex flex-col items-center justify-center h-full gap-12">

<div class="text-3xl font-bold text-center">
HGM on SWE-bench Verified
</div>

<div class="grid grid-cols-2 gap-16 text-center">

<div>
<div class="text-6xl font-bold text-blue-600">53.2%</div>
<div class="text-xl mt-2">Initial agent</div>
</div>

<div>
<div class="text-6xl font-bold text-green-600">61.4%</div>
<div class="text-xl mt-2">HGM discovered ⭐</div>
</div>

</div>

<div class="text-2xl text-center bg-yellow-50 dark:bg-yellow-900 p-6 rounded-lg max-w-3xl">
🏆 <strong>Top-10</strong> on leaderboard (all models)<br/>
<strong>#1</strong> GPT-5-mini based system
</div>

</div>

---

# Result 4: Human-Level Performance! 🎉

<div class="flex flex-col items-center justify-center h-full gap-8">

<div class="text-2xl text-center">
HGM optimized with <strong>GPT-5-mini</strong> → Evaluated with <strong>GPT-5</strong>
</div>

<div class="bg-green-50 dark:bg-green-900 p-8 rounded-lg text-center max-w-4xl">

| Agent | SWE-Lite Standard (%) |
|-------|------------------------|
| SWE-agent (Best human design) | 56.7 |
| <strong>HGM + GPT-5</strong> | <strong>57.0</strong> 🏆 |

</div>

<div class="grid grid-cols-3 gap-8 text-xl">

<div class="text-center">
✅ Transfers across<br/><strong>model sizes</strong>
</div>

<div class="text-center">
✅ Optimized on<br/><strong>different dataset</strong>
</div>

<div class="text-center">
✅ Not overfitting,<br/><strong>genuine ability</strong>
</div>

</div>

</div>

---

# Emergent Behaviors

<div class="flex items-center justify-center h-full">

<div class="grid grid-cols-2 gap-12 max-w-5xl">

<div class="bg-purple-50 dark:bg-purple-900 border-2 border-purple-400 dark:border-purple-600 rounded-xl p-10 shadow-lg">
<div class="text-6xl text-center mb-6">🔄</div>
<div class="text-2xl font-bold text-center mb-6">Self-Motivated Iteration</div>
<div class="text-lg text-center">
Agents perform <strong>multiple self-modifications</strong> per instruction
</div>
<div class="mt-6 text-center text-base bg-purple-100 dark:bg-purple-800 p-3 rounded italic">
→ Arbitrary levels of meta-improvement!
</div>
</div>

<div class="bg-orange-50 dark:bg-orange-900 border-2 border-orange-400 dark:border-orange-600 rounded-xl p-10 shadow-lg">
<div class="text-6xl text-center mb-6">🌀</div>
<div class="text-2xl font-bold text-center mb-6">Nested Diff Structures</div>
<div class="text-lg text-center">
Diff patches of diff patches<br/>
Multiple levels of changes
</div>
<div class="mt-6 text-center text-base bg-orange-100 dark:bg-orange-800 p-3 rounded italic">
"Mind-bending to understand manually"
</div>
</div>

</div>

</div>

---

# Key Contributions

<div class="grid grid-cols-2 gap-8 mt-6">

<div class="space-y-4">

<div class="bg-blue-50 dark:bg-blue-900 p-4 rounded-xl shadow-md border-l-4 border-blue-500">
<div class="text-2xl mb-1">🔍</div>
<div class="text-base"><strong>Identified</strong> Metaproductivity-Performance Mismatch</div>
</div>

<div class="bg-green-50 dark:bg-green-900 p-4 rounded-xl shadow-md border-l-4 border-green-500">
<div class="text-2xl mb-1">🌿</div>
<div class="text-base"><strong>Introduced</strong> Clade-Metaproductivity (CMP)</div>
</div>

<div class="bg-purple-50 dark:bg-purple-900 p-4 rounded-xl shadow-md border-l-4 border-purple-500">
<div class="text-2xl mb-1">🧮</div>
<div class="text-base"><strong>Proved</strong> Theorem 1 (CMP = Gödel Machine)</div>
</div>

</div>

<div class="space-y-4">

<div class="bg-orange-50 dark:bg-orange-900 p-4 rounded-xl shadow-md border-l-4 border-orange-500">
<div class="text-2xl mb-1">⚡</div>
<div class="text-base"><strong>Developed</strong> HGM Algorithm</div>
</div>

<div class="bg-yellow-50 dark:bg-yellow-900 p-4 rounded-xl shadow-md border-l-4 border-yellow-500">
<div class="text-2xl mb-1">📊</div>
<div class="text-base"><strong>Validated</strong> 2-3× better CMP estimation</div>
</div>

<div class="bg-red-50 dark:bg-red-900 p-4 rounded-xl shadow-md border-l-4 border-red-500">
<div class="text-2xl mb-1">🏆</div>
<div class="text-base"><strong>Achieved</strong> Human-level performance</div>
</div>

</div>

</div>

---

# HGM vs. Baselines

<div class="flex items-center justify-center h-full">

<div class="max-w-5xl">

| | SICA | DGM | <strong>HGM</strong> |
|---|:---:|:---:|:---:|
| <strong>Guidance</strong> | Performance | Performance | <strong>🌿 CMP</strong> |
| <strong>Expansion</strong> | Greedy | Probabilistic | <strong>Thompson Sampling</strong> |
| <strong>Decoupled?</strong> | ❌ | ❌ | <strong>✅</strong> |
| <strong>Theory</strong> | ❌ | ❌ | <strong>✅ Gödel Machine</strong> |
| <strong>Correlation</strong> | 0.44 | 0.29 | <strong>0.78</strong> |
| <strong>Speed</strong> | 1× | 1× | <strong>2-7×</strong> |

<div class="mt-8 text-2xl text-center bg-green-50 dark:bg-green-900 p-4 rounded-lg">
🎯 CMP-based approach → Better long-term self-improvement
</div>

</div>

</div>

---

# Key Takeaways

<div class="flex flex-col items-center justify-center h-full gap-6">

<div class="grid grid-cols-2 gap-6 max-w-5xl">

<div class="bg-gradient-to-br from-red-50 to-red-100 dark:from-red-900 dark:to-red-800 p-5 rounded-xl shadow-lg border-2 border-red-200 dark:border-red-700">
<div class="text-3xl mb-2">❌</div>
<div class="text-lg font-bold">Performance ≠ Metaproductivity</div>
</div>

<div class="bg-gradient-to-br from-green-50 to-green-100 dark:from-green-900 dark:to-green-800 p-5 rounded-xl shadow-lg border-2 border-green-200 dark:border-green-700">
<div class="text-3xl mb-2">✅</div>
<div class="text-lg font-bold">Lineages > Individuals</div>
</div>

<div class="bg-gradient-to-br from-blue-50 to-blue-100 dark:from-blue-900 dark:to-blue-800 p-5 rounded-xl shadow-lg border-2 border-blue-200 dark:border-blue-700">
<div class="text-3xl mb-2">🧮</div>
<div class="text-lg font-bold">CMP Oracle = Gödel Machine</div>
</div>

<div class="bg-gradient-to-br from-purple-50 to-purple-100 dark:from-purple-900 dark:to-purple-800 p-5 rounded-xl shadow-lg border-2 border-purple-200 dark:border-purple-700">
<div class="text-3xl mb-2">🏆</div>
<div class="text-lg font-bold">Human-Level Performance</div>
</div>

</div>

<div class="text-xl text-center bg-gradient-to-r from-yellow-50 to-orange-50 dark:from-yellow-900 dark:to-orange-900 p-6 rounded-xl shadow-xl max-w-4xl border-2 border-yellow-300 dark:border-yellow-700">
💡 <strong>Paradigm Shift:</strong> Focus on capacity to <strong>keep improving</strong>
</div>

</div>
