https://leetcode.com/problems/top-k-frequent-elements/

```
class Solution {
public:

    vector<int> topKFrequent(vector<int>& nums, int k) {
        unordered_map<int,int> mp;
        for(int num: nums)
            mp[num]++;

        vector<vector<int>> bucket(nums.size()+1);

        for(auto& p: mp)
            bucket[p.second].push_back(p.first);

        vector<int> ans;
        for(int freq = nums.size(); freq >= 0 && ans.size() < k; freq--){
            for(auto num : bucket[freq]){
                ans.push_back(num);
                if(ans.size() == k) break;
            }
        }

        return ans;
    }
};
```

Return -> [[Arrays, Prefix-Suffix, Hashing, Maps]] , [[Sorting Algos]]

