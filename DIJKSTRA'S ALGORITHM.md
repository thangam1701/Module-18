# Experiment 12(c): Dijkstra's Algorithm

## Aim
To write a Python program for Dijkstra's single-source shortest path algorithm.

---

## Algorithm

1. **Initialize Distance Array**:
   - Set the distance for all vertices to infinity (`∞`), except for the source vertex which is set to 0.

2. **Track Processed Vertices**:
   - Create a set `sptSet` to keep track of the processed vertices (shortest path tree).

3. **Pick the Minimum Distance Vertex**:
   - Select the vertex with the smallest distance that has not been processed.

4. **Update Adjacent Vertices**:
   - For the selected vertex, update the distances of its adjacent vertices if a shorter path is found through this vertex.

5. **Mark the Vertex as Processed**:
   - Once the vertex is processed, mark it as part of the shortest path tree.

6. **Repeat Steps**:
   - Continue the process until all vertices are processed.

7. **Print the Shortest Distances**:
   - Once all vertices are processed, print the shortest distances from the source vertex to all other vertices.

---

## Program

```
# Python program for Dijkstra's single source shortest path algorithm. 
# The program is for adjacency matrix representation of the graph

# Library for INT_MAX
import sys

class Graph():

	def __init__(self, vertices):
		self.V = vertices
		self.graph = [[0 for column in range(vertices)]
					for row in range(vertices)]

	def printSolution(self, dist):
		print("Vertex   Distance from Source")
		for node in range(self.V):
			print(node, "           ", dist[node])

	# A utility function to find the vertex with
	# minimum distance value, from the set of vertices
	# not yet included in shortest path tree
	def minDistance(self, dist, sptSet):

		# Initialize minimum distance for next node
		min = sys.maxsize

		# Search not nearest vertex not in the
		# shortest path tree
		for u in range(self.V):
			if dist[u] < min and sptSet[u] == False:
				min = dist[u]
				min_index = u

		return min_index

	# Function that implements Dijkstra's single source
	# shortest path algorithm for a graph represented
	# using adjacency matrix representation
	def dijkstra(self, src):

		dist = [sys.maxsize] * self.V
		dist[src] = 0
		sptSet = [False] * self.V

		for cout in range(self.V):

			# Pick the minimum distance vertex from
			# the set of vertices not yet processed.
			# x is always equal to src in first iteration
			x = self.minDistance(dist, sptSet)

			# Put the minimum distance vertex in the
			# shortest path tree
			sptSet[x] = True

			# Update dist value of the adjacent vertices
			# of the picked vertex only if the current
			# distance is greater than new distance and
			# the vertex in not in the shortest path tree
			for y in range(self.V):
				if self.graph[x][y] > 0 and sptSet[y] == False and 				dist[y] > dist[x] + self.graph[x][y]:
						dist[y] = dist[x] + self.graph[x][y]

		self.printSolution(dist)

# Driver program
g = Graph(9)
g.graph = [[0, 4, 0, 0, 0, 0, 0, 8, 0],
		[4, 0, 8, 0, 0, 0, 0, 11, 0],
		[0, 8, 0, 7, 0, 4, 0, 0, 2],
		[0, 0, 7, 0, 9, 14, 0, 0, 0],
		[0, 0, 0, 9, 0, 10, 0, 0, 0],
		[0, 0, 4, 14, 10, 0, 2, 0, 0],
		[0, 0, 0, 0, 0, 2, 0, 1, 6],
		[8, 11, 0, 0, 0, 0, 1, 0, 7],
		[0, 0, 2, 0, 0, 0, 6, 7, 0]
		];

g.dijkstra(0);
```

## OUTPUT
![Screenshot 2025-05-18 223953](https://github.com/user-attachments/assets/c74f1e6a-c8ac-4670-a051-5846d280b803)

## RESULT
Thus the program for Dijkstra's single-source shortest path algorithm is executed Successfully.
