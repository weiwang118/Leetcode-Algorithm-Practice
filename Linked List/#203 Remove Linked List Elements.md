#### #203 Remove Linked List Elements
[Leetcode #203](https://leetcode.com/problems/remove-linked-list-elements/)  
##### My Solution
```
class Solution {
public:
    ListNode* removeElements(ListNode* head, int val) {
            ListNode *pre=nullptr;
            while(head!=NULL&&head->val==val)
                    head=head->next;
            
            ListNode *cur=head;
            while(cur){
                if(cur->val==val){
                        if(cur->next==nullptr)
                        {pre->next=nullptr;cur=nullptr;}
                        else{
                                pre->next=cur->next;
                                cur=cur->next;
                        }
                }
                    else{
                     pre=cur;
                     cur=cur->next;
                    }
            }
            return head;
    }
};
```

##### Solution from Carl
```
class Solution {
public:
    ListNode* removeElements(ListNode* head, int val) {
        // 删除头结点
        while (head != NULL && head->val == val) { // 注意这里不是if
            ListNode* tmp = head;
            head = head->next;
            delete tmp;
        }

        // 删除非头结点
        ListNode* cur = head;
        while (cur != NULL && cur->next!= NULL) {
            if (cur->next->val == val) {
                ListNode* tmp = cur->next;
                cur->next = cur->next->next;
                delete tmp;
            } else {
                cur = cur->next;
            }
        }
        return head;
    }
};
```

```
class Solution {
public:
    ListNode* removeElements(ListNode* head, int val) {
        ListNode* dummyHead = new ListNode(0); // 设置一个虚拟头结点
        dummyHead->next = head; // 将虚拟头结点指向head，这样方面后面做删除操作
        ListNode* cur = dummyHead;
        while (cur->next != NULL) {
            if(cur->next->val == val) {
                ListNode* tmp = cur->next;
                cur->next = cur->next->next;
                delete tmp;
            } else {
                cur = cur->next;
            }
        }
        head = dummyHead->next;
        delete dummyHead;
        return head;
    }
};
```
