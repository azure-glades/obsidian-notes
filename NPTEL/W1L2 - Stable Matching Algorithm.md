## Core Concept: Preference Orderings
### What is a Preference Ordering?
1. **Definition**: 
   - A ranked list where each member of one group orders all members of the other group by desirability
   - Example: In dating context, each man ranks all women from most to least preferred

2. **Key Properties**:
   - Must be complete (all alternatives ranked)
   - Must be transitive (if A>B and B>C, then A>C)
   - Typically strict (no ties allowed in basic model)

3. **Notation**:
   - For Boy B: Woman W₁ > W₂ > W₃ means B prefers W₁ most, W₂ second, etc.
   - For Girl G: Man M₃ > M₁ > M₂ means G prefers M₃ most, etc.

## Problem Setup
### Stable Marriage Problem Components
1. **Two Disjoint Sets**:
   - Set X (e.g. men/employers/colleges)
   - Set Y (e.g. women/employees/students)
   - Equal size (|X| = |Y|)

2. **Preference Lists**:
   - Every x ∈ X has preference ordering over Y
   - Every y ∈ Y has preference ordering over X

3. **Matching**:
   - Bijection (one-to-one pairing) between X and Y

## Key Concepts with Examples
### 1. Rogue Couples
**Definition**: A pair (x,y) where:
- x prefers y over his current match
- y prefers x over her current match

**Example**:
- Current matching: (Rahul-Anjali), (Aman-Tina)
- Rogue couple: (Rahul,Tina) because:
  - Rahul prefers Tina > Anjali
  - Tina prefers Rahul > Aman

### 2. Stability Conditions
A matching is stable iff:
1. It's perfect (everyone matched)
2. No rogue couples exist

**Visualization**:
```
Boys: Girls:  
1: C>B>A A: 3>2>1  
2: A>B>C B: 2>1>3  
3: A>C>B C: 1>3>2

Unstable Matching:  
1-A, 2-B, 3-C → (1,C) form rogue couple

Stable Matching:  
1-C, 2-B, 3-A
```


## Algorithm Deep Dive
### Gale-Shapley Algorithm (1962)
**Key Steps**:
1. Initialization:
   - All boys free
   - All girls' preference lists intact

2. Proposal Phase:
   - Each free boy proposes to highest-ranked girl not yet rejected

3. Response Phase:
   - Each girl compares new proposals with current "maybe"
   - Keeps best offer (as per her preferences), rejects others

4. Termination:
   - When no boy is free
   - Guaranteed in O(n²) time

**Execution Example**:
```
Day 1:

- Boys propose to 1st choices
    
- Girl A gets proposals from 2,4,5 → keeps 5 (top preference)
    

Day 2:

- Rejected boys 2,4 propose to next choices
    
- Girl B gets 2, Girl C gets 4
    
- Girl C compares new proposal (4) vs none → keeps 4
    

Final Matching:  
1-E, 2-B, 3-D, 4-C, 5-A
```


## Why It Works: Theoretical Guarantees
1. **Termination Proof**:
   - Each boy makes ≤n proposals
   - n boys → ≤n² proposals total

2. **Perfect Matching**:
   - If boy unmatched, some girl unmatched (but she'd accept any proposal)

3. **Stability Proof**:
   - Suppose (x,y) is rogue couple:
     - Case 1: y rejected x → has better match
     - Case 2: x never proposed to y → has better match
   - Contradiction in both cases

## Practical Implications
1. **Algorithm Variants**:
   - Girl-proposing version (changes optimality)
   - Many-to-one matching (e.g. hospitals-residents)

2. **Real-world Applications**:
   - National Residency Matching Program (US medical graduates)
   - School choice systems
   - Sorority rush process

3. **Limitations**:
   - Requires complete preference lists
   - No side payments/negotiations
   - Assumes participants truthfully report preferences

[[W1L3 - Hedging]]