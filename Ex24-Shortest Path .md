# Ex24 Shortest Path and Reachability in a Heritage Town using BFS
## DATE:  24/10/25 
## AIM:
To design and implement a java program that, given a map of attractions in a heritage town connected by walking paths, recommends:
The shortest number of paths (minimum hops) from a starting attraction to a target attraction.
The number of reachable attractions from the same starting point using Breadth-First Search (BFS)


## Algorithm
1. Start the program.
2. Read integers.
3. Create an adjacency list graph of size n.
4. Build the Graph.
5. Read Start and Target.
6. Initialize BFS.
7. Initialize DFS
8. Counting Reachable Attractions and Print.
9. End the program.  

## Program:
```
/*
Program to determine Shortest Path and Reachability in a Heritage Town using BFS
Developed by: HARISH S
Register Number: 212223230071
*/

import java.util.*;

public class TouristNavigation {
    
    public static int bfs(List<List<Integer>> graph, int start, int target, int n) {
        boolean[] visited = new boolean[n];
        int[] dist = new int[n];
        Queue<Integer> q = new LinkedList<>();
        q.offer(start);
        visited[start] = true;
        dist[start] = 0;

        while (!q.isEmpty()) {
            int curr = q.poll();
            if (curr == target) return dist[curr];
            for (int neigh : graph.get(curr)) {
                if (!visited[neigh]) {
                    visited[neigh] = true;
                    dist[neigh] = dist[curr] + 1;
                    q.offer(neigh);
                }
            }
        }
        return -1;
    }

    public static void dfs(List<List<Integer>> graph, boolean[] visited, int node) {
        visited[node] = true;
        for (int neighbor : graph.get(node)) {
            if (!visited[neighbor]) {
                dfs(graph, visited, neighbor);
            }
        }
    }

    public static int countReachable(boolean[] visited) {
        int count = 0;
        for (boolean v : visited) if (v) count++;
        return count;
    }

    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        int n = sc.nextInt(), e = sc.nextInt();
        List<List<Integer>> graph = new ArrayList<>();
        for (int i = 0; i < n; i++) graph.add(new ArrayList<>());

        for (int i = 0; i < e; i++) {
            int u = sc.nextInt(), v = sc.nextInt();
            graph.get(u).add(v);
            graph.get(v).add(u);
        }

        int start = sc.nextInt();
        int target = sc.nextInt();

        int shortest = bfs(graph, start, target, n);
        boolean[] visited = new boolean[n];
        dfs(graph, visited, start);
        int reachable = countReachable(visited);

        System.out.println("Shortest path from start to target: " + shortest);
        System.out.println("Total reachable attractions from start: " + reachable);
    }
}

```

## Output:

<img width="1018" height="348" alt="image" src="https://github.com/user-attachments/assets/35cd0887-e929-44a0-ba30-178db803b751" />

## Result:
The program has been successfully implemented and executed.
It correctly computes:
The shortest number of paths (minimum hops) between two attractions.
The total number of reachable attractions from a given starting point using BFS traversal.
