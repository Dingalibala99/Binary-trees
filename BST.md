# Binary Search Trees (BST) - Lecture
What is a Binary Tree?
A binary tree is a hierarchical data structure where each node has at most two children:

Left Child: Contains smaller values.
Right Child: Contains larger values.
Binary trees have many real-world applications, such as:

Heaps: Keeping data ordered as it is added.
Tries: Storing words efficiently for quick lookups.
HTML Trees: Representing the structure of an HTML document.
Example of an HTML Tree

~~~
   <div>
  /     \
<h1>    <p>
~~~

Types of Tree Traversal
Tree traversal refers to visiting each node in a specific order. The three main types of traversal are:

- In-order Traversal: Visits the left subtree, then the root, then the right subtree. This gives the nodes in ascending order.
- Post-order Traversal: Visits the left subtree, then the right subtree, and finally the root. This is often used to delete a tree.
- Pre-order Traversal: Visits the root first, followed by the left and right subtrees. This is used to create a copy of a tree.

Binary Search Tree (BST) Example
Consider the following values to be inserted into a tree:

[23, 16, 45, 3, 22, 99, 40]
These values can be represented in a binary search tree like this:


                       23
                    /      \
                 16          45
               /   \       /    \
             3      22   40      99
             
Code Explanation
We will now break down the code step by step to understand how the Binary Search Tree (BST) is built and traversed.

Node Class
The Node class defines the structure of a node in the binary tree.

~~~
class Node {
    constructor(data, left, right) {
        this.data = data;  // The value stored in the node
        this.left = left;  // Pointer to the left child
        this.right = right;  // Pointer to the right child
        this.show = show;  // Method to display node's data
    }
}
~~~

data: The value inside the node (e.g., 23, 16).
left: Pointer to the left child (nodes with smaller values).
right: Pointer to the right child (nodes with larger values).
show(): Returns the node's data when called.
Show Function
This function is used to return the data stored in a node.

~~~
function show() {
  return this.data;
}
~~~

BTS (Binary Tree Structure) Class
This class represents the entire binary search tree.

~~~
class BTS {
    constructor() {
        this.root = null;  // The root node of the tree
        this.insert = insert;  // Method to insert data into the tree
        this.inOrder = inOrder;  // Method for in-order traversal
    }
}
~~~

root: Initially set to null, meaning the tree is empty.
insert(): Method to add nodes to the tree.
inOrder(): Method to perform in-order traversal and print the nodes in ascending order.
Insert Method
The insert() method adds a new value into the tree.

~~~
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
~~~

Key Points:
Inserting a new node:
If the tree is empty, the new node becomes the root.
The algorithm compares the new node's value with existing nodes and traverses the tree to the left or right.
The node is inserted in the correct position based on the comparison.
In-order Traversal Method
The inOrder() function traverses the tree in ascending order (left, root, right).

~~~
function inOrder(node) {
  if (node != null) {
    inOrder(node.left);  // Visit the left subtree
    console.log(node.show() + " ");  // Visit the root (current node)
    inOrder(node.right);  // Visit the right subtree
  }
}
~~~

Key Points:
The function is recursive:
It first traverses the left subtree.
Then it visits the current node (root).
Finally, it traverses the right subtree.
This results in the nodes being printed in ascending order.
Example Usage
Now, let's see how to use these classes and functions to create and traverse a BST.

~~~
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
~~~

Expected Output
After inserting the values and performing an in-order traversal, the output will be:

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


The main focal points (key criteria) to validate whether a binary tree is a valid Binary Search Tree (BST) are centered around its structural properties and the relationships between nodes. Here's what you need to check:

1. BST Property (Order Property)
At the core of a valid BST is the binary search tree property:

For every node:
All nodes in the left subtree have values less than the node's value.
All nodes in the right subtree have values greater than the node's value.
This property must hold recursively for every node in the tree.
2. Binary Tree Structure
The tree must be a binary tree, meaning:
Each node has at most two children: a left child and a right child.
The tree is composed of nodes connected by edges, forming a hierarchical structure without cycles.
3. In-Order Traversal Produces Sorted Sequence
In-order traversal of a valid BST should yield nodes in ascending order (if duplicates are not allowed) or non-decreasing order (if duplicates are allowed).
This means:
Visiting the left subtree, then the node itself, then the right subtree should produce a sorted list of values.
4. No Violations in Subtrees
Subtree Validation:

