# 🧠 BJIT AI Engineering Trainee — Practice Problems with Solutions

> Solve these **on paper** to simulate exam conditions. Time yourself: 10 min per problem.

---

## DATA STRUCTURES

### Problem 1: Move All Zeros to End (BJIT-style)
**Input:** `[1, 0, 2, -4, 0, 5, 0, 11]`  
**Output:** `[1, 2, -4, 5, 11, 0, 0, 0]`  
**Constraint:** In-place, O(n) time, O(1) extra space.

<details>
<summary>Solution</summary>

```cpp
void moveZeros(vector<int>& nums) {
    int j = 0; // Position to place next non-zero
    for (int i = 0; i < nums.size(); i++) {
        if (nums[i] != 0) {
            swap(nums[i], nums[j]);
            j++;
        }
    }
}
```
**Idea:** `j` tracks where the next non-zero should go. Swap non-zero elements forward.
</details>

---

### Problem 2: Detect Loop in Linked List
**Given:** Head of singly linked list.  
**Return:** `true` if cycle exists, else `false`.

<details>
<summary>Solution</summary>

```cpp
bool hasCycle(ListNode* head) {
    if (!head || !head->next) return false;
    ListNode *slow = head, *fast = head;
    while (fast && fast->next) {
        slow = slow->next;          // Move 1 step
        fast = fast->next->next;    // Move 2 steps
        if (slow == fast) return true; // Collision = loop
    }
    return false;
}
```
**Idea:** Floyd's Cycle Detection. If there's a loop, fast ptr will eventually meet slow ptr.
</details>

---

### Problem 3: Valid Parentheses
**Input:** `"{[()]}", "{[(])}", "{{[[(())]]}}"`  
**Output:** `true, false, true`

<details>
<summary>Solution</summary>

```cpp
bool isValid(string s) {
    stack<char> st;
    for (char c : s) {
        if (c == '(' || c == '{' || c == '[') st.push(c);
        else {
            if (st.empty()) return false;
            char top = st.top(); st.pop();
            if ((c == ')' && top != '(') ||
                (c == '}' && top != '{') ||
                (c == ']' && top != '[')) return false;
        }
    }
    return st.empty();
}
```
</details>

---

## ALGORITHMS

### Problem 4: Binary Search — Find First and Last Position
**Input:** `nums = [5,7,7,8,8,10], target = 8`  
**Output:** `[3,4]`

<details>
<summary>Solution</summary>

```cpp
int findBound(vector<int>& nums, int target, bool isFirst) {
    int lo = 0, hi = nums.size() - 1, ans = -1;
    while (lo <= hi) {
        int mid = lo + (hi - lo) / 2;
        if (nums[mid] == target) {
            ans = mid;
            if (isFirst) hi = mid - 1; // Look left
            else lo = mid + 1;         // Look right
        } else if (nums[mid] < target) lo = mid + 1;
        else hi = mid - 1;
    }
    return ans;
}
```
**Key:** When you find target, don't return immediately. Keep searching in the relevant half to find the boundary.
</details>

---

### Problem 5: QuickSort Partition (Lomuto)
**Task:** Implement partition function used in QuickSort.

<details>
<summary>Solution</summary>

```cpp
int partition(vector<int>& arr, int low, int high) {
    int pivot = arr[high]; // Choose last element as pivot
    int i = low - 1;       // Index of smaller element
    for (int j = low; j < high; j++) {
        if (arr[j] < pivot) {
            i++;
            swap(arr[i], arr[j]);
        }
    }
    swap(arr[i + 1], arr[high]);
    return i + 1; // Pivot's final position
}
```
**Trick:** `i` always points to the last element smaller than pivot. Swap `arr[i+1]` with pivot at end.
</details>

---

### Problem 6: Find Duplicate (Floyd's Tortoise-Hare for Array)
**Input:** `nums = [1,3,4,2,2]` (values in range [1,n], array size n+1)  
**Output:** `2`

<details>
<summary>Solution</summary>

