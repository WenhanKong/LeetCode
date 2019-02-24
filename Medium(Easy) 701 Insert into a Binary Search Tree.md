# [Medium(?Easy) 701](https://leetcode.com/problems/insert-into-a-binary-search-tree/submissions/)

## Problem:
Given the root node of a binary search tree (BST) and a value to be inserted into the tree, insert the value into the BST.  
Return the root node of the BST after the insertion.  
It is guaranteed that the new value does not exist in the original BST.  

## Thoughts:
Just normal binary tree insertion, BST? Flip?

## Code:
```c++
/**
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
    TreeNode* insertIntoBST(TreeNode* root, int val) {
        if(!root) return new TreeNode(val);
        
        if(val<root->val){
            root->left = insertIntoBST(root->left, val);
        } else {
            root->right = insertIntoBST(root->right, val);            
        }
        return root;
    }
};
```
## Result:
Runtime: 96 ms, faster than 99.75% of C++ online submissions for Insert into a Binary Search Tree.  
Memory Usage: 33.1 MB, less than 59.91% of C++ online submissions for Insert into a Binary Search Tree.  
