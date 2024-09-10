Binary Search Trees (BST) - Lecture
What is a Binary Tree?
A binary tree is a hierarchical data structure where each node has at most two children:

Left Child: Contains smaller values.
Right Child: Contains larger values.
Binary trees have many real-world applications, such as:

Heaps: Keeping data ordered as it is added.
Tries: Storing words efficiently for quick lookups.
HTML Trees: Representing the structure of an HTML document.
Example of an HTML Tree
html
Copy code
<div>
  /     \
<h1>    <p>
Types of Tree Traversal
Tree traversal refers to visiting each node in a specific order. The three main types of traversal are:

In-order Traversal: Visits the left subtree, then the root, then the right subtree. This gives the nodes in ascending order.
Post-order Traversal: Visits the left subtree, then the right subtree, and finally the root. This is often used to delete a tree.
Pre-order Traversal: Visits the root first, followed by the left and right subtrees. This is used to create a copy of a tree.
Binary Search Tree (BST) Example
Consider the following values to be inserted into a tree:

[23, 16, 45, 3, 22, 99, 40]
These values can be represented in a binary search tree like this:

text
Copy code
                       23
                    /      \
                 16          45
               /   \       /    \
             3      22   40      99
Code Explanation
We will now break down the code step by step to understand how the Binary Search Tree (BST) is built and traversed.

Node Class
The Node class defines the structure of a node in the binary tree.

javascript
Copy code
class Node {
    constructor(data, left, right) {
        this.data = data;  // The value stored in the node
        this.left = left;  // Pointer to the left child
        this.right = right;  // Pointer to the right child
        this.show = show;  // Method to display node's data
    }
}
data: The value inside the node (e.g., 23, 16).
left: Pointer to the left child (nodes with smaller values).
right: Pointer to the right child (nodes with larger values).
show(): Returns the node's data when called.
Show Function
This function is used to return the data stored in a node.

javascript
Copy code
function show() {
  return this.data;
}
BTS (Binary Tree Structure) Class
This class represents the entire binary search tree.

javascript
Copy code
class BTS {
    constructor() {
        this.root = null;  // The root node of the tree
        this.insert = insert;  // Method to insert data into the tree
        this.inOrder = inOrder;  // Method for in-order traversal
    }
}
root: Initially set to null, meaning the tree is empty.
insert(): Method to add nodes to the tree.
inOrder(): Method to perform in-order traversal and print the nodes in ascending order.
Insert Method
The insert() method adds a new value into the tree.

javascript
Copy code
class insert {
    constructor(data) {
        let val = new Node(data, null, null);  // Create a new node

        if (this.root == null) {  // If the tree is empty, set the root to the new node
            this.root = val; 
        } else {  // Otherwise, find the correct position for the new node
            let currentVal = this.root;
            let parent;

            while (currentVal != null) {  // Traverse the tree to find the correct spot
                parent = currentVal;
                if (data < currentVal.data) {  // Go to the left if the new data is smaller
                    currentVal = currentVal.left;
                    if (currentVal == null) {  // Insert the node at the left
                        parent.left = val;
                        break;
                    }
                } else {  // Go to the right if the new data is larger
                    currentVal = currentVal.right;
                    if (currentVal == null) {  // Insert the node at the right
                        parent.right = val;
                        break;
                    }
                }
            }
        }
    }
}
Key Points:
Inserting a new node:
If the tree is empty, the new node becomes the root.
The algorithm compares the new node's value with existing nodes and traverses the tree to the left or right.
The node is inserted in the correct position based on the comparison.
In-order Traversal Method
The inOrder() function traverses the tree in ascending order (left, root, right).

javascript
Copy code
function inOrder(node) {
  if (node != null) {
    inOrder(node.left);  // Visit the left subtree
    console.log(node.show() + " ");  // Visit the root (current node)
    inOrder(node.right);  // Visit the right subtree
  }
}
Key Points:
The function is recursive:
It first traverses the left subtree.
Then it visits the current node (root).
Finally, it traverses the right subtree.
This results in the nodes being printed in ascending order.
Example Usage
Now, let's see how to use these classes and functions to create and traverse a BST.

javascript
Copy code
let nums = new BTS()

nums.insert(23); // Root node
nums.insert(16); // Left of 23
nums.insert(45); // Right of 23
nums.insert(3);  // Left of 16
nums.insert(22); // Right of 16
nums.insert(99); // Right of 45
nums.insert(40); // Left of 45

console.log("In order traversal......")
console.log(nums.root)  // Displays the root of the tree
inOrder(nums.root)  // Performs in-order traversal
Expected Output
After inserting the values and performing an in-order traversal, the output will be:

text
Copy code
3 16 22 23 40 45 99
Summary
This Binary Search Tree (BST) code provides:

A way to insert new nodes into the tree, maintaining a sorted structure.
The ability to traverse the tree in different orders, such as in-order traversal, which prints the nodes in ascending order.
Key Concepts Recap:
Binary Tree: A tree with at most two children per node.
Binary Search Tree: A binary tree where the left child is smaller and the right child is larger than the root.
In-order Traversal: Visits nodes in ascending order (left, root, right).
This basic understanding of Binary Search Trees can be applied to more advanced tree-based algorithms and data structures!
