#### #160 Intersection of Two Linked Lists
[Leetcode 160](https://leetcode.com/problems/intersection-of-two-linked-lists/)  
##### My Solution
```
class Solution {
public:
    ListNode *getIntersectionNode(ListNode *headA, ListNode *headB) {
        ListNode *fastIndexA=headA;
        ListNode *fastIndexB=headB;
        ListNode *slowIndexA=headA;
        ListNode *slowIndexB=headB;
        while(fastIndexA&&fastIndexB){
                fastIndexA=fastIndexA->next;
                fastIndexB=fastIndexB->next;
        }
        if(fastIndexA!=nullptr)
        {
                while(fastIndexA){
                        fastIndexA=fastIndexA->next;
                        slowIndexA=slowIndexA->next;
                }
        }
        if(fastIndexB!=nullptr)
        {
                while(fastIndexB){
                        fastIndexB=fastIndexB->next;
                        slowIndexB=slowIndexB->next;
                }
        }
        // The distances between slowIndex and fastIndex of A and B are equal, which means slowIndexA and slowIndexB have the same distance to the end of each List.
        while(slowIndexA&&slowIndexB){
                if(slowIndexA==slowIndexB) return slowIndexA;
                slowIndexA=slowIndexA->next;
                slowIndexB=slowIndexB->next;
        }
            return NULL;
    }
};
```

##### Solution from Carl
```
class Solution {
public:
    ListNode *getIntersectionNode(ListNode *headA, ListNode *headB) {
        ListNode* curA = headA;
        ListNode* curB = headB;
        int lenA = 0, lenB = 0;
        while (curA != NULL) { // 求链表A的长度
            lenA++;
            curA = curA->next;
        }
        while (curB != NULL) { // 求链表B的长度
            lenB++;
            curB = curB->next;
        }
        curA = headA;
        curB = headB;
        // 让curA为最长链表的头，lenA为其长度
        if (lenB > lenA) {
            swap (lenA, lenB);
            swap (curA, curB);
        }
        // 求长度差
        int gap = lenA - lenB;
        // 让curA和curB在同一起点上（末尾位置对齐）
        while (gap--) {
            curA = curA->next;
        }
        // 遍历curA 和 curB，遇到相同则直接返回
        while (curA != NULL) {
            if (curA == curB) {
                return curA;
            }
            curA = curA->next;
            curB = curB->next;
        }
        return NULL;
    }
};
```
