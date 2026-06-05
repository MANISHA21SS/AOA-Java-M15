
# EX 5C Graph coloring
## DATE: 19/05/26
## AIM:
To write a Java program to for given constraints.
Problem Description:
In a hilly region, several radio towers are installed to provide communication services. However, due to signal interference, two adjacent towers (i.e., in communication range of each other) must not use the same frequency channel.

You are given N radio towers and their communication ranges represented as an undirected graph. Your task is to assign channels (colors) to these towers using at most M channels such that no two adjacent towers use the same channel.

Write a program to determine if such an assignment is possible or not.

Input Format:
First line contains two integers: N (number of towers), and M (number of available frequency channels).

Next line contains an integer E — number of edges representing the communication range.

Next E lines contain two integers u and v — representing that tower u and tower v are within range (0-based index).

Output Format:
Print "YES" if it's possible to assign frequencies to towers such that no two adjacent towers have the same frequency.

Otherwise, print "NO".

<img width="182" height="440" alt="image" src="https://github.com/user-attachments/assets/b32078a2-c79d-4a25-88c4-e51144b5456f" />


## Algorithm
1.Input:

Read the number of towers n, available channels m, and number of connections e.

Read each connection pair (u, v) and build an adjacency list for the graph.

2.Initialization:

Create an integer array color[n] initialized with 0 (meaning no channel assigned).

Each tower (node) can be assigned a color (channel) from 1 to m.

3.Safety Check (isSafe):

Before assigning a channel to a tower, check all its adjacent towers.

If any adjacent tower already uses the same channel, assignment is not safe.

4.Backtracking Solution (solve):

Try assigning each channel (1 to m) to the current tower.

If safe, recursively assign channels to the next tower.

If no valid channel exists, backtrack and try another combination.

5.Output:

If all towers can be assigned channels without conflict → print "YES".

Otherwise → print "NO".   

## Program:
```
/*
Developed by: Manisha selvakumari.S.S.
Register Number:212223220055 
*/
import java.util.*;

public class prog {

    static int[] assignPhases(List<List<Integer>> adj, int N) {

        int[] color = new int[N];
        Arrays.fill(color, -1);

        color[0] = 0;

        boolean[] available = new boolean[N];

        for (int u = 1; u < N; u++) {

            Arrays.fill(available, true);

            for (int neighbor : adj.get(u)) {
                if (color[neighbor] != -1) {
                    available[color[neighbor]] = false;
                }
            }

            int phase;
            for (phase = 0; phase < N; phase++) {
                if (available[phase]) {
                    break;
                }
            }

            color[u] = phase;
        }

        return color;
    }

    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);

        int N = sc.nextInt();
        int M = sc.nextInt();

        List<List<Integer>> adj = new ArrayList<>();
        for (int i = 0; i < N; i++) {
            adj.add(new ArrayList<>());
        }

        for (int i = 0; i < M; i++) {
            int u = sc.nextInt();
            int v = sc.nextInt();

            adj.get(u).add(v);
            adj.get(v).add(u);
        }

        int[] result = assignPhases(adj, N);

        int maxPhase = 0;
        for (int color : result) {
            maxPhase = Math.max(maxPhase, color);
        }

        System.out.println(maxPhase + 1);

        for (int i = 0; i < N; i++) {
            System.out.println(i + " -> " + result[i]);
        }

        sc.close();
    }
}
```

## Output:

<img width="1170" height="491" alt="image" src="https://github.com/user-attachments/assets/c787a9ca-727f-40b9-8a0e-b06f3458d311" />



## Result:
The program successfully implemented and the expected output is verified.
