#### #819 Most Common Word
[Leetcode #819](https://leetcode.com/problems/most-common-word/)  

##### Solution in discussion board
```
class Solution {
public:
    string mostCommonWord(string paragraph, vector<string>& banned) {
     paragraph+=' ';
     string temp="";
     unordered_map<string,int> map;
     set<string> ban(banned.begin(),banned.end());
     for(char ch:paragraph){
             if(!isalpha(ch)){
                     //check if the char is alpha letter. 
                     if(!temp.empty()){
                             map[temp]++;
                             temp.clear();
                     }
             }
             else temp+=tolower(ch);
             //convert to lowercase letter.
     }
            vector<string>words;
            for(auto p:map)
                    words.push_back(p.first);
            sort(words.begin(),words.end(),[&](string&s,string&t){return map[s]>map[t];});
            if(banned.empty())
                    return words[0];
            for(auto w:words){
                    if(ban.find(w)==ban.end())
                            return w;
            }
        
           return "";
    }
};
```
Space Complexity: O(M+N)  
