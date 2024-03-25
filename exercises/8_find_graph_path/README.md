# Problem description

In this exercise, we are asked to design a Non-deterministic Turing
Machine (NTM) that, given a string that represents a set of edges of a
graph, is able to decide whether there is a path between vertices A and
B. The machine should halt in an accepting state if a path is found, and
in a rejecting state otherwise.

The input format is `<edge1>,<edge2>,...,<edgeN>`, where each edge is
represented by a pair of vertices separated by a symbol \"`,`\". The
undirected graph has the following vertices: `A`, `B`, `1`, `2`, `3`,
`4`.

To tackle this problem, I decided to implement a non-deterministic
Turing Machine that explores systematically all possible paths between
vertices A and B. The machine will start from vertex A (tree root) and
will explore all possible edges that start/arrive to/from A in different
branches of the computation.

This approach allows to explore all possible paths in the graph, and to
halt in an accepting state if we find a path that leads to vertex B, and
in a rejecting state if no path is found.

These are the main steps of the algorithm:

1. First, the machine verifies if the string input has the correct
   format. If the input string is not correct, the machine will halt in
   a rejecting state. This is done by checking if the input string
   contains only 2-character elements separated by a comma.

2. After the input string has been validated, the machine starts by
   looking for an edge that starts/end in vertex `A`. As soon as it
   finds this edge, the machine will non-deterministically check which
   edge to explore next. This is needed as vertex `A` could be either a
   starting vertex (i.e. `AB`) or an ending point of an edge (i.e.
   `BA`).

3. After having identified the next edge to explore, the machine will
   check if we have reached vertex `B`. If this is the case, the
   machine will halt in an accepting state, as a path has been found.
   Otherwise, the machine will continue to explore the graph by marking
   this edge point as visited (marking the edge with a special symbol
   `X`) and will look for where this current edge leads to.

4. The machine will continue iteratively this process until:

   1. A path from vertex A to B is found, in which case the machine
      will halt in an accepting state.

   2. All possible paths have been explored, and no path from vertex A
      to B has been found, in which case the machine will halt in a
      rejecting state.

For this exercise, I have implemented the algorithm in the file
`exercise6.txt` and tested it using the non-deterministic Turing machine
simulator available
[](https://francoisschwarzentruber.github.io/turingmachinesimulator/).

I have tested the machine with the following input strings:

- `AB`, final state: `acc`

- `A1,1B`, final state: `acc`

- `2A,2B`, final state: `acc`

- `A1,12,23,34,4B`, final state: `acc`

- `_` (empty string), final state: `rej`

- `A` final state: `rej`

- `,` final state: `rej`

- `AB,` final state: `rej`

- `A1,,1B` final state: `rej`

- `A1,1B,` final state: `rej`

- `12` final state: `rej`
