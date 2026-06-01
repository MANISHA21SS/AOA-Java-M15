
# EX 5D Flower Planting.
## DATE:
## AIM:
To write a Java program to for given constraints.
You are given n gardens, labelled from 1 to n.

You also have a list called paths, where each element paths[i] = [xi, yi] represents a bidirectional road connectingthe  garden xi and garden yi.

You want to plant one flower in each garden, and there are exactly 4 types of flowers labelled as 1, 2, 3, and 4.

Your goal is to plant flowers such that:

No two connected gardens (i.e., connected via a path) have the same flower type.

Return any valid flower assignment as an array where:

answer[i] is the flower type planted in the (i+1) ᵗʰ garden

It is guaranteed that:

No garden is connected to more than 3 other gardens

A valid flower assignment always exists

<img width="177" height="292" alt="image" src="https://github.com/user-attachments/assets/36aa40cb-1cdd-4746-b1a6-fc51ce6e96aa" />

## Algorithm
1.Input:

Read the number of gardens n and the number of paths m.

Read each path pair (u, v) that connects two gardens.

2.Graph Construction:

Create an adjacency list for all gardens.

For every path (u, v), add each garden to the other's adjacency list.

3.Initialization:

Create an integer array flowers[n] to store the flower type (1–4) assigned to each garden.

Each garden can have one of four flower types.

4.Assignment Logic:

For each garden i, check all adjacent gardens.

Mark the flower types already used by its neighbors and assign the first available flower type to garden i.

5.Output:

Print the final flower type assigned to each garden in order.  

## Program:
```
/*
Developed by: Manisha selvakumari.S.S.
Register Number: 212223220055
*/
import java.util.*;

public class TeacherAssignment {

    public static int[] assignTeachers(int n, List<List<Integer>> graph) {

        int[] color = new int[n]; 

        for (int u = 0; u < n; u++) {

            boolean[] used = new boolean[n + 1];

            for (int v : graph.get(u)) {
                if (color[v] != 0) {
                    used[color[v]] = true;
                }
            }

            for (int c = 1; c <= n; c++) {
                if (!used[c]) {
                    color[u] = c;
                    break;
                }
            }
        }

        return color;
    }

    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);

        int n = sc.nextInt(); 
        int m = sc.nextInt(); 

        List<List<Integer>> graph = new ArrayList<>();
        for (int i = 0; i < n; i++) {
            graph.add(new ArrayList<>());
        }

        for (int i = 0; i < m; i++) {
            int u = sc.nextInt();
            int v = sc.nextInt();
            graph.get(u).add(v);
            graph.get(v).add(u);
        }

        int[] assigned = assignTeachers(n, graph);

        for (int i = 0; i < n; i++) {
            System.out.println("Lab " + i + ": Teacher " + assigned[i]);
        }
    }
}
```

## Output:

<img width="1175" height="531" alt="image" src="https://github.com/user-attachments/assets/18cd9bd3-8312-44be-9928-d63e71f29f29" />


## Result:
The program successfully implemented and the expected output is verified.
