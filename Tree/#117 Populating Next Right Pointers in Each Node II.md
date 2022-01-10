#### #117 Populating Next Right Pointers in Each Node II
[Leetcode #117](https://leetcode.com/problems/populating-next-right-pointers-in-each-node-ii/)  

##### My Solution
```
class Solution {
public:
    Node* connect(Node* root) {
        queue<Node*> que;
        if(root==NULL) return root;
        que.push(root);
        while(!que.empty()){
                int size=que.size();
                for(int i=0;i<size;i++){
                        Node*cur=que.front();
                        que.pop();
                        if(i<size-1) cur->next=que.front();
                        if(cur->left)que.push(cur->left);
                        if(cur->right)que.push(cur->right);
                }
        }
            return root;
    }
};
```

##### Solution from Carl
```
class Solution {
public:
    Node* connect(Node* root) {
        queue<Node*> que;
        if (root != NULL) que.push(root);
        while (!que.empty()) {
            int size = que.size();
            vector<int> vec;
            Node* nodePre;
            Node* node;
            for (int i = 0; i < size; i++) {
                if (i == 0) {
                    nodePre = que.front(); // 取出一层的头结点
                    que.pop();
                    node = nodePre;
                } else {
                    node = que.front();
                    que.pop();
                    nodePre->next = node; // 本层前一个节点next指向本节点
                    nodePre = nodePre->next;
                }
                if (node->left) que.push(node->left);
                if (node->right) que.push(node->right);
            }
            nodePre->next = NULL; // 本层最后一个节点指向NULL
        }
        return root;
    }
};
```