Not only should the immediate left and right children satisfy the BST property relative to their parent, but all descendants in the left subtree must be less than the node, and all descendants in the right subtree must be greater.
Example of Violation:

      10
     /  \
    5    15
        /
       6  <-- Violation: 6 is less than 10 but is in the right subtree of 10
In this example, even though 6 is a left child of 15, it's less than 10, violating the BST property.
5. Handling Duplicate Values
Consistency:
If duplicates are allowed, they must be handled consistently throughout the tree.
Common Rules:
Left-Leaning: All duplicates go to the left subtree.
Right-Leaning: All duplicates go to the right subtree.
Comparison Adjustments:
Use < and ≥, or ≤ and > operators consistently based on how duplicates are handled.
6. Range Constraints (Min/Max Values)
Each Node's Value Must Be Within a Valid Range:
Left Child:
Must be less than the current node's value.
Must be greater than the minimum allowed value for that subtree.
Right Child:
Must be greater than the current node's value.
Must be less than the maximum allowed value for that subtree.
Recursive Checks:
These constraints must be applied recursively to all nodes in the tree.
Methods to Validate a BST
To ensure that a binary tree is a valid BST, you can implement the following validation methods:

Method 1: In-Order Traversal Check
Perform an In-Order Traversal:
Traverse the tree in-order and collect the node values in a list or compare them on the fly.
Check for Sorted Order:
Ensure that each value is greater than (or equal to, if duplicates are allowed) the previous value.
Validation:
If the sequence is not sorted, the tree is not a valid BST.
Limitations:

This method doesn't handle all cases, especially when the BST property is violated in deeper subtrees.
Method 2: Recursive Min/Max Validation
Define a Recursive Function:
The function checks whether each node's value is within the allowed range.
Initialize with Infinite Bounds:
Start with min = -Infinity and max = Infinity.
Update Bounds While Traversing:
For the left child:
max = parent node's value
For the right child:
min = parent node's value
Check Node's Value Against Bounds:
If a node's value is not within min < value < max, it's invalid.
Recursive Call:
Recursively validate the left and right subtrees with updated bounds.
Example Code:

function isValidBST(node, min = -Infinity, max = Infinity) {
  if (node == null) return true;
  
  if (node.data <= min || node.data >= max) {
    return false;  // Violation found
  }
  
  // Recursively validate left and right subtrees
  return isValidBST(node.left, min, node.data) &&
         isValidBST(node.right, node.data, max);
}
Edge Cases to Consider
Empty Tree:
An empty tree (null root) is considered a valid BST.
Single Node Tree:
A tree with a single node is always a valid BST.
Duplicate Values:
Ensure your validation logic aligns with how duplicates are handled in your BST implementation.
Practical Steps to Validate a BST
Start at the Root:
Begin validation from the root node with initial bounds (min = -Infinity, max = Infinity).
Traverse the Tree:
Use recursive traversal to visit all nodes.
Apply the BST Property at Each Node:
Check if left child < current node < right child.
Ensure all nodes in the left subtree are less than the current node.
Ensure all nodes in the right subtree are greater than the current node.
Update Bounds Appropriately:
When moving to the left child, the max bound becomes the current node's value.
When moving to the right child, the min bound becomes the current node's value.
Return Validation Result:
If any node violates the BST property, the function should return false.
If all nodes satisfy the property, the tree is a valid BST.
Summary
To validate if a binary tree is a valid Binary Search Tree, focus on these main points:

BST Property:

Every node's left subtree contains values less than the node's value.
Every node's right subtree contains values greater than the node's value.
This must hold true for every node in the tree.
In-Order Traversal Produces Sorted Order:

An in-order traversal should yield a sequence of values in ascending order.
Consistent Handling of Duplicates:

If duplicates are allowed, they must be placed and compared consistently throughout the tree.
No Violations in Subtrees:

Ensure that there are no violations deeper in the tree, not just at immediate children.
By carefully checking these properties, you can confirm whether a binary tree maintains the integrity required of a Binary Search Tree.