```cpp
int findDuplicate(vector<int>& nums) {
    int slow = nums[0], fast = nums[0];
    // Phase 1: Find meeting point
    do {
        slow = nums[slow];
        fast = nums[nums[fast]];
    } while (slow != fast);
    // Phase 2: Find entrance to cycle
    slow = nums[0];
    while (slow != fast) {
        slow = nums[slow];
        fast = nums[fast];
    }
    return slow;
}
```
**Why it works:** Treat values as pointers. Duplicate value creates a cycle. Floyd's algorithm finds cycle entrance.
</details>

---

## OOP & DESIGN

### Problem 7: Design a Parking Lot (System Design Mini)
**Requirements:**
- Multiple floors, multiple spots per floor
- Spots can be compact, large, handicapped, motorcycle
- Vehicle can park if suitable spot available

<details>
<summary>Solution Outline</summary>

```java
abstract class Vehicle {
    String licensePlate;
    VehicleSize size;
    abstract boolean canFitInSpot(ParkingSpot spot);
}
class Car extends Vehicle { ... }
class Truck extends Vehicle { ... }

class ParkingSpot {
    VehicleSize size;
    Vehicle currentVehicle;
    boolean isAvailable() { return currentVehicle == null; }
}

class ParkingLot {
    List<ParkingFloor> floors;
    boolean parkVehicle(Vehicle v) { ... } // Find first available spot
}
```
**Design points:**
- Use **inheritance** for Vehicle types (IS-A)
- Use **composition** for ParkingLot has Floors, Floors have Spots (HAS-A)
- **Encapsulation:** Spot availability managed internally
- **Single Responsibility:** Each class has one job
</details>

---

### Problem 8: Singleton Thread-Safe (Java)

<details>
<summary>Solution</summary>

```java
public class Singleton {
    private static volatile Singleton instance;
    private Singleton() {}
    public static Singleton getInstance() {
        if (instance == null) {
            synchronized (Singleton.class) {
                if (instance == null) instance = new Singleton();
            }
        }
        return instance;
    }
}
```
**Key:** `volatile` prevents instruction reordering. Double-checked locking for performance.
</details>

---

## DATABASE

### Problem 9: SQL — Department Top 3 Salaries
**Table:** Employee (id, name, salary, departmentId), Department (id, name)  
**Task:** Find top 3 salaries in each department.

<details>
<summary>Solution</summary>

```sql
SELECT d.name AS Department, e.name AS Employee, e.salary AS Salary
FROM Employee e
JOIN Department d ON e.departmentId = d.id
WHERE (
    SELECT COUNT(DISTINCT e2.salary)
    FROM Employee e2
    WHERE e2.salary > e.salary AND e2.departmentId = e.departmentId
) < 3;
```
**Or using window function (modern, preferred):**
```sql
SELECT Department, Employee, Salary
FROM (
    SELECT d.name AS Department, e.name AS Employee, e.salary AS Salary,
           DENSE_RANK() OVER (PARTITION BY d.id ORDER BY e.salary DESC) as rnk
    FROM Employee e
    JOIN Department d ON e.departmentId = d.id
) ranked
WHERE rnk <= 3;
```
**Use DENSE_RANK** not ROW_NUMBER if ties should share a rank.
</details>

---

## AI / MACHINE LEARNING

### Problem 10: Explain Backpropagation in 3 Steps

<details>
<summary>Answer (Write this in exam)</summary>

1. **Forward Pass:** Input flows through network layers. Compute predicted output ŷ. Calculate loss `L = Loss(y, ŷ)`.
2. **Backward Pass:** Compute gradient of loss w.r.t each weight using **chain rule** of calculus. `∂L/∂w = ∂L/∂a · ∂a/∂z · ∂z/∂w`.
3. **Weight Update:** Adjust weights in opposite direction of gradient to minimize loss: `w = w - α·(∂L/∂w)`, where α = learning rate.

**Key terms to mention:** Chain rule, gradient descent, learning rate, partial derivatives.
</details>

---

### Problem 11: Bias-Variance Tradeoff
**Question:** Your model has 95% training accuracy but 60% test accuracy. Diagnose and fix.

<details>
<summary>Answer</summary>

**Diagnosis:** High variance → **Overfitting**

**Fixes:**
1. Add more training data
2. Regularization (L1/L2)
3. Dropout layers (neural nets)
4. Early stopping during training
5. Simplify model (reduce depth/features)
6. Cross-validation for hyperparameter tuning
7. Feature selection / dimensionality reduction
</details>

