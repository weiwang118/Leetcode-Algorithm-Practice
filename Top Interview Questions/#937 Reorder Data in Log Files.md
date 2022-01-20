#### #937 Reorder Data in Log Files
[Leetcode #937](https://leetcode.com/problems/reorder-data-in-log-files/)  

##### My Solution
```
class Solution {
public:
    static bool cmp(const string&s1,const string&s2){
            int i=s1.find(' ');
            int j=s2.find(' ');
            string temp1=s1.substr(i+1,s1.size()-i-1);
            string temp2=s2.substr(j+1,s2.size()-j-1);
            if(temp1==temp2)
                    return s1<s2;
            else{
                    return temp1<temp2;
            }
    }
    vector<string> reorderLogFiles(vector<string>& logs) {
            vector<string>nums;
            vector<string>texts;
            for(int i=0;i<logs.size();i++){
                    if(logs[i][logs[i].size()-1]>='0'&&logs[i][logs[i].size()-1]<='9')
                            nums.push_back(logs[i]);
                    else texts.push_back(logs[i]);
            }
            sort(texts.begin(),texts.end(),cmp);
            for(int i=0;i<nums.size();i++)
                    texts.push_back(nums[i]);
            return texts;
    }
};
```
Time Complexity: O(NlogN)  
Space Complexity: O(N)  

