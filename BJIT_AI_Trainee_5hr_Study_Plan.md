# 🎯 BJIT AI Engineering Trainee — 5-Hour Power Study Plan
**Goal:** Top 1% on the written exam. Maximum signal, zero filler.

---

## 📌 What I Learned About BJIT's Written Exam (from real candidate reports)

| Fact | Implication for you |
|---|---|
| ~1 hour, ~100 marks, onsite, **written on paper** | Practice writing code by hand. No IDE = no autocomplete crutches. |
| Recurring topics: Array, Linked List, Stack/Queue, Recursion, String | These 5 = ~60% of DSA weight. Prioritize. |
| Common asked: left-rotate array by k, move zeros to end (stable), DFS, HashMap problems, code-fixing/sorting | Practice these *exact* patterns. |
| OOP questions try to **confuse** you (overload vs override, IS-A vs HAS-A) | Master edge cases, not just definitions. |
| Always at least one **non-programming analytical/IQ/puzzle** | Don't skip puzzle practice. |
| For **AI Trainee** specifically: AI Fundamentals + Math/Stats carry extra weight | New addition vs. old SWE trainee exam — many candidates will be weak here. **This is your differentiator.** |
| Negative marking is possible in MCQ sections | Don't blind-guess unless you can eliminate 2+ options. |

**Strategic insight:** Most candidates over-prepare DSA and under-prepare AI/Math. To hit top 1%, do *solid* DSA + **dominate AI/Stats + nail the puzzle**. That's the asymmetric edge.

---

## ⏱️ THE 5-HOUR PLAN (with strict timeboxes)

### 🟦 HOUR 1 — DSA Core Patterns (60 min)
Goal: lock in the patterns that *actually appear*.

| Min | Task | Deliverable |
|---|---|---|
| 0–10 | **Arrays** — write by hand: (1) left rotate by k using reversal trick, (2) move zeros to end preserving order (two-pointer), (3) find duplicates, (4) max subarray (Kadane) | 4 clean snippets on paper |
| 10–20 | **Strings** — reverse words, check palindrome, anagram check (HashMap), longest unique substring (sliding window) | 4 snippets |
| 20–30 | **Linked List** — reverse iterative + recursive, detect cycle (Floyd), find middle, merge two sorted lists | 4 snippets |
| 30–40 | **Stack/Queue** — balanced parentheses, next greater element, implement queue using 2 stacks, min-stack | 4 snippets |
| 40–55 | **Recursion** — factorial, fibonacci (memoized), permutations of a string, Tower of Hanoi logic, subset generation | 5 snippets |
| 55–60 | **Big-O cheat sheet** — memorize: array O(1) access, LL O(n) access, HashMap avg O(1) lookup, BST O(log n), sorting O(n log n), DFS/BFS O(V+E) | Recite from memory |

✅ **Rule:** Write each on paper at least once. Muscle memory beats reading.

---

### 🟦 HOUR 2 — Algorithms + OOP + Design Patterns (60 min)

#### Part A: Algorithms (25 min)
- **Searching:** Binary search + lower_bound/upper_bound (asked in BJIT past) — write the template
- **Sorting:** Know how QuickSort, MergeSort, BubbleSort work; complexity; stability
- **Graph:** DFS + BFS templates (BJIT asked DFS!) — write recursive DFS and iterative BFS
- **DP basics:** Fibonacci memoization, 0/1 knapsack idea, longest common subsequence concept

#### Part B: OOP (20 min) — **HIGH YIELD**
Memorize crisp 1-line answers (they ask trick questions here):

- **4 pillars:** Encapsulation, Inheritance, Polymorphism, Abstraction
- **Overloading vs Overriding:**
  - Overloading = same method name, different params, **compile-time**, same class
  - Overriding = subclass redefines parent method, **runtime**, same signature
- **IS-A vs HAS-A:** IS-A = inheritance (Dog IS-A Animal). HAS-A = composition (Car HAS-A Engine). **Prefer composition over inheritance.**
- **Abstract class vs Interface:** Abstract can have state + partial impl; interface = pure contract (Java 8+ allows default methods)
- **Access modifiers:** private < default/package < protected < public
- **`this` vs `super`**, **constructor chaining**, **why no multiple inheritance in Java (diamond problem)**
- **SOLID principles** (know all 5 by name + 1-line each)

