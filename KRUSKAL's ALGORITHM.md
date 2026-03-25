# Experiment 12(b): Kruskal's Algorithm

## Aim
To write a Python program for Kruskal's algorithm to find the Minimum Spanning Tree (MST) of a given connected, undirected, and weighted graph.

---

## Algorithm

1. **Sort all edges**:
   - Sort all the edges in non-decreasing order of their weights.

2. **Initialize parent and rank arrays**:
   - Initialize the `parent` array to keep track of the set to which each vertex belongs.
   - Initialize the `rank` array to manage the union of sets efficiently.

3. **Iterate over sorted edges**:
   - Pick the smallest edge and check if it forms a cycle with the MST formed so far by checking if the vertices are in the same set.
   
4. **Check and add the edge**:
   - If it doesn't form a cycle, include this edge in the MST and perform a union of the two sets.

5. **Repeat until MST contains V-1 edges**:
   - Continue adding edges to the MST until it contains `V-1` edges, where `V` is the number of vertices.

6. **Print the MST**:
   - Finally, print the edges in the MST along with the minimum cost.

---

## Program

```
# Python program for Kruskal's algorithm to find
# Minimum Spanning Tree of a given connected,
# undirected and weighted graph

from collections import defaultdict

# Class to represent a graph


class Graph:

	def __init__(self, vertices):
		self.V = vertices # No. of vertices
		self.graph = [] # default dictionary
		# to store graph

	# function to add an edge to graph
	def addEdge(self, u, v, w):
		self.graph.append([u, v, w])

	# A utility function to find set of an element i
	# (uses path compression technique)
	def find(self, parent, i):
		if parent[i] == i:
			return i
		return self.find(parent, parent[i])

	# A function that does union of two sets of x and y
	# (uses union by rank)
	def union(self, parent, rank, x, y):
		xroot = self.find(parent, x)
		yroot = self.find(parent, y)

		# Attach smaller rank tree under root of
		# high rank tree (Union by Rank)
		if rank[xroot] < rank[yroot]:
			parent[xroot] = yroot
		elif rank[xroot] > rank[yroot]:
			parent[yroot] = xroot

		# If ranks are same, then make one as root
		# and increment its rank by one
		else:
			parent[yroot] = xroot
			rank[xroot] += 1

	# The main function to construct MST using Kruskal's
		# algorithm
	def KruskalMST(self):

		result = [] # This will store the resultant MST
		
		# An index variable, used for sorted edges
		i = 0
		
		# An index variable, used for result[]
		e = 0

		# Step 1: Sort all the edges in
		# non-decreasing order of their
		# weight. If we are not allowed to change the
		# given graph, we can create a copy of graph
		self.graph = sorted(self.graph,
							key=lambda item: item[2])

		parent = []
		rank = []

		# Create V subsets with single elements
		for node in range(self.V):
			parent.append(node)
			rank.append(0)

		# Number of edges to be taken is equal to V-1
		while e < self.V - 1:

			# Step 2: Pick the smallest edge and increment
			# the index for next iteration
			u, v, w = self.graph[i]
			i = i + 1
			x = self.find(parent, u)
			y = self.find(parent, v)

			# If including this edge doesn't
			# cause cycle, include it in result
			# and increment the indexof result
			# for next edge
			if x != y:
				e = e + 1
				result.append([u, v, w])
				self.union(parent, rank, x, y)
			# Else discard the edge

		minimumCost = 0
		print ("Edges in the constructed MST")
		for u, v, weight in result:
			minimumCost += weight
			print("%d -- %d == %d" % (u, v, weight))
		print("Minimum Spanning Tree" , minimumCost)

# Driver code
g = Graph(4)
g.addEdge(0, 1, 10)
g.addEdge(0, 2, 6)
g.addEdge(0, 3, 5)
g.addEdge(1, 3, 15)
g.addEdge(2, 3, 4)

# Function call
g.KruskalMST()
```

## OUTPUT
![Screenshot 2025-05-18 222812](https://github.com/user-attachments/assets/2b66d9b1-4692-4a07-bb60-555ad70f6e4a)

## RESULT
Thus the program for Kruskal's algorithm to find the Minimum Spanning Tree (MST) of a given connected, undirected, and weighted graph is executed Successfully.