---

### Problem 12: CNN vs RNN — When to Use What?

<details>
<summary>Answer</summary>

| | CNN | RNN/LSTM/Transformer |
|---|---|---|
| **Data type** | Grid-like: images, videos | Sequential: text, time series, speech |
| **Key concept** | Convolution filters for spatial feature extraction | Hidden state for temporal dependencies |
| **Parameter sharing** | Yes (same filter across image) | Yes (same weights across time steps) |
| **Examples** | Image classification, object detection | Machine translation, sentiment analysis, stock prediction |

**For NLP:** Transformer > RNN/LSTM now because of parallelization and attention mechanism capturing long-range dependencies.
</details>

---

## MATH / PROBABILITY

### Problem 13: Bayes' Theorem Application
**Scenario:** A disease affects 1% of population. Test is 99% accurate (true positive and true negative). You tested positive. What's probability you actually have disease?

<details>
<summary>Solution</summary>

- P(Disease) = 0.01
- P(Positive|Disease) = 0.99
- P(Positive|No Disease) = 0.01

```
P(Disease|Positive) = P(Positive|Disease)·P(Disease) / P(Positive)
                   = (0.99 × 0.01) / [(0.99×0.01) + (0.01×0.99)]
                   = 0.0099 / (0.0099 + 0.0099)
                   = 0.5
```
**Answer: 50%** — Counterintuitive! Even with 99% accurate test, rare disease + false positives from healthy population bring it to 50%.

**Exam tip:** Always write the formula first, then substitute values.
</details>

---

### Problem 14: Probability — Two Dice
**Question:** What's the probability that sum of two dice is 7 or 11?

<details>
<summary>Solution</summary>

Total outcomes = 36.
- Sum = 7: (1,6), (2,5), (3,4), (4,3), (5,2), (6,1) → 6 ways
- Sum = 11: (5,6), (6,5) → 2 ways

P(7 or 11) = (6 + 2) / 36 = 8/36 = **2/9**
</details>

---

## ANALYTICAL / PUZZLE

### Problem 15: The 25 Horses Puzzle
**You have 25 horses, 5 tracks. Each race has 5 horses. You need top 3 horses. Minimum races?**

<details>
<summary>Solution</summary>

**Answer: 7 races**

1. Divide into 5 groups (A,B,C,D,E). Race each → 5 races. Keep positions within each group.
2. Race winners of each group → 6th race. Say result: A1 > B1 > C1 > D1 > E1.

**Eliminate:**
- D and E groups entirely (their winners lost to C1)
- C2, C3, C4, C5 (C1 is at best 3rd overall)
- B3, B4, B5 (B1 is at best 3rd, so B3+ can't be top 3)
- A4, A5

**Candidates left:** A1, A2, A3, B1, B2, C1
3. Race these 6 (but track holds 5, so actually A2,A3,B1,B2,C1) → 7th race. Top 2 from this race + A1 = overall top 3.
</details>

---

### Problem 16: Clock Angle
**Question:** What's the angle between hour and minute hands at 3:15?

<details>
<summary>Solution</summary>

- Minute hand: 15 mins → `15 × 6° = 90°` from 12
- Hour hand: 3 hours + 15 mins = `3.25 hrs` → `3.25 × 30° = 97.5°` from 12
- Angle = `|97.5 - 90| = 7.5°`

**Formula:** `|30H - 5.5M|`
</details>

---

## ⚡ SPEED DRILL (Do in 10 Minutes)

Without looking at solutions, write code/pseudocode for:
1. Binary Search (iterative)
2. Reverse a linked list
3. SQL: Select employees earning above average in their department
4. Explain gradient descent in 2 sentences
5. A biased coin (P(H)=0.6). What's P(2 heads in 3 flips)?

---

**Answers to Speed Drill:**
<details>
<summary>Click after attempting</summary>

5. P(2 heads in 3 flips) = C(3,2) × (0.6)² × (0.4)¹ = 3 × 0.36 × 0.4 = **0.432**

SQL:
```sql
SELECT e.* 
FROM Employee e
WHERE e.salary > (
    SELECT AVG(salary) FROM Employee e2 
    WHERE e2.departmentId = e.departmentId
);
```
</details>
