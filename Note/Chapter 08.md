# Chapter 08 NP and Computational Intractability

### 8.1 Polynomial-Time Reductions

#### I. Classify Problems

##### A. Definition

+ Q. Which problems will we be able to solve in practice?
+ A. A working definition. [Cobham 1964, Edmonds 1965, Rabin 1966]  
  + Those with polynomial-time algorithms. 
  + (In practice, poly-time  algorithms scale to huge problems.)
  + i.e. If the problem exists polynomial-time algorithm 
+ Desiderata
  + Classify problems  ->  what we want to do
  + according to those that can be solved in polynomial-time and those that cannot

### 8.2 Reductions via "Gadgets"

#### I. Satisfiability

⭐Remember these concepts, they are basic of follow part

+ Literal	->	文字
  + A Boolean variable or its negation
  + $x_i$ or $\bar{x_i}$
+ Clause   ->    子句
  + A disjunction of literals
  + $C_j=x_1\or\bar{x_2}\or x_3$
+ Conjunctive normal form    ->    CNF    ->    合取范式
  + A propositional formula $\Phi$ that is the conjunction of clauses
  + $\Phi=C_1\and C_2\and C_3\and C_4$
+ SAT
  + Given CNF formula $\Phi$, does it have a satisfying truth assignment?
  + $\Phi$ is true    ->    all $C_i$ is true    ->    one of Literals in Clause is true
+ 3-SAT
  + SAT where each clause contains exactly 3 literals

<img src="./Image/Slide7.20.png" alt="Slide7.20" align='left' style="zoom: 60%;" />

#### II. 3 Satisfiability Reduces to Independent Set

⭐⭐This is a typical reducing case, and the format of homework could follow this

##### A. Construct

+ Claim
  + 3-SAT $\leq_p$  `INDEPENDENT-SET`
+ Pf
  + Given an instance $\Phi$ of 3-SAT, we construct an instance (G, k) of  `INDEPENDENT-SET` that has an independent set of size k iff $\Phi$ is satisfiable
+ Construction    ->    
  + G contains 3 vertices for each clause, one for each literal
  + Connect 3 literals in a clause in a triangle
  + Connect literal to each of its own negations

<img src="./Image/Slide7.21.png" alt="Slide7.20" align='left' style="zoom: 40%;" />

##### B. Proof

+ Claim
  + G contains independent set of size k = |$\Phi$| iff $\Phi$ is satisfiable.
+ Pf    $\Rightarrow$    Let S be independent set of size k    ->    k is the num of triangle
  + S must contain exactly one vertex in each triangle
    + i.e. each triangle, at least one vertex in S
  + Set these literals to true
    + we know $x_2$ connect with $\bar{x_2}$, so the variable value have no possibility to conflict
  + Truth assignment is consistent and all clauses are satisfied
+ Pf    $\Leftarrow$    Given satisfying assignment, select one true literal from each  triangle. This is an independent set of size k
  + Observe the graph, it is exactly right

#### III. Review

##### A. Feature

Why review? Because it is a basic and important method

+ Basic reduction strategies
  + Simple equivalence: INDEPENDENT-SET $\equiv_P$ VERTEX-COVER
    + Reduce to each other
  + Special case to general case: VERTEX-COVER $\leq_P$ SET-COVER
  + Encoding with gadgets: 3-SAT $\leq_P$ INDEPENDENT-SET
+ Transitivity
  + If X $\leq_P$ Y and Y $\leq_P$ Z, then X $\leq_P$ Z
+ Pf idea
  + Compose the two algorithms
+ Ex: 
  + 3-SAT $\leq_P$ INDEPENDENT-SET $\leq_P$ VERTEX-COVER $\leq_P$ SET-COVER

##### B. Self-Reducibility

+ Decision problem
  + Does there exist a vertex cover of size $\leq$ k?
+ Optimization problem
  + Find vertex cover of minimum cardinality

Chapter 8 cares about decision

+ Self-reducibility    ->    Optimization problem $\leq_P$ decision version
  + Applies to all (NP-complete) problems in this chapter
  + Justifies our focus on decision problems
+ Ex: to find min cardinality vertex cover
  + (Binary) search for cardinality k* of min vertex cover
  + Find a vertex v such that `G - {v}` has a vertex cover of size d k* - 1    ->    a natural idea
    + v must be in a vertex cover of size $\leq$ k*
    + Prove by construction: a vertex cover of `G - {v}` plus v must be a  vertex cover of G
  + Include v in the vertex cover
  + Recursively find a min vertex cover in `G - {v}`

