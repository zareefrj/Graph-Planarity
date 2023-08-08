# Graph-Planarity
Determining Planarity of Randomly Generated Simple Graphs Using Design Thinking Processes
## 1. Empathise
The problem statement was to generate 10 different simple graphs with 20 vertices at
random and determine their planarity. 

To understand the problem statement and gather
information about graph theory and planarity, relevant literature was reviewed, and discussions
were held among group members to understand the concepts of graph theory before tackling the
problem.
## 2. Define
Based on the understanding of the problem statement and information gathered, the
problem was defined in clear and concise terms. The objective was to develop a computer
program that can generate 10 different simple graphs with 20 vertices at random and determine
their planarity.

We define a simple graph here as an undirected graph that has no loops (edges that
connect a vertex to itself) and no multiple edges (two or more edges that connect the same pair of
vertices). In other words, a simple graph is a graph that has at most one edge between any pair of
vertices, and no edge that connects a vertex to itself. 

And a planar graph is a graph that can be
drawn in the plane without any of its edges crossing. In other words, a planar graph is a graph
that can be embedded in the plane without any edge intersection.
## 3. Ideate
Brainstorming sessions were held as a group to generate ideas on how to develop a
computer program that can generate random graphs and determine their planarity. Different
programming languages, libraries, and algorithms were considered to select the best approach to
achieve the objective.
### 3.1 Graph Generation
For graph generation, we decided to import an existing library on Python for
network/graph analysis called NetworkX to help us create a graph object & use the methods
found to visualise the graphs. 

This library makes it easier for us to add vertices & edges to the
graph objects without actually having to deal with building vertices, edges & the graph from
scratch. 

This saves a lot of time for us, & we used the extra time we have to properly brainstorm
the latter part of the problem.
### 3.2 Planarity Check
This was trickier than expected. Initially we thought of just using Euler’s Identity
(v-e+f=2) to prove the graphs planarity, however the “f” part of the equation proved to be hard
to implement into a computer program, we were unable to come up with a solution to identify
the number of faces on a graph.

Hence, we moved on to the 3 corollaries, yet again we were hit with the realisation that
these corollaries are necessary conditions for a graph to be planar, not sufficient conditions. 

This means that we can prove that a graph is NOT a planar graph, but we are unable to prove that it
IS planar. This applies to Euler’s Identity as well.

There was an attempt to implement Kuratowski's Theorem from scratch– a graph is
planar if and only if it does not contain a subdivision of 𝐾5 or 𝐾3,3 & is not homeostatic to
those 2 graphs. But the first crucial step to apply that theorem is to eliminate vertices & edges
so that we can get to the resemblance of 𝐾5 or 𝐾3,3. With a graph with 20 vertices, choosing
which vertices to remove & how many vertices to be removed is a complete nightmare to
implement.

We noticed that the NetworkX library we used to visualise the graph has a “is_planar”
function. The algorithms implemented in the "is_planar" function of the NetworkX library
include the Boyer-Myrvold & Hopcroft and Tarjan planarity testing algorithm. These algorithms
check for the existence of a Kuratowski subgraph by a sequence of edge subdivisions and edge
deletions. If a Kuratowski subgraph is found, the graph is not planar. Otherwise, it is planar. The
"is_planar" function in NetworkX is utilised for our program to test the planarity.
#### 3.2.1 Boyer-Myrvold
The Boyer-Myrvold algorithm is a graph isomorphism algorithm that determines if two graphs
have the same structure but potentially different node labels. It uses a partition refinement
approach by iteratively refining a partition of the graph nodes based on their connectivity
patterns.

Initially, it computes properties like node degrees and neighbour sets for efficient access.
Then, an initial partition is created based on node degrees. The algorithm iterates through the
nodes, refining the partition using connectivity patterns.

If the partition is refined and all sets have more than one node, a high-degree node
becomes the "distinguishing set." The algorithm recursively applies itself to the subgraphs of the
distinguishing set, checking their isomorphism.

Finally, it checks if nodes in the sets can be paired without violating connectivity
patterns. If not, the graphs are not isomorphic. 

The Boyer-Myrvold algorithm incorporates
optimizations like caching computations and heuristics for efficient partition refinement.
While it may not be the fastest algorithm in terms of worst-case time complexity, it
performs well in practice and is widely used for graph isomorphism testing. The algorithm's
source code for planarity testing and extraction of multiple Kuratowski subdivisions is publicly
available.
#### 3.2.2 Hopcroft & Tarjan
The Hopcroft-Tarjan algorithm, also known as the path-addition algorithm, is a significant
contribution to planarity testing in graph theory. 

Proposed by Hopcroft and Tarjan in 1974, it was
the first algorithm capable of determining whether a graph is planar in linear time. The
Hopcroft-Tarjan algorithm's efficiency lies in its ability to determine planarity in linear time,
making it suitable for large graphs. It combines depth-first search, biconnected component
identification, and path addition techniques to achieve its goal.

The algorithm starts with an initial cycle in the graph and gradually adds one path at a
time. It utilises various techniques, including depth-first search, to analyse the graph's structure.
During the process, the algorithm evaluates important features such as parent links, pre order
ranks, and highpt1 and highpt2 functions.

Here is a simple flow how this algorithm works:

● Initialising the input graph and selecting a vertex as the root for the depth-first search
traversal

● Assigns preorder ranks to vertices and maintains parent links

● Identifies biconnected components in the graph by tracking back edges and utilising
parent links

● If a non-planar condition is encountered, the algorithm terminates and determines that the
graph is not planar

● Otherwise, it constructs a planar embedding by adding one path at a time to the initial
cycle

● The algorithm repeats the path addition step until either all paths have been added or a
non-planar condition arises

Overall, the Hopcroft-Tarjan algorithm revolutionised planarity testing by enabling
efficient linear-time analysis of graph planarity. Subsequent research and enhancements have
built upon this foundation, ensuring its broader applicability and facilitating its implementation
in various algorithms and libraries.
## 4. Prototype
A computer program was developed using Python and the NetworkX package. The
program generated 10 different simple graphs with 20 vertices at random, and their planarity was
determined using established planarity testing algorithms.
### 4.1 Pseudocode
1. Import random, NetworkX and Matplotlib libraries
2. Initialise variable num_graphs (number of graphs to generate) and num_vertices (number of vertices that each graph should have)
3. Initialise a loop that will iterate until ‘num_graphs’ times.While inside the loop: (*Steps 4-13)*
4. Create a new empty graph
5. Add vertices
6. Determine a probability of adding an edge based on the current number of graphs. If it’s number (i) greater than half of num_graphs, the probability to add an edge is 50%, otherwise probability is set to 10%.
7. Initialise a nested loop to iterate through all pair of vertices.
8. Add an edge for each vertices pair with its specified probability randomly.
9. If randomly generated value is less than probability, then add an edge between two vertices.
10. Print the graph number
11. Check if the graph is planar or not using the NetworkX library. If it’s planar, print “planar”, otherwise print “Non-planar”
12. Draw the graph using NetworkX library
13. Display the graph
