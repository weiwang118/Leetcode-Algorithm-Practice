#### #886 Possible Bipartition
[Leetcode #886](https://leetcode.com/problems/possible-bipartition/)  

##### Leetcode Solution
![](https://pic.leetcode-cn.com/1616218613-zwSqZw-image.png)  
```
class Solution {
public:
    bool paint(int x,int c,vector<vector<int>>& edges,vector<int>& colors){
            //Aim to paint c to the x point
            if(colors[x]==c) return true;
            // if the point x is already c, then return true;
            else if(colors[x]!=0&&colors[x]!=c) return false;
            // if the point is already painted but not color c, return false;
            // if the point is not painted, we do as follows:
            colors[x]=c;// paint the point to color c
            int reversed=(c==1?2:1);
            for(auto &e:edges[x]){
                    if(!paint(e,reversed,edges,colors))
                    {
                            colors[x]=0;// We can't paint c to the point x because other edges can't be painted the opposite color
                            return false;
                    }
            }
            return true;
    }
    bool possibleBipartition(int n, vector<vector<int>>& dislikes) {
        vector<vector<int>> Edges(n);
        for(auto pair:dislikes)
                Edges[pair[0]-1].push_back(pair[1]-1);
        vector<int> Colors(n,0);
        for(int i=0;i<n;i++){
//If the point i can't be painted in any of two colors, then it means the n people can't be splited into two groups.
                if(!paint(i,1,Edges,Colors)&&!paint(i,2,Edges,Colors))
                        return false;
        }
            return true;
    }
};
```
