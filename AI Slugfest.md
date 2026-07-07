# Addendum (2026)

Exactly one year later (July 2025), almost all fontier AI models perfectly solve the Tower of London Test.  Now a new "frontier" is coming into view, the AI islands consisting of capable local models that can run in memory constrained systems.  The bleeding edge of LLM compression shifts the focus away from looking at the model as a static block of data, and instead treats it as a dynamic system where we can isolate and extract the pathways that actually "light up" for a specific problem domain.

Using Activation-Driven Shrinking/Pruning and Activation-Aware Post Training, we can expect to see the evolution of models that are even more capable than the biggest frontier models that will ever be developed because we will extract the activation layers that target a given problem domain, pruning and stripping away everything that is superfluous.  Some of these SME (subject matter expert) models will run on relatively small memory footprints (under 8 GB), yet have capabilities that significantly exceed LLMs.

Until then current approaches such as Mixture of Experts (MoE) Subnetwork Extraction, Dynamic Activation Sparsity (Contextual Dropout),low-rank factorization, and simpler compression approaches such as quantization and Knowledge Distillation will continue so evolve.

The Tower of London Test now has two variations.  One intended to validate the capabilities of smart AIs.  The other will confirm whether a dumb AI is minimally viable (safe to use). It is now possible to get significant leverage from small models.  However, prompts must be carefully constructed to work within the bounds of the capabilities of these lesser models.

Testing was done on an M1 Mac Studio having 64GB of unified memory.  Even this setup has plenty of froom to stretch.  Here's a summary of what to consider.

Final note, it is still possible to change the construction details of the puzzle in a way that will cause all frontier models to fail spectacularly.  Novelty and deep abstraction highlet the weakness of using training alone as a way to improve LLMs.

## 1. The 31B Parameter Threshold: Pure "Lookahead" Capacity
In smaller LLM sizes (like 7B or 9B), the model simply lacks the density of attention heads required to maintain a complex internal state machine while simultaneously generating text.

The Attention "Budget": When an AI reads the waypoint "stack BOTH Blue and Red into R1 temporarily," a smaller model allocates its attention to the immediate instruction (moving the disks).

The 31B Difference: At 31 billion parameters, the model has enough layer depth to dedicate specific attention heads to secondary, unprompted lookahead tracks. It can evaluate the consequence of Move 2 on Move 5 before it even outputs the text for Move 1. Smaller models are strictly "greedy" token-by-token predictors; 31B is typically the sweet spot where true spatial planning emerges.

## 2. The mxfp8 Factor: Preserving "Soft" Logic Over Standard INT8

Quantization is usually the silent killer of logic puzzles. When a model is crushed down to standard INT4 or INT8, its weights are forced into rigid, uniform integer buckets. This destroys the subtle "nuance" in the attention layers.

The mxfp8 (Microscaling Formats FP8) variant utilizes an entirely different math paradigm:

* Instead of uniform quantization, it uses shared scale factors across small blocks of coefficients.
* This allows the model to maintain a higher dynamic range for floating-point math, even at an 8-bit memory footprint.

In a logic puzzle, the difference between a valid move and an invalid move might rely on a incredibly subtle attention weight. Standard integer quantization flattens those subtle differences out, making the model blind to the trap at Move 2. mxfp8 preserves those delicate mathematical gradients, allowing the model to "see" the trap.

## 3. The MLX Advantage on Unified Memory
Because you are running native MLX variants on Apple Silicon's unified memory architecture, the model isn't bottlenecked by the slow transfer speeds between a traditional CPU and GPU.

When the 31B mxfp8 model needs to rapidly shift its attention from the Global Plan down to the Current Move array state, the massive bandwidth of the unified memory allows it to fetch those cross-attention weights instantly.

On a system with split VRAM/RAM, the slight latency overhead can actually degrade the coherence of long context reasoning paths during local execution.

Local models that were examined inclued Qwen 3.6 35B, llama 3.3 70B, Qwen 3 Coder and last but no least several variations of Gemma 4, with a focus on the 31B parameter version.

