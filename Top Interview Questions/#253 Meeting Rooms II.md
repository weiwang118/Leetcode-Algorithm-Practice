#### #253 Meeting Rooms II
[Leetcode #253](https://leetcode.com/problems/meeting-rooms-ii/)  

##### Leetcode Solution
```
class Solution {
public:
    class cmp{
            public:
            bool operator()(const int &t1,const int &t2){
                    return t1>t2;
            }
    };
    int minMeetingRooms(vector<vector<int>>& intervals) {
        if(intervals.size()==0)
                return 0;
        priority_queue<int,vector<int>,cmp> queue;
        sort(intervals.begin(),intervals.end());
        queue.push(intervals[0][1]);
        for(int i=1;i<intervals.size();i++){
                if(intervals[i][0]>=queue.top())
                        queue.pop();
                
                queue.push(intervals[i][1]);
        }
            return queue.size();
        
    }
};
```
Time Complexity: O(NlogN)  
Space Complexity: O(N)  
