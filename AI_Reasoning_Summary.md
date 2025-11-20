# ⭐ AI: REASONING & PROBLEM SOLVING — Full Course Summary

This course builds the foundations of **classical AI**: representing problems, reasoning about them, and solving them via search, logic, constraint satisfaction, game-playing, and probabilistic reasoning. It teaches **how AI systems think**, not just what they output.

Below is everything you learned across all 30 sessions.

---

# 1. Foundations of AI (Sessions 1–2)

## What is AI?
AI can be defined as systems that:
- **Think humanly** (cognitive modeling)  
- **Act humanly** (Turing test)  
- **Think rationally** (logic)  
- **Act rationally** (rational agents — standard model)

## History of AI
- **1940–1956:** Neurons, Hebbian learning, Turing  
- **1956–1969:** Early enthusiasm, GPS, Lisp, perceptrons  
- **1966–1973:** AI winter  
- **1969–1986:** Expert systems (MYCIN, DENDRAL)  
- **1987–2010:** Probabilistic methods, ML  
- **2011–today:** Deep learning, transformers, LLMs

## Modern AI Applications
Machine translation, speech recognition, self-driving, games (Go, StarCraft), medical AI, image understanding.

---

# 2. Agents & Environments (Sessions 3–4)

## Types of Agents
- Simple reflex  
- Model-based reflex  
- Goal-based  
- Utility-based  
- Learning agents (with critic + performance element)

## Environment Types (PEAS)
- Fully vs partially observable  
- Single vs multi-agent  
- Deterministic vs stochastic  
- Episodic vs sequential  
- Static vs dynamic  
- Discrete vs continuous  
- Known vs unknown  

## Problem Formulation
- States  
- Actions  
- Transition model  
- Goal test  
- Path cost  

---

# 3. Uninformed Search (Sessions 5–6)

- **Breadth-first search (BFS)**  
- **Depth-first search (DFS)**  
- **Uniform-cost search (UCS / Dijkstra)**  
- **Depth-limited search**  
- **Iterative deepening search**
- **Bidirectional search**

Properties: completeness, optimality, time & space complexity.

---

# 4. Informed Search (Session 7)

## Heuristics
- h(n): estimate of distance to goal  
- **Admissible** = never overestimates  
- **Consistent** = respects triangle inequality  

## Algorithms
- **Greedy Best-First Search** (f = h)  
- **A\*** (f = g + h)  
- Heuristic dominance, relaxed problems, pattern databases  

---

# 5. Local Search & Optimization (Session 9)

- Hill climbing  
- Simulated annealing  
- Genetic algorithms  
- Continuous optimization (gradients, Newton methods)

---

# 6. Non-Determinism & Partial Observability (Sessions 10–11)

- AND-OR search  
- Conditional plans  
- Belief states  
- Sensorless planning  
- Online search  
- LRTA*  

---

# 7. Adversarial Search & Games (Sessions 12–15)

- Minimax  
- Alpha-beta pruning  
- Evaluation functions  
- Cutoffs, forward pruning  
- Monte Carlo Tree Search (MCTS)  
- Stochastic games (expectiminimax)  
- Partially observable games (belief states, information gain)

---

# 8. Constraint Satisfaction Problems (Sessions 16–17)

## Core components
- Variables  
- Domains  
- Constraints  

## Consistency & Propagation
- Node consistency  
- **Arc consistency (AC-3)**  
- Path consistency  
- K-consistency  
- Global constraints (AllDiff, AtMost)

## Search for CSPs
- Backtracking  
- MRV, Degree heuristic  
- LCV heuristic  
- Forward checking  
- Maintaining Arc Consistency (MAC)

## Local Search
- Min-conflicts  
- Constraint weighting  

## Structure
- Tree-structured CSPs (linear-time)  
- Cutset conditioning  
- Tree decomposition  

---

# 9. Logical Agents & Knowledge Representation (Sessions 18–22)

## Propositional Logic
- Syntax, semantics  
- Model checking  
- Resolution  
- Wumpus world axioms  

## First-Order Logic (FOL)
- Terms, predicates, quantifiers  
- Models & interpretations  
- Unification  
- Generalized Modus Ponens  
- Resolution in FOL  
- Skolemization  

## Knowledge Representation Topics
- Categories, objects, taxonomies  
- Ontologies  
- Event calculus  
- Physical composition (PartOf, collections)

## Planning
- Classical planning  
- PDDL  
- Action schemas  
- Forward/backward search  
- Hierarchical Task Networks (HTN)

---

# 10. Reasoning Under Uncertainty (Sessions 23–25)

## Probability Theory
- Priors, posteriors  
- Conditional probability  
- Independence & conditional independence  

## Bayesian Inference
- **Bayes’ Rule**  
- Combining evidence  

## Naive Bayes
- Text classification  

## Bayesian Networks
- CPTs  
- Markov blanket  
- D-separation  
- Exact inference (enumeration, variable elimination)  
- Approximate inference (sampling, MCMC)

## Causal Networks
- do-operator  
- Counterfactuals  

## Probabilistic Programming
- Representing stochastic processes

---

# 11. LLMs & Traditional AI (Sessions 28–29)

- Reasoning processes in LLMs  
- Symbolic vs neural compatibility  

---

# 12. Final Exam Preparation (Session 30)

- Understanding > memorization  
- Choosing the right algorithm  
- Knowing assumptions (observability, determinism, etc.)
- Tradeoffs in optimality, completeness, efficiency  

---

# ⭐ In One Sentence
This course teaches how intelligent agents represent problems, reason about them, and choose optimal actions through search, logic, constraints, planning, and probabilistic inference—even under uncertainty or adversaries.
