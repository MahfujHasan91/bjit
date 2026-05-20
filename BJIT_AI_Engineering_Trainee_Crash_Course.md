# 🎯 BJIT AI Engineering Trainee — 5-Hour Top 1% Crash Course

> **Exam Source:** BJIT Limited (Bangladesh-Japan IT)  
> **Role:** AI Engineering Trainee  
> **Strategy:** High-yield topic targeting + BJIT-specific pattern analysis + AI differentiator mastery

---

## ⚡ EXAM STRATEGY (Read This First)

Based on BJIT's past written exams (Glassdoor, GitHub repo analysis):
- **Format mix:** Problem-solving (55%) + MCQ (45%)
- **Coding section:** Write/complete code on paper (C++/Java/Python)
- **Passing threshold:** ~50%, but you need **85%+** to be in top 1% and get shortlisted among 350+ candidates
- **BJIT-specific focus:** Strong OOP (Java-heavy), clean code logic, recursion, array/string manipulation
- **AI Role differentiator:** They will test AI Fundamentals & Math heavier than standard SWE roles

### Top 1% Mindset
1. **Speed + Accuracy:** Don't get stuck on one problem. Move on and return.
2. **Show OOP Mastery:** Use inheritance, interfaces, proper encapsulation in design questions.
3. **Write Clean Paper Code:** Indent properly, use meaningful variable names even on paper.
4. **AI Edge:** Know basic ML pipeline, neural nets, and probability — most candidates neglect this.

---

## ⏰ 5-HOUR BATTLE PLAN

| Time | Topic | Focus Area |
|------|-------|------------|
| **0:00–0:45** | Data Structures | Arrays, Linked List, Stack/Queue, BST, HashMap |
| **0:45–1:30** | Algorithms + Programming | Sorting, Binary Search, Two Pointers, Recursion, Complexity |
| **1:30–2:15** | OOP + Design Patterns | 4 Pillars, SOLID, Singleton, Factory, UML basics |
| **2:15–2:45** | Database | SQL queries, Normalization, ACID, Indexing, Joins |
| **2:45–3:45** | AI Fundamentals | ML pipeline, Neural Networks, Backpropagation, Overfitting, CNN/RNN basics |
| **3:45–4:15** | Math / Statistics | Probability, Bayes, Mean/Var/StdDev, Linear Algebra (matrix basics), Derivatives |
| **4:15–4:45** | Analytical / IQ / Puzzle | Pattern recognition, logical grids, probability puzzles, clock/calendar |
| **4:45–5:00** | Rapid Review | Read the "Quick Recall Cheat Sheet" at the end twice |

---

## 1️⃣ DATA STRUCTURES (45 min)

### Must-Know Concepts (BJIT Frequently Tests)

#### **Arrays & Strings**
- **Two-pointer technique:** Merge sorted arrays, remove duplicates, move zeros
- **Sliding window:** Max sum subarray of size K, longest substring without repeating chars
- **Rotation:** Left/right rotate array by K positions (BJIT asked this exact question)
- **In-place operations:** Dutch national flag (sort 0s,1s,2s), merge without extra space

