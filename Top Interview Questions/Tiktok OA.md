## Tiktok OA
1.[Circular Printer](https://leetcode.com/discuss/interview-question/1263982/Thomson-Reuters-or-OA-or-Circular-Printer)  
```
int main(){
    string s="ZNMD";
    int time=0;
    char pointer='A';
    for(char word:s){
        if(word==pointer) continue;
        else if(abs(word-pointer)<=13) time+=abs(word-pointer);
        else{
            time+=26-abs(word-pointer);
        }
        pointer=word;
    }
    cout<<time<<endl;
}
```

2.[Minimum Size Subarray Sum](https://leetcode.com/problems/minimum-size-subarray-sum/)  
```
class Solution {
public:
    int minSubArrayLen(int target, vector<int>& nums) {
        int len=INT32_MAX,i=0;
        int sum=0;
            for(int j=0;j<nums.size();j++){
                    sum+=nums[j];
                    while(sum>=target) {
                            len=min(len,j-i+1);
                            sum-=nums[i];
                            i++;}
            }
            if(len==INT32_MAX) return 0;
            return len;
    }
};
```

3.Dominos Tiling 3D  

![Dominos Tiling 3D](https://oss.1point3acres.cn/forum/202202/05/204551tvzz6a8o799hzk7h.png)  

4.[1507. Reformat Date](https://leetcode.com/problems/reformat-date/)  
``` 
class Solution {
public:
    string reformatDate(string date) {
        string year,month,dat;
        int loc1=date.find(' ');
        dat=date.substr(0,loc1);
        date=date.substr(loc1+1,date.size()-loc1);
        int loc2=date.find(' ');
        month=date.substr(0,loc2);
        year=date.substr(loc2+1,date.size()-loc2);
        int loc3;
        string day;
        for(char c:dat){
                if(c>='0'&&c<='9')
                        day+=c;
                else break;
        }
        string result;
        if(month=="Jan")
                month="01";
        if(month=="Feb")
                month="02";
        if(month=="Mar")
                month="03";
        if(month=="Apr")
                month="04";
         if(month=="May")
                 month="05";
         if(month=="Jun")
                 month="06";
            if(month=="Jul")
                month="07";
        if(month=="Aug")
                month="08";
        if(month=="Sep")
                month="09";
        if(month=="Oct")
                month="10";
         if(month=="Nov")
                 month="11";
         if(month=="Dec")
                 month="12";
          result=day.size()>1?year+'-'+month+'-'+day:year+'-'+month+'-'+'0'+day;
            return result;
    }
};
```
5. [Shared Interest](https://leetcode.com/discuss/interview-question/725801/amazon-shared-interest-problem)  
```
#include<bits/stdc++.h>
using namespace std;

int product(vector<int> from,vector<int> to,vector<int> w) {
    // assigning set of friend_nodes to their shared weights
    //   Wieghts      nodes
    //     1         {1,2,3}  
    //     2         {1,2}
    //     3         {2,3,4}
    map<int,set<int>> m;
    for(int i=0;i<to.size();i++)
    {
        m[w[i]].insert(from[i]);
        m[w[i]].insert(to[i]);
    }
    
    //make set of pairs for each weight 
    //   Wieghts      nodes
    //     1         (1,2),(2,3),(1,3)  
    //     2         (1,2)
    //     3         (2,3),(3,4),(2,4)
    //count no of pairs 
    //    (1,2)    2
    //    (2,3)    2
    //    (1,3)    1
    //    (3,4)    1
    //    (2,4)    1
    map<pair<int,int>,int> p;
    int max=INT_MIN;
    int max_product=INT_MIN;
    for(auto it=m.begin();it!=m.end();it++)
    {
        set<int> s=it->second;
        vector<int> v(s.begin(),s.end());
        int siz=v.size();
        for(int i=0;i<siz-1;i++)
        {
            p[make_pair(v[i],v[i+1])]++;
            if(max<p[make_pair(v[i],v[i+1])]) max=p[make_pair(v[i],v[i+1])];
        }
        if(siz>2)
        {
            p[make_pair(v[0],v[siz-1])]++;
            if(max<p[make_pair(v[0],v[siz-1])]) max=p[make_pair(v[0],v[siz-1])];
        }
    }
    //since max shared weights is 2 ,we have two pairs
    //    (1,2)    2
    //    (2,3)    2
    //  The product of first pair  (1,2) = 1*2 = 2
    //  The product of second pair (2,3) = 2*3 = 6
    // So , we return maximum product among the above two (i.e) 6
    for(auto itr=p.begin();itr!=p.end();itr++)
    {
        pair<int,int> pr=itr->first;
        if(itr->second==max)
            if(max_product<pr.first*pr.second)
                max_product=pr.first*pr.second;
    }
    return max_product;
}

int main() {
int nodes=4,edges=5;

vector<int> from =  {1, 1, 2, 2, 2};
vector<int> to =   {2, 2, 3, 3, 4};
vector<int> wt =  {1, 2, 1, 3, 3 };

cout<<product(from,to,wt);
}
```

6.[Counting Inversions](https://www.hackerrank.com/challenges/ctci-merge-sort/problem)  
```
long merge(vector<int>&arr, vector<int> &temp, int l,int mid, int r){
     long count=0;
     int i=l,j=mid,k=l;
     while(i<=mid-1&&j<=r){
         if(arr[i]<=arr[j])
             temp[k++]=arr[i++];
         else{
             temp[k++]=arr[j++];
             count+=mid-i;
         }
     }
     while(i<=mid-1)
         temp[k++]=arr[i++];
     while(j<=r)
         temp[k++]=arr[j++];
     for(int m=l;m<=r;m++)
         arr[m]=temp[m];
         
     return count;
 }
long mergeSort(vector<int>&arr, vector<int> &temp, int l,int r){
    long count=0;
    if(l<r){
        int mid=l+(r-l)/2;
        count+=mergeSort(arr, temp, l, mid);
        count+=mergeSort(arr, temp, mid+1, r);
        count+=merge(arr,temp,l,mid+1,r);
    }
    return count;
}

long countInversions(vector<int> arr) {
    vector<int> temp(arr.size(),0);
    return mergeSort(arr,temp,0,arr.size()-1);

}
```
7.[Ancestral Names](https://leetcode.com/discuss/interview-question/848711/roblox-new-grad-oa)  
```
int conDecimal(char c) {
    switch(c) {
        case 'I':
            return 1;
        case 'V':
            return 5;
        case 'X':
            return 10;
        case 'L':
            return 50;
        default:
            return 1;
    }
}

int romanInt(string s) {
    int res = conDecimal(s[0]);
    for(int i = 1; i < s.size(); i++) {
        res += conDecimal(s[i]);
        if(conDecimal(s[i - 1]) < conDecimal(s[i]))
            res -= 2 * conDecimal(s[i - 1]);
    }

    return res;
}

bool cmp(pair<string, pair<string, int>> a, pair<string, pair<string, int>> b) {
    pair<string, int> resa = a.second;
    pair<string, int> resb = b.second;
    if(resa.first == resb.first)
        return resa.second < resb.second;
    // strcmp can only be used on char array
    // compare is better choice on string
    //
    // the order you want should return true
    return resa.first.compare(resb.first) < 0;
}

int main() {
    vector<string> names = {"Steven XL", "Steven XVI", "David IX", "Mary XV", "Mary XIII", "Mary XX"};
    map<string, pair<string, int>> name_map;

    for(auto name : names) {
        for(int i = 0; i < name.size(); i++) {
            if(name[i] == ' ') {
                name_map[name] = make_pair(name.substr(0, i), romanInt(name.substr(i + 1)));
            }
        }
    }

    vector<pair<string, pair<string, int>>> sorted_names;
    for(auto it : name_map) {
        sorted_names.push_back(make_pair(it.first, it.second));
    }

    sort(sorted_names.begin(), sorted_names.end(), cmp);

    for(auto it : sorted_names) {
        cout << it.first << '\n';
    }

    return 0;
}
```
8. [Lexicographically smallest and largest substring of size k](https://www.geeksforgeeks.org/lexicographically-smallest-and-largest-substring-of-size-k/)  
```
	void getSmallestAndLargest(string s, int k)
	{
		
		// Initialize min and max as
		// first substring of size k
		string currStr = s.substr(0, k);
		string lexMin = currStr;
		string lexMax = currStr;

		// Consider all remaining substrings. We consider
		// every substring ending with index i.
		for (int i = k; i < s.length(); i++)
		{
			currStr = currStr.substr(1, k) + s[i];
			if (lexMax < currStr)	
				lexMax = currStr;
			if (lexMin >currStr)
				lexMin = currStr;	
		}

		// Print result.
		cout << (lexMin) << endl;
		cout << (lexMax) << endl;
	}

	// Driver Code
	int main()
	{
		string str = "GeeksForGeeks";
		int k = 3;
		getSmallestAndLargest(str, k);
	}
```
9. [1381. Design a Stack With Increment Operation](https://leetcode.com/problems/design-a-stack-with-increment-operation/)  
```
class CustomStack {
private:
        deque<int> stack;
        int Max=0;
        int size=0;
public:
    CustomStack(int maxSize) {
        if(size<=Max)
        Max=maxSize;
    }
    
    void push(int x) {
        if(size<Max){
                stack.push_back(x);
                size++;
        }
    }
    
    int pop() {
        if(stack.empty())
                return -1;
        int temp=stack.back();
        stack.pop_back();
        size--;
        return temp;
    }
    
    void increment(int k, int val) {
        k=size>k?k:size;
        for(int i=0;i<size;i++){
                int temp=stack.front();
                if(i<k)
                temp+=val;
                stack.pop_front();
                stack.push_back(temp);    
        }
    }
};
```

10.[780. Reaching Points](https://leetcode.com/problems/reaching-points/)  
```
class Solution {
public:
    bool reachingPoints(int sx, int sy, int tx, int ty) {
        while(tx>=sx&&ty>=sy){
                if(tx==ty) break;
                if(tx>ty){
                        if(ty>sy)tx%=ty;
                        else return (tx-sx)%ty==0;
                }
                else if(tx<ty){
                        if(tx>sx) ty%=tx;
                        else return (ty-sy)%tx==0;
                }
        }
            return (ty==sy)&&(tx==sx);
    }
};
```
11.[13. Roman to Integer](https://leetcode.com/problems/roman-to-integer/)  
```
class Solution {
public:
    int romanToInt(string s) {
        int number=0;
        for(int i=0;i<s.size();i++){
                switch(s[i]){
                case 'I': {number+=1;break;}
                case 'X': {number+=10;
                           if(i>0&&s[i-1]=='I') number-=2;break;}
                case 'C': {number+=100;
                           if(i>0&&s[i-1]=='X') number-=20;break;}
                case 'V': {number+=5;
                           if(i>0&&s[i-1]=='I') number-=2;break;}
                case 'L': {number+=50;
                           if(i>0&&s[i-1]=='X') number-=20;
                           break;}
                case 'D': {number+=500;
                           if(i>0&&s[i-1]=='C') number-=200;break;}
                case 'M': {number+=1000;
                           if(i>0&&s[i-1]=='C') number-=200;break;}
        }
        
        }
            return number;
    }
};
```

12. [Stars and Bars](https://www.chegg.com/homework-help/questions-and-answers/given-string-stars-bars-determine-number-stars-two-bars-within-substring-star-represented--q38765107)  
![Stars and Bars](https://oss.1point3acres.cn/forum/202202/05/204734l8baxhlrhgfefrdd.png)  

13. [Jump to the flag](https://www.1point3acres.com/bbs/thread-841725-1-1.html)  
```
int main(){
    int flagHeight=3;
    int bigJump=1;
    int mini_steps=0;
    for(int i=0;i<flagHeight;){
        if(i+bigJump<flagHeight)
           i= i+bigJump;
        else i++;
        mini_steps++;
    }
    cout<<mini_steps<<endl;
    }
```

14.[412. Fizz Buzz](https://leetcode.com/problems/fizz-buzz/)  
```
class Solution {
public:
    vector<string> fizzBuzz(int n) {
        vector<string> result;
            for(int i=1;i<=n;i++){
                    if(i%3==0&&i%5==0)
                            result.push_back("FizzBuzz");
                    else if(i%3==0)
                            result.push_back("Fizz");
                    else if(i%5==0)
                            result.push_back("Buzz");
                    else result.push_back(to_string(i));
            }
            return result;
    }
};
```
15. [1385. Find the Distance Value Between Two Arrays](https://leetcode.com/problems/find-the-distance-value-between-two-arrays/)  
```
class Solution {
public:
    int findTheDistanceValue(vector<int>& arr1, vector<int>& arr2, int d) {
        sort(arr2.begin(), arr2.end());
        int cnt = 0;
        for (auto &x: arr1) {
            unsigned p = lower_bound(arr2.begin(), arr2.end(), x) - arr2.begin();
            bool ok = true;
            if (p < arr2.size()) {
                ok &= (arr2[p] - x > d);
            }
            if (p - 1 >= 0 && p - 1 <= arr2.size()) {
                ok &= (x - arr2[p - 1] > d);
            }
            cnt += ok;
        }
        return cnt;
    }
};
```
16. [Count Inversions of size three in a given array](https://www.geeksforgeeks.org/count-inversions-of-size-three-in-a-give-array/)  
```
// A O(n^2) C++ program to count inversions of size 3
#include<bits/stdc++.h>
using namespace std;

// Returns count of inversions of size 3
int getInvCount(int arr[], int n)
{
	int invcount = 0; // Initialize result

	for (int i=1; i<n-1; i++)
	{
		// Count all smaller elements on right of arr[i]
		int small = 0;
		for (int j=i+1; j<n; j++)
			if (arr[i] > arr[j])
				small++;

		// Count all greater elements on left of arr[i]
		int great = 0;
		for (int j=i-1; j>=0; j--)
			if (arr[i] < arr[j])
				great++;

		// Update inversion count by adding all inversions
		// that have arr[i] as middle of three elements
		invcount += great*small;
	}

	return invcount;
}

// Driver program to test above function
int main()
{
	int arr[] = {8, 4, 2, 1};
	int n = sizeof(arr)/sizeof(arr[0]);
	cout << "Inversion Count : " << getInvCount(arr, n);
	return 0;
}
```
