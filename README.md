# Maze-generator-and-solver
Maze is generated using recursive deep search method and is solved using dijkstra's algorithm. Pygame is used for the visualization software and python is used for coding.
1.	Introduction
This project has two algorithmic parts to it. The first one is about generating the 20x20 grid sized maze and second one is about solving it. There are a total of 400 cells named from 0 to 399. The first row contains the cells from 0 to 19. The second row contains cells from 20 to 39 and so on. 
The language we have used over here for the complete program is python, as it is easy to understand. In order to visualize all this, we have used pygame as our animation software.

The generation of maze is done by the Recursive deep first search algorithm. While carving the maze itself, a map stores the parent of all vertices as we proceed while carving the maze. Hence, we have the shortest path ready with us by the time whole maze is carved out. 
As an additional solution to it using the very famous Dijkstra’s algorithm, we have created that function in such a way that it takes two arguments in it. One is the source vertex and other is destination vertex. So, the shortest possible route from the source vertex to the destination vertex will be plotted.

Note: The code link is given here. This complete code is unique and is not exactly copied from anywhere. Many additional features and functions are added to the code and will be also developed further in future.

 
Figure 1. The visual representation of generation of 20x20 maze carved from a 20x20 grid.
 
Figure 2. The shortest possible path plotted using the map that we created while carving the maze.

 
Figure 3. The maze solved using Dijkstra’s Algorithm for the source vertex as 19 (row 0 and column 19) and destination vertex as 159 (row 8 and column 19).

2.	Problems faced
We had no clear idea that how a 20x20 maze can be put into the program such that computer can read that out. There was some intuition that graph as the data structure could be used to represent this maze, but we were not able to figure it out. 

The foremost challenge was how to represent the maze with the help of graph? The next challenge was representing the project with the help of visualizer. Pygame was quite new for us to understand. The arguments given to the functions in pygame is usually in the unit of pixels. So, it became quite obvious to make functions like converting the pixel number to the corresponding vertex or cell number and vice versa. 
 
Figure 4. shows the initial pygame setup (like colour selection and describing the size of cells) before creating the maze.










3.	Maze Generation
For the generation of maze, we have used the Recursive deep first search algorithm. Recursive deep first search algorithm goes as follows:
1.	Given a current cell as a parameter,
2.	Mark the current cell as visited
3.	While the current cell has any unvisited neighbor cells
1.	Choose one of the unvisited neighbors
2.	Remove the wall between the current cell and the chosen cell
3.	Invoke the routine recursively for a chosen cell

How the maze is represented in the form of graph?
To represent the maze in pygame visualizer, we will first build the 20x20 grid with the help of white lines and then carve the maze out of it using the ocean blue color. To represent the maze in the form of graph surely, we will need an adjacency matrix. Since it is a 20x20 maze, there would be 400 cells and to show the connections of these 400 cells we would require a 400x400 matrix. 

We will also require a 20x20 bool matrix to keep a track of visited cells. Along with that, we will also use a stack to keep the history of cells we came across. A HashMap would be required to store the parent of respective cells in which the shortest path would be stored. 
 
Figure 5. explains how the above-mentioned data structures are set up in python code.
 
Figure 6. shows the main function of our program where in, 4 functions are called one by one.

The first function buil_grid (40, 0, 20) will make the 20x20 grids using white lines. 
The second function carve_out_maze (x, y) will carve the maze from the grid made using function 1 as shown in figure 1.
The third function plot_route_back (400, 400) will plot the shortest possible path from top-left corner to bottom-right corner using the map that we store while carving the maze as shown in figure 2.
The fourth function dijkstra (19, 159) will plot the shortest possible path from cell 19 to 159 as shown in figure 3.

Let us understand the maze generation on a smaller 4x4 grid.
  
The “Graph to be built” contains total 16 cells numbered from 0 to 15. And as mentioned before, we have a stack and a bool matrix named as “visited”. 
 
Suppose, we start from the cell 12. So, let’s mark the same cell as visited and also add it to the stack. Here, the pointer has two available neighbours. One is 8 (top) and other is 13 (right). 
 
Let’s say that cell selects to go to its top neighbour. So, we will mark cell 8 as visited and will add it to the stack. Further, in the solution dictionary (HashMap) 12 is marked as parent of 8. So, the cell 12 and 8 are now connected to each other (i.e., adjacenecy_matrix[12][8] and adjacenecy_matrix[8][12] are given the weights 1). 

To represent this in our visualizer, rather than removing the wall between cell 8 and 12, we will overwrite the grid with blue colour to make them look like the wall has been removed.

Similarly, now the cell has again 2 options to move upwards or rightwards. 
  
Suppose the cell moves rightwards. So, the same process repeats and the connections in the graph are respectively made.
 
 
 
Now, here the cell has no further option to move because all the neighbour cells are already visited. So, using the stack the pointer will now backtrack to the previous cell and look for the unvisited neighbour cells. 
 
 
 
 
 
 
 
 
 
 
 
 
 
Now, all the cells are marked visited which means our graph representation is ready, both in the adjacency matrix form and the pygame visualizer form.

Code in python
 
The first function runs and hence the 20x20 grid is generated.
 
 
 
To support the carve_out_maze function we require to create the following sub-functions that help it. Refer the code comments for better understanding.
 
 
 










4.	Solving the maze
Using the Recursive Backtracking
As mentioned earlier, the “solution” HashMap already contains the respective parent of each and every cell, which was created while carving the maze. So, to find the shortest possible path from cell to cell 399, we will ask cell 399 to go its parent cell and then further asking for their parent cells till we reach cell 0 (whose parent is -1).
 
So, after running this function we will have our shortest path plotted in yellow square shaped signs as shown in figure 2. 

Using the Dijkstra’s Algorithm
Once, the graph is represented in the form of adjacency matrix, it is not that difficult to implement the Dijkstra’s algorithm to find the shortest path. Since, we have covered this algorithm in our academics too. This function will return the list starting from the destination cell to the source cell, which gives the shortest possible path. 
 
 
Hence, running this function will plot the shortest path from the given source cell to the destination cell as shown in figure 3.
