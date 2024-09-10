Binary Search Trees (BST) - Lecture 1
What is a Binary Tree?
A binary tree is a hierarchical data structure where each node has at most two children, typically referred to as the left child and right child. The node at the top of the hierarchy is called the root.

Binary trees are useful for various tasks, such as:

Heaps - Keeping things in a specific order as you add them.
Tries - Efficiently storing words for quick lookups.
HTML Trees - Representing HTML structure in a tree form, where each HTML tag is a node.
Here’s an HTML tree as an example:

HTML

<div>
  /     \
<h1>    <p>
Types of Tree Traversal
Tree traversal is the process of visiting each node in a specific order. There are three common traversal methods:

In-order Traversal: This gives you the nodes in ascending order: left, root, right.
Post-order Traversal: Here, you visit the nodes in the order: left, right, root. It's commonly used to delete a tree from the leaves to the root.
Pre-order Traversal: This visits nodes in the order: root, left, right. It's often used to create a copy of a tree.
Example of a Binary Search Tree (BST)
Let's consider the following values that need to be added to a tree:

[23, 16, 45, 3, 22, 99, 40]
We can represent this in a tree structure:

                       23
                    /      \
                 16          45
               /   \       /    \
             3      22   40      99
Code Breakdown
Now, let's break down the provided code step by step to understand how the Binary Search Tree (BST) is built and traversed.

1. Node Class
This class defines the structure of a node, the building block of a binary tree.

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
show(): This method returns the data when called.
2. Show Function
This function simply returns the data value from the node.

function show() {
  return this.data;
}
3. BTS (Binary Tree Structure) Class
This class represents the entire binary search tree.

class BTS {
    constructor() {
        this.root = null;  // The root node of the tree
        this.insert = insert;  // Method to insert data into the tree
        this.inOrder = inOrder;  // Method for in-order traversal
    }
}
root: Initially, the root is set to null (the tree is empty).
insert(): This method inserts new nodes into the tree.
inOrder(): This method performs an in-order traversal to display nodes in ascending order.
4. Insert Method
The insert() method adds a new value to the tree in the correct position.

class insert {
    constructor(data) {
        let val = new Node(data, null, null);  // Create a new node

        if (this.root == null) {  // If the tree is empty, set the root to the new node
            this.root = val; 
        } else {  // Otherwise, find the correct position
            let currentVal = this.root;
            let parent;

            while (currentVal != null) {  // Traverse the tree to find the spot
                parent = currentVal;
                if (data < currentVal.data) {  // Go to the left if the new data is smaller
                    currentVal = currentVal.left;
                    if (currentVal == null) {  // Insert the node when an empty spot is found
                        parent.left = val;
                        break;
                    }
                } else {  // Otherwise, go to the right
                    currentVal = currentVal.right;
                    if (currentVal == null) {  // Insert the node when an empty spot is found
                        parent.right = val;
                        break;
                    }
                }
            }
        }
    }
}
This method works by:

Creating a new node with the given data.
If the tree is empty, the new node becomes the root.
If not, it traverses the tree:
If the data is less than the current node, it moves to the left.
If the data is greater, it moves to the right.
Once a null pointer (an empty child) is found, it inserts the new node.
5. In-order Traversal
The inOrder() function recursively visits nodes in ascending order: left, root, right.

function inOrder(node) {
  if (node != null) {
    inOrder(node.left);  // Visit the left subtree
    console.log(node.show() + " ");  // Visit the root (current node)
    inOrder(node.right);  // Visit the right subtree
  }
}
This function ensures that:

It recursively goes down the left subtree first.
Then it prints the root (current node).
Finally, it traverses the right subtree.
6. Using the Code
Now, let’s see how to use the classes and functions.

let nums = new BTS()

nums.insert(23); // Root node
nums.insert(16); // Inserted to the left of 23
nums.insert(45); // Inserted to the right of 23
nums.insert(3);  // Inserted to the left of 16
nums.insert(22); // Inserted to the right of 16
nums.insert(99); // Inserted to the right of 45
nums.insert(40); // Inserted to the left of 45

console.log("In order traversal......")
console.log(nums.root)
inOrder(nums.root)  // Perform an in-order traversal
What happens here:
Inserting values: The insert() method inserts the values into the correct positions in the tree.
In-order Traversal: The inOrder() function prints the values in ascending order: 3, 16, 22, 23, 40, 45, 99.

The code defines a Binary Search Tree (BST) that allows for adding nodes and performing in-order traversal. The BST structure helps maintain the data in a way that supports fast lookups, inserts, and ordered traversal.

Key Takeaways:
BST Properties: Left child is always smaller, right child is always larger.
Insert: Adds nodes in the correct position based on value comparison.
In-order Traversal: Prints nodes in ascending order.
