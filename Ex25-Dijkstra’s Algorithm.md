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