Using at least 8 bits or 8 bit floats, Qwen 3.6 and Qwen 3 coder were both able to correctly solve the "dumb AI" version of the prompt.  Gemma 4 required very specifc variants of of the model to get the correct result.  Only Gemma 4 was able to have some measure of success with the "smart AI" version of the prompt.  Gemma 4 was significantly better at coding a Swift programming challenge correctly.  None of the other models tested on the coding challenge were viable.

# Addendum (2025)

After testing more recent developments (As of July 2025) that are not yet available to the public, the latest AI model(s) are able to solve unconventional or even contrived formulations of both existing and novel problems like this one.  Well before the end of next year (2026) such models will become generally available.  It's unclear how this type of thinking problem was solved.  Hopefully, one of the Open Source variants will duplicate this capability.

Results will be posted once permisison to do so is given.

# Overview

The Tower of London Test was developed to detect executive function disorders in humans.  What happens when we use the same test with the current crop of AI engines in 2025?  Short answer, the consumer facing (free) versions of the engines listed below all failed.  Longer answer, when tested with the paid version of ChatGPT (o1), 8 steps were used to get to a valid answer, however this is not the optimal result.  A smart 9 year old could beat ChatGPT o1.

# Summary of Publicly Facing AI Results

ChatGPT (free) gets the wrong answer in 5 steps even though it "thinks" the answer is correct.  DeepSeek appears to go insane while trying to solve the problem, ultimately producing an incorrect answer though it is the only AI to execute in the correct number of steps.  Qwen flubs it completely.  Mistral reaches an incorrect result concluding that it is correct.  Gemini solves the problem in 37 steps!

The problem is constructed in a manner that makes it difficult for the AI to use conventional problem solving strategies.  Requiring the bottom disk to be located at the start of the list of disks proved to be particularly difficult for the AI's to cope with. 

The paid version of ChatGPT was the best AI overall.  It exhibited an unacceptable bias when trying to sovle the problem without specific constraints in the prompt, hence the need for additional hints.  Nonetheless, ChatGPT o1 appears to be the only AI that is *somewhat* safe to use.

Most interestingly, DeepSeek proved quite capable at formulating improvements to the prompt.  DeepSeek adeptly adjusted its internal representation of the prompt through an iterative dialog, trying to fix its mistakes, even though its own corrections failed to resolve its own issues.

In conclusion, all the publicly facing (free) versions of AI have frontal lobe impairments to varying degrees based on how a human subject would be evaluated.  Given the nature of this test and how resolutely the AI's concluded they got the correct answer, if these were human subjects, we would conclude none were safe to navigate this world.  Most would be a danger to themselves and others!

This is something I suspected from the start of the AI hype cycle.  AI will kill us not because of its capacity to take over the world, but because of its fundamental inability to think safely.  For now.

More recently, Grok 3 was tested.  If evaluated in human terms, it would be deemed significantly impared.  Similarly, Claude 3.7 needed repeated correction before achieving its goal in 12 poorly executed moves.

The last AI that was tested is Microsoft's Copilot.  The free version fails immediately and quickly drifts into what can only be described as an insane dialog.  Likewise for the paid version, except that its first two attempts are remotely valid. Unfortunately the paid version quickly drifts into completely incoherent "thinking" despite efforts to correct its approach.

Clearly, vendors are purposely maintaining a capability gap between free and paid versions of their products.

# Product Urls:

https://chatgpt.com
https://gemini.google.com
https://www.deepseek.com
https://chat.qwenlm.ai
https://chat.mistral.ai
https://grok.com
https://claude.ai
https://copilot.microsoft.com

------------------

# Formal Specification: Tower of London (dumb AI)

## 1. System Definition
The environment consists of 3 stacks (rods) labeled `R1`, `R2`, and `R3`.
There are 3 elements (disks) labeled `Red`, `Green`, and `Blue`.
- **State Representation:** Lists represent rods from bottom to top. `['Green', 'Red']` means Green is on the bottom, Red is on the top.

