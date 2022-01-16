#### #347 Top K Frequent Elements
[Leetcode #347](https://leetcode.com/problems/top-k-frequent-elements/)  

##### My Solution
```
class Solution {
   bool static  cmp(pair<int,int>&a,pair<int,int>&b){
           return a.second>b.second;
   }
public:
    vector<int> topKFrequent(vector<int>& nums, int k) {
        unordered_map<int,int> map;
        for(int i=0;i<nums.size();i++)
                map[nums[i]]++;
        vector<pair<int,int>> vec(map.begin(),map.end());
        sort(vec.begin(),vec.end(),cmp);
        vector<int> ans;
        for(int i=0;i<k;i++){
                ans.push_back(vec[i].first);
        }
            return ans;
    }
};
```

##### Solution from Carl  
```
// 时间复杂度：O(nlogk)
// 空间复杂度：O(n)
class Solution {
public:
    // 小顶堆
    class mycomparison {
    public:
        bool operator()(const pair<int, int>& lhs, const pair<int, int>& rhs) {
            return lhs.second > rhs.second;
        }
    };
    vector<int> topKFrequent(vector<int>& nums, int k) {
        // 要统计元素出现频率
        unordered_map<int, int> map; // map<nums[i],对应出现的次数>
        for (int i = 0; i < nums.size(); i++) {
            map[nums[i]]++;
        }

        // 对频率排序
        // 定义一个小顶堆，大小为k
        priority_queue<pair<int, int>, vector<pair<int, int>>, mycomparison> pri_que;

        // 用固定大小为k的小顶堆，扫面所有频率的数值
        for (unordered_map<int, int>::iterator it = map.begin(); it != map.end(); it++) {
            pri_que.push(*it);
            if (pri_que.size() > k) { // 如果堆的大小大于了K，则队列弹出，保证堆的大小一直为k
                pri_que.pop();
            }
        }

        // 找出前K个高频元素，因为小顶堆先弹出的是最小的，所以倒序来输出到数组
        vector<int> result(k);
        for (int i = k - 1; i >= 0; i--) {
            result[i] = pri_que.top().first;
            pri_que.pop();
        }
        return result;

    }
};
```

##### Notes: priority queue
 A priority queue is an abstract data-type similar to a regular queue or stack data structure in which each element additionally has a "priority" associated with it. In a priority queue, an element with high priority is served before an element with low priority.  
 Define a priority queue: priority_queue<Data Type, Container//(vector/deque)//, Functional//(compare function)//>, the default setting is max-heap with vector as the container.  
 
