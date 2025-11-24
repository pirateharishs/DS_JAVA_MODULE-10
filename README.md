# Ex21 Count the Number of Nodes in the Left Subtree of a Binary Tree
## DATE: 15/10/25
## AIM:
To design and implement a java program that constructs a binary tree from given level order input and counts the number of nodes present in the left subtree of the root node

## Algorithm
1. Start the program.
2. Read integer.
3. Create an array of size n.
4.  Read n integers and store them in array.
5.   Building the Tree (Level-Order).
6. Counting Left Subtree Nodes.
7. Print the result.
8. Stop the program.

## Program:
```
/*
Program to constructs a binary tree from given level order input and counts the number of nodes 
Developed by: HARISH S
Register Number: 212223230071
*/

import java.util.*;

class Node {
    int data;
    Node left, right;
    Node(int data) {
        this.data = data;
        this.left = this.right = null;
    }
}

public class Main {

    // Build binary tree in level-order fashion
    static Node buildTree(int[] arr) {
        if (arr.length == 0) return null;
        Node root = new Node(arr[0]);
        Queue<Node> q = new LinkedList<>();
        q.add(root);
        int i = 1;

        while (!q.isEmpty() && i < arr.length) {
            Node current = q.poll();
            if (i < arr.length) {
                current.left = new Node(arr[i++]);
                q.add(current.left);
            }
            if (i < arr.length) {
                current.right = new Node(arr[i++]);
                q.add(current.right);
            }
        }

        return root;
    }

    static int countNodes(Node root) {
        if (root == null) return 0;
        return 1 + countNodes(root.left) + countNodes(root.right);
    }

    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        int n = sc.nextInt();
        int[] arr = new int[n];
        for (int i = 0; i < n; i++) arr[i] = sc.nextInt();
        Node root = buildTree(arr);

        if (root.left == null) {
            System.out.println(0);
        } else {
            System.out.println(countNodes(root.left));
        }
    }
}

```

## Output:

<img width="458" height="307" alt="image" src="https://github.com/user-attachments/assets/18dffde7-2a1c-4c9a-a6f2-05074bb58667" />

## Result:
The program has been successfully implemented and executed.
It correctly constructs the binary tree from level order input and counts the number of nodes in the left subtree of the root node.

# Ex22 Searching for a Book ID in a Binary Search Tree (BST)
## DATE: 17/10/25
## AIM:
To design and implement java program that constructs a Binary Search Tree (BST) using given Book IDs and checks whether a specific Book ID exists in the BST.
## Algorithm
1. Start the program.
2. Read integer.
3. Initialize root equals to null.
4. Repeat n times.
5. Insert(root, key).
6. Searching Book ID.
7. Search(root, key).
8.  Stop the program.   

## Program:
```
/*
Program to constructs a Binary Search Tree (BST) using given Book IDs 
Developed by: HARISH S
Register Number: 212223230071
*/

import java.util.*;

public class BookIDSearch {
    static class Node {
        int data;
        Node left, right;
        Node(int data) {
            this.data = data;
        }
    }

    public static Node insert(Node root, int key) {
        if (root == null) return new Node(key);
        if (key < root.data) root.left = insert(root.left, key);
        else root.right = insert(root.right, key);
        return root;
    }

    public static boolean search(Node root, int key) {
        if (root == null) return false;
        if (root.data == key) return true;
        if (key < root.data) return search(root.left, key);
        else return search(root.right, key);
    }

    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        int n = sc.nextInt();
        Node root = null;
        for (int i = 0; i < n; i++) {
            root = insert(root, sc.nextInt());
        }
        int q = sc.nextInt();
        while (q-- > 0) {
            int key = sc.nextInt();
            System.out.println(search(root, key) ? "Found" : "Not Found");
        }
    }
}

```

## Output:

<img width="507" height="387" alt="image" src="https://github.com/user-attachments/assets/3959e1d5-1697-4cd0-8afd-d13836b92af2" />

## Result:
The program has been successfully implemented and executed.
It constructs a Binary Search Tree from the given Book IDs and accurately determines whether a queried Book ID exists in the library system.

# Ex23 Breadth-First Search (BFS) Traversal of a City Junction Map
## DATE: 22/10/25
## AIM:
To design and implement a java program to perform Breadth-First Search (BFS) traversal on a city’s junction map represented as a graph, and find all reachable locations from a given source junction.
## Algorithm
1. Start the program.
2. Read two integers.
3. Create an adjacency list g of size n.
4. Repeat e times.
5. Read the source node.
6. Initialize a boolean array of size n, all set to false.
7. Create an empty queue.
8. Mark src as visited and enqueue it.
9. Continue until all reachable nodes are processed.
10. Stop the program.

