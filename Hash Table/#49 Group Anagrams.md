#### #49 Group Anagrams

##### My Solution
```
class Solution:
    def groupAnagrams(self, strs: List[str]) -> List[List[str]]:
        
        ans = defaultdict(list)
        
        for s in strs:
                count = [0]*26
                for c in s:
                        count[ord(c)-ord('a')] += 1
                ans[tuple(count)].append(s)
                
        return ans.values()
```
Time Complexity: O(M\*N)  
Space Complexity: O(N)  

##### Neetcode Solution
```
class Solution:
    def groupAnagrams(self, strs: List[str]) -> List[List[str]]:
        hashmap = defaultdict(list)
        for s in strs:
            # keys can be strings, bcz they are immutable.
            hashmap[str(sorted(s))].append(s) 
        return hashmap.values()
```
Time Complexity: N\*MlogM  
Space Complexity: N  

##### Notes
Remember in Python, the key of dict must be immutable which means list can not be the key.  
