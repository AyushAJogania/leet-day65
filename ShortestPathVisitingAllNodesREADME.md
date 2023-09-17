# leet-day65

## Problem Statement
You are given an undirected, connected graph of n nodes labeled from 0 to n - 1. The task is to find the length of the shortest path that visits every node at least once. You may start and stop at any node, revisit nodes multiple times, and reuse edges.

## Approach
To solve this problem, we can use a Breadth-First Search (BFS) approach with a bit mask to keep track of visited nodes. The idea is to start BFS from every node as a potential starting point and traverse the graph while keeping track of visited nodes.

Here are the steps of the approach:

1. Initialize a 2D boolean array `visited`, where `visited[i][mask]` represents whether we have visited node `i` with the bitmask `mask` indicating which nodes have been visited. Initially, all entries are set to `false`.

2. Create a queue to perform BFS. We will push pairs `(node, mask)` into the queue, where `node` is the current node, and `mask` is the bitmask representing visited nodes.

3. Initialize the BFS queue with all nodes. For each node `i`, push the pair `(i, 1 << i)` into the queue and mark `visited[i][1 << i]` as `true` since we have visited this node.

4. Start the BFS traversal:
   - For each node `u` and bitmask `mask` in the queue:
     - If `mask` represents that all nodes have been visited (`mask` is a bitmask of all 1s), return the number of steps as we have found a valid path.
     - Otherwise, iterate over all neighbors `v` of node `u`. Calculate a new bitmask `newMask` by setting the bit representing node `v` to 1 (`mask | (1 << v)`).
     - If `newMask` has not been visited before (`visited[v][newMask]` is `false`), push the pair `(v, newMask)` into the queue and mark `visited[v][newMask]` as `true`.

5. If the BFS traversal completes and we haven't found a valid path (all nodes visited), return -1 to indicate that there is no valid path.

## Complexity Analysis
- Time Complexity: O(n * 2^n), where n is the number of nodes. In the worst case, we visit each node with all possible bitmasks.
- Space Complexity: O(n * 2^n) for the `visited` array and O(n) for the queue.

## Summary
This algorithm uses BFS with a bit mask to find the shortest path that visits all nodes in a graph. It explores all possible starting nodes and keeps track of visited nodes to find the optimal solution.
