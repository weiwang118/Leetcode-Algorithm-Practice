#### #19 Remove Nth Node From End of List
[Leetcode #19](https://leetcode.com/problems/remove-nth-node-from-end-of-list/)  
##### My Solution
```
class Solution {
public:
    ListNode* removeNthFromEnd(ListNode* head, int n) {
        ListNode *dummyHead=new ListNode(0,head);
        ListNode *fastIndex=dummyHead;
        ListNode *slowIndex=dummyHead;
        while(n--&&fastIndex){
                fastIndex=fastIndex->next;
        }
            fastIndex=fastIndex->next;
        while(fastIndex){
                fastIndex=fastIndex->next;
                slowIndex=slowIndex->next;
        }
        slowIndex->next=slowIndex->next->next;
        return dummyHead->next;
            
    }
};
```
* 定义fast指针和slow指针，初始值为虚拟头结点，如图：

<img src='https://code-thinking.cdn.bcebos.com/pics/19.%E5%88%A0%E9%99%A4%E9%93%BE%E8%A1%A8%E7%9A%84%E5%80%92%E6%95%B0%E7%AC%ACN%E4%B8%AA%E8%8A%82%E7%82%B9.png' width=600> </img></div>

* fast首先走n + 1步 ，为什么是n+1呢，因为只有这样同时移动的时候slow才能指向删除节点的上一个节点（方便做删除操作），如图：  
<img src='https://code-thinking.cdn.bcebos.com/pics/19.%E5%88%A0%E9%99%A4%E9%93%BE%E8%A1%A8%E7%9A%84%E5%80%92%E6%95%B0%E7%AC%ACN%E4%B8%AA%E8%8A%82%E7%82%B91.png' width=600> </img></div>

* fast和slow同时移动，直到fast指向末尾，如图：  
<img src='https://code-thinking.cdn.bcebos.com/pics/19.%E5%88%A0%E9%99%A4%E9%93%BE%E8%A1%A8%E7%9A%84%E5%80%92%E6%95%B0%E7%AC%ACN%E4%B8%AA%E8%8A%82%E7%82%B92.png' width=600> </img></div>

* 删除slow指向的下一个节点，如图：  
<img src='https://code-thinking.cdn.bcebos.com/pics/19.%E5%88%A0%E9%99%A4%E9%93%BE%E8%A1%A8%E7%9A%84%E5%80%92%E6%95%B0%E7%AC%ACN%E4%B8%AA%E8%8A%82%E7%82%B93.png' width=600> </img></div>

##### Solution from Carl
```
class Solution {
public:
    ListNode* removeNthFromEnd(ListNode* head, int n) {
        ListNode* dummyHead = new ListNode(0);
        dummyHead->next = head;
        ListNode* slow = dummyHead;
        ListNode* fast = dummyHead;
        while(n-- && fast != NULL) {
            fast = fast->next;
        }
        fast = fast->next; // fast再提前走一步，因为需要让slow指向删除节点的上一个节点
        while (fast != NULL) {
            fast = fast->next;
            slow = slow->next;
        }
        slow->next = slow->next->next;
        return dummyHead->next;
    }
};
```
