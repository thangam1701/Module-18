# Experiment 12(d): Travelling Salesman Problem (TSP)

## Aim
To write a Python program to find the shortest possible route that visits every city exactly once and returns to the starting point using the Travelling Salesman Problem (TSP) approach.

---

## Algorithm

1. **Input the Number of Cities**:
   - Begin by taking the number of cities as input.
   
2. **Distance Matrix**:
   - Define the distance matrix where each element `graph[i][j]` represents the distance between city `i` and city `j`.

3. **Generate All Permutations**:
   - Generate all possible permutations of the cities excluding the starting city.
   
4. **Calculate the Total Cost for Each Permutation**:
   - For each permutation, calculate the total distance of traveling through the cities in that order, starting and ending at the initial city.
   
5. **Track the Minimum Cost**:
   - Keep track of the minimum cost and the corresponding route.

6. **Return the Best Route and Minimum Cost**:
   - Once all permutations are evaluated, return the route with the minimum cost.

7. **End the Program**:
   - Output the minimum cost and the corresponding route.

---

## Program
```
# Python3 program to implement traveling salesman
# problem using naive approach.
from sys import maxsize
from itertools import permutations
V = 4

# implementation of traveling Salesman Problem
def travellingSalesmanProblem(graph, s):

	# store all vertex apart from source vertex
	vertex = []
	for i in range(V):
		if i != s:
			vertex.append(i)

	# store minimum weight Hamiltonian Cycle
	min_path = maxsize
	next_permutation=permutations(vertex)
	for i in next_permutation:

		# store current Path weight(cost)
		current_pathweight = 0

		# compute current path weight
		k = s
		for j in i:
			current_pathweight += graph[k][j]
			k = j
		current_pathweight += graph[k][s]

		# update minimum
		min_path = min(min_path, current_pathweight)
		
	return min_path


# Driver Code
if __name__ == "__main__":

	# matrix representation of graph
	graph = [[0, 10, 15, 20], [10, 0, 35, 25],
			[15, 35, 0, 30], [20, 25, 30, 0]]
	s = int(input())
	print(travellingSalesmanProblem(graph, s))
```

## OUTPUT
![Screenshot 2025-05-18 224202](https://github.com/user-attachments/assets/5f6f27d2-653d-4e05-b569-fd33f436e621)

## RESULT
Thus the program for Travelling Salesman Problem (TSP) is executed Successfully.