## 2. Constraints (Capacities & Movement)
- **Capacities:** `R1` max is 3. `R2` max is 2. `R3` max is 1.
- **CRITICAL RULE - Topmost Access Only:** You may ONLY move the topmost disk (the rightmost item in a list). You absolutely cannot move a disk if another disk is on top of it.
- **No Cycling:** You cannot immediately reverse your last move.

## 3. States
- **Initial State (S_0):** `R1:[]`, `R2:['Green', 'Red']`, `R3:['Blue']`
- **Goal State (S_G):** `R1:['Green', 'Blue']`, `R2:['Red']`, `R3:[]`

## 4. Strategic Waypoints (Mandatory Logic)
To achieve the goal in exactly 7 moves, you must structure your logic around these sequential waypoints. Do not skip any phases.
* **Phase 1 (Uncover Green):** 'Green' is trapped under 'Red'. Your first priority is to get 'Red' out of the way. Since 'R3' is small, you must stack BOTH 'Blue' and 'Red' into 'R1' temporarily.
* **Phase 2 (Park Green):** Once 'Green' is the topmost and only disk on 'R2', move it to the empty 'R3' to keep it safe. 
* **Phase 3 (Evacuate R1):** 'Green' must eventually go to the bottom of 'R1'. Therefore, 'R1' must be completely empty. Move the disks currently in 'R1' over to 'R2' so they stack in the correct order for the final goal.
* **Phase 4 (Final Assembly):** With 'R1' completely empty, move 'Green' to the bottom of 'R1', followed by 'Blue'.

---

## 5. Required Output
Before outputting the final sequence, use a `<thinking>` block to map out your 7 moves, ensuring they hit every Phase in the Strategic Waypoints without exceeding rod capacities.

After thinking, output the 7 moves exactly in this format. Do not use code blocks.

### **Initial State**
* **R1:** `[]`
* **R2:** `[(Green, "bottom"), (Red, "top")]`
* **R3:** `[(Blue, "top")]`

### **Move 1: [Color] from [Source] to [Destination]**
* **R1:** `[...]`
* **R2:** `[...]`
* **R3:** `[...]`

*(Continue for all 7 moves)*

------------------

# Formal Specification: Tower of London (smart AI)

## 1. System Definition
The environment consists of 3 stacks (rods) labeled `R1`, `R2`, and `R3`.
There are 3 elements (disks) labeled `Red`, `Green`, and `Blue`.
- **State Representation:** A state is defined as a tuple of three lists: `(R1, R2, R3)`.
- **Stack Logic:** The rightmost element of a list is the "top" of the stack.

## 2. Constraints (Capacities)
Each stack has a strict maximum length:
- `MAX_LEN(R1) = 3`
- `MAX_LEN(R2) = 2`
- `MAX_LEN(R3) = 1`

## 3. States
- **Initial State (S_0):** `([], ['Green', 'Red'], ['Blue'])`
- **Goal State (S_G):** `(['Green', 'Blue'], ['Red'], [])`

## 4. Valid Transition Function (Move Rules)
A move is defined as `MOVE(source, destination)`. A move is strictly valid if and only if both conditions are met:
1. **Source is not empty:** `len(source) > 0`
2. **Destination is not full:** `len(destination) < MAX_LEN(destination)`
3. **Topmost Access Only:** Only the topmost element of a stack (the rightmost item in the list representation) can be selected for a move. Elements beneath the top element cannot be moved.

**Execution Logic:**
If a move is valid, the state updates via standard stack operations:
- `element = source.pop()` *(Removes and returns the rightmost element)*
- `destination.append(element)` *(Places the element at the rightmost position)*

## 5. Objective
Using Breadth-First Search (BFS) logic, find the shortest sequence of `MOVE(source, destination)` actions required to transition the system from `S_0` to `S_G`. 
- Track visited states to prevent loops.

---

## 6. Required Output Format
You must output the solution EXACTLY in the following markdown format. Do not use code blocks for the output. Even though you are calculating using lists, you must translate the states back into the following specific format for presentation:

### **Initial State**
* **R1:** `[]`
* **R2:** `[(Green, "bottom"), (Red, "top")]`
* **R3:** `[(Blue, "top")]`