Remember: Validating a BST is crucial for ensuring that operations like search, insert, and delete can be performed efficiently, maintaining the performance guarantees that make BSTs valuable data structures in computer science and software engineering.


  inOrder(node) {
        if (node != null) {
            this.inOrder(node.left);
            console.log(node.show() + " ");
            this.inOrder(node.right);
        }
    }

i want a break down of this recursive function call. how does it order them from smallest to biggest

The inOrder function you provided is an example of in-order traversal for a binary search tree (BST). In-order traversal is a type of depth-first search that visits the nodes of a tree in a specific order: left subtree → node → right subtree.

In the case of a Binary Search Tree (BST), performing an in-order traversal will visit the nodes in ascending order (from smallest to largest). This happens because the structure of the tree ensures that all values in the left subtree are smaller than the current node, and all values in the right subtree are larger.

Let's break down the recursive function step by step.

inOrder(node) {
    if (node != null) { // Check if the current node exists
        this.inOrder(node.left);  // Recursively traverse the left subtree
        console.log(node.show() + " ");  // Process the current node (print its value)
        this.inOrder(node.right);  // Recursively traverse the right subtree
    }
}
Breakdown:
Base Case: if (node != null)

This is the base case of the recursion. It ensures that we stop the recursion when we reach a null node (i.e., a leaf node's child, which doesn't exist).
If node == null, we do nothing and return to the previous call. This prevents the function from attempting to process non-existent nodes.
Step 1: this.inOrder(node.left)

This recursive call traverses the left subtree of the current node.
Since, in a binary search tree, the left child is always smaller than the current node, the function first processes all the smaller values.
In-Order Traversal Rule: Always visit the left subtree before processing the current node.
Example:

If the current node has a value of 23, the inOrder(node.left) will be called first, taking us to the left child (for example, node 16), and this pattern will continue until we reach the leftmost node in the subtree (the smallest node).
Step 2: console.log(node.show() + " ")

After recursively visiting all the nodes in the left subtree, the function processes the current node.
Here, node.show() is called to print the data (value) of the current node.
At this point, we know all nodes in the left subtree (which are smaller) have already been processed, so we print the current node's value in the correct order.
Step 3: this.inOrder(node.right)

After processing the current node, the function now recursively traverses the right subtree.
Since the right subtree contains values larger than the current node, this step ensures that we visit all the larger values after processing the current node.
How Does It Order from Smallest to Largest?
This happens because of the recursive nature of in-order traversal and the structure of the BST:

Left Subtree: The recursive call this.inOrder(node.left) ensures that the left subtree (with smaller values) is visited first. This means that when we finally print the current node's value, we have already printed all the smaller values in the left subtree.

Current Node: After the left subtree is fully processed, we print the current node's value, ensuring that it comes after all smaller values but before any larger values.

Right Subtree: Finally, the recursive call this.inOrder(node.right) ensures that all larger values in the right subtree are processed after the current node.

Recursive Call Stack Flow:
Let's walk through the function's behavior with an example tree:


            23
          /    \
        16      45
       /  \    /   \
      3   22  40   99
We call inOrder(root), where root is the node with value 23.

We first go left to 16 (inOrder(16)).
At 16, we again go left to 3 (inOrder(3)).

3 has no left child, so the left subtree traversal returns immediately (inOrder(null) does nothing).
We print 3.
3 has no right child, so the right subtree traversal also returns immediately.
We return to 16, print 16, and then go right to 22 (inOrder(22)).

22 has no left child, so we print 22.
22 has no right child, so we return back to 23.
We print 23, and now go right to 45 (inOrder(45)).

At 45, we first go left to 40 (inOrder(40)).

40 has no left child, so we print 40.
40 has no right child, so we return back to 45.
We print 45 and then go right to 99 (inOrder(99)).

99 has no left child, so we print 99.
99 has no right child, so we are done.
Final Order of Printed Values:

3 16 22 23 40 45 99
This is the sorted order of the node values in the BST, achieved by visiting nodes in the sequence: left subtree → node → right subtree.

