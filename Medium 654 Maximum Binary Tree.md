# [Medium 654](https://leetcode.com/problems/maximum-binary-tree/)

## Problem:

Given an integer array with no duplicates. A maximum tree building on this array is defined as follow:  
The root is the maximum number in the array.  
The left subtree is the maximum tree constructed from left part subarray divided by the maximum number.  
The right subtree is the maximum tree constructed from right part subarray divided by the maximum number.  
Construct the maximum tree by the given array and output the root node of this tree.  

## Thoughts:

+ binary tree traversal.
+ [Cartesian_tree](https://en.wikipedia.org/wiki/Cartesian_tree):  
  
  - 1. use stack keep track of back of the stack;  
  - 2. iterate array;
  - 3. **while** the stack is not empty and the item value is less/large(depending on context) than the value of back of the stack:  
          item_node->left = back_node of the stack;  
          stack.pop();
  - 4. if the stack is not empty (else stmt of c):  
          back_node->right = item_node;
  - 5. append each item to the back of the stack;  
  -   **This method keeps track of the stack to find the second largest node and place it to the right side of the largest node.
    And if find the largest node, add previous largest node to the left side of current largest node.**
  
## Code:  
``` c++
 /*
 * Definition for a binary tree node.
 * struct TreeNode {
 *     int val;
 *     TreeNode *left;
 *     TreeNode *right;
 *     TreeNode(int x) : val(x), left(NULL), right(NULL) {}
 * };
 */
class Solution {
public:
    TreeNode* constructMaximumBinaryTree(vector<int>& nums) {
        vector<TreeNode*> stack;
        
        for(auto i : nums){
            TreeNode* curr = new TreeNode(i);
            while(stack.size()&&i>stack.back()->val){
                curr->left = stack.back();
                stack.pop_back();
            }
            if(stack.size()){
                stack.back()->right = curr;
            }
            stack.push_back(curr);
        }
        return stack.front();
    }
};
```
