## Two Pointers Fundamentals
#### Two Pointers
Two pointers technique is easy to understand which is generally used to solve problem within linear time complexity.  
**Types of Two Pointers**  
Collision - One array, move from two sides to middle.  
Forward - One array, both move forward.  
Parallel - Two arrays, each array has been assigned with a pointer.  
#### When to use the two-pointer technique?
A two-pointer isn’t the answer to every problem. To employ the two-pointer technique, the following aspects must be recognized or verified:  
**Is it necessary to sort the array before initialising the pointers?**  
For example: In the TwoSum problem, if the array was unsorted, we would be unable to determine which direction pointers should be moved.  

**Is it necessary for pointers to move at various speeds?**    
Using the fast and slow pointer techniques in the Detecting cycle in Linked List, we demonstrated how moving pointers at different speeds help us depending on the problem.  

**Is it possible to reduce a three-pointer problem to multiple two-pointer problems if managing three or more pointers is impossible or extremely difficult?**  
Yes, we can do that. Consider the problem Triplets with a Given Sum. Learn how to reduce the three-pointers problem to multiple two-pointer problems in this problem.  

**If the problem requires it, how should relationships between three or more pointers be managed?**
This would vary from problem to problem. Using the two pointer approach, we can update the pointer in any necessary way.  

**Should pointers be updated one by one or all at once?;**
Depends on the requirements of the problem.
