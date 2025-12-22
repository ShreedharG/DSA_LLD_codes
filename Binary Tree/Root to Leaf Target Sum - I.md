https://leetcode.com/problems/path-sum/?envType=study-plan-v2&envId=top-interview-150

```
class Solution {
public:
    bool dfs(TreeNode* root, int targetSum, int sum){
        if(!root) return false;
        if(!root->left && !root->right){
            if(sum + root->val == targetSum)
                return true;
            return false;
        }
  
        return (dfs(root->left, targetSum, sum + root->val) ||
               dfs(root->right, targetSum, sum + root->val)) ;
    }

    bool hasPathSum(TreeNode* root, int targetSum) {
        return dfs(root,targetSum,0);
    }
};
```

Return -> [[Binary tree]]

