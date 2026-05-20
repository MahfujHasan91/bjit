# 🎓 BJIT AI Engineering Trainee — Master Q&A Bank
**Compiled by:** Senior Engineer + Senior Examiner perspective
**Strategy:** Every Q below mirrors *real BJIT-style* phrasing. Master these → top 1%.

> **How to use:** Read Q → try to answer aloud → check answer → mark anything you got <100% on for re-review. Don't just read passively.

---

# 📚 SECTION 1 — DATA STRUCTURES

### Q1.1 What is the difference between an Array and a Linked List?
| Aspect | Array | Linked List |
|---|---|---|
| Memory | Contiguous | Non-contiguous (nodes + pointers) |
| Access | O(1) random access by index | O(n) — must traverse |
| Insert/Delete at head | O(n) (shift) | O(1) |
| Insert/Delete at end | O(1) amortized (dynamic array) | O(n) without tail pointer, O(1) with |
| Memory overhead | None per element | Extra pointer per node |
| Cache friendliness | Excellent | Poor |
**When to use which:** Array when you need fast random access and size is known/stable. Linked list when frequent insert/delete at known positions.

### Q1.2 Explain Stack vs Queue with real-world examples.
- **Stack (LIFO — Last In First Out):** plate stack, browser back button, function call stack, undo operation.
- **Queue (FIFO — First In First Out):** ticket counter line, printer job queue, BFS traversal, OS process scheduling.

### Q1.3 What is a Circular Queue and why do we need it?
A queue where the last position connects back to the first. In a normal array-based queue, after several enqueue/dequeue operations, the front pointer moves forward and we **waste space** at the beginning. Circular queue reuses that space using `(rear + 1) % size`.

### Q1.4 What is a Doubly Linked List? Advantages over singly?
Each node has `prev` and `next` pointers.
**Advantages:** O(1) deletion if you have a pointer to the node, can traverse both directions.
**Disadvantage:** Extra memory for `prev` pointer.

### Q1.5 What is a Hash Table / HashMap? How does it work?
A data structure that maps keys → values using a **hash function** to compute an index into an array of buckets.
- Average: O(1) insert/lookup/delete
- Worst: O(n) when many collisions
- **Collision handling:** (1) Chaining (linked list at each bucket), (2) Open addressing (linear/quadratic probing)
- **Load factor** = entries / buckets. When > 0.75 typically, resize (rehash).

### Q1.6 Trees — Binary Tree vs Binary Search Tree (BST)?
- **Binary Tree:** each node has ≤ 2 children. No ordering rule.
- **BST:** for every node, left subtree values < node < right subtree values. Enables O(log n) search/insert/delete (when balanced).
- **Unbalanced BST worst case:** O(n) — becomes a linked list. Solution: self-balancing trees (AVL, Red-Black).

### Q1.7 What is a Heap?
A complete binary tree satisfying the **heap property**:
- **Min-heap:** parent ≤ children → root is minimum
- **Max-heap:** parent ≥ children → root is maximum
- Used in: Priority Queue, Heap Sort, Dijkstra's algorithm, finding top-K
- Operations: insert O(log n), extract-min/max O(log n), peek O(1)
- Usually implemented as an array: parent at `i`, children at `2i+1`, `2i+2`

### Q1.8 What is a Graph? Representations?
A set of vertices (V) and edges (E). Can be directed/undirected, weighted/unweighted, cyclic/acyclic.

| Representation | Space | Edge check | Use when |
|---|---|---|---|
| **Adjacency Matrix** | O(V²) | O(1) | Dense graphs |
| **Adjacency List** | O(V+E) | O(degree) | Sparse graphs (most cases) |

### Q1.9 What is a Trie?
A tree where each node represents a character. Used for prefix-based searches, autocomplete, spell-check, IP routing.
- Insert/Search a word of length L: O(L)
- Space: heavy (one node per char per word, but shared prefixes)

### Q1.10 Time complexity cheat sheet (MEMORIZE):
| Operation | Array | Linked List | Stack/Queue | Hash Table (avg) | BST (avg) | Heap |
|---|---|---|---|---|---|---|
| Access | O(1) | O(n) | O(n) | O(1) | O(log n) | O(1) peek |
| Search | O(n) | O(n) | O(n) | O(1) | O(log n) | O(n) |
| Insert | O(n) | O(1)* | O(1) | O(1) | O(log n) | O(log n) |
| Delete | O(n) | O(1)* | O(1) | O(1) | O(log n) | O(log n) |
*at known position

### Q1.11 Common DS interview trick Qs:
**Q:** Difference between `Array` and `ArrayList` (Java)?
**A:** Array = fixed size, can hold primitives. ArrayList = dynamic (auto-resizes), only objects, has methods like add/remove.

**Q:** Difference between `HashMap` and `HashTable`?
**A:** HashMap = not synchronized, allows 1 null key & multiple null values, faster. HashTable = synchronized (thread-safe), no nulls, slower (legacy).

**Q:** What's the difference between `Stack` (Java's) and `Deque`?
**A:** `Stack` extends `Vector` (legacy, synchronized). Prefer `ArrayDeque` for stack operations — faster and not legacy.

---

# 📚 SECTION 2 — ALGORITHMS

### Q2.1 Explain Binary Search.
Find target in **sorted** array by repeatedly halving the search range.
```python
def binary_search(arr, target):
    lo, hi = 0, len(arr) - 1
    while lo <= hi:
        mid = (lo + hi) // 2          # safer: lo + (hi - lo) // 2 to avoid overflow
        if arr[mid] == target: return mid
        elif arr[mid] < target: lo = mid + 1
        else: hi = mid - 1
    return -1
```
**Complexity:** O(log n) time, O(1) space.
**Common trap:** must be sorted! Off-by-one in `lo <= hi`.

### Q2.2 Lower bound and Upper bound (BJIT asked this!)
- **Lower bound:** smallest index `i` such that `arr[i] >= target`
- **Upper bound:** smallest index `i` such that `arr[i] > target`
- Count of `target` in sorted array = `upper_bound(t) - lower_bound(t)`

### Q2.3 Sorting algorithms comparison:
| Algorithm | Best | Avg | Worst | Space | Stable? |
|---|---|---|---|---|---|
| Bubble | O(n) | O(n²) | O(n²) | O(1) | Yes |
| Selection | O(n²) | O(n²) | O(n²) | O(1) | No |
| Insertion | O(n) | O(n²) | O(n²) | O(1) | Yes |
| **Merge** | O(n log n) | O(n log n) | O(n log n) | O(n) | Yes |
| **Quick** | O(n log n) | O(n log n) | **O(n²)** | O(log n) | No |
| Heap | O(n log n) | O(n log n) | O(n log n) | O(1) | No |
| Counting | O(n+k) | O(n+k) | O(n+k) | O(k) | Yes |

