# Chapter 07 Network Flow

### 7.1 Max-flow and Ford-Fulkerson Algorithm

#### I. Problem

+ G = (V, E) = directed graph

+ Two distinguished nodes: s = source, t = sink.
+ c(e) = nonnegative capacity of edge e

##### A. Def.

+ The value of a flow f is: $v( f ) = \sum{f (e)}$

<img src="./Image/Slide6.6.png" alt="Slide5.4" align='left' style="zoom: 45%;" />

##### B. Maximum Flow Problem

+ Max flow problem. Find s-t flow of maximum value
+ Same as above, greedy doesn't work

#### II. Concept

##### A. Residual Graph

+ Important concept, throughout the network flow work
+ Original edge: $e = (u, v) \in E$
  + Flow f(e), capacity c(e)

<img src="./Image/Slide6.15_1.png" alt="Slide5.4" align='left' style="zoom: 60%;" />

+ Residual edge.
  +  "Undo" flow sent.
  + $e = (u, v)$ and $e^R = (v, u).$

<img src="./Image/Slide6.15_2.png" alt="Slide5.4" align='left' style="zoom: 60%;" />

##### B. Augmenting Path

+ Def. Augmenting path
  + a simple s-t path P in the residual graph $G_f$ 
  + ❗Notion: in residual graph
+ Def. Bottleneck capacity
  + of an augmenting path P is the minimum residual  capacity of any edge in P
+ Def. Claim
  + After augmentation, f is still a flow

#### III. Ford-Fulkerson Algorithm

- Start with f(e) = 0 for all edge e $\in$ E.
  - flow = 0 at start
- Find an augmenting path P in the residual graph  $G_f$ 
- Augment flow along path P.
- Repeat until you get stuck.

<img src="./Image/Slide6.17.png" alt="Slide5.4" align='left' style="zoom: 60%;" />

### 7.2 Max-flow and Min-cut

#### I. Problem

Minimum Cut Problem

##### A. Concept

+ An s-t cut is a partition (A, B) of V with s $\in$ A and t $\in$ B.
+ ⭐The capacity of a cut (A, B) is: $cap(A,B) = \sum\limits_{e-out-of-A} c(e)$
  + Definition of $cap(A,B)$ is important
+ Min s-t cut problem.  
  + Find an s-t cut of minimum capacity

<img src="./Image/Slide6.29.png" alt="Slide5.4" align='left' style="zoom: 40%;" />

+ ❗Notion:
  + Capacity is only out of A, not reduce the capacity of edge into A.
  + Value need to reduce the capacity of edge into A

+ Flow value lemma
  + Let f be any flow, and let (A, B) be any s-t cut. Then
  + $\sum\limits_{e-out-of-A} f(e) - \sum\limits_{e-in-of-A} f(e) = v(f)$

<img src="./Image/Slide6.32.png" alt="Slide5.4" align='left' style="zoom: 40%;" />

+ cap(A, B)
  + sum of A to B edge capacity

#### II. Max-Flow Min-Cut Theorem

+ We know in 7.1, augmenting path is to find the **max flow**
+ In this case, we want to prove the **max flow = min cut**

##### A. Lemma

+ Augmenting path theorem
  + Flow f is a max flow iff (if and only if) there are no  augmenting paths. 
+ Max-flow min-cut theorem. [Ford-Fulkerson 1956] 
  + The value of the  max flow is equal to the value of the min cut.

##### B. Proof

+ Proof strategy. We prove both simultaneously by showing the  equivalence of the following three conditions for any flow f:
  + (i) There exists a cut (A, B) such that v(f) = cap(A, B).
  + (ii) Flow f is a max flow.
  + (iii) There is no augmenting path relative to f.
+ (i) $\Rightarrow$ (ii) 
  + This was the corollary to weak duality lemma.
+ (ii) $\Rightarrow$ (iii) We show contrapositive.
  + If there exists an augmenting path, then we can improve f by  sending flow along path.

### 7.3 Choosing Good Augmenting Paths

#### I. Choosing Good Augmenting Paths

+ Selection
  + Some choices lead to exponential algorithms.   -> $O(2^n)$
  + Clever choices lead to polynomial algorithms.   -> $O(n)$
+ Goal
  + Can find augmenting paths efficiently.
  + Few iterations.
+ Choose augmenting paths with: [Edmonds-Karp 1972, Dinitz 1970]
  + Max bottleneck capacity.
  + Fewest number of edges.
  + Sufficiently large bottleneck capacity.
  + PS: Find the large enough bottleneck capacity

#### II. Capacity Scaling

+ Intuition -> Choosing path with high bottleneck capacity
  + Maintain scaling parameter $\Delta$
  + Let the $\Delta$-residual graph $G_f(\Delta)$ be the subgraph of the residual  graph consisting of only arcs with capacity at least $\Delta$.

<img src="./Image/Slide6.44.png" alt="Slide5.4" align='left' style="zoom: 40%;" />

+ Correctness -> If the algorithm terminates, then f is a max flow.
  + Pf.
  + By integrality invariant, when $\Delta$ = 1 $\Rightarrow$ $G_f(\Delta)$ = $G_f$.
    + $\Delta$ = 1, it won't filter out any edges
  + Upon termination of $\Delta$ = 1 phase, there are no augmenting paths.

### 7.5 Bipartite Matching

#### I. Definition

+ Matching
  + Input: undirected graph G = (V, E).
  + M $\subseteq$ E is a matching if each node appears in at most one edge in M.
    + i.e. one node, one edge
  +  Max matching: find a max cardinality matching.

<img src="./Image/Slide6.53.png" alt="Slide5.4" align='left' style="zoom: 40%;" />

+ Bipartite matching
  + Input: undirected, bipartite graph G = (L $\cup$ R, E).
    + like hw2 problem 5 and 6, constructs a bipartite graph
  + M $\subseteq$ E is a matching if each node appears in at most one edge in M.
  +  Max matching: find a max cardinality matching.

<img src="./Image/Slide6.55.png" alt="Slide5.4" align='left' style="zoom: 40%;" />

#### II. Algorithm

+ Max flow formulation
  + Create digraph G' = (L $\cup$ R $\cup$ {s, t}, E' ).
  + Direct all edges from L to R, and assign infinite (or unit) capacity.
  + Add source s, and unit capacity edges from s to each node in L.
  + Add sink t, and unit capacity edges from each node in R to t.

<img src="./Image/Slide6.56.png" alt="Slide5.4" align='left' style="zoom: 40%;" />

##### A. Proof

+ Theorem. 
  + Max cardinality matching in G = value of max flow in G'.
+ Pf. first prove  $\leq$
  + Given max matching M of cardinality k.
  + Consider flow f that sends 1 unit along each of k paths.
  + f is a flow, and has cardinality k.
  + My understanding
    + 左边有k条边match，右边至少可以找到这么k path，所以flow value至少是k ->  左边 $\leq$ 右边

<img src="./Image/Slide6.57.png" alt="Slide5.4" align='left' style="zoom: 40%;" />

+ Pf. prove  $\geq$
  + Let f be a max flow in G' of value k.
  + Integrality theorem $\Rightarrow$ k is integral and can assume f is 0-1
  + Consider M = set of edges from L to R with f(e) = 1
    + each node in L and R participates in at most one edge in M
    + |M| = k: consider cut (L $\cup$ s, R $\cup$ t)
  + My understanding
    + 中间的 flow 非0即1 -> max matching $\geq$ k -> 左边  $\geq$  右边
+ Therefore, Max cardinality matching in G = value of max flow in G'

### 7.7 Extensions to Max Flow