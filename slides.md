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
katex:
  macros:
    \argmax: "\\operatorname{arg\\,max}"
    \E: "\\mathbb{E}"
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

<v-click>
<div class="bg-red-50 dark:bg-red-900 p-6 rounded-lg">
<div class="text-xl font-bold mb-2">❌ Prior Approach</div>
<div>DGM & SICA use benchmark scores</div>
<div class="text-sm opacity-70 mt-2">Assume: High score → Better lineage</div>
</div>
</v-click>

<v-click>
<div class="bg-orange-50 dark:bg-orange-900 p-6 rounded-lg">
<div class="text-xl font-bold mb-2">⚠️ The Problem</div>
<div class="text-lg">High scores ≠ Good descendants</div>
</div>
</v-click>

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

# Visualizing the Mismatch

<div class="flex flex-col h-full justify-center gap-4">

<div class="grid grid-cols-2 gap-12">

<div class="text-center">
<div class="text-xl font-bold text-red-600 mb-4">❌ High Score, Poor Lineage</div>

```mermaid
graph TD
    A["Agent A<br/>Score: 0.85<br/>⭐"] --> B["Child 1<br/>0.80"]
    A --> C["Child 2<br/>0.78"]
    B --> D["Gen 3<br/>0.75"]
    B --> E["Gen 3<br/>0.72"]
    C --> F["Gen 3<br/>0.70"]
    C --> G["Gen 3<br/>0.68"]

    style A fill:#ffd700,stroke:#ff6b6b,stroke-width:4px
    style B fill:#ffecb3
    style C fill:#ffecb3
    style D fill:#ffcdd2
    style E fill:#ffcdd2
    style F fill:#ffcdd2
    style G fill:#ffcdd2
```

<div class="mt-4 bg-red-50 dark:bg-red-900 p-3 rounded-lg text-sm">
<div class="font-bold">Trend: ⬇️ Declining</div>
<div class="text-xs mt-1">CMP ≈ 0.70 (max descendant)</div>
</div>

</div>

<div class="text-center">
<div class="text-xl font-bold text-green-600 mb-4">✅ Lower Score, Great Lineage</div>

```mermaid
graph TD
    X["Agent X<br/>Score: 0.70<br/>🌱"] --> Y["Child 1<br/>0.78"]
    X --> Z["Child 2<br/>0.82"]
    Y --> P["Gen 3<br/>0.85"]
    Y --> Q["Gen 3<br/>0.88"]
    Z --> R["Gen 3<br/>0.92"]
    Z --> S["Gen 3<br/>0.95 🏆"]

    style X fill:#ffd700,stroke:#66bb6a,stroke-width:4px
    style Y fill:#c8e6c9
    style Z fill:#c8e6c9
    style P fill:#a5d6a7
    style Q fill:#81c784
    style R fill:#66bb6a
    style S fill:#4caf50
```

<div class="mt-4 bg-green-50 dark:bg-green-900 p-3 rounded-lg text-sm">
<div class="font-bold">Trend: ⬆️ Improving</div>
<div class="text-xs mt-1">CMP ≈ 0.95 (max descendant)</div>
</div>

</div>

</div>

<div class="text-center mt-2">
<div class="text-base bg-yellow-50 dark:bg-yellow-900 p-3 rounded-lg inline-block max-w-4xl">
💡 <strong>Greedy selection picks Agent A</strong> (0.85 > 0.70), but <strong>HGM picks Agent X</strong> (higher CMP)
</div>
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

<v-click>
<div class="flex items-center gap-4">
<div class="text-4xl">🔧</div>
<div><strong>Modify</strong> agent → create child</div>
</div>
</v-click>

<v-click>
<div class="flex items-center gap-4">
<div class="text-4xl">📊</div>
<div><strong>Evaluate</strong> agent on task</div>
</div>
</v-click>

<v-click>
<div class="flex items-center gap-4">
<div class="text-4xl">🎯</div>
<div><strong>Goal:</strong> Find best final agent</div>
</div>
</v-click>

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

<v-click>
<div>
✅ Modest ancestor can have great descendants
</div>
</v-click>

<v-click>
<div>
✅ More statistically robust
</div>
</v-click>

<v-click>
<div>
✅ Inspired by biology (Huxley)
</div>
</v-click>

<v-click>
<div>
✅ Captures long-term potential
</div>
</v-click>

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

<v-click>
<div class="flex flex-col items-center gap-4">
<div class="text-5xl">🎯</div>
<div class="text-xl">CMP ≡ Q-value</div>
</div>
</v-click>

<v-click>
<div class="flex flex-col items-center gap-4">
<div class="text-5xl">✓</div>
<div class="text-xl">Provably optimal</div>
</div>
</v-click>

<v-click>
<div class="flex flex-col items-center gap-4">
<div class="text-5xl">⚡</div>
<div class="text-xl">No proofs needed</div>
</div>
</v-click>

</div>

<v-click>
<div class="text-2xl text-center bg-green-50 dark:bg-green-900 p-6 rounded-lg max-w-3xl">
💡 <strong>Insight:</strong> Estimate CMP → Approximate Gödel Machine
</div>
</v-click>

</div>

---

# Deep Dive: What is a Gödel Machine?

<div class="flex flex-col items-center justify-center h-full gap-4">

<div class="text-xl text-center max-w-4xl">
<strong>Self-referential universal problem solver</strong> that makes provably optimal self-improvements
</div>

<div class="grid grid-cols-2 gap-8">

<div class="space-y-4">

<div class="bg-blue-50 dark:bg-blue-900 p-4 rounded-lg">
<div class="text-lg font-bold mb-2">🔍 Core Mechanism</div>
<div class="text-sm">
Runs a <strong>proof searcher</strong> looking for formal proofs that a code modification will increase expected utility
</div>
</div>

<div class="bg-green-50 dark:bg-green-900 p-4 rounded-lg">
<div class="text-lg font-bold mb-2">✅ When proof found</div>
<div class="text-sm">
The modification is <strong>executed</strong> and permanently alters the machine
</div>
</div>

</div>

