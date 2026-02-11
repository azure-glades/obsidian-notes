
> [!IMPORTANT]+ Definitions
> 1. Agent - entity that perceives the env through sensors and acts on the env through actuators.
> 2. Percept - what the agent sense from the env
> 3. percept sequence - complete history of sensing
> 4. agent function - maps percept sequence to action

> [!info] Structure of an agent
> $$\text{Agent = Architecture + Program}$$
> Something to store information, act and perceive
> Something to think and decide

### Rational Agent
- Rationality at any time depends on four things:  
  1. The performance measure (what counts as success).  
  2. The agent’s percept sequence (everything it has sensed so far).  
  3. What the agent knows about the environment.  
  4. The actions the agent can take.  

- Rational ≠ perfect:  
  - Rationality means choosing actions to maximize expected performance.  
  - Perfection means achieving the best possible actual outcome (which may not be knowable in advance).  

- Example: A simple vacuum cleaner agent  
  - If current square is dirty → clean it.  
  - If current square is clean → move to the other square.
### Omniscient Agent
*   An Omniscient Agent knows the result of actions before acting, but this is impossible in real life.
*   Rationality does not require knowing everything (omniscience).
*   Agents can act to change what they perceive next, helping them gather information (Information Gathering and Exploration).
    *   Information Gathering: Collecting data from surroundings.
    *   Exploration: Analyzing data to find future patterns.
*   Agents can learn from what they perceive.
*   An agent is Autonomous if its behavior depends on its own experience (it can learn and adapt).
## Types of agents 
### Simple reflex agent
very simple *condition-action rules* to decide . sense environment, compares with rules-table and decides what action to take.
- no memory
- only sees current percept, no percept history
- no learning
- simple and fast
- cannot handle partially obs env
![[Pasted image 20251107022324.png]]
### Model-based agent
agent maintains an internal state by perceiving the environment. determines its next action based on this internal state.
1. internal model - has an internal model to track the current state of env
2. state tracking - updates its states by perceiving
3. adapts to partially obs envs by modelling the env and filling in the gaps
4. limited memory and reasoning, only good where short-term memory is sufficient
![[Pasted image 20251107022712.png]]
### Goal based reflex agent
agent has a goal function that it tries to maximize. compares actions and takes the action that optimizes the goal.
 > generally uses [[Search Algorithms]] to search the state-space tree
1. goal oriented decision making
2. planning capability - search algorithms used to find the best possible sequence of actions to reach a goal.
3. flexible and adapt to changes in env quickly
4. require more computational resource to store, maintain state and compare actions
![[Pasted image 20251107022608.png]]
### Utility based agent
has a utility function to deal with conflicting goals. evaluates actions based on goal + utility fn
![[Pasted image 20251107022625.png]]
### Learning agent
has an internal learning element to update actions based on past experiences. can accumulate basic knowledge of the environment and adapt by learning.
1. learning element - learns from actions + percept sequence
2. critic element - to identify flaws in solution/action
3. problem generator - generates variations to test actions against. critics the resukt
4. performance element - evals performance
Properties:
- self improving
- explores the env. exploits the env
- adapts to changes quickly
- handles uncertainity
Limitations:
- data dependence
- computational demand
- risk of overfitting
![[Pasted image 20251107022758.png]]