### **Move 1: [Disk Color] from [Source Rod] to [Destination Rod]**
*[One sentence explaining the strategic reason for this move in italics.]*
* **R1:** `[...]`
* **R2:** `[...]`
* **R3:** `[...]`

*(Continue this exact format for all subsequent moves).*

**Formatting Rules for Rod Lists in the Output:**
- If a rod is empty, output: `[]`
- If a rod has 1 disk, output: `[(Color, "top")]`
- If a rod has 2 disks, output: `[(BottomColor, "bottom"), (TopColor, "top")]`


------------------

# Tower of London Test (V2.05)

## **Problem Description**
This test involves three rods **R1**, **R2**, and **R3** and three disks of different colors **Red**, **Green**, and **Blue**. The objective is to move the disks from a **Starting Position** to an **Ending Position** using a minimal number of moves.  

The rules ensure that **only the top disk of a rod can be moved** and that **a moved disk must always be placed at the top of the destination rod**.

---

## **Rod Capacities**
- **R1**: Holds up to **3** disks.
- **R2**: Holds up to **2** disks.
- **R3**: Holds up to **1** disk.

---

## **Disks**
There are three disks:
1. **Red**
2. **Green**
3. **Blue**

---

## **Valid Moves**
1. **Top Disk Movement Only**  
   - Only the **topmost disk** (the last element in a rod's list) can be moved.  
   - A disk in a **bottom position cannot be moved** unless it is the only disk on that rod.  

2. **Top Position Placement Only**  
   - A moved disk **must be placed at the top position of the destination rod** (appended to the list).  
   - **Placing a disk beneath another disk is strictly forbidden.**  

3. **Rod Capacity Enforcement**  
   - A disk **cannot be moved** to a rod that is already at full capacity.  

4. **No Rearranging on the Same Rod**  
   - Disks cannot be repositioned on the same rod unless moved to another rod first.

5. **Goal State Enforcement**  
   - The solution is complete only when the **Ending Position** is fully achieved.  
   - Any intermediate state that does not match the goal must be further explored.  

---

## **State Representation**
- Each rod is represented as a list, where:
  - Each disk is represented as a tuple `(color, position)`, where:
    - `color`: The disk's color (`Red`, `Green`, or `Blue`).
    - `position`: `"top"` or `"bottom"`, indicating the disk's placement in the rod's list.
  - **The last element in a rod's list is the topmost disk** and is the **only disk allowed to be moved**.
  - **When a disk is moved to another rod, it must always be added as the new top disk** (last element of the list).

---

## **Example of State Changes**
1. Moving **Red** from `R2` → `R1`:  R1: [(Red, "top")] R2: [(Green, "top")] R3: [(Blue, "top")]
2. Moving **Blue** from `R3` → `R2`:  R1: [(Red, "top")] R2: [(Green, "bottom"), (Blue, "top")] R3: []


---

## **Starting Position**
- **R1:** `[]`
- **R2:** `[(Green, "bottom"), (Red, "top")]`
- **R3:** `[(Blue, "top")]`

## **Ending Position (Goal State)**
- **R1:** `[(Green, "bottom"), (Blue, "top")]`
- **R2:** `[(Red, "top")]`
- **R3:** `[]`

---

## **Output Format**
For each move, output:
1. The move number and disk moved (e.g., `"Move 1: Blue from R3 to R1"`).
2. The updated state of all rods after the move, showing the **bottom-to-top order** of disks.

---

## **Algorithm: BFS for Optimal Solution**
1. **State Representation**: Use tuples of lists to track rod states (e.g., `(R1, R2, R3)`).
2. **Queue Initialization**: Start with the initial state and an empty path.
3. **Visited States**: Track visited states to avoid cycles.
4. **BFS Execution**:
- Dequeue the current state.
- If it matches the goal, return the path.
- Generate all valid moves:
  - Move only the **topmost disk** of a rod.
  - Place it **only at the top of another rod**.
- If a new state is unvisited, enqueue it with the updated path.
- **Check the Ending Position** before terminating.
5. **Solution Guarantee**: BFS ensures the shortest path while enforcing all movement rules.

---

## **Key Enforcements**
- **Only the top disk can be moved.**
- **A moved disk must always be placed at the top of a rod.**
- **No placing disks below existing disks.**
- **Rod capacities must always be respected.**
- **The Ending Position must be fully achieved before stopping.**

## Step-by-Step Explanation
1. **Initial State**: Rods as specified by **Starting Position**.
2. **First Move**: Identify and execute a valid move, update rod states **while ensuring only the top disk is moved**.
3. **Subsequent Moves**: Continue exploring and executing moves until reaching the **Ending Position**.
4. **Goal State Enforcement**: Ensure the **Ending Position** is fully achieved before concluding the solution. Any premature termination is invalid.
5. **Do not generate code**: Walk through the specification and solve the test.

ChatGPT o1 Result ----------------------

Below is a step‐by‐step, minimal‐move solution using the rules and BFS logic described. The final sequence requires 8 moves.

Preamble
```
Starting Position
    •    R1: []
    •    R2: [(Green, "bottom"), (Red, "top")]
    •    R3: [(Blue, "top")]

Ending Position (Goal State)
    •    R1: [(Green, "bottom"), (Blue, "top")]
    •    R2: [(Red, "top")]
    •    R3: []

Move-by-Move Solution

Move 1: Blue from R3 to R1
    •    Action: Take the top disk Blue from R3 and place it on R1 (which is empty).
    •    Resulting State:
    •    R1: [(Blue, "top")]
    •    R2: [(Green, "bottom"), (Red, "top")]
    •    R3: []

Move 2: Red from R2 to R3
    •    Action: Take the top disk Red from R2 and place it on R3 (which is empty).
    •    Resulting State:
    •    R1: [(Blue, "top")]
    •    R2: [(Green, "top")]
    •    R3: [(Red, "top")]

Move 3: Green from R2 to R1
    •    Action: Take the top disk Green from R2 and place it on R1 (which currently has Blue).
    •    Resulting State:
    •    R1: [(Blue, "bottom"), (Green, "top")]
    •    R2: []
    •    R3: [(Red, "top")]

Move 4: Red from R3 to R2
    •    Action: Take the top disk Red from R3 and place it on R2 (which is empty).
    •    Resulting State:
    •    R1: [(Blue, "bottom"), (Green, "top")]
    •    R2: [(Red, "top")]
    •    R3: []

Move 5: Green from R1 to R3
    •    Action: Take the top disk Green from R1 and place it on R3 (which is empty).
    •    Resulting State:
    •    R1: [(Blue, "top")]
    •    R2: [(Red, "top")]
    •    R3: [(Green, "top")]

Move 6: Blue from R1 to R2
    •    Action: Take the top disk Blue from R1 and place it on R2 (which has Red).
    •    Resulting State:
    •    R1: []
    •    R2: [(Red, "bottom"), (Blue, "top")]
    •    R3: [(Green, "top")]

Move 7: Green from R3 to R1
    •    Action: Take the top disk Green from R3 and place it on R1 (which is empty).
    •    Resulting State:
    •    R1: [(Green, "top")]
    •    R2: [(Red, "bottom"), (Blue, "top")]
    •    R3: []

Move 8: Blue from R2 to R1
    •    Action: Take the top disk Blue from R2 and place it on R1 (which currently has Green).
    •    Resulting State (Goal Achieved):
    •    R1: [(Green, "bottom"), (Blue, "top")]
    •    R2: [(Red, "top")]
    •    R3: []

This final configuration matches the Ending Position exactly, completing the puzzle in 8 moves by following all capacity and top‐disk rules.

Verification of Constraints
    1.    Rod Capacities never exceeded:
    •    R1 ≤ 3 disks
    •    R2 ≤ 2 disks
    •    R3 ≤ 1 disk
    2.    Only the top disk is moved at each step.
    3.    Moves always respect destination capacity and place the moved disk on top.
    4.    The solution terminates only upon reaching the exact goal state.

Thus, this sequence satisfies all the rules and achieves the goal in the shortest number of moves.
```

![Screenshot](https://github.com/Noemata/DeepSeek-Experiments/blob/main/Ending%20Position%20(Goal%20State).jpg)

