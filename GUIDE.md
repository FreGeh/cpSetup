# Table of Contents

- [Practical](#practical)
- [C++ Basic Overview](#c-basic-overview)
- [Datastructures](#datastructures)
- [Algorithm Design](#algorithm-design)
- [Sort & Search](#sort--search)
- [Graphs](#graphs)
  - [Data Structures](#data-structures-1)
  - [BFS](#bfs)
  - [DFS](#dfs)
  - [Floyd-Warshall](#floyd-warshall)
  - [Dijkstra](#dijkstra)
- [Dynamic Programming](#dynamic-programming-1)
  - [Knapsack](#knapsack)
  - [Longest Subsequence](#longest-subsequence)
- [Strings](#strings)
- [Geometry](#geometry)
- [Mathematics](#mathematics)

# Practical

## Workflow
1. `g++ -std=c++20 -O2 -Wall program.cpp -o program`
2. `./program < input.txt`

## Must Have Header
```cpp
#include "bits/stdc++.h"
using namespace std;
#define ll long long
```
## Fast I/O template
Inside main function, always add:
```cpp
ios::sync_with_stdio(false);
cin.tie(nullptr);
```

## Estimate Runtime
| Typical technique | Time complexity | Safe max |
|-------------------|----------------|----------|
| Binary exponentiation, binary search, GCD | $\mathcal O(\log n)$ | $n \le 10^{18}$ |
| Trial division, sieve of Eratosthenes | $\mathcal O(\sqrt n)$ | $n \le 10^{15}$ |
| Linear scan, two-pointer, cumulative sums | $\mathcal O(n)$ | $n \le 10^{8}$ |
| Sorting (merge sort, quicksort, heapsort) | $\mathcal O(n \log n)$ | $n \le 10^{6}$ |
| BFS / DFS on graph $(n+m)$ | $\mathcal O(n+m)$ | $n,m \le 2\cdot 10^{5}$ |
| Dijkstra / Prim (binary heap) | $\mathcal O(m \log n)$ | $n,m \le 2\cdot 10^{5}$ |
| Segment tree / Fenwick tree (updates + queries) | $\mathcal O\!\bigl((n+q)\log n\bigr)$ | $n,q \le 2\cdot 10^{5}$ |
| Mo’s algorithm, block decomposition | $\mathcal O(n\sqrt n)$ | $n \le 10^{5}$ |
| DP on pairs, prefix tables, double loop | $\mathcal O(n^{2})$ | $n \le 5000$ |
| Floyd–Warshall, cubic DP, matrix multiplication | $\mathcal O(n^{3})$ | $n \le 500$ |
| Bitmask DP / enumerate all subsets | $\mathcal O(2^{n})$ | $n \le 20$ |
| Backtracking all permutations | $\mathcal O(n!)$ | $n \le 11$ |

# C++ Basic Overview

## Input
- `cin >>` reads whole string till space
- `cin.get(c)` reads `char c`, also spaces and `\n`
- `getline(cin, s)` reads whole line as `string s`
- `vector<char> S(tmp.begin(), tmp.end())` seperates string into char vector

for $n$ numbers:
```cpp
int n;
cin >> n;
vector<int> A(n);
for (int &x : A) {
    cin >> x;
}
```

## Output
- `cout <<` standard
- `(bool ? "true" : "false")` to output a value depending on the bool value

## Math Tricks
- Round Up in fractions, use `a+b-1/b` instead of `a/b`.

## STL Tricks
```cpp
iota(v.begin(), v.end(), 0); // 0,1,2,...
accumulate(v.begin(), v.end(), 0LL); // sum
sort(v.begin(), v.end(), greater<>()); // descending
equal(v.begin(), v.begin()+n/2, v.rbegin()); // palindrome
```

## Data Types
| Type | Size / Range | Notable properties |
|------|--------------|-------------------|
| `int` | $4\text{ B},\;[-2^{31},\,2^{31}\!-\!1]$ | fastest arithmetic, default loop index |
| `long long` | $8\text{ B},\;\approx[-9{\times}10^{18},\,9{\times}10^{18}]$ | 64-bit signed, safe for most sums/products |
| `unsigned int` | $4\text{ B},\;[0,\,2^{32}\!-\!1]$ | wrap-around mod $2^{32}$; bit masks |
| `unsigned long long` | $8\text{ B},\;[0,\,2^{64}\!-\!1]$ | 64-bit unsigned, modular hashes |
| `double` | $8\text{ B},\;\sim15$ decimal digits | hardware FPU; geometry, probabilistic DP |
| `long double` (GCC) | $16\text{ B},\;\sim18$ digits | extra precision for numeric analysis |
| `char` | $1\text{ B},\;[0,255]$ | tiny integer; ASCII grids, bit tricks |
| `bool` | $1\text{ B}$ (bit-packed in `vector<bool>`) | logical flags, visited arrays |
| `size_t` | $8\text{ B},\;[0,\,2^{64}\!-\!1]$ | unsigned type returned by `sizeof`, container sizes |

## Data Structures
| Container / Helper | Key operations & complexity | Typical contest use |
|--------------------|----------------------------|--------------------|
| `vector<T>` | Dynamic array, index/push_back O(1) amortized | Arrays, graphs, DP tables |
| `deque<T>` | Push/pop front/back O(1) | Sliding window, 0-1 BFS |
| `list<T>` | Insert/erase O(1) with iterator | Rarely used; custom linked lists |
| `array<T,N>` | Fixed-size array, index O(1) | Small static arrays, DP, geometry |
| `stack<T>` | LIFO push/pop/top O(1) | DFS, parentheses checker |
| `queue<T>` | FIFO push/pop/front O(1) | BFS, task scheduling |
| `priority_queue<T>` | Push/pop/top O(log n) | Dijkstra, K-largest elements |
| `set<T>`/`multiset<T>` | Insert/erase/find O(log n) | Ordered sets, coordinate compression |
| `map<K,V>`/`multimap<K,V>` | Insert/erase/find O(log n) | Ordered maps, frequency counts |
| `unordered_set<T>`/`unordered_multiset<T>` | Insert/erase/find O(1) avg | Fast lookup, frequency counts |
| `unordered_map<K,V>`/`unordered_multimap<K,V>` | Insert/erase/find O(1) avg | Fast maps, hash tables |
| `bitset<N>` | Bitwise ops O(1), access O(1) | Bitmask DP, subset problems |
| `string` | Access O(1), concat O(n) | Token parsing, hashing, string algorithms |
| `pair<A,B>`/`tuple<...>` | Structured grouping, lex compare | Edges, multi-value returns |

# Datastructures

# Algorithm Design
## Problemtypes
* **Decision**: True/False
* **Search** (Valid Solution)
* **Construct** (Valid Structure)
* **Counting** (Number of Solutions)
* **Enumeration** (All Solutions)
* **Approximation** (Near Optimal)
* **Optimization** (Best Value)

## Brute Force
Search through entire solution space for correct one.
- easy, correct
- too slow

## Greedy
Local optimal decisions need to be globally optimal, since it doesn't take back previous decisions. Otherwise it's incorrect.
- efficient
- incorrect for many types of problems

## Divide & Conquer
* **Idea:** break problem into $k$ sub-instances, solve recursively, merge.
* **Classic uses:**
  * Merge sort, quicksort
  * Closest pair of points $O(n\log n)$
  * “Divide & Conquer DP” / “CDQ” optimisation $O(n\log n)$

## Backtracking
1. **Filter**: Generate all possible candidates (raw recursion - validation at end)
2. **Generator**: Generate only valid candidates (recursion with logic at every step)
3. **Pruning**: Try to recognize invalid solutions during generation and only continue working on possible valid ones

## Parametric Search
- Solution $x$ doesn't work => smaller $<x$ won't either
- Solution $x$ works => bigger $>x$ will too
*(the reverse is also possible)*
Implement **predicate** `can(x)`; binary-search smallest/largest `x` for quick checks.

## Dynamic Programming
1. Segment hard problem into easier problems
2. Solve each problem independently
3. Bring the solutions together to solve the hard problem

### Bottom Up
1. Define Sequence of which problems get solved
2. Save sub-solutions
3. Solve bigger problem with sub-solutions

### Top-Down
1. Segment hard problem into easier problems
2. Define Recursion Formula
3. Solution Known => Use it
3. Solution Unknown => Solve and then save it, so you dont have to do it again (**Memoisation**)

# Sort & Search
## BinarySearch
Search for biggest element in sorted list. Split up search space each round.
```pseudo
function binarySearch(A, target)
    low ← 0
    high ← |A| − 1
    while low ≤ high do
        mid ← low + (high − low) / 2 // overflow-safe
        if A[mid] == target then return mid
        if A[mid] < target then low ← mid + 1 // go right
        else high ← mid − 1 // go left
    return −1 // not in A
```
In C++ there are:
| Function | Meaning | Typical use |
|----------|---------|-------------|
| `binary_search(first, last, val)` | Returns **`true`** iff `val` exists in `[first, last)`. | Quick membership test. |
| `lower_bound(first, last, val)` | Iterator to **first element `≥ val`** (or `last` if none). | Insert position that keeps the range sorted. |
| `upper_bound(first, last, val)` | Iterator to **first element `> val`** (strictly greater). | Right end of the run of equal keys. |
| `equal_range(first, last, val)` | Returns `{lower_bound, upper_bound}`. | Span of all elements equal to `val`. |

# Graphs
## Data Structures
### Adjacency Matrice
- **Description**: $n \times n$ Matrice. $A_{i,j}=1$ means there is an edge from vertice $i$ to $j$
- **Space**: $O(n^2)$
- **Count Neighbours**: $O(n)$
- **Test Edge**: $O(1)$
- **Implementation**: ``vector<vector<bool>> A(n, vector<bool>(n, false))``

### Adjacency List
- **Description**: List with $n$ Entries, each having an array containing all vertices it's connected to.
- **Space**: $O(n+m)$
- **Count Neighbours**: $O(|\text{neighbours}|)$
- **Test Edge**: $O(|\text{neighbours}|)$
- **Implementation**: ``vector<vector<int>> adjlist``, for *weighted* ``vector<vector<pair<int,ll>>> adj``

### Edge List
- **Description**: List of all Edges displayed as a pair of the connected vertices
- **Space**: $O(m)$
- **Count Neighbours**: $O(m)$
- **Test Edge**: $O(m)$
- **Implementation**: ``vector<pair<int,int>> edges``

## BFS
- **Purpose**: Find shortest paths in unweighted Graph (and discover connectivity by layers)
- **Description**: Level‐by‐level (breadth‐first) exploration from the start vertex $s$
- **Runtime**: $O(n+m)$
- **Input**: Adjacency List, Starting Vertice $s$
- **Output**:
- **Code**:
```cpp
int s = 42; // Startknoten
vector<vector<int>> &adjlist;
int n = adjlist.size();
queue<int> q;
q.push(s);
vector<int> dist(n, INF), parent(n, -1);
dist[s] = 0;
parent[s] = -1;
while (!q.empty()) {
    int v = q.front();
    q.pop();
    for (int w : adjlist[v]) {
        if (dist[w] == INF) {
            dist[w] = dist[v] + 1;
            parent[w] = v;
            q.push(w);
        }
    }
}
```
and for the output:
```cpp
for (int w = 0; w < n; ++w) {
    if (parent[w] != -1)
        cout << parent[w] << " --> " << w << "  (dist=" << dist[w] << ")\n";
}
```

## DFS
- **Purpose**: Detect connectivity, reachability, cycles. Construct Paths. Perform topological sorting. Solve *backtracking* problems.
- **Description**: Explores Graph greedy from starting vertice $s$
- **Runtime**: $O(n+m)$
- **Input**: Adjacency List, Starting Vertice
- **Output**: DFS Tree
- **Code**:
```cpp
void visit(int v, vector<bool> &visited, vector<int> &parent) {
    visited[v] = true;
    for (int w : adjlist[v]) {
        if (!visited[w]) {
            parent[w] = v;
            visit(w, visited, parent);
        }
    }
}
```
to kick of the search and get the output:
```cpp
vector<vector<int>> &adjlist;
vector<bool> visited(n, false);
vector<int> parent(n, -1);
visit(s, visited, parent); // s = Startknoten
for (int w = 0; w < n; ++w) {
  if (parent[w] != -1)
    cout << parent[w] << " --> " << w << "\n";
}
```

## Floyd-Warshall
- **Purpose**: Find all shortest Paths in a (weighted) Graph
- **Description**: Iterates over all vertice combinations
- **Runtime**: $O(n^3)$
- **Input**: Adjacency Matrice
- **Output**: 2D Array with shortest distance from vertice $i$ to $j$
- **Code**:
```cpp
// Initialisierung: mat [i][j] = Laenge / infty
for (k = 0; k < n; k++) {
    for (i = 0; i < n; i++) {
        for (j = 0; j < n; j++) {
            if (mat[i][k] + mat[k][j] < mat[i][j]) {
                mat[i][j] = mat[i][k] + mat[k][j];
            }
        }
    }
}
// Ergebnis: mat [i][j] = Distanz von i nach j .
```

## Dijkstra
- **Purpose**: Compute shortest paths from a single source to every other vertex in a non-negatively weighted graph
- **Description**: Use a min-heap to repeatedly extract the closest vertex and relax its outgoing edges until all shortest distances from the source are determined.
- **Runtime**: $O(m \log n)$
- **Input**: Adjacency List `vector<vector<pair<int,int>>> adj`, Starting Vertice $s$
- **Output**: Vector with shortest distance from $s$ to every vertex $v$ `vector<ll> dist(n)`, optionally also `vector<int> prev(n)` for the reconstructed path
- **Code**:
```cpp
vector<ll> dijkstra(const vector<vector<pair<int,int>>>& adj, int s,
                    vector<int>* parent = nullptr)
{
    int n = adj.size();
    vector<ll> dist(n, INF);
    if (parent) parent->assign(n, -1);
    using State = pair<ll,int>;
    priority_queue<State, vector<State>, greater<State>> pq;
    dist[s] = 0;
    pq.emplace(0, s);
    while (!pq.empty()) {
        auto [d, u] = pq.top(); pq.pop();
        if (d != dist[u]) continue;
        for (auto [v, w] : adj[u]) {
            ll alt = d + w;
            if (alt < dist[v]) {
                dist[v] = alt;
                if (parent) (*parent)[v] = u;
                pq.emplace(alt, v);
            }
        }
    }
    return dist;
}
```
When you have many queries on the same graph, pay the $O(n \cdot m \cdot log(n))$ “up‐front” cost:
```cpp
vector<vector<ll>> buildAllPairs(const vector<vector<pair<int,int>>>& adj)
{
    int n = adj.size();
    vector<vector<ll>> D(n, vector<ll>(n, INF));
    for (int s = 0; s < n; ++s) {
        D[s][s] = 0;
        D[s] = dijkstra(adj, s);
    }
    return D;
}
```

# Dynamic Programming

## Knapsack
**Given**:
- $G=\{1, \dots, n\}$ **Objects** ($1 \leq |G| \leq 10^3$)
- $C \in \mathbb{N}$ **Capacity** ($1 \leq C \leq 10^4$)
- $v: G \to \mathbb{N}$ **Value** ($1 \leq v_i \leq 10^9$)
- $w: G \to \mathbb{N}$ **Weight** ($1 \leq w_i \leq 10^9$)

**Question**:
- What is the **max total value of unique objects**, which total weight is smaller than the capacity?

Sub-Solution:
- $F_{i,j}$ is max value of first $i$ objects with $j$ capacity
- We are looking for $F_{n,C}$
- Define **Base Cases**: $\forall j: F_{0,j}=0$ and $\forall i: F_{i,0}=0$
- Define **Recurrence**: For $i,j \geq 1$ is
$$
F_{i,j} =
\begin{cases}
F_{i-1,j} & w_i > j\\[4pt]
\max\bigl(F_{i-1,j},\; F_{i-1,\,j-w_i}+v_i\bigr) & \text{else}
\end{cases}
$$

DP Solution:
```cpp
for(int64_t i = 1; i <= n; ++i)
    for(int64_t j = 1; j <= C; ++j) {
        f[i][j] = f[i-1][j];
        if (j >= w[i])
            f[i][j] = max(f[i - 1][j], f[i-1][j-w[i]] + v[i]);
}
```

## Longest Subsequence

# Strings
| Technique | Solves | Core idea | Time |
|-----------|--------|-----------|------|
| **KMP** | Find a single pattern `P` (`m`) inside text `T` (`n`) | Build `pi[]` (longest proper border of each prefix). While scanning `T`, on mismatch jump to `pi[k-1]` instead of restarting. Implement with `vector<int> pi(m);`. | `O(n + m)` |
| **Z-algorithm** | Get, for every position, the longest prefix starting there (runs, pattern search) | Maintain current match box `[l,r]` equal to the prefix; extend each new index using that box. One forward pass filling `vector<int> z(n);`. | `O(n)` |
| **Rolling hash** | Constant-time substring compare, sliding window, duplicate detection | Store prefix hashes `H[i]` and powers `pow[i]`; hash of `[l,r]` is `H[r+1] − H[l]·pow[len]` mod `M`. Use two moduli to dodge collisions. | Build `O(n)`, query `O(1)` |
| **Aho–Corasick** | Locate **many** patterns (total length `L`) in a single text (`n`) | Insert patterns into a trie; BFS builds failure links (KMP on the trie). One linear scan over text follows `fail`/`next` edges and reports matches. | Build `O(L)`, search `O(n)` |

# Geometry
```cpp
struct P{ long long x,y; };
long long cross(P a,P b,P c){
    return (b.x-a.x)*(c.y-a.y) - (b.y-a.y)*(c.x-a.x);
}
```
* `cross>0` left turn, `<0` right turn, `=0` collinear.
* Distance squared `dsq = (dx*dx + dy*dy)` avoids `sqrt`.

# Mathematics