https://www.naukri.com/code360/problems/graph-valid-tree_1376618?leftPanelTabValue=PROBLEM

```
bool checkgraph(vector<vector<int>> edges, int n, int m){
    DSU dsu(n);
    for(auto e: edges){
        int u = e[0], v = e[1];
        int p_u = dsu.find_parent(u), p_v = dsu.find_parent(v);

        if(p_u != p_v)
            dsu.union_(u,v);
        else
            return false;
    }
    return true;
}
```

Return -> [[MST and Disjoint Set Problems]]