Summary of the Recursive Process:
Recursive left subtree traversal ensures that smaller values are processed first.
Processing the current node happens after the left subtree has been processed.
Recursive right subtree traversal ensures that larger values are processed after the current node, which results in values being printed in ascending order for a BST.
This combination of steps guarantees that the function visits and processes the nodes in increasing order, from the smallest (leftmost) node to the largest (rightmost) node.

# Advantages and Uses of Binary Search Trees (BST)

A **Binary Search Tree (BST)** is a versatile data structure widely used in tech companies to solve real-world problems that involve quick data access, manipulation, and efficient searching. Below are some key uses and advantages of BST:

## 1. Efficient Searching and Sorting

**Problem**: Tech companies often need to search through large datasets quickly, such as databases of users, products, or transactions.

**Solution**: BST allows for efficient searching, insertion, and deletion of elements in **O(log n)** time (in a balanced tree). This makes it a powerful tool for handling large data sets in applications where fast access is critical.

---

## 2. Database Indexing

**Problem**: Database systems require efficient methods for data retrieval.

**Solution**: Binary Search Trees, especially **self-balancing variants** like AVL or Red-Black Trees, are used for indexing data to enable fast retrieval, insertion, and deletion of records. For instance, searching for a user by name or ID in a database can be efficiently handled by a BST.

---

## 3. Autocomplete and Spell Check

**Problem**: When users type into a search bar, companies provide real-time suggestions or spelling corrections.

**Solution**: A BST can be used to store words in a structured manner. For example, a **Trie** (a specialized tree) can efficiently find words with common prefixes, enabling search engine autocomplete and spell check features.

---

## 4. File Systems and Directories

**Problem**: File systems need to manage directories and files hierarchically for quick access.

**Solution**: Trees, particularly binary search trees, are used in file systems (like Unix file systems) to manage the hierarchical structure of directories, allowing for fast file access and organization.

---

## 5. Priority Queues

**Problem**: Many systems require handling tasks with different priorities, such as process scheduling or load balancing.

**Solution**: A specialized tree like a **Heap** (which can be implemented using a binary tree) is used to efficiently manage priority queues, ensuring the highest-priority task is processed first.

---

## 6. Network Routing Algorithms

**Problem**: Efficient routing of network traffic requires algorithms to find the shortest paths.

**Solution**: Trees, including Binary Search Trees, are key in algorithms like **Dijkstra’s Algorithm**, which finds the shortest path between nodes in a network. This is critical for **Internet routing** and other network applications.

---

## 7. Memory Management

**Problem**: Operating systems and applications need efficient memory management to avoid fragmentation and optimize performance.

**Solution**: BSTs are used in **memory allocators** to track free memory blocks. This enables quick searching for the best-fit or first-fit memory blocks, improving memory allocation performance.

---

## 8. Data Compression (Huffman Coding)

**Problem**: Large files need to be compressed for efficient storage or transmission.

**Solution**: **Huffman Coding**, a lossless data compression algorithm, uses binary trees to assign variable-length codes to input characters. This algorithm is widely used in data compression formats like JPEG and MP3.

---

## 9. Geographical Data (GIS)

**Problem**: Applications like Google Maps need to search spatial data efficiently (e.g., finding locations, routes, etc.).

**Solution**: BST variants like **K-D Trees** (a multi-dimensional BST) are used to organize and search geographical data, helping in finding nearby places or optimal routes in mapping software.

---

## 10. Version Control Systems (Git)

**Problem**: Companies need tools to track and manage changes in software projects.

**Solution**: Trees, especially **Merkle Trees** (a type of hash tree), are used in **Git** for efficiently managing and verifying versions of files in a project, enabling version control systems to work effectively.

---

## 11. Machine Learning (Decision Trees)

**Problem**: Machine learning models need efficient methods for classifying data.

**Solution**: **Decision Trees**, which are structured similarly to binary trees, are used for classification and regression tasks. These trees help make real-time predictions and decisions in fields such as fraud detection, recommendation engines, and more.

---

## Conclusion

Binary Search Trees (BST) and their variants play an essential role in numerous applications, from improving search efficiency to powering machine learning models. Their versatility and efficiency make them invaluable in solving complex problems in tech companies.