## Program:
```
/*
Program to perform Breadth-First Search (BFS) traversal on a city’s junction map represented as a graph
Developed by: HARISH S
Register Number: 212223230071
*/

import java.util.*;

public class EmergencyRouteBFS {
    public static void addEdge(List<List<Integer>> g, int u, int v) {
        g.get(u).add(v);
        g.get(v).add(u);
    }

    public static void bfs(List<List<Integer>> g, int src, boolean[] visited) {
        Queue<Integer> q = new LinkedList<>();
        q.offer(src);
        visited[src] = true;
        while (!q.isEmpty()) {
            int curr = q.poll();
            System.out.print(curr + " ");
            for (int neighbor : g.get(curr)) {
                if (!visited[neighbor]) {
                    visited[neighbor] = true;
                    q.offer(neighbor);
                }
            }
        }
    }

    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        int n = sc.nextInt(), e = sc.nextInt();
        List<List<Integer>> g = new ArrayList<>();
        for (int i = 0; i < n; i++) g.add(new ArrayList<>());
        for (int i = 0; i < e; i++) addEdge(g, sc.nextInt(), sc.nextInt());
        int src = sc.nextInt();
        bfs(g, src, new boolean[n]);
    }
}

```

## Output:
<img width="464" height="325" alt="image" src="https://github.com/user-attachments/assets/ba67be71-eb74-438b-8171-68be3a1a498e" />

## Result:
The program has been successfully implemented and executed.
It performs Breadth-First Search (BFS) traversal on a city junction map and correctly lists all reachable locations from the given source node.

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

# Ex25 Finding the Fastest Route to a Charging Station using Dijkstra’s Algorithm
## DATE: 29/10/25
## AIM:
To design and implement a java program that helps an electric vehicle (EV) find the shortest travel time from its current block to the nearest charging station using Dijkstra’s shortest path algorithm.
## Algorithm
1. Start the program.
2. Read integers.
3. Create an adjacency list graph of size n, where each node stores a list of (neighbor, time) pairs.
4. Build the Graph.
5. Read Remaining Input.
6. Initialize Dijkstra’s setup.
7. Dijkstra’s Relaxation Loop.
8. Find minimum time among stations.
9. End the program.   

## Program:
```
/*
Program to find the Fastest Route to a Charging Station using Dijkstra’s Algorithm
Developed by: HARISH S
Register Number: 212223230071
*/

import java.util.*;

public class EVChargingNavigation {

    static class Pair {
        int node, time;
        Pair(int node, int time) {
            this.node = node;
            this.time = time;
        }
    }

    static int findNearestChargingStation(int n, List<List<Pair>> graph, int source, Set<Integer> stations) {
        int[] dist = new int[n];
        Arrays.fill(dist, Integer.MAX_VALUE);
        dist[source] = 0;

        PriorityQueue<Pair> pq = new PriorityQueue<>(Comparator.comparingInt(a -> a.time));
        pq.offer(new Pair(source, 0));

        while (!pq.isEmpty()) {
            Pair current = pq.poll();
            for (Pair neighbor : graph.get(current.node)) {
                int newDist = dist[current.node] + neighbor.time;
                if (newDist < dist[neighbor.node]) {
                    dist[neighbor.node] = newDist;
                    pq.offer(new Pair(neighbor.node, newDist));
                }
            }
        }

        int minTime = Integer.MAX_VALUE;
        for (int s : stations) {
            if (dist[s] < minTime) minTime = dist[s];
        }
        return minTime == Integer.MAX_VALUE ? -1 : minTime;
    }

    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);

        int n = sc.nextInt(), m = sc.nextInt();
        List<List<Pair>> graph = new ArrayList<>();
        for (int i = 0; i < n; i++) graph.add(new ArrayList<>());

        for (int i = 0; i < m; i++) {
            int u = sc.nextInt(), v = sc.nextInt(), w = sc.nextInt();
            graph.get(u).add(new Pair(v, w));
            graph.get(v).add(new Pair(u, w)); // Undirected
        }

        int source = sc.nextInt();
        int k = sc.nextInt();
        Set<Integer> stations = new HashSet<>();
        for (int i = 0; i < k; i++) stations.add(sc.nextInt());

        System.out.println(findNearestChargingStation(n, graph, source, stations));
    }
}

```

## Output:

<img width="433" height="429" alt="image" src="https://github.com/user-attachments/assets/a6a651b4-0d47-45e1-8b34-011beaf16bc1" />

## Result:
The program has been successfully implemented and executed.
It uses Dijkstra’s algorithm to determine the shortest travel time from the EV’s current location to the nearest charging station and correctly handles cases where no station is reachable.
