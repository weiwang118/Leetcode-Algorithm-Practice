#### #2 Add Two Numbers
[Leetcode #2](https://leetcode.com/problems/add-two-numbers/)  

##### My Solution
```
class Solution {
public:
    ListNode* addTwoNumbers(ListNode* l1, ListNode* l2) {
        int add=0;
        ListNode *head=l1;
        while(l1!=NULL&&l2!=NULL){
                l1->val=l1->val+l2->val+add;
                if(l1->val>9){
                        add=l1->val/10;
                        l1->val=l1->val%10;
                }
                else add=0;
                if(l1->next&&l2->next){
                        l1=l1->next;
                        l2=l2->next;
                }
                else break;
        }
           if(l1->next==NULL&&l2->next==NULL){
                   if(add!=0) {l1->next=new ListNode(add);}
           }
           else if(l1->next!=NULL&&l2->next==NULL){
                while(l1->next){
                     l1=l1->next;
                        l1->val+=add;
                if(l1->val>9){
                        add=l1->val/10;
                        l1->val=l1->val%10;
                }
                else add=0;   
                }
                if(add!=0) {l1->next=new ListNode(add);}
           }
           
           else if (l1->next==NULL&&l2->next!=NULL){
                   l1->next=l2->next;
                   while(l2->next){
                           l2=l2->next;
                           l2->val+=add;
                           if(l2->val>9){
                        add=l2->val/10;
                        l2->val=l2->val%10;
                }
                else add=0;
                   }
                if(add!=0) l2->next=new ListNode(add);   
           }
           
           return head; 
    }
};
```
Time Complexity: O(max(l1.length,l2.length))  
Space Complexity: O(1)  

##### Leetcode Solution
```
class Solution {
public:
    ListNode* addTwoNumbers(ListNode* l1, ListNode* l2) {
        ListNode *head = nullptr, *tail = nullptr;
        int carry = 0;
        while (l1 || l2) {
            int n1 = l1 ? l1->val: 0;
            int n2 = l2 ? l2->val: 0;
            int sum = n1 + n2 + carry;
            if (!head) {
                head = tail = new ListNode(sum % 10);
            } else {
                tail->next = new ListNode(sum % 10);
                tail = tail->next;
            }
            carry = sum / 10;
            if (l1) {
                l1 = l1->next;
            }
            if (l2) {
                l2 = l2->next;
            }
        }
        if (carry > 0) {
            tail->next = new ListNode(carry);
        }
        return head;
    }
};
```
Time Complexity: O(max(l1.length,l2.length))  
Space Complexity: O(1)  
