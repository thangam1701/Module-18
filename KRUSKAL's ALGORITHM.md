# Experiment 12(a): Prim's Minimum Spanning Tree (MST)

## Aim
To write a Python program for Prim's Minimum Spanning Tree (MST) algorithm.

---

## Algorithm

1. **Initialize Key Array**:
   - Initialize a `key` array to represent the minimum weight edge for each vertex, setting all values to infinity except for the first vertex, which is set to 0.

2. **Select the Minimum Key Vertex**:
   - Use the `minKey()` function to find the vertex with the smallest key value that is not yet included in the MST.

3. **Update Key Values**:
   - For each adjacent vertex of the selected vertex, if the edge weight is smaller than the current key value and the vertex is not in the MST, update the key value and parent of the vertex.

4. **Repeat**:
   - Repeat steps 2 and 3 for all vertices until all vertices are included in the MST.

5. **Print the MST**:
   - Finally, print the Minimum Spanning Tree using the parent array which holds the parent vertex for each vertex in the MST.

---

## Program

```
# A Python program for Prim's Minimum Spanning Tree (MST) algorithm.
# The program is for adjacency matrix representation of the graph

import sys # Library for INT_MAX

class Graph():

	def __init__(self, vertices):
		self.V = vertices
		self.graph = [[0 for column in range(vertices)]
					for row in range(vertices)]

	# A utility function to print the constructed MST stored in parent[]
	def printMST(self, parent):
		print ("Edge   Weight")
		for i in range(1, self.V):
			print (parent[i], "-", i, "  ",self.graph[i][parent[i]])

	# A utility function to find the vertex with
	# minimum distance value, from the set of vertices
	# not yet included in shortest path tree
	def minKey(self, key, mstSet):

		# Initialize min value
		min = sys.maxsize

		for v in range(self.V):
			if key[v] < min and mstSet[v] == False:
				min = key[v]
				min_index = v

		return min_index

	# Function to construct and print MST for a graph
	# represented using adjacency matrix representation
	def primMST(self):

		# Key values used to pick minimum weight edge in cut
		key = [sys.maxsize] * self.V
		parent = [None] * self.V # Array to store constructed MST
		# Make key 0 so that this vertex is picked as first vertex
		key[0] = 0
		mstSet = [False] * self.V

		parent[0] = -1 # First node is always the root of

		for cout in range(self.V):

			# Pick the minimum distance vertex from
			# the set of vertices not yet processed.
			# u is always equal to src in first iteration
			u = self.minKey(key, mstSet)

			# Put the minimum distance vertex in
			# the shortest path tree
			mstSet[u] = True

			# Update dist value of the adjacent vertices
			# of the picked vertex only if the current
			# distance is greater than new distance and
			# the vertex in not in the shortest path tree
			for v in range(self.V):

				# graph[u][v] is non zero only for adjacent vertices of m
				# mstSet[v] is false for vertices not yet included in MST
				# Update the key only if graph[u][v] is smaller than key[v]
				if self.graph[u][v] > 0 and mstSet[v] == False and key[v] > self.graph[u][v]:
						key[v] = self.graph[u][v]
						parent[v] = u

		self.printMST(parent)

g = Graph(5)
g.graph = [ [0, 2, 0, 6, 0],
			[2, 0, 3, 8, 5],
			[0, 3, 0, 0, 7],
			[6, 8, 0, 0, 9],
			[0, 5, 7, 9, 0]]

g.primMST();
```

## OUTPUT
![Screenshot 2025-05-18 222425](https://github.com/user-attachments/assets/9465565e-d45e-4c3d-bd59-fda85d6b0ae2)

## RESULT
Thus the program for Prim's Minimum Spanning Tree (MST) algorithm is executed Successfully.
