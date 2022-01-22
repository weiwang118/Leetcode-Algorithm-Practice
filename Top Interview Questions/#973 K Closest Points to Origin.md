#### #973 K Closest Points to Origin
[Leetcode #973](https://leetcode.com/problems/k-closest-points-to-origin/)  

##### My Solution
```
class Solution {
public:
    vector<vector<int>> kClosest(vector<vector<int>>& points, int k) {
        vector<vector<int>> distance(points.size());
        int j=0;
        for(int i=0;i<points.size();i++){
         distance[j].push_back(points[i][0]*points[i][0]+points[i][1]*points[i][1]);
                distance[j++].push_back(i);
        }
            sort(distance.begin(),distance.end());
            for(int i=0;i<k;i++){
                    distance[i][0]=points[distance[i][1]][0];
                    distance[i][1]=points[distance[i][1]][1];
            }
            distance.resize(k);
            return distance;
    }
};
```
Time Complexity: O(nlogn)  
Space Complexity: O(n)  

##### Sort with Custom Comparator
```
class Solution {
public:
    static bool cmp(vector<int> &dot1,vector<int>dot2){
            return dot1[0]*dot1[0]+dot1[1]*dot1[1] < dot2[0]*dot2[0]+dot2[1]*dot2[1];
    }
    vector<vector<int>> kClosest(vector<vector<int>>& points, int k) {
            sort(points.begin(),points.end(),cmp);
            points.resize(k);
            return points;
    }
};
```
Time Complexity: O(nlogn)  
Space Complexity: O(logn)  

##### Max Heap with priority queue  
```
class Solution {
public:
    vector<vector<int>> kClosest(vector<vector<int>>& points, int k) {
            //The priority_que defaults to be the max heap;
         priority_queue<pair<int,int>> maxPQ;
            for(int i=0;i<points.size();i++){
                 pair<int,int> entry={points[i][0]*points[i][0]+points[i][1]*points[i][1],i};
                    if(maxPQ.size()<k){
                            maxPQ.push(entry);
                    }
                    else if(entry.first<maxPQ.top().first){
                            maxPQ.pop();
                            maxPQ.push(entry);
                    }
            }
            vector<vector<int>> answer;
            while(!maxPQ.empty()){
                    answer.push_back(points[maxPQ.top().second]);
                    maxPQ.pop();
            }
            return answer;
    }
};
```
Time Complexity: O(Nlogk)  
Sapce Complexity: O(k)  



