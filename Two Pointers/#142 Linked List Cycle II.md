#### #142 Linked List Cycle II
[Leetcode #142](https://leetcode.com/problems/linked-list-cycle-ii/)  

##### 101 Solution

```
ListNode *detectCycle(ListNode *head) {
ListNode *slow = head, *fast = head;
// 判断是否存在环路
do {
if (!fast || !fast->next) return nullptr;
fast = fast->next->next;
slow = slow->next;
} while (fast != slow);
// 如果存在，查找环路节点
fast = head;
while (fast != slow){
slow = slow->next;
fast = fast->next;
}
return fast;
}
```
Time Complexity: O(N)  
Space Complexity: O(1)  
