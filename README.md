# Binary-trees

Lecture: Introduction to Binary Search Trees (BST)
1. What is a Binary Tree?
A binary tree is a hierarchical data structure in which each node has at most two children:

Left child
Right child
In a binary search tree (BST), the following properties are maintained:

Left subtree contains nodes with values less than the root node.
Right subtree contains nodes with values greater than the root node.
Both left and right subtrees are themselves BSTs.
2. Properties of a Binary Search Tree
Each node can have 0, 1, or 2 children.
All left child nodes must be smaller than the parent node.
All right child nodes must be larger than the parent node.
This property makes searching faster because, at each step, we can decide whether to move left or right based on the value we're looking for.
3. Diagram of a Binary Search Tree
Below is a diagram that shows how a binary search tree is built step by step:

                23
               /  \
             16    45
            /  \     \
           3   22    99
In this tree:

Root node (23): The top-most node.
Left subtree: Contains 16, 3, and 22 (all smaller than 23).
Right subtree: Contains 45 and 99 (both greater than 23).
Now, let's discuss how this tree is constructed programmatically.

4. Code Explanation
Let’s go through the code you provided, line by line, to see how it builds and traverses a binary search tree.

Node Definition

function Node(data, left, right) {
    this.data = data;
    this.left = left;
    this.right = right;
    this.show = show;
}
This is the constructor function for creating a node in the tree.
data: Holds the value of the node.
left and right: These hold references to the left and right child nodes, respectively.
this.show = show: Each node has a method show() to return its data.

function show() {
    return this.data;
}
The show() function simply returns the value of the node (this.data).
Binary Search Tree (BST) Definition
javascript
Copy code
function BTS() {
    this.root = null;  // The tree starts with an empty root.
    this.insert = insert;  // Attaching the 'insert' function to add nodes.
    this.inOrder = inOrder;  // Attaching the 'inOrder' function for traversal.
}
this.root = null: Initially, the tree is empty, so the root is null.
insert function: This is used to add values to the tree.
inOrder function: This allows us to traverse the tree in a specific order.
Insert Function

function insert(data) {
    let val = new Node(data, null, null);  // Create a new node with the given data.
    
    if (this.root == null) {
        this.root = val;  // If the tree is empty, the new node becomes the root.
    } else {
        let currentVal = this.root;  // Start at the root of the tree.
        let parent;

        while (currentVal != null) {  // Traverse the tree to find the correct position.
            parent = currentVal;

            if (data < currentVal.data) {  // If data is smaller, move to the left.
                currentVal = currentVal.left;
                if (currentVal == null) {
                    parent.left = val;  // Insert the new node on the left.
                }
            } else {  // If data is larger, move to the right.
                currentVal = currentVal.right;
                if (currentVal == null) {
                    parent.right = val;  // Insert the new node on the right.
                }
            }
        }
    }
}
let val = new Node(data, null, null);: A new node is created with the given data and both its left and right child nodes set to null.
If the tree is empty (this.root == null), the new node becomes the root.
Otherwise, the function will traverse the tree starting at the root, following the rules of a BST (move left for smaller values, right for larger).
Once the correct spot is found (either the left or right child is null), the new node is inserted.
In-Order Traversal
javascript
Copy code
function inOrder(node) {
    if (node != null) {  // As long as the node exists
        inOrder(node.left);  // First, traverse the left subtree.
        console.log(node.show() + " ");  // Then, process the current node (print its value).
        inOrder(node.right);  // Finally, traverse the right subtree.
    }
}
In-order traversal follows the sequence: left subtree → current node → right subtree.
This traversal method will print the nodes in ascending order for a BST.
5. Example Execution
Let's see how the tree is built step-by-step:

Insert 23: Since the tree is empty, 23 becomes the root.
Insert 45: Since 45 > 23, it goes to the right of 23.
Insert 16: Since 16 < 23, it goes to the left of 23.
Insert 37: 37 > 23, so it moves right, but 37 < 45, so it goes left of 45.
Insert 3: 3 < 23, then 3 < 16, so it goes to the left of 16.
Insert 99: 99 > 23, then 99 > 45, so it goes to the right of 45.
Insert 22: 22 < 23, then 22 > 16, so it goes to the right of 16.
The final tree looks like this:


                23
               /  \
             16    45
            /  \     \
           3   22    99
                \
                 37
6. In-Order Traversal Output
Running inOrder(nums.root) will print the nodes in the following order:

3, 16, 22, 23, 37, 45, 99
This is the ascending order traversal of the BST.

7. Summary
Binary Search Tree (BST): A tree where the left child is smaller and the right child is greater than the parent.
Insert Function: Adds nodes to the correct location based on the BST rules.
In-Order Traversal: Visits nodes in ascending order by recursively visiting the left subtree, the current node, and then the right subtree.
I'll now create a diagram to visualize this tree traversal.



Here’s a visual representation of the binary search tree we discussed, showing how the nodes are arranged and connected. It highlights the structure of the tree and the traversal paths. You can see how nodes like 16, 3, 22, and 37 are set up on the left side of the root (23), while nodes 45 and 99 are on the right.
