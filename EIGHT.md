# Assignment 8
## Imagine you were to take an empty binary search tree and insert the following sequence of numbers in this order: [1, 5, 9, 2, 4, 10, 6, 3, 8]. Draw a diagram showing what the binary search tree would look like. Remember, the numbers are being inserted in the order presented here. 
[View BST](https://github.com/christophervanvalkenburgh-blip/Coding-assignments-CISC-187/blob/main/BST.pdf)
## If a well-balanced binary search tree contains 1,000 values, what is the maximum number of steps it would take to search for a value within it?
A well balanced BST has a search time of log2N. So the max steps here would be log2(1000) which is 9.97 steps. 
## Write an algorithm that finds the greatest value within a binary search tree. 
```
Algorithm FindGreatest(root)
  if root is null
    return "Tree is empty"

current = root

while current.right is not null
  current = current.right

return current.data
```
## Write a code in C++ using the same array mentioned in #1 and implement a binary search tree. Only insertion operation is required.
```
#include <iostream>
using namespace std;

// Node structure
struct Node
{
    int data;
    Node* left;
    Node* right;

    // node constructor
    Node(int value)
    {
        data = value;
        left = nullptr;
        right = nullptr;
    }
};

class BST
{
private:
    Node* root;

    // recursive helper for insertion
    Node* insert(Node* node, int value)
    {
        // create a new node if empty spot found
        if (node == nullptr)
        {
            return new Node(value);
        }

        // go left for smaller value
        if (value < node->data)
        {
            node->left = insert(node->left, value);
        }
        // go right for bigger value
        else if (value > node->data)
        {
            node->right = insert(node->right, value);
        }

        // return node
        return node;
    }

    // inorder traversal to test BST
    // void inorder(Node* node)
    // {
    //     if (node != nullptr)
    //     {
    //         inorder(node->left);          // visit left subtree
    //         cout << node->data << " ";    // visit current node
    //         inorder(node->right);         // visit right subtree
    //     }
    // }


public:
    BST()
    {
        root = nullptr;
    }

    // insert values
    void insert(int value)
    {
        root = insert(root, value);
    }

    // show tree in order, to test
    //void displayInorder()
    //{
    //    inorder(root);
    //    cout << endl;
    //}
};

int main()
{
    // array values required to use from problem
    int arr[] = {1, 5, 9, 2, 4, 10, 6, 3, 8};
    int size = sizeof(arr) / sizeof(arr[0]);

    BST tree;

    // insert required values
    for (int i = 0; i < size; i++)
    {
        tree.insert(arr[i]);
    }

    // more testing
    // cout << "Inorder traversal: ";
    // tree.displayInorder();
    //
    // return 0;
}
```