#### Part C: Design Patterns (15 min) — know these 6 cold:
| Pattern | One-line purpose | Example |
|---|---|---|
| **Singleton** | One instance only | DB connection, logger |
| **Factory** | Create objects without specifying exact class | `ShapeFactory.create("circle")` |
| **Observer** | One-to-many notify | Event listeners, pub-sub |
| **Strategy** | Interchangeable algorithms | Payment methods |
| **Decorator** | Add behavior dynamically | Java I/O streams |
| **MVC** | Separate data/UI/logic | Web frameworks |

Bonus: be able to **write Singleton in Java** (with private constructor + static getInstance + thread-safe note).

---

### 🟦 HOUR 3 — Database + AI Fundamentals (60 min)

#### Part A: Database (20 min)
- **SQL essentials:** `SELECT … JOIN … WHERE … GROUP BY … HAVING … ORDER BY` — practice writing a query with all
- **JOIN types:** INNER, LEFT, RIGHT, FULL — draw the Venn diagrams mentally
- **Normalization:** 1NF (atomic), 2NF (no partial dep), 3NF (no transitive dep), BCNF
- **ACID:** Atomicity, Consistency, Isolation, Durability — 1 line each
- **Indexes:** B-tree, speeds reads, slows writes
- **Primary vs Foreign vs Unique key**
- **SQL vs NoSQL:** when to use each
- Practice query: *"Get 2nd highest salary"* (`SELECT MAX(salary) FROM emp WHERE salary < (SELECT MAX(salary) FROM emp)`)

#### Part B: AI Fundamentals (40 min) — **YOUR EDGE**
This is what separates AI Trainee applicants. Master these:

**ML Basics:**
- **Supervised vs Unsupervised vs Reinforcement** — definitions + example each
- **Classification vs Regression** — output type
- **Training / Validation / Test split** — typical 70/15/15 or 80/10/10
- **Overfitting vs Underfitting** — high variance vs high bias. Fixes: regularization (L1/L2), dropout, more data, cross-validation

**Core Algorithms (know what they do + when to use):**
- Linear Regression, Logistic Regression
- Decision Trees, Random Forest
- K-Nearest Neighbors (KNN)
- K-Means clustering (unsupervised)
- Naive Bayes
- SVM (1-line)
- Neural Network basics: neuron = weighted sum + activation; layers; forward/backprop
- **Gradient Descent:** iteratively minimize loss by moving against gradient. Variants: Batch, SGD, Mini-batch

**Evaluation Metrics:**
- **Classification:** Accuracy, Precision, Recall, F1, Confusion Matrix, ROC-AUC
  - **Precision** = TP / (TP+FP) → "of what I predicted positive, how many right"
  - **Recall** = TP / (TP+FN) → "of all actual positives, how many caught"
  - **F1** = harmonic mean of P & R
- **Regression:** MSE, RMSE, MAE, R²

**Deep Learning quick hits:**
- CNN → images (convolution + pooling)
- RNN/LSTM → sequences/text
- Transformer → modern NLP (attention mechanism)
- Activation functions: ReLU (most common), Sigmoid, Tanh, Softmax (multi-class output)

**Bonus high-value terms:** epoch, batch size, learning rate, loss function, one-hot encoding, normalization vs standardization, feature engineering, bias-variance tradeoff.

---

### 🟦 HOUR 4 — Math/Statistics + Analytical/IQ/Puzzles (60 min)

#### Part A: Math & Stats (30 min)
**Probability:**
- P(A ∩ B) = P(A)·P(B) if independent
- P(A ∪ B) = P(A) + P(B) − P(A ∩ B)
- **Bayes' theorem:** P(A|B) = P(B|A)·P(A) / P(B) — practice 1 example
- Expected value: Σ x·P(x)
- Permutations nPr = n!/(n−r)!, Combinations nCr = n!/(r!(n−r)!)

**Statistics:**
- Mean, median, mode, range
- **Variance** = avg of squared deviations from mean; **Std Dev** = √variance
- Normal distribution: 68-95-99.7 rule
- Correlation vs Causation
- Type I error (false positive) vs Type II (false negative)

**Linear Algebra (AI essentials):**
- Vector dot product, matrix multiplication rules (m×n · n×p = m×p)
- Identity matrix, transpose, inverse (conceptually)
- Eigenvalue/eigenvector — 1-line intuition (direction unchanged by transform)

