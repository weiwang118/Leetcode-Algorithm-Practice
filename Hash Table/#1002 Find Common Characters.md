#### #1002 Find Common Characters
[Leetcode #1002](https://leetcode.com/problems/find-common-characters/)  
##### My Solution
```
class Solution {
public:
    vector<string> commonChars(vector<string>& words) {
        int hash[26]={0};
        vector<string> result;
        if(words.size()==0)return result;
        for(int i=0;i<words[0].size();i++){
                hash[words[0][i]-'a']++;
        }
        int hashother[26]={0};
        for(int j=1;j<words.size();j++){
                memset(hashother, 0, 26 * sizeof(int));
                for(int i=0;i<words[j].size();i++){
                        
                        hashother[words[j][i]-'a']++;
                }
                for(int k=0;k<26;k++)
                hash[k]=min(hash[k],hashother[k]);
        }
        
        for(int k=0;k<26;k++){
                string s;
                while(hash[k]--){
                        s=k+'a';
                        result.push_back(s);
                }
        }
            return result;
    }
};
```


![1002.查找常用字符](https://code-thinking.cdn.bcebos.com/pics/1002.查找常用字符.png)

##### Solution from Carl
```
class Solution {
public:
    vector<string> commonChars(vector<string>& A) {
        vector<string> result;
        if (A.size() == 0) return result;
        int hash[26] = {0}; // 用来统计所有字符串里字符出现的最小频率
        for (int i = 0; i < A[0].size(); i++) { // 用第一个字符串给hash初始化
            hash[A[0][i] - 'a']++;
        }

        int hashOtherStr[26] = {0}; // 统计除第一个字符串外字符的出现频率
        for (int i = 1; i < A.size(); i++) {
            memset(hashOtherStr, 0, 26 * sizeof(int));
            for (int j = 0; j < A[i].size(); j++) {
                hashOtherStr[A[i][j] - 'a']++;
            }
            // 更新hash，保证hash里统计26个字符在所有字符串里出现的最小次数
            for (int k = 0; k < 26; k++) {
                hash[k] = min(hash[k], hashOtherStr[k]);
            }
        }
        // 将hash统计的字符次数，转成输出形式
        for (int i = 0; i < 26; i++) {
            while (hash[i] != 0) { // 注意这里是while，多个重复的字符
                string s(1, i + 'a'); // char -> string
                result.push_back(s);
                hash[i]--;
            }
        }

        return result;
    }
};
```