#### **Linked List**
- Reverse singly linked list (iterative + recursive)
- Detect loop (Floyd's Cycle)
- Find middle node
- Merge two sorted linked lists
- **Practice:** Write the `Node` class and full reverse function on paper NOW.

#### **Stack & Queue**
- Implement queue using two stacks
- Next Greater Element (NGE)
- Balanced parentheses checker
- **LRU Cache** concept (uses HashMap + Doubly Linked List)

#### **Tree & BST**
- Inorder/Preorder/Postorder (recursive + iterative)
- Height of tree, diameter
- **BST:** Insert, delete, search, validate BST, LCA (Lowest Common Ancestor)
- BFS vs DFS (when to use which)

#### **Heap & Hashing**
- Min/Max heap for "K largest/smallest elements"
- HashMap for frequency counting, two-sum
- Collision resolution: Chaining vs Open Addressing

### BJIT-Style Questions to Solve Mentally
1. Reverse a linked list. Draw the pointer changes.
2. Find duplicate in array without extra space ( Floyd's Tortoise-Hare for arrays).
3. Check balanced parentheses: `{{[[(())]]}}` → valid?
4. Merge `[[1,3],[2,6],[8,10],[15,18]]` → overlapping intervals.

---

## 2️⃣ ALGORITHMS & PROGRAMMING (45 min)

### Complexity Analysis (Always Asked)
| Big-O | Name | Example |
|-------|------|---------|
| O(1) | Constant | HashMap access |
| O(log n) | Logarithmic | Binary Search |
| O(n) | Linear | Single loop |
| O(n log n) | Linearithmic | Merge/Quick Sort |
| O(n²) | Quadratic | Nested loops (bubble sort) |
| O(2ⁿ) | Exponential | Recursive Fibonacci |

**Quick Tricks:**
- Drop constants: `O(2n) → O(n)`
- Drop non-dominant terms: `O(n² + n) → O(n²)`
- Space complexity = extra space used (excluding input)

### Essential Algorithms

#### **Binary Search Variants** (BJIT asks this heavily)
```cpp
// Standard binary search
int bs(vector<int>& arr, int target) {
    int lo = 0, hi = arr.size() - 1;
    while (lo <= hi) {
        int mid = lo + (hi - lo) / 2;  // Prevent overflow!
        if (arr[mid] == target) return mid;
        else if (arr[mid] < target) lo = mid + 1;
        else hi = mid - 1;
    }
    return -1;
}
```
- Lower bound: first element ≥ target
- Upper bound: first element > target
- Search in rotated sorted array

#### **Sorting (Know Intimately)**
| Algorithm | Best | Average | Worst | Space | Stable? |
|-----------|------|---------|-------|-------|---------|
| QuickSort | O(n log n) | O(n log n) | O(n²) | O(log n) | No |
| MergeSort | O(n log n) | O(n log n) | O(n log n) | O(n) | Yes |
| HeapSort | O(n log n) | O(n log n) | O(n log n) | O(1) | No |
- **BJIT favorite:** QuickSort partition logic, MergeSort merge logic

#### **Recursion (BJIT Written Exam Heavy Topic)**
- Base case + recursive case = must define both
- Classic problems: Fibonacci, factorial, tower of hanoi, permutations, subsets
- **Head recursion vs tail recursion**
- **Memoization trick:** `dp[n] = dp[n-1] + dp[n-2]` to avoid O(2ⁿ)

#### **Two Pointers / Sliding Window**
- Pair sum in sorted array
- 3Sum problem
- Longest substring with K distinct characters

#### **Graph Basics** (Since it's AI role)
- BFS (queue) vs DFS (stack/recursion)
- Dijkstra's shortest path (conceptual)
- Adjacency list vs matrix representation

### Paper-Coding Drills (Do These Now)
Write **pseudocode + actual code** for:
1. Binary search implementation (iterative)
2. QuickSort partition function
3. Factorial using tail recursion
4. Detect cycle in linked list
5. Merge two sorted arrays without extra space

---

## 3️⃣ OOP + DESIGN PATTERNS (45 min)

### OOP — The 4 Pillars (BJIT Interview & Written Focus)

| Pillar | Definition | BJIT Trap Questions |
|--------|-----------|---------------------|
| **Encapsulation** | Hide data, expose methods (getters/setters) | Why private fields? |
| **Inheritance** | IS-A relationship. Child extends Parent | Multiple inheritance in Java? (No, use interfaces) |
| **Polymorphism** | Same name, different behavior | Overloading vs Overriding |
| **Abstraction** | Hide implementation, show functionality | Abstract class vs Interface (Java 8+) |

### Key Distinctions (Memorize)
- **Overloading:** Same method name, different parameters. Compile-time polymorphism.
- **Overriding:** Same signature in parent/child. Runtime polymorphism. Needs `@Override`.
- **Abstract Class:** Can have constructors, instance variables, non-abstract methods. `extends`.
- **Interface:** All methods public abstract (pre-Java 8). `implements`. Supports multiple inheritance.
- **IS-A** = Inheritance. **HAS-A** = Composition/Aggregation.

### SOLID Principles (Top 1% Differentiator)
| Letter | Principle | One-Liner |
|--------|-----------|-----------|
| S | Single Responsibility | One class, one job |
| O | Open/Closed | Open for extension, closed for modification |
| L | Liskov Substitution | Child class should substitute parent without issues |
| I | Interface Segregation | Don't force clients to depend on methods they don't use |
| D | Dependency Inversion | Depend on abstractions, not concretions |

### Design Patterns (High-Yield Only)

#### **Creational**
- **Singleton:** One instance only. Private constructor, static getInstance().
  ```java
  public class Singleton {
      private static Singleton instance;
      private Singleton() {}
      public static Singleton getInstance() {
          if (instance == null) instance = new Singleton();
          return instance;
      }
  }
  ```
- **Factory:** Create objects without specifying exact class. `ShapeFactory.getShape("CIRCLE")`

#### **Structural**
- **Adapter:** Convert interface to another (wrapper)
- **Decorator:** Add behavior dynamically (Java I/O streams)

#### **Behavioral**
- **Observer:** One-to-many dependency (event listeners)
- **Strategy:** Family of interchangeable algorithms

### UML Basics (Know the Symbols)
- `---->` : Association
- `——▷` : Inheritance (IS-A)
- `——◆>` : Composition (strong HAS-A, lifetime linked)
- `——◇>` : Aggregation (weak HAS-A, lifetime independent)

---

## 4️⃣ DATABASE (30 min)

### SQL — Write These Queries Blindfolded

```sql
-- 1. Select with JOIN
SELECT e.name, d.dept_name 
FROM employees e 
INNER JOIN departments d ON e.dept_id = d.id;

-- 2. Aggregation with HAVING
SELECT dept_id, AVG(salary) as avg_sal 
FROM employees 
GROUP BY dept_id 
HAVING AVG(salary) > 50000;

-- 3. Subquery / CTE
WITH high_earners AS (
    SELECT * FROM employees WHERE salary > 100000
)
SELECT * FROM high_earners WHERE dept_id = 5;

-- 4. Window Function (AI/Data role differentiator)
SELECT name, salary, 
       RANK() OVER (ORDER BY salary DESC) as salary_rank
FROM employees;
```

### Normalization (Know 1NF–3NF)
| Form | Rule | Fix |
|------|------|-----|
| 1NF | Atomic values, no repeating groups | Split multi-valued attributes |
| 2NF | 1NF + no partial dependency | Remove columns depending on part of PK |
| 3NF | 2NF + no transitive dependency | Remove columns depending on non-key |

### ACID Properties
- **Atomicity:** All or nothing (transaction)
- **Consistency:** Valid state to valid state
- **Isolation:** Concurrent transactions don't interfere
- **Durability:** Committed data survives crashes

### Indexing
- **B-Tree index:** Default, good for range queries
- **Hash index:** Good for exact match (=)
- **When to index:** Columns in WHERE, JOIN, ORDER BY. Don't over-index (slows INSERT/UPDATE).

### Key Differences (MCQ Traps)
- **WHERE vs HAVING:** WHERE filters rows; HAVING filters groups.
- **INNER JOIN:** Only matching rows. **LEFT JOIN:** All left + matching right.
- **DELETE:** Remove rows, structure stays. **DROP:** Remove table entirely. **TRUNCATE:** Remove all rows, fast, no rollback.
- **UNION:** Distinct rows. **UNION ALL:** Keep duplicates.

---

## 5️⃣ AI FUNDAMENTALS (60 min) — YOUR BIGGEST DIFFERENTIATOR

Since most candidates focus only on DSA, **mastering this section puts you in the top 1%**.

### Machine Learning Pipeline
```
Raw Data → Cleaning → Feature Engineering → Model Training → Evaluation → Deployment
```

### Types of Learning
| Type | Description | Example |
|------|-------------|---------|
| **Supervised** | Labeled data | Regression, Classification |
| **Unsupervised** | No labels | Clustering (K-Means), PCA |
| **Reinforcement** | Rewards/penalties | Game playing, Robotics |

### Core Algorithms (Know Concept + Use Case)

#### **Regression**
- **Linear Regression:** `y = mx + c`. Minimize MSE. Gradient descent.
- **Logistic Regression:** Sigmoid function `σ(z) = 1/(1+e⁻ᶻ)`. For classification.

#### **Classification**
- **Decision Tree:** Split on entropy/gini. Prone to overfitting.
- **Random Forest:** Ensemble of trees. Bagging technique.
- **SVM:** Find hyperplane with maximum margin. Kernel trick for non-linear.
- **KNN:** Lazy learner. Distance metric (Euclidean). K = odd number for binary.

#### **Clustering**
- **K-Means:** Minimize within-cluster sum of squares. Choose K via Elbow method.
- **Hierarchical:** Agglomerative (bottom-up) vs Divisive (top-down).

### Neural Networks (Since BJIT mentions DeepLearning)

#### **Perceptron → MLP**
```
Input (x) → Weights (w) → Summation (Σwx + b) → Activation (σ) → Output
```
- **Forward Propagation:** Compute predicted output
- **Loss Function:** MSE (regression), Cross-Entropy (classification)
- **Backpropagation:** Chain rule to update weights. `w_new = w_old - α(∂L/∂w)`

#### **Activation Functions**
| Function | Formula | Use Case | Problem |
|----------|---------|----------|---------|
| Sigmoid | `1/(1+e⁻ˣ)` | Binary output | Vanishing gradient |
| ReLU | `max(0,x)` | Hidden layers | Dying ReLU |
| Tanh | `(eˣ-e⁻ˣ)/(eˣ+e⁻ˣ)` | Hidden layers | Vanishing gradient |
| Softmax | `e^(zᵢ)/Σe^(zⱼ)` | Multi-class output | — |

#### **CNN (Convolutional Neural Network)** — For image tasks
- **Convolution:** Filter/kernel slides over image to extract features
- **Pooling:** Max/Avg pooling for downsampling
- **Flatten → Dense → Output**
- **Concept:** Parameter sharing, translation invariance

#### **RNN / LSTM** — For sequence tasks
- **RNN:** Hidden state feeds into next step. Short-term memory.
- **LSTM:** Long Short-Term Memory. Gates (input, forget, output) control information flow.
- **Use:** Time series, NLP, speech recognition

### Overfitting vs Underfitting
| Scenario | Symptom | Fix |
|----------|---------|-----|
| **Underfitting** | High train error, high test error | More features, complex model, longer training |
| **Overfitting** | Low train error, high test error | Regularization (L1/L2), dropout, more data, early stopping, cross-validation |

### Regularization
- **L1 (Lasso):** `Loss + λ|w|` → Sparse weights (feature selection)
- **L2 (Ridge):** `Loss + λw²` → Small weights
- **Dropout:** Randomly drop neurons during training (p = 0.2–0.5)

### Evaluation Metrics
| Metric | Formula | When to Use |
|--------|---------|-------------|
| **Accuracy** | `(TP+TN)/(Total)` | Balanced classes |
| **Precision** | `TP/(TP+FP)` | When FP is costly (spam filter) |
| **Recall** | `TP/(TP+FN)` | When FN is costly (disease detection) |
| **F1-Score** | `2·Precision·Recall/(P+R)` | Imbalanced classes |
| **ROC-AUC** | Area under ROC curve | Binary classification comparison |
| **Confusion Matrix** | TP, FP, TN, FN grid | All classification problems |

### Cross-Validation
- **K-Fold:** Split into K parts. Train on K-1, test on 1. Rotate. Average scores.
- **Stratified K-Fold:** Preserves class distribution in each fold.

### Bias-Variance Tradeoff
- **Bias:** Error from overly simple assumptions (underfitting)
- **Variance:** Error from sensitivity to small fluctuations (overfitting)
- **Goal:** Minimize total error = Bias² + Variance + Irreducible Error

### NLP Basics (Bonus — BJIT works on Pocketalk translator)
- **Tokenization:** Split text into words/subwords
- **Word Embedding:** Word2Vec, GloVe — map words to dense vectors
- **Transformer:** Self-attention mechanism. "Attention Is All You Need"
- **BERT:** Bidirectional encoder representations. Pre-training + fine-tuning.

---

## 6️⃣ MATH / STATISTICS (30 min)

### Probability (BJIT asks this!)
- **P(A∪B) = P(A) + P(B) - P(A∩B)**
- **Conditional:** `P(A|B) = P(A∩B)/P(B)`
- **Bayes' Theorem:** `P(A|B) = P(B|A)·P(A)/P(B)` ← **MEMORIZE**
- **Independent:** `P(A∩B) = P(A)·P(B)`
- **Mutually Exclusive:** `P(A∩B) = 0`

#### Common Probability Traps
- **Birthday Problem:** 23 people → >50% chance of shared birthday
- **Monty Hall:** Switch doors → 2/3 win probability
- **Gambler's Fallacy:** Past events don't affect independent future events

### Statistics for ML
| Concept | Formula | Meaning |
|---------|---------|---------|
| Mean (μ) | `Σx/n` | Average |
| Variance (σ²) | `Σ(x-μ)²/n` | Spread of data |
| Std Dev (σ) | `√variance` | Typical distance from mean |
| Covariance | `Σ(x-x̄)(y-ȳ)/n` | How two variables vary together |
| Correlation | `Cov(X,Y)/(σₓ·σᵧ)` | Normalized covariance (-1 to 1) |

### Linear Algebra (Basics for AI)
- **Matrix multiplication:** `(A·B)[i,j] = Σ A[i,k]·B[k,j]` — inner dimensions must match
- **Transpose:** Rows ↔ Columns
- **Identity Matrix I:** Diagonal 1s, rest 0s. `A·I = A`
- **Inverse A⁻¹:** `A·A⁻¹ = I`. Only square matrices may have inverses.
- **Dot Product:** `a·b = Σ aᵢbᵢ`. Used in attention mechanisms, similarity.
- **Eigenvalues/Eigenvectors:** `Av = λv`. PCA uses this (reduce dimensions).

### Calculus (For understanding backprop)
- **Derivative of x² = 2x**
- **Derivative of eˣ = eˣ**
- **Chain rule:** `d/dx f(g(x)) = f'(g(x))·g'(x)`
- **Partial derivative:** Derivative w.r.t one variable, treat others as constant
- **Gradient:** Vector of partial derivatives. Points in direction of steepest ascent.

---

## 7️⃣ ANALYTICAL / IQ / PUZZLES (30 min)

### Pattern Recognition
- Number series: 2, 6, 12, 20, 30, ? (Answer: 42; pattern n(n+1))
- Visual rotation/reflection patterns
- Letter coding: If CAT = 3120, then DOG = ? (Position in alphabet multiplied)

### Logical Reasoning
- **Syllogisms:** All A are B. All B are C. Therefore All A are C. ✓
- **Venn diagrams:** 3-set problems
- **Direction sense:** "Face east, turn 45° left, walk 10m..."
- **Blood relations:** Draw a family tree quickly

### Classic Puzzles (Know the Trick)
1. **Two eggs, 100 floors:** Optimal strategy uses decreasing intervals (14, 27, 39...)
2. **25 horses, 5 tracks:** Find top 3 in minimum races (Answer: 7)
3. **Poisoned bottle, 10 mice:** Binary encoding. 1000 bottles need 10 mice (2¹⁰=1024)
4. **Bridge crossing:** 1,2,5,10 minutes. Fastest pair shuttles flashlight. Total: 17 min.
5. **Water jugs:** 3L and 5L to get 4L. Fill 5, pour to 3 (leaves 2), empty 3, pour 2 into 3, fill 5, pour 1 into 3 → 4L in 5-jug.

### Clock & Calendar
- **Angle between hands:** `|30H - 5.5M|` degrees
- **Leap year:** Divisible by 4, except centuries not divisible by 400
- **Odd days:** Jan 1, 2000 to Jan 1, 2024. Calculate leap years.

---

## 📝 QUICK RECALL CHEAT SHEET

### Complexity Cheat Sheet
| Operation | Array | LinkedList | BST (balanced) | HashMap |
|-----------|-------|------------|----------------|---------|
| Access | O(1) | O(n) | O(log n) | O(1) |
| Search | O(n) | O(n) | O(log n) | O(1) |
| Insert | O(n) | O(1)* | O(log n) | O(1) |
| Delete | O(n) | O(1)* | O(log n) | O(1) |

### Sorting Summary
- **QuickSort:** In-place, not stable, worst O(n²)
- **MergeSort:** Not in-place, stable, guaranteed O(n log n)
- **HeapSort:** In-place, not stable, guaranteed O(n log n)
- **Bubble/Insertion:** O(n²), only for small/nearly sorted data

### OOP Quick Memory
- **Overloading:** Compile-time, same name different params
- **Overriding:** Runtime, same signature, `@Override`
- **Interface:** 100% abstract (Java 7), multiple inheritance
- **Abstract Class:** 0-100% abstract, single inheritance
- **SOLID:** Single, Open/Closed, Liskov, Interface Segregation, Dependency Inversion

### SQL Quick Triggers
- `WHERE` before `GROUP BY`; `HAVING` after
- `INNER JOIN` = intersection; `LEFT JOIN` = all left table
- `COUNT(*)` counts NULLs; `COUNT(column)` doesn't
- Index speeds up SELECT, slows down INSERT/UPDATE

### AI Quick Triggers
- **Overfitting?** → Regularize, dropout, more data, simpler model
- **Imbalanced data?** → SMOTE, class weights, F1-score over accuracy
- **Images?** → CNN
- **Sequences?** → RNN/LSTM/Transformer
- **Labeled data?** → Supervised (Regression/Classification)
- **No labels?** → Unsupervised (Clustering)

### Probability Quick Triggers
- `P(A|B) = P(B|A)P(A)/P(B)` ← Bayes
- Independent: `P(A∩B) = P(A)·P(B)`
- Mutually exclusive: `P(A∩B) = 0`, so `P(A∪B) = P(A)+P(B)`

---

## 🎯 FINAL 15-MINUTE PRE-EXAM RITUAL

1. **Read through this cheat sheet twice.**
2. **Re-write on paper:** Linked list reverse, binary search, quicksort partition.
3. **Verbalize:** Explain Backpropagation and Bayes' theorem to yourself in 2 minutes each.
4. **Mindset:** You are not just solving problems; you are demonstrating **structured thinking** (Japanese companies value this deeply).

---

## ✅ BJIT EXAM DAY CHECKLIST

- [ ] Arrive early with multiple pens/pencils
- [ ] For coding problems: Write pseudocode first, then actual code
- [ ] Indent properly on paper — readability matters for Japanese evaluators
- [ ] For MCQs: Eliminate obviously wrong answers first
- [ ] If stuck >3 min on one problem: Mark and MOVE ON. Come back later.
- [ ] AI-specific questions: Use correct terminology (gradient descent, backprop, regularization)
- [ ] Show OOP thinking: If asked to design a system, mention classes, relationships, encapsulation
- [ ] Analytical puzzles: State assumptions clearly before solving

---

## 💬 BJIT-SPECIFIC INSIGHTS

- **Japanese work culture values:** Punctuality, respect, attention to detail, team harmony.
- If there's an HR component: Show willingness to learn, long-term commitment, interest in Japanese culture/语言 (they sometimes teach Japanese).
- **Technical Interview likely after written:** Be ready to explain your code and optimize it.
- Common BJIT follow-up: "How would you optimize this further?" or "What's the space complexity?"

---

**Good luck. You've got this. Focus, breathe, and execute systematically. Top 1% is about precision under pressure.** 🚀
