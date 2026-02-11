The env that a rational agent interacts with. 4 aspects - PEAS;
- performance
- environment
- actuator
- sensor

| Agent Name                          | Performance Measure                                          | Environment                                                | Actuators                                                       | Sensors                                                     |
| :---------------------------------- | :----------------------------------------------------------- | :--------------------------------------------------------- | :-------------------------------------------------------------- | :---------------------------------------------------------- |
| **Taxi Driver**                     | • Safe, Fast, Legal, Comfortable trip<br>• Maximize profits  | • Roads<br>• Other traffic<br>• Pedestrians<br>• Customers | • Steering, accelerator, brake, signal, horn, display           | • Camera, sonar, speedometer, GPS, odometer, engine sensors |
| **Medical Diagnosis System**        | • Healthy patient<br>• Minimize costs<br>• Minimize lawsuits | • Patient<br>• Hospital<br>• Staff                         | • Display of questions, tests, diagnosis, treatments, referrals | • Keyboard entry of symptoms, findings, patient’s answers   |
| **Satellite Image Analysis System** | • Correct image categorization                               | • Downlink from orbiting satellite                         | • Display of the images (categories)                            | • Color pixel arrays                                        |
| **Part-Picking Robot**              | • Percentage of parts in correct bins                        | • Conveyor belt with parts<br>• Bins                       | • Jointed arm and hand                                          | • Camera, joint angle sensors                               |
| **Refinery Control**                | • Purity, Yield, Safety                                      | • Refinery<br>• Operators                                  | • Valves, pumps, heaters, display                               | • Temperature, pressure, chemical sensors                   |
| **Interactive English Tutor**       | • Student’s score on test                                    | • Set of students<br>• Testing agency                      | • Display of exercises, suggestions, corrections                | • Keyboard entry                                            |
### 1. Fully vs. Partially Observable
*   **Question:** Can the agent see everything it needs to?
*   **Fully Observable:** The agent has access to **all** the relevant information (like a player seeing the whole board in Chess).
*   **Partially Observable:** The agent’s view is limited (like driving in fog or a Poker hand where you can't see opponents' cards).
*   **Note:** If the agent has **no sensors**, the environment is unobservable.

### 2. Deterministic vs. Stochastic
*   **Question:** Does doing the same action always produce the same result?
*   **Deterministic:** The next state is completely decided by the current state and the agent's action. It’s predictable (like a puzzle game).
*   **Stochastic:** The next state involves randomness or chance. It’s unpredictable (like rolling dice).
*   **Strategic:** If the environment is deterministic *except* for the actions of other agents (like Chess), it is called **Strategic**.

### 3. Episodic vs. Sequential
*   **Question:** Do past decisions affect the future?
*   **Episodic:** The agent's work is divided into independent "episodes." What you do in one episode does not affect the next (like an assembly line scanning separate items; if you mess up one, the next is still fine).
*   **Sequential:** Current decisions affect future decisions. The agent must think ahead (like playing Chess or driving; a wrong move now changes the game later).

### 4. Static vs. Dynamic
*   **Question:** Does the environment change while the agent is "thinking"?
*   **Static:** The environment stays the same while the agent is deliberating. The agent can take its time to decide.
*   **Dynamic:** The environment changes while the agent is thinking (like driving; traffic moves while you decide where to turn).
*   **Semi-dynamic:** The environment doesn’t change, but the agent’s **performance score** does (like a timed test; the clock is ticking, but the questions aren't changing).

### 5. Discrete vs. Continuous
*   **Question:** Are the options limited or infinite?
*   **Discrete:** There is a clear, limited number of distinct choices (like Chess: you have a specific set of moves).
*   **Continuous:** The spectrum of actions and data is smooth and infinite (like driving: you can turn the wheel 1 degree, 1.5 degrees, 1.55 degrees, etc.).

### 6. Single Agent vs. Multiagent
*   **Question:** Is the agent alone?
*   **Single Agent:** The agent operates by itself (like a Solitaire puzzle).
*   **Multiagent:** There are other agents involved.

**In Multiagent environments, the relationship matters:**
*   **Competitive:** You are fighting against the other agents (e.g., Chess).
*   **Cooperative:** You are working with the other agents to achieve a goal (e.g., Autonomous driving—cars avoid crashing into each other to keep traffic flowing).

| Property          | Key Difference                        | Example                                         |
| :---------------- | :------------------------------------ | :---------------------------------------------- |
| **Observable**    | See All vs. See Some                  | Chess (Full) vs. Poker (Partial)                |
| **Deterministic** | Predictable vs. Random                | Puzzle (Det) vs. Dice (Stochastic)              |
| **Episodic**      | Independent tasks vs. Chain of events | Factory Line (Episodic) vs. Chess (Sequential)  |
| **Dynamic**       | Changes while thinking vs. Stays same | Driving (Dynamic) vs. Crossword Puzzle (Static) |
| **Discrete**      | Clear steps vs. Smooth flow           | Chess (Discrete) vs. Driving (Continuous)       |
| **Multiagent**    | Co-op vs. Competitive                 | Traffic (Co-op) vs. Chess (Competitive)         |
