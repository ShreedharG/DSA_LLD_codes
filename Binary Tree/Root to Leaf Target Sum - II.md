https://leetcode.com/problems/path-sum-ii/

```
class Solution {
public:
    void dfs(TreeNode* root, int targetSum,int sum, vector<int>& path, vector<vector<int>>& ans){
        if(!root) return;
        if(!root->left && !root->right){
            if(sum+root->val == targetSum){
                path.push_back(root->val);
                ans.push_back(path);
                path.pop_back();
            }
            return;
        }

        path.push_back(root->val);
        dfs(root->left, targetSum, sum + root->val, path, ans);
        path.pop_back();

        path.push_back(root->val);
        dfs(root->right, targetSum, sum + root->val, path, ans);
        path.pop_back();
    }

    vector<vector<int>> pathSum(TreeNode* root, int targetSum) {
        vector<vector<int>> ans;
        vector<int> path;
        
        if(root == nullptr) return ans;

        int sum = 0;
        dfs(root, targetSum, sum, path, ans);
        return ans;
    }
};
```

Return -> [[Binary tree]]

