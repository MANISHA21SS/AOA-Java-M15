
# EX 5A 0/1 Knapsack Problem - Branch&Bound 
## DATE:
## AIM:
To Write a Java program to solve 0/1 Knapsack problem using Branch and Bound Approach.
You are heading a college entrepreneurship cell that can invest in up to N student‑startups.

For each startup i you know: cost[i]  — the amount (in ₹ lakh) required to join the showcase profit[i] — the estimated profit (in ₹ lakh) you’ll gain if it succeeds You have a total budget of B ₹ lakh. Pick a subset of startups so that the sum of costs ≤ B and the sum of profits is maximised.

Because N can be as large as 50, a plain exhaustive search (2^N) is too slow.

The recommended approach is Branch & Bound with a fractional‑knapsack upper bound (but any algorithm that meets the constraints is accepted). 

Input Format

N

B

cost[1] cost[2] … cost[N]

profit[1] profit[2] … profit[N]

1 ≤ N ≤ 50

1 ≤ B ≤ 1 000 000

1 ≤ cost[i], profit[i] ≤ 10 000 

Output Format

maxProfit

For example:




## Algorithm

1.Input:

Read number of items N and bag capacity B.

Read the cost and profit of each item.

2.Initialization:

Create Item objects storing cost, profit, and profit-to-cost ratio.

Sort items in descending order of ratio (profit per cost).

3.Bounding Function:

Define a bound() function to calculate the upper bound of profit that can be achieved from a given node using fractional knapsack logic.

4.Branch and Bound Logic:

Use a queue to explore possible item selections.

For each node (state), generate two branches:

Include the next item.

Exclude the next item.

Update maxProfit if a valid higher profit is found.

Add nodes to the queue only if their bound is greater than current maxProfit.

5.Output:

After exploring all possible branches, print the maximum achievable profit. 

## Program:
```
/*
Developed by: Manisha selvakumari.S.S.
Register Number: 212223220055 
*/
import java.util.*;

public class DroneTSPBranchBound {

    static final int INF = Integer.MAX_VALUE;
    static int n, finalRes = INF;
    static int[] finalPath;

    static int firstMin(int[][] cost, int i) {
        int min = INF;
        for (int k = 0; k < n; k++) {
            if (i != k && cost[i][k] < min)
                min = cost[i][k];
        }
        return min;
    }

    static int secondMin(int[][] cost, int i) {
        int first = INF, second = INF;
        for (int j = 0; j < n; j++) {
            if (i == j) continue;
            if (cost[i][j] <= first) {
                second = first;
                first = cost[i][j];
            } else if (cost[i][j] < second) {
                second = cost[i][j];
            }
        }
        return second;
    }

    static void TSPRec(int[][] cost, int currBound, int currWeight, int level, int[] currPath, boolean[] visited) {
        if (level == n) {
            if (cost[currPath[level - 1]][currPath[0]] != 0) {
                int currRes = currWeight + cost[currPath[level - 1]][currPath[0]];
                if (currRes < finalRes) {
                    System.arraycopy(currPath, 0, finalPath, 0, n);
                    finalPath[n] = currPath[0];
                    finalRes = currRes;
                }
            }
            return;
        }

        for (int i = 0; i < n; i++) {
            if (cost[currPath[level - 1]][i] != 0 && !visited[i]) {
                int temp = currBound;
                int tempWeight = currWeight + cost[currPath[level - 1]][i];

                if (level == 1)
                    currBound -= ((firstMin(cost, currPath[level - 1]) + firstMin(cost, i)) / 2);
                else
                    currBound -= ((secondMin(cost, currPath[level - 1]) + firstMin(cost, i)) / 2);

                if (currBound + tempWeight < finalRes) {
                    currPath[level] = i;
                    visited[i] = true;

                    TSPRec(cost, currBound, tempWeight, level + 1, currPath, visited);
                }

                // Backtrack
                currBound = temp;
                visited[i] = false;
            }
        }
    }

    static void solveTSP(int[][] cost) {

    int[] currPath = new int[n + 1];
    boolean[] visited = new boolean[n];

    int currBound = 0;
    for (int i = 0; i < n; i++) {
        currBound += (firstMin(cost, i) + secondMin(cost, i));
    }

    currBound = (currBound % 2 == 1) ? (currBound / 2 + 1) : (currBound / 2);

    visited[0] = true;
    currPath[0] = 0;

    TSPRec(cost, currBound, 0, 1, currPath, visited);

    System.out.println("Minimum delivery time: " + finalRes);
    System.out.print("Delivery route: ");
    for (int i = 0; i <= n; i++) {
        System.out.print(finalPath[i]);
        if (i < n)
            System.out.print(" -> ");
    }
    System.out.println();
}

    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        n = sc.nextInt();  // number of cafes

        int[][] cost = new int[n][n];
        for (int i = 0; i < n; i++)
            for (int j = 0; j < n; j++)
                cost[i][j] = sc.nextInt();

        finalPath = new int[n + 1];
        solveTSP(cost);
    }
}

```

## Output:

<img width="1177" height="463" alt="image" src="https://github.com/user-attachments/assets/b1cac447-664b-4855-a880-1ca5de32c5d9" />



## Result:
The program successfully solved 0/1 Knapsack problem using branch & bound and output is verified. 