**Quick Sort worst case** happens when pivot is always smallest/largest (already sorted). Fix: random pivot or median-of-three.

### Q2.4 DFS vs BFS (BJIT asked DFS!)
**DFS (Depth-First Search):** Go deep, then backtrack. Uses **stack** (or recursion).
```python
def dfs(graph, node, visited):
    if node in visited: return
    visited.add(node)
    print(node)
    for neighbor in graph[node]:
        dfs(graph, neighbor, visited)
```
**BFS (Breadth-First Search):** Explore level by level. Uses **queue**.
```python
from collections import deque
def bfs(graph, start):
    visited, queue = {start}, deque([start])
    while queue:
        node = queue.popleft()
        print(node)
        for neighbor in graph[node]:
            if neighbor not in visited:
                visited.add(neighbor)
                queue.append(neighbor)
```
**Complexity:** Both O(V + E) time, O(V) space.
**Use DFS for:** topological sort, cycle detection, path existence.
**Use BFS for:** shortest path in **unweighted** graph, level-order traversal.

### Q2.5 Recursion vs Iteration?
- **Recursion:** function calls itself; needs base case; uses call stack (risk of stack overflow); often cleaner code.
- **Iteration:** loops; constant space (no call stack overhead); usually faster.
- Convert recursion → iteration using explicit stack.

### Q2.6 What is Dynamic Programming (DP)?
Solve problems by **breaking into overlapping subproblems** and storing results to avoid recomputation.
Two requirements: **(1) Optimal substructure**, **(2) Overlapping subproblems**.

**Approaches:**
- **Top-down (memoization):** recursion + cache
- **Bottom-up (tabulation):** iterative, fill a table

**Classic Fibonacci DP:**
```python
def fib(n):
    if n <= 1: return n
    dp = [0, 1]
    for i in range(2, n+1):
        dp.append(dp[i-1] + dp[i-2])
    return dp[n]
```

### Q2.7 Greedy vs DP?
- **Greedy:** make locally optimal choice at each step. Works when problem has greedy choice property (e.g., activity selection, Huffman coding, Dijkstra).
- **DP:** explore all subproblem solutions and combine. Use when greedy fails (e.g., 0/1 knapsack).

### Q2.8 Divide and Conquer?
1. **Divide** problem into smaller subproblems
2. **Conquer** each recursively
3. **Combine** results
Examples: Merge Sort, Quick Sort, Binary Search, closest pair of points.

### Q2.9 BJIT-style classic coding problems (PRACTICE BY HAND):

**Problem 1: Left rotate array by k (real BJIT past question)**
Input: `[1,2,3,4,5,6,7,8]`, k=3 → Output: `[4,5,6,7,8,1,2,3]`
```python
def rotate_left(arr, k):
    n = len(arr)
    k = k % n
    # Reversal trick: reverse(0,k-1), reverse(k,n-1), reverse(0,n-1)
    arr[:k] = arr[:k][::-1]
    arr[k:] = arr[k:][::-1]
    arr.reverse()
    return arr
```
**Complexity:** O(n) time, O(1) extra space.

**Problem 2: Move zeros to end, preserve order of non-zeros (real BJIT past)**
Input: `[1,0,2,-4,0,5,0,11]` → Output: `[1,2,-4,5,11,0,0,0]`
```python
def move_zeros(arr):
    write = 0
    for read in range(len(arr)):
        if arr[read] != 0:
            arr[write] = arr[read]
            write += 1
    while write < len(arr):
        arr[write] = 0
        write += 1
    return arr
```
**Complexity:** O(n) time, O(1) space. **Two-pointer technique.**

**Problem 3: Reverse a linked list**
```python
def reverse_ll(head):
    prev, curr = None, head
    while curr:
        nxt = curr.next
        curr.next = prev
        prev = curr
        curr = nxt
    return prev
```

