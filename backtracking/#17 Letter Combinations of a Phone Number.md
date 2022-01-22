#### #17 Letter Combinations of a Phone Number
[Leetcode #17](https://leetcode.com/problems/letter-combinations-of-a-phone-number/)  

##### My Solution
```
class Solution {
public:
    vector<string> result;
    void backtracking(string digits,string str,int startIndex,vector<string> map){
            int index=digits[startIndex]-48;
            if(digits.empty())return;
            if(str.size()==digits.size()){
                    result.push_back(str);
                    return;
            }
            for(int i=0;;i++){
                    str.push_back(map[index][i]);
                    backtracking(digits,str,startIndex+1,map);
                    str.pop_back();
                    if(!map[index][i+1])break;
            }
    }
        
    vector<string> letterCombinations(string digits) {
        vector<string> map(10,"0");
        map[2]="abc";map[3]="def";map[4]="ghi";map[5]="jkl";map[6]="mno";map[7]="pqrs";map[8]="tuv";map[9]="wxyz";
        backtracking(digits,"",0,map);
        return result;
    }
};
```

##### Solution from Carl
```
// 版本一
class Solution {
private:
    const string letterMap[10] = {
        "", // 0
        "", // 1
        "abc", // 2
        "def", // 3
        "ghi", // 4
        "jkl", // 5
        "mno", // 6
        "pqrs", // 7
        "tuv", // 8
        "wxyz", // 9
    };
public:
    vector<string> result;
    string s;
    void backtracking(const string& digits, int index) {
        if (index == digits.size()) {
            result.push_back(s);
            return;
        }
        int digit = digits[index] - '0';        // 将index指向的数字转为int
        string letters = letterMap[digit];      // 取数字对应的字符集
        for (int i = 0; i < letters.size(); i++) {
            s.push_back(letters[i]);            // 处理
            backtracking(digits, index + 1);    // 递归，注意index+1，一下层要处理下一个数字了
            s.pop_back();                       // 回溯
        }
    }
    vector<string> letterCombinations(string digits) {
        s.clear();
        result.clear();
        if (digits.size() == 0) {
            return result;
        }
        backtracking(digits, 0);
        return result;
    }
};
```
