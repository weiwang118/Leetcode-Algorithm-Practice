#### #151 Reverse Words in a String
[Leetcode #151](https://leetcode.com/problems/reverse-words-in-a-string/)  

##### My Solution
```
class Solution {
public:
    void removeSpace(string &s){
        int fastIndex=0,slowIndex=0;
            //remove space in the front;
        while(s.size()>0&&fastIndex<s.size()&&s[fastIndex]==' ')
                fastIndex++;
            //remove space in the middle;
        for(;fastIndex<s.size();fastIndex++){
                if(fastIndex>1&&s[fastIndex-1]==s[fastIndex]&&s[fastIndex]==' ')
                        continue;
                else s[slowIndex++]=s[fastIndex];
        }
            //remove space in the back;
       if(slowIndex-1>0&&s[slowIndex-1]==' ') 
               s.resize(slowIndex-1);
            else s.resize(slowIndex);
    }
        
    string reverseWords(string s) {
        removeSpace(s);
        reverse(s.begin(),s.end());
        int j=0;
        for(int i=0;i<s.size();i++){
                if(s[i]==' '){
                        reverse(&s[j],&s[i]);
                        j=i+1;
                }
        }
            reverse(&s[j],&s[s.size()]);
            return s;
            
    }
};
```

##### Solution from Carl
```
// 版本一
class Solution {
public:
    // 反转字符串s中左闭又闭的区间[start, end]
    void reverse(string& s, int start, int end) {
        for (int i = start, j = end; i < j; i++, j--) {
            swap(s[i], s[j]);
        }
    }

    // 移除冗余空格：使用双指针（快慢指针法）O(n)的算法
    void removeExtraSpaces(string& s) {
        int slowIndex = 0, fastIndex = 0; // 定义快指针，慢指针
        // 去掉字符串前面的空格
        while (s.size() > 0 && fastIndex < s.size() && s[fastIndex] == ' ') {
            fastIndex++;
        }
        for (; fastIndex < s.size(); fastIndex++) {
            // 去掉字符串中间部分的冗余空格
            if (fastIndex - 1 > 0
                    && s[fastIndex - 1] == s[fastIndex]
                    && s[fastIndex] == ' ') {
                continue;
            } else {
                s[slowIndex++] = s[fastIndex];
            }
        }
        if (slowIndex - 1 > 0 && s[slowIndex - 1] == ' ') { // 去掉字符串末尾的空格
            s.resize(slowIndex - 1);
        } else {
            s.resize(slowIndex); // 重新设置字符串大小
        }
    }

    string reverseWords(string s) {
        removeExtraSpaces(s); // 去掉冗余空格
        reverse(s, 0, s.size() - 1); // 将字符串全部反转
        int start = 0; // 反转的单词在字符串里起始位置
        int end = 0; // 反转的单词在字符串里终止位置
        bool entry = false; // 标记枚举字符串的过程中是否已经进入了单词区间
        for (int i = 0; i < s.size(); i++) { // 开始反转单词
            if (!entry) {
                start = i; // 确定单词起始位置
                entry = true; // 进入单词区间
            }
            // 单词后面有空格的情况，空格就是分词符
            if (entry && s[i] == ' ' && s[i - 1] != ' ') {
                end = i - 1; // 确定单词终止位置
                entry = false; // 结束单词区间
                reverse(s, start, end);
            }
            // 最后一个结尾单词之后没有空格的情况
            if (entry && (i == (s.size() - 1)) && s[i] != ' ' ) {
                end = i;// 确定单词终止位置
                entry = false; // 结束单词区间
                reverse(s, start, end);
            }
        }
        return s;
    }
    
    // 当然这里的主函数reverseWords写的有一些冗余的，可以精简一些，精简之后的主函数为：
    /* 主函数简单写法
    string reverseWords(string s) {
        removeExtraSpaces(s);
        reverse(s, 0, s.size() - 1);
        for(int i = 0; i < s.size(); i++) {
            int j = i;
            // 查找单词间的空格，翻转单词
            while(j < s.size() && s[j] != ' ') j++;
            reverse(s, i, j - 1);
            i = j;
        }
        return s;
    }
    */
};
```
