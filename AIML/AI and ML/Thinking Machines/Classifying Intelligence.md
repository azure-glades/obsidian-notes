4 methods of measuring intelligence has developed
## Acting humanly : Turing Test Approach
*   Proposed by Alan Turing (1950) as a practical definition of intelligence.
*   A computer passes if it performs well enough to fool a human interrogator.
*   The interrogator communicates via text (teletype) and cannot tell if they are talking to a human or a computer.
*   The computer needs specific capabilities to pass:
	*   **Natural Language Processing (NLP):** To communicate in English (or another language).
	*   **Knowledge Representation:** To store what it learns during the interrogation.
	*   **Automated Reasoning:** To use stored info to answer questions and draw conclusions.
	*   **Machine Learning (ML):** To adapt to new situations and detect patterns.
*   The standard test avoids physical interaction because looking like a human isn't necessary for intelligence.

*   **The Total Turing Test**
    *   Includes a video signal to allow the interrogator to test perception.
    *   Includes a "hatch" to pass physical objects.
    *   To pass this version, the computer also needs:
        *   **Computer Vision:** To perceive objects.
        *   **Robotics:** To move and manipulate objects.

*   **Real-world Application**
    *   Acting humanly is important when AI interacts with people (e.g., chatbots or expert systems explaining a diagnosis).
    *   Programs must follow normal human conventions to be understood.

## Thinking humanly : The Cognitive Modelling Approach
*   Goal: Make a computer think like a human.
*   Understanding the mind requires two methods:
    *   Introspection: Trying to catch our own thoughts.
    *   Psychological Experiments: Observing human behavior.
*   We turn theories of the mind into computer programs.
*   If the program's input/output and timing match human behavior, it proves the program's mechanisms might be similar to human thought.
*   **Cognitive Science:** Combines computer models (AI) and psychology to create testable theories of the mind.
*   AI and Cognitive Science influence each other, especially in vision, language, and learning.


## Thinking rationally : The Laws of Thought Approach
The laws of thought (i.e logic) where decisions/actions/thoughts happen through reason, understanding and is based on evidence and truth.
Rational thinking needs
- logic and reasoning
- evidence-based
- clarity of thought
- consistency

*   Based on logic (developed by logicians in the 19th century).
*   Uses formal notation to represent objects and relations.
*   Programs exist that can solve problems if given enough time and memory (Logicist tradition).
*   **Two Main Obstacles:**
    *   **Translation:** It is hard to turn informal knowledge into strict logical notation.
    *   **Efficiency:** Solving a problem in theory is different from solving it quickly in practice.
*   Even small problems (few dozen facts) can exhaust computer resources without guidance on which reasoning steps to try first.

## Acting rationally
An agent is a entity that is capable of perceiving and interacting with the environment.
> A rational agent is one that makes the best decisions given its situation and knowledge about the environment

**Rational agents work through Perception -> Think -> Act loop.**

> Rational agents have performance measure, available actions to choose from, knowledge, and can learn from actions.
> Rational agents interact with the task environment. This environment determines the complexity of the agent

*   An **Agent** is something that perceives and acts.
*   **Goal:** Do the "right thing" (act rationally to achieve goals).
*   **Comparison with "Laws of Thought":**
    *   The "Laws of Thought" approach focused entirely on correct inferences.
    *   Rationality includes inference but isn't limited to it.
*   **Why correct inference isn't enough:**
    *   Sometimes there is no provably "correct" thing to do, but you must still act.
    *   Some rational actions are reflexes (like pulling a hand from a hot stove) and don't involve logical reasoning.
*   **Requirements:**
    *   Rational agents still need the "Cognitive Skills" from the Turing Test (NLP, Knowledge Representation, Reasoning) to make good decisions.
*   **Limited Rationality:**
    *   Perfect rationality (always doing the absolute best thing) is impossible in complex environments due to high computational demands.
    *   Limited Rationality is acting appropriately even when you don't have enough time to calculate everything.