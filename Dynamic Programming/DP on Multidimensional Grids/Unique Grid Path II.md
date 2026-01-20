https://leetcode.com/problems/unique-paths-ii/
###### Recursive
```
class Solution {
public:
    int solve(int row,int col,vector<vector<int>>& obstacleGrid){
        if(row==0 && col==0) return 1;
        if(row<0 || col<0 || obstacleGrid[row][col]==1) return 0;
        
        int up = solve(row-1,col,obstacleGrid);
        int left = solve(row,col-1,obstacleGrid);
  
        return (up+left);
    }

    int uniquePathsWithObstacles(vector<vector<int>>& obstacleGrid) {
        if(obstacleGrid[0][0]==1) return 0;
        int n = obstacleGrid.size();
        int m = obstacleGrid[0].size();
  
        return solve(n-1,m-1,obstacleGrid);
    }
};
```

###### Memoization Approach
```
class Solution {
public:
    int solve(vector<vector<int>>& og, vector<vector<int>> &dp,int i,int j){
        if(i==0 && j==0) return 1;
        if(i<0 || j<0) return 0;  
        if(dp[i][j]!=-1) return dp[i][j];
        if(og[i][j]==1) return (dp[i][j] = 0);               

        return (dp[i][j] = solve(og,dp,i-1,j) + solve(og,dp,i,j-1));
    } 

    int uniquePathsWithObstacles(vector<vector<int>>& obstacleGrid) {
        int m = obstacleGrid.size();
        int n = obstacleGrid[0].size();
        if(obstacleGrid[0][0]==1) return 0;

        vector<vector<int>> dp(m,vector<int>(n,-1));    
        return solve(obstacleGrid,dp,m-1,n-1);        
    }
};
```

###### Tabulation
```
class Solution {
public:
    int uniquePathsWithObstacles(vector<vector<int>>& obstacleGrid) {
        int m = obstacleGrid.size();
        int n = obstacleGrid[0].size();
        if(obstacleGrid[0][0]==1) return 0;

        vector<vector<int>> dp(m,vector<int>(n,0));
        
        for(int i=0;i<m;i++){
            if(obstacleGrid[i][0]) break;
            else dp[i][0] = 1;
        }

        for(int j=0;j<n;j++){
            if(obstacleGrid[0][j]) break;
            else dp[0][j] = 1;
        }

        for(int i=1;i<m;i++){
            for(int j=1;j<n;j++){
                if(obstacleGrid[i][j]==1) dp[i][j] = 0;
                else dp[i][j] = dp[i-1][j] + dp[i][j-1];
            }
        }
        return dp[m-1][n-1];
    }
};
```

Return -> [[DP on 2D,3D Grids]]