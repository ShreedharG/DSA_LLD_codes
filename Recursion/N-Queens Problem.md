https://leetcode.com/problems/n-queens/
###### Optimal Approach
```
class Solution {
public:
    void solve(int col,vector<string> &board,vector<vector<string>> &ans,vector<int>& leftRow,vector<int>& upperDiagnol,vector<int>& lowerDiagnol,int n){
        if(col==n){
            ans.push_back(board);
            return;
        }  

        for(int row=0;row<n;row++){
            if(leftRow[row]==0 && upperDiagnol[n-1-(row-col)]==0 && lowerDiagnol[row+col]==0){
                board[row][col] = 'Q';
                leftRow[row] = 1;
                upperDiagnol[n-1-(row-col)] = 1;
                lowerDiagnol[row+col] = 1;

                solve(col+1,board,ans,leftRow,upperDiagnol,lowerDiagnol,n);

                board[row][col] = '.';
                leftRow[row] = 0;
                upperDiagnol[n-1-(row-col)] = 0;
                lowerDiagnol[row+col] = 0;
            }
        }
    }  

    vector<vector<string>> solveNQueens(int n) {
        vector<vector<string>> ans;
        string s(n ,'.');
        vector<string> board(n);
  
        vector<int> leftRow(n,0);
        vector<int> upperDiagnol(2*n-1,0);
        vector<int> lowerDiagnol(2*n-1,0);  

        for(int i=0;i<n;i++)
            board[i] = s;
            
        solve(0,board,ans,leftRow,upperDiagnol,lowerDiagnol,n);
        return ans;
    }
};
```


https://leetcode.com/problems/n-queens-ii/submissions/1845444056/
###### Return Distinct Number of Sequences
```
class Solution {
public:
    void generate(int row,int n,vector<int>& usedCol,vector<int>& uUD,vector<int>& uLD,int& count){
        if(row == n){
            count++;
            return;
        }
  
        for(int col=0;col<n;col++){
            int diag1 = n-1-(col-row);
            int diag2 = row + col;

            if(!usedCol[col] && !uUD[diag1] && !uLD[diag2]){
                usedCol[col] = 1;
                uUD[diag1] = 1;
                uLD[diag2] = 1;
                
                generate(row+1,n,usedCol,uUD,uLD,count);
  
                usedCol[col] = 0;
                uUD[diag1] = 0;
                uLD[diag2] = 0;                
            }
        }
    }
  
    int totalNQueens(int n) {        
        vector<int> usedCol(n,0);
        vector<int> usedUpperDiag(2*n-1,0);
        vector<int> usedLowerDiag(2*n-1,0);
        int count = 0;
  
        generate(0,n,usedCol,usedUpperDiag,usedLowerDiag,count);
        return count;
    }
};
```

Return -> [[Recursion + Backtracking]]