**Problem 4: Detect cycle in linked list (Floyd's algorithm)**
```python
def has_cycle(head):
    slow = fast = head
    while fast and fast.next:
        slow = slow.next
        fast = fast.next.next
        if slow == fast: return True
    return False
```

**Problem 5: Check balanced parentheses**
```python
def is_balanced(s):
    stack, pairs = [], {')':'(', '}':'{', ']':'['}
    for c in s:
        if c in '({[': stack.append(c)
        elif c in ')}]':
            if not stack or stack.pop() != pairs[c]: return False
    return not stack
```

**Problem 6: Find duplicates in array (Floyd's tortoise & hare on array)**
```python
def find_duplicate(nums):  # nums has n+1 elements in [1,n]
    slow = fast = nums[0]
    while True:
        slow = nums[slow]
        fast = nums[nums[fast]]
        if slow == fast: break
    slow = nums[0]
    while slow != fast:
        slow, fast = nums[slow], nums[fast]
    return slow
```

**Problem 7: Maximum subarray (Kadane's algorithm)**
```python
def max_subarray(arr):
    cur = best = arr[0]
    for x in arr[1:]:
        cur = max(x, cur + x)
        best = max(best, cur)
    return best
```

**Problem 8: Longest substring without repeating chars (sliding window)**
```python
def longest_unique(s):
    seen, left, best = {}, 0, 0
    for right, c in enumerate(s):
        if c in seen and seen[c] >= left:
            left = seen[c] + 1
        seen[c] = right
        best = max(best, right - left + 1)
    return best
```

---

# 📚 SECTION 3 — PROGRAMMING

### Q3.1 Compiled vs Interpreted languages?
- **Compiled:** source → machine code before running (C, C++, Rust). Faster execution, slower dev cycle.
- **Interpreted:** executed line-by-line at runtime (Python, JavaScript). Slower, more flexible.
- **Hybrid:** Java (bytecode → JVM), C# (IL → CLR).

### Q3.2 Pass by value vs pass by reference?
- **Pass by value:** copy of the argument is passed. Changes inside function don't affect original.
- **Pass by reference:** reference/address is passed. Changes affect original.
- **Java:** technically always pass by value, but **object references are passed by value** — so you can mutate the object but not reassign it.
- **Python:** "pass by object reference" — same idea; mutable objects (list, dict) can be modified in place.

### Q3.3 What is a memory leak? (asked at BJIT)
Memory that's allocated but never freed even though it's no longer needed.
- **C/C++:** forgot to `free()`/`delete` after `malloc()`/`new`
- **Java:** objects still referenced (e.g., static collections growing forever, unclosed streams, listener not removed) — GC can't reclaim them
- **Detection:** profilers (VisualVM, Valgrind), heap dumps
- **Prevention:** RAII (C++), try-with-resources (Java), proper listener removal

### Q3.4 Stack vs Heap memory?
| Stack | Heap |
|---|---|
| Stores: local variables, function call frames | Stores: dynamically allocated objects |
| Fast allocation (move pointer) | Slower (allocator) |
| Auto-cleaned on function return | Manual or GC |
| Small, fixed size | Large |
| Stack overflow = too many frames | Heap fragmentation possible |

### Q3.5 What is Garbage Collection?
Automatic memory management — runtime frees unused objects. Languages: Java, C#, Python, Go.
**Common algorithms:** Mark-and-Sweep, Reference Counting (Python uses this + GC for cycles), Generational GC (Java).

### Q3.6 Difference between `==` and `equals()` in Java?
- `==` compares **references** (memory addresses) for objects, **values** for primitives.
- `.equals()` compares **content** (when overridden, e.g., String).
```java
String a = new String("hi");
String b = new String("hi");
a == b        // false (different objects)
a.equals(b)   // true  (same content)
```

### Q3.7 What is `final` / `static` / `const`?
- **`final` (Java):** variable can't be reassigned; method can't be overridden; class can't be subclassed.
- **`static`:** belongs to the class, not instance. One copy shared by all instances.
- **`const` (C++):** value can't change.

### Q3.8 What is `try-catch-finally`?
- `try`: code that might throw
- `catch`: handles exception
- `finally`: **always runs** (even if exception or return) — used for cleanup (close files, connections)
- **Java 7+ try-with-resources:** auto-closes resources implementing `AutoCloseable`

### Q3.9 Checked vs Unchecked exceptions (Java)?
- **Checked:** must be declared/handled (IOException, SQLException). Compile-time check.
- **Unchecked (Runtime):** NullPointerException, ArrayIndexOutOfBounds, ArithmeticException. Not forced to handle.

### Q3.10 What is multithreading? Race condition? Deadlock?
- **Multithreading:** running multiple threads concurrently within a process.
- **Race condition:** outcome depends on thread scheduling; multiple threads modify shared data without sync.
- **Deadlock:** two+ threads waiting on each other forever. **Conditions (Coffman's):** mutual exclusion, hold-and-wait, no preemption, circular wait.
- **Solutions:** locks/mutex, synchronized blocks, semaphores, lock ordering, timeouts.

### Q3.11 What is async/await? (BJIT asked this!)
Syntactic sugar for promises/futures to write asynchronous code that looks synchronous.
- `async` marks a function that returns a Promise/Task
- `await` pauses execution until promise resolves, without blocking the thread
```javascript
async function getData() {
    const res = await fetch(url);
    const data = await res.json();
    return data;
}
```
Underneath: state machine + event loop / scheduler.

### Q3.12 Shallow copy vs Deep copy?
- **Shallow:** new object, but inner references point to same objects. Changes to inner affect both.
- **Deep:** recursive copy — completely independent.

### Q3.13 What is recursion's space complexity?
O(depth of recursion) due to call stack — even if "no extra data structures" are used. Tail recursion can be optimized to O(1) in some languages (not Python/Java).

---

# 📚 SECTION 4 — OBJECT-ORIENTED PROGRAMMING (HIGH-YIELD!)

### Q4.1 What are the 4 pillars of OOP? (must memorize)
1. **Encapsulation** — bundle data + methods, hide internal state (private fields + public getters/setters)
2. **Inheritance** — child class inherits properties/methods from parent (code reuse)
3. **Polymorphism** — same interface, different behavior. Two types:
   - **Compile-time (overloading)**
   - **Runtime (overriding)**
4. **Abstraction** — show essential features, hide complexity (abstract classes, interfaces)

### Q4.2 Overloading vs Overriding (THEY WILL TRY TO CONFUSE YOU)
| Aspect | Overloading | Overriding |
|---|---|---|
| When resolved | **Compile time** | **Runtime** |
| Where | Same class | Subclass redefines parent method |
| Signature | **Different** parameters | **Same** signature |
| Return type | Can differ (with params differ) | Same (or covariant) |
| Access modifier | Any | Cannot be more restrictive |
| Static methods | Can be overloaded | **Cannot be overridden** (hidden) |
| Private/final | Allowed | Cannot override |
| Polymorphism type | Static (ad-hoc) | Dynamic |

**Trick Q:** "Can you override a static method?" → **No**, you can only hide it. The call is resolved at compile time based on the reference type.

### Q4.3 IS-A vs HAS-A relationship?
- **IS-A:** Inheritance — `Dog IS-A Animal` → `class Dog extends Animal`
- **HAS-A:** Composition — `Car HAS-A Engine` → `class Car { Engine engine; }`
- **Principle:** "**Favor composition over inheritance**" — composition is more flexible, avoids tight coupling, doesn't break encapsulation.

### Q4.4 Abstract Class vs Interface?
| Feature | Abstract Class | Interface |
|---|---|---|
| Methods | Can have implemented + abstract | All abstract (pre-Java 8); Java 8+ allows `default` and `static` methods |
| Fields | Can have any field | Only `public static final` (constants) |
| Constructor | Yes | No |
| Multiple inheritance | No (single inheritance) | Yes (a class can implement many interfaces) |
| `extends` vs `implements` | extends | implements |
| Use when | Closely related classes sharing common state/behavior | Define a contract; unrelated classes can implement |

**Real-world:** `Animal` abstract class (with shared fields like `name`), `Swimmable` interface (any class that swims).

### Q4.5 Access Modifiers (Java):
| Modifier | Same class | Same package | Subclass (diff pkg) | Anywhere |
|---|---|---|---|---|
| `private` | ✅ | ❌ | ❌ | ❌ |
| (default/package) | ✅ | ✅ | ❌ | ❌ |
| `protected` | ✅ | ✅ | ✅ | ❌ |
| `public` | ✅ | ✅ | ✅ | ✅ |

### Q4.6 What is `this` and `super`?
- **`this`:** reference to current instance. Used to disambiguate (`this.x = x`), call another constructor (`this(args)`).
- **`super`:** reference to parent class. Used to call parent constructor (`super(args)`), parent method (`super.method()`).

### Q4.7 Constructor chaining?
Calling one constructor from another (same class via `this()`, parent via `super()`). Must be **first statement** in the constructor. If you don't call `super()`, compiler inserts implicit `super()` (no-arg).

### Q4.8 Why no multiple inheritance in Java?
**Diamond problem:** if class D extends both B and C, and both override method from A, which version does D inherit? Java avoids this by allowing only single inheritance for classes but multiple interface implementation (Java 8+ default methods resolve diamond explicitly).

### Q4.9 SOLID Principles (be ready to name + explain all 5):
1. **S — Single Responsibility:** a class should have one reason to change.
2. **O — Open/Closed:** open for extension, closed for modification (use interfaces/inheritance).
3. **L — Liskov Substitution:** subclasses must be substitutable for their base class without breaking behavior.
4. **I — Interface Segregation:** many small focused interfaces > one fat interface.
5. **D — Dependency Inversion:** depend on abstractions, not concretions. (High-level modules shouldn't depend on low-level; both depend on interfaces.)

### Q4.10 Encapsulation example in code?
```java
public class BankAccount {
    private double balance;          // hidden
    public double getBalance() { return balance; }
    public void deposit(double amt) {
        if (amt > 0) balance += amt;   // controlled access
    }
}
```

### Q4.11 Method overloading examples:
```java
class Calc {
    int add(int a, int b) { return a+b; }
    double add(double a, double b) { return a+b; }
    int add(int a, int b, int c) { return a+b+c; }   // different # params
}
```

### Q4.12 Method overriding example:
```java
class Animal { void sound() { System.out.println("generic"); } }
class Dog extends Animal {
    @Override void sound() { System.out.println("Bark"); }
}
Animal a = new Dog();
a.sound();   // "Bark" — runtime polymorphism
```

### Q4.13 What is `instanceof`?
Tests if an object is an instance of a specific class/interface.
```java
if (a instanceof Dog) { Dog d = (Dog) a; }
```

### Q4.14 Difference between Composition and Aggregation?
- **Composition:** strong "has-a"; child can't exist without parent. (House HAS-A Room — destroy house, rooms gone.)
- **Aggregation:** weak "has-a"; child can exist independently. (Department HAS-A Professors — close department, professors still exist.)

### Q4.15 What is Coupling and Cohesion?
- **Coupling:** how dependent modules are on each other. **Aim: low coupling.**
- **Cohesion:** how focused a module's responsibilities are. **Aim: high cohesion.**

---

# 📚 SECTION 5 — DESIGN PATTERNS

### Q5.1 What is a Design Pattern?
A reusable, proven solution to a commonly recurring problem in software design. **Not** code — a template.

**3 categories (GoF):**
- **Creational:** Singleton, Factory, Abstract Factory, Builder, Prototype
- **Structural:** Adapter, Decorator, Facade, Proxy, Composite, Bridge, Flyweight
- **Behavioral:** Observer, Strategy, Command, Iterator, State, Template Method, Chain of Responsibility, Visitor, Mediator

### Q5.2 Singleton pattern — code by heart:
```java
public class Singleton {
    private static volatile Singleton instance;
    private Singleton() {}                            // private constructor

    public static Singleton getInstance() {
        if (instance == null) {                       // double-checked locking
            synchronized (Singleton.class) {
                if (instance == null) {
                    instance = new Singleton();
                }
            }
        }
        return instance;
    }
}
```
**Use:** logger, DB connection pool, config, cache.
**Drawbacks:** global state (hard to test), hidden dependencies, thread-safety overhead.

### Q5.3 Factory Pattern?
Creates objects without exposing the instantiation logic.
```java
interface Shape { void draw(); }
class Circle implements Shape { public void draw() { ... } }
class Square implements Shape { public void draw() { ... } }

class ShapeFactory {
    public Shape getShape(String type) {
        if ("circle".equals(type)) return new Circle();
        if ("square".equals(type)) return new Square();
        return null;
    }
}
```
**Use:** when creation logic is complex or depends on input.

### Q5.4 Observer Pattern?
One-to-many: when subject changes, all observers are notified.
- **Subject:** maintains list of observers, has `attach`, `detach`, `notify`
- **Observer:** has `update()` method
**Example:** event listeners (button clicks), pub/sub systems, model-view in MVC.

### Q5.5 Strategy Pattern?
Define a family of algorithms, encapsulate each, make them interchangeable at runtime.
```java
interface PaymentStrategy { void pay(int amount); }
class CreditCard implements PaymentStrategy { ... }
class PayPal implements PaymentStrategy { ... }
class Cart {
    private PaymentStrategy strategy;
    void setStrategy(PaymentStrategy s) { this.strategy = s; }
    void checkout(int amt) { strategy.pay(amt); }
}
```
**Use:** choose algorithm at runtime (sorting strategy, payment, compression).

### Q5.6 Decorator Pattern?
Add new behavior to objects dynamically without altering their structure.
**Example:** Java I/O — `new BufferedReader(new InputStreamReader(new FileInputStream("f")))`.

### Q5.7 Adapter Pattern?
Convert interface of a class into another interface the client expects.
**Example:** plug adapter; wrapping a legacy API.

### Q5.8 Facade Pattern?
Provide a simplified interface to a complex subsystem.
**Example:** `JDBCTemplate` hiding all JDBC complexity.

### Q5.9 Proxy Pattern?
Provide a placeholder for another object to control access (security, lazy loading, logging, remote access).

### Q5.10 MVC architecture?
- **Model:** data + business logic
- **View:** UI
- **Controller:** handles user input, updates model, selects view
- **Benefit:** separation of concerns, easier testing & maintenance.

### Q5.11 Repository Pattern?
Mediates between domain and data mapping. Encapsulates DB access. Used heavily in Spring, .NET.

### Q5.12 Dependency Injection (DI)?
Provide dependencies from outside instead of creating them inside the class.
- **Constructor injection** (preferred), setter injection, interface injection.
- **Benefit:** loose coupling, easier testing (mock dependencies).
```java
class Service {
    private final Repo repo;
    Service(Repo repo) { this.repo = repo; }   // injected
}
```

---

# 📚 SECTION 6 — DATABASE

### Q6.1 SQL vs NoSQL?
| | SQL | NoSQL |
|---|---|---|
| Schema | Fixed, predefined | Flexible / schema-less |
| Structure | Tables (rows/columns) | Documents/key-value/column/graph |
| Scaling | Vertical (mostly) | Horizontal |
| ACID | Strong | Often eventual consistency (BASE) |
| Examples | MySQL, PostgreSQL, Oracle | MongoDB, Redis, Cassandra, Neo4j |
| Use when | Structured data, complex queries, transactions | Big data, rapid scale, unstructured data |

### Q6.2 ACID properties (must memorize):
- **A — Atomicity:** transaction is all-or-nothing
- **C — Consistency:** DB moves from one valid state to another
- **I — Isolation:** concurrent transactions don't interfere
- **D — Durability:** committed data persists (even after crash)

### Q6.3 Normalization (1NF → BCNF):
- **1NF:** atomic values (no repeating groups, no arrays in a cell)
- **2NF:** 1NF + no **partial dependency** (non-key attrib must depend on whole PK)
- **3NF:** 2NF + no **transitive dependency** (non-key shouldn't depend on another non-key)
- **BCNF:** 3NF + every determinant is a candidate key
- **Why normalize?** reduce redundancy, avoid update anomalies
- **Denormalization:** sometimes done for read performance (data warehouses)

### Q6.4 SQL JOINs:
- **INNER JOIN:** rows matching in both tables
- **LEFT (OUTER) JOIN:** all from left + matching from right (NULL if no match)
- **RIGHT JOIN:** mirror of LEFT
- **FULL OUTER:** all rows from both (NULL where no match)
- **CROSS JOIN:** Cartesian product
- **SELF JOIN:** join table with itself (e.g., employee-manager)

### Q6.5 Practical SQL queries (PRACTICE WRITING):

**Q:** Find 2nd highest salary
```sql
SELECT MAX(salary) FROM Employees
WHERE salary < (SELECT MAX(salary) FROM Employees);

-- or using LIMIT (MySQL):
SELECT DISTINCT salary FROM Employees
ORDER BY salary DESC LIMIT 1 OFFSET 1;

-- or DENSE_RANK:
SELECT salary FROM (
    SELECT salary, DENSE_RANK() OVER (ORDER BY salary DESC) rnk
    FROM Employees
) t WHERE rnk = 2;
```

**Q:** Highest-paid employee per department
```sql
SELECT e.name, e.dept_id, e.salary
FROM Employees e
WHERE e.salary = (
    SELECT MAX(salary) FROM Employees WHERE dept_id = e.dept_id
);
```

**Q:** Find duplicate emails
```sql
SELECT email, COUNT(*) FROM Users
GROUP BY email HAVING COUNT(*) > 1;
```

**Q:** Department with most employees
```sql
SELECT dept_id, COUNT(*) cnt FROM Employees
GROUP BY dept_id ORDER BY cnt DESC LIMIT 1;
```

**Q:** Employees who never made a sale (LEFT JOIN trick)
```sql
SELECT e.name FROM Employees e
LEFT JOIN Sales s ON e.id = s.emp_id
WHERE s.id IS NULL;
```

### Q6.6 Primary key vs Unique key vs Foreign key?
- **Primary key:** uniquely identifies a row. Cannot be NULL. One per table.
- **Unique key:** unique values, can have one NULL. Multiple per table.
- **Foreign key:** references PK of another table — enforces referential integrity.

### Q6.7 What is an Index?
A data structure (often B-tree or hash) that speeds up data retrieval.
- **Pros:** much faster SELECT
- **Cons:** slows INSERT/UPDATE/DELETE; uses extra space
- **Types:** clustered (one per table; data physically ordered by it), non-clustered (separate structure pointing to rows), composite (multi-column)

### Q6.8 DELETE vs TRUNCATE vs DROP?
| | DELETE | TRUNCATE | DROP |
|---|---|---|---|
| Removes | Specific rows (WHERE clause) | All rows | Entire table (structure + data) |
| Type | DML | DDL | DDL |
| Rollback | Yes (in transaction) | Usually No | No |
| Speed | Slow (logs each row) | Fast | Fastest |
| Triggers | Fires | Doesn't | N/A |

### Q6.9 GROUP BY vs HAVING vs WHERE?
- **WHERE:** filters rows **before** grouping
- **GROUP BY:** groups rows sharing a value
- **HAVING:** filters groups **after** aggregation
```sql
SELECT dept_id, COUNT(*) FROM Emp
WHERE salary > 30000              -- before
GROUP BY dept_id
HAVING COUNT(*) > 5;              -- after
```

### Q6.10 What is a Transaction? Isolation levels?
A unit of work that is treated atomically.
**Isolation levels (lowest → highest):**
1. **READ UNCOMMITTED** — dirty reads possible
2. **READ COMMITTED** — no dirty reads (Postgres default)
3. **REPEATABLE READ** — no dirty, no non-repeatable (MySQL default)
4. **SERIALIZABLE** — strictest, like running serially
**Trade-off:** higher isolation → lower concurrency.

### Q6.11 What is a View / Stored Procedure / Trigger?
- **View:** virtual table from a query. No physical storage. Simplifies complex queries, security layer.
- **Stored Procedure:** precompiled SQL stored on server. Called by name with params. Encapsulates business logic.
- **Trigger:** auto-executes on event (INSERT/UPDATE/DELETE). E.g., audit log on row change.

### Q6.12 CAP Theorem (NoSQL context)?
In a distributed system, you can only guarantee 2 of 3:
- **C — Consistency:** all nodes see same data
- **A — Availability:** every request gets a response
- **P — Partition tolerance:** system works despite network failures
In practice: P is mandatory → you choose between C and A.

---

# 📚 SECTION 7 — AI FUNDAMENTALS (YOUR EDGE — MEMORIZE COLD)

### Q7.1 What is Artificial Intelligence vs Machine Learning vs Deep Learning?
- **AI:** broad field — machines mimicking intelligent behavior.
- **ML:** subset of AI — algorithms that learn patterns from data without being explicitly programmed.
- **DL:** subset of ML — uses neural networks with many layers.

### Q7.2 Types of Machine Learning?
1. **Supervised:** labeled data (input → output). Tasks: classification (discrete), regression (continuous). E.g., spam detection, house price prediction.
2. **Unsupervised:** no labels. Tasks: clustering (K-means), dimensionality reduction (PCA), anomaly detection.
3. **Semi-supervised:** small labeled + large unlabeled.
4. **Reinforcement Learning:** agent learns by interacting with environment, receives rewards. E.g., AlphaGo, robotics, game AI.

### Q7.3 Classification vs Regression?
- **Classification:** output is **discrete categories** (spam/not spam, cat/dog).
- **Regression:** output is **continuous numeric** (price, temperature).

### Q7.4 What is overfitting? Underfitting? How to detect & fix? (HIGH-VALUE Q)
- **Overfitting:** model fits training data too well, fails on new data. **High variance, low bias.** Train acc ↑, Test acc ↓.
- **Underfitting:** model too simple to capture pattern. **High bias, low variance.** Both train & test acc low.

**Fixes for overfitting:**
1. More training data
2. Reduce model complexity (fewer features/parameters)
3. **Regularization** (L1 Lasso, L2 Ridge) — penalize large weights
4. **Dropout** (neural nets)
5. **Cross-validation**
6. **Early stopping**
7. Data augmentation (especially for images)
8. Ensembling

**Fixes for underfitting:**
1. More complex model
2. Add features / better feature engineering
3. Reduce regularization
4. Train longer

### Q7.5 Bias-Variance Tradeoff?
- **Bias:** error from wrong assumptions (underfitting)
- **Variance:** error from sensitivity to training data (overfitting)
- **Total error = Bias² + Variance + Irreducible error**
- Goal: find the sweet spot where total error is minimized.

### Q7.6 Train / Validation / Test split — why three?
- **Train:** model learns weights
- **Validation:** tune hyperparameters, pick best model
- **Test:** final unbiased evaluation (touch only once!)
- Typical: 70/15/15 or 80/10/10.
- **Cross-validation (k-fold):** split into k folds, train on k-1, validate on 1, rotate. Maximizes data use.

### Q7.7 Evaluation metrics — Classification (memorize formulas!):

**Confusion matrix:**
|  | Predicted Positive | Predicted Negative |
|---|---|---|
| **Actual Positive** | TP | FN |
| **Actual Negative** | FP | TN |

- **Accuracy** = (TP + TN) / (TP + TN + FP + FN) — bad for imbalanced classes
- **Precision** = TP / (TP + FP) — "of my positive predictions, how many were right"
- **Recall (Sensitivity, TPR)** = TP / (TP + FN) — "of actual positives, how many did I catch"
- **F1-score** = 2 · (P·R) / (P+R) — harmonic mean
- **Specificity (TNR)** = TN / (TN + FP)
- **ROC curve:** TPR vs FPR at various thresholds. **AUC:** area under ROC; 1.0 = perfect, 0.5 = random.

**When to prefer Precision vs Recall:**
- **High precision needed:** spam filter (don't lose good email)
- **High recall needed:** cancer detection (don't miss a case)

### Q7.8 Evaluation metrics — Regression:
- **MAE (Mean Absolute Error):** average |actual − predicted|
- **MSE:** average (actual − predicted)² — penalizes big errors more
- **RMSE:** √MSE — same units as target
- **R² (coefficient of determination):** 1 − SS_res/SS_tot — proportion of variance explained; 1 = perfect, 0 = predicting mean

### Q7.9 Gradient Descent — explain in detail.
Optimization algorithm to minimize a loss function by iteratively moving in the direction of steepest descent.
- Update rule: **θ = θ − η · ∇L(θ)**
  where η = learning rate, ∇L = gradient of loss w.r.t. parameters
- Too large η → diverges; too small → slow convergence

**Variants:**
- **Batch GD:** uses all data per step. Accurate but slow.
- **Stochastic GD (SGD):** one example per step. Noisy but fast.
- **Mini-batch GD:** small batch (e.g., 32) per step. **Most common.**
- **Momentum, RMSProp, Adam:** advanced optimizers with adaptive learning rates.

### Q7.10 Cost / Loss functions?
- **Regression:** MSE, MAE, Huber loss
- **Binary classification:** Binary cross-entropy / log loss
- **Multi-class:** Categorical cross-entropy
- **Why not accuracy as a loss?** Not differentiable.

### Q7.11 Key ML algorithms — one-liners:

| Algorithm | Type | Idea | Use case |
|---|---|---|---|
| **Linear Regression** | Supervised, regression | Fit straight line y = wx + b minimizing MSE | Price prediction |
| **Logistic Regression** | Supervised, classification | Linear + sigmoid → probability | Binary classification |
| **K-Nearest Neighbors** | Supervised | Predict by majority of K nearest points | Recommendation |
| **Decision Tree** | Supervised | Split on feature that maximizes info gain (Gini/Entropy) | Interpretable models |
| **Random Forest** | Supervised, ensemble | Many trees, bagging + feature randomness | General-purpose |
| **Gradient Boosting (XGBoost)** | Supervised, ensemble | Sequentially fix errors of previous tree | Tabular data king |
| **SVM** | Supervised | Find hyperplane with max margin | Small/medium datasets |
| **Naive Bayes** | Supervised | Bayes theorem + feature independence assumption | Text classification |
| **K-Means** | Unsupervised | Iteratively assign points to nearest centroid | Customer segmentation |
| **DBSCAN** | Unsupervised | Density-based clustering | Arbitrary-shape clusters, outliers |
| **PCA** | Unsupervised | Project data onto top variance directions | Dimensionality reduction |

### Q7.12 Neural Network basics:
- **Neuron:** computes `output = activation(Σ wᵢxᵢ + b)`
- **Layers:** input → hidden(s) → output
- **Forward propagation:** compute output
- **Backpropagation:** compute gradients of loss w.r.t. weights using chain rule, then update via gradient descent
- **Epoch:** one full pass over training data
- **Batch size:** examples per gradient update
- **Iteration:** one batch update

### Q7.13 Activation functions:
- **Sigmoid:** σ(x) = 1/(1+e⁻ˣ); range (0,1); used in binary output. Problem: vanishing gradient.
- **Tanh:** range (-1, 1); zero-centered.
- **ReLU:** max(0, x); **most popular**; fast, mitigates vanishing gradient. Problem: dying ReLU.
- **Leaky ReLU:** small slope for x<0 to fix dying ReLU.
- **Softmax:** converts logits to probabilities summing to 1; multi-class output layer.

### Q7.14 CNN vs RNN vs Transformer?
- **CNN (Convolutional NN):** for images. Uses convolution + pooling. Captures spatial features.
- **RNN/LSTM/GRU:** for sequences (text, time series). Maintains hidden state. LSTM/GRU fix vanishing gradient.
- **Transformer:** for sequences using **self-attention** (no recurrence). Parallelizable. Basis of GPT, BERT, etc.

### Q7.15 What is Attention / Self-Attention (1-line)?
A mechanism that lets the model weigh the importance of different input parts when producing each output element. Self-attention: every element attends to every other element in the same sequence.

### Q7.16 Feature engineering vs Feature selection?
- **Engineering:** creating new features from raw data (e.g., extracting day-of-week from timestamp).
- **Selection:** picking the most relevant subset of existing features (e.g., via correlation, mutual info, L1 regularization).

### Q7.17 Normalization vs Standardization?
- **Normalization (Min-Max):** scale to [0,1]: `(x - min)/(max - min)`. Sensitive to outliers.
- **Standardization (Z-score):** mean 0, std 1: `(x - μ)/σ`. Better for outliers.
- **Why?** Many algorithms (KNN, SVM, NN, gradient descent) work better when features are on similar scale.

### Q7.18 One-hot encoding vs Label encoding?
- **Label encoding:** category → integer (Red=0, Green=1, Blue=2). Implies false ordering.
- **One-hot:** binary column per category. No false ordering. Increases dimensionality.

### Q7.19 What is regularization (L1 vs L2)?
- **L1 (Lasso):** adds λΣ|w| to loss. Drives some weights to **0** → feature selection.
- **L2 (Ridge):** adds λΣw². Shrinks weights but rarely zero. Smoother solutions.
- **Elastic Net:** combines both.

### Q7.20 What is the curse of dimensionality?
As # features increases, data becomes sparse, distances lose meaning, more data needed exponentially. Solutions: PCA, feature selection.

### Q7.21 Generative vs Discriminative models?
- **Discriminative:** model P(y|x) directly (logistic regression, SVM, neural nets).
- **Generative:** model P(x, y), can generate new samples (Naive Bayes, GANs, VAEs, LLMs).

### Q7.22 What is transfer learning?
Reuse a model pre-trained on a large dataset (e.g., ImageNet) for a new task with smaller data. Freeze early layers, fine-tune later ones.

### Q7.23 What is an LLM? Brief.
**Large Language Model** — a transformer-based neural net trained on massive text corpora to predict next tokens. Examples: GPT, Claude, LLaMA. Capable of text generation, summarization, Q&A, code, reasoning.

### Q7.24 What is data leakage?
When info from outside the training set sneaks into training (e.g., using future data, or test data statistics for normalization). Causes overly optimistic metrics that don't generalize.

### Q7.25 Imbalanced datasets — how to handle?
- **Resampling:** oversample minority (SMOTE), undersample majority
- **Class weights:** penalize errors on minority more
- **Right metric:** F1, ROC-AUC, PR-AUC (not accuracy)
- **Threshold tuning**
- Anomaly-detection framing

---

# 📚 SECTION 8 — MATH / STATISTICS

### Q8.1 Mean, Median, Mode — when to use which?
- **Mean:** arithmetic average. Sensitive to outliers.
- **Median:** middle value. Robust to outliers (use for income, house prices).
- **Mode:** most frequent. Used for categorical data.

### Q8.2 Variance and Standard Deviation?
- **Variance:** σ² = Σ(xᵢ − μ)² / N — average squared deviation from mean
- **Std Dev:** σ = √variance — same units as data
- Higher = more spread

### Q8.3 Probability — basic rules:
- 0 ≤ P(A) ≤ 1
- P(A or B) = P(A) + P(B) − P(A and B)
- If independent: P(A and B) = P(A) · P(B)
- If mutually exclusive: P(A and B) = 0
- Conditional: P(A | B) = P(A and B) / P(B)

### Q8.4 Bayes' Theorem — formula + classic problem:
**P(A|B) = P(B|A) · P(A) / P(B)**

**Classic Q:** A test is 99% accurate for a disease that affects 1 in 10,000. You test positive. What's the chance you have it?
- P(D) = 0.0001, P(¬D) = 0.9999
- P(+|D) = 0.99, P(+|¬D) = 0.01 (false positive rate)
- P(+) = P(+|D)·P(D) + P(+|¬D)·P(¬D) = 0.99·0.0001 + 0.01·0.9999 ≈ 0.0101
- **P(D|+) = 0.99·0.0001 / 0.0101 ≈ 0.0098 ≈ 0.98%**
- **Insight:** even with 99% accurate test, if disease is rare, positive result is mostly a false positive!

### Q8.5 Permutations vs Combinations?
- **Permutation (order matters):** nPr = n! / (n−r)!
- **Combination (order doesn't):** nCr = n! / (r!(n−r)!)

**Examples:**
- Arrange 3 of 5 books on shelf: 5P3 = 60
- Choose 3 of 5 books to read: 5C3 = 10

### Q8.6 Expected Value?
E[X] = Σ xᵢ · P(xᵢ)
**Example:** Roll a fair die: E = (1+2+3+4+5+6)/6 = 3.5

### Q8.7 Normal Distribution — 68-95-99.7 rule:
- 68% of data within 1σ of mean
- 95% within 2σ
- 99.7% within 3σ
- Bell-shaped, symmetric.

### Q8.8 Central Limit Theorem?
The sampling distribution of the sample mean approaches a **normal distribution** as sample size grows, regardless of the population's distribution. Foundation of inferential statistics.

### Q8.9 Type I vs Type II error?
- **Type I (α, False Positive):** reject H₀ when it's true. ("Convict innocent.")
- **Type II (β, False Negative):** fail to reject H₀ when it's false. ("Free guilty.")
- **Power = 1 − β**

### Q8.10 P-value? Hypothesis testing?
- **H₀ (null):** default assumption (no effect)
- **H₁ (alternative):** what you're trying to prove
- **P-value:** probability of observing data as extreme as yours, **assuming H₀ is true**
- **If p < α (typically 0.05):** reject H₀

### Q8.11 Correlation vs Causation?
- **Correlation:** variables move together. r ∈ [−1, 1].
- **Causation:** one causes the other.
- **Correlation does NOT imply causation** (confounding variables possible).

### Q8.12 Linear Algebra essentials for AI:

**Vectors:** ordered list of numbers. Dot product: a·b = Σ aᵢbᵢ
**Matrix multiplication:** (m×n) · (n×p) = (m×p). NOT commutative: AB ≠ BA generally.
**Identity matrix I:** AI = IA = A.
**Transpose Aᵀ:** flip rows/cols.
**Inverse A⁻¹:** AA⁻¹ = I (exists only if det ≠ 0).
**Eigenvalue/Eigenvector:** Av = λv. v is unchanged in direction by A; scaled by λ. Used in PCA, spectral methods.

### Q8.13 Derivatives — why they matter for AI?
- Derivative = instantaneous rate of change = slope
- **Gradient** ∇f = vector of partial derivatives
- Gradient descent uses **−∇f** to move toward minimum
- Chain rule: (f∘g)'(x) = f'(g(x))·g'(x) — basis of backpropagation

### Q8.14 Logarithm properties (useful):
- log(ab) = log(a) + log(b)
- log(a/b) = log(a) − log(b)
- log(aⁿ) = n·log(a)
- log_b(x) = ln(x) / ln(b)
- Used in: log-likelihood, cross-entropy, big-O complexity, information theory

### Q8.15 Entropy & Information Gain (Decision Trees):
- **Entropy:** H = −Σ pᵢ log₂(pᵢ); measures disorder; 0 = pure, 1 = max uncertainty for binary
- **Information Gain:** entropy before split − weighted entropy after split. Decision tree splits on feature with max gain.
- **Gini impurity:** 1 − Σ pᵢ² — alternative to entropy; faster to compute.

---

# 📚 SECTION 9 — ANALYTICAL / IQ / PUZZLES

### Q9.1 25 horses, 5 tracks, find top 3. Minimum races?
**Answer: 7 races.**
1. Race all 25 in groups of 5 → **5 races**. Rank within each group.
2. Race the 5 winners → **1 race (race 6)**. Now we know overall #1 and which groups have which rankings.
3. Eliminate horses that can't be top 3:
   - From group of loser-of-race-6: all 5 out
   - From group of 4th in race 6: all 5 out
   - From group of 3rd in race 6: 2nd-5th out (only winner of that group could be top 3)
   - From group of 2nd in race 6: 3rd-5th out (only top 2)
   - From group of 1st in race 6: 4th-5th out (top 3 are candidates), but #1 already crowned
4. **Race 7:** the 5 remaining candidates → determines 2nd and 3rd.

### Q9.2 3 bulbs, 3 switches, one room visit.
- Turn ON switch 1 for 5 minutes, then OFF.
- Turn ON switch 2. Leave switch 3 OFF.
- Enter room: **bulb that is ON** → switch 2. **OFF but warm** → switch 1. **OFF and cold** → switch 3.

### Q9.3 4 people cross bridge with 1 torch, max 2 at a time. Times: 1, 2, 5, 10 min. Minimum total?
**Answer: 17 min.**
- 1 & 2 cross → 2 min. 1 returns → 1 min. (Total 3)
- 5 & 10 cross → 10 min. 2 returns → 2 min. (Total 15)
- 1 & 2 cross → 2 min. (Total **17**)

### Q9.4 2 eggs, 100 floors. Find critical floor with min worst-case drops.
**Answer: 14.**
- Drop first egg from 14, then 14+13=27, 27+12=39, … until it breaks. Then linearly with second egg.
- Worst case = 14 drops regardless of where it breaks.
- General formula: smallest n such that n(n+1)/2 ≥ 100 → n=14.

### Q9.5 8 balls, 1 heavier. Find it in 2 weighings with balance scale.
- Weighing 1: 3 vs 3 (leave 2 aside).
  - Balanced → heavy is among 2 set aside. Weighing 2: 1 vs 1 → done.
  - Unbalanced → heavy is in the heavier group of 3. Weighing 2: pick 2 of 3, 1 vs 1. Balanced → 3rd one. Unbalanced → heavier.

### Q9.6 3L jug, 5L jug — measure exactly 4L.
1. Fill 5L → (0, 5)
2. Pour into 3L → (3, 2)
3. Empty 3L → (0, 2)
4. Pour 5L's 2 into 3L → (2, 0)
5. Fill 5L → (2, 5)
6. Pour into 3L until full (needs 1 more) → (3, **4**) ✅

### Q9.7 Knight & Knave (logic).
You meet 2 people. A says: "We are both knaves." Knights always tell truth, knaves always lie.
- If A is knight, statement is true → both knaves. Contradiction (A is knight).
- So A is knave. Then statement is a lie → not both knaves → B is knight.
- **Answer: A is knave, B is knight.**

### Q9.8 Number / letter series — patterns to spot:
- **Arithmetic:** +2, +2, +2 … (2, 4, 6, 8)
- **Geometric:** ×2 (1, 2, 4, 8, 16)
- **Differences of differences:** 2, 6, 12, 20, 30, ? → diffs 4,6,8,10 → next diff 12 → **42**
- **Squares/Cubes:** 1, 4, 9, 16, 25, ? → **36**
- **Fibonacci:** 1, 1, 2, 3, 5, 8, **13**
- **Alternating:** 2, 9, 4, 8, 6, 7, 8, ? → odd-position +2, even-position −1 → **6**
- **Prime numbers:** 2, 3, 5, 7, 11, **13**
- **Letters with skip:** A, C, F, J, O, ? → skip 1,2,3,4,5 → **U**

### Q9.9 Classic age/work puzzles:
**Q:** A is twice as old as B was when A was as old as B is now. If A is 35, find B.
Let B = x. When A was x, time passed = 35 − x. At that time, B was x − (35 − x) = 2x − 35.
A (35) = 2 · (2x − 35) → 35 = 4x − 70 → x = **26.25**. Hmm, suggests a slightly different framing — but this is the kind of setup. **Method:** assign variables for current ages, use "years ago"/"years from now" shifts.

**Q:** 6 workers build a wall in 8 days. How long for 4 workers?
Work = 6·8 = 48 worker-days. 48/4 = **12 days**.

### Q9.10 Probability puzzle:
**Q:** Two dice rolled. P(sum = 7)?
Favorable: (1,6)(2,5)(3,4)(4,3)(5,2)(6,1) = 6. Total = 36. **P = 6/36 = 1/6.**

### Q9.11 Monty Hall problem:
3 doors. Behind 1 is a car, 2 are goats. Pick a door. Host opens a different door revealing a goat. Should you switch?
**Yes! Switching wins 2/3 of the time.**
Intuition: your original pick was 1/3 right. The remaining 2/3 probability is concentrated on the single unopened door.

### Q9.12 Clock angle problem:
**Q:** Angle between hour and minute hand at 3:15?
- Minute hand at 3:15 → 90° (15 min × 6°/min)
- Hour hand at 3:15 → 3·30 + 15·0.5 = 97.5°
- Angle = |97.5 − 90| = **7.5°**

### Q9.13 Coin/water problems:
**Q:** You have 9 identical-looking coins; 1 is fake (lighter). Find it with 2 weighings using a balance scale.
Split into 3 groups of 3. Weighing 1: group A vs B. If equal → fake in C; if unequal → in lighter pan. Then 1 vs 1 of that group → done.

### Q9.14 Lateral thinking:
**Q:** A man pushes his car to a hotel and tells the owner he's bankrupt. Why?
**A:** They're playing Monopoly.

### Q9.15 Strategy for unfamiliar puzzles (general method):
1. **Restate** the problem in your own words.
2. **Identify constraints and goal.**
3. **Try a small case** (n=1, 2, 3) to spot pattern.
4. **Work backwards** from goal.
5. **Find the invariant** (something that doesn't change).
6. **Use symmetry / parity / divide-and-conquer.**
7. If stuck → show your reasoning anyway. Examiners reward thought process.

---

# 🎯 FINAL EXAM STRATEGY (BJIT-SPECIFIC)

### Time Allocation (for 60-min exam, ~100 marks)
| Activity | Time |
|---|---|
| Read entire paper, mark easy/medium/hard | 2 min |
| Solve all easy questions | 15 min |
| Solve medium questions | 25 min |
| Tackle hard / coding deep-dive | 13 min |
| Review, complexity notes, fix bugs | 5 min |

### Top 1% Behaviors (what most candidates DON'T do)
1. **Annotate complexity** on every coding answer: `// Time: O(n), Space: O(1)`.
2. **Comment your approach** in 1 line before the code: `// two pointers + reverse trick`.
3. **Dry-run** with a small example in the margin to verify.
4. **Mention edge cases**: empty input, single element, all duplicates, negative numbers, very large input.
5. **Cite the technique name**: "this uses Floyd's algorithm", "Kadane's", "two-pointer", "sliding window" — shows depth.
6. **For OOP/AI questions:** use bullets, give a code example or concrete real-world example.
7. **For SQL:** prefer JOIN syntax over subqueries when both work. Mention indexes.
8. **For puzzles:** show ALL steps even if unsure. Partial credit is huge.
9. **Handwriting matters.** Neatness affects perception.
10. **Always put your name/ID on every sheet.**

### Common Pitfalls to Avoid
- ❌ Solving the hardest first and burning time
- ❌ Writing code without a plan
- ❌ Forgetting to handle edge cases
- ❌ Not specifying complexity
- ❌ Skipping the puzzle (it's often worth 10–15 marks!)
- ❌ Memorizing without understanding (they ask follow-ups)
- ❌ Leaving SQL queries un-aliased and unreadable

### Last Words
You now have ~150+ Q&As covering every BJIT exam topic at depth. The candidate who:
- Codes clean + annotates complexity
- Answers OOP trick questions confidently
- Writes correct SQL with JOINs
- Knows overfitting, gradient descent, and Bayes
- Solves the puzzle with shown reasoning

…**finishes in the top 1%.** That candidate is now you.

**Go get the offer. 🚀**