<div class="space-y-4">

<div class="bg-purple-50 dark:bg-purple-900 p-4 rounded-lg">
<div class="text-lg font-bold mb-2">🎯 Guarantee</div>
<div class="text-sm">
<strong>Provably optimal</strong> with respect to given objective
</div>
</div>

<div class="bg-orange-50 dark:bg-orange-900 p-4 rounded-lg">
<div class="text-lg font-bold mb-2">⚠️ Challenge</div>
<div class="text-sm">
Finding proofs is <strong>computationally expensive</strong> and impractical
</div>
</div>

</div>

</div>

<div class="text-base text-center bg-yellow-50 dark:bg-yellow-900 p-3 rounded-lg max-w-2xl">
📚 <em>Schmidhuber (2003)</em>
</div>

</div>

---

# Assumption 1: Our Specialized Setting

<div class="flex flex-col h-full justify-center gap-4">

<div class="text-xl text-center mb-2">
How does our <strong>coding agent development</strong> setting differ from general Gödel Machine?
</div>

<div class="grid grid-cols-2 gap-6">

<div class="space-y-3">

<div class="bg-blue-50 dark:bg-blue-900 p-4 rounded-lg">
<div class="text-base font-bold mb-1">1️⃣ Final-only objective</div>
<div class="text-sm">
Only care about the <strong>final agent</strong>, not intermediate rewards
</div>
</div>

<div class="bg-green-50 dark:bg-green-900 p-4 rounded-lg">
<div class="text-base font-bold mb-1">2️⃣ Repeatable trials</div>
<div class="text-sm">
Can <strong>reset environment</strong> for each test; evaluations are independent
</div>
</div>

</div>

<div class="space-y-3">

<div class="bg-purple-50 dark:bg-purple-900 p-4 rounded-lg">
<div class="text-base font-bold mb-1">3️⃣ No proof cost</div>
<div class="text-sm">
Proofs don't consume budget (unlike original GM)
</div>
</div>

<div class="bg-orange-50 dark:bg-orange-900 p-4 rounded-lg">
<div class="text-base font-bold mb-1">4️⃣ Uniform costs</div>
<div class="text-sm">
Each self-modification costs <strong>exactly 1 budget unit</strong>
</div>
</div>

</div>

</div>

<div class="text-base text-center bg-yellow-50 dark:bg-yellow-900 p-3 rounded-lg">
💡 These simplifications make optimal policy <strong>tractable</strong> via CMP!
</div>

</div>

---

# Global Metaproductivity (GMP)

<div class="flex flex-col items-center justify-center h-full gap-6">

<div class="text-2xl text-center max-w-4xl">
How does evolving agent <em>a</em> affect the <strong>entire tree's</strong> final performance?
</div>

<div class="grid grid-cols-2 gap-12 items-center">

<div>

```mermaid
graph TD
    A0[a₀] --> A1[a₁]
    A0 --> A2[a₂]
    A1 --> A3[a₃]
    A1 --> A4[a₄]
    A2 --> A5[a₅]
    A2 --> A6[a₆]
    A4 --> A7[a₇]
    A4 --> A8[a₈]

    style A0 fill:#ffd700,stroke:#ff6600,stroke-width:3px
    style A1 fill:#ffe4b3,stroke:#ff6600,stroke-width:2px,stroke-dasharray: 5
    style A2 fill:#ffe4b3,stroke:#ff6600,stroke-width:2px,stroke-dasharray: 5
    style A3 fill:#fff3d9,stroke:#ff6600,stroke-width:1px,stroke-dasharray: 5
    style A4 fill:#fff3d9,stroke:#ff6600,stroke-width:1px,stroke-dasharray: 5
    style A5 fill:#fff3d9,stroke:#ff6600,stroke-width:1px,stroke-dasharray: 5
    style A6 fill:#fff3d9,stroke:#ff6600,stroke-width:1px,stroke-dasharray: 5
    style A7 fill:#fff9ec,stroke:#ff6600,stroke-width:1px,stroke-dasharray: 5
    style A8 fill:#fff9ec,stroke:#ff6600,stroke-width:1px,stroke-dasharray: 5
```

<div class="text-center text-sm mt-4">
<div class="font-bold text-orange-600">⚠️ Global Impact</div>
<div>Expanding a₀ affects ALL future nodes</div>
</div>

</div>

<div class="space-y-4">

<div class="bg-blue-50 dark:bg-blue-900 p-6 rounded-xl">
<div class="text-lg mb-3">

