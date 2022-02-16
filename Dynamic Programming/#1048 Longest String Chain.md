#### #1048 Longest String Chain
[Leetcode #1048](https://leetcode.com/problems/longest-string-chain/)  

##### Leetcode Solution
**Top-Down Dynamic Programming (Recursion + Memoization)**  
![](https://leetcode.com/problems/longest-string-chain/Figures/1048/1048_Overview_Diagram.png)
```
class Solution {
    
private:

    int dfs(unordered_set<string> &words, unordered_map<string, int> &memo, string currentWord) {
        // If the word is encountered previously we just return its value present in the map (memoization).
        if (memo.find(currentWord) != memo.end()) {
            return memo[currentWord];
        }
        // This stores the maximum length of word sequence possible with the 'currentWord' as the
        int maxLength = 1;

        // creating all possible strings taking out one character at a time from the `currentWord`
        for (int i = 0; i < currentWord.length(); i++) {
            string newWord = currentWord.substr(0, i) + currentWord.substr(i + 1);
            // If the new word formed is present in the list, we do a dfs search with this newWord.
            if (words.find(newWord) != words.end()) {
                int currentLength = 1 + dfs(words, memo, newWord);
                maxLength = max(maxLength, currentLength);
            }
        }
        memo[currentWord] = maxLength;

        return maxLength;
    }

public :
    int longestStrChain(vector<string> &words) {
        unordered_map<string, int> memo;
        unordered_set<string> wordsPresent;
        for (const string &word : words) {
            wordsPresent.insert(word);
        }
        int ans = 0;
        for (const string &word : words) {
            ans = max(ans, dfs(wordsPresent, memo, word));
        }
        return ans;
    }
};
```
Time Complexity: O(N L^2)  
Space Complexity: O(N)  
**Bottom-Up Dynamic Programming**  
```
class Solution {
public: 
    int longestStrChain(vector<string>& words) {
        unordered_map<string,int> dp;
        //sorting the list in terms of the word Length;
        sort(words.begin(),words.end(),[](string &a,string&b){return a.size()<b.size();});
        int maxLen=1;
        for(const string &word:words){
                int presentLen=1;
                //Find all possible predecessor for the current word by removing one letter at a time.
                for(int i=0;i<word.length();i++){
                        string predecessor=word.substr(0,i)+word.substr(i+1);
                        if(dp.find(predecessor)!=dp.end()){
                                int previousLen=dp[predecessor];
                                presentLen=max(presentLen,previousLen+1);
                        }
                }
                dp[word]=presentLen;
                maxLen=max(maxLen,presentLen);
        }
            return maxLen;
        
    }
};
```
Time Complexity: O(N(logN+L^2))  
Space Complexity: O(N)  
