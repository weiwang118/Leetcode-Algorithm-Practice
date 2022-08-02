#### #24 Swap Nodes in Pairs
[Leetcode #24](https://leetcode.com/problems/swap-nodes-in-pairs/)  

##### My Solution
```
class Solution {
public:
    ListNode* swapPairs(ListNode* head) {
       ListNode *dummyHead=new ListNode(0,head);
       ListNode *pre=dummyHead;
       ListNode *Node1=head;
       ListNode *Node2;
       while(Node1&&Node1->next){
               Node2=Node1->next;
               Node1->next=Node2->next;
               Node2->next=Node1;
               pre->next=Node2;
               pre=Node1;
               Node1=Node1->next;
       }
            head=dummyHead->next;
            return head;
    }
};
```
Time Complexity: O(n)  
Space Complexity: O(1)

2022.08.01  
```
class Solution {
public:
    ListNode* swapPairs(ListNode* head) {
        ListNode *dummyhead = new ListNode(0,head);
        ListNode *pre = dummyhead, *cur = head;
        while(cur!= NULL && cur->next != NULL){
                ListNode *tmp = cur->next->next ;
                cur->next->next = cur;
                pre->next = cur->next;
                cur->next = tmp;
                pre = cur;
                cur = cur->next;
        }
            return dummyhead->next;
    }
};
```

##### Solution from Carl
```
class Solution {
public:
    ListNode* swapPairs(ListNode* head) {
        ListNode* dummyHead = new ListNode(0); // 设置一个虚拟头结点
        dummyHead->next = head; // 将虚拟头结点指向head，这样方面后面做删除操作
        ListNode* cur = dummyHead;
        while(cur->next != nullptr && cur->next->next != nullptr) {
            ListNode* tmp = cur->next; // 记录临时节点
            ListNode* tmp1 = cur->next->next->next; // 记录临时节点

            cur->next = cur->next->next;    // 步骤一
            cur->next->next = tmp;          // 步骤二
            cur->next->next->next = tmp1;   // 步骤三

            cur = cur->next->next; // cur移动两位，准备下一轮交换
        }
        return dummyHead->next;
    }
};
```
Time Complexity: O(n)  
Space Complexity: O(1)  
