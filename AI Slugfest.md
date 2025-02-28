# Overview

The Tower of London Test was developed to detect executive function disorders in humans.  What happens when we use the same test with the current crop of AI engines in 2025?  Short answer, the consumer facing (free) versions of the engines listed below all failed.  Longer answer, when tested with the paid version of ChatGPT (o1), 8 steps were used to get to a valid answer, however this is not the optimal result.  A smart 9 year old could beat ChatGPT o1.

# Summary of Publicly Facing AI Results

ChatGPT (free) gets the wrong answer in 5 steps even though it "thinks" the answer is incorrect.  DeepSeek appears to go insane while trying to solve the problem, ultimately producing an incorrect answer though it is the only AI to execute in the correct number of steps.  Qwen flubs it completely.  Mistral reaches an incorrect result concluding that it is correct.  Gemini solves the problem in 37 steps!

The problem is constructed in a manner that makes it difficult for the AI to use conventional problem solving strategies.  Requiring the bottom disk to be located at the start of the list of disks proved to be particularly difficult for the AI's to cope with. 

The paid version of ChatGPT was the best AI overall.  It exhibited an unacceptable bias when trying to sovle the problem without specific constraints in the prompt, hence the need for additional hints.  Nonetheless, ChatGPT o1 appears to be the only AI that is *somewhat* safe to use.

Most interestingly, DeepSeek proved quite capable at formulating improvements to the prompt.  DeepSeek adeptly adjusted its internal representation of the prompt through an iterative dialog, trying to fix its mistakes, even though its own corrections failed to resolve its own issues.

In conclusion, all the publicly facing (free) versions of AI have frontal lobe impairments to varying degrees based on how a human subject would be evaluated.  Given the nature of this test and how resolutely the AI's concluded they got the correct answer, if these were human subjects, we would conclude none were safe to navigate this world.  Most would be a danger to themselves and others!

This is something I suspected from the start of the AI hype cycle.  AI will kill us not because of its capacity to take over the world, but because of its fundamental inability to think safely.  For now.

More recently, Grok 3 was tested.  If evaluated in human terms, it would be deemed significantly impared.  Similarly, Claude 3.7 needed repeated correction before achieving its goal in 12 poorly executed moves.

# Product Urls:

https://chatgpt.com
https://gemini.google.com
https://www.deepseek.com
https://chat.qwenlm.ai
https://chat.mistral.ai
https://grok.com
https://claude.ai

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

