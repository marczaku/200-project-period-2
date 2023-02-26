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

When describing your pathfinding problem, it would be helpful to include the following components:

- **Problem statement**: Clearly state the problem you are trying to solve. For example, finding the shortest path from point A to point B on a map with obstacles.
- **Constraints**: Describe any limitations or constraints that need to be considered. For example, some areas on the map may be inaccessible or there may be a limit on the number of moves.
- **Rules**: Explain any rules or guidelines that need to be followed. For example, if you are solving a puzzle, there may be rules about how pieces can be moved.
- **Unique aspects**: Highlight what makes your problem unique. This could be a particular type of movement that is not usually encountered, a novel way of scoring or winning, or any other unconventional feature that sets your problem apart from others.
- **Approaches**: Discuss different approaches that can be used to solve the problem. This could include algorithms, heuristics, or other techniques that have been successful in similar problems.
- **Potential applications**: Describe any potential applications or real-world scenarios where this problem might be encountered.

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
- Furthermore, your Repository's README.md should contain documentation:
  - A summary of the problem you're facing
  - What Algorithms & Data Structures did you choose and why are they suitable?
  - Would there have been alternatives?
  - Add screenshots and/or videos

## Passing Criteria:
- The student has provided a Pathfinding Problem and was able to visualize and solve it in an Application.
- The documentation
  - describes the problem
  - demonstrates the decisions that were made for solving the problems (e.g. choice of data structures and algorithms)
  - documents the results with screenshots and/or videos
- If the approach has failed
  - there is a visible attempt at solving a complex problem 
  - and the steps taken are documented understandably
  - the problems/bugs are documented professionally
    - describe the situation
    - describe the expected outcome
    - describe the actual outcome
    - describe possible causes of that issue

## Excellent Criteria:
- All from before and furthermore: The Problem is special in its complexity and requires a custom-tailored solution.
  - e.g. a custom data structure and/or a custom algorithm
- The documentation supports the decision-making and demonstrates the uniqueness of the problem.
- A working build of the pathfinding application is available to test online or to download under Releases.

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

## 2 Develop your Data Model for State and Game

## 2.1 Develop a Written Model for the Start-State
- What defines any state of your problem?
- What does your exact state look like?
- How can you describe your Start State in Words
  - So that if you gave the description to any other person
  - They'd be able to reconstruct the Game only from your notes

Example:
- There is a 2D Map of 8x4 Tiles.
- The Coordinates include x from left to right and y from bottom to top.
- On this map, there is 
  - walls at (4,0) (4,1) (4,3)
  - a closed door at (4,2)
  - the player at (2,2)
  - the goal at (6,2)
  - a key at (0,0)

## 2.2 Identify static Parts of the State
- What are the `static` parts of your problem that don't change?

Example:
- There is a 2D Map of 8x4 Tiles.
- The Coordinates include x from left to right and y from bottom to top.
- On this map, there is 
  - walls at (4,0) (4,1) (4,3)
  - the goal at (6,2)

## 2.3 Identify the variable Parts of the State
- What are the `variable` parts of your problem that can change during the game?

Example:
- The closed door (because it can be opened)
- The player (because he can move)
- The key (because it can be picked up)

## 2.4 Translate your Description into Classes

- Design classes that can hold all the information from above descriptions

Example:

```cs
public class Door {
   public bool isOpen;
   public Vector2Int position;
}
public class Key {
   public bool isPickedUp;
   public Vector2Int position;
}
public class State {
   // this is the variable part
   public Door door;
   public Key key;
   public Vector2Int player;
   
   // this is the static part
   public World world;
}
public class World{
   public bool[,] isWall;
   public Vector2Int goal;
}
```

## 2.5 Create the Start State

- You can use either Code, or the Inspector (if your classes are `[Serializable]`) to create the Start State that you defined in Step 2.1:

```cs
void Awake(){
   var world = new World();
   world.isWall = new bool[8,4];
   // ...
   startState = new State();
   startState.world = world;
   startState.player = new Vector2Int(2, 2);
   // ...
}
```

<img width="255" alt="image" src="https://user-images.githubusercontent.com/7360266/219337137-a0326ddc-2e9c-4fb1-a3aa-7002dd6d9492.png">


## 3. Create a View for The Data Model
- Visualize the Game State on the Screen.
- e.g. Console ASCII Output

One example:
```cs
public class GameView : MonoBehaviour {
   public Transform Player;
   public Transform Goal;
   
   // This function should only visualize the current state on the screen
   // It is not supposed to change anything in the State!!!
   public void UpdateView(State state){
      Player.position = state.playerPosition;
      Goal.position = state.goalPosition;
      Player.color = state.isPlayerBlue ? Color.blue : Color.red;
   }
}
```

## 4. Develop a Data Model for the Target-State
- Sometimes, there's exactly one Target State

```cs
// for a moving puzzle:
var targetState = new State(){
   // all numbers should be in perfect order when the puzzle is solved:
   numbers = new int[]{1,2,3,4,5,6,7,8,9};
}
```

- sometimes, there's various possible Target States in this case, you don't do if(state == target_state), but rather if(is_target_state(state)) where you for example check Win Conditions.

```cs
// e.g. a game where the player needs to get a score of 100 in tetris
// it's unclear, what bricks will be exactly on the screen when he reaches those points
// all you care about is that the score is at least 100
public class State {
   public bool IsWinState(){
      return score >= 100;
   }
}
```

- e.g. in Tic-Tac-Toe, any state with a filled row or column or diagonal is a Target-State
- The exact order of X and O does not matter

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
