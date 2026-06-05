
# EX 5E Minimum Spanning Tree -Boruvka's Algorithm
## DATE: 20/05/26
## AIM:
To write a Java program to for given constraints.
Boruvka's Algorithm - Minimum Spanning Tree

Find the MST using Boruvka's Algorithm for a weighted undirected graph.

<img width="292" height="235" alt="image" src="https://github.com/user-attachments/assets/06246b27-37a9-40a8-bd7a-37a1d5187cd1" />

## Algorithm
1.Input:

Read number of vertices V and edges E.

For each edge, read its source src, destination dest, and weight w.

Store all edges in a list.

2.Initialization:

Set up a parent[] array for Disjoint Set Union (DSU).

Initially, each vertex is its own parent.

Initialize numTrees = V (number of connected components) and MSTweight = 0.

3.Finding Cheapest Edges:

For every iteration (while more than one tree exists):

Initialize an array cheapest[] to store the minimum-cost edge for each component.

For each edge, find the sets of its two vertices.

Update cheapest for both sets if the current edge has a smaller weight.

4.Building the MST:

For each vertex, pick its cheapest edge (if any).

If the two endpoints belong to different sets, include the edge in the MST, print it, and merge the sets using union().

Decrease numTrees after each successful merge.

5.Output:

Continue until only one tree (MST) remains.

Print each chosen edge and finally display the Total Weight of MST.
## Program:
```
/*
Developed by: Manisha selvakumari.S.S.
Register Number: 212223220055 
*/
import java.util.*;

public class UpdateMST {
    static class Edge {
        int src, dest, weight;
        Edge(int s, int d, int w) { src = s; dest = d; weight = w; }
    }

    static class UnionFind {
        int[] parent, rank;

        UnionFind(int n) {
            parent = new int[n];
            rank = new int[n];
            for (int i = 0; i < n; i++) parent[i] = i;
        }

        int find(int x) {
            if (parent[x] != x)
                parent[x] = find(parent[x]);
            return parent[x];
        }

        boolean union(int x, int y) {
            int rx = find(x), ry = find(y);

            if (rx == ry) return false;

            if (rank[rx] < rank[ry]) parent[rx] = ry;
            else if (rank[ry] < rank[rx]) parent[ry] = rx;
            else {
                parent[ry] = rx;
                rank[rx]++;
            }

            return true;
        }
    }

    public static int kruskalMST(int V, List<Edge> edges) {

        // sort edges by weight
        Collections.sort(edges, (a, b) -> a.weight - b.weight);

        UnionFind uf = new UnionFind(V);

        int mstWeight = 0;
        int count = 0;

        for (Edge e : edges) {

            if (uf.union(e.src, e.dest)) {
                mstWeight += e.weight;
                count++;

                if (count == V - 1) break;
            }
        }

        return mstWeight;
    }

    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);

        int V = sc.nextInt();
        int E = sc.nextInt();

        List<Edge> edges = new ArrayList<>();

        for (int i = 0; i < E; i++) {
            edges.add(new Edge(sc.nextInt(), sc.nextInt(), sc.nextInt()));
        }

        Edge newEdge = new Edge(sc.nextInt(), sc.nextInt(), sc.nextInt());
        edges.add(newEdge);

        int updatedWeight = kruskalMST(V, edges);
        System.out.println(updatedWeight);

    }
}
```

## Output:

<img width="1184" height="464" alt="image" src="https://github.com/user-attachments/assets/e72cd55e-cc55-44ed-963d-5e242637be9a" />



## Result:
The program successfully implemented and the expected output is verified.
