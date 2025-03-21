# Grid-Based Robot Navigation with A* and IDA* Algorithms

This repository (CSE366_Assignment1) contains implementations of two advanced pathfinding algorithms—A* and IDA*—for grid-based robot navigation. The simulation demonstrates how these algorithms perform in environments with obstacles, allowing for comparison of their efficiency, path quality, and computational characteristics.

## Table of Contents
- [Introduction](#introduction)
- [Setup Instructions](#setup-instructions)
- [Running the Simulations](#running-the-simulations)
- [Algorithm Details](#algorithm-details)
  - [A* Implementation](#a-implementation)
  - [IDA* Implementation](#ida-implementation)
- [Analysis and Observations](#analysis-and-observations)
- [Challenges and Solutions](#challenges-and-solutions)
- [Future Improvements](#future-improvements)

## Introduction

This project explores pathfinding in grid-based environments using two advanced algorithms: A* and IDA* (Iterative Deepening A*). The simulation features an agent navigating through a grid containing barriers to reach randomly placed tasks. The implementation allows for direct comparison of these algorithms' performance characteristics, showcasing their strengths and limitations in practical applications.

## Setup Instructions

### Requirements
- Python 3.6 or later
- Pygame library

### Installation

1. Clone this repository to your local machine:
```
git clone https://github.com/yourusername/CSE366_Assignment1.git
```

2. Navigate to the repository:
```
cd CSE366_Assignment1
```

3. Install required dependencies:
```
pip install pygame
```

## Running the Simulations

The repository is organized into two main folders—`A_Star` and `IDA_Star`—each containing a complete implementation of the respective algorithm.

### To run the A* simulation:

```
cd A_Star
python run.py
```

### To run the IDA* simulation:

```
cd IDA_Star
python run.py
```

### Simulation Controls:
- Click the "Start" button to begin the simulation
- The agent (blue square) will automatically navigate to tasks (red squares with numbers)
- The simulation tracks task completion and path costs in the status panel
- Close the window to end the simulation

## Algorithm Details

### A* Implementation

The A* algorithm uses a best-first search approach with an open list (priority queue) and a closed set to find the optimal path from start to goal. Key features of our implementation:

- **Priority Queue Management**: Uses Python's `heapq` module to efficiently manage the open list
- **Heuristic Function**: Implements Manhattan distance as the heuristic
- **Path Reconstruction**: Traces the path backward from goal to start using the `came_from` map
- **Memory Usage**: Stores all visited nodes in memory for efficient lookup
- **Completeness**: Guaranteed to find the optimal path if one exists

The A* implementation can be found in `A_Star/agent.py` in the `find_path_to` method.

### IDA* Implementation

The IDA* algorithm uses iterative deepening with a depth-first search approach to find optimal paths while using less memory. Key features:

- **Recursive Implementation**: Uses a recursive function for depth-first search
- **Iterative Deepening**: Gradually increases the cost limit until a path is found
- **Cycle Detection**: Avoids revisiting nodes in the current path
- **Memory Efficiency**: Uses memory proportional to the path length rather than the number of nodes
- **Optimality**: Guarantees finding the optimal path with minimal memory usage

The IDA* implementation can be found in `IDA_Star/agent.py` in the `find_path_to` method.

## Analysis and Observations

Both algorithms have been tested in various grid configurations with different numbers of tasks and barriers. Key observations include:

1. **Memory Usage**:
   - A* maintains an open list and closed set, requiring more memory for large grids
   - IDA* uses memory proportional to the path depth, making it more memory-efficient for large grids

2. **Speed**:
   - A* generally finds paths faster in open environments
   - IDA* may re-explore the same states multiple times, potentially making it slower in some scenarios
   - In constrained environments with many barriers, the performance gap narrows

3. **Path Quality**:
   - Both algorithms produce optimal paths with the same length when using the same heuristic
   - Path visualization shows identical routes for the same start/goal configurations

4. **Grid Size Impact**:
   - A* performance degrades more noticeably as grid size increases
   - IDA* maintains consistent memory usage regardless of grid size

5. **Task Completion Strategy**:
   - Both implementations use a "nearest task first" approach
   - The path cost tracking shows the cumulative effort required to complete all tasks

## Challenges and Solutions

1. **Memory Management for A***:
   - **Challenge**: A* can exhaust memory on very large grids.
   - **Solution**: Implemented a bounded A* variant that limits the size of the open set.

2. **Stack Overflow in IDA***:
   - **Challenge**: Deep recursion in IDA* can lead to stack overflow.
   - **Solution**: Implemented a maximum depth limit to prevent excessive recursion.

3. **Performance Optimization**:
   - **Challenge**: Initial implementations were slow for complex environments.
   - **Solution**: Optimized neighbor generation and heuristic calculations for both algorithms.

4. **Path Visualization**:
   - **Challenge**: Displaying the search process effectively.
   - **Solution**: Added step-by-step movement with delays to visualize the agent's decision-making process.

5. **Cost Function Accuracy**:
   - **Challenge**: Ensuring consistent cost tracking across implementations.
   - **Solution**: Standardized the cost calculation and added detailed logging in the status panel.

## Future Improvements

- Implement a hybrid approach that switches between A* and IDA* based on grid properties
- Add visualization of the search space exploration for educational purposes
- Incorporate weighted edges for more realistic terrain representation
- Implement dynamic obstacles that change position during navigation
- Add multi-agent pathfinding scenarios to test coordination
