Autonomous Delivery Agent PathfindingThis project, developed for CSA2001-Fundamentals of AI and ML, features an autonomous delivery agent that navigates a 2D grid-based city. The agent is designed to find the most efficient path from a starting point to a goal, considering static obstacles, varied terrain costs, and dynamic obstacles.The simulation implements and compares several fundamental AI search algorithms to solve this pathfinding problem.Features2D Grid City Environment: The agent operates in a grid world loaded from custom map files. The environment can include:Start (S) and Goal (G) points.Static Obstacles (#): Impassable walls.Variable Terrain Costs (1-9): Cells with different movement costs.Dynamic Obstacles (D): Obstacles that appear at specific locations at given times.Pathfinding Algorithms Implemented:Uninformed Search:Breadth-First Search (BFS)Uniform-Cost Search (UCS)Informed Search:A* Search (using Manhattan Distance as a heuristic)Local Search for Replanning:Hill-Climbing with Random Restarts to adapt to unexpected obstacles.Project Structure.
├── maps/
│   ├── dynamic.txt
│   ├── medium.txt
│   └── ... (other map files)
├── src/
│   ├── a_star.py
│   ├── bfs.py
│   ├── grid_city.py
│   ├── local_search.py
│   └── ucs.py
├── main.py
└── README.md
Getting StartedPrerequisitesPython 3.xNo external libraries are required for this project.InstallationClone the repository to your local machine:git clone <your-repository-url>
Navigate to the project directory:cd <repository-name>
Running the PlannersThe main entry point is main.py. You can run the different planning algorithms from your terminal using command-line arguments.Syntax:python main.py <path_to_map_file> <planner_name>
<path_to_map_file>: The relative path to the map file (e.g., maps/medium.txt).<planner_name>: The algorithm to use. Choices are: bfs, ucs, a_star, replan.Usage Examples1. Breadth-First Search (BFS)Finds the shortest path in terms of the number of steps.python main.py maps/medium.txt bfs
2. Uniform-Cost Search (UCS)Finds the path with the lowest total cost, considering terrain.python main.py maps/medium.txt ucs
3. A Search*An informed search algorithm that finds the lowest-cost path more efficiently than UCS by using a heuristic (Manhattan distance).python main.py maps/medium.txt a_star
*4. Dynamic Replanning (A with Hill-Climbing)**This simulation first calculates an optimal path using A*. Then, a "dynamic" obstacle is placed on the path, forcing the agent to replan a new route using a Hill-Climbing local search algorithm.python main.py maps/dynamic.txt replan
Map File FormatThe grid city is defined by .txt files. The characters have the following meanings:S: Starting position of the agent.G: Goal/delivery location..: Standard terrain with a movement cost of 1.#: A static obstacle (wall) that cannot be entered.1-9: Terrain with a higher movement cost, equal to the number's value.D: A cell associated with a dynamic obstacle. The schedule for this obstacle is defined on a separate line at the end of the file.Dynamic Obstacle Schedule:To define a dynamic obstacle, add a line at the end of the map file with the following format:D:<r1>,<c1>,<t1>;<r2>,<c2>,<t2>;...<r>: Row of the obstacle.<c>: Column of the obstacle.<t>: Time step at which the obstacle is at that (r, c) position.Example (dynamic.txt):S...
.D..
...G
D:1,1,2;2,1,3;3,2,3
In this example, the cell at (1,1) is marked as D. The schedule D:1,1,2;2,1,3;3,2,3 means:At time t=2, an obstacle appears at (1,1).At time t=3, an obstacle appears at (2,1).At time t=3, another obstacle appears at (3,2).
