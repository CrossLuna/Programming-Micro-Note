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


## Vector of `unique_ptr`
Source:  
[Why can I not push_back a unique_ptr into a vector?](http://stackoverflow.com/questions/3283778/why-can-i-not-push-back-a-unique-ptr-into-a-vector)

Q:  
I tried to `push_back` a `unique_ptr` to a vector, but I got compilation error.
```C++
vector<unique_ptr<int>> v;
unique_ptr<int> uptr(new int(1));
v.push_back(uptr);
```

A:  
`push_back` implies copy. `unique_ptr` guarantees ownership of only one smart pointer, therefore you can't make a copy. Instead, you should move it.
```C++
v.push_back(move(uptr));
```