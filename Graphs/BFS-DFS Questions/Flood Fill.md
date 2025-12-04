https://leetcode.com/problems/flood-fill/
###### BFS Approach
```
class Solution {
public:
	bool inBoard(int ni,int nj,int m,int n){
		return (ni>=0 && ni<m && nj>=0 && nj<n);
	}
	
    vector<vector<int>> floodFill(vector<vector<int>>& image, int sr, int sc, int color) {
        int m = image.size();
        int n = image[0].size();
  
        if(image[sr][sc] == color) return image;
  
        int o_col = image[sr][sc];
  
        vector<int> dx = {-1,1,0,0};
        vector<int> dy = {0,0,-1,1};
        queue<pair<int,int>> q;

        image[sr][sc] = color;
        q.push({sr,sc});

        while(!q.empty()){
            auto [i,j] = q.front();
            q.pop();
  
            for(int k=0;k<4;k++){
                int ni = i + dx[k];
                int nj = j + dy[k];


                if(inBoard(ni,nj,m,n) && image[ni][nj]==o_col){
                    q.push({ni,nj});
                    image[ni][nj] = color;
                }
            }
        }
        return image;
    }
};
```

Return -> [[Based on BFS-DFS Traversals]]

