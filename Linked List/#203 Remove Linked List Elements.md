#### #203 Remove Linked List Elements
[Leetcode #203](https://leetcode.com/problems/remove-linked-list-elements/)  
##### My Solution
```
class Solution {
public:
    ListNode* removeElements(ListNode* head, int val) {
            ListNode *pre=nullptr;
            ListNode *cur=head;
            while(cur){
                if(cur->val==val){
                        if(pre==nullptr){
                               head=head->next; 
                               cur=head;
                        }
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
Use DummyHead  
```
class Solution {
public:
    ListNode* removeElements(ListNode* head, int val) {
        ListNode* dummyHead=new ListNode(0,head);
        ListNode* pre=dummyHead;
        ListNode* cur=head;
        while(cur!=NULL){
                if(cur->val==val)
                        pre->next=cur->next;
                else pre=pre->next;
                cur=cur->next;
                
        }
            return dummyHead->next;
    }
};
```

##### Solution from Carl
```
//Without DummyHead
//Removing the head is a special case which need be processed specifically
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
// With DummyHead
//Removing head is not a special case anymore
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

##### Notes
Sometimes if we want to simplify the codes, we can add a dummy head to the original head so that we don't need to deal with the special situaiton of head.  