**Calculus (minimal):**
- Derivative = slope; gradient = vector of partial derivatives
- Why it matters: gradient descent uses derivatives to minimize loss

#### Part B: Analytical / IQ / Puzzles (30 min)
**Classic puzzles to know cold (1 of these often appears):**

1. **25 horses, 5 tracks, find top 3** → 7 races
2. **2 eggs, 100 floors** (find critical floor minimizing worst-case) → answer 14
3. **3 bulbs, 3 switches** (one room visit) → use heat
4. **Bridge & torch:** 4 people cross with 1 torch, times 1,2,5,10 → 17 min
5. **Weighing 8 balls, 1 heavier, balance scale** → 2 weighings
6. **Truth-teller / liar** logic (knight & knave)
7. **Light bulb in series/parallel** circuit puzzles

**Pattern recognition warmup:**
- Number series: 2, 6, 12, 20, 30, ? → 42 (add consecutive even numbers)
- Letter series: A, C, F, J, O, ? → U (skip 1, 2, 3, 4, 5)
- Odd one out, analogies

**Tip:** When a puzzle stumps you, write what you know, find the invariant, work backwards from the goal.

---

### 🟦 HOUR 5 — Mock Exam + Weak-Spot Patching (60 min)

#### Part A: Self-Mock (40 min)
Simulate the real exam. Set a timer, paper + pen, NO laptop.

**Mini mock paper (do this!):**
1. (15 min) Write a function in your preferred language: **rotate an array left by k positions** (in-place, O(1) extra space using reversal trick).
2. (10 min) Write **DFS on an adjacency list** (recursive).
3. (5 min) **OOP question:** Explain the difference between abstract class and interface with one example each.
4. (5 min) **SQL:** Given `Employees(id, name, dept_id, salary)` and `Departments(id, name)`, write a query to get the **highest-paid employee per department**.
5. (5 min) **AI:** What is overfitting? Name 3 ways to prevent it.
6. (5 min) **Puzzle:** You have a 3L jug and a 5L jug. Measure exactly 4L. Show steps.
7. (5 min) **Stats:** A test is 99% accurate. Disease affects 1 in 10,000. You test positive. What's the chance you actually have it? (Bayes' theorem.)

#### Part B: Review & Patch (20 min)
- Review what you got wrong
- Re-read your weakest area from Hours 1–4
- Write a **1-page cheat sheet** of formulas / patterns / definitions you keep forgetting
- Sleep early. Brain consolidates overnight.

---

## 🧠 EXAM-DAY TACTICS (Top 1% behavior)

1. **First pass — skim the whole paper** (2 min). Mark easy/medium/hard.
2. **Easy first.** Bank points fast. Build confidence.
3. **For coding questions on paper:**
   - Write your **approach in 1 line first** (e.g., "// two pointers, O(n)")
   - Then **dry-run with a small example** in the margin
   - Then write clean code
   - Mention **time & space complexity** at the end — examiners love this
4. **For OOP/AI conceptual:** Use **bullets + 1 example**. Avoid walls of text.
5. **For the puzzle:** Show your reasoning steps even if unsure of final answer — partial credit is real.
6. **Last 5 minutes:** review, fix obvious bugs (off-by-one, null checks), ensure name/ID on every page.
7. **Don't blank-fill MCQs** if there's negative marking and you can't eliminate ≥2 options.
8. **Comment your code** — shows clarity of thought. Big differentiator.

---

## 🚫 What NOT to do in the next 5 hours
- ❌ Don't start a new framework/language
- ❌ Don't deep-dive a single Leetcode hard problem for 1 hour
- ❌ Don't read theory passively for >15 min straight — always write something
- ❌ Don't skip the puzzle/AI sections to "do more DSA" — that's where the herd over-invests

---

## 🎯 The Top-1% Mindset
Most candidates will be solid at DSA + OOP but **weak at AI fundamentals, stats, and the puzzle**. Those are the *exact* sections this role weighs more heavily because it's an **AI** trainee role. Be the candidate who is *good* at code AND *confident* on overfitting, Bayes, and gradient descent. That combo is rare and that's how you stand out.

**You've got this. Now close this file and start Hour 1. Good luck. 🚀**
