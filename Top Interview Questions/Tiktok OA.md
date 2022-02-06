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


