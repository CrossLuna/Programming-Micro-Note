#Programming Micro Note 20161011
##Morris traversal
Source:  
[Morris Traversal方法遍歷二叉樹](http://www.cnblogs.com/AnnieKim/archive/2013/06/15/MorrisTraversal.html)  
[Youtube - Morris Inorder Tree Traversal by Tushar Roy](https://www.youtube.com/watch?v=wGXB9OWhPTg) 

Q:   
How do you traverse a binary tree in-order non-recursively in `O(N)` time and constant space?  
A:  
Morris traversal.  
`TreeNode` is defined as
```C++
struct TreeNode {
    int val;
    TreeNode* left;
    TreeNode* right;
    TreeNode(int x): val(x), left(nullptr), right(nullptr) {}
};
```
and we define a functor `Functor visit` to visit a node.  
The code for Morris traversal  
```C++
void morrise_traversal(TreeNode* root, Functor visit) {
    TreeNode* curr = root;
    while(curr) {
        if(!curr->left) {
            visit(curr);
            curr = curr->right;
        }
        else {
            TreeNode* pred = predecessor(curr);
            if(!pred->right) {
                pred->right = curr;
                curr = curr->left;
            }
            else { // pred->right == curr
                pred->right = nullptr;
                visit(curr);
                curr = curr->right;
            }
        }
    }
} 

TreeNode* predecessor(TreeNode* curr) {
    TreeNode* pred = curr;
    pred = pred->left;   //Safe, only called when left child exists 
    while(pred->right && pred->right != curr)
        pred = pred->right;
    return pred;
}
``` 

*  Caution: when getting precedent node, remember to check if right child equals to current node. Otherwise infinite loop.
