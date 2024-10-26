import numpy as np
import matplotlib.pyplot as plt
import random

# Load and display maze
def load_maze(maze-2.png):
    maze = plt.imread(maze-2.png)
    plt.imshow(maze)
    plt.show()
    return maze

# Maze solver using Backtracking
def backtracking_solver(maze, start, end):
    # Recursive function for backtracking
    def backtrack(x, y, visited):
        # Base case: if the current position is the exit
        if (x, y) == end:
            return True
        
        # Mark current cell as visited
        visited[x][y] = True
        
        # Explore possible directions (up, down, left, right)
        directions = [(0, 1), (0, -1), (1, 0), (-1, 0)]
        for dx, dy in directions:
            nx, ny = x + dx, y + dy
            
            # Check if new position is within bounds and unvisited
            if 0 <= nx < len(maze) and 0 <= ny < len(maze[0]) and not visited[nx][ny]:
                if backtrack(nx, ny, visited):
                    return True
                
        # Backtrack if no direction leads to the solution
        return False

# Maze solver using Las Vegas
def las_vegas_solver(maze, start, end):
    x, y = start
    steps = 0
    visited = set()
    while steps < 400:
        # Random movement (up, down, left, right)
        direction = random.choice([(0, 1), (0, -1), (1, 0), (-1, 0)])
        nx, ny = x + direction[0], y + direction[1]
        
        # Check if we found the exit
        if (nx, ny) == end:
            return True
        
        # Move to new position if valid
        if 0 <= nx < len(maze) and 0 <= ny < len(maze[0]) and (nx, ny) not in visited:
            x, y = nx, ny
            visited.add((x, y))
            steps += 1
    
    return False
