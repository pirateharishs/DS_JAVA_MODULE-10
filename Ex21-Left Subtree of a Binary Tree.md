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
