
# EX 5B Topological Sort - Khan's Algorithm
## DATE: 20/05/26
## AIM:
To write a Java program to for given constraints.
Problem Description:
A software development team is preparing for a product release. The release consists of multiple tasks, each dependent on other tasks being completed first. You are to determine a valid order in which all tasks can be completed. If it's not possible due to cyclic dependencies, output that the release cannot be scheduled.

Each task is labeled from 0 to n-1. The dependencies are provided in the form of pairs [a, b] which means task a depends on task b.

Implement a program to find a valid task execution order using topological sort.

Input Format:

An integer n — number of tasks.

An integer m — number of dependencies.

m lines follow with two integers a and b — representing a depends on b.

Output Format:

If a valid order exists, print the task numbers in a possible execution order (space-separated).

If not, print "Release cannot be scheduled".

<img width="341" height="363" alt="image" src="https://github.com/user-attachments/assets/f0355541-4f66-49da-bcd3-171a799a7c1f" />

## Algorithm
1.Input:

Read the number of tasks n and the number of dependency pairs m.

Read each dependency pair and store them in a 2D array.

2.Graph Construction:

Create an adjacency list to represent task dependencies.

Maintain an indegree array to count incoming edges for each task.

3.Initialization:

Add all tasks with indegree = 0 (no dependencies) to a queue.

4.Topological Sorting:

Repeatedly remove a task from the queue, add it to the order list, and decrease the indegree of its dependent tasks.

If a dependent task’s indegree becomes 0, add it to the queue.

5.Output:

If all tasks are processed, print the valid order of execution.

Otherwise, display “Release cannot be scheduled” if a cycle (dependency conflict) exists.

  

## Program:
```
/*
Developed by: Manisha selvakumari.S.S.
Register Number: 212223220055 
*/
import java.util.*;

public class MetroProjectPlanner {

    // Method to determine valid metro construction order
    public static List<Integer> findMetroOrder(int n, int[][] dependencies) {

    List<List<Integer>> graph = new ArrayList<>();
    for (int i = 0; i < n; i++) {
        graph.add(new ArrayList<>());
    }

    int[] indegree = new int[n];

    for (int[] dep : dependencies) {
        int a = dep[0];
        int b = dep[1];

        graph.get(b).add(a); // b -> a
        indegree[a]++;
    }

    Queue<Integer> queue = new LinkedList<>();

    for (int i = 0; i < n; i++) {
        if (indegree[i] == 0) {
            queue.offer(i);
        }
    }

    List<Integer> order = new ArrayList<>();

    while (!queue.isEmpty()) {
        int current = queue.poll();
        order.add(current);

        for (int neighbor : graph.get(current)) {
            indegree[neighbor]--;

            if (indegree[neighbor] == 0) {
                queue.offer(neighbor);
            }
        }
    }

    // Cycle detected
    if (order.size() != n) {
        return null;
    }

    return order;
}

    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        int n = sc.nextInt(); // number of phases
        int m = sc.nextInt(); // number of dependencies

        int[][] dependencies = new int[m][2];
        for (int i = 0; i < m; i++) {
            dependencies[i][0] = sc.nextInt(); // a depends on b
            dependencies[i][1] = sc.nextInt();
        }

        List<Integer> result = findMetroOrder(n, dependencies);

        if (result == null) {
            System.out.println("Metro project cannot be scheduled");
        } else {
            for (int phase : result) {
                System.out.print(phase + " ");
            }
        }
        sc.close();
    }
}

```

## Output:

<img width="1179" height="740" alt="image" src="https://github.com/user-attachments/assets/72bdd869-143f-43a2-b9bd-af9c628d168d" />




## Result:
The program successfully implemented and the expected output is verified.
