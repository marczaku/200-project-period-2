# Part 1
Please submit a topic of your choice for this assignment. It should:
- be some kind of pathfinding problem
  - e.g. finding a way or the best way from A to B
  - e.g. solving a puzzle
  - e.g. beating an opponent in a turn-based game
- be a unique problem in some way
  - e.g. have unconventional types of movement
  - e.g. not be sudoku or a standard moving puzzle
  - e.g. not be chess or tic-tac-toe

# Part 2
Please submit a link to the results of your assignment work.

## Requirements:
- Your Application needs to face a Pathfinding Problem of some kind.
- A Graph Representation of some sort (Grid, Graph, Mesh) needs to be created for the Problem's States by you. 
  - Manually creating or defining it counts as creating.
- A Visual Representation of the current State needs to be created.
  - Text counts as a Visual Representation in a Console Application.
- Your Application needs to use a Pathfinding Algorithm of your choice to solve the Problem.
- Your Application needs to show the solution of your Problem.
  - The Path of the solution is important.
  - Not just the Final Step.
  - Consider running it Step by Step (WaitForSeconds) or displaying the full Path, if applicable.
- All above points need to be documented in your Repository's README.md.
  - What is the problem.
  - What Algorithm & Data Structure did you choose and why is it suitable?
  - Would there have been alternatives?

## Passing Criteria:
- The student has provided a Pathfinding Problem and was able to visualize and solve it.
- The documentation demonstrates the decisions that were made for solving the problems in an understandable manner.
- If the approach has failed
  - there is a visible attempt at solving a complex problem 
  - and the steps are documented understandably

## Excellent Criteria:
- All from before and furthermore: The Problem is special in its complexity and requires a custom-tailored solution.
- The documentation supports the decision-making and demonstrates the uniqueness of the problem.
- This does not require the student to reinvent a pathfinding Algorithm, but the Data-Structure or the problem of the game may require a custom approach for creating the Graph.

# Where to start?

## 1. Find a problem that you'd like to solve.
A few characteristics of a problem:
- All States Are Visible right away
  - Else: You have to Rebuild the Graph as new information is gained.
  - Else: You also need to sometimes make moves that don't bring you to the Goal, just to get further. (Bug-Algorithm)
- There is no opponent that can do unexpected Moves (Easy)
  - Else: Your algorithm has to avoid running into traps.
- There is always a solution
  - Else: Your algorithm has to handle unsolvable problems.

## 2. Develop a Data Model for the Start-State
- What defines any state of your problem?
- What does your exact state look like?
- e.g. Tic-Tac-Toe: 9 empty cells

## 3. Create a View for The Data Model
- Visualize the Game State on the Screen.
- e.g. Console ASCII Output

## 4. Develop a Data Model for the Target-State
- Sometimes, there's exactly one Target State, sometimes, there's various possible Target States in this case, you don't do if(state == target_state), but rather if(is_target_state(state)) where you for example check Win Conditions.
- e.g. in Tic-Tac-Toe, each state with a filled row or column or diagonal is a Target-State

## 5. Develop a Data Model for the State Transitions and Adjacent States
- What Moves are possible?
- Do they come at costs or risks?
- You don't need to create a full Grid on Start.
- But you need to have rules that tell you, what other States are reachable from one State to another.
- e.g. in Tic-Tac-Toe many moves are possible, but not all
  - e.g. if Player has lost, the game is over
  - and if one Player has made a turn, it's the other player's turn

## 6. Choose a Pathfinding Algorithm
- Choose the best fitting algorithm and run it. Receive a Path.
- e.g. MinMax-Algorithm

## 7. Execute the Path
- Execute the Path with all its connections step by step on the View.
- e.g. Show each turn one by one with a one second delay.

## 8. Replace your Repository's README your own Documentation
- As specificed in the Requirements.

## 9. Bonus (Advanced):
- Can you create Random Start States or Target States for the Problem?
- Can you make sure that your generated States are solvable?
- Can you make it Playable with a "Solve From Here"-Button?
- Maybe you can make a "Suggest Next Move"-Button?