$$
\text{GMP}_\pi(\mathcal{T}, a) = \mathbb{E} \left[ U\left(\max_{a' \in \mathcal{T}_B} a'\right) \right]
$$

</div>
<div class="text-sm opacity-80">Expected utility of best agent in ENTIRE final tree</div>
</div>

<div class="grid grid-cols-3 gap-3 text-center text-sm">
<v-click>
<div class="bg-purple-100 dark:bg-purple-900 p-3 rounded">
<div class="text-2xl mb-1">🌳</div>
<div class="font-semibold">Full tree</div>
</div>
</v-click>
<v-click>
<div class="bg-purple-100 dark:bg-purple-900 p-3 rounded">
<div class="text-2xl mb-1">🎲</div>
<div class="font-semibold">Rollout</div>
</div>
</v-click>
<v-click>
<div class="bg-purple-100 dark:bg-purple-900 p-3 rounded">
<div class="text-2xl mb-1">🏆</div>
<div class="font-semibold">Best</div>
</div>
</v-click>
</div>

<div class="bg-purple-50 dark:bg-purple-900 p-4 rounded-lg border-2 border-purple-400">
<div class="font-bold mb-2">⚡ Key insight:</div>
<div class="text-sm">GMP = Q-value in RL</div>
<div class="text-xs mt-2 opacity-80">(state = tree, action = expand agent)</div>
</div>

</div>

</div>

</div>

---

# From GMP to CMP: Why Clades?

<div class="flex items-center justify-center h-full">

<div class="grid grid-cols-2 gap-12">

<div class="space-y-6">

<v-click>
<div class="bg-red-50 dark:bg-red-900 p-6 rounded-lg border-2 border-red-400">
<div class="text-xl font-bold mb-3">❌ Problem with GMP</div>
<div class="text-base space-y-2">
<div>• Too global - considers entire tree</div>
<div>• Self-modifications can affect ancestors</div>
<div>• Hard to conceptualize</div>
<div>• Difficult to estimate</div>
</div>
</div>
</v-click>

<v-click>
<div class="bg-blue-50 dark:blue-green-900 p-6 rounded-lg border-2 border-blue-400">
<div class="text-xl font-bold mb-3">🧮 Gödel Machine Focus</div>
<div class="text-base">
Decides whether to <strong>accept or reject</strong> based on provable potential of <strong>subsequent</strong> self-improvements
</div>
</div>
</v-click>

</div>

<div class="space-y-6">

<v-click>
<div class="bg-green-50 dark:bg-green-900 p-6 rounded-lg border-2 border-green-400">
<div class="text-xl font-bold mb-3">✅ Solution: CMP</div>
<div class="text-base space-y-2">
<div>• Localized to <strong>subtree</strong> (clade)</div>
<div>• Only descendants matter</div>
<div>• Conceptually clear</div>
<div>• Practically estimable</div>
</div>
</div>
</v-click>

<v-click>
<div class="bg-yellow-50 dark:bg-yellow-900 p-6 rounded-lg border-2 border-yellow-400">
<div class="text-xl font-bold mb-3">🌿 Biological Inspiration</div>
<div class="text-base">
<strong>Clade</strong> (Huxley, 1957): lineages of common ancestry
</div>
</div>
</v-click>

</div>

</div>

</div>

---

# GMP vs CMP: Visual Comparison

<div class="flex flex-col h-full justify-center gap-4">

<div class="grid grid-cols-2 gap-10">

<div class="text-center">
<div class="text-xl font-bold text-orange-600 mb-3">GMP: Global Scope</div>

```mermaid
graph TD
    A0[a₀] --> A1[a₁]
    A0 --> A2[a₂]
    A1 --> A3[a₃]
    A1 --> A4[a₄]
    A2 --> A5[a₅]
    A2 --> A6[a₆]

    style A0 fill:#ff9800,stroke:#ff6600,stroke-width:3px
    style A1 fill:#ffcc80,stroke:#ff6600,stroke-width:2px
    style A2 fill:#ffcc80,stroke:#ff6600,stroke-width:2px
    style A3 fill:#ffe0b2,stroke:#ff6600,stroke-width:1px
    style A4 fill:#ffe0b2,stroke:#ff6600,stroke-width:1px
    style A5 fill:#ffe0b2,stroke:#ff6600,stroke-width:1px
    style A6 fill:#ffe0b2,stroke:#ff6600,stroke-width:1px
```

<div class="bg-orange-50 dark:bg-orange-900 p-3 rounded-lg mt-3 text-sm">
<div class="font-bold mb-1">Considers ALL nodes</div>
<div class="text-xs">

Max over $\mathcal{T}_B$ (entire tree)

</div>
</div>

</div>

<div class="text-center">
<div class="text-xl font-bold text-green-600 mb-3">CMP: Clade Scope</div>

```mermaid
graph TD
    A0[a₀] -.-> A1[a₁]
    A0 -.-> A2[a₂]
    A1 --> A3[a₃]
    A1 --> A4[a₄]
    A2[a₂]
    A2 -.-> A5[a₅]
    A2 -.-> A6[a₆]

    style A0 stroke:#999,stroke-width:1px,stroke-dasharray: 5
    style A1 fill:#4caf50,stroke:#2e7d32,stroke-width:3px
    style A2 stroke:#999,stroke-width:1px,stroke-dasharray: 5
    style A3 fill:#81c784,stroke:#2e7d32,stroke-width:2px
    style A4 fill:#81c784,stroke:#2e7d32,stroke-width:2px
    style A5 stroke:#999,stroke-width:1px,stroke-dasharray: 5
    style A6 stroke:#999,stroke-width:1px,stroke-dasharray: 5
```

<div class="bg-green-50 dark:bg-green-900 p-3 rounded-lg mt-3 text-sm">
<div class="font-bold mb-1">Only descendants of a₁</div>
<div class="text-xs">

Max over $C(\mathcal{T}_B, a_1)$ (clade of a₁)

</div>
</div>

</div>

</div>

<div class="text-center">
<div class="text-base bg-purple-50 dark:bg-purple-900 p-3 rounded-lg inline-block max-w-4xl">
💡 <strong>CMP is localized</strong>: Only the <strong>subtree</strong> rooted at an agent matters
</div>
</div>

</div>

---

# The Mathematics of CMP

<div class="flex flex-col items-center justify-center h-full gap-4">

<div class="text-xl text-center">
Clade-Metaproductivity: Expected utility of best agent in <strong>clade</strong>
</div>

<div class="bg-blue-50 dark:bg-blue-900 p-6 rounded-xl shadow-lg max-w-5xl">
<div class="text-center text-lg mb-4">

$$
\begin{aligned}
\text{CMP}_\pi(\mathcal{T}, a) &= \mathbb{E}_{\mathcal{T}_B \sim p_\pi(\cdot | \mathcal{T}, a)} \left[ U\left(\operatorname*{arg\,max}_{a' \in C(\mathcal{T}_B, a)} \text{Score}_\pi(a')\right) \right] \\
&= \mathbb{E}_{\mathcal{T}_B \sim p_\pi(\cdot | \mathcal{T}, a)} \left[ \max_{a' \in C(\mathcal{T}_B, a)} U(a') \right] \quad \text{(if Score = U)}
\end{aligned}
$$

</div>
<div class="text-center text-sm opacity-80">

where $C(\mathcal{T}_B, a)$ is the clade (subtree rooted at $a$) in final tree $\mathcal{T}_B$

</div>
</div>

<div class="grid grid-cols-3 gap-4">

<div class="bg-green-50 dark:bg-green-900 p-4 rounded-lg">
<div class="text-base font-bold mb-2">📊 Estimator</div>
<div class="text-sm">

$$
\widehat{\text{CMP}}(a) = \frac{n_{\text{success}}^C(a)}{n_{\text{success}}^C(a) + n_{\text{failure}}^C(a)}
$$

</div>
</div>

<div class="bg-purple-50 dark:bg-purple-900 p-4 rounded-lg">
<div class="text-base font-bold mb-2">🔢 Where</div>
<div class="text-xs">

$$
n^C_{\text{success}}(a) = \sum_{a' \in C(a)} n_{\text{success}}(a')
$$

</div>
</div>

<div class="bg-orange-50 dark:bg-orange-900 p-4 rounded-lg">
<div class="text-base font-bold mb-2">⚖️ Weighted</div>
<div class="text-sm">
More evaluated agents get higher weight
</div>
</div>

</div>

</div>

---

# CMP Estimator: Step-by-Step

<div class="flex flex-col h-full justify-center gap-3">

<div class="text-xl text-center">
How to estimate CMP: Aggregate test results across the <strong>clade</strong>
</div>

<div class="grid grid-cols-2 gap-8 items-center">

<div>

```mermaid
graph TD
    A1["a₁<br/>(7✓, 3✗)"] --> A2["a₂<br/>(5✓, 2✗)"]
    A1 --> A3["a₃<br/>(4✓, 6✗)"]
    A2 --> A4["a₄<br/>(8✓, 1✗)"]
    A2 --> A5["a₅<br/>(6✓, 4✗)"]

    style A1 fill:#4caf50,stroke:#2e7d32,stroke-width:3px
    style A2 fill:#81c784
    style A3 fill:#ffcc80
    style A4 fill:#66bb6a
    style A5 fill:#a5d6a7
```

<div class="text-center text-xs mt-2 opacity-70">
Tree showing test results (successes ✓, failures ✗)
</div>

</div>

<div class="space-y-3">

<v-click>
<div class="bg-blue-50 dark:bg-blue-900 p-3 rounded-lg">
<div class="font-bold text-base mb-1">Step 1: Collect in Clade</div>
<div class="text-xs">

Gather all results from $a_1$ and descendants:

$a_1$: 7✓, 3✗ | $a_2$: 5✓, 2✗ | $a_3$: 4✓, 6✗ | $a_4$: 8✓, 1✗ | $a_5$: 6✓, 4✗

</div>
</div>
</v-click>

<v-click>
<div class="bg-green-50 dark:bg-green-900 p-3 rounded-lg">
<div class="font-bold text-base mb-1">Step 2: Sum Totals</div>
<div class="text-xs">

$$
\begin{aligned}
n^C_{\text{success}}(a_1) &= 7 + 5 + 4 + 8 + 6 = 30 \\
n^C_{\text{failure}}(a_1) &= 3 + 2 + 6 + 1 + 4 = 16
\end{aligned}
$$

</div>
</div>
</v-click>

<v-click>
<div class="bg-purple-50 dark:bg-purple-900 p-3 rounded-lg">
<div class="font-bold text-base mb-1">Step 3: Compute CMP</div>
<div class="text-xs">

$$
\widehat{\text{CMP}}(a_1) = \frac{30}{30 + 16} = \frac{30}{46} ≈ 0.652
$$

</div>
</div>
</v-click>

</div>

</div>

<div class="text-center">
<div class="text-sm bg-yellow-50 dark:bg-yellow-900 p-2 rounded-lg inline-block">
💡 CMP uses <strong>entire lineage</strong> → more robust than single-agent score
</div>
</div>

</div>

---

# Theorem 1: The Main Result

<div class="flex flex-col items-center justify-center h-full gap-4">

<div class="bg-gradient-to-r from-blue-100 to-purple-100 dark:from-blue-900 dark:to-purple-900 p-6 rounded-xl shadow-2xl max-w-5xl border-4 border-blue-400 dark:border-blue-600">
<div class="text-center text-2xl font-bold mb-3">
Theorem 1
</div>
<div class="text-center text-lg">
Under <strong>Assumption 1</strong>, access to the <strong>CMP oracle</strong> is <em>sufficient</em> to implement the <strong>Gödel Machine</strong>.
</div>
</div>

<div class="grid grid-cols-3 gap-4 max-w-5xl">

<v-click>
<div class="bg-blue-50 dark:bg-blue-900 p-4 rounded-lg">
<div class="text-lg font-bold mb-2">🔑 Key Equality</div>
<div class="text-base">

$$
\text{CMP}_\pi(\mathcal{T}, a) = Q_\pi(\mathcal{T}, a)
$$

</div>
<div class="text-xs mt-1 opacity-80">
CMP is exactly the Q-value in the Gödel POMDP!
</div>
</div>
</v-click>

<v-click>
<div class="bg-green-50 dark:bg-green-900 p-4 rounded-lg">
<div class="text-lg font-bold mb-2">🎯 POMDP Setup</div>
<div class="text-sm space-y-1">
<div>• <strong>State:</strong> Tree + parent + child</div>
<div>• <strong>Action:</strong> Accept or reject</div>
<div>• <strong>Observe:</strong> Only parent, child, budget</div>
</div>
</div>
</v-click>

<v-click>
<div class="bg-purple-50 dark:bg-purple-900 p-4 rounded-lg">
<div class="text-lg font-bold mb-2">✓ Optimality</div>
<div class="text-sm">
Selecting max CMP = selecting max Q-value
= <strong>Bellman optimal</strong>
</div>
</div>
</v-click>

</div>

<div class="text-base text-center bg-yellow-50 dark:bg-yellow-900 p-3 rounded-lg max-w-4xl">
💡 <strong>Implication:</strong> No need for expensive proofs! Just estimate CMP well.
</div>

</div>

---

# Proof Sketch: Why CMP = Q-value

<div class="flex flex-col h-full justify-center gap-6">

<div class="grid grid-cols-2 gap-8">

<div class="space-y-5">

<div class="bg-blue-50 dark:bg-blue-900 p-5 rounded-lg">
<div class="text-lg font-bold mb-2">1️⃣ Gödel Machine Policy</div>
<div class="text-base">

At each step: observe $(a_{\text{parent}}, a_{\text{child}}, b)$ and choose to accept or reject child

</div>
</div>

<div class="bg-green-50 dark:bg-green-900 p-5 rounded-lg">
<div class="text-lg font-bold mb-2">2️⃣ Final Selection</div>
<div class="text-base">

$\text{Score}_\pi$ is indicator function: picks either final parent <em>or</em> final child

</div>
</div>

<div class="bg-purple-50 dark:bg-purple-900 p-5 rounded-lg">
<div class="text-lg font-bold mb-2">3️⃣ Clade Structure</div>
<div class="text-base">
Only descendants reachable; ancestors above clade are <strong>not accessible</strong>
</div>
</div>

</div>

<div class="space-y-5">

<div class="bg-orange-50 dark:bg-orange-900 p-5 rounded-lg">
<div class="text-lg font-bold mb-2">4️⃣ Expected Return</div>
<div class="text-base">

$$
\begin{aligned}
&\text{CMP}_\pi((\mathcal{T}, a_p, a_c, b), a) \\
&= \mathbb{E} [ U(\operatorname*{arg\,max}_{a' \in C} \text{Score}(a')) ] \\
&= \mathbb{E} [ U(\operatorname*{arg\,max}_{a' \in \{a_p, a_c\}} \text{Score}(a')) ] \\
&= Q_\pi((\mathcal{T}, a_p, a_c, b), a)
\end{aligned}
$$

</div>
</div>

<div class="bg-yellow-50 dark:bg-yellow-900 p-5 rounded-lg">
<div class="text-lg font-bold mb-2">✅ Conclusion</div>
<div class="text-base">
CMP oracle knows the true Q-values → can make optimal accept/reject decisions
</div>
</div>

</div>

</div>

<div class="text-base text-center opacity-70 mt-2">
Full proof in Appendix A of paper
</div>

</div>

---

# POMDP: The Gödel Machine's Decision Process

<div class="flex flex-col h-full justify-center gap-3">

<div class="text-xl text-center">
Gödel Machine operates as a POMDP: Partial observability, Accept/Reject decisions
</div>

<div class="grid grid-cols-3 gap-6">

<div class="text-center">
<div class="text-lg font-bold text-blue-600 mb-3">State</div>

```mermaid
graph TD
    T[Tree 𝒯] --> AP[a_parent]
    T --> AC[a_child]
    T --> B[Budget b]

    style T fill:#e3f2fd
    style AP fill:#ffd54f,stroke:#f57f17,stroke-width:3px
    style AC fill:#ffeb3b,stroke:#f57f17,stroke-width:2px
    style B fill:#fff9c4
```

<div class="bg-blue-50 dark:bg-blue-900 p-2 rounded mt-2 text-xs">
Full state includes entire tree + special nodes
</div>

</div>

<div class="text-center">
<div class="text-lg font-bold text-green-600 mb-3">Observation</div>

```mermaid
graph TD
    O["👁️ Observe"] --> AP[a_parent]
    O --> AC[a_child]
    O --> B[Budget b]

    style O fill:#c8e6c9
    style AP fill:#ffd54f,stroke:#f57f17,stroke-width:3px
    style AC fill:#ffeb3b,stroke:#f57f17,stroke-width:2px
    style B fill:#fff9c4
```

<div class="bg-green-50 dark:bg-green-900 p-2 rounded mt-2 text-xs">
Only see parent, child, budget (not full tree!)
</div>

</div>

<div class="text-center">
<div class="text-lg font-bold text-purple-600 mb-3">Action</div>

```mermaid
graph LR
    D{Decision} -->|Accept| C[Move to<br/>a_child]
    D -->|Reject| P[Stay at<br/>a_parent]

    style D fill:#e1bee7
    style C fill:#81c784
    style P fill:#ef9a9a
```

<div class="bg-purple-50 dark:bg-purple-900 p-2 rounded mt-2 text-xs">
Binary choice: Accept or Reject
</div>

</div>

</div>

<div class="grid grid-cols-2 gap-6">

<div class="bg-orange-50 dark:bg-orange-900 p-3 rounded-lg">
<div class="font-bold text-base mb-1">🔄 Transition</div>
<div class="text-xs">
1. Generate child via self-modification
2. New parent = accepted agent
3. Budget decreases by 1
</div>
</div>

<div class="bg-yellow-50 dark:bg-yellow-900 p-3 rounded-lg">
<div class="font-bold text-base mb-1">🎯 Reward</div>
<div class="text-xs">

Final reward = $U(\text{Score}_\pi)$ picks best from final (parent, child) pair

</div>
</div>

</div>

</div>

---

# Why CMP = Q-value: Visual Proof

<div class="flex flex-col h-full justify-center gap-3">

<div class="grid grid-cols-2 gap-8 items-center">

<div>

```mermaid
graph TD
    GP["a_parent<br/>(Current)"] -.-> GC["a_child<br/>(Generated)"]
    GC --> D1[Descendant 1]
    GC --> D2[Descendant 2]
    D1 --> D3[Gen 3]
    D2 --> D4[Gen 3]

    style GP fill:#ffd54f,stroke:#f57f17,stroke-width:4px
    style GC fill:#ffeb3b,stroke:#f57f17,stroke-width:4px
    style D1 fill:#c8e6c9,stroke:#2e7d32,stroke-width:2px
    style D2 fill:#c8e6c9,stroke:#2e7d32,stroke-width:2px
    style D3 fill:#e8f5e9
    style D4 fill:#e8f5e9
```

<div class="text-center text-xs mt-2">
<div class="font-bold">Clade of a_child</div>
<div class="opacity-70">Only these nodes are reachable!</div>
</div>

</div>

<div class="space-y-2">

<v-click>
<div class="bg-blue-50 dark:bg-blue-900 p-3 rounded-lg">
<div class="font-bold text-base mb-1">1️⃣ Final Selection Constraint</div>
<div class="text-xs">

$\text{Score}_\pi$ is an <strong>indicator function</strong>: Picks either $a_{\text{parent}}$ OR $a_{\text{child}}$. All other agents get score 0

</div>
</div>
</v-click>

<v-click>
<div class="bg-green-50 dark:bg-green-900 p-3 rounded-lg">
<div class="font-bold text-base mb-1">2️⃣ Clade = Reachable Set</div>
<div class="text-xs">

If we accept $a_{\text{child}}$, only its <strong>descendants</strong> are reachable. $C(\mathcal{T}_B, a_{\text{child}})$ = all nodes below $a_{\text{child}}$

</div>
</div>
</v-click>

<v-click>
<div class="bg-purple-50 dark:bg-purple-900 p-3 rounded-lg">
<div class="font-bold text-base mb-1">3️⃣ The Equality</div>
<div class="text-xs">

$$
\text{CMP} = \mathbb{E}[\max_{a' \in C} U(a')] = \mathbb{E}[\max_{a' \in \{a_p, a_c\}} U(a')] = Q_\pi
$$

</div>
</div>
</v-click>

</div>

</div>

<div class="text-center mt-1">
<div class="text-sm bg-yellow-50 dark:bg-yellow-900 p-2 rounded-lg inline-block max-w-4xl">
💡 <strong>Key insight:</strong> CMP measures exactly what Gödel Machine needs!
</div>
</div>

</div>

---

# Thompson Sampling for Exploration-Exploitation

<div class="flex flex-col items-center justify-center h-full gap-8">

<div class="text-2xl text-center max-w-4xl">
How to select which agent to expand when we only have <strong>estimates</strong> of CMP?
</div>

<div class="grid grid-cols-2 gap-12">

<v-click>
<div class="bg-blue-50 dark:bg-blue-900 p-6 rounded-lg">
<div class="text-xl font-bold mb-4">🎲 Thompson Sampling</div>
<div class="text-base space-y-3">
<div>1. Model CMP as Beta distribution:</div>
<div class="text-center text-lg">

$\text{Beta}(\tau(1 + n_s^C), \tau(1 + n_f^C))$

</div>
<div>2. Sample from each posterior</div>
<div>3. Select agent with highest sample</div>
</div>
</div>
</v-click>

<v-click>
<div class="bg-green-50 dark:bg-green-900 p-6 rounded-lg">
<div class="text-xl font-bold mb-4">⚖️ Exploration Scheduler</div>
<div class="text-base space-y-3">
<div>

Temperature parameter $\tau(t)$ increases over time:

</div>
<div>

• <strong>Early:</strong> Low $\tau$ → more exploration

</div>
<div>

• <strong>Late:</strong> High $\tau$ → more exploitation

</div>
<div>Automatically balances discovery vs refinement</div>
</div>
</div>
</v-click>

</div>

<div class="text-lg text-center bg-purple-50 dark:bg-purple-900 p-4 rounded-lg max-w-4xl">
🎯 Unlike greedy baselines, TS <strong>probabilistically</strong> explores promising clades
</div>

</div>

---

# Temperature Schedule: τ(t) Over Time

<div class="flex flex-col h-full justify-center gap-4">

<div class="text-xl text-center">

Temperature $\tau(t) = \frac{B}{b}$ increases over time: more <strong>exploitation</strong> as budget runs out

</div>

<div class="grid grid-cols-2 gap-8">

<div>

```mermaid
graph LR
    T0["t=0<br/>τ≈1<br/>🔍"] --> T1["t=B/2<br/>τ≈2<br/>⚖️"]
    T1 --> T2["t=B<br/>τ→∞<br/>🎯"]

    style T0 fill:#e3f2fd,stroke:#1976d2,stroke-width:3px
    style T1 fill:#fff9c4,stroke:#f57f17,stroke-width:3px
    style T2 fill:#ffccbc,stroke:#d84315,stroke-width:3px
```

<div class="mt-4 space-y-3">

<v-click>
<div class="bg-blue-50 dark:bg-blue-900 p-3 rounded-lg border-l-4 border-blue-500">
<div class="font-bold text-sm mb-1">🔍 Early (low τ)</div>
<div class="text-xs">Wide Beta distributions → more random sampling → <strong>exploration</strong></div>
</div>
</v-click>

<v-click>
<div class="bg-yellow-50 dark:bg-yellow-900 p-3 rounded-lg border-l-4 border-yellow-600">
<div class="font-bold text-sm mb-1">⚖️ Middle (medium τ)</div>
<div class="text-xs">Moderate distributions → balanced → <strong>mixed strategy</strong></div>
</div>
</v-click>

<v-click>
<div class="bg-orange-50 dark:bg-orange-900 p-3 rounded-lg border-l-4 border-orange-600">
<div class="font-bold text-sm mb-1">🎯 Late (high τ)</div>
<div class="text-xs">Narrow distributions → pick best → <strong>exploitation</strong></div>
</div>
</v-click>

</div>

</div>

<div class="space-y-3">

<div class="bg-gradient-to-r from-blue-50 to-purple-50 dark:from-blue-900 dark:to-purple-900 p-4 rounded-xl">
<div class="font-bold text-base mb-3 text-center">Beta Distributions Evolution</div>

<div class="grid grid-cols-3 gap-3 text-center text-xs">

<div class="bg-blue-100 dark:bg-blue-800 p-2 rounded">
<div class="font-bold mb-1">Low τ = 1</div>
<div class="text-xs">

$\text{Beta}(1+7, 1+3)$

</div>
<div class="mt-1 text-xs">Wide curve 📊</div>
</div>

<div class="bg-yellow-100 dark:bg-yellow-800 p-2 rounded">
<div class="font-bold mb-1">Med τ = 5</div>
<div class="text-xs">

$\text{Beta}(5+35, 5+15)$

</div>
<div class="mt-1 text-xs">Medium 📈</div>
</div>

<div class="bg-orange-100 dark:bg-orange-800 p-2 rounded">
<div class="font-bold mb-1">High τ = 20</div>
<div class="text-xs">

$\text{Beta}(20+140, 20+60)$

</div>
<div class="mt-1 text-xs">Peaked 📉</div>
</div>

</div>

</div>

<div class="bg-purple-50 dark:bg-purple-900 p-3 rounded-lg border-2 border-purple-400">
<div class="font-bold text-base mb-2">📊 Effect on Selection</div>
<div class="text-xs space-y-1">
<div>• <strong>Low τ:</strong> Sample values spread out → try different agents</div>
<div>• <strong>High τ:</strong> Sample values concentrated → pick highest CMP</div>
</div>
</div>

</div>

</div>

<div class="text-center">
<div class="text-sm bg-green-50 dark:bg-green-900 p-2 rounded-lg inline-block max-w-4xl">
✨ <strong>Automatic annealing:</strong> HGM shifts from exploration to exploitation naturally
</div>
</div>

</div>

---

# Connection to Infinite-Armed Bandits

<div class="flex flex-col h-full justify-center gap-8">

<div class="text-2xl text-center">
When to <strong>expand</strong> (create new agent) vs <strong>evaluate</strong> (test existing)?
</div>

<div class="grid grid-cols-2 gap-12 items-center">

<div>

```mermaid
graph LR
    A[Known Arms<br/>Existing Agents] -->|Evaluate| B[Reduce<br/>Uncertainty]
    C[New Arms<br/>Expand Tree] -->|Discover| D[New<br/>Potential]

    style A fill:#e3f2fd
    style C fill:#f3e5f5
    style B fill:#e8f5e9
    style D fill:#fff9c4
```

</div>

<div class="space-y-6">

<v-click>
<div class="bg-orange-50 dark:bg-orange-900 p-5 rounded-lg">
<div class="text-xl font-bold mb-3">📊 UCB-Air Strategy</div>
<div class="text-base">

Expand when:

$$N_t^\alpha \geq |\mathcal{T}_t|$$

</div>
<div class="text-sm mt-2 opacity-80">
Number of evaluations vs number of agents
</div>
</div>
</v-click>

<v-click>
<div class="bg-purple-50 dark:bg-purple-900 p-5 rounded-lg">
<div class="text-xl font-bold mb-3">⚡ Decoupled Policy</div>
<div class="text-base space-y-2">
<div>• DGM/SICA: Always expand then evaluate</div>
<div>• <strong>HGM:</strong> Adaptive choice each step</div>
</div>
</div>
</v-click>

</div>

</div>

</div>

---

# HGM: How to Estimate CMP?

<div class="flex flex-col items-center justify-center h-full gap-10">

<div class="text-2xl text-center max-w-3xl">
Aggregate success across <strong>entire clade</strong> (lineage)
</div>

<div class="bg-blue-50 dark:bg-blue-900 p-8 rounded-xl shadow-lg">
<div class="text-3xl text-center">

$$
\widehat{\text{CMP}}(a) = \frac{\text{successes in clade}}{\text{total tests in clade}}
$$

</div>
</div>

<div class="grid grid-cols-3 gap-10 mt-4">

<v-click>
<div class="text-center">
<div class="text-5xl mb-3">📊</div>
<div class="text-lg font-semibold">Clade-level</div>
<div class="text-sm opacity-70">aggregation</div>
</div>
</v-click>

<v-click>
<div class="text-center">
<div class="text-5xl mb-3">⚖️</div>
<div class="text-lg font-semibold">Weighted by</div>
<div class="text-sm opacity-70">evaluations</div>
</div>
</v-click>

<v-click>
<div class="text-center">
<div class="text-5xl mb-3">🎲</div>
<div class="text-lg font-semibold">Thompson</div>
<div class="text-sm opacity-70">Sampling</div>
</div>
</v-click>

</div>

</div>

---

# HGM Algorithm: Complete Walkthrough

<div class="flex flex-col h-full justify-center gap-2">

<div class="text-lg text-center mb-1">
Step-by-step execution of one HGM iteration
</div>

<div class="grid grid-cols-2 gap-6">

<div class="space-y-2">

<v-click>
<div class="bg-blue-50 dark:bg-blue-900 p-3 rounded-lg border-l-4 border-blue-500">
<div class="font-bold text-sm mb-1">Step 1: Compute CMP Estimates</div>
<div class="text-xs">

For each agent $a$ in tree:

$$
\widehat{\text{CMP}}(a) = \frac{n^C_{\text{success}}(a)}{n^C_{\text{success}}(a) + n^C_{\text{failure}}(a)}
$$

</div>
</div>
</v-click>

<v-click>
<div class="bg-green-50 dark:bg-green-900 p-3 rounded-lg border-l-4 border-green-500">
<div class="font-bold text-sm mb-1">Step 2: Thompson Sample</div>
<div class="text-xs">

For each $a$, sample:

$$
S_C(a) \sim \text{Beta}(\tau(1 + n^C_s), \tau(1 + n^C_f))
$$

Select $a^* = \arg\max_a S_C(a)$

</div>
</div>
</v-click>

<v-click>
<div class="bg-purple-50 dark:bg-purple-900 p-3 rounded-lg border-l-4 border-purple-500">
<div class="font-bold text-sm mb-1">Step 3: Decide Action</div>
<div class="text-xs">

If $N_t^\alpha \geq |\mathcal{T}_t|$: <strong>Expand</strong> (create child)

<br/>

Otherwise: <strong>Evaluate</strong> (test agent)

</div>
</div>
</v-click>

</div>

<div class="space-y-2">

<v-click>
<div class="bg-orange-50 dark:bg-orange-900 p-3 rounded-lg border-l-4 border-orange-500">
<div class="font-bold text-sm mb-1">Step 4a: If Expanding</div>
<div class="text-xs">

1. Agent $a^*$ self-modifies → creates child $c$

<br/>

2. Add $c$ to tree $\mathcal{T}$

<br/>

3. Initialize counters for $c$

</div>
</div>
</v-click>

<v-click>
<div class="bg-yellow-50 dark:bg-yellow-900 p-3 rounded-lg border-l-4 border-yellow-600">
<div class="font-bold text-sm mb-1">Step 4b: If Evaluating</div>
<div class="text-xs">

1. Sample agent to test (by individual stats)

<br/>

2. Run on one task → get result

<br/>

3. Update $n_{\text{success}}$ or $n_{\text{failure}}$

<br/>

4. Bubble up to ancestors (update $n^C$)

</div>
</div>
</v-click>

<v-click>
<div class="bg-red-50 dark:bg-red-900 p-3 rounded-lg border-l-4 border-red-500">
<div class="font-bold text-sm mb-1">Step 5: Repeat</div>
<div class="text-xs">

Continue until budget exhausted. Return best-belief agent:

$$
\arg\max_a I_\epsilon(1 + n_s, 1 + n_f)
$$

</div>
</div>
</v-click>

</div>

</div>

</div>

---

# HGM: Three Adaptive Policies

<div class="grid grid-cols-3 gap-8 mt-10">

<v-click>
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
</v-click>

<v-click>
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
</v-click>

<v-click>
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
</v-click>

</div>

<v-click>
<div class="mt-10 text-center text-xl bg-yellow-50 dark:bg-yellow-900 p-5 rounded-xl shadow-md max-w-4xl mx-auto">
🚀 <strong>Key Innovation:</strong> Decoupled expansion from evaluation!
</div>
</v-click>

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

<v-click>
<div>
<div class="text-5xl mb-4">📊</div>
<div class="text-xl font-bold mb-3">Benchmarks</div>
<div class="text-base">
SWE-bench Verified (500)<br/>
SWE-bench Lite (300)<br/>
Polyglot
</div>
</div>
</v-click>

<v-click>
<div>
<div class="text-5xl mb-4">🤖</div>
<div class="text-xl font-bold mb-3">Baselines</div>
<div class="text-base">
DGM<br/>
SICA<br/>
SWE-agent
</div>
</div>
</v-click>

<v-click>
<div>
<div class="text-5xl mb-4">🧠</div>
<div class="text-xl font-bold mb-3">Models</div>
<div class="text-base">
GPT-5 / GPT-5-mini<br/>
Qwen3-Coder
</div>
</div>
</v-click>

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

<v-click>
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
</v-click>

<v-click>
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
</v-click>

</div>

</div>

---

# Key Contributions

<div class="grid grid-cols-2 gap-8 mt-6">

<div class="space-y-4">

<v-click>
<div class="bg-blue-50 dark:bg-blue-900 p-4 rounded-xl shadow-md border-l-4 border-blue-500">
<div class="text-2xl mb-1">🔍</div>
<div class="text-base"><strong>Identified</strong> Metaproductivity-Performance Mismatch</div>
</div>
</v-click>

<v-click>
<div class="bg-green-50 dark:bg-green-900 p-4 rounded-xl shadow-md border-l-4 border-green-500">
<div class="text-2xl mb-1">🌿</div>
<div class="text-base"><strong>Introduced</strong> Clade-Metaproductivity (CMP)</div>
</div>
</v-click>

<v-click>
<div class="bg-purple-50 dark:bg-purple-900 p-4 rounded-xl shadow-md border-l-4 border-purple-500">
<div class="text-2xl mb-1">🧮</div>
<div class="text-base"><strong>Proved</strong> Theorem 1 (CMP = Gödel Machine)</div>
</div>
</v-click>

</div>

<div class="space-y-4">

<v-click>
<div class="bg-orange-50 dark:bg-orange-900 p-4 rounded-xl shadow-md border-l-4 border-orange-500">
<div class="text-2xl mb-1">⚡</div>
<div class="text-base"><strong>Developed</strong> HGM Algorithm</div>
</div>
</v-click>

<v-click>
<div class="bg-yellow-50 dark:bg-yellow-900 p-4 rounded-xl shadow-md border-l-4 border-yellow-500">
<div class="text-2xl mb-1">📊</div>
<div class="text-base"><strong>Validated</strong> 2-3× better CMP estimation</div>
</div>
</v-click>

<v-click>
<div class="bg-red-50 dark:bg-red-900 p-4 rounded-xl shadow-md border-l-4 border-red-500">
<div class="text-2xl mb-1">🏆</div>
<div class="text-base"><strong>Achieved</strong> Human-level performance</div>
</div>
</v-click>

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

<v-click>
<div class="bg-gradient-to-br from-red-50 to-red-100 dark:from-red-900 dark:to-red-800 p-5 rounded-xl shadow-lg border-2 border-red-200 dark:border-red-700">
<div class="text-3xl mb-2">❌</div>
<div class="text-lg font-bold">Performance ≠ Metaproductivity</div>
</div>
</v-click>

<v-click>
<div class="bg-gradient-to-br from-green-50 to-green-100 dark:from-green-900 dark:to-green-800 p-5 rounded-xl shadow-lg border-2 border-green-200 dark:border-green-700">
<div class="text-3xl mb-2">✅</div>
<div class="text-lg font-bold">Lineages > Individuals</div>
</div>
</v-click>

<v-click>
<div class="bg-gradient-to-br from-blue-50 to-blue-100 dark:from-blue-900 dark:to-blue-800 p-5 rounded-xl shadow-lg border-2 border-blue-200 dark:border-blue-700">
<div class="text-3xl mb-2">🧮</div>
<div class="text-lg font-bold">CMP Oracle = Gödel Machine</div>
</div>
</v-click>

<v-click>
<div class="bg-gradient-to-br from-purple-50 to-purple-100 dark:from-purple-900 dark:to-purple-800 p-5 rounded-xl shadow-lg border-2 border-purple-200 dark:border-purple-700">
<div class="text-3xl mb-2">🏆</div>
<div class="text-lg font-bold">Human-Level Performance</div>
</div>
</v-click>

</div>

<v-click>
<div class="text-xl text-center bg-gradient-to-r from-yellow-50 to-orange-50 dark:from-yellow-900 dark:to-orange-900 p-6 rounded-xl shadow-xl max-w-4xl border-2 border-yellow-300 dark:border-yellow-700">
💡 <strong>Paradigm Shift:</strong> Focus on capacity to <strong>keep improving</strong>
</div>
</v-click>

</div>
