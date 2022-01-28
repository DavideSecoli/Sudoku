# Description
This is a program of an agent that optimally solves any Sudoku games in under 4μs using backtracking depth-first search with constraint propagation

# Sudoku Solver: 

Sudoku is played on a grid of 9 x 9 spaces. Within the rows and columns are 9 “squares” (made up of 3 x 3 spaces). Each row, column and square (9 spaces each) needs to be filled out with the numbers 1-9, without repeating any numbers within the row, column or square. 

The sudoku.ipynb file contains an implementation of a solver function called sudoku_solver which is capable of solving most hard Sudoku puzzles in ~5 milliseconds using a standard Apple M1 Chip and 8GB of memory. 


Algorithmic choices, implementation and optimisation: 

The solver implementation leverages the power of constraint propagation by implementing two strategies: 

If a square has only one possible value, then eliminate that value from the    square's groups 
If there’s only one possible place for a value, put the value there

The main operation is not assigning a value, but rather deleting possible values for any given square. In the code, this is implemented by the delete(values_left, sq, digit). In turn allocate(values_left, sq, digit) eliminates all the values from the square sq except for digit d.
This allows to keep the search space to a minimum and benefit from faster conversion.

The solve(values_left) function first checks that a solution or error is found and if not, chooses one unfilled square considering all its possible values. If a position fails, goes back and considers another value. This is a depth-first search because recursively considers all possibilities before trying a different value.

To keep each branch of the search tree independent, on each recursive call to solve()  a copy of values_left is created. This has proven to be an efficient implementation driven by a careful data structure choice. More detail in the section below. 
In the solve() function, two implementations were made to make it more efficient: square and value ranking. 
Square ranking uses a common heuristic called minimum remaining values, which chooses the square with the minimum number of possible values.
Value ranking considers the digits in numeric order.

In terms of data structure, as per assignment guidelines, sudoku_solver takes in a 9x9 Numpy array and returns an equally shaped array with the correct solution or one with -1s to indicate it’s unsolvability. As described above given the nature of the problem, internally within functions, a dictionary with each of the 81 squares  from A1 to I9 is used as keys and 1-9 digits in string format (instead of a set or list). After several trials this turned out to be the most efficient solution because strings allow the use of copy() instead of copy.deepcopy() that would be needed if Python set or list was used. 




# References: 

https://sudoku.com/how-to-play/sudoku-rules-for-complete-beginners/  

https://www.conceptispuzzles.com/index.aspx?uri=puzzle/sudoku/techniques

http://www.cs.cornell.edu/courses/cs4700/2011fa/lectures/05_CSP.pdf 